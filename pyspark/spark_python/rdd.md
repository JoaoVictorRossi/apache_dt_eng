# RDD (Resilient Distributed Dataset)
Estrutura de dados tolerante a falhas e fundamental do Apache Spark, utilizada como base para a os Dataframes.
- Se um nó do cluster falhar, os dados podem ser reconstruídos automaticamente.
- Os dados são divididos entre os nós do cluster.
- Uma vez criado, o RDD não pode ser alterado.
- As operações só são executadas quando um "action" é chamado **(Lazy Execution)**.
- Utiliza um mecanismo chamado Lineage, que permite recuperar dados perdidos sem necessidade de replicação.
## Criando um RDD

````
from pyspark.sql import SparkSession

spark = SparkSession.builder.appName("RDDExemplo").getOrCreate()

# Criando um RDD a partir de um List
dados = [1,2,3,4,5]
rdd1 = spark.parallelize(dados)

# Criando um RDD a partir de um arquivo
rdd2 = spark.textFile("dados.txt")
````

## Principais Transformações
| Função | Descrição | Exemplo |
|----------|-------|-------------|
| map(func) | Aplica uma função a cada elemento do RDD e retorna um novo RDD. | rdd.map(lambda x: x * 2) |
| filter(func) | 	Retorna um novo RDD apenas com os elementos que atendem à condição. | rdd.filter(lambda x: x > 2) |
| flatMap(func) | Similar ao map, mas "achata" a saída, retornando múltiplos valores por entrada. | rdd.flatMap(lambda x: (x, x*2)) |
| distinct() | Remove valores duplicados do RDD. | rdd.distinct() |
| union(rdd2) | Une dois RDDs. | rdd.union(outro_rdd) |
| intersection(rdd2) | Retorna os elementos comuns entre dois RDDs. | rdd.intersection(outro_rdd) |
| groupByKey() | Agrupa os valores pelo mesmo "chave" (chave-valor). | rdd_kv.groupByKey() |
| reduceByKey(func) | Aplica uma função de redução aos valores com a mesma chave. | rdd_kv.reduceByKey(lambda x, y: x + y) |
### Exemplo
````
from pyspark.sql import SparkSession

spark = SparkSession.builder.appName("RDDTransformacoes").getOrCreate()

rdd = spark.parallelize([1, 2, 3, 4, 5])

# Multiplicando cada elemento por 2
rdd_map = rdd.map(lambda x: x * 2)
print(rdd_map.collect())  # Saída: [2, 4, 6, 8, 10]

# Filtrando valores maiores que 3
rdd_filtrado = rdd.filter(lambda x: x > 3)
print(rdd_filtrado.collect())  # Saída: [4, 5]
````
## RDD principais Actions
| Ação | Descrição | Exemplo |
|----------|-------|-------------|
| collect() | Retorna todos os elementos do RDD. | rdd.collect() |
| count() | Retorna o número de elementos. | rdd.count() |
| first() | Retorna o primeiro elemento do RDD. | rdd.first() |
| take(n) | Retorna os n primeiros elementos. | rdd.take(3)  |
| reduce(func) | Aplica uma função de agregação (exemplo: soma). | rdd.reduce(lambda x, y: x + y) |
| foreach(func) | Aplica uma função a cada elemento (sem retorno). | rdd.foreach(print) |
### Exemplo
````
from pyspark.sql import SparkSession

spark = SparkSession.builder.appName("RDDActions").getOrCreate()

rdd = spark.parallelize([10, 20, 30, 40])

# Contar o número de elementos
print("Número de elementos:", rdd.count())  # Saída: 4

# Somar os elementos do RDD
soma = rdd.reduce(lambda x, y: x + y)
print("Soma dos elementos:", soma)  # Saída: 100

# Pegando os dois primeiros elementos
print("Primeiros elementos:", rdd.take(2))  # Saída: [10, 20]

````