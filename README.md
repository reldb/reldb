# rel - The backend for frontend developers

There has been quite the renaissance in the Javascript world over the past 10 years. New frontend tooling is pushing the boundaries of both native and web applications.

Our goal is to apply some of the foundations that have made frontend tooling successful to the backend. We want to have you up and running in minutes

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
