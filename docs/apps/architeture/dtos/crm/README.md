# CRM Capability

> Capability responsável por padronizar integrações com plataformas de **Customer Relationship Management (CRM)**.

---

## Objetivo

A Capability **CRM** define o modelo canônico utilizado pela Dialyn para representar informações relacionadas ao gerenciamento de clientes, oportunidades de negócio e organizações.

Seu objetivo é abstrair as diferenças entre provedores de CRM, permitindo que Agentes e Engines interajam através de um único contrato de dados.

> Independentemente do Provider utilizado, todas as operações deverão utilizar os Resources definidos nesta Capability.

---

## Filosofia

Cada plataforma de CRM possui sua própria estrutura de dados e nomenclatura.

| Provider | Conceitos Base |
|----------|----------------|
| ☁️ Salesforce | Lead, Contact, Account, Opportunity |
| 🟠 HubSpot | Contact, Company, Deal |
| 🔵 Pipedrive | Lead, Person, Organization, Deal |
| 🟢 Zoho CRM | Lead, Contact, Account, Deal |
| 🟣 RD Station CRM | Lead, Contact, Company, Deal |
| ✅ **Dialyn** | **Lead, Contact, Company, Deal** |

> Apesar das diferenças de implementação, todas compartilham conceitos fundamentais. O CRM Engine é responsável por converter esses modelos para os contratos definidos pela Dialyn.

---

## Arquitetura

```
crm/
├── README.md
├── common.md
├── relationships.md
├── glossary.md
├── lead.md
├── contact.md
├── company.md
└── deal.md
```

---

## Resources

| Resource | Objetivo |
|----------|----------|
| **Lead** | Representa um potencial cliente ainda em fase de qualificação |
| **Contact** | Representa uma pessoa conhecida pela organização |
| **Company** | Representa uma empresa ou organização |
| **Deal** | Representa uma oportunidade de negócio em andamento |

> Cada Resource possui seu próprio contrato canônico, regras de negócio e DTOs.

---

## Tipos Compartilhados

Os tipos reutilizados entre os Resources encontram-se em [common.md](./common.md).

| Tipo | Descrição |
|------|-----------|
| `Address` | Endereço |
| `Phone` | Telefone |
| `Email` | E-mail |
| `Metadata` | Dados adicionais |
| `OwnerReference` | Referência ao responsável |
| `CompanyReference` | Referência à empresa |
| `ContactReference` | Referência ao contato |

---

## Operações

Todos os Resources deverão implementar o conjunto de operações definido pela Arquitetura da Dialyn.

| Categoria | Operações |
|-----------|-----------|
| ⚡ **Core** | `List`, `Get`, `Create`, `Update`, `Delete` |
| 🔧 **Extended** | `Search`, `Count`, `Exists`, `Archive`, `Restore`, `Merge`, `Assign` |
| 🔄 **System** | `Connect`, `Disconnect`, `Refresh`, `HealthCheck`, `HandleWebhook` |

---

## Compatibilidade

Esta Capability foi projetada para suportar provedores como:

- Salesforce
- HubSpot
- Pipedrive
- Zoho CRM
- RD Station CRM

> Novos Providers deverão reutilizar os mesmos contratos definidos nesta documentação.

---

## Princípios

| # | Princípio | Descrição |
|---|-----------|-----------|
| 1 | 🔗 **Independência** | De qualquer plataforma de CRM |
| 2 | 🔄 **Estabilidade** | Contratos estáveis e versionados |
| 3 | 🧩 **Baixo acoplamento** | Resources independentes entre si |
| 4 | 📖 **Reutilização** | Tipos compartilhados entre Resources |
| 5 | 🚫 **Isolamento** | Conversão realizada exclusivamente pelo CRM Engine |

---

## Benefícios

| # | Benefício |
|---|-----------|
| 1 | 🔗 **Desacoplamento** completo entre a Dialyn e plataformas de CRM |
| 2 | 🏗️ **Padronização** da comunicação entre CRM Engines |
| 3 | ➕ **Simplificação** da integração de novos CRMs |
| 4 | 📉 **Redução da complexidade** ao unificar o modelo de dados |
| 5 | 🚀 **Facilidade** para evolução sem impacto na IA |

---

## Organização da Documentação

```
README.md
├── common.md
├── relationships.md
├── glossary.md
├── lead.md
├── contact.md
├── company.md
└── deal.md
```

Cada Resource define:
- Modelo Canônico
- Campos
- Regras de Negócio
- Operações
- DTOs
- Responsabilidades do CRM Engine

---

## Veja também

| Documento | Objetivo |
|-----------|----------|
| [common.md](./common.md) | Tipos compartilhados da Capability |
| [relationships.md](./relationships.md) | Relacionamentos entre Resources |
| [glossary.md](./glossary.md) | Conceitos e terminologias |
| [lead.md](./lead.md) | Potenciais clientes |
| [contact.md](./contact.md) | Contatos |
| [company.md](./company.md) | Empresas |
| [deal.md](./deal.md) | Oportunidades de negócio |
