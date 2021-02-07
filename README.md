# Rel DB

Rel is a semi-opinionated, [cypher-based](http://www.opencypher.org/) graph database as a service, with automatic [GraphQL](https://graphql.org/) generation and type definitions.

## Introduction - Why are we here?

I'm not sure the last time you got to work in the frontend world of JS but the framework ecosystem is highly robust. 

Why is it that backend frameworks stop at the metal/middleware layer?  

Enter Rel: The domain-first, NoSQL + relational framework.

## Domain first approach

Building backend services requires a good head when it comes to domain modeling. Understanding how data relates is the first step in designing a robust system.

But this is where modern server frameworks leave off. Rel is designed to be a schema-first approach to backend services. 

Building and launching a serice is about as easy as it gets:

```
import Server, { Schema } from "@rel/server"

const schema = {
  Person: {
    fields: {
      name: Schema.string().required(),
    },
    accessors: {
      find: {
        findBy: ["name"],
      },
      list: true,
    },
  },
  Movie: {
    fields: {
      title: Schema.string().required(),
      tagline: Schema.string(),
    },
    accessors: {
      find: true,
      list: true,
    },
  },
}

Server.start({
  schema,
})

const PORT = process.env.PORT || 4000
console.log(`Rel server running on localhost:${PORT}`)
```

## Why not use a Headless CMS?

There are some great options out there but most fall down when it comes to relational data. 

No, not relational as in a SQL-based relational DB. Relational as in having complex relationships between data.

Modern applications need a robust relational layer between objects and the users acting in the system. Otherwise, content is really just static.

## Under the hood

Rel DB is designed to act as a service in front of [redis-graph](https://oss.redislabs.com/redisgraph/). 

Through a plugin ecosystem Rel will handle all of the following for you:

 - Authentication via Auth0
 - Images via ImgIX
 - Video via Mux
 
