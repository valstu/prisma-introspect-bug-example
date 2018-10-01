# prisma-introspect-bug-example
Repo for reproducing Prisma introspect bug

To preproduce described issuer follow these steps:

1. Run `docker-compose up -d`
2. Wait a sec and test that prisma is up and running by checking out `http://localhost:4466`;
3. Go back to console, run `prisma introspect`. You probably get error `Could not connect to database. Prisma Config doesn't have any database connection``

Running `prisma introspect -i` and filling in the credentials from `docker-compose.yml` file works just fine. Although introspect 
fails to write the `datamodel-xxxx.prisma` filename to `prisma.yml` and you will get following error:


```
Created 1 new file:    GraphQL SDL-based datamodel (derived from existing database)

  datamodel-1538410125550.prisma

 ▸    Cannot read property 'datamodel' of undefined
```

Which most likely to this line here
https://github.com/prisma/prisma/blob/06304e5f6e13174cadc05be94ecbcb104d43d032/cli/packages/prisma-cli-core/src/commands/introspect/introspect.ts#L113
