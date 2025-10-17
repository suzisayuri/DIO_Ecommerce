# DIO_Ecommerce
# 🛍️ Modelo Relacional de E-commerce Refinado

Este repositório contém o modelo de dados relacional (DER - Diagrama Entidade-Relacionamento) de um sistema de e-commerce, desenvolvido como parte do desafio de projeto do **Bootcamp [Radstad - Análise de Dados]** da **DIO (Digital Innovation One)**.

## 🎯 Objetivo do Projeto

O objetivo principal deste desafio foi refinar e aplicar os conceitos avançados de **Modelagem de Dados Relacionais** para estruturar um banco de dados eficiente e normalizado, endereçando requisitos específicos de negócio, como a especialização de clientes, flexibilidade de pagamento e rastreabilidade de entregas.

## ⚙️ Tecnologias e Ferramentas

* **Ferramenta de Modelagem:** Oracle SQL Developer Data Modeler.
* **Conceito:** Modelo Entidade-Relacionamento (MER) e Modelo Relacional, com foco em Normalização e Especialização.
* **Linguagem de Definição de Dados (DDL):** SQL.



## ✨ Destaques da Modelagem (Pontos de Refino)

O modelo relacional foi refinado para atender aos seguintes requisitos específicos:

### 1. Clientes Pessoa Física e Pessoa Jurídica

Para garantir que uma conta seja **exclusivamente PF ou PJ**, apliquei o conceito de **Especialização com Exclusão Mútua** (Super-tipo/Sub-tipo):

* **Tabela `CLIENTE`:** Serve como super-tipo, contendo o `ID_CLIENTE` (PK) e atributos comuns (ex: telefone, e-mail).
* **Tabelas `CLIENTE_PF` e `CLIENTE_PJ`:** São sub-tipos. Ambas possuem uma chave primária que é também uma chave estrangeira (`ID_CLIENTE`) referenciando a tabela `CLIENTE` (relação 1:1).
* **Restrição:** No nível lógico, a exclusão mútua é garantida pelo fato de um `ID_CLIENTE` poder existir em `CLIENTE_PF` **ou** `CLIENTE_PJ`, mas nunca em ambas simultaneamente.

### 2. Múltiplas Formas de Pagamento

Para permitir que o cliente tenha **mais de uma forma de pagamento cadastrada** (ex: dois cartões de crédito e uma conta PayPal), foi criada a entidade:

* **`FORMAS_PAGAMENTO_CLIENTE`:** Esta tabela estabelece uma relação **1:N** com a tabela `CLIENTE`.
    * Campos: `ID_PAGAMENTO` (PK), `ID_CLIENTE` (FK), `Tipo_Pagamento`, `Número do cartão` (hash do cartão, etc.).

### 3. Rastreabilidade da Entrega

A informação logística foi isolada para permitir o rastreio e a atualização independente do pedido:

* **Tabela `ENTREGA`:** Criada para detalhar o processo de envio. Possui uma relação **1:1** ou **1:N** com a tabela `PEDIDO`.
    * Campos:
        * `ID_ENTREGA` (PK)
        * `ID_PEDIDO` (FK)
        * `Status_Entrega` (Ex: "Preparando Envio", "Em Transporte", "Entregue")
        * `Codigo_Rastreio` (Atributo essencial para o acompanhamento).

---
**Desenvolvido por:** [Seu Nome ou Nome de Usuário do GitHub]
