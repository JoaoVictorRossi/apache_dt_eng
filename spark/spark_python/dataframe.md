# Spark DataFrames
Principal estrutura de dados PySpark, projeto para trabalhar com grandes volumes de dados de forma distribuída.
- Estrutura semelhante ao Pandas DataFrame.
- Processamento distribuído em cluster.
- Mais eficiente e simples comparados aos RDDs.
- Possui as mesmas características de um RDD.
## Criando um DataFrame
````
from pyspark.sql import SparkSession

spark = SparkSession.builder.appName("ExemploDataFrame").getOrCreate()

# Criando um DataFrame a partir de uma lista
dados = [("João", 25), ("Maria", 30), ("Pedro", 35)]
colunas = ["Nome", "Idade"]
df = spark.createDataFrame(dados, colunas)

# Criando um DataFrame a partir de um arquivo
df_csv = spark.read.csv("dados.csv", header=True, inferSchema=True)
df_csv.show()
````
- "header=True" parametro para dizer se o arquivo csv possui ou não um header.
- "inferSchema=True" permite que o Spark detecte automaticamente os tipos das colunas.
## Principais Transformações
As transformações em DataFrames no PySpark não modificam os dados diretamente, mas retornam um novo DataFrame com as mudanças aplicadas.
| Transformação | Descrição | Exemplo |
|----------|-------|-------------|
| select(colunas) | Seleciona colunas específicas do DataFrame. | df.select("Nome").show() |
| filter(condição) | Filtra linhas com base em uma condição. | df.filter(df.Idade > 25).show() |
| withColumn(nova_coluna, expressão) | Adiciona uma nova coluna ou modifica uma existente. | df.withColumn("Idade+10", df.Idade + 10).show() |
| drop(coluna) | Remove colunas do DataFrame. | df.drop("Idade").show() |
| groupBy(coluna).agg(função) | Agrupa e aplica funções de agregação. | df.groupBy("Nome").agg({"Idade": "avg"}).show() |
| orderBy(coluna, asc/desc) | Ordena os dados. | df.orderBy(df.Idade.desc()).show() |
### Exemplos
````
from pyspark.sql.functions import col

# Selecionando apenas as colunas "Nome" e "Idade"
df.select("Nome", "Idade").show()

# Filtrando apenas pessoas com idade maior que 25
df.filter(df.Idade > 25).show()
df.where(df.Idade < 30).show()  # Alternativa ao filter()

## AND(&) , OR(|) e NOT(~) (expressão por paranteses)
despachantes.filter((col("vendas") > 20) & (col("vendas") < 40))

# Renomeando uma coluna do dataframe
df_renomeado = df.withColumnRenamed("Idade", "Anos")

# Criando ou modifica uma coluna "Idade+10"
df = df.withColumn("Idade+10", df.Idade + 10)

# Removendo uma coluna
df_sem_idade = df.drop("Idade")

# Ordenando por idade de forma decrescente
df.orderBy(col("Idade").desc()).show()

# Agregando e agrupando dados
df.groupBy("Nome").count().show()  # Conta quantas vezes cada "Nome" aparece
df.groupBy("Nome").avg("Idade").show()  # Média da idade por nome
df.groupBy("Categoria").sum("Vendas").show() # Soma de vendas
````
## Principais Action
| Nome     | Idade | Cidade       |
|----------|-------|-------------|
| show(n) | Exibe os primeiros n registros do DataFrame.    | df.show(5) |
| count() | Retorna o número total de linhas. | df.count() |
| collect() | Retorna os dados como uma lista de linhas. | df.collect() |
| first() | Retorna a primeira linha do DataFrame. | df.first() |
| describe() | Retorna estatísticas das colunas numéricas. | df.describe().show() |

## JOINs em PySpark
| Join | Descrição |
|----------|-------|
| Inner Join | 	Mantém apenas as linhas com correspondência nas duas tabelas.|
| Left Join | Mantém todas as linhas da esquerda e as correspondências da direita (valores não correspondentes na direita ficam NULL). |
| Right Join | Mantém todas as linhas da direita e as correspondências da esquerda (valores não correspondentes na esquerda ficam NULL). |
| Full Outer Join | Mantém todas as linhas de ambas as tabelas. Se não houver correspondência, valores ficam NULL. |
| Cross Join | 	Faz um produto cartesiano (todas as combinações possíveis). |
| Left Semi Join | Retorna apenas as linhas da esquerda que têm correspondência na direita, sem incluir colunas da direita. |
| Left Anti Join | Retorna apenas as linhas da esquerda que não têm correspondência na direita. |
### Exemplos
````
# Inner join
df_inner = clientes.join(compras, "id_cliente", "inner")

# Left join
df_left = clientes.join(compras, "id_cliente", "left")

# Right join
df_right = clientes.join(compras, "id_cliente", "right")

# Full outer join
df_full = clientes.join(compras, "id_cliente", "outer")

# Cross join
df_cross = clientes.crossJoin(compras)

# Left semi join
df_semi = clientes.join(compras, "id_cliente", "left_semi")

# Left anti join
df_anti = df1.join(df2, "Nome", "left_anti")
````
---
**[Voltar](./pyspark.md)**