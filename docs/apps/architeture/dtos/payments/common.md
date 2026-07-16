# Common Types

> Define os tipos compartilhados utilizados pela Capability **Payments**.

---

## Objetivo

Este documento centraliza todos os **tipos reutilizáveis** da Capability **Payments**.

Nenhum Resource deverá redefinir enums ou estruturas presentes neste documento. Sempre que um DTO necessitar de um tipo compartilhado, ele deverá **referenciar este documento**.

---

## Filosofia

A Capability **Payments** deve possuir uma **linguagem única**.

Conceitos como moeda, status, método de pagamento, cliente, endereço e valores monetários deverão ser representados **sempre da mesma maneira**.

> Essa padronização reduz duplicação, facilita a manutenção e garante consistência entre todos os Resources.

---

## Tipos Compartilhados

### Money

Representa qualquer **valor monetário** utilizado pela plataforma.

```typescript
Money {
    value: decimal
    currency: Currency
}
```

| Campo | Obrigatório | Descrição |
|-------|:-----------:|-----------|
| `value` | ✅ | Valor monetário |
| `currency` | ✅ | Código ISO-4217 |

---

### Currency

Representa a moeda utilizada na operação. Sempre deverá utilizar o padrão **ISO-4217**.

```
BRL, USD, EUR, GBP, JPY, ARS, MXN
```

---

### PaymentStatus

Estado atual de um **pagamento**.

| Status | Descrição |
|--------|-----------|
| `PENDING` | Aguardando processamento |
| `PROCESSING` | Em processamento |
| `AUTHORIZED` | Autorizado |
| `APPROVED` | Aprovado |
| `PARTIALLY_PAID` | Parcialmente pago |
| `REFUNDED` | Reembolsado |
| `PARTIALLY_REFUNDED` | Parcialmente reembolsado |
| `FAILED` | Falhou |
| `CANCELED` | Cancelado |
| `EXPIRED` | Expirado |

> Todos os Providers deverão converter seus estados para um destes valores.

---

### PaymentMethod

Método utilizado para realizar um **pagamento**.

| Método | Descrição |
|--------|-----------|
| `PIX` | Pagamento instantâneo brasileiro |
| `CREDIT_CARD` | Cartão de crédito |
| `DEBIT_CARD` | Cartão de débito |
| `BOLETO` | Boleto bancário |
| `BANK_TRANSFER` | Transferência bancária |
| `DIGITAL_WALLET` | Carteira digital |
| `CASH` | Dinheiro |
| `OTHER` | Outro |

> Nenhum método específico de um Provider deverá ser exposto para a Dialyn.

---

### CustomerReference

Representa uma referência **simplificada** de um cliente.

```typescript
CustomerReference {
    id: string
    name: string
}
```

> Este modelo deverá ser utilizado quando apenas uma referência ao cliente for necessária.

---

### Address

Representa um **endereço** padronizado.

```typescript
Address {
    street: string
    number: string
    complement: string
    district: string
    city: string
    state: string
    postalCode: string
    country: string
}
```

> Este tipo poderá ser utilizado por Customer, Invoice e demais Resources.

---

### Metadata

Representa informações **adicionais não padronizadas**.

```typescript
Metadata {
    values: object
}
```

> Cada Engine poderá preencher este objeto com informações específicas do Provider, desde que não sejam utilizadas como contrato oficial da Dialyn.

---

### Pagination

Representa informações de **paginação**.

```typescript
Pagination {
    page: integer
    limit: integer
    total: integer
    pages: integer
}
```

> Deverá ser reutilizado por **todos os DTOs de listagem**.

---

### DateRange

Representa um **intervalo de datas**.

```typescript
DateRange {
    start: datetime
    end: datetime
}
```

> Utilizado em consultas e filtros.

---

### Error

Representa um erro **padronizado** da Capability.

```typescript
Error {
    code: string
    message: string
    details: object
}
```

> Os Engines deverão converter erros específicos dos Providers para este formato.

---

### ValidationError

Representa um erro de **validação**.

```typescript
ValidationError {
    field: string
    message: string
}
```

---

## Convenções

| # | Regra |
|---|-------|
| 1 | 🔄 **Reutilizáveis** entre Resources |
| 2 | 🔗 **Independentes** de Providers |
| 3 | 🔖 **Versionáveis** |
| 4 | 📦 **Serializáveis** |
| 5 | 🧩 **Compatíveis** entre diferentes Engines |

> ⚠️ Nenhum tipo compartilhado deverá conter informações específicas de uma integração.

---

## Utilização

Os Resources da Capability **Payments** deverão reutilizar estes tipos sempre que possível.

| Resource | Tipos Utilizados | Documentação |
|----------|------------------|--------------|
| **Payment** | `Money`, `PaymentStatus`, `PaymentMethod`, `CustomerReference`, `Metadata` | [payment.md](./payment.md) |
| **Invoice** | `Money`, `Currency`, `CustomerReference`, `Address`, `Metadata` | [invoice.md](./invoice.md) |
| **Refund** | `Money`, `Currency`, `CustomerReference`, `Metadata` | [refund.md](./refund.md) |
| **Customer** | `Address`, `Metadata` | [customer.md](./customer.md) |

---

## Evolução

Novos tipos compartilhados poderão ser adicionados neste documento conforme a Capability **Payments** evoluir.

> A criação de tipos duplicados em Resources deverá ser **evitada** sempre que existir um modelo compartilhado adequado.
