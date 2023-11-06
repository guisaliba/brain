O algoritmo de Dijkstra é um método de busca em grafos que encontra o caminho mais curto entre um vértice (nó) inicial e todos os outros vértices do grafo. Ele foi criado pelo cientista da computação holandês Edsger Dijkstra em 1956.

O algoritmo é iterativo, ou seja, ele trabalha com os nós aos poucos, adicionando-os ao conjunto solução até que todos os nós tenham sido visitados. Para cada nó, o algoritmo calcula a distância à partir do nó inicial e adiciona-o ao conjunto solução se a distância calculada for menor que a distância armazenada (distância mínima).

O algoritmo de Dijkstra segue os seguintes passos:

1.  Selecione o nó inicial e atribua a ele a distância 0.
2.  Para cada nó adjacente ao nó selecionado, calcule a distância a partir desse nó e compare-a à distância armazenada. Se for menor, atualize a distância e guarde o nó anterior.
3.  Selecione o nó não visitado com a menor distância e repita os passos 2 e 3 até que todos os nós tenham sido visitados.

Um exemplo de problema que poderia ser resolvido usando o algoritmo de Dijkstra é encontrar a rota mais curta entre dois pontos de um mapa. Por exemplo, considere o seguinte mapa:

![https://upload.wikimedia.org/wikipedia/commons/5/57/Dijkstra_Animation.gif](https://upload.wikimedia.org/wikipedia/commons/5/57/Dijkstra_Animation.gif)

Usando o algoritmo de Dijkstra, podemos encontrar a rota mais curta entre o vértice A e o vértice F. Primeiro, definimos o vértice A como o vértice inicial e atribuímos a ele a distância 0. Então, para cada nó adjacente ao nó A (B, C, D e E), calculamos a distância a partir de A e comparamos com a distância armazenada. Se for menor, atualizamos a distância e guardamos o nó anterior. Nesse caso, a distância para o nó B é de 7, para o nó C é de 9, para o nó D é de 14 e para o nó E é de 9.

Em seguida, selecionamos o nó não visitado com a menor distância (C), repetimos os passos 2 e 3 e, assim, encontramos a rota mais curta entre A e F.

Com isso, concluímos que a rota mais curta entre A e F é **A-C-F**, com uma distância total de **11**.

Assim, concluímos que o algoritmo de Dijkstra é uma ótima ferramenta para encontrar o caminho mais curto entre um vértice inicial e todos os outros vértices de um grafo. Ele é amplamente usado em serviços de navegação, como o Google Maps, para encontrar rotas entre dois pontos.

#alg #logic 