# 🌐 Arquitetura de Microserviços com API Gateway e Clean Architecture

Bem-vindo à organização do projeto de Microserviços! Este ecossistema foi desenvolvido como parte de um projeto acadêmico focado em práticas avançadas do curso de Desenvolvimento de Sistemas, simulando cenários reais de produção com alta escalabilidade, segurança e baixo acoplamento.

---

## 🎯 Visão Geral

Este projeto consiste na construção de um sistema distribuído baseado em microserviços. O objetivo principal é gerenciar Clientes e Produtos (com fluxo de compras), centralizando o acesso, o roteamento e a validação de segurança através de um **API Gateway**.

A arquitetura foi rigorosamente desenhada seguindo os princípios de **Clean Architecture**, garantindo que as regras de negócio puras fiquem isoladas de frameworks e detalhes de infraestrutura.

---

## 🏗️ Estrutura da Organização e Repositórios

Cada microserviço é um projeto independente e possui seu próprio repositório dentro desta organização. 

Abaixo está o mapa de repositórios:

* **[`api-gateway`](#)**: Ponto de entrada único da aplicação. Responsável pelo roteamento de requisições (`/auth/**`, `/clientes/**`, `/produtos/**`), balanceamento de carga e aplicação de filtros globais (ex: validação de token JWT).
* **[`auth-service`](#)**: Serviço responsável pela gestão de usuários e autenticação. Gera os tokens JWT para acesso seguro aos demais recursos.
* **[`cliente-service`](#)**: Serviço de gerenciamento de clientes, incluindo dados pessoais e endereços.
* **[`produto-service`](#)**: Serviço de catálogo de produtos e registro de compras associadas aos clientes.

---

## 🧩 Clean Architecture (Arquitetura Limpa)

Com exceção do API Gateway, todos os microserviços (`auth`, `cliente`, `produto`) são divididos internamente em dois módulos distintos para garantir o desacoplamento:

1.  **Módulo `domain` (Núcleo):** Contém as regras de negócio puras, entidades e interfaces (portas). Zero dependência de frameworks externos.
2.  **Módulo `spring` (Infraestrutura):** Contém os Controllers REST, DTOs, configurações de segurança, e a implementação dos repositórios utilizando Spring Data e MongoDB (adaptadores).

**Fluxo de Requisição:**
`Controller (Spring)` ➡️ `DTO -> Adapter` ➡️ `Service (Domain)` ➡️ `Repository Interface (Domain)` ➡️ `Repository Impl (Spring/MongoDB)`

---

## 🚀 Tecnologias e Ferramentas

O ecossistema foi construído utilizando as seguintes tecnologias:

* **Linguagem:** Java 17
* **Framework Principal:** Spring Boot / Spring Web
* **Gateway:** Spring Cloud Gateway
* **Banco de Dados:** MongoDB (Spring Data MongoDB)
* **Segurança:** Spring Security, JWT (JSON Web Tokens) e BCrypt
* **Padrões:** REST, API Gateway, Clean Architecture, Microserviços

---

## 🔐 Segurança e Autenticação

A segurança é tratada de forma centralizada. 
1.  O usuário se autentica no `auth-service`.
2.  O serviço retorna um token **JWT** assinado (Bearer token).
3.  Todas as requisições subsequentes passam pelo `api-gateway`, que intercepta e valida a assinatura do token antes de rotear para os serviços internos (`cliente` e `produto`).
4.  Controle de acesso rigoroso baseado em Roles (`USER`, `ADMIN`).

---

> **Desenvolvido por:** Diogo Marques e Gabriel Messias
