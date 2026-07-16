# Arquitetura de Comunicação

> Dialyn, Engines e aplicações de terceiros.

---

## Objetivo

Este documento define a **arquitetura** utilizada para comunicação entre a Dialyn, seus Engines e aplicações de terceiros.

O objetivo é **desacoplar completamente a IA das APIs externas**, permitindo que novos provedores sejam adicionados sem alterar o comportamento dos agentes.

---

## Filosofia da Arquitetura

A Dialyn **nunca** conversa diretamente com APIs externas. Ela se comunica exclusivamente com **Engines especializados**, responsáveis por conhecer as regras de negócio, autenticação e particularidades de cada provedor.

```mermaid
flowchart LR
    A[Agente IA] --> B[Engine da Dialyn]
    B --> C[Engine Especializado]
    C --> D[API Externa]
```

> O agente **nunca** sabe qual provedor está sendo utilizado. Ele apenas solicita uma ação.

**Exemplo:** O agente solicita `Criar cobrança PIX` — o Engine responsável decide qual provedor utilizar de acordo com a configuração da conta.

---

## Organização dos Engines

Os Engines são divididos por **domínio de negócio**.

| Engine | Responsabilidade | Apps |
|--------|-----------------|------|
| 💳 **Payments Engine** | Integrações financeiras | Stripe, Mercado Pago, Asaas |
| 📅 **Productivity Engine** | Integrações de produtividade | Google Calendar, Trello, Notion |
| 👥 **CRM Engine** | Integrações de CRM | Salesforce, HubSpot |
| 🛒 **Ecommerce Engine** | Integrações de e-commerce | Shopify, WooCommerce, Hotmart |

> Novos Engines poderão ser adicionados futuramente **sem necessidade de alterar a arquitetura** da Dialyn.

---

## Modelo de Comunicação

A comunicação ocorre em **diferentes camadas**.

### Dialyn → Engine

| Tecnologia | Motivos |
|------------|---------|
| **gRPC** | Baixa latência, comunicação tipada, contratos bem definidos, suporte a streaming, excelente desempenho entre microsserviços, escalabilidade |

> A Dialyn atua apenas como **orquestradora**.

### Engine → APIs Externas

| Tecnologia | Descrição |
|------------|-----------|
| **REST API** | Padrão utilizado pela maioria dos provedores |

**Provedores que utilizam REST:** Google Calendar, Stripe, Mercado Pago, Asaas, Shopify, Salesforce, Notion, Hotmart, Trello, Typeform.

---

## Comunicação Síncrona

A comunicação **síncrona** será utilizada sempre que o usuário precisar de uma resposta imediata.

```mermaid
sequenceDiagram
    participant C as Cliente
    participant A as Agente
    participant D as Dialyn
    participant E as Payments Engine
    participant MP as Mercado Pago

    C->>A: Solicita PIX
    A->>D: Criar cobrança PIX
    D->>E: Execute(CreatePix)
    E->>MP: Chama API
    MP-->>E: QRCode PIX
    E-->>D: Resposta processada
    D-->>A: QRCode PIX
    A-->>C: Envia QRCode
```

| Exemplos de uso | Descrição |
|-----------------|-----------|
| 💰 Criar PIX | Pagamento instantâneo |
| 📄 Gerar boleto | Cobrança bancária |
| 🔗 Criar Link de Pagamento | Link de cobrança |
| 📅 Consultar agenda | Verificar disponibilidade |
| ➕ Criar evento no Google Calendar | Agendamento |
| 🃏 Criar cartão no Trello | Nova tarefa |
| 👤 Criar Lead no Salesforce | Novo prospect |

---

## Comunicação Assíncrona

A comunicação **assíncrona** ocorre quando um sistema externo notifica a Dialyn sobre uma alteração. O fluxo é iniciado pelo próprio provedor.

### Mercado Pago

```mermaid
sequenceDiagram
    participant MP as Mercado Pago
    participant E as Payments Engine
    participant D as Dialyn
    participant A as Agente

    MP->>E: Webhook (pagamento recebido)
    E->>E: Converte para evento interno
    E->>D: Evento Interno
    D->>A: Novo contexto disponível
```

### Google Calendar

```mermaid
sequenceDiagram
    participant GC as Google Calendar
    participant E as Productivity Engine
    participant D as Dialyn

    GC->>E: Webhook (evento alterado)
    E->>E: Converte para evento interno
    E->>D: Evento Interno
```

### Typeform

```mermaid
sequenceDiagram
    participant TF as Typeform
    participant E as Engine
    participant D as Dialyn

    TF->>E: Webhook (nova resposta)
    E->>E: Converte para evento interno
    E->>D: Evento Interno
```

### Shopify

```mermaid
sequenceDiagram
    participant S as Shopify
    participant E as Engine
    participant D as Dialyn

    S->>E: Webhook (pedido criado)
    E->>E: Converte para evento interno
    E->>D: Evento Interno
```

---

## Política de Webhooks

| Prioridade | Mecanismo | Quando usar |
|------------|-----------|-------------|
| ✅ **Preferencial** | Webhooks | Quando o provedor oferecer suporte |
| ❌ **Exceção** | Polling | Apenas quando Webhooks não estiverem disponíveis |

> Esta regra aplica-se a **todos os Engines** da plataforma.

---

## Recebimento de Webhooks

Os Webhooks **nunca** deverão ser recebidos diretamente pela Dialyn. Sempre deverão passar pelo **Engine responsável**.

### ✅ Correto

```mermaid
flowchart LR
    A[Mercado Pago] --> B[Payments Engine]
    B --> C[Dialyn]
```

### ❌ Incorreto

```mermaid
flowchart LR
    A[Mercado Pago] --> B[Dialyn]
```

> A Dialyn **não** deve conhecer detalhes de nenhum provedor externo. Essa responsabilidade pertence **exclusivamente ao Engine**.

---

## Padronização de Eventos

Cada provedor possui sua própria nomenclatura para eventos. Os Engines deverão **converter** todos esses eventos para um padrão interno.

| Provedor | Evento Original | Evento Interno |
|----------|-----------------|----------------|
| Mercado Pago | `payment.updated` | `PaymentReceived` |
| Stripe | `invoice.payment_succeeded` | `PaymentReceived` |
| Asaas | `PAYMENT_RECEIVED` | `PaymentReceived` |
| Google Calendar | `calendar.updated` | `CalendarUpdated` |
| Shopify | `order.created` | `OrderCreated` |

> Os agentes sempre trabalharão **apenas com os eventos internos** da Dialyn.

---

## Contrato entre Dialyn e Engines

Todo Engine deverá implementar **obrigatoriamente** as seguintes operações:

| Método | Objetivo |
|--------|----------|
| `Connect()` | Conectar uma conta |
| `Disconnect()` | Remover uma conexão |
| `Execute()` | Executar uma ação |
| `HandleWebhook()` | Processar eventos externos |
| `Query()` | Consultar informações do App  |


> Este contrato deverá permanecer **igual para todos os Engines**. Consulte a documentação de [capabilities](https://github.com/guicarvalho274/dialyn/master/docs/apps/architeture/capabilities/README.md) para entender melhor.

---

## Execução de Ações

Cada Engine será responsável por disponibilizar suas próprias **Actions**.

| Engine | Exemplo de Action |
|--------|-------------------|
| 📅 Google Calendar | `Execute(CreateEvent)` |
| 💳 Stripe | `Execute(CreatePix)` |
| 📝 Notion | `Execute(CreatePage)` |
| 👥 Salesforce | `Execute(CreateLead)` |

> Embora as ações sejam diferentes, o **contrato permanece exatamente o mesmo**.

---

## Resumo da Arquitetura

| Comunicação | Tecnologia | Objetivo |
|-------------|------------|----------|
| 🧠 Agente → Dialyn | Comunicação interna | Orquestração da IA |
| 🔗 Dialyn → Engines | **gRPC** | Comunicação rápida e tipada |
| 🌐 Engines → APIs Externas | **REST API** | Integração com provedores |
| 🔔 APIs Externas → Engines | **Webhooks** | Eventos em tempo real |
| 📡 Engines → Dialyn | **Eventos Internos** | Padronização dos provedores |
| ⏱️ Polling | **Exceção** | Apenas quando Webhooks não existirem |

---

## Benefícios da Arquitetura

| # | Benefício |
|---|-----------|
| 1 | 🧠 A IA **nunca** conhece APIs externas |
| 2 | 🏗️ Cada domínio possui seu próprio **Engine especializado** |
| 3 | ➕ Novos provedores podem ser adicionados **sem alterar os agentes** |
| 4 | 🔄 Eventos são **padronizados** independentemente do provedor |
| 5 | 📋 Toda comunicação segue **contratos únicos e bem definidos** |
| 6 | 📈 A arquitetura é **escalável** e preparada para microsserviços |

Consulta a documentação de ciclos de um app [app-life-cycle](app-lifecycle.md)
