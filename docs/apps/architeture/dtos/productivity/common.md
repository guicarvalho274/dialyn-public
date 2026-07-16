# Common Types

> Tipos compartilhados utilizados pelos Resources da Capability **Productivity**.

---

## Objetivo

Este documento define os tipos reutilizáveis da Capability **Productivity**.

Seu objetivo é evitar duplicação de estruturas entre Resources como **Calendar**, **Event**, **Task**, **Board**, **Card**, **Page**, **Database** e **Block**, mantendo um modelo canônico consistente para toda a arquitetura da Dialyn.

> Sempre que um mesmo conceito for utilizado por mais de um Resource, ele deverá ser definido neste documento.

---

## Filosofia

| Característica | Descrição |
|---------------|-----------|
| 🎯 Escopo | Conceitos compartilhados entre plataformas de produtividade |
| 🚫 Propriedade | Não pertencem a um Provider específico |
| ⚖️ Regras | Não devem conter regras de negócio |
| 📡 Responsabilidade | Padronizar a comunicação entre Dialyn e Productivity Engines |

---

## Shared Types

### UserReference

Representa um usuário responsável ou participante.

```typescript
UserReference {
    id: string
    name: string
}
```

### MemberReference

Representa um membro de um Workspace.

```typescript
MemberReference {
    id: string
    name: string
}
```
---

### WorkspaceReference

Representa um Workspace ou espaço de trabalho.

```typescript
WorkspaceReference {
    id: string
    name: string
}
```

### CardReference
Representa um card.

```typescript

CardLabel {
    id: string
    name: string
    color: string
}
```

### ColorReference

```typescript
ColorReference{
    value: string
}
```
---

### CalendarReference

Representa um calendário.

```typescript
CalendarReference {
    id: string
    name: string
}
```

### TimezoneReference

```typescript
TimezoneReference{
    name: string
    offset: string
}
```
---

### BoardReference

Representa um quadro de trabalho.

```typescript
BoardReference {
    id: string
    name: string
}

BoardLayout {
    type: string
}
```

---

### PageReference

Representa uma página.

```typescript
PageReference {
    id: string
    title: string
}
```

---

### DatabaseReference

Representa uma base de dados.

```typescript
DatabaseReference {
    id: string
    name: string
}
```

---

### DateTimeRange

Representa um intervalo de tempo.

```typescript
DateTimeRange {
    start: datetime
    end: datetime
    timezone: string
}
```
---

### OptionReference

```typescript
Icon {
    type: string
    value: string
}

Cover {
    url: string
}
```

---

### Attachment

Representa um arquivo associado a um Resource.

```typescript
Attachment {
    id: string
    name: string
    url: string
    mimeType: string
    size: integer
}
```

### Content
Respresenta o conteudo de um Bloco.

```typescript
Content {
    type: BlockType
    text: string
    richText: RichText[]
    url: string
    checked: boolean
    language: string
    children: boolean
}
```
---

### Participant

Represente um User e seu Papel.

```typescript
Participant {
    user: UserReference
    role: string
    responseStatus: string
}
```

### SchemaReference
Representa a estrutura de uma Database.

```typescript
SchemaField {
    id: string
    name: string
    type: string
    required: boolean
}
```

---

### Metadata

Representa informações específicas do Provider.

```typescript
Metadata {
    values: map<string, any>
}
```

---

## Enumerations

### Visibility

```
PUBLIC
PRIVATE
SHARED
```

---

### Priority

```
LOW
MEDIUM
HIGH
URGENT
```

---

### Status

Representa um estado genérico para Resources da Capability.

```
ACTIVE
INACTIVE
ARCHIVED
```

---

### Permission

Representa o nível de acesso de um usuário.

```
READ
WRITE
ADMIN
```

---

## Utilização

Os Resources da Capability **Productivity** deverão reutilizar estes tipos sempre que possível.

| Resource | Tipos Utilizados |
|----------|------------------|
| **Calendar** | `WorkspaceReference`, `UserReference`, `Visibility`, `Metadata` |
| **Event** | `CalendarReference`, `DateTimeRange`, `UserReference`, `Attachment`, `Metadata` |
| **Task** | `UserReference`, `Priority`, `Status`, `Attachment`, `Metadata` |
| **Board** | `WorkspaceReference`, `UserReference`, `Visibility`, `Metadata` |
| **Card** | `BoardReference`, `UserReference`, `Priority`, `Attachment`, `Metadata` |
| **Page** | `WorkspaceReference`, `UserReference`, `Attachment`, `Metadata` |
| **Database** | `WorkspaceReference`, `PageReference`, `Metadata` |
| **Block** | `PageReference`, `Metadata` |

---

## Convenções

| # | Convenção |
|---|-----------|
| 1 | Reutilizar os tipos definidos neste documento |
| 2 | Utilizar tipos `Reference` para representar relacionamentos |
| 3 | Utilizar `Metadata` para armazenar informações específicas do Provider |
| 4 | Evitar duplicação de estruturas compartilhadas |

---

## Evolução

Novos tipos compartilhados poderão ser adicionados conforme a Capability **Productivity** evoluir.

> A criação de tipos duplicados entre Resources deverá ser evitada sempre que existir um modelo compartilhado adequado.

---

## Princípios

| # | Princípio | Descrição |
|---|-----------|-----------|
| 1 | 🔗 **Reutilização** | Evitar duplicação entre Resources |
| 2 | 🏗️ **Consistência** | Mesmo tipo = mesmo significado |
| 3 | 🔄 **Evolução** | Novos tipos podem ser adicionados sem quebrar contratos |
| 4 | 📖 **Documentação** | Tipos compartilhados centralizados |

---

## Benefícios

| # | Benefício |
|---|-----------|
| 1 | 🏗️ **Consistência** entre todos os Resources da Capability |
| 2 | 🔄 **Manutenção simplificada** com tipos centralizados |
| 3 | ➕ **Reutilização** evitando duplicação de código e documentação |
| 4 | 📖 **Clareza** sobre quais tipos cada Resource utiliza |

---

## Veja também

| Documento | Objetivo |
|-----------|----------|
| [README.md](./README.md) | Visão geral da Capability |
| [glossary.md](./glossary.md) | Conceitos da Capability |
| [relationships.md](./relationships.md) | Relacionamentos entre Resources |
| [calendar.md](./calendar.md) | Calendários |
| [event.md](./event.md) | Eventos |
| [task.md](./task.md) | Tarefas |
| [board.md](./board.md) | Quadros |
| [card.md](./card.md) | Cartões |
| [page.md](./page.md) | Páginas |
| [database.md](./database.md) | Bases de dados |
| [block.md](./block.md) | Blocos |
