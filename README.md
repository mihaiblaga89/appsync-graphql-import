# graphql-import

[![npm version](https://badge.fury.io/js/@mihaiblaga89/appsync-graphql-import.svg)](https://badge.fury.io/js/graphql-import)

Import &amp; export definitions in GraphQL SDL (also refered to as GraphQL modules)

*Forked from https://github.com/ardatan/graphql-import since that seems to not be maintained anymore and I needed a way for AppSync's GQL tags to work with this*

## Features
1. same as https://github.com/ardatan/graphql-import
2. added support for `@searchable`, `@model` and `@aws_auth`

## Install

```sh
yarn add @mihaiblaga89/appsync-graphql-import
```

## Usage

```ts
import { importSchema } from 'graphql-import'
import { makeExecutableSchema } from 'graphql-tools'

const typeDefs = importSchema('schema.graphql')
const resolvers = {}

const schema = makeExecutableSchema({ typeDefs, resolvers })
```

Assume the following directory structure:

```
.
├── schema.graphql
├── posts.graphql
└── comments.graphql
```

`schema.graphql`

```graphql
# import Post from "posts.graphql"

type Query {
  posts: [Post]
}
```

`posts.graphql`

```graphql
# import Comment from 'comments.graphql'

type Post {
  comments: [Comment]
  id: ID!
  text: String!
  tags: [String]
}
```

`comments.graphql`

```graphql
type Comment {
  id: ID!
  text: String!
}
```

Running `console.log(importSchema('schema.graphql'))` produces the following output:

```graphql
type Query {
  posts: [Post]
}

type Post {
  comments: [Comment]
  id: ID!
  text: String!
  tags: [String]
}

type Comment {
  id: ID!
  text: String!
}
```

