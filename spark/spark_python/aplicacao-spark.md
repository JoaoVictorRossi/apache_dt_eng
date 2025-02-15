# Aplicações Spack
## Módulos PySpark
- **SparkContext** é o responsável por conectar, interagir e gerenciar os recursos do cluster usando Spark.
- **SparkSession** API unificada que combina a funcionalidade do _SparkContext_ e falicita o acesso as funcionalidades do spark usando a API PySpark.

## Criando uma Aplicação (SparkSession)
````
from pyspark.sql import SparkSession

# Criando uma SparkSession
spark = SparkSession.builder.appName("NomeSparkSession").getOrCreate()

# Código PySpark ...
````
---
**[Voltar](./pyspark.md)**
