
from datetime import datetime

# Lista de usuários
usuarios = []

# Função para exibir o menu
def exibir_menu():
    print("Menu:")
    print("1. Criar usuário")
    print("2. Listar usuários")
    print("3. Atualizar usuário")
    print("4. Deletar usuário")
    print("5. Verificar status do boleto")
    print("6. Sair")

# Função para criar um novo usuário
def criar_usuario():
    nome = input("Digite o nome do usuário: ")
    cpf = input("Digite o CPF do usuário: ")
    data_boleto = input("Digite a data de vencimento do boleto (no formato dd/mm/aaaa): ")
    endereco = input("Digite o endereço do usuário: ")
    usuario = {'Nome': nome, 'CPF': cpf, 'Data de vencimento do boleto': datetime.strptime(data_boleto, '%d/%m/%Y'), 'Endereço': endereco}
    usuarios.append(usuario)
    print("Usuário criado com sucesso!")

# Função para listar todos os usuários
def listar_usuarios():
    if not usuarios:
        print("Nenhum usuário cadastrado.")
    else:
        for usuario in usuarios:
            print(usuario)

# Função para atualizar um usuário
def atualizar_usuario():
    cpf = input("Digite o CPF do usuário que deseja atualizar: ")
    for usuario in usuarios:
        if usuario['CPF'] == cpf:
            usuario['Nome'] = input("Novo nome do usuário: ")
            usuario['Data de vencimento do boleto'] = datetime.strptime(input("Nova data de vencimento do boleto (no formato dd/mm/aaaa): "), '%d/%m/%Y')
            usuario['Endereço'] = input("Novo endereço do usuário: ")
            print("Usuário atualizado com sucesso!")
            return
    print("Usuário não encontrado.")

# Função para deletar um usuário
def deletar_usuario():
    cpf = input("Digite o CPF do usuário que deseja deletar: ")
    for usuario in usuarios:
        if usuario['CPF'] == cpf:
            usuarios.remove(usuario)
            print("Usuário deletado com sucesso!")
            return
    print("Usuário não encontrado.")

# Função para verificar o status do boleto de um usuário
def verificar_status_boleto():
    cpf = input("Digite o CPF do usuário para verificar o status do boleto: ")
    for usuario in usuarios:
        if usuario['CPF'] == cpf:
            data_atual = datetime.now()
            mes_atual = data_atual.month
            mes_vencimento = usuario['Data de vencimento do boleto'].month
            if mes_vencimento == 4:  # Se o mês de vencimento for abril
                print("O boleto do usuário está vencido.")
            elif mes_atual < mes_vencimento:  # Se o mês atual for menor que o mês de vencimento
                print("O boleto do usuário ainda não venceu.")
            else:
                print("O boleto do usuário está dentro da data de vencimento.")
            return
    print("Usuário não encontrado.")

# Loop principal
while True:
    exibir_menu()
    opcao = input("Escolha uma opção: ")

    if opcao == '1':
        criar_usuario()
    elif opcao == '2':
        listar_usuarios()
    elif opcao == '3':
        atualizar_usuario()
    elif opcao == '4':
        deletar_usuario()
    elif opcao == '5':
        verificar_status_boleto()
    elif opcao == '6':
        print("Saindo...")
        break
    else:
        print("Opção inválida. Tente novamente.")


