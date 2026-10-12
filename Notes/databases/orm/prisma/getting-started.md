## Iniciando o Prisma num projeto

Inicializar o Prisma em um projeto é bem fácil e intuitivo. O Prisma possui sua própria CLI, a qual facilita a experiência do usuário em utilizar comandos prisma através do próprio terminal.

Em primeiro lugar, é extremamente preferível que estejamos utilizando TypeScript em nosso projeto o qual gostaríamos de integrar o Prisma. O Prisma funciona muito melhor com o TypeScript e ter seu projeto escrito utilizando-o é quase um requerimento obrigatório.

Então, antes de tudo, instale e inicialize o TypeScript no projeto:

```bash
$ npm init -y
```

Inicializa o arquivo ************************package.json************************ no projeto com a flag -y (para preencher todas as perguntas).

```bash
$ npm install typescript ts-node @types/node --save-dev
```

Esse comando instala o TypeScript e suas tipagens para o Node.js como devDependencies.

```bash
$ npx tsc --init
```

Por fim, inicializa o TypeScript no projeto.

Tendo isso feito, basta instalar agora a CLI do Prisma:

```bash
$ npm install prisma --save-dev
```

Esse comando instala a CLI do Prisma como uma devDependency.

Agora, com a CLI do Prisma disponível, podemos começar a utilizar os comandos que ela disponibiliza ao usuário. Primeiramente, precisamos criar um arquivo prisma.schema e dizer ao Prisma qual banco de dados usaremos em nosso projeto:

```bash
$ npx prisma init --datasource-provider sqlite
```

Nesse caso, esse comando está inicializando o Prisma com um banco de dados SQLite.

Pronto, agora o Prisma está inicializado no projeto. Muito provavelmente será possível ver uma nova pasta criada nos arquivos do projeto e dentro dela um arquivo **prisma.schema**, o qual será o arquivo aonde modelaremos nossas tables do banco.

Após termos criado pelo menos um **Model** (que será convertido em uma table) em nosso arquivo prisma.schema, ainda não criamos de fato um banco de dados. O Prisma precisa criar as tables a partir dos Models presentes no prisma.schema, e para isso, é necessário o seguinte comando:

```bash
$ npx prisma migrate dev --name init
```

O que esse comando está fazendo é chamado de **Migration**. Uma migration é como se fosse um **snapshot** do arquivo prisma.schema, aonde estão os Models que são convertidos em tables. Quando inicializamos o Prisma num projeto pela primeira vez, **precisamos** rodar uma migration para que o Prisma converta seu schema num banco de dados **real**.

**Toda alteração feita no prisma.schema** após a primeira migration **necessita que outra migration seja feita novamente**, para que outro snapshot do banco de dados seja convertido e **gravado**.

Agora que o Prisma está devidamente inicializado e configurando no projeto, já é possível executarmos queries ao nosso banco de dados com o **PrismaClient**.

Todos os registros inseridos nas tables através do PrismaClient podem ser vistos no **Prisma Studio**.