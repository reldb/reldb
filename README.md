# rel - The Backend Framework You'll Enjoy Using

Building backends for production applications is always a cumbersome and repetetive task. Adding Authentication, DB persistence, search, file storages, images, etc is always the same. So why can't we generate this automagically?

For the last several years I've been using Graph databases as my primary DB persistence. Cypher is a magical query language and offers so much more than SQL does.

Combining these two concepts is Rel: Cypher based persistence + Generative GraphQL API.

Only recently with the introduction of redis-graph does this become feasible. Neo4j was a great early-stage entrant but the costs associated with hosting (multiple) databases is cost-prohibitive for early stage projects. Now, we can have a persistence layer for around $5/month.

Our goal is to apply the same feel of a React/Vue/Next.js project to the backend. We want to have you up and running in minutes without the repetetion.

# Documentation

Visit [https://rel.run](https://rel.run) to view the full documentation.

# Quickstart

Run `npx create-rel-app` to initialize a new project.

This will run your though a few questions about your project and generate a runnable server.

Once finished, you will have the following project structure:

```
./myapp
│
├── schema
│   └── ...
├── server.ts
├── package.json
├── relconfig.json
├── tsconfig.json
└── Dockerfile
```

Add new models in ./models

```
// ./models/Book.ts

import Rel from "@reldb/run"

export default Rel.model({
  name: Rel.string().required(),
  slug: Rel.slug({ from: "name" })
  // ... add other fields
})
```

Add endpoints in ./api

```
// ./api/hello.ts

import Rel from "@reldb/run"

export default Rel.query("Hello", {}, Rel.string())
  .resolver(() => {
    return "Hello, World!"
  })
```

Then run your project:

```
rel dev
```

This will run a GraphQL server with the following schema:

```
type Query {
  FindBook(where: BookWhere): Book
  ListBooks(where: BookWhere): [Book]!
  
  Hello: String
}

type Mutation {
  CreateBook(input: BookInput!): Book
  UpdateBook(id: UUID!, input: BookInput!): Book
  DeleteBook(id: UUID!): Book
}
```
