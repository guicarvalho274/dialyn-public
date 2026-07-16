# Hotmart

> Integração de comércio digital utilizada pela Dialyn para permitir que agentes de IA gerenciem produtos digitais, vendas, alunos e processos de pós-venda.

---

# Por que utilizar Hotmart?

O Hotmart é utilizado pela Dialyn para conectar agentes inteligentes a plataformas de comercialização de produtos digitais.

A integração permite que o agente participe de toda a jornada do cliente, desde a venda até o acesso ao conteúdo adquirido.

Entre os principais cenários estão:

- venda de cursos online;
- comercialização de e-books;
- venda de mentorias;
- gestão de membros;
- consulta de pedidos;
- acompanhamento de alunos;
- automação do pós-venda.

O objetivo é permitir que agentes automatizem processos comerciais e de atendimento relacionados a produtos digitais.

---

# Principais problemas resolvidos

## Atendimento manual aos alunos

Sem integração:

```
Aluno faz uma pergunta

↓

Equipe acessa Hotmart

↓

Consulta compra

↓

Verifica acesso

↓

Responde manualmente
```

Com a Dialyn:

```
Aluno

↓

Agente

↓

Commerce Capability

↓

Hotmart

↓

Resposta imediata
```

O agente consulta as informações automaticamente.

---

## Acompanhamento da jornada do cliente

O agente pode responder perguntas como:

- Minha compra foi aprovada?
- Já tenho acesso ao curso?
- Qual produto comprei?
- Posso solicitar reembolso?

Tudo utilizando informações em tempo real.

---

# Casos de uso

## 1. Consulta de produtos

Permite consultar informações sobre produtos digitais.

Exemplos:

- cursos;
- mentorias;
- comunidades;
- e-books;
- assinaturas.

---

## 2. Consulta de pedidos

O agente pode acompanhar pedidos realizados pelos clientes.

Exemplos:

- pagamento aprovado;
- pagamento pendente;
- compra cancelada;
- reembolso solicitado.

---

## 3. Consulta de clientes

Permite consultar informações relacionadas aos compradores.

Exemplos:

- histórico de compras;
- produtos adquiridos;
- status da conta;
- informações cadastrais.

---

## 4. Acompanhamento de acesso

Após a confirmação da compra, o agente pode informar:

- se o acesso já foi liberado;
- quais produtos estão disponíveis;
- como acessar a plataforma.

---

## 5. Automação do pós-venda

O agente pode automatizar diversas etapas após a compra.

Exemplos:

- confirmação de pagamento;
- boas-vindas;
- orientações de acesso;
- suporte inicial;
- acompanhamento da jornada do aluno.

---

# Quando utilizar Hotmart?

O Hotmart é recomendado para empresas e criadores que comercializam produtos digitais.

Exemplos:

- cursos online;
- infoprodutos;
- mentorias;
- programas de assinatura;
- comunidades exclusivas;
- treinamentos corporativos.

---

# Principais benefícios

A integração oferece diversas vantagens.

Entre elas:

- acompanhamento completo das vendas;
- consulta automática de pedidos;
- acesso ao histórico de compras;
- suporte automatizado aos alunos;
- integração entre vendas e atendimento;
- redução de processos manuais.

---

# Capacidades utilizadas

A integração implementa a Capability:

```
Commerce
```

Principais Resources:

```
Product

Order

Customer

Category
```

> Dependendo das funcionalidades disponibilizadas pelo Provider, alguns Resources da Capability Commerce podem não estar disponíveis ou possuir limitações.

---

# Actions disponibilizadas

## Produtos

- Consultar produto
- Listar produtos
- Pesquisar produtos

---

## Pedidos

- Consultar pedido
- Listar pedidos
- Atualizar pedido

---

## Clientes

- Consultar cliente
- Atualizar cliente

---

## Categorias

- Listar categorias
- Consultar categoria

---

# Benefícios para agentes de IA

A integração permite que o agente:

- acompanhe todo o ciclo de venda de produtos digitais;
- consulte pedidos em tempo real;
- responda dúvidas sobre acesso aos conteúdos;
- automatize o atendimento de alunos;
- personalize respostas utilizando o histórico de compras;
- reduza a carga operacional das equipes de suporte.

---

# Quando NÃO utilizar Hotmart?

Embora seja uma excelente plataforma para produtos digitais, alguns cenários são mais adequados para outros Providers.

Exemplos:

- venda de produtos físicos;
- controle detalhado de estoque;
- operações completas de logística;
- gerenciamento de inventário.

Nesses casos, outros Providers da Capability **Commerce** podem ser mais adequados.

---

# Papel dentro da Dialyn

O Hotmart não define as capacidades da plataforma.

Ele implementa a Capability **Commerce**, permitindo que agentes utilizem recursos de comércio digital através de um contrato universal.

```
Agente

↓

Action:
Consultar pedido

↓

Commerce Capability

↓

Order.Get

↓

Commerce Engine

↓

Hotmart
```

Operações como consultar produtos, acompanhar compras ou acessar informações de clientes seguem o mesmo fluxo, mantendo os agentes desacoplados das particularidades da plataforma.

---

# Observações

O foco principal do Hotmart é a comercialização e distribuição de produtos digitais.

Por isso, funcionalidades como controle de estoque físico ou gestão logística podem não estar disponíveis, diferentemente de plataformas de e-commerce tradicionais.