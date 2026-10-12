O PrismaClient é o responsável por acessar os Models presentes no seu schema.prisma e expôr todos os dados ali dentro e realizar operações CRUD com eles. Em outras palavras, é o PrismaClient quem irá realizar as queries para o seu banco de dados.

Para isso, é necessário que exista pelo menos um Model definido no seu projeto.

```bash
$ npm install @prisma/client
```

O comando acima é necessário para instalar o pacote do PrismaClient. Ele disponibiliza o comando `prisma generate` que quando executado vai ler o arquivo **prisma.schema** e gerar todo o código do PrismaClient.

```bash
$ prisma generate
```

Qualquer alteração no data model, ou seja, em algum dos Models fará com que seja necessário reexecutar o comando `prisma generate.`

Pronto, agora o PrismaClient está disponivel no projeto para executar queries ao banco de dados.

Basta importá-lo no arquivo em que nossa aplicação (server) está rodando:

```tsx
import { PrismaClient } from '@prisma/client'

const prisma = new PrismaClient()
```

Agora já é possível rodar queries ao banco de dados. Perceba que todas as queries feitas com o PrismaClient retornam os bons e velhos objetos JavaScript de sempre:

```tsx
export async function server(){
	const allUsers = await prisma.user.findMany();

	const allUsers = await prisma.user.findMany({
	  include: { posts: true },
	})
}
```

Duas queries estão sendo feitas dentro da nossa função async. A primeira delas é uma query do método findMany(..) que busca por todos os dados existentes daquele objeto. A segunda é a mesma query findMany(..) que vai buscar no banco de dados todos os registros existentes no Model User, porém, com o `include: { posts: true }` a query está também retornando todos os registros do model Post relacionados ao model User.