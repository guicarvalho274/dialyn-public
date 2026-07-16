# Stripe

> Integração financeira utilizada pela Dialyn para automatizar cobranças, pagamentos e operações financeiras em escala global através de agentes de IA.

---

## Objetivo

A Stripe é utilizada pela Dialyn para permitir que agentes inteligentes realizem operações financeiras em mais de um país, com suporte a pagamentos internacionais, múltiplas moedas e diversos métodos de pagamento.

> O agente pode vender para clientes do mundo inteiro sem conhecer detalhes técnicos sobre gateways de pagamento.

---

## Resumo

| Característica | Descrição |
|---------------|-----------|
| 🎯 **Foco** | Empresas com operação global |
| 💳 **Recursos** | Cartão, link de pagamento, assinaturas |
| 🌎 **Alcance** | Internacional (dezenas de moedas) |
| 🔁 **Recorrência** | Assinaturas e pagamentos recorrentes |
| 🔄 **Reembolso** | Suporte completo |
| 🤖 **Integração** | Payments Capability da Dialyn |

---

## Problemas que resolve

### Vendas internacionais

| Sem Dialyn | Com Dialyn |
|------------|-----------|
| Cliente internacional solicita compra | Cliente internacional conversa com agente |
| Processo manual de cobrança | Payments Capability processa |
| Confirmação manual | Stripe processa o pagamento |
| Risco de erro em moeda estrangeira | Pagamento internacional concluído |

> O agente realiza vendas para clientes em diferentes países da mesma forma que vendas nacionais.

---

## Casos de uso

### Cobranças internacionais

Cliente: *"I'd like to purchase your subscription."*

O agente cria a cobrança, gera o link de pagamento, aceita a moeda local do cliente e conclui a venda durante a conversa.

```mermaid
flowchart LR
    C[Cliente internacional] --> A[Agente Dialyn]
    A --> P[Payments Capability]
    P --> S[Stripe]
    S --> R[Pagamento em moeda local]
```

---

### Assinaturas

A Stripe possui um dos ecossistemas mais completos para pagamentos recorrentes.

| Exemplos | O agente pode |
|----------|---------------|
| SaaS, streaming, cursos online, clubes | Criar, consultar, cancelar assinaturas e atualizar métodos de pagamento |

---

### Consulta de pagamentos

O agente responde perguntas como:

- *"Meu pagamento foi aprovado?"*
- *"Minha assinatura está ativa?"*
- *"Qual o status da cobrança?"*

---

### Confirmação automática

```mermaid
flowchart LR
    S[Stripe] --> WH[Webhook]
    WH --> PE[Payments Engine]
    PE --> D[Dialyn]
    D --> A[Agente]
```

Após a confirmação, o agente pode automaticamente:

- liberar acesso
- iniciar onboarding
- criar pedidos
- atualizar CRM
- enviar mensagens

---

### Reembolsos

Cliente: *"Gostaria de cancelar minha compra."*

O agente inicia todo o fluxo de devolução sem intervenção manual.

---

## Público recomendado

| Perfil | Exemplos |
|--------|----------|
| 🌐 **SaaS internacionais** | Plataformas digitais globais |
| 🛒 **Marketplaces globais** | Empresas com clientes em múltiplos países |
| 💱 **Múltiplas moedas** | Negócios que operam com diferentes moedas |
| 📚 **Infoprodutores internacionais** | Cursos e conteúdos para o exterior |

---

## Capacidades utilizadas

| Capability | Resources |
|-----------|-----------|
| **Payments** | `Payment` · `Customer` · `Invoice` · `Refund` |

---

## Actions disponibilizadas

| Categoria | Ações |
|-----------|-------|
| Pagamentos | Criar, consultar, atualizar, cancelar |
| Clientes | Criar, consultar, atualizar |
| Cobranças | Criar, consultar, listar |
| Reembolsos | Criar, consultar |

---

## Princípios

| # | Princípio | Descrição |
|---|-----------|-----------|
| 1 | 🌎 **Escala global** | Pagamentos em dezenas de moedas e países |
| 2 | 🔗 **Independência** | A Dialyn não depende da Stripe — ela é um Provider |
| 3 | 🔄 **Automação** | Cobranças, assinaturas e reembolsos sem intervenção manual |
| 4 | 📖 **Confiabilidade** | Infraestrutura robusta para operações críticas |

---

## Benefícios

| # | Benefício |
|---|-----------|
| 1 | 🌎 **Alcance global** sem necessidade de múltiplas integrações |
| 2 | ⚡ **Agilidade** em vendas internacionais |
| 3 | 🤖 **Redução** de processos operacionais da equipe |
| 4 | 🔁 **Automação** de assinaturas e recorrência |
| 5 | 📉 **Menos atrito** com clientes de diferentes países |

---

## Quando não usar

Embora poderosa para operações globais, em alguns cenários um Provider regional pode ser mais adequado:

- empresas que operam exclusivamente no Brasil
- negócios que dependem de funcionalidades específicas do mercado brasileiro
- operações locais sem necessidade de pagamentos internacionais

> Para esses casos, o Payments Engine oferece Providers como Asaas e Mercado Pago.

---

## Papel na arquitetura

A Stripe não define as capacidades da plataforma — ela **implementa** a Capability **Payments**.

```mermaid
flowchart LR
    A[Agente] --> ACT[Action: Criar pagamento]
    ACT --> CAP[Payments Capability]
    CAP --> CMD[Payment.Create]
    CMD --> PE[Payments Engine]
    PE --> S[Stripe]
```

> Toda a lógica permanece desacoplada do Provider, permitindo que a Dialyn evolua sem alterar o comportamento dos agentes.

---

## Veja também

| Documento | Objetivo |
|-----------|----------|
| [README.md](./README.md) | Visão geral da integração |
| [Asaas](../asaas/provider.md) | Provider Brasil |
| [Mercado Pago](../mercado-pago/provider.md) | Provider América Latina |
