# crud
#e uma função que so mostar o menu principal
def menu_principal():
    while True:
        print('***bem vindo ao menu principal***')
        print('1. estudante: ')
        print('2. disciplina: ')
        print('3. professor: ')
        print('4. turma: ')
        print('5. matrícula: ')
        print('9.sair: ')
        return str(input('faça uma escolha'))



#e uma função que so mostar o menu de operações
def mostrar_menu_operacoes():
    print('bem vindo ao menu de operações')
    print('***escolha uma opção***')
    print('1. incluir; ')
    print('2. listar; ')
    print('3. excluir ;')
    print('4. atualizar ;')
    print('9.voltar ao menu principal; ')
    return input('faça uma escolha ;')



#a partir daqui e so função para aluno

def incluir_aluno(nome_arquivo):
    while True:
        try:
            codigo = int(input('digite o codigo; '))
        except:
            print('ATENÇÃO o codigo so aceita numeros')
            break
        nome = input('nome do aluno; ')
        cpf = input('digite o cpf; ')
        novo_estudante=[{
            'cod':codigo,
            'nome':nome,
            'cpf':cpf
            }]
        lista_qualquer = ler_arquivo(nome_arquivo)
        lista_qualquer.append(novo_estudante)
        salvar_arquivo(lista_qualquer,nome_arquivo)




def listagem_cadastro(nome_arquivo):
    lista_qualquer = ler_arquivo(nome_arquivo)
    if len(lista_qualquer) == 0:
        print('a lista esta vazia')
    else:
        for cadastro in lista_qualquer:
            print(f'dados do cadastro {cadastro}')


def exclusao_cadastro(codigo,nome_arquivo):
    cadastro_para_remover = None
    lista_qualquer = ler_arquivo(nome_arquivo)
    for cadastro in lista_qualquer:
        if cadastro['codigo'] == codigo:
            cadastro_para_remover = cadastro
            break

    if cadastro_para_remover is not None:
        lista_qualquer.remove(cadastro_para_remover)
        salvar_arquivo(lista_qualquer,nome_arquivo)
    else:
        print('codigo não encontrado')

def edicao_cadastro(codigo,nome_arquivo):
    lista_qualquer = ler_arquivo(nome_arquivo)
    for cadastro in lista_qualquer:
        if cadastro['codigo']==codigo:
            cadastro['nome'] = input('digite o novo nome')
            cadastro['cpf'] = input('digite o novo cpf')
            salvar_arquivo(lista_qualquer, nome_arquivo)
            return

    print('codigo não encontrado')

def processar_menu_operacoes(opcao_secundaria,nome_arquivo):
    if opcao_secundaria == '1':
        incluir_aluno(nome_arquivo)
    elif opcao_secundaria == '2':
        listagem_cadastro(nome_arquivo)
    elif opcao_secundaria == '3':
        codigo = int(input('digite o codigo para remover'))
        exclusao_cadastro(codigo, nome_arquivo)
    elif opcao_secundaria == '4':
        codigo = int(input('digite o codigo para editar'))
        edicao_cadastro(codigo, nome_arquivo)
    elif opcao_secundaria == '9':
        print('voltando ao menu principal')
        return False
    else:
        input('opção invalida; ')

    return True

#ate aqui e função so para aluno

#a partir daqui e displina

def incluir_disciplina(nome_arquivo):
    while True:
        global codigo_discipina
        try:
            codigo_discipina = int(input('digite o codigo da disciplina; '))
        except:
            print('ATENÇÃO digite um numero')
            break
        nome_disciplina = input('nome da disciplina ; ')
        nova_disciplina = {
            'codigo': codigo_discipina,
            'nome_disciplina': nome_disciplina,
        }
        lista_qualquer = ler_arquivo(nome_arquivo)
        lista_qualquer.append(nova_disciplina)
        salvar_arquivo(lista_qualquer, nome_arquivo)

def processar_menu_operacoes_disciplina(opcao_secundaria, nome_arquivo):
        if opcao_secundaria == '1':
            incluir_disciplina(nome_arquivo)
        elif opcao_secundaria == '2':
            listagem_cadastro(nome_arquivo)
        elif opcao_secundaria == '3':
            codigo = int(input('digite o codigo para remover'))
            exclusao_cadastro(codigo, nome_arquivo)
        elif opcao_secundaria == '4':
            codigo = int(input('digite o codigo para editar'))
            edicao_cadastro_disciplina(codigo,nome_arquivo)
        elif opcao_secundaria == '9':
            print('voltando ao menu principal')
            return False
        else:
            input('opção invalida; ')

def edicao_cadastro_disciplina(codigo,nome_arquivo):
    lista_qualquer = ler_arquivo(nome_arquivo)
    for cadastro in lista_qualquer:
        if cadastro['codigo']==codigo:
            cadastro['nome_disciplina'] = input('digite o novo nome da disciplina')
            salvar_arquivo(lista_qualquer, nome_arquivo)
            return

#displina ate aqui

#professor


def incluir_professor(nome_arquivo):
    global codigo
    while True:
        try:
            codigo = int(input('digite o codigo; '))
        except:
            print('ATENÇÃO digite um numero')
            break
        nome = input('nome do professor; ')
        cpf = input('digite o cpf do professor; ')
        novo_estudante = {
               'codigo': codigo,
            'nome': nome,
            'cpf': cpf
        }
        lista_qualquer = ler_arquivo(nome_arquivo)
        lista_qualquer.append(novo_estudante)
        salvar_arquivo(lista_qualquer, nome_arquivo)

def processar_menu_operacoes_professor(opcao_secundaria,nome_arquivo):
    if opcao_secundaria == '1':
        incluir_professor(nome_arquivo)
    elif opcao_secundaria == '2':
        listagem_cadastro(nome_arquivo)
    elif opcao_secundaria == '3':
        codigo = int(input('digite o codigo para remover'))
        exclusao_cadastro(codigo, nome_arquivo)
    elif opcao_secundaria == '4':
        codigo = int(input('digite o codigo para editar'))
        edicao_cadastro_professor(codigo,nome_arquivo)
    elif opcao_secundaria == '9':
        print('voltando ao menu principal')
        return False
    else:
        input('opção invalida; ')

    return True

def edicao_cadastro_professor(codigo,nome_arquivo):
    lista_qualquer = ler_arquivo(nome_arquivo)
    for cadastro in lista_qualquer:
        if cadastro['codigo']==codigo:
            cadastro['nome'] = input('digite o novo nome do professor')
            cadastro['cpf'] = input('digite o novo cpf')
            salvar_arquivo(lista_qualquer, nome_arquivo)
            return

    print('codigo não encontrado')

#professor

#turma

def incluir_turma(nome_arquivo):
    while True:
        try:
            codigo = int(input('digite o codigo da turma; '))
        except:
            print('ATENÇÃO digite numeros')
            break
        codigo_do_professor = int(input('codigo do professor; '))
        codigo_da_disciplina = int(input('digite o codigo da disciplina; '))
        turma = {
            'codigo': codigo,
             'codigo_do_professor': codigo_do_professor,
             'codigo_da_disciplina': codigo_da_disciplina
        }
        lista_qualquer = ler_arquivo(nome_arquivo)
        lista_qualquer.append(turma)
        salvar_arquivo(lista_qualquer, nome_arquivo)

def processar_menu_operacoes_turma(opcao_secundaria,nome_arquivo):
    if opcao_secundaria == '1':
        incluir_turma(nome_arquivo)
    elif opcao_secundaria == '2':
        listagem_cadastro(nome_arquivo)
    elif opcao_secundaria == '3':
        codigo = int(input('digite o codigo para remover'))
        exclusao_cadastro(codigo, nome_arquivo)
    elif opcao_secundaria == '4':
        codigo = int(input('digite o codigo para editar'))
        edicao_cadastro_turma(codigo,nome_arquivo)
    elif opcao_secundaria == '9':
        print('voltando ao menu principal')
        return False
    else:
        input('opção invalida; ')

    return True

def edicao_cadastro_turma(codigo,nome_arquivo):
    lista_qualquer = ler_arquivo(nome_arquivo)
    for cadastro in lista_qualquer:
        if cadastro['codigo']==codigo:
            cadastro['codigo_do_professor'] = int(input('digite o novo codigo do professor '))
            cadastro['codigo_da_disciplina'] = int(input('digite o novo codigo da disciplina'))
            salvar_arquivo(lista_qualquer, nome_arquivo)
            return
#turma

#matricula
def incluir_matricula(nome_arquivo):
        try:
            codigo_turma = int(input('digite o codigo da turma; '))
        except:
            print('ATENÇÃO digite numeros')

        codigo_do_estudante = int(input('codigo do estudante; '))
        turma = {
            'codigo_turma': codigo_turma,
            'codigo_do_estudante': codigo_do_estudante
        }
        lista_qualquer = ler_arquivo(nome_arquivo)
        lista_qualquer.append(turma)
        salvar_arquivo(lista_qualquer, nome_arquivo)

def processar_menu_operacoes_matricula(opcao_secundaria,nome_arquivo):
    if opcao_secundaria == '1':
        incluir_matricula(nome_arquivo)
    elif opcao_secundaria == '2':
        listagem_cadastro(nome_arquivo)
    elif opcao_secundaria == '3':
        codigo = int(input('digite o codigo para remover'))
        exclusao_cadastro(codigo, nome_arquivo)
    elif opcao_secundaria == '4':
        codigo = int(input('digite o codigo para editar'))
        edicao_cadastro_matricula(codigo,nome_arquivo)
    elif opcao_secundaria == '9':
        print('voltando ao menu principal')
        return False
    else:
        input('opção invalida; ')

    return True

def edicao_cadastro_matricula(codigo,nome_arquivo):
    lista_qualquer = ler_arquivo(nome_arquivo)
    for cadastro in lista_qualquer:
        if cadastro['codigo_turma']==codigo:
            cadastro['codigo_do_estudante'] = int(input('digite o novo codigo do estudante'))
            salvar_arquivo(lista_qualquer, nome_arquivo)
            return

    print('codigo não encontrado')

#embaixo e duas uma salva e outra para ler que estão de maneira generica

def salvar_arquivo(lista_qualquer,nome_arquivo):
    with open(nome_arquivo,'w',encoding='utf-8') as arquivo_aberto:
        json.dump(lista_qualquer,arquivo_aberto,ensure_ascii=False)

def ler_arquivo(nome_arquivo):
    try:
        with open(nome_arquivo,'r',encoding='utf-8') as arquivo_aberto:
            lista_qualquer = json.load(arquivo_aberto)

        return lista_qualquer
    except:
        return[]



#Sistema de Gerenciamento Acadêmico puc
#menu principal
arquivo_estudante = 'estudantes.json'
arquivo_disciplina = 'disciplina.json'
arquivo_professor = 'professor.json'
arquivo_turma = 'turma.json'
arquivo_matricula = 'matricula.json'

#menu de operações
while True:
    opcao=menu_principal()
    if opcao == '1':
        print('voce escolheu a opção aluno')
        while True:

            opcao_secundaria=mostrar_menu_operacoes()
            if not processar_menu_operacoes(opcao_secundaria,arquivo_estudante):
                break
    elif opcao == '2':
        print('voce escolheu a opção disciplina')
        while True:

            opcao_secundaria=mostrar_menu_operacoes()
            if not processar_menu_operacoes_disciplina(opcao_secundaria,arquivo_disciplina):
                break
    elif opcao == '3':
        print('voce escolheu a opção professor')
        while True:

            opcao_secundaria = mostrar_menu_operacoes()
            if not processar_menu_operacoes_professor(opcao_secundaria,arquivo_professor):
                break
    elif opcao == '4':
        print('voce escolheu a opção turma')
        while True:

            opcao_secundaria = mostrar_menu_operacoes()
            if not processar_menu_operacoes_turma(opcao_secundaria,arquivo_turma):
                break
    elif opcao == '5':
        print('voce escolheu a opção matricula')
        while True:

            opcao_secundaria = mostrar_menu_operacoes()
            if not processar_menu_operacoes_matricula(opcao_secundaria,arquivo_matricula):
                break
    else:
        opcao == '9'
        break
