# Arquivos HDFS
Sistemas de arquivos distribuído do Hadoop, projetado para armazenar grande volume de dados de forma eficiente e segura.
- Tolerância a falhas
- Escalabilidade
- Capacidades de ligar com terabytes ou petabytes.

## Arquitetura do HDFS (Master-Slave)
Arquitetura utilizada em sistemas distribuidos (como o HDFS), onde um nó (master) controla um ou mais nós(slaves).
### Master
Responsável por gerenciar os outros nós e armazenar metadados como localização, permisões, entre outras informações.
### Slave
Responsável por armazenar fisicamente os blocos de dados, executar operações sob o comando do master.
**Cada bloco é replicado em múltiplos DataNodes para garantir a tolerância a falhas (por padrão, 3 cópias).**
## Armazenamento no HDFS
1. Um arquivo grande é fragmentado e distribuído entre os slaves.
2. Cada fragmento (bloco) é replicado entre outros nós (slaves) para garantir a disponibilidade em caso de falhas.
3. O master armazena os metadados em memória:
I. Localização dos blocos.
II. Permisão de arquivos.
III. Estrutura dos diretórios.

---
**[Voltar](../hadoop.md)**