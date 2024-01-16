O npm (Node Package Manager) é um lugar para compartilhar módulos JavaScript. Um desenvolvedor pode criar algo de utilidade ao público e decidir compartilhá-lo com todos. A esse objetivo citado, utilizamos o npm.

**O yarn funciona exatamente como o npm, porém com algumas diferenças.**

### **O que é o arquivo .lock?**

O “.lock” é um arquivo que trava a versão das dependências que são instaladas. Foi desenvolvido pelo Facebook e Google, esse arquivo garante que todas as pessoas que forem utilizar uma certa dependência vai instalar ela na versão utilizada naquele projeto.

**No yarn esse arquivo é o `yarn.lock`, no npm é o `package-lock.json`**

O comando para **instalar** uma dependência no **npm** é o `npm install` e no **yarn** é `yarn add`.

O comando para criar um package.json com yarn é `yarn init` (e sua variação `yarn init -y`

com a flag **-y** para criar uma versão simplificada do arquivo).
