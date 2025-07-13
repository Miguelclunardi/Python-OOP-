# Python-OOP-

Documento de Projeto: Sistema Bancário Simples com POO em Python

Este documento descreve as etapas e requisitos para a construção de um Sistema Bancário simples, focado em demonstrar os pilares da Programação Orientada a Objetos (POO): Encapsulamento, Herança e Polimorfismo.
1. Objetivo do Projeto

O objetivo principal é criar um sistema funcional que permita gerenciar clientes e diferentes tipos de contas bancárias (corrente e poupança), aplicando os conceitos de POO de forma clara e organizada. Este projeto servirá como portfólio no seu GitHub para comprovar suas habilidades em POO em Python.
2. Estrutura de Pastas e Arquivos

A organização do projeto é crucial. Siga a seguinte estrutura para manter o código modular e legível:

sistema_bancario_oo/
├── src/
│   ├── __init__.py      # Torna 'src' um pacote Python
│   ├── conta.py         # Contém as classes ContaBancaria, ContaCorrente, ContaPoupanca
│   ├── cliente.py       # Contém a classe Cliente
│   └── banco.py         # Contém a classe Banco
├── main.py              # Ponto de entrada do programa (interação com o usuário)
└── README.md            # Documentação do projeto

3. Implementação das Classes

A seguir, a descrição detalhada de cada classe e seus requisitos. Lembre-se de aplicar o encapsulamento utilizando o prefixo _ para atributos que devem ser internos à classe, e forneça métodos "getters" para acessá-los.
3.1. Classe ContaBancaria (src/conta.py)

Esta é a classe base que define o comportamento comum a todas as contas.

    Atributos (privados/protegidos):

        _numero_conta: str ou int (identificador único da conta).

        _titular: str (nome do titular da conta).

        _saldo: float (saldo atual da conta, inicializado em 0.0 por padrão).

    Métodos:

        __init__(self, numero_conta, titular, saldo_inicial=0.0): Construtor que inicializa os atributos.

        depositar(self, valor):

            Recebe um valor (float).

            Se valor for positivo, adiciona ao _saldo.

            Caso contrário, imprime uma mensagem de erro.

            Imprime uma mensagem de sucesso e o novo saldo.

        sacar(self, valor):

            Recebe um valor (float).

            Implementa a lógica padrão: se valor for positivo e _saldo for suficiente, subtrai do _saldo.

            Imprime mensagens de sucesso/erro ("Saldo insuficiente.").

            Retorna True em caso de sucesso, False caso contrário.

            Este método será sobrescrito nas classes filhas para implementar regras específicas.

        exibir_saldo(self): Imprime o número da conta, titular e o saldo atual.

        get_numero_conta(self): Retorna o _numero_conta.

        get_titular(self): Retorna o _titular.

        get_saldo(self): Retorna o _saldo.

        __str__(self): Retorna uma representação em string formatada da conta (e.g., "Conta: [numero] | Titular: [titular] | Saldo: R$[saldo]").

3.2. Classe ContaCorrente (src/conta.py)

Esta classe herda de ContaBancaria e adiciona a funcionalidade de cheque especial.

    Herança: Deve herdar de ContaBancaria.

    Atributos Adicionais (privados/protegidos):

        _limite_cheque_especial: float (valor máximo que o saldo pode ficar negativo).

    Métodos:

        __init__(self, numero_conta, titular, saldo_inicial=0.0, limite_cheque_especial=0.0):

            Chama o construtor da classe pai (super().__init__()).

            Inicializa o _limite_cheque_especial.

        sacar(self, valor):

            Sobrescreve (Polimorfismo) o método sacar da ContaBancaria.

            Permite o saque se o _saldo mais o _limite_cheque_especial for suficiente para cobrir o valor.

            Atualiza o _saldo e imprime mensagens apropriadas.

            Retorna True em caso de sucesso, False caso contrário.

3.3. Classe ContaPoupanca (src/conta.py)

Esta classe também herda de ContaBancaria e adiciona a funcionalidade de aplicação de juros.

    Herança: Deve herdar de ContaBancaria.

    Atributos Adicionais (privados/protegidos):

        _taxa_juros: float (percentual de juros, e.g., 0.005 para 0.5%).

    Métodos:

        __init__(self, numero_conta, titular, saldo_inicial=0.0, taxa_juros=0.0):

            Chama o construtor da classe pai (super().__init__()).

            Inicializa a _taxa_juros.

        aplicar_juros(self):

            Calcula os juros (_saldo * _taxa_juros) e os adiciona ao _saldo.

            Imprime uma mensagem de sucesso e o novo saldo.

        sacar(self, valor):

            Sobrescreve (Polimorfismo) o método sacar da ContaBancaria.

            NÃO permite saque se o _saldo for insuficiente (não permite saldo negativo).

            Retorna True em caso de sucesso, False caso contrário.

3.4. Classe Cliente (src/cliente.py)

Representa um cliente do banco, que pode possuir múltiplas contas.

    Atributos (privados/protegidos):

        _nome: str.

        _cpf: str (identificador único do cliente).

        _contas: list (uma lista de objetos ContaBancaria, ContaCorrente ou ContaPoupanca).

    Métodos:

        __init__(self, nome, cpf): Construtor.

        adicionar_conta(self, conta):

            Recebe um objeto conta (instância de ContaBancaria ou suas subclasses).

            Adiciona a conta à lista _contas.

        remover_conta(self, numero_conta):

            Remove uma conta da lista _contas pelo numero_conta.

            Imprime mensagem de sucesso/erro.

        listar_contas(self):

            Imprime os detalhes de todas as contas associadas ao cliente.

            Se não houver contas, informa.

        encontrar_conta(self, numero_conta):

            Procura e retorna o objeto ContaBancaria (ou subclasse) correspondente ao numero_conta.

            Retorna None se a conta não for encontrada.

        get_nome(self): Retorna o _nome.

        get_cpf(self): Retorna o _cpf.

        __str__(self): Retorna uma representação em string formatada do cliente.

3.5. Classe Banco (src/banco.py)

A classe que orquestra todo o sistema, gerenciando clientes e a criação/busca de contas.

    Atributos (privados/protegidos):

        _clientes: list (uma lista de objetos Cliente).

    Métodos:

        __init__(self): Construtor.

        adicionar_cliente(self, cliente):

            Recebe um objeto cliente (instância de Cliente).

            Adiciona o cliente à lista _clientes.

            Verifica se o CPF já existe para evitar duplicidade.

        encontrar_cliente(self, cpf):

            Procura e retorna o objeto Cliente correspondente ao cpf.

            Retorna None se o cliente não for encontrado.

        criar_conta_para_cliente(self, cpf_cliente, tipo_conta, numero_conta, saldo_inicial=0.0, **kwargs):

            Localiza o cliente pelo cpf_cliente. Se não encontrar, informa e retorna None.

            Verifica se o numero_conta já existe em alguma conta do banco para evitar duplicidade global.

            Cria uma nova conta (instância de ContaCorrente ou ContaPoupanca) com base em tipo_conta (e.g., "corrente", "poupanca").

            Utiliza **kwargs para passar argumentos específicos (limite_cheque_especial, taxa_juros).

            Adiciona a conta recém-criada ao cliente e imprime sucesso/erro.

            Retorna o objeto da conta criada.

        realizar_operacao(self, numero_conta, tipo_operacao, valor):

            Encontra a conta pelo numero_conta.

            Se a conta for encontrada, executa a tipo_operacao ("depositar" ou "sacar") com o valor.

            Imprime mensagens de sucesso/erro.

        exibir_todos_clientes_e_contas(self):

            Itera sobre todos os clientes e, para cada cliente, chama listar_contas().

4. Lógica Principal do Programa (main.py)

Este arquivo será o "ponto de entrada" do seu programa. Ele importará as classes e fornecerá uma interface de usuário simples (baseada em texto) para interagir com o sistema.

    Importações: Importe as classes necessárias de src.

    Instanciação: Crie uma instância da classe Banco.

    Menu de Interação:

        Implemente um loop while que exiba um menu de opções para o usuário (ex: "1. Adicionar Cliente", "2. Criar Conta", "3. Depositar", "4. Sacar", "5. Listar Contas de Cliente", "6. Aplicar Juros (Poupança)", "7. Sair").

        Use input() para capturar a escolha do usuário.

        Utilize if/elif/else para direcionar a execução com base na escolha.

    Fluxo de Operações:

        Adicionar Cliente: Solicita nome e CPF, cria um objeto Cliente e o adiciona ao Banco.

        Criar Conta: Solicita CPF do cliente, tipo de conta (corrente/poupança), número da conta, saldo inicial e, se aplicável, limite de cheque especial ou taxa de juros. Chama o método criar_conta_para_cliente do Banco.

        Depositar/Sacar: Solicita número da conta, valor e o tipo de operação. Chama o método realizar_operacao do Banco.

        Listar Contas de Cliente: Solicita CPF e chama o listar_contas() do Cliente encontrado.

        Aplicar Juros (Conta Poupança): Solicita o número da conta, encontra a conta, verifica se é uma ContaPoupanca e chama aplicar_juros().

        Sair: Encerra o programa.

    Tratamento de Entrada: Valide as entradas do usuário (ex: números devem ser números, CPF deve ser string, etc.).

5. Documentação para o GitHub (README.md final)

Ao final do projeto, crie ou atualize o arquivo README.md na raiz do seu repositório GitHub. Ele deve conter:

    Título: Nome do projeto (ex: "Sistema Bancário Simples com Python e POO").

    Descrição: O que o projeto faz и seus objetivos.

    Tecnologias: Python.

    Conceitos de POO Aplicados: Explique como você utilizou Encapsulamento, Herança e Polimorfismo no seu código.

    Como Executar: Instruções claras sobre como clonar o repositório e rodar o main.py.

    Exemplos de Uso: Pequenos exemplos de como usar o menu do programa.

    Autor: Seu nome/usuário do GitHub.

6. Avaliação e Refinamento

A avaliação do código será focada em:

    Correta aplicação dos princípios de POO: Encapsulamento, Herança, Polimorfismo.

    Organização do Código: Clareza das classes, métodos e estrutura de arquivos.

    Legibilidade: Nomes de variáveis e métodos significativos, comentários úteis.

    Tratamento de Erros: Validações básicas de entrada e lógicas de negócio.

    Funcionalidade: O programa funciona como esperado.
