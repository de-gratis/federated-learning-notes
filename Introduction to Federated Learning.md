Dispositivos com capacidade de Processamento, Armazenamento e Comunicação são capazes de coletar dados do ambiente e também atuar neste mesmo ambiente com alguma atividade, Ex: semáforo inteligente da Audi, carregamento do celular da Apple, Gboard do Google, etc

Federated Learning tem uma conexão GIGANTESCA com o IoT

Geralmente os dados são enviados para a nuvem para o seu processamento 

Os celulares são entidades passivas, não tomam decisões, basicamente somente disponibilizando informações e o usuário toma as decisões. Uma ou outra aplicação consegue tomar decisão mas ainda em níveis muito baixos

"Smartphone mas de inteligente não tem nada ou não é muito inteligente"

Sem colaboração, teremos dados pequenos, isolados e fragmentados, incompletos. Por isso os mesmos são levados a servidores para que possam ser usados de forma conjunta e colaborativa, trazendo alguns problemas de privacidade e custo operacional

Os métodos de Machine Learning deverão se adequar a um ambiente onde os dados estão espalhados em um sistema distribuído, sem que tenha que transferir do mesmo para uma unidade central

"E se os dispositivos aprendessem com seus dados locais, sem a necessidade de enviar os dados para uma unidade central?"

Dados locais por si só podem possuir:

- Desempenho limitado
- Resultados não estatisticamente significativos
- Dados enviesados
- Falta de representatividade da distribuição alvo

"Mas então como lidar com a fragmentação dessas estruturas de dados em um cenário de proteção à privacidade?"

FL permite o treinamento dos modelos de forma distribuída e colaborativa, modelo este compartilhado entre os dispositivos, com os dados não saindo dos mesmos

Separa-se então a capacidade de ser feito o Machine Learning da necessidade de armazenar estes dados em uma unidade central ou nuvem

Então mandam-se os modelos ao servidor (criando-se um consenso entre eles, agregação), e não os dados

Recebe-se o modelo global -> Treina-se localmente no seu dispositivo -> Novo modelo enviado ao servidor -> Agregação de modelos -> Modelo atualizado enviado de volta aos dispositivos -> Loop pela acurácia

- Etapa 1: Inicialização de modelos locais (hiperparâmetros)
- Etapa 2: Treinamento e atualização do modelo local
- Etapa 3: Agregação e atualização do modelo no lado do servidor

> Aprendizado de Máquina Distribuído é de forma paralelizada, paralisa-se o treinamento, ganhando-se desempenho por meio de uma gpu com vários núcleos de processamento para agilizar o processo de treinamento

Desafios:

- Compreensão de modelos, eles não podem ser muito robustos, pesados
- Dados não independentes e identicamente distribuídos
- Custo de comunicação

Prós:

- Uso altamente eficiente da largura de banda da rede
- Privacidade

O modelo mais comum para FL é o FedAvg, Média Federada

Na solução a exemplo de um B2C (Business to Consumers, sendo o Google o business e o usuário final android o consumer) do Google Gboard, os gradientes são criptografados para que os dados do usuário não sejam coletados e que não seja possível inferir algo deles. 

Para modelos B2B (Business to Business), há o exemplo de federações entre hospitais

FL envolve a área de Machine Learning, Sistemas Distribuídos, Privacidade, Segurança, IoT, etc

FL compreende 2 etapas: o Treinamento e a Inferência do modelo

> Aprendizado Centralizado: Os dados dos dispositivos são mandados para uma unidade central, retornando modelos eficientes e robustos, apesar da falta de privacidade e comunicação
>
> Aprendizado Distribuído: Os dispositivos sinais treinam seus modelos locais sem o compartilhamento com servidor ou outros dispositivos, o contrário do Aprendizado Centralizado, com privacidade mas sem modelos eficientes

Alguns artigos que fazem estudos sobre a solução do Google Gboard:

- Federated Learning for Emoji Prediction in a Mobile Keyboard
- Applied Federated Learning: Improving Google Keyboard Query Suggestions
- Federated Learning Of Out-Of-Vocabulary Words

Cross-device (B2C ?):

- Grandes quantidades de dispositivos intermitentes
- Clientes não podem ser indexados diretamente
- Servidor acessa amostras aleatórias dos clientes
- Atualizações anônimas dos clientes
- Comunicação pode ser um gargalo
- Ex: Reconhecimento de fala da Siri

Cross-silo (B2B ?):

- Pequena quantidade de clientes, resultando em alta disponibilidade (instituições, data silos)
- Cada cliente tem sua ID, podendo ser indexado
- Maioria dos clientes participam em todos os rounds
- Pode manter o estado durante vários rounds
- Ex: Detecção de tumores cerebrais com modelos reforçados entre instituições de saúde, realizado pela UPenn
- Ex: Predição de possibilidade de necessidade de oxigênio para pacientes de covid, realizado pela NVIDIA

"Ampliar a capacidade preditiva do modelo, tornando aplicável em uma gama mais ampla de serviços da área desejada"

Desafios em FL:

- Comunicação
  - Limitar número de dispositivos por round
  - Reduzir número de rounds
  - Reduzir tamanho das mensagens
- Privacidade
  - Manter os dados nos dispositivos locais
  - Agregação segura com acesso somente ao modelo final
  - Criptografia
  - Privacidade Diferencial
- Estatística
  - Não balanceado
  - Dados sem ID
- Heterogeneidade dos Dados
  - Enviesamento dos modelos 

Uso do framework Flower para Aprendizado Federado

Antes do Flower não tinham os clientes distintos que se comunicavam com uma entidade central ou entre si, compartilhando mensagens, tudo era feito com loops

Primeiro loop (externo) é a quantidade de rounds de comunicação e o segundo (interno) é a simulação dos clientes. Adicionavam-se os pesos de cada cliente a uma lista e depois tirava-se a média deles

Depois do Flower foi possível explorar diferentes clientes heterogêneos com diferentes capacidades de comunicação, de armazenamento, além de considerar atraso na rede e fragmentação de pacotes

Artigo do Flower:

- Flower: A Friendly Federated Learning Framework

gRPC é um framework de chamada de procedimento remoto que o Flower faz uso, criando templates de mensagem que será trocado entre clientes
