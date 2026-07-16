# Common Types

> Tipos compartilhados utilizados por todos os Resources da Capability **Commerce**.

---

## Objetivo

Este documento define os tipos reutilizáveis da Capability **Commerce**.

Seu objetivo é evitar duplicação de estruturas entre os Resources, garantindo consistência na representação de produtos, pedidos, clientes e estoque.

> Sempre que possível, os Resources deverão reutilizar os tipos definidos neste documento.

---

## Filosofia

Todos os Providers possuem estruturas próprias.

| Provider | Estrutura |
|----------|-----------|
| 🛒 Shopify | `ProductVariant` |
| 🏪 WooCommerce | `Product` |
| 🎓 Hotmart | Produtos digitais |
| ✅ **Dialyn** | **Tipos canônicos compartilhados** |

> Independentemente dessas diferenças, todos os Engines deverão converter seus modelos para os tipos compartilhados definidos pela Dialyn.

---

## Money

Representa um valor monetário.

```typescript
Money {
    value: decimal
    currency: Currency
}
```

---

## Currency

Representa a moeda utilizada. Segue o padrão **ISO-4217**.

```
BRL
USD
EUR
GBP
```

---

## Identifier

Identificador universal de um Resource.

```typescript
Identifier {
    id: string
    externalId: string
}
```

| Campo | Descrição |
|--------|-----------|
| id | Identificador interno da Dialyn |
| externalId | Identificador do Provider |

---

## Metadata

Informações adicionais preservadas pelo Engine.

```typescript
Metadata {
    values: object
}
```

> A Dialyn **não interpreta** o conteúdo deste objeto.

---

## Image

Representa uma imagem.

```typescript
Image {
    url: string
    alt: string
}
```

---

## Dimensions

Representa as dimensões físicas de um item.

```typescript
Dimensions {
    width: decimal
    height: decimal
    length: decimal
    unit: string
}
```

Exemplos de unidade:

```
cm
m
mm
in
```

---

## Weight

Representa o peso de um recurso.

```typescript
Weight {
    value: decimal
    unit: string
}
```

Exemplos:

```
g
kg
lb
oz
```

---

## Address

Endereço utilizado para entrega ou faturamento.

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

---

## CustomerReference

Referência simplificada de um cliente.

```typescript
CustomerReference {
    id: string
    name: string
}
```

---

## ProductReference

Referência simplificada de um produto.

```typescript
ProductReference {
    id: string
    name: string
    sku: string
}
```
---

## CategoryReference
Referencia de estoque
```typescript
CategoryReference {
    id: string
    name: string
}
```

---

## OrderReference

Referência simplificada de um pedido.

```typescript
OrderReference {
    id: string
    number: string
}
```

---

## InventoryReference

Referência simplificada de um estoque.

```typescript
InventoryReference {
    id: string
    location: string
}
```

---

## Status

### ProductStatus

```
DRAFT
ACTIVE
INACTIVE
ARCHIVED
```

### OrderStatus

```
PENDING
PROCESSING
PAID
SHIPPED
DELIVERED
CANCELED
REFUNDED
```

### InventoryStatus

```
IN_STOCK
LOW_STOCK
OUT_OF_STOCK
BACKORDER
```

---

## ProductType

```
PHYSICAL
DIGITAL
SERVICE
SUBSCRIPTION
```

---

## SKU

Representa o código de identificação de um produto.

```typescript
SKU {
    value: string
}
```

> Cada Provider poderá utilizar sua própria estrutura, mas a Dialyn sempre trabalhará com um identificador canônico.

---

## Pagination

Representa informações de paginação.

```typescript
Pagination {
    page: integer
    limit: integer
    total: integer
    pages: integer
}
```

---

## Utilização

Os Resources da Capability **Commerce** deverão reutilizar estes tipos sempre que possível.

| Resource | Tipos Utilizados |
|----------|------------------|
| **Product** | `Money`, `SKU`, `Dimensions`, `Weight`, `Image`, `ProductStatus`, `ProductType`, `Metadata` |
| **Order** | `Money`, `Currency`, `OrderStatus`, `Address`, `CustomerReference`, `ProductReference`, `Metadata` |
| **Customer** | `Address`, `Metadata` |
| **Inventory** | `InventoryStatus`, `ProductReference`, `Metadata` |

---

## Convenções

Todos os tipos definidos neste documento deverão seguir as seguintes regras:

| # | Regra |
|---|-------|
| 1 | Ser independentes de qualquer Provider |
| 2 | Não conter regras específicas de Shopify, WooCommerce ou Hotmart |
| 3 | Ser reutilizáveis entre múltiplos Resources |
| 4 | Ser compatíveis com todos os Engines da Capability Commerce |
| 5 | Sempre que possível utilizar enums canônicos definidos pela Dialyn |

---

## Evolução

> Novos tipos compartilhados poderão ser adicionados neste documento conforme a Capability **Commerce** evoluir.

Tipos específicos de um único Resource não deverão ser adicionados ao `common.md`.

> A criação de estruturas duplicadas deverá ser evitada sempre que existir um tipo compartilhado adequado.

---

## Princípios

| # | Princípio | Descrição |
|---|-----------|-----------|
| 1 | 🔗 **Independência** | De qualquer plataforma de e-commerce |
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

- [README](./README.md)
- [Glossary](./glossary.md)
- [Relationships](./relationships.md)
- [Product](./product.md)
- [Order](./order.md)
- [Customer](./customer.md)
- [Inventory](./inventory.md)
