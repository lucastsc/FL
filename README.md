# FL
Federated Learning
O arquivo FL2.ipynb é a implementação de um algoritmo de Aprendizado Federado (Federated Learning).
A implementação consiste em:
1 - Servidor seleciona um modelo de rede neural e compartilha com os N clientes.
2 - Cada cliente treina o modelo recebido, mas com seus dados locais e privados.
3 - Os clientes, após treinarem o modelo com dados locais, enviam apenas o modelo (pesos) de volta ao servidor.
4 - O servidor recebe os modelos treinados dos N clientes e agrega seus pesos segundo a lógica de Weighted FedAvg.
5 - Após agregar os pesos (modelos) dos N clientes, o servidor compartilha os pesos resultantes (modelos) de volta para os clientes.
6 - O processo se repete até possível convergência.
