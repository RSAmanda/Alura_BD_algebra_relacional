# Modelagem de banco de dados relacional: Álgebra relacional

# Link do Curso

[](https://cursos.alura.com.br/course/modelagem-banco-dados-algebra-relacional)

# Materiais de Apoio

## Download Software Relational

[Relational](https://ltworf.github.io/relational/)

## Dicas para a instalação:

[Relational não abre no windows | Fórum Alura](https://cursos.alura.com.br/forum/topico-relational-nao-abre-no-windows-243052)

## Base de dados

**Aula 1**

[livros.csv](Modelagem%20de%20banco%20de%20dados%20relacional%20A%CC%81lgebra%20re%2025d8490dce044ff094fa7d5a2aff6488/livros.csv)

[vendedores.csv](Modelagem%20de%20banco%20de%20dados%20relacional%20A%CC%81lgebra%20re%2025d8490dce044ff094fa7d5a2aff6488/vendedores.csv)

[vendas.csv](Modelagem%20de%20banco%20de%20dados%20relacional%20A%CC%81lgebra%20re%2025d8490dce044ff094fa7d5a2aff6488/vendas.csv)

**Aula 3**

[livros_novo.csv](Modelagem%20de%20banco%20de%20dados%20relacional%20A%CC%81lgebra%20re%2025d8490dce044ff094fa7d5a2aff6488/livros_novo.csv)

# Aulas

## Apresentação e Instalação

A **álgebra relacional** é uma derivação da álgebra de conjuntos em relação às operações. Ela ajuda a identificar os componentes de uma tupla por nome (chamado o atributo) ao invés de uma coluna de chaves numéricas, na qual é chamada a relação na terminologia de banco de dados.

*Software* utilizado no curso: **Relational.**

O Relational é uma ferramenta educacional, que permite o trabalho com a álgebra relacional. Além de ter uma interface bastante intuitiva, que facilita fazer testes, consultas e expressões. 

## Seleção e Projeção

A **Operação de seleção** nos retorna tuplas que satisfazem uma condição. Ou seja, precisamos de um filtro para que a seleção nos retorne o resultado desejado. Ela traz as tuplas que satisfazem as condições e descarta as demais.

Na terminologia de bancos de dados relacionais, "tupla" significa "linha", ou seja, a **tupla** é um registro na tabela. Já os cabeçalhos das colunas são chamados de **Atributos.** Todo conjunto que forma a tabela é chamado de **Relação ou Entidade**.

### Sintaxe da fórmula da operação de seleção

```
σ <condicao_selecao>(R)
```

O símbolo sigma `σ` é usado para representar a seleção. A `<condicao_selecao>` é onde colocaremos a condição para que as tuplas sejam retornadas. Já o `(R)` é onde informaremos a tabela em que buscaremos a condição de seleção.

Dentro da condição de seleção, temos ainda algumas cláusulas que precisamos entender para continuar. São elas: o `<nome_atributo>`, que é o nome da coluna; o `<operador_comparacao>`, referente aos operadores, igual (=), maior que (>), menor que (<), maior ou igual (≥), menor ou igual (≤) e diferente (!=); e o `<valor_constante>`, que é o valor que adicionaremos para buscar as tuplas.

### Sintaxe da fórmula da operação projeção

```
π <lista_atributos> (R)
```

O símbolo "pi (π)" é indicado para representar a projeção. Já a `<lista_atributos>` são as colunas que desejamos trazer. O `(R)` é a entidade, ou seja, a tabela que estamos buscando na lista de atributos. Vamos até o Relational verificar como isso funciona!!

Diferentemente da seleção, que seleciona algumas linhas e remove outras, a projeção seleciona algumas colunas e remove outras. Tanto a seleção quando a projeção não trazem tuplas repetidas. 

A operação de projeção é muito interessante para trazer apenas colunas selecionadas, mas também podemos utilizá-la com outras operações da álgebra relacional, em consultas mais robustas. Agora que Arthur, por meio da Josefina, conseguiu entender como funciona a projeção e seleção, quais serão os próximos desafios? Vamos acompanhar nos próximos vídeos!!

## União, Interseção e Diferença

### Sintaxe da fórmula da operação união

União é a junção de duas relações, independentemente do que esteja na relação 1 e na relação 2.

```
π nome_livro (livros) U π nome_livro (livros_novo)
```

O símbolo  `U` representa a união

Com isso, podemos unir os nomes de livros da tabela ‘livros’ e ‘livros_novo’.

### Sintaxe da fórmula da operação interseção

A interseção retorna o que há em comum entre duas tabelas. Para fazer a interseção entre os livros no estoque e os livros vendidos, precisamos primeiramente declarar uma variável temporária com a união das duas listas de livros:

```
livros_estoque = π nome_livro (livros) U π nome_livro (livros_novo)
```

Em seguida, realizar a interseção entre a variável temporária e a lista de nomes de livros da tabela vendas

```
livros_estoque ∩ πnome_livro (vendas)
```

### Sintaxe da fórmula da diferença de conjuntos

A **diferença de conjuntos** nos permite encontrar tuplas que estão em uma relação, mas não em outra.

Assim conseguindo extrair do livros em estoque os nomes de livros que não foram vendidos (ou seja, nomes de livros que não estão listados na tabela de vendas).

```
livros_estoque - π nome_livro (vendas)
```

## Produto Cartesiano e Junção

### Produto Cartesiano

O produto cartesiano é representado pela letra "X" (ou * no Relational )que é o símbolo da multiplicação. O **produto cartesiano** retorna todas as combinações de tuplas de duas relações, formando assim uma terceira relação contendo todas as **combinações** possíveis entre os elementos das relações originais.

```
vendedores * vendas
```

### Junção

A **junção**, que é representada pelo símbolo da gravata borboleta, **⋈**, é a operação que simplifica o produto cartesiano. Ela realiza um produto cartesiano, depois uma seleção das tuplas de interesse e, por fim, uma projeção, para remoção das colunas duplicadas.

```
vendedores ⋈ vendas
```

Quando as duas tabelas não apresentam campo em comum, o resultado da junção será igual ao do produto cartesiano, ou seja, a função não reconhece o critério de junção.

Para contornar esse problema, será necessário renomear (utilizando o rho ρ) a coluna id_vendedor_vendas (da tabela vendas) para apenas id_vendedor, para ficar igual em ambas as tabelas. E em seguida executar o comando anterior, alterando *vendas* por *vendas_novo*.

```
vendas_novo = ρ id_vendedor_vendas ➡ id_vendedor (vendas)
```

- junção esquerda: traz todas as tuplas da entidade à esquerda no resultado
    - Símbolo ⧒
- junção direita: priorizará as tuplas da tabela à direita
    - Símbolo ⧑
- junção total: faz ambas as operações
    - Símbolo ⧓

## Outras Operações

### Atribuição (→ ou =)

A **atribuição** é utilizada para designar a consulta a uma variável temporária. Ela é representada por uma seta para a esquerda. Ao atribuirmos a consulta a uma variável temporária, fica fácil utilizar essa consulta posteriormente, já que ela fica salva no Relational.

```
R =  π nome_livro(livros) U  π nome_livro(livros_novo)
```

### Renomear (ρ   ⇒)

Esta operação nos permite alterar nomes de atributos de uma relação.

```
livros_estoque = ρ autor ➡ autor_livro (livros_estoque)
```