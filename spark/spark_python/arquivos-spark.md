# Arquivos com Dataframes
O PySpark possibilita uma fácil leitura e escrita de arquivos transformando em DFs.
## Leitura de Arquivos
````
# Leitura de um arquivo CSV
df_csv = spark.read.option("delimiter", ";").csv("caminho/do/arquivo.csv", header=True, inferSchema=True)

# Leitura de um arquivo JSON
df_json = spark.read.json("caminho/do/arquivo.json")

# Leitura de um arquivo Parquet
df_parquet = spark.read.parquet("caminho/do/arquivo.parquet")

# Leitura de arquivos de texto
df_texto = spark.read.text("caminho/do/arquivo.txt")
````
## Escrita de Arquivos
````
# Salvando o DataFrame como CSV
df_csv.write.option("header", "true").csv("caminho/de/saída/arquivo.csv")

# Salvando o DataFrame como Parquet
df_parquet.write.parquet("caminho/de/saída/arquivo.parquet")

# Salvando o DataFrame como JSON
df_json.write.json("caminho/de/saída/arquivo.json")

# Salvando o DataFrame como arquivo de texto
df_texto.write.text("caminho/de/saída/arquivo.txt")

````

### Outras Configurações de Escrita
````
# Particionamento na Escrita
df_parquet.write.partitionBy("coluna_de_particao").parquet("caminho/de/saída/arquivo.parquet")


# Sobrescrita ou append
# Leitura de Parquet
df_parquet = spark.read.parquet("caminho/do/arquivo.parquet")

# Processamento e escrita de volta em Parquet
df_parquet.write.mode("overwrite").parquet("caminho/de/saída/arquivo_parquet_otimizado.parquet")
df.write.mode("append").parquet("caminho/de/saída")

# Ignorar a escrita do arquivo se já existir
df.write.mode("ignore").parquet("caminho/de/saída")
````