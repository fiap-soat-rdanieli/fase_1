# Tech Challenge Fase 1

![Docker Image Version (latest semver)](https://img.shields.io/docker/v/rdanieli/soat_api)
![Docker Pulls](https://img.shields.io/docker/pulls/rdanieli/soat_api)


Entrega da Fase 1 do Tech Challenge da Pos-Graduação de Arquitetura de Software (SOAT).

Aluno: Rodrigo Mariano Danieli Merlucci

---
## Indice
1. [Documentacao](#documentação-ddd)
    * [Linguagem Ubiqua](#linguagem-ubiqua)
    * [Fluxos](#fluxos)
2. [Projeto](#projeto)
    * [Instalação](#instalação)
    * [API](#api)
        * [Cliente](#cliente)
            * Lista 
            * Consulta por CPF
            * Cadastro
        * [Produto](#produto)
            * Lista 
            * Consulta por Categoria
            * Cadastro
            * Editar
            * Remover
        * [Pedido](#pedido)
            * Lista 
            * Consulta por Status
            * Novo
            * Adicionar Produto
            * Remover Produto
            * Lista de Produtos
            * Checkout


---

## Documentação DDD

   Nesse repositorio é apresentada a Linguagem Ubiqua usada, e os fluxos usados como referencia para a contrução e compreenção do projeto.

---

### Linguagem Ubiqua

* Cliente

  Pessoa que deseje consumir e realizar um pedido no estabelecimento
* Produto

  Todos os itens que são vendidos dentro do estabelecimento, podendo ser Bebidas, Lanches, Acompanhamentos e Sobremesas

* Pedido

  Conjuto de produtos selecionados pelo Cliente
* Atendente

  Funcionario que possui interação com o Cliente
* Bebida

  Todos os produtos liquidos, como Agua, Suco, Refrigerante e Drinks
* Lanche

  Todos os produtos feitos com pão e uma proteina, podendo ser de origem animal ou vegetal.
* Acompanhamento

  Todos os produtos que podem ser servidos com o lanche ou individualmente, como Nuggets, Batata Frita, Batata Rustica, Frutas e molhos
* Sobremesa

  Todos os produtos doces em geral, como Sorvetes, MilkShakes e Bolos.
* Cozinha

  Conjunto das praças que realizara a produção do pedido do Cliente assim como a entrega do pedido.
* Praça da Chapa

  Local onde será preparado todos os produtos de relação aos lanches
* Praça dos Acompanhamentos

  Local onde é preparado os acompanhamentos do pedido, tais como Batadas, Nuggets, Frutas
* Praça das Sobremesas

  Local onde é preparada as sobremesas de um pedido, tais como Sorvetes, MilkShakes, Bolos e Doces
* Praça das Bebidas

  Local onde é preparada as babidas de um pedido, tais como Agua, Refrigerantes, Drinks e Sucos

  ---

### Fluxos

  Fluxos representados:
  * Cadastro Cliente
  * Realização do Pedido
  * Realização do Pagamento
  * Preparação do Pedido
  * Entrega do Pedido

    Link para acesso aos fluxos: [Miro](https://miro.com/app/board/uXjVM_ldY2o=/?share_link_id=862090014137)


---
## Projeto

   O projeto foi desenvolvido na linguagem de programação PHP e utilizando o MySql como banco de dados. 
   
   Esse documento possui todas as instruções para a instalação do projeto, mas o codigo fonte original esta disponibilizado no repositorio [fiap-soat-rdanieli/backend_api](https://github.com/fiap-soat-rdanieli/backend_api).

   Neste repositorio existe um docker-compose que é usado para a configuração dos containers de banco e aplicação, e um diretorio **db**, onde estao os scripts iniciais do banco de dados, que seram executados ao iniciar o container.
   
---
### Instalação 

   Fazendo download do repositorio:

    > git init
    > git pull https://github.com/fiap-soat-rdanieli/fase_1

   Iniciando o projeto 

    > docker compose -f docker-compose.yml up

   Após isso o projeto estará rodando e poderar ser acessado atraves da porta 80 da maquina
   
---
### API

  Exemplo via PHP:
  ~~~php

$parameters = [
    "status" => "Checkout"
];

$client = new GuzzleHttp\Client(
    [
        "base_uri" => "http://localhost",
        "headers" => [
            "Content-Type" => "application/json"
        ]
    ]
);

$response = $client->post(
    "/api/pedido/buscar_status",
    [
        "body" => json_encode($parameters)
    ]
);

$content = $response->getBody()->getContents();

var_dump(json_decode($content, true));

  ~~~

  ### Cliente

  * Lista
    ---
        
    *Descrição*: Listagem dos Clientes

    *Path*: **/api/cliente/lista**
  
    *Metodo*: **GET**
  
    *Parâmetros*: None
  
    *Retorno*:

        {
          "status" : String,
          "data" : Cliente[]
        }
  
  
  * Consulta por CPF
    ---
        
    *Descrição*: Buscar um cliente pelo CPF

    *Path*: **/api/cliente/buscar**
  
    *Metodo*: **POST**
  
    *Parâmetros*: 

        {
          "cpf" : String
        }
  
  
    *Retorno*:

        {
          "status" : String,
          "data" : Cliente[]
        }
  
  
  
  * Cadastrar
    ---
        
    *Descrição*: Cadastro do Cliente

    *Path*: **/api/cliente/cadastrar**
  
    *Metodo*: **POST**
  
    *Parâmetros*: 

        {
          "cpf": String,
          "nome": String,
          "email": String
        }
  
  
    *Retorno*:

        {
          "status" : String
        }
  

  
  ### Produto
  
  * Lista
    ---
        
    *Descrição*: Listagem de todos os produtos

    *Path*: **/api/produto/lista**
  
    *Metodo*: **GET**
  
    *Parâmetros*: None
  
    *Retorno*:

        {
          "status" : String,
          "data" : Produto[]
        }
  
  
  * Consulta por categoria
    ---
        
    *Descrição*: Listagem de todos os produtos filtrado pela categoria

    *Path*: **/api/produto/buscar**
  
    *Metodo*: **POST**
  
    *Parâmetros*: 

        {
          "categoria" : String
        }
  
  
    *Retorno*:

        {
          "status" : String,
          "data" : Produto[]
        }
  
  
  
  * Cadastrar
    ---
        
    *Descrição*: Cadastrar um novo produto

    *Path*: **/api/produto/cadastrar**
  
    *Metodo*: **POST**
  
    *Parâmetros*: 

        {
          "nome": String,
          "descricao": String,
          "categoria": String,
          "valor": String
        }
  
  
    *Retorno*:

        {
          "status" : String
        }
  
  
 
  
  * Editar
    ---
        
    *Descrição*: Editar as informações de um campo do produto

    *Path*: **/api/produto/editar**
  
    *Metodo*: **POST**
  
    *Parâmetros*: 

        {
          "id": String,
          "campo": Enum('nome', 'descricao', 'valor','categoria'),
          "valor": Mixed
        }
  
  
    *Retorno*:

        {
          "status" : String
        }

  
  * Remover
    ---
        
    *Descrição*: Remove um produto

    *Path*: **/api/produto/remover**
  
    *Metodo*: **POST**
  
    *Parâmetros*: 

        {
          "id": String
        }
  
  
    *Retorno*:

        {
          "status" : String
        }
  
    
  ### Pedido
  
  * Lista
    ---
        
    *Descrição*: Listagem de todos os pedidos

    *Path*: **/api/pedido/lista**
  
    *Metodo*: **GET**
  
    *Parâmetros*: None
  
    *Retorno*:

        {
          "status" : String,
          "data" : Pedido[]
        }
   
  * Consulta por Status
    ---
        
    *Descrição*: Listagem de todos os pedidos filtrado pelo status

    *Path*: **/api/pedido/buscar_status**
  
    *Metodo*: **POST**
  
    *Parâmetros*: 

        {
          "status" : String,
        }
  
  
    *Retorno*:

        {
          "status" : String,
          "data" : Pedido[]
        }
   
  * Novo
    ---
        
    *Descrição*: Cria um novo pedido

    *Path*: **/api/pedido/novo**
  
    *Metodo*: **POST**
  
    *Parâmetros*: 

        {
          "cliente" : String,
        }
  
  
    *Retorno*:

        {
          "status" : String,
          "data" : PedidoId
        }
  
  

  * Adicionar Produto no Pedido
    ---
        
    *Descrição*: Adiciona um produto ao pedido
    
    *Path*: **/api/pedido_produto/add**
  
    *Metodo*: **POST**
  
    *Parâmetros*: 

        {
          "pedido_id": String,
          "produto_id": String,
          "observacao": String,
          "quantidade": Ini
        }
  
  
    *Retorno*:

        {
          "status" : String
        }
  
  

  

  * Remover Produto no Pedido
    ---
        
    *Descrição*: Remove um produto ao pedido
    
    *Path*: **/api/pedido_produto/remove**
  
    *Metodo*: **POST**
  
    *Parâmetros*: 

        {
          "pedido_id": String,
          "produto_id": String
        }
  
  
    *Retorno*:

        {
          "status" : String
        }
  
  


  * Lista de Produtos no Pedido
    ---
        
    *Descrição*: Lista dos produtos dentro do pedido
    
    *Path*: **/api/pedido_produto/get**
  
    *Metodo*: **POST**
  
    *Parâmetros*: 

        {
          "pedido_id": String
        }
  
  
    *Retorno*:

        {
          "status" : String,
          "data" : ProdutoPedido[]
        }
  
  


  * Checkout
    ---
        
    *Descrição*: Confirma o Pedido e da inicio a preparacao
    
    *Path*: **/api/pedido/checkout**
  
    *Metodo*: **POST**
  
    *Parâmetros*: 

        {
          "pedido_id": String
        }
  
  
    *Retorno*:

        {
          "status" : String
        }
  
  

  
  

    


  
    
    
  
