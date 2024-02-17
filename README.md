![Static Badge](https://img.shields.io/badge/Azure-blue?style=flat&logo=azure&logoColor=black)
![Static Badge](https://img.shields.io/badge/javascript-orange?style=flat&logo=javascript&logoColor=black&cacheSeconds=!%5BStatic%20Badge%5D(https%3A%2F%2Fimg.shields.io%2Fbadge%2FAzure-blue%3Fstyle%3Dflat%26logo%3Dazure%26logoColor%3Dblack))


# mslearn-bike-rental
## Criar um workspace do Azure Machine Learning

Para utilizar o Azure Machine Learning, você precisa provisionar um workspace do Azure Machine Learning em sua assinatura do Azure. Em seguida, você poderá usar o Azure Machine Learning studio para trabalhar com os recursos em seu workspace.

1. Faça login no [Portal do Azure](https://google.com) usando suas credenciais da Microsoft.
2. Selecione + Criar um recurso, pesquise por Machine Learning, e crie um novo recurso do Azure Machine Learning com as seguintes configurações:

| Configuração            | Descrição                                                                                                      |
|-------------------------|----------------------------------------------------------------------------------------------------------------|
| **Assinatura**              | Sua assinatura do Azure.                                                                                      |
| **Grupo de recursos**       | Crie ou selecione um grupo de recursos.                                                                       |
| **Nome**                    | Digite um nome único para o seu workspace.                                                                    |
| **Região**                  | Selecione a região geográfica mais próxima.                                                                   |
| **Conta de armazenamento**  | Anote a conta de armazenamento padrão que será criada para o seu workspace.                                   |
| **Cofre de chaves**         | Anote o cofre de chaves padrão que será criado para o seu workspace.                                          |
| **Insights de aplicativos** | Anote o recurso de insights de aplicativos padrão que será criado para o seu workspace.                        |
| **Registro de contêiner**   | Nenhum (um será criado automaticamente na primeira vez que você implantar um modelo em um contêiner).         |



3. Selecione Revisar + criar e, em seguida, selecione Criar. Aguarde a criação do seu workspace (pode levar alguns minutos) e, em seguida, vá para o recurso implantado.
4. Selecione Iniciar studio (ou abra uma nova guia do navegador e acesse Azure Machine Learning studio e faça login usando sua conta da Microsoft). Feche quaisquer mensagens que sejam exibidas.
5. No Azure Machine Learning studio, você deverá ver seu workspace recém-criado. Se não visualizar, selecione Todos os workspaces no menu à esquerda e, em seguida, selecione o workspace que você acabou de criar.

## Usar aprendizado de máquina automatizado para treinar um modelo

- O aprendizado de máquina automatizado permite que você experimente vários algoritmos e parâmetros para treinar múltiplos modelos e identifique o melhor para seus dados. Neste exercício, você usará um conjunto de dados de detalhes históricos de aluguel de bicicletas para treinar um modelo que prevê o número de aluguéis de bicicletas esperados em um determinado dia, com base em características sazonais e meteorológicas.

> Citação: Os dados usados neste exercício são derivados do Capital Bikeshare e são usados de acordo com o contrato de licença de dados publicado.

1. No Azure Machine Learning studio, visualize a página de AutoML (em Authoring).
2. Crie um novo trabalho de AutoML com as seguintes configurações, usando Próximo conforme necessário para progredir pela interface do usuário:

    **Configurações básicas:**

| Configuração                  | Descrição                                                                                     |
|-------------------------------|-----------------------------------------------------------------------------------------------|
| **CONFIGURAÇÕES BASICAS**     |                                                                                               |
| Nome do trabalho              | mslearn-bike-automl                                                                          |
| Novo nome do experimento      | mslearn-bike-rental                                                                          |
| Descrição                     | Aprendizado de máquina automatizado para previsão de aluguel de bicicletas                    |
| Tags                          | nenhum                                                                                          |
| **TIPO DE TAREFAS E DADOS**    |                                                                                               |
| Selecione o tipo de tarefa    | Regressão                                                                                     |
| Selecione o conjunto de dados | Crie um novo conjunto de dados com as seguintes configurações:                                |
| **TIPO DE DADOS**                |                                                                                               |
|   - Nome                      | aluguéis-de-bicicleta                                                                        |
|   - Descrição                 | Dados históricos de aluguel de bicicletas                                                    |
|   - Tipo                      | Tabular                                                                                       |
| **FONTE DE DADOS**               |                                                                                               |
|   - Selecionar               | De arquivos da web                                                                            |
| **URL DA WEB**                  |                                                                                               |
|   - URL da Web                | [https://aka.ms/bike-rentals](https://aka.ms/bike-rentals)                                    |
|   - Ignorar validação de dados| não selecionar                                                                                 |
| **CONFIGURAÇÕES**                 |                                                                                               |
|   - Formato do arquivo        | Delimitado                                                                                    |
|   - Delimitador               | Vírgula                                                                                       |
|   - Codificação               | UTF-8                                                                                         |
|   - Cabeçalhos de coluna      | Somente o primeiro arquivo tem cabeçalhos                                                    |
|   - Pular linhas              | Nenhum                                                                                       |
|   - O conjunto de dados contém dados de várias linhas| não selecionar                              |
| **ESQUEMA**                       |                                                                                               |
|   - Incluir todas as colunas exceto Path |                                                                                                          |
|   - Revisar os tipos detectados automaticamente |                                                                                                             |

- Selecione Criar. Após a criação do conjunto de dados, selecione o conjunto de dados aluguéis-de-bicicleta para continuar a enviar o trabalho de AutoML.
  
| Configuração                                  | Descrição                                                                                           |
|-----------------------------------------------|-----------------------------------------------------------------------------------------------------|
| **CONFIGURAÇÕES DA TAREFA**                   |                                                                                                     |
| Tipo de tarefa                                | Regressão                                                                                           |
| Conjunto de dados                             | aluguéis-de-bicicleta                                                                               |
| Coluna alvo                                   | Aluguéis (inteiro)                                                                                  |
| **CONFIGURAÇÕES ADICIONAIS**                     |                                                                                                     |
|   - Métrica primária                          | Erro quadrático médio normalizado                                                                   |
|   - Explicar melhor modelo                    | Não selecionado                                                                                     |
|   - Usar todos os modelos suportados          | Não selecionado. Você restringirá o trabalho para tentar apenas alguns algoritmos específicos.    |
|   - Modelos permitidos                        | Selecionar apenas RandomForest e LightGBM — normalmente, você gostaria de tentar o máximo possível, mas cada modelo adicionado aumenta o tempo necessário para executar o trabalho. |
| **LIMITES**                                      |                                                                                                     |
|   - Tentativas máximas                       | 3                                                                                                   |
|   - Tentativas simultâneas máximas           | 3                                                                                                   |
|   - Máximo de nós                            | 3                                                                                                   |
|   - Limiar de pontuação da métrica           | 0.085 (para que, se um modelo alcançar uma pontuação métrica de erro quadrático médio normalizado de 0.085 ou menos, o trabalho termine.) |
|   - Tempo limite                             | 15                                                                                                  |
|   - Tempo limite da iteração                 | 15                                                                                                  |
|   - Ativar término antecipado                | Selecionado                                                                                         |
| **VALIDAÇÃO E TESTE**                            |                                                                                                     |
|   - Tipo de validação                        | Divisão de treinamento-validação                                                                    |
|   - Porcentagem de dados de validação        | 10                                                                                                  |
|   - Conjunto de dados de teste               | Nenhum                                                                                              |
| **COMPUTAÇÃO**                               |                                                                                                     |
|   - Selecionar tipo de computação            | Serverless                                                                                          |
|   - Tipo de máquina virtual                  | CPU                                                                                                 |
|   - Nível da máquina virtual                 | Dedicado                                                                                            |
|   - Tamanho da máquina virtual               | Standard_DS3_V2*                                                                                    |
|   - Número de instâncias                     | 1                                                                                                   |

- >Se sua assinatura restringir os tamanhos de VM disponíveis para você, escolha qualquer tamanho disponível.

3. Envie o trabalho de treinamento. Ele começa automaticamente.
4. Aguarde o término do trabalho. Pode levar um tempo — agora pode ser um bom momento para uma pausa para o café!

## Referências
[Explore Automated Machine Learning in Azure Machine Learning](https://microsoftlearning.github.io/mslearn-ai-fundamentals/Instructions/Labs/01-machine-learning.html)

[Explore Azure AI services](https://microsoftlearning.github.io/mslearn-ai-fundamentals/Instructions/Labs/02-content-safety.html)