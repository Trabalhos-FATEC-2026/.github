Arquitetura de Microserviços

O sistema foi estruturado em uma arquitetura baseada em microserviços, com comunicação indireta centralizada por um API Gateway. Cada domínio da aplicação é isolado em um serviço independente, com banco de dados e responsabilidade próprios, evitando acoplamento entre módulos.


---

Estrutura dos serviços

A arquitetura é composta pelos seguintes microserviços:

API Gateway Responsável por ser o ponto único de entrada do sistema. Todas as requisições passam por ele antes de chegar aos serviços internos. Ele realiza o roteamento das rotas (/auth/**, /clientes/**, /produtos/**) e aplica validações globais, principalmente a verificação de token JWT.

Auth Service Responsável pela autenticação de usuários. Realiza login, valida credenciais e gera tokens JWT utilizados para acesso aos demais serviços.

Cliente Service Responsável pelo gerenciamento de clientes, incluindo cadastro e manutenção de dados pessoais.

Produto Service Responsável pelo catálogo de produtos e pelo processamento das operações de compra.



---

Funcionamento da arquitetura

O fluxo básico do sistema ocorre da seguinte forma:

1. O cliente realiza login no Auth Service.


2. O serviço autentica as credenciais e retorna um JWT (Bearer Token).


3. As requisições seguintes são feitas através do API Gateway, incluindo o token no header de autorização.


4. O Gateway valida o token antes de encaminhar a requisição para o microserviço correspondente.


5. Os microserviços (cliente e produto) processam a requisição de forma independente, cada um com sua própria lógica de negócio e persistência.



Essa abordagem garante isolamento entre serviços, escalabilidade independente e menor acoplamento entre as partes do sistema.


---

Organização interna dos microserviços

Com exceção do API Gateway, todos os microserviços seguem separação interna baseada em Clean Architecture:

Domain Contém as regras de negócio, entidades e interfaces. Não possui dependência de frameworks.

Spring (Infrastructure) Responsável pela camada de entrada e saída do sistema:

Controllers REST

DTOs

Configurações de segurança

Implementação de repositórios com Spring Data MongoDB



Fluxo interno: Controller → DTO → Service (Domain) → Repository Interface → Implementação Spring/MongoDB


---

Tecnologias utilizadas

Java 17

Spring Boot

Spring Cloud Gateway

Spring Security

JWT (JSON Web Token)

MongoDB

Spring Data MongoDB

Arquitetura REST

Microserviços



---

Segurança

A autenticação é centralizada no Auth Service. O controle de acesso funciona via JWT:

O token é gerado no login.

O API Gateway intercepta todas as requisições.

O token é validado antes do redirecionamento para os serviços internos.

O acesso é controlado por roles (ex: USER, ADMIN).



---

Responsáveis pelo projeto

Diogo Marques
Gabriel Messias
