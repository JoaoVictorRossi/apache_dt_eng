# Outros Recursos Úteis
## Spark SQL
Utilizar a linguagem SQL para transformar dados no PySpark.
````
from pyspark.sql import SparkSession

spark = SparkSession.builder.appName("ExemploSparkSQL").getOrCreate()

data = [("João", 30), ("Maria", 25), ("Pedro", 35)]
columns = ["Nome", "Idade"]
df = spark.createDataFrame(data, columns)

# Registrando o DataFrame como uma tabela SQL temporária
df.createOrReplaceTempView("pessoas")

# Consultando com SQL
resultado_df = spark.sql("SELECT Nome, Idade FROM pessoas WHERE Idade > 30")
````
## Dataframe functions
### Agregações
````
from pyspark.sql.functions import count, sum, avg, min, max

# Conta quantidade de linhas
df.groupby("coluna").agg(count("coluna")).show()

# Soma valores
df.groupby("coluna").agg(sum("valor")).show()

# Média dos valores
df.groupby("coluna").agg(avg("valor")).show()

# Valor mínimo e máximo
df.groupby("coluna").agg(min("valor"), max("valor")).show()
````
### Manipulação de String
````
from pyspark.sql.functions import concat, substring, length, upper, lower, trim

# Remove espaços em branco no início e no fim
df.withColumn("trimmed_name", trim(df["name"])).show()

# Converte para maiúsculas ou minúsculas.
df.withColumn("name_upper", upper(df["name"])).show()

# Retorna o comprimento de uma string.
df.withColumn("name_length", length(df["name"])).show()

# Extrai uma parte de uma string([inicio, fim]).
df.withColumn("short_name", substring(df["name"], 1, 5)).show()

# Concatena várias colunas de texto.
df.withColumn("full_name", concat(df["first_name"], df["last_name"])).show()

````
### Condição e Lógica
````
from pyspark.sql.functions import when, col

# Mesmo que WHEN CASE no SQL
df.withColumn("age_group", when(df["age"] > 18, "Adulto").otherwise("Menor")).show()

# Referência de coluna do DF
df.withColumn("double_age", col("age") * 2).show()
df.filter(col("age").isNull()).show()
df.filter(col("age").isNotNull()).show()
````

### Funções de Janela (Window)
````
from pyspark.sql import Window
from pyspark.sql.functions import row_number

# Atribui um número de linha exclusivo a cada linha dentro de uma partição.
windowSpec = Window.partitionBy("category").orderBy("value")
df.withColumn("row_num", row_number().over(windowSpec)).show()
````

### Controle de NULLs
````
from pyspark.sql.functions import coalesce

# Retorna o primeiro valor não nulo entre várias colunas.
df.withColumn("first_non_null", coalesce(df["col1"], df["col2"], df["col3"])).show()

````
---
**[Voltar](./pyspark.md)** 