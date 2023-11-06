O Git possui três estágios (ou estados), que são o principal mecanismo de como tudo funciona. Esse é o conceito mais importante desse VCS. Seus arquivos podem residir em três estados diferentes: **modified**, **commited** e ************staged.************

- ********************Modified:******************** Esse estado significa que algo foi modificado nos seus arquivos/diretório porém ainda **não** foram commitados à sua database.
- ************Staged************: Um arquivo que está no estado ************staged************ é um arquivo que foi modificado e marcado como **pronto** para ser commitado e guardado no próximo snapshot do seu código.
- ********************Commited:******************** O commited significa que seu arquivo (ou mais de um) subiu para a database e está guardado em segurança. No snapshot tirado pelo Git, esses arquivos estarão lá.

Esses três estados nos introduzem ao conceito de ************************working tree************************ do Git, um fluxo de trabalho.

O fluxo de trabalho do Git é basicamente isso:

1. Você **modifica** arquivos na sua working tree.
2. Você **seleciona** à mão quais mudanças você quer que estejam no próximo commit, ou seja, você põe esses arquivos selecionados em **stage**.
3. Você faz o **commit**, que pega somente os arquivos modificados selecioandos (**staged**), e guarda um **snapshot** permanente no seu diretório Git.

Um **diretório Git** é uma pasta criada automaticamente pelo Git uma vez que você o inicializa no seu projeto. É nessa pasta que ele guarda todas as informações de mudanças, stage, commit, fluxo e **.gitignore** (um arquivo onde você diz ao Git o que ele deve **ignorar** no próximo snapshot).

#git 