#Variáveis

cod1 = []
desc1 = []
valor1 = []
lista_prod = []
alterar = []
apagar1 = []

#Funções

def login():
    print("-- Logon --")
    print("1) Administrador")
    print("2) Operador")
    print("0) Sair")

def adm():
    print("-- Menu ADM --")
    print("1) Cadastrar")
    print("2) Listar")
    print("3) Alterar")
    print("4) Apagar")

def cadastrar(cod, desc, valor):
    arquivo = open("Lista_prod", '+a', encoding="utf-8")
    arquivo.write(cod + ';' +  desc + ";" + valor + "\n")
    print("-- Cadastro Concluído --")
    arquivo.close()

def listar():
    arquivo = open("Lista_prod", 'r')
    dados = arquivo.readlines()
    if dados == []:
        print("Não há produtos cadastrados")
    else:
        for i in range(len(dados)):
            dados[i] = dados[i].strip("\n")
            dados[i] = dados[i].split(";")
            lista_prod.append(dados[i])
        for x in range(len(lista_prod)):
            print(lista_prod[x][0] + " -- " + lista_prod[x][1] + " -- " + " R$ " + lista_prod[x][2])

def apagar():
    for i in range(len(lista_prod)):
        apagar1.append(lista_prod[i][0])
    apagar = (input("Digite o código do produto que deseja apagar: "))
    while apagar not in apagar1:
        print("Código inválido")
        apagar = input("Digite o código do produto que deseja apagar: ")
    indice = apagar1.index(apagar)
    print(f"O produto escolhido foi {lista_prod[indice][1]}")
    del lista_prod[indice]
    arquivo = open('Lista_prod', 'w', encoding='utf-8')
    for i in range(len(lista_prod)):
        arquivo.write(lista_prod[i][0] + ";" + lista_prod[i][1] + ";" + lista_prod[i][2] + "\n")
    arquivo.close()

#Main

print(login())

op = float(input("Digite uma opção válida: "))
while op < 0 or op > 2:
    print("Opção inválida")
    op = float(input("Digite uma opção válida: "))

if op == 1:
    adm()
    opc = float(input("Digite uma opção válida: "))
    while opc <= 0 or opc > 4:
        print("Opção inválida")
        opc = float(input("Digite uma opção válida: "))
    if opc == 1:
        cod = (input("Insira o código: "))
        desc = (input("Insira o nome do produto: "))
        valor = (input("Insira o valor do produto: "))
        cadastrar(cod, desc, valor)
        cod1.append(cod)
        desc1.append(desc)
        valor1.append(valor)
        lista_prod = (cod1, desc1, valor1)
    elif opc == 2:
        print("-- Produtos Cadastrados --")
        listar()
    if opc == 3:
        listar()
        print("-- Alterar Produtos --")
        for i in range(len(lista_prod)):
            alterar.append(lista_prod[i][0])
        alteracao = input("Digite o código do produto que deseja alterar: ")
        while alteracao not in alterar:
            print("Código inválido")
            alteracao = input("Digite o código do produto que deseja alterar: ")
        cod_alterar = alterar.index(alteracao)
        novocod = input("Digite seu novo código: ")
        while novocod in cod1 or novocod == "" or novocod == str:
            print("Código inválido")
            novocod = input("Digite seu novo código: ")
        novodesc = input("Digite sua nova descrição: ")
        while novodesc == "":
            print("Descrição inválida")
            novodesc = input("Digite sua nova descrição: ")
        novovalor = input("Digite o novo valor: ")
        while novovalor == "" or novovalor.isalpha():
            print("Valor inválido")
            novovalor = input("Digite o novo valor: ")
        lista_prod[i][0] = novocod
        lista_prod[i][1] = novodesc
        lista_prod[i][2] = novovalor
        arquivo = open("Lista_prod", 'w', encoding="utf-8")
        arquivo.write(lista_prod[i][0] + ";" + lista_prod[i][1] + ";" + lista_prod[i][2] + "\n")
        arquivo.close()
    elif opc == 4:
        listar()
        print("-- Apagar Produtos --")
        apagar()
        print("Apagado com sucesso")

if op == 2:
    print("-- Menu Produtos --")
    listar()
    nome = input("insira seu nome: ")
    while nome == "":
        print("Nome inválido")
        nome = input("insira seu nome: ")
    ped = (input("Digite o código do produto que deseja escolher: "))
    while ped == "":
        print("Código inválido")
        ped = (input("Digite o código do produto que deseja escolher: "))
    if ped == 100:
        x = 0
    elif ped == 101:
        x = 1
    elif ped == 102:
        x = 2
    elif ped == 103:
        x = 3
    elif ped == 104:
        x = 4
    elif ped == 105:
        x = 5
    elif ped == 106:
        x = 6
    elif ped == 107:
        x = 7
    elif ped == 108:
        x = 8
    elif ped == 109:
        x = 9
    elif ped == 110:
        x = 10
    quantidade = int(input("Quantidade que deseja: "))
    while quantidade <= 0:
        print("Quantidade inválida")
        quantidade = int(input("Quantidade que deseja: "))
    preco = quantidade * valor1[x]
    print(f"Pedido: O(A) cliente {nome} pediu {quantidade} {desc1[x]}(s) totalizando R$ {preco} reais")
    print("Volte sempre!")

if op == 0:
    print("Programa encerrado")