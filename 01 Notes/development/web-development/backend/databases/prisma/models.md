Os **Models** no Prisma (ou modelos) são a representação das **tables** (ou tabelas) dos bancos de dados relacionais (SQL) e das **coleções** do MongoDB por exemplo.

O arquivo **prisma.schema** é o arquivo aonde ficam guardados nossos modelos, esse arquivo pode ser chamado também de ********************data model********************. Um data model é uma coleção de **models** no Prisma. Um data model é responsável por:

- Representar as ******************entidades****************** da aplicação.
- Fazer um mapeamento com as tables (tabelas em bancos de dados relacionais) ou com as collections (coleções em MongoDB) no seu banco de dados.
- Formarem a fundação das queries disponíveis na API do Prisma Client.
- Quando utilizado com TypeScript, o PrismaClient provê tipagem para todos os Models no seu prisma.schema para que toda a aplicação esteja tipadamente segura.

Esse é um exemplo de um **prisma.schema** com alguns Models definidos dentro dele:

```sql
datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

generator client {
  provider = "prisma-client-js"
}

model User {
  id      Int      @id @default(autoincrement())
  email   String   @unique
  name    String?
  role    Role     @default(USER)
  posts   Post[]
  profile Profile?
}

model Profile {
  id     Int    @id @default(autoincrement())
  bio    String
  user   User   @relation(fields: [userId], references: [id])
  userId Int    @unique
}

model Post {
  id         Int        @id @default(autoincrement())
  createdAt  DateTime   @default(now())
  title      String
  published  Boolean    @default(false)
  author     User       @relation(fields: [authorId], references: [id])
  authorId   Int
  categories Category[] @relation(references: [id])
}

model Category {
  id    Int    @id @default(autoincrement())
  name  String
  posts Post[] @relation(references: [id])
}

enum Role {
  USER
  ADMIN
}
```

Uma **query** utilizando o PrismaClient feita no arquivo TypeScript da aplicação ao banco de dados que está sendo definido pelo Prisma no arquivo acima se assemelha a algo assim:

```tsx
const user = await prisma.user.create({
  data: {
    email: 'ariadne@prisma.io',
    name: 'Ariadne',
    posts: {
      create: [
        {
          title: 'My first day at Prisma',
          categories: {
            create: {
              name: 'Office',
            },
          },
        },
        {
          title: 'How to connect to a SQLite database',
          categories: {
            create: [{ name: 'Databases' }, { name: 'Tutorials' }],
          },
        },
      ],
    },
  },
})
```

Essa **query** está criando uma série de dados dentro do banco de dados através dos métodos disponíveis no PrismaClient. Ela está basicamente criando um usuário no model User. Porém, além disso, criando dois registros no model Post e três no model Category.

**O método (query)** utilizado para fazer esses registros é o `prisma.model.create(..)` onde o model é o nome do Model em que queremos criar o resgitro. Esse método está vindo diretamente do **PrismaClient** importado em algum lugar desse arquivo previamente.

Perceba como tudo isso está sendo feito como se estivéssemos escrevendo um **JSON**. O Prisma é responsável por fazer essa tradução e facilitar a manipulação de dados SQL.