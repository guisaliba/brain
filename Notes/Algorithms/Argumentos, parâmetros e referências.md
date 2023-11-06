### Diferença entre valor e argumento:
int soma(int a, int b)
-> a e b são dois parametros, eles possuem espaços reservados na memoria que serao preenchidos quando este método for invocado.

int r = soma(5, 3)
-> 5 e 3 sao argumentos. eles sao os valores (qualquer valor int nesse caso) que serao copiados e alocados no espaço reservado na memoria pelos parametros.

importante notar que qualquer valor (inteiro nesse caso) pode ser colocado no lugar de 5 e 3, podendo ser ate mesmo uma expressao. ex: soma((2×2), 7).

copia por valor: no exemplo acima do metodo soma() acontece uma copia por valor. quando o metodo recebe seus argumentos, o valor deles sao copiados para os parametros do metodo, que por sua vez serao responsaveis por algo no metodo.

copia por retorno: diferente da copia por valor, a copia por retorno seria o caminho inverso. no mesmo exemplo da soma() existiria um argumento de retorno (essa classe é exclusiva das linguagens .NET como o C#) que, apos ser retornado seria copiado para o argumento do metodo.

ex:
public static void int soma(int a, int b, out c) {
    c = a + b;
}

int x = 4, y = 7, r;
soma(x, y, out r);

nesse exemplo, o argumento r referencia o parametro c, e c so recebe um valor no momento que a copia por retorno é feita. nesse exemplo, r não possui um valor, APESAR de possuir espaço reservado na memória, ele na verdade possui uma referencia à c (que nao possui espaço na memória, pois é uma variável de retorno) este sim retornará um valor que r copiará para si.

vetores sao estruturas de dados homogeneas, bem como matrizes que sao vetores bidimensionais. isso quer dizer que ambos recebem somente um mesmo tipo de dado por toda sua extensão.

uma classe por sua vez é uma estrutura de dado heterogênea. ela é a definição de uma estrutura de dados, esses que podem ser de diferentes tipos desde objetos até variaveis int string etc.
