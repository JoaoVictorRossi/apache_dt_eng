# Apache Hive
Um Datawarehouse dentro do hadoop, permite todas as funcionalidades e vantagens de um DW para um grande volume de dados armazenados no HDFS, a ideia principal é acesso a dados massivos sem a necessidade do MapReduce.
- Utiliza HiveQL para consultas (parecido com SQL).
- Gera tarefas MapReduce a partir das consultas.
- Possui Metastore igualmente o Sqoop, responsável por armazenar metadados.
## Tipos de tabela
Dentro do Hive é possível ter dois tipos de tabela:
- Tabelas Gerenciadas/Internas: Hive controla o ciclo de vida dos dados.
- Tabelas Externas: Dados são contralados fora do Hive, úteis para integração com outras ferramentas.