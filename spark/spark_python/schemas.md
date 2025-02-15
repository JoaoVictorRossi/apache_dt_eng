# Schemas
Schemas são a definição de colunas de um DF spark, possibilitando definir nome, tipo de dados, e constraints de cada coluna.
## Declação Simplificada
Utilizado quando é um schema mais simples e não possui necessidades de definir schemas ou tipos de dados complexos.
````
schema = "id INT, nome STRING, salario FLOAT, data DATE, ativo BOOLEAN"
dados = [(1, "João", 15000.5, "12/06/2004", True)]

df = spark.createDataFrame(dados, schema)
````

## Declaração Completa
Utilizando o módulo do PySpark para criar schemas, utilizados quando existe uma necessidade de criar schemas complexos e com constraints.
````
from pyspark.sql.types import *

schema = StructType([
    StructField("Nome", StringType(), False),      # Nome - tipo String - Not null
    StructField("Idade", IntegerType(), True),    # Idade - tipo Integer - Not null
    StructField("Estado", StringType(), True)     # Estado - tipo String - Null
])
data = [("João", 25, "SP"), ("Maria", 30, "RJ"), ("Carlos", 40, "MG")]

df = spark.createDataFrame(data, schema)
````

## Tipos de Dados
| Tipo de Dados | Descrição | Exemplo |
|----------|-------|-------------|
| StringType | 	Representa dados de texto ou cadeias de caracteres. | "João", "Texto" |
| IntegerType | Representa um número inteiro (32 bits) | 	25, 100 |
| LongType | Representa um número inteiro longo (64 bits). | 1234567890, -9876543210 |
| FloatType | 	Representa um número de ponto flutuante de precisão simples (32 bits). | 3.14, -2.5 |
| DoubleType | Representa um número de ponto flutuante de precisão dupla (64 bits). | 3.14159, -100.75 |
| BooleanType | Representa valores booleanos (verdadeiro ou falso). | True, False |
| DateType | Representa uma data (sem hora). | 2023-01-01, 1999-12-31 |
| TimestampType | Representa uma data e hora com precisão de microssegundos | 2023-01-01 12:30:45, 1999-12-31 00:00:00 |
| ArrayType | Representa uma lista ordenada de valores de um tipo específico. Pode ser um tipo primitivo ou um StructType. | ["João", "Maria", "Carlos"], [1, 2, 3] |
| MapType | Representa um conjunto de pares chave-valor, onde tanto a chave quanto o valor podem ter tipos definidos. | {"chave1": "valor1", "chave2": "valor2"} |
| StructType | 	Representa um tipo de dados estruturados, onde cada campo pode ter um tipo específico (usado para representar tabelas). | StructType([StructField("Nome", StringType()), StructField("Idade", IntegerType())]) |