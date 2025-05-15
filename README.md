# Sistema-Bancario

SISTEMA BANCARIO

Projeto a Ser Desenvolvido:
1 Funcionalidades: O programa deve: • Exibir um menu de opções para o usuário. • Solicitar ao usuário que escolha uma opção. • Executar a operação correspondente à opção escolhida: • Consulta de Saldo: Exibir o saldo atual da conta. o Saque: Permitir ao usuário sacar um valor da conta, verificando se há saldo suficiente. o Depósito: Permitir ao usuário depositar um valor na conta. o Extrato: Exibir as últimas transações realizadas na conta. o Sair: Encerrar o programa. • Repetir o processo até que o usuário escolha a opção de sair. • Exibir mensagens claras e informativas para o usuário.
2 Dados de Entrada: • Opção do menu escolhida pelo usuário (inteiro). • Valor do saque ou depósito (real).
3 Dados de Saída: • Saldo atual da conta (real). • Mensagens informativas (ex: "Saldo insuficiente", "Saque realizado com sucesso"). • Menu de opções.
4 Etapas de Desenvolvimento (Fluxo do Programa): • Etapa 1: Apresentação e Menu o Exibir uma mensagem de boas-vindas. o Definir as opções do menu (1 - Consulta de Saldo, 2 - Saque, 3 - Depósito, 4 - Sair). o Solicitar ao usuário que escolha uma opção. o Validar a opção escolhida (verificar se é uma opção válida). • Etapa 2: Implementação das Operações o Implementar a função/procedimento para cada operação (consulta de saldo, saque, depósito). o Consulta de Saldo: Exibir o valor do saldo. o Saque: Solicitar o valor do saque, verificar se há saldo suficiente, atualizar o saldo e exibir uma mensagem de sucesso ou erro. o Depósito: Solicitar o valor do depósito, atualizar o saldo e exibir uma mensagem de sucesso. • Etapa 3: Laço Principal o Utilizar um laço while para repetir as operações até que o usuário escolha a opção de sair. o Chamar a função/procedimento correspondente à opção escolhida pelo usuário. • Etapa 4: Validação de Entrada Robusta o Adicionar tratamento de exceções para garantir que o usuário sempre forneça entradas válidas (números inteiros para opções do menu e números reais para valores de saque/depósito). • Etapa 5: Extrato Bancário Detalhado o Implementar a funcionalidade de extrato, armazenando as transações em uma lista e exibindo-as formatadas. • Etapa 6: Persistência de Dados (Básico) • Adicionar a funcionalidade de salvar o saldo e o extrato em arquivos e carregá-los ao iniciar o programa.

Validação de Entrada Robusta Criação do Algoritmo: Modificar o código para usar try-except para tratar erros quando o usuário digita uma opção de menu que não é um número inteiro. Dentro das funções sacar() e depositar(), usar try-except para garantir que o valor digitado pelo usuário seja um número real. Se ocorrer um erro de tipo (ValueError), exibir uma mensagem de erro clara para o usuário e pedir para digitar o valor novamente.

# Exemplo de código para validação de entrada robusta
def sacar(saldo):
    try:
        valor = float(input("Digite o valor do saque: "))
        if valor <= saldo:
            saldo -= valor
            print("Saque realizado com sucesso!")
        else:
            print("Saldo insuficiente.")
    except ValueError:
        print("Valor inválido. Tente novamente.")
    return saldo

def depositar(saldo):
    try:
        valor = float(input("Digite o valor do depósito: "))
        saldo += valor
        print("Depósito realizado com sucesso!")
    except ValueError:
        print("Valor inválido. Tente novamente.")
    return saldo


Extrato Bancário Detalhado Criação do Algoritmo: Criar uma lista vazia chamada extrato para armazenar as transações. Cada transação será um dicionário com a data/hora, tipo de transação e valor. Modificar as funções sacar() e depositar() para, antes de atualizar o saldo, adicionar um dicionário à lista extrato com os detalhes da transação. Para a data e hora, utilize a biblioteca datetime. Criar uma função exibir_extrato() que itera sobre a lista extrato e exibe cada transação formatada. Se o extrato estiver vazio, exibir a mensagem "Não foram realizadas transações."

import datetime

extrato = []

def sacar(saldo):
    try:
        valor = float(input("Digite o valor do saque: "))
        if valor <= saldo:
            saldo -= valor
            transacao = {"data": datetime.datetime.now(), "tipo": "Saque", "valor": valor}
            extrato.append(transacao)
            print("Saque realizado com sucesso!")
        else:
            print("Saldo insuficiente.")
    except ValueError:
        print("Valor inválido. Tente novamente.")
    return saldo

def depositar(saldo):
    try:
        valor = float(input("Digite o valor do depósito: "))
        saldo += valor
        transacao = {"data": datetime.datetime.now(), "tipo": "Depósito", "valor": valor}
        extrato.append(transacao)
        print("Depósito realizado com sucesso!")
    except ValueError:
        print("Valor inválido. Tente novamente.")
    return saldo

def exibir_extrato():
    if extrato:
        for transacao in extrato:
            print(f"{transacao['data']} - {transacao['tipo']}: R${transacao['valor']:.2f}")
    else:
        print("Não foram realizadas transações.")


Persistência de Dados (Básico) Criação do Algoritmo: Importar o módulo json para salvar e carregar os dados em formato JSON. No início do programa, tentar abrir um arquivo chamado "banco_dados.json" em modo de leitura ("r"). Se o arquivo existir, carregar o saldo e o extrato de lá. Se o arquivo não existir (FileNotFoundError), definir o saldo inicial e o extrato como uma lista vazia. No final do programa, antes de sair do loop while, abrir o arquivo "banco_dados.json" em modo de escrita ("w") e salvar o saldo e o extrato no arquivo usando json.dump(). Implementação do código:

import json

def carregar_dados():
    try:
        with open("banco_dados.json", "r") as file:
            dados = json.load(file)
            saldo = dados["saldo"]
            extrato = dados["extrato"]
    except FileNotFoundError:
        saldo = 0.0
        extrato = []
    return saldo, extrato

def salvar_dados(saldo, extrato):
    with open("banco_dados.json", "w") as file:
        dados = {"saldo": saldo, "extrato": extrato}
        json.dump(dados, file)

# Exemplo de uso
saldo, extrato = carregar_dados()
# ... operações bancárias ...
salvar_dados(saldo, extrato)

