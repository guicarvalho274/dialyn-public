# Shopify

> Integração de e-commerce utilizada pela Dialyn para permitir que agentes de IA consultem produtos, acompanhem pedidos e automatizem operações comerciais.

---

# Por que utilizar Shopify?

O Shopify é utilizado pela Dialyn para conectar agentes inteligentes a lojas virtuais, permitindo que eles participem ativamente do processo de vendas e atendimento.

A integração possibilita que o agente consulte informações do catálogo, acompanhe pedidos, verifique disponibilidade de produtos e automatize processos comerciais sem que o usuário precise acessar o painel administrativo da loja.

Entre os principais cenários estão:

- consulta de produtos;
- gerenciamento de pedidos;
- consulta de estoque;
- acompanhamento de clientes;
- organização do catálogo;
- automação do pós-venda.

O objetivo é transformar o agente em um assistente de vendas capaz de acompanhar toda a jornada do cliente.

---

# Principais problemas resolvidos

## Atendimento comercial manual

Sem integração:

```
Cliente pergunta sobre um produto

↓

Vendedor acessa Shopify

↓

Procura produto

↓

Consulta estoque

↓

Responde o cliente
```

Com a Dialyn:

```
Cliente

↓

Agente

↓

Commerce Capability

↓

Shopify

↓

Resposta imediata
```

O agente consulta todas as informações em tempo real.

---

## Acompanhamento de pedidos

O agente pode responder perguntas como:

- Meu pedido já foi enviado?
- O produto está em estoque?
- Qual o status da compra?
- Qual o código de rastreamento?

Sem necessidade de intervenção humana.

---

# Casos de uso

## 1. Consulta de produtos

Permite pesquisar o catálogo da loja.

Exemplos:

- nome;
- descrição;
- preço;
- categoria;
- imagens;
- disponibilidade.

---

## 2. Consulta de estoque

Antes de recomendar um produto, o agente pode verificar sua disponibilidade.

Exemplo:

Cliente:

> Esse produto ainda está disponível?

O agente consulta o estoque em tempo real.

---

## 3. Acompanhamento de pedidos

Permite acompanhar pedidos durante todo o processo.

Exemplos:

- pedido recebido;
- pagamento aprovado;
- separação;
- envio;
- entrega.

---

## 4. Consulta de clientes

O agente pode acessar informações relacionadas aos clientes da loja.

Exemplos:

- histórico de compras;
- pedidos realizados;
- dados cadastrais;
- preferências.

---

## 5. Automação do pós-venda

Após uma compra, o agente pode:

- confirmar o pedido;
- informar status;
- acompanhar entrega;
- responder dúvidas;
- iniciar fluxos de fidelização.

---

# Quando utilizar Shopify?

O Shopify é recomendado para empresas que utilizam a plataforma como operação principal de e-commerce.

Exemplos:

- lojas virtuais;
- marcas próprias;
- vendas internacionais;
- D2C (Direct to Consumer);
- empresas com grande catálogo de produtos.

---

# Principais benefícios

A integração oferece diversas vantagens.

Entre elas:

- consulta ao catálogo em tempo real;
- acompanhamento de pedidos;
- consulta de estoque;
- acesso aos dados dos clientes;
- automação do atendimento;
- integração entre vendas e suporte.

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

Inventory

Category
```

---

# Actions disponibilizadas

## Produtos

- Consultar produto
- Listar produtos
- Pesquisar produtos
- Atualizar produto

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

## Estoque

- Consultar estoque
- Atualizar estoque

---

## Categorias

- Listar categorias
- Consultar categoria

---

# Benefícios para agentes de IA

A integração permite que o agente:

- responda dúvidas sobre produtos em tempo real;
- consulte disponibilidade antes de recomendar itens;
- acompanhe pedidos durante todo o ciclo de venda;
- personalize o atendimento utilizando o histórico do cliente;
- automatize processos de suporte e pós-venda.

---

# Quando NÃO utilizar Shopify?

Embora seja uma plataforma extremamente completa para e-commerce, alguns cenários podem ser mais adequados para outros Providers.

Exemplos:

- venda de produtos digitais e cursos online;
- marketplaces especializados;
- plataformas baseadas em WordPress.

Nesses casos, outros Providers da Capability **Commerce** podem ser mais adequados.

---

# Papel dentro da Dialyn

O Shopify não define as capacidades da plataforma.

Ele implementa a Capability **Commerce**, permitindo que agentes utilizem recursos de e-commerce através de um contrato universal.

```
Agente

↓

Action:
Consultar produto

↓

Commerce Capability

↓

Product.Get

↓

Commerce Engine

↓

Shopify
```

Da mesma forma, operações como consultar pedidos, verificar estoque ou atualizar informações de clientes seguem o mesmo fluxo, mantendo os agentes desacoplados das particularidades do Provider.