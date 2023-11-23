# Federated Learning
O arquivo FL2.ipynb é a implementação manual de um algoritmo de Aprendizado Federado (Federated Learning).  

A implementação consiste em:  
1. Servidor seleciona um modelo de rede neural e compartilha com os N clientes.  
2. Cada cliente treina o modelo recebido, mas com seus dados locais que são privados e não podem ser acessados pelo servidor de agregação.  
3. Os clientes, após treinarem o modelo com dados locais, enviam apenas o modelo (pesos) de volta ao servidor.  
4. O servidor recebe os modelos treinados dos N clientes e agrega seus pesos segundo a lógica de Weighted FedAvg.  
5. Após agregar os pesos (modelos) dos N clientes, o servidor compartilha os pesos resultantes (modelos) de volta para os clientes.  
6. O processo se repete até possível convergência.

O algoritmo principal é a função FL. Ela recebe como parâmetros:  

1. NCLIENTS: (int) Universo do número de clientes (ativos e inativos) no aprendizado federado  
2. PROBFAIL: (0<=p<=1) Probabilidade de falha de cada cliente  
3. ROUNDS: (int) Rodadas de Aprendizado Federado  
4. OVERLAPPING_ENTRIES_PERCENT: (0<=p<=1) Percentual de overlap no treinamento não-caótico
5. RANDOM_TRAINING_ENTRIES: (True/False) Clientes com conjuntos de treino totalmente caóticos  
6. MAX_CHAOTIC_ENTRIES: (int) Até quantos elementos poderão ter os conjuntos aleatórios de treinamento de cada cliente, caso RANDOM_TRAINING_ENTRIES = True  
7. TRAIN_SIZE: (int) Tamanho do conjunto dos dados de treino  
8. TEST_SIZE: (int) Tamanho do conjunto dos dados de teste

O treinamento dos modelos pode ocorrer de 2 maneiras:  

RANDOM_TRAINING_ENTRIES: (True/False) Clientes com conjuntos de treino totalmente aleatórios. Isso significa que se for:    
1. True: Cada cliente (ci) terá como conjunto de treinamento um número aleatório de entradas de até MAX_CHAOTIC_ENTRIES nos seus dados locais, extraídos da totalidade de 60.000 dados de treinamento do MNIST.
2. False: Cada cliente (ci) terá como conjunto de treinamento um número fixo de entradas de treinamento, partition = TRAIN_SIZE // len(active_clients_list), podendo haver overlap de dados de treinamento entre os clientes por meio da variável OVERLAPPING_ENTRIES_PERCENT, para simular clientes que apresentem conjuntos de dados semelhantes, caso necessário.


