O Prisma trabalha com um arquivo **schema**. Nesse arquivo é onde declaramos nossos **Models** (modelos) que servirão como nossas **tables** (tabelas) uma vez que nosso schema esteja conectado a um banco de dados.

Toda vez que o Prisma for inicializado em um projeto ele criará um arquivo **prisma.schema**. Esse arquivo nos permite definir nossos modelos numa aplicação de forma bem intuitiva. Isso quer dizer que, podemos modelar nossos dados fora do padrão comum dos bancos de dados SQL e NoSQL.

Esse arquivo também contém a ligação a uma banco de dados e define um gerador:

```sql
datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

generator client {
  provider = "prisma-client-js"
}

model Post {
  id        Int     @id @default(autoincrement())
  title     String
  content   String?
  published Boolean @default(false)
  author    User?   @relation(fields: [authorId], references: [id])
  authorId  Int?
}

model User {
  id    Int     @id @default(autoincrement())
  email String  @unique
  name  String?
  posts Post[]
}
```

Nesse arquivo **prisma.schema**, configura-se três coisas:

- **Datasource**: Declara a **ligação** à base de dados (através de uma variável de ambiente).
- **Generator**: Indica que queremos gerar um **PrismaClient**.
- **Data model**: Define os **Models** (modelos) da nossa aplicação.