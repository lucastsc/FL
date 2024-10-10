# Federated Learning

Este repositório contém uma implementação manual de um algoritmo de **Aprendizado Federado** (Federated Learning) no arquivo `FL2.ipynb`.

## Descrição

O Aprendizado Federado é uma técnica de aprendizado distribuído onde um **servidor central** seleciona um modelo de rede neural e compartilha com vários **clientes**. Cada cliente treina o modelo localmente com seus próprios dados privados e, em seguida, retorna apenas os **pesos do modelo** ao servidor. O servidor, então, agrega os pesos recebidos dos clientes e distribui o modelo atualizado de volta aos clientes. Este processo se repete até a convergência.

## Funcionamento

A implementação do algoritmo de Aprendizado Federado consiste nas seguintes etapas:

1. O servidor seleciona um **modelo de rede neural** e compartilha com os **N clientes**.
2. Cada cliente treina o modelo com seus dados locais privados, que **não são acessíveis pelo servidor**.
3. Os clientes enviam de volta ao servidor apenas os **pesos do modelo treinado**.
4. O servidor **agrega os pesos** dos N clientes utilizando a lógica de **Weighted FedAvg**.
5. O servidor compartilha o modelo atualizado de volta aos clientes.
6. O processo se repete por várias rodadas até a convergência do modelo.

## Algoritmo Principal

O algoritmo principal é implementado na função `FL`, que recebe os seguintes parâmetros:

- **NCLIENTS**: (int) Número total de clientes (ativos e inativos) no aprendizado federado.
- **PROBFAIL**: (float) Probabilidade de falha de cada cliente durante o treinamento, no intervalo \[0, 1\].
- **ROUNDS**: (int) Número de rodadas de Aprendizado Federado.
- **OVERLAPPING_ENTRIES_PERCENT**: (float) Percentual de overlap no treinamento não-caótico, no intervalo \[0, 1\].
- **RANDOM_TRAINING_ENTRIES**: (bool) Define se os conjuntos de treino dos clientes são totalmente caóticos.
- **MAX_CHAOTIC_ENTRIES**: (int) Número máximo de entradas que podem compor os conjuntos de treino aleatórios de cada cliente, caso `RANDOM_TRAINING_ENTRIES = True`.
- **TRAIN_SIZE**: (int) Tamanho do conjunto de dados de treino.
- **TEST_SIZE**: (int) Tamanho do conjunto de dados de teste.

## Métodos de Treinamento

O treinamento dos modelos pode ocorrer de duas maneiras, com base na variável `RANDOM_TRAINING_ENTRIES`:

### 1. Treinamento Caótico (`RANDOM_TRAINING_ENTRIES = True`)

Cada cliente terá um **conjunto de treinamento aleatório**, com um número variável de entradas de até **MAX_CHAOTIC_ENTRIES**, extraídas da totalidade dos **60.000 dados de treinamento do MNIST**.

### 2. Treinamento Organizado (`RANDOM_TRAINING_ENTRIES = False`)

Cada cliente terá um **conjunto fixo de treinamento**, calculado como `partition = TRAIN_SIZE // len(active_clients_list)`. Pode haver **sobreposição** (overlap) de dados de treinamento entre os clientes, controlada pela variável `OVERLAPPING_ENTRIES_PERCENT`, simulando cenários onde os clientes possuem **dados semelhantes**.

## Estrutura do Repositório

- `FL2.ipynb`: Implementação do algoritmo de Aprendizado Federado.
- `README.md`: Este arquivo, com a documentação do projeto.

## Como Usar

1. Clone este repositório:
   ```bash
   git clone https://github.com/seu-usuario/seu-repositorio.git

2. Abra e execute o notebook FL2.ipynb para rodar a simulação do algoritmo de Aprendizado Federado.
