# Federated Learning

This repository contains a manual implementation of a **Federated Learning** algorithm in the file `FL2.ipynb`.

## Description

Federated Learning is a distributed learning technique where a **central server** selects a neural network model and shares it with multiple **clients**. Each client trains the model locally on its own private data and then returns only the **model weights** to the server. The server then aggregates the weights received from clients and distributes the updated model back to the clients. This process repeats until convergence.

## Operation

The implementation of the Federated Learning algorithm consists of the following steps:

1. The server selects a **neural network model** and shares it with **N clients**.
2. Each client trains the model with its private local data, which **the server cannot access**.
3. The clients send back only the **trained model weights** to the server.
4. The server **aggregates the weights** from the N clients using the **Weighted FedAvg** logic.
5. The server shares the updated model back with the clients.
6. The process repeats for several rounds until model convergence.

## Main Algorithm

The main algorithm is implemented in the `FL` function, which takes the following parameters:

- **NCLIENTS**: (int) Total number of clients (active and inactive) in federated learning.
- **PROBFAIL**: (float) Failure probability for each client during training, in the range \[0, 1\].
- **ROUNDS**: (int) Number of Federated Learning rounds.
- **OVERLAPPING_ENTRIES_PERCENT**: (float) Overlap percentage in non-chaotic training, in the range \[0, 1\].
- **RANDOM_TRAINING_ENTRIES**: (bool) Specifies whether the clients' training sets are completely chaotic.
- **MAX_CHAOTIC_ENTRIES**: (int) Maximum number of entries that can make up each client’s random training set if `RANDOM_TRAINING_ENTRIES = True`.
- **TRAIN_SIZE**: (int) Size of the training dataset.
- **TEST_SIZE**: (int) Size of the test dataset.

## Training Methods

The model training can occur in two ways, based on the `RANDOM_TRAINING_ENTRIES` variable:

### 1. Chaotic Training (`RANDOM_TRAINING_ENTRIES = True`)

Each client will have a **random training set** with a variable number of entries, up to **MAX_CHAOTIC_ENTRIES**, drawn from the entire **60,000 MNIST training data entries**.

### 2. Organized Training (`RANDOM_TRAINING_ENTRIES = False`)

Each client will have a **fixed training set**, calculated as `partition = TRAIN_SIZE // len(active_clients_list)`. There may be **overlap** in training data among clients, controlled by the `OVERLAPPING_ENTRIES_PERCENT` variable, simulating scenarios where clients have **similar data**.

## Repository Structure

- `FL2.ipynb`: Implementation of the Federated Learning algorithm.
- `README.md`: This file, containing project documentation.

## How to Use

1. Clone this repository:
   ```bash
   git clone https://github.com/lucastsc/FL.git
   
2. Open and run the FL2.ipynb notebook to simulate the Federated Learning algorithm.
