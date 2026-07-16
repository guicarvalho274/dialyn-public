# Common Types

> Tipos compartilhados utilizados pelos Resources da Capability **CRM**.

---

## Objetivo

Este documento define os tipos reutilizáveis da Capability **CRM**.

Seu objetivo é evitar duplicação de estruturas entre Resources como **Lead**, **Contact**, **Company** e **Deal**, mantendo um modelo canônico consistente para toda a arquitetura da Dialyn.

> Sempre que um mesmo conceito for utilizado por mais de um Resource, ele deverá ser definido neste documento.

---

## Filosofia

Os tipos definidos neste documento representam conceitos compartilhados entre diferentes Resources.

Eles não pertencem a um Provider específico e também não devem conter regras de negócio.

> Sua responsabilidade é padronizar a comunicação entre a Dialyn e os CRM Engines.

---

## Address

Representa um endereço.

```typescript
Address {
    street: string
    number: string
    complement: string
    district: string
    city: string
    state: string
    country: string
    zipCode: string
}
```

---

## Email

Representa um endereço de e-mail.

```typescript
Email {
    address: string
    verified: boolean
}
```

---

## Phone

Representa um telefone.

```typescript
Phone {
    countryCode: string
    areaCode: string
    number: string
    type: PhoneType
}
```

---

## Metadata

Representa informações específicas do Provider que não fazem parte do modelo canônico.

```typescript
Metadata {
    values: map<string, any>
}
```

---

## OwnerReference

Representa o responsável por um Resource dentro do CRM.

```typescript
OwnerReference {
    id: string
    name: string
}
```

---

## CompanyReference

Representa uma empresa.

```typescript
CompanyReference {
    id: string
    name: string
}
```

---

## ContactReference

Representa um contato.

```typescript
ContactReference {
    id: string
    name: string
}
```

---

## LeadReference

Representa um Lead.

```typescript
LeadReference {
    id: string
    name: string
}
```

---

## DealReference

Representa uma oportunidade de negócio.

```typescript
DealReference {
    id: string
    title: string
}
```
```typescript
PipelineReference {
    id: string
    name: string
}
```

```typescript
StageReference {
    id: string
    name: string
}
```
---

## Enumerations

### LeadStatus

```
NEW
QUALIFIED
CONTACTED
CONVERTED
LOST
```

### DealStatus

```
OPEN
WON
LOST
CANCELED
```

### ContactType

```
PERSON
ORGANIZATION
```

### CompanySize

```
MICRO
SMALL
MEDIUM
LARGE
ENTERPRISE
```

### PhoneType

```
MOBILE
HOME
WORK
OTHER
```

---

## Utilização

Os Resources da Capability **CRM** deverão reutilizar estes tipos sempre que possível.

| Resource | Tipos Utilizados |
|----------|------------------|
| **Lead** | `Address`, `Email`, `Phone`, `OwnerReference`, `Metadata` |
| **Contact** | `Address`, `Email`, `Phone`, `CompanyReference`, `Metadata` |
| **Company** | `Address`, `Metadata` |
| **Deal** | `CompanyReference`, `ContactReference`, `OwnerReference`, `Money`, `Metadata` |

---

## Convenções

| # | Regra |
|---|-------|
| 1 | Reutilizar os tipos definidos neste documento |
| 2 | Evitar estruturas duplicadas |
| 3 | Utilizar `Reference` para relacionamentos entre Resources |
| 4 | Armazenar informações específicas do Provider em `Metadata` |

---

## Evolução

> Novos tipos compartilhados poderão ser adicionados neste documento conforme a Capability **CRM** evoluir.

A criação de tipos duplicados em Resources deverá ser evitada sempre que existir um modelo compartilhado adequado.

---

## Princípios

| # | Princípio | Descrição |
|---|-----------|-----------|
| 1 | 🔗 **Independência** | De qualquer plataforma de CRM |
| 2 | 🔄 **Reutilização** | Dos mesmos tipos entre diferentes Resources |
| 3 | 🧩 **Consistência** | Estruturas padronizadas em toda a Capability |
| 4 | 📖 **Documentação** | Tipos documentados de forma consistente |
| 5 | 🚫 **Isolamento** | Sem dependência de estruturas específicas de providers |

---

## Benefícios

| # | Benefício |
|---|-----------|
| 1 | 🔗 **Desacoplamento** entre tipos Dialyn e estruturas de provedores |
| 2 | 🏗️ **Padronização** da representação de dados na Capability |
| 3 | ➕ **Simplificação** da criação de novos Resources |
| 4 | 📉 **Redução de duplicação** de tipos entre documentos |
| 5 | 🚀 **Facilidade** para evolução sem impacto na IA |

---

## Veja também

| Documento | Objetivo |
|-----------|----------|
| [README.md](./README.md) | Visão geral da Capability |
| [glossary.md](./glossary.md) | Conceitos da Capability |
| [relationships.md](./relationships.md) | Relacionamentos entre Resources |
