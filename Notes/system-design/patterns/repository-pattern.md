O repository pattern é um padrão de design de um sistema que implementa uma camada de abstração no sistema entre a camada responsável pela regra de negócios e a camada de dados (database). Esse design é utilizado em um sistema quando o objetivo é fazer com que a camada que manipula as informações não necessariamente precise saber quais são os métodos/ações da aplicação para alterar esses dados.

Temos um exemplo simples num sistema de C.R.U.D. (Create Read Update Delete) onde uma das camadas desse sistema performa essas operações de inserção, deleção, atualização etc. Nesse sistema, ao implementar o design do Repository Pattern, a camada que manipula os dados do sistema não saberia o que acontece para se inserir uma nova informação, alterar ou deletá-la.

Ainda nesse exemplo, o que a camada de manipulação saberia e teria acesso seria somente as informações em si. A responsabilidade de performar operações com esses dados se transfere para o Repository, e não mais para a camada de manipulação, por exemplo, um Controller.

Visualizando o design de um sistema que não implementa esse padrão, temos algo assim:

``` 
	Controller <--> Data source
```

Aqui, o Controller tem acesso direto à fonte de dados e ele mesmo performa os métodos para se alterar as informações dessa fonte, tais como insert, edit, delete, etc.

Já em um sistema que o Repository Pattern é implementado, podemos enxergar algo dessa forma:

```
	Controller <--> Repository (operations) <--> Data source
```

Nesse sistema, a camada responsável pelos métodos citados acima como exemplo é a camada do Repository, e não mais a camada de manipulação, o Controller. Ainda nesse caso, o Controller faz requisições à camada de abstração (Repository), que por sua vez realiza as operações que dizem respeito à base de dados (data source).