Por que escrever testes?

Um código complexo não é fácil de debuggar só com olho. Os erros precisam ser identificados e resolvidos antes de ir para produção.

### Testar é uma forma de validar o software:

Funciona como eu espero?

Funciona como o usuário espera?

Se eu mexer aqui, meu código quebra?

**Testes funcionam como uma documentação primária do código para outros desenvolvedores. Ajudam muito para o dev. ter uma noção do que aquilo se trata e como funciona.**

### Que tipos de testes existem?

Os tipos de testes mais fundamentais são:

1.  Testes Unitários: testam isoladamente pequenas unidades do código, apenas um método, sempre de forma isolada. O teste unitário vê se o código está funcionando como o desenvolvedor espera.
    
2.  Testes Funcionais: checa se as unidades funcionam entre si, não mais de forma isolada. Pode analisar diversos métodos, classes, etc. O teste funcional checa se o código está funcionando como o usuário espera.

### Test-Driven Development (TDD)

A prática TDD é escrever o código baseado nos testes, ou seja, antes os testes, depois os códigos. O conceito segue o seguinte fluxo: Escrever o teste -> Fazer o teste passar (testar o código) -> Refatorar o código.

### E quais são as ferramentas para escrever testes?

Algumas delas, as mais famosas/bem avaliadas são:

-   Jest
-   Cypress (end-to end)
-   Storybook
-   Enzyme
-   Jasmine
-   Mocha

**E muitos outros…**

**O Jest é o framework de teste mais popular e satisfatório, mantido pelo Facebook (Meta).**

#tests