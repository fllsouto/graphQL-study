## How to GraphQL - Resumo

- [Artigos](#artigos)
- [Palestras e Vídeos](#palestras-e-videos)
- [Ferramentas e Recursos](#ferramentas-e-recursos)
- [Introduction](#introduction)
  * [Revisão histórica sobre o REST](#revisao-historica-sobre-o-rest)
- [GraphQL vs REST - A comparasion](#graphql-vs-rest---a-comparasion)
  * [Blogging App with REST](#blogging-app-with-rest)
  * [Benefícios de um Schema & Types](#beneficios-de-um-schema--types)
- [Core Concepts](#core-concepts)
- [Big Picture (Architecture)](#big-picture-architecture)
  * [Caso de uso 1](#caso-de-uso-1)
  * [Caso de uso 2](#caso-de-uso-2)
  * [Caso de uso 3](#caso-de-uso-3)
  * [Resolver Function](#resolver-function)
  * [Diferenças entre data fetching imperativo e declarativo](#diferencas-entre-data-fetching-imperativo-e-declarativo)
    + [Imperativo](#imperativo)
    + [Declarativo](#declarativo)
- [Advanced Tutorials - Client](#advanced-tutorials---client)
  * [Directly Sending Queries and Mutations](#directly-sending-queries-and-mutations)
  * [View layer integrations & UI updates](#view-layer-integrations--ui-updates)
  * [Caching query results: concepts and strategies](#caching-query-results-concepts-and-strategies)
- [Advanced Tutorials - Server](#advanced-tutorials---server)
  * [Batched Resolving](#batched-resolving)
- [Advanced Tutorials - More GraphQL Concepts](#advanced-tutorials---more-graphql-concepts)
  * [Enhancing Reusability with Fragments](#enhancing-reusability-with-fragments)
  * [Advanced SDL](#advanced-sdl)
- [Advanced Tutorials - Tooling and Ecosystem](#advanced-tutorials---tooling-and-ecosystem)
- [Advanced Tutorials - Security](#advanced-tutorials---security)
- [Advanced Tutorials - Common Questions](#advanced-tutorials---common-questions)

### Artigos

- [x] [Top 5 Reasons to Use GraphQL](https://www.prisma.io/blog/top-5-reasons-to-use-graphql-b60cfa683511)
- [ ] [React.js Conf 2015 - Data fetching for React applications at Facebook](https://www.youtube.com/watch?v=9sc8Pyc51uU)
- [ ] [Lessons From 4 Years of GraphQL](https://www.graphql.com/articles/4-years-of-graphql-lee-byron)
- [ ] [GraphQL SDL — Schema Definition Language](https://www.prisma.io/blog/graphql-sdl-schema-definition-language-6755bcb9ce51)
- [ ] [GraphQL Server Basics: GraphQL Schemas, TypeDefs & Resolvers Explained](https://www.prisma.io/blog/graphql-server-basics-the-schema-ac5e2950214e)
- [ ] [GraphQL Server Basics: The Network Layer](https://www.prisma.io/blog/graphql-server-basics-the-network-layer-51d97d21861)
- [ ] [GraphQL Server Basics: Demystifying the info Argument in GraphQL Resolvers](https://www.prisma.io/blog/graphql-server-basics-demystifying-the-info-argument-in-graphql-resolvers-6f26249f613a)
- [x] [Greenfield Project](https://en.wikipedia.org/wiki/Greenfield_project)
- [ ] [Começando com fetch no Javascript](https://blog.alura.com.br/comecando-com-fetch-no-javascript/)
- [ ] [Introduction to fetch(   )](https://developers.google.com/web/updates/2015/03/introduction-to-fetch)
- [ ] [High-order components](https://reactjs.org/docs/higher-order-components.html)
- [ ] [Functional reactive programming](https://en.wikipedia.org/wiki/Functional_reactive_programming)
- [ ] [GraphQL concepts visualized](https://blog.apollographql.com/the-concepts-of-graphql-bc68bd819be3)
- [ ] [GraphQL explained - How GraphQL turns a query into a response](https://blog.apollographql.com/graphql-explained-5844742f195e)
- [ ] [Busca em largura](https://pt.wikipedia.org/wiki/Busca_em_largura)
- [ ] [React + Apollo Tutorial](https://www.howtographql.com/react-apollo/0-introduction/)
- [ ] [GraphQL + NodeJs Tutorial](https://www.howtographql.com/graphql-js/0-introduction/)

### Palestras e Vídeos

- [ ] [React.js Conf 2015 - Data fetching for React applications at Facebook](https://www.youtube.com/watch?v=9sc8Pyc51uU)

- [ ] [GraphQL - The Documentary](https://www.youtube.com/watch?v=783ccP__No8)

- [ ] [REST vs GraphQL : Critical Look](https://www.youtube.com/watch?v=yLf0rIaRtRc)

- [ ] [GraphQL, Array e impedindo que a tela desligue com JS](https://www.youtube.com/watch?v=vtbyOxmrMpk)]

- [ ] [Dan Schafer - GraphQL at Facebook at react-europe 2016](https://www.youtube.com/watch?v=etax3aEe2dA)

- [ ] [Robert Zhu - Realtime React Apps with GraphQL - React Conf 2017](https://www.youtube.com/watch?v=AYbVMNtO-ro)

- [ ] [Lessons from 4 Years of GraphQL](https://www.youtube.com/watch?v=zVNrqo9XGOs)

### Ferramentas e Recursos

- [graphql-up](https://www.npmjs.com/package/graphql-up)
- [How to GraphQL choose tutorial](https://www.howtographql.com/choose/)
- [Build a GraphQL server from scratch](https://www.prisma.io/docs/tutorials/-nahgaghei6)
- [Netflix Falcor](https://github.com/Netflix/falcor)
- [GraphQL Playground](https://github.com/prisma/graphql-playground)
- [GraphiQL](https://github.com/graphql/graphiql)
- [Dataloader](https://github.com/graphql/dataloader)


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

### Big Picture (Architecture)

Na verdade o GraphQL nasceu como uma especificação, o longo documento de texto que descreve como um cliente e uma servidor deveriam se comportar.

Existem três casos de uso principais para o GraphQL:
1. Um servidor GraphQL conectado a um banco de dados
2. Um servidor GraphQL integrado a um sistema existente
3. Um híbrido dos dois casos

#### Caso de uso 1

- Bastante presente em greenfield projects (Um projeto totalmente novo, sem código legado)
- Utiliza um servidor web que implementa a especificação
- O servidor irá resolver a query e retornar a resposta para o cliente
- O GraphQL é agnóstico quanto ao protocolo utilizado ou quanto ao banco de dados utilizado

#### Caso de uso 2

- Comum em projetos legados, ou que já possuem uma infraestrutura com diferentes APIs
- Nesse caso o GraphQL pode ser usado para unificar sistemas existentes, escondendo a complexidade da manipulação dos dados
- O servidor não se importa qual será a fonte dos dados (banco de dados, web services, 3rd party APIs, ...)

#### Caso de uso 3
- É a combinação dos dois casos


#### Resolver Function
O elemento principal do funcionamento do GraphQL é o conceito de **resolver functions**, através dele será possível recuperar os dados de **um determinado campo** seguindo uma lógica

#### Diferenças entre data fetching imperativo e declarativo

##### Imperativo
1. Construímos e enviamos o request https
2. Recebemos e parseamos a resposta do servidor
3. Armazenamos localmente as informações
4. Representamos essas informações na interface

##### Declarativo
1. Declaramos nossos requisitos de dados
2. Representamos essas informações na interface

Tudo que acontece entre o 1 e o 2 é de responsabilidade do cliente e do servidor GraphQL.

### Advanced Tutorials - Client

Infraestrutura que gostariamos de ter em um app qualquer:
- Fazer queries e mutations sem ter que criar um request HTTP complexo
- Integração com a camada de visualização
- Estratégia de cache
- Validar e otimizar queries baseado no nosso esquema

Embora essas atividades possam ser feitas pelo desenvolvedor, o GraphQL facilita a abstração dessas tarefas, evitando excesso de trabalho manual, assim podemos focar no que realmente é importante.

Existem atualmente dois clientes para o GraphQL:
1. [Apollo Client](https://github.com/apollographql/apollo-client) : Uma alternativa open-source, mantida pela comunidade. Tem implementação para a maioria das plataformas de frontend
2. [Relay Client](https://relay.dev): Cliente criado pelo Facebook, com diversas otimizações

#### Directly Sending Queries and Mutations

Antigamente tinhamos que utilizar o `XMLHttpRequest` ou `fetch` para consumir algum recurso de uma API. Vamos delegar essa função para o GraphQL, iremos declarar nossos requisitos de dados através de uma query, e deixar que o sistema cuide do resto para nós. Essa será a tarefa do Cliente.

#### View layer integrations & UI updates

Após solicitar os dados do servidor e recebermos a resposta, teremos de alguma forma apresentar esses dados na interface. Existirá bastante variação nas estratégias que cada framework. Os que mais se saem bem nessa tarefa são os frameworks que se apoiam no paradigma funcional reativo.



#### Caching query results: concepts and strategies

Existem diversas estratégias de cacheamento, a mais simples seria colocar o resultado das queries em algum esquema de armazenamento, e caso essa query tente ser executada novamente, o conteudo cacheado será utilizado. O problema é que essa estratégia se torna bastante ineficiente com o tempo.

Devido ao dinamismo das consultas que o cliente pode fazer, nada garante que o resultado que foi cacheado na primeira consulta será reutilizado em algum momento posterior. Teríamos que ter uma abordagem um pouco mais complexas, mas pensando que ainda teremos um ORM em alguma ponta da nossa estrutura, que já pode ter sua própria estratégia de cache, a ausência de uma estratégia direto no graphQL pode não ser tão problemática.

Por fim, uma outra abordagem seria normalizar esses dados e utilizar um identificador global único para se refererir a esses elementos.

### Advanced Tutorials - Server

O GraphQL não descreve apenas um esquema e uma linguagem de consulta para esse esquema, mas também um algoritmo de como transformar a consulta em um resultado efetivo. O processo é o seguinte: A query é percorrida campo a campo, executando funções resolvers para cada campo.

Considere o seguinte esquema:

```
type Query {
  author(id: ID!): Author
}

type Author {
  posts: [Post]
}

type Post {
  title: String
  content: String
}
```

Com esse esquema definido, podemos mandar a seguinte query:
```
query {
  author(id: "abc") {
    posts {
      title
      content
    }
  }
}
```

E cada campo está associado unicament a um tipo:
```
query: Query {
  author(id: "abc"): Author {
    posts: [Post] {
      title: String
      content: String
    }
  }
}
```

A resolução dessa query seguirá a ideia de Breadth-first (Busca em largura), resolvendo primeiro `Query.author`, pegando o resultado e passando para o resolver `Author.posts` . Seria algo semelhante a seguinte execução:

```javascript
Query.authors(root, {id: 'abc'}, context) -> author
Author.posts(author, null, context) -> posts
for each post in posts
	Post.title(post, null, context) -> title
	Post.content(post, null, context) -> content

# Existem uma estrutura nesses resolvers:
#
# TipoPai.tipoFilho(raizDaBuscaTipPai, atributosTipoPai, contextoDaBusca) -> tipoFilho
```

Quando todas as resoluções são executadas os dados serão colocados em um resultado formatado e retornado.

#### Batched Resolving

Ao fazer uma consulta no nosso backend isso pode desencadear chamadas sucessivas para nosso banco de dados que serão iguais. Considere a seguinte query:

```grahql
query {
	posts {
		title
		author {
			name
			avatar
		}
	}
}
```

 Se um mesmo autor, com por exemplo`id = 1`, tiver mais de um post, iremos gerar várias buscas repetidas no banco:

```javascript
fetch('/authors/1')
fetch('/authors/1')
fetch('/authors/2')
fetch('/authors/3')
fetch('/authors/1')
fetch('/authors/2')
```

A forma de evitar esse problema seria preparar todos os fetchs, colocando o ID dos autores em uma lista que não permite duplicidade. Isso permitiria que os registros fossem buscados apenas 1 vez cada.

### Advanced Tutorials - More GraphQL Concepts

#### Enhancing Reusability with Fragments 
Fragmentos são são trechos do nosso sistema de tipos que podem ser reaproveitados, com o intuito de diminuir a quantidade de declarações que precisamos fazer. Um tipo `User` poderia ter um fragmento chamado `addressDetails`:

```graphql
type User {
  name: String!
  age: Int!
  email: String!
  street: String!
  zipcode: String!
  city: String!
}

fragment addressDetails on User {
  name
  street
  zipcode
  city
}
```

Com isso podemos fazer uma query da seguinte forma:

```
{
	allUsers {
		addressDetails
	}
}
# Em vez de
{ 
	allUsers {
		name
		street
		zipcode
		city
	}
}
```

Também podemos passar parâmetros para nossas queries durante a pesquisa:

```graphql
# Fazendo named query com parâmetros 
{
	moreThan10: allUsers(olderThan: 10): [Users!]!
	moreThan20: allUsers(oltherThan: 20): [Users!]!
}

# Podemos te um valor default caso o campo não seja passado

type Query{
	allUsers(olderThan: Int = 16): [Users!]!
}
```

#### Advanced SDL

No GraphQL temos dois conjuntos de tipos que podemos usar para contruir no schema:

1. Tipos escalares: Representam unidades concretas de dados. Podem ser: String, Int, Float, Boolean e ID
2. Tipos objetos: São tipos compostos pela composição de objetos e escalares

Existe ainda os conceitos de Enum e interfaces. No primeiro podemos representar tipos de dados fixos que estão definidos em um conjunto de valores, por exemplo:

```graphql
enum Months {
	January
	February
	March
	April
	...
}
```

No segundo podemos descrever um conjunto de tipos abstratos que devem estar presentes em um tipo concreto que implemente essa interface:

```
interface User {
	id: ID!
	email: String!
}

type Section {
	name: String!
}

type Moderator implements User {
	id: ID!
	email: String!
	sectionsToModerate: [Section!]!
}
```

Além desses dois conceitos úteis para modelar nossos tipos, ainda temos as `union`, que nos permitem definir tipos concretos que podem ter um tipo interno opcional. Importante dizer que o graphQL **não possui um tipo Date** nativo. 



### Advanced Tutorials - Tooling and Ecosystem

O cliente tem a capacidade de perguntar para o servidor do GraphQL sobre sua estrutura interna, ou seja, requisitar metadados. Esse processo é conhecido com **introspecção**. Um exemplo disso é a seguinte query:

```graphql
query {
  __schema {
    types {
      name
    }
  }
}
# E seu retorno
{
  "data": {
    "__schema": {
      "types": [
        {
          "name": "Query"
        },
        {
          "name": "Author"
        },
        {
          "name": "Post"
        }
        ...
}
```

Esse tipo de funcionalidade é realmente muito útil, diversas ferramentas do ecossistema do graphQL fazem uso disso para gerar documentação, autocomplete, geração de código e etc. Dos exemplos de ferramentas que fazem intenso uso disso são o [GraphQL Playground](https://github.com/graphcool/graphql-playground) e o [GraphiQL](https://github.com/graphql/graphiql/blob/master/packages/graphiql#readme).

.

### Advanced Tutorials - Security

Existem diversas estratégias para proteger nosso servidor GraphQL de queries maliciosas ou muito complexas.  Nenhuma das abordagem é infalível, algumas se apoiam em heurísticas básicas ou um conhecimento prévio da modelagem do sistema. A definição precisa de cada estratégia pode ser encontrada [aqui](https://www.howtographql.com/advanced/4-security/).

Temos como possiveis estratégias:

1. Timeout
2. Limitar a profundidade máxima de cada query
3. Atribuir pontuações quanto a complexidade de uma query
4. Regulação manual do número de requisições (Throttling)
   1. Baseado no tempo de execução no servidor
   2. Baseado na complexidade da operação 

O github utiliza essa abordagem para limitar as consultas na sua API pública feita com GraphQL. Mais sobre isso nesse [link](https://developer.github.com/v4/guides/resource-limitations/)

### Advanced Tutorials - Common Questions

Os principais pontos de atenção são:

1. GraphQL é uma query language para API's, não para banco de dados.
2. O GraphQL é agnostico quanto a tecnologias, ele não passa de uma especificação. A maioria das linguagens terão suas respectivas implementações da especificação.
3. Server-side caching é muito complicado de manter, se comparado ao padrão REST. Isso se deve a capacidade que o endpoint tem de alterar a estrutura dos dados que serão devolvidos.
4. É possível utilizar processos de autenticação e autorização junto com o GraphQL.
5. Quando uma operação da errado um segundo root no json de resposta será criado, com o nome de `errors`.