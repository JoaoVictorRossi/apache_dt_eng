# Apache Sqoop

Ferramenta usada para transferir grandes volumes de dados entre bancos de dados relacionais e o próproio Hadoop (HDFS, Hive, Hbase, Accumulo).
- Pode importar tabelas inteiras ou consultas.
- Suporta paralelismo.
- Agendamentos de importação e exportação.
- Compatibilidade com DBs usando conectoras JDBC.

## Jobs

Usados para automatizar e simplificar processos de importação ou exportação no Sqoop, em vez de repetir comandos longs toda vez que precisa transferir dados, é possível salvar a configuração do comando em um job.

- Você cria um job especificando os detalhas do processo, como conexão com o DB, tabela, diretório, etc.
- Você pode deletar jobs facilmente.
- Os jobs são salvos em um repositório do sqoop, que mantém essas configurações.
## Exemplos de Código

**Listando bancos de dados**
```
sqoop list-database --connect jdbc:mysql://localhost/retail_db --username meuUsuario --password 12345

```
**Importando tabela**
```
sqoop import --connect jdbc:mysql://localhost/retail_db --username meuUsuario --password 12345 --check-column customer_id --incremental append --last_value 0 -m 1
```

**Criando um Job**
```
sqoop job -D sqoop.metastore.client.record.password=true --create customers --import --connect jdbc:mysql://localhost/retail_db --username meuUsuario --password 12345 --check-column customer_id --incremental append --last_value 0 -m 1

## Executando job
sqoop job --exec customers
```

---
**[Voltar](../hadoop.md)**