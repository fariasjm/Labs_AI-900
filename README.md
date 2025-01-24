# Labs_AI-900

# Trabalhando com Machine Learning na Prática no Azure ML

## Passo a passo para criar um jobs ML automatizado no Azure Machine Learning

1. No Azure Machine Learning studio, visualize a página Automated ML (em Authoring)
2. Crie um novo trabalho de ML automatizado com as seguintes configurações:

Configurações básicas:
- Nome do trabalho: mslearn-bike-automl
- Novo nome do experimento: mslearn-bike-rental
- Descrição: Aprendizado de máquina automatizado para previsão de aluguel de bicicletas
- Tags: nenhum

Tipo de tarefa e dados:
- Selecione o tipo de tarefa: Regressão
- Selecione o conjunto de dados: Crie um novo conjunto de dados com as seguintes configurações:

Tipo de dados:
- Nome: bike-rentals
- Descrição: Dados históricos de aluguel de bicicletas
- Tipo: Tabular

Fonte de dados:
- Selecione arquivo local
- Faça o download do arquivo bike-data.zip na URL https://aka.ms/bike-rentals
- Extraia os arquivos numa pasta local
- Selecione Carregar Pasta, apontando para a pasta com os arquivos: daily-bike-share.csv e MLTable

Configurações da tarefa:
- Tipo de tarefa: Regressão
- Conjunto de dados: bike-rentals
- Coluna alvo: Aluguéis (inteiro)
- Configurações adicionais:
  - Métrica primária: Erro médio quadrático normalizado
  - Explicar o melhor modelo: Não selecionado
  - Habilitar empilhamento de conjunto : Não selecionado
  - Usar todos os modelos suportados: Não selecionado (Você vai trabalhar apenas com alguns algoritmos específicos)
  - Modelos permitidos: Selecione apenas RandomForest e LightGBM

Limites: (Expanda esta seção)
- Máximo de tentativas: 3
- Máximo de tentativas simultâneas: 3
- Máximo de nós: 3
- Limiar de pontuação métrica: 0.085
- Tempo limite: 15
- Tempo limite de iteração: 15
- Ativar término antecipado: Selecionado

Validação e teste:
- Tipo de validação: Divisão de treinamento-validação
- Porcentagem de dados de validação: 10
- Conjunto de dados de teste: Nenhum

Computação:
- Selecione o tipo de computação: Sem servidor
- Tipo de máquina virtual: CPU
- Nível da máquina virtual: Dedicado
- Tamanho da máquina virtual: Standard_DS3_V2
- Número de instâncias: 1

3. Envie o trabalho de treinamento
4. Inicia automaticamente.

## Implantar e testar o modelo

1. Na guia Modelo selecione Implantar e use a opção ponto de extremidade em tempo real para implantar o modelo com as seguintes configurações:
- Máquina virtual: Standard_DS3_v2
- Contagem de instâncias: 3
- Ponto de extremidade: Novo
- Nome do ponto de extremidade: Deixe o padrão
- Nome da implantação: Manter o padrão
- Coleta de dados de inferência: Disabled
- Empacotar modelo: Disabled

2. Aguarde a implantação (pode levar alguns minutos)
3. Aguarde o status de Implantação mudar para Concluído.

4. Agora você pode testar o serviço implantado
5. Em Estúdio do Azure Machine Learning, no menu à esquerda, selecione Pontos de Extremidade e abra o ponto de extremidade em tempo real
6. Na página do ponto de extremidade em tempo real de previsão de aluguel, exiba a guia Teste
7. No painel Dados de entrada para testar o ponto de extremidade, substitua o modelo JSON pelos seguintes dados de entrada:

 {
   "input_data": {
     "columns": [
         {
             "day": 1,
             "mnth": 1,   
             "year": 2022,
             "season": 2,
             "holiday": 0,
             "weekday": 1,
             "workingday": 1,
             "weathersit": 2, 
             "temp": 0.3, 
             "atemp": 0.3,
             "hum": 0.3,
             "windspeed": 0.3 
         }
     ],
     "index": [],
     "data": []
   }
 }

8. Clique no botão Testar.




