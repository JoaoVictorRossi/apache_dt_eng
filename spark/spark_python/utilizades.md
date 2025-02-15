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
---
**[Voltar](./pyspark.md)** 