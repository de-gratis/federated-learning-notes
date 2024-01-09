Os modelos de agregação são responsáveis por combinar as atualizações dos modelos enviadas pelos dispositivos clientes e gerar um novo modelo global. Existem várias abordagens para a agregação de modelos em aprendizado federado, os mesmos sendo cruciais para garantir a qualidade e a precisão do modelo global, enquanto mantêm a privacidade dos dados

Aprendizado Distribuído: Dispõe de um conjunto de dados grande, mas "plano", sendo os clientes nós de computação em um único cluster ou datacenter. Dados armazenados centralmente e embralahados e balanceados entre os clientes, os mesmos com acesso a qualquer parte do conjunto de dados. Gargalo de computação no datacenter, com poucas falhas

Aprendizado Federado entre Silos: Dados isolados, diferentes organizações ou datacenter em diferentes regiões geográficas. Dados gerados localmente e permanecem descentralizados, sem os clientes terem acesso aos dados e eles não sendo distribuídos de forma independente ou idêntica (ID). Gargalo de computação e comunicação, com poucas falhas

Aprendizado Federado entre Dispositivos: Número muito grande de dispositivos móveis ou IoT. Gargalo de comunicação, dependendo da tarefa pois utiliza o wifi ou conexões mais lentas, com muitas falhas



Os dispositivos finais são heterogêneos, instáveis, não sendo dedicados à tarefa de treinamento de modelo, com o desempenho e disponibilidade não sendo garantidos durante o treinamento

Estratégias de timing depois que disponibilizam o modelo, após expirar, já faz a agregação dos que recebeu. Ou até recebeu o modelo e já faz a agregação com o último que recebeu logo

Ver estratégias para mitigar os problemas do FedAVG

FedAVG faz a média ponderada de todos os modelos recebidos dos clientes

![image-20240109052847102](C:\Users\Home\AppData\Roaming\Typora\typora-user-images\image-20240109052847102.png)

![image-20240109052913932](C:\Users\Home\AppData\Roaming\Typora\typora-user-images\image-20240109052913932.png)

![image-20240109052932796](C:\Users\Home\AppData\Roaming\Typora\typora-user-images\image-20240109052932796.png)

![image-20240109052949387](C:\Users\Home\AppData\Roaming\Typora\typora-user-images\image-20240109052949387.png)

Existem parâmetros de personalização para que não tenha necessidade de todos os dispositivos participarem do aprendizado

A ideia é que o servidor aguarde os modelos dos clientes para computar o modelo global até que todos os modelos de cliente tenham, sido recebidos 

Os participantes devem ser síncronos

​	Problema retardatário

​	Problema de eficiência de comunicação

​	Há propostas de métodos assíncronos ou semi-síncronos para mitigar o problema acima

​	Convergem lentamente quando as amostras são não ID

Redução do tempo de treinamento é um importante objetivo de pesquisa em FL, com a sincronização de parâmetros sendo um gargalo importante para atingir este objetivo

Artigos:

Assynchronous federated optimization

SAFA: a semi-synchronous protocol for fast federated learning with low overhead

> Quando os clientes ficam offlines com muita frequência

Agregar apenas os modelos de clientes de dispositivos rápidos e iniciar a próxima rodada sem esperar mais por modelos de clientes de dispositivos lentos reduz a precisão do treinamento e pode muito provavelmente enviesar os resultados, exigindo mais rodadas para uma precisão satisfatória

Agregação de modelo parcial: Não desconsidera os participantes mais lentos, mas continua para o próximo round, utilizando os mais lentos em paralelo com dados de treinamento de rounds anteriores (?). Quanto o modelo deve esperar até entrar na próxima rodada?

Seleção de clientes e Compreensão de modelos para redução do volume de dados a ser transmitido aos clientes

FedAsync atualiza o modelo global assim que recebe o primeiro modelo, apesar de a taxa de convergência fica lenta e tende a precisar de muitas rodadas para a conclusão do treinamento

Existem basicamente 2 ideias:

​	Evitar selecionar nós lentos

​	O servidor não espera por nós lentos em uma rodada antes de entrar na próxima rodada e os modelos obsoletos retardatários podem ser agregados ao modelo global quando chegarem mais tarde 

É mais razoável assumir que os dispositivos finais tenham recursos computacionais e energéticos limitados

Não é feita a avaliação do impacto negativo ou positivo dos modelos obsoletos
