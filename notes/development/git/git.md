## 1. Introdução:

Git é um tipo de **Version Control System (VCS)** utilizado para manter o código atualizado/na versão correta, voltar atrás quando surgir um erro crítico, entre várias outras funções.

Ele é fundamental quando trabalhamos em equipe, e até mesmo sozinhos. O Git é o responsável por nos permitir interagir com o Github e organizarmos nossos arquivos e projetos.

## 2. Snapshots:

O Git funciona com **snapshots**, basicamente ele tira uma foto de todos os arquivos do seu projeto toda vez que o estado dele é alterado, seja por commits ou saves.

Para ser eficiente, o Git não tira uma foto dos arquivos caso nada tenha sido alterado.

O Git trabalha com dados como se fosse um **álbum de fotos**.

Essa é uma importante distinção do Git e de outros VCSs.

## 3. Operações locais:

A maioria das operações realizadas com o Git são feitas utilizando apenas **arquivos e recursos locais**, geralmente nenhuma informação de outro computador ou de uma rede é necessária.

Isso é possível pelo fato que todo o histórico do seu projeto está salvo no seu **disco loca**l, o Git usa vantagem disso para que as operações pareçam quase **instantâneas.**

Por exemplo, se você quiser ver as diferenças dos arquivos atuais do seu projeto e desse mesmo projeto há 1 mês atrás, o Git apenas calcula quais arquivos estavam presentes naquele momento e quais estão presentes agora.

## 4. Integridade:

Tudo no Git passa por uma **checksum** antes de ser armazenado e então essa checksum é o p**onto de referência** para todas as alterações feitas no projeto. Isso significa que é **impossível** mudar o conteúdo de um arquivo ou diretório **sem o Git saber** da existência deles.

Por causa disso, é impossível **perder** alguma informação ou ter algum arquivo **corrompido** sem o Git detectar antes de algo assim acontecer.

O mecanismo que o Git usa para fazer essas checksums é chamado de **SHA-1 hash**. É uma string de 40 caracteres de 0-9 e a-f.

Uma hash SHA-1 se parece com isso: `24b9da6552252987aa493b52f8696cd6d3b00373`.

#git