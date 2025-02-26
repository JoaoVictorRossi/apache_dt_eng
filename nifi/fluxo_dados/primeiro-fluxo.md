# Fluxo de Dados simples
1. Para iniciar a configuração do processor arrastei e solte o icone do processor para a área de trabalho do NiFi.

![Fluxo Simples1](../Imgs/fluxo/fluxo_simples/fluxo-simples1.png)
2. Existem diversos tipos de processor que pode ser criado, como podemos ver na tela que abriu, porém vou utilizar o "GenerateFlowFile".

![Fluxo Simples2](../Imgs/fluxo/fluxo_simples/fluxo-simples2.png)
3. Acessando o processador criado, defini que acada 5 segundos será gerado um uma quantidade de dados random.

![Fluxo Simples3](../Imgs/fluxo/fluxo_simples/fluxo-simples3.png)
4. Logo configurei as propriedades do flowfile que será gerado, como o tamanho e o formato dos dados.

![Fluxo Simples4](../Imgs/fluxo/fluxo_simples/fluxo-simples4.png)
5. Criei mais um processor para utilizar como log, tendo como tipo "LogAttribute" com as configurações padrões.

![Fluxo Simples5](../Imgs/fluxo/fluxo_simples/fluxo-simples5.png)
6. Após isso criei uma conexão entre os dois processors que criei, definindo o nome como SaidaDados:

![Fluxo Simples6](../Imgs/fluxo/fluxo_simples/fluxo-simples6.png)
7. Após isso executei o fluxo de dados, iniciando o processador responsável por gerar os dados de forma random.

![Fluxo Simples7](../Imgs/fluxo/fluxo_simples/fluxo-simples7.png)
8. Após isso salvei todo o trabalho desenvolvido, cliando em uma área em branco e selecionando "Create template"

---
**[Voltar](./fluxo-dados.md)**