## How to GraphQL

- [Artigos](#artigos)
- [Ferramentas](#ferramentas)
- [Introduction](#introduction)
  * [Revisão histórica sobre o REST](#revisao-historica-sobre-o-rest)
- [GraphQL vs REST - A comparasion](#graphql-vs-rest---a-comparasion)
  * [Blogging App with REST](#blogging-app-with-rest)
  * [Benefícios de um Schema & Types](#beneficios-de-um-schema--types)
- [Core Concepts](#core-concepts)

### Artigos

- [ ] [Top 5 Reasons to Use GraphQL](https://www.prisma.io/blog/top-5-reasons-to-use-graphql-b60cfa683511)
- [ ] [React.js Conf 2015 - Data fetching for React applications at Facebook](https://www.youtube.com/watch?v=9sc8Pyc51uU)
- [ ] [Netflix Falcor](https://github.com/Netflix/falcor)
- [ ] [Lessons From 4 Years of GraphQL](https://www.graphql.com/articles/4-years-of-graphql-lee-byron)
- [ ] [GraphQL SDL — Schema Definition Language](https://www.prisma.io/blog/graphql-sdl-schema-definition-language-6755bcb9ce51)
- [ ] [GraphQL Server Basics: GraphQL Schemas, TypeDefs & Resolvers Explained](https://www.prisma.io/blog/graphql-server-basics-the-schema-ac5e2950214e)
- [ ] [GraphQL Server Basics: The Network Layer](https://www.prisma.io/blog/graphql-server-basics-the-network-layer-51d97d21861)
- [ ] [GraphQL Server Basics: Demystifying the info Argument in GraphQL Resolvers](https://www.prisma.io/blog/graphql-server-basics-demystifying-the-info-argument-in-graphql-resolvers-6f26249f613a)


### Ferramentas

- [graphql-up](https://www.npmjs.com/package/graphql-up)
### Introduction

- O GraphQL é um novo padrão de API inventado pelo Facebook, que oferece uma alternativa mais poderosa e robusta ao padrão REST.
- A grande diferença do GraphQL é a forma como podemos declarar a manipulação de dados de uma forma declarativa
- O GraphQL oferece apenas um endpoint, através do qual iremos nos comunicar através de queries. O tipo de retorno será dinâmico, de acordo com o que declararmos
- O GraphQL é uma linguage de busca para APIS, não para banco de dados.

#### Revisão histórica sobre o REST

- O padrão REST tem sido uma forma comum de expor informações em um servidor
- Uma das motivações por trás da criação do GraphQL foi o crescimento do uso de dispositivos mobile, e a necessidade de um consumo de dados eficiente pelos aplicativos
- O GrapQL tem a capacidade de minimizar a quantidade de dados que serão trafegados pela rede, isso aumenta a capacidade dos aplicativos que estão sendo executados sobre essas circunstancias
- A rapida evolução de requisitos pode levar a uma necessidade de se alternar a forma como o servidor disponibiliza seus dados. Além dos diferentes clientes que uma aplicação pode ter, onde cada um pode ter sido escrito utilizando uma tecnologia diferente.

### GraphQL vs REST - A comparasion

- Algumas ideias boas na tecnologia REST
  - O servidor é stateless
  - O acesso aos recursos é estruturado
- Mesmo o REST sendo uma especificação bem rígida, existem muitas APIS que se dizem RESTful e que implementam a sua maneira a especificação
- Mudanças rápidas e constantes no client-side não funcionam muito bem com a natureza estática do REST

#### Blogging App with REST

Imagine que temos um aplicativo de blog, onde apresentaremos as seguintes informações:
- O nome do criador
- Os últimos posts que ele escreveu
- Os três últimos seguidores que ele ganhou

No modelo REST teriamos 3 API endpoints, uma para pegar cada uma dessas informações. Cada endpoint retornaria um conjunto de informações, com informações adicionais. Por exemplo, se pedirmos por um usuário específico, outras informações podem ser devolvidas também, como:
```json
{
  "user" : {
    "id" : "lfkasjlkajsf",
    "name" : "Mary",
    "address" : { ... },
    "birthday" : "January 10, 1988"
  }
}
```

Esse não é o comportamento desejado. Poderiamos criar um DTO que representasse esses dados, mas acabariamos criando um novo problema. Se os requisitos do cliente mudarem em algum momento teremos que alterar nossa API, bem como nosso DTO. Isso pode ser mais comum do que imaginamos, criando uma dependência entre as duas pontas, se o servidor não fornece o que o cliente precisa, ele para de ser desenvolvido.

Utilizando o GraphQL esse processo pode ser mais otimizado, mandamos para o servidor uma requisição do tipo POST, onde no corpo dela estará descrita a operação que queremos realizar no servidor:

```json
{
  "data" : {
    "User" : {
      "name" : "Mary",
      "posts" : [
        { "title" : "Learn GraphQL Today"}
      ],
      "followers" : [
        { "name" : "John" },
        { "name" : "Alice" },
        { "name" : "Sarah" },
      ]
    }
  }
}
```

Na estrutura REST os endpoints são pensados de acordo com as necessidades do cliente (nesse caso podemos pensar em uma tela específica). Se uma necessidade mudar, se houver uma diminuição na quantidade de dados que precisamos, vai ser necessário uma mudança na API, caso contrário estaremos fornecendo mais dados que é preciso, levando a um over-fetching (quando o endpoint retorna mais informação do que seria necessário). O cenário oposto a esse seria o underfetching, onde um endpoint específico não consegue prover todas as informações necessárias que o usuário precisa, por conta disso, requisições adicionais terão que ser feita.

Um exemplo disso seria o fetch pelos três ultimos seguidores e seus respectivos nomes, que dispararia três novas requisições para `/users/<user-id>`.

#### Benefícios de um Schema & Types

O GraphQL utiliza um forte sistema de tipos para definir as capacidades de uma API. Essas esquemas funcionam como um contrato entre o cliente e o servidor. Dessa forma, os times do backend e do frontend podem trabalhar de forma independente, já que as duas pontas contam com esse contrato que define como a comunicação será feita.

Podemos manter um tracking de quais informações foram mais solicitadas pelo cliente, através de métricar implementadas no servidor.

### Core Concepts


Escreveremos o sistema de tipos do GraphQL com o SDL (Schema definition language), a sintaxe é muito simples, podemos definir tipo básicos da seguinte forma:

```graphql
type Person {
  name: String!
  age: Int!
  posts: [Post!]!
}

type Post {
  title: String!
  author: Person
}
```

Para conversar com o servidor o cliente terá que enviar muito mais informação, ele terá que descrever que tipo de dados precisa, para que assim, o servidor seja capaz de fornece-los.

A marcação `!` serve para definir que um campo será de obrigatório preenchimento. Criamos no exemplo acima uma relação bi-direcional de muitos Posts para uma pessoa.

Quando criarmos nossas queries teremos que passar os parâmetros dela. Esse trecho será conhecido como `Query payload`. No payload definiremos quais dados devem ser retornados. A ordem que eles serão escritos pode varias, e caso algum campo seja repetido várias vezes, apenas uma resposta será retornada para cada campo.

```graphql
# Query

{
  allPersons {
    name
    name
    name
    name
  }
  allPosts {
    title
  }
}

# Resposta
{
  "data": {
    "allPersons": [
      {
        "name": "Johnny"
      },
      {
        "name": "Sarah"
      },
      {
        "name": "Alice"
      }
    ],
    "allPosts": [
      {
        "title": "GraphQL is awesome"
      },
      {
        "title": "Relay is a powerful GraphQL Client"
      },
      {
        "title": "How to get started with React & GraphQL"
      }
    ]
  }
}
```

Precisamos colocar ao menos 1 campo no payload, caso contrário teremos um erro de execução:

```graphql
{
  allPersons {
  }
}

{
  "error": "Syntax error while parsing GraphQL query.
  Invalid input query expected OperationDefinition,
  FragmentDefinition or TypeSystemDefinition (line 1, column 1)"
}
```
Podemos também fazer queries encadeadas, com argumentos, basta seguir a ideia a seguir:

```graphql
{
  allPersons {
    name
    posts {
      title
    }
  }
}

{
  allPersons {
    name
    posts(last: 1) {
      title
    }
  }
}
```

Perceba que a sintaxe de busca varia da sintaxe de definição de um sistema de tipos. Além de buscar dados no servidor nós podemos criar, alterar e remover. Essas operações que modificam os dados de alguma forma são chamadas de `Mutations`. No nosso exemplo, podemos cria uma pessoa da seguinte forma:

```graphql
mutation {
  createPerson(name: "Bob", age: 36) {
    id
    name
  }
}
```

Estamos criando uma nova pessoa e passando no payload quais são os dados que queremos que sejam retornados.

Além dessas operações citadas, o cliente pode fazer uma inscrição no servidor, e ficar esperando por eventos de algum tipo, por exemplo, uma subscription para novos usuários:

```graphql
subscription {
  newPerson {
    name
    age
  }
}
```

Dessa forma o servidor vai enviar para o cliente informações sempre que um evento desse tipo ocorrer, algo semelhante a um streaming de dados. Isso varia bastante do modelo `request-response` encontrado no REST.
