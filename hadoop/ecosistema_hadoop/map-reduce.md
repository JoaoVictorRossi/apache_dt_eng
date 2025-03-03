# Map Reduce

Ferramenta utilizado para processamento em batch de grandes volumes de dados de forma distribuida.

## Fases
O MapReduce divide o processamento de dados em três fases principais:

### Map´
Os dados são dividios em partes menores e distribuidos entre os nós do cluster, e cada nó executa uma função **map**, que processa sua parte dos dados e gera pares de chave-valor como saída.

### Shuffle
Os pares de chave-valor gerados na etapa anterior são agrupados pela chave.

### Reduce
Cada nó executa uma função **reduce**, que processa a chave e todos os valores associados e gera a saída final.

- As funções reduce e map são definidas pelo usuário.

---
**[Voltar](../hadoop.md)**
