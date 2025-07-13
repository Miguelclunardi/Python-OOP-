🏦 Sistema Bancário com Python e POO 🐍

Bem-vindo ao projeto do Sistema Bancário! Este repositório contém uma implementação de um sistema bancário simples, projetado para demonstrar de forma clara e prática os pilares fundamentais da Programação Orientada a Objetos (POO): Encapsulamento, Herança e Polimorfismo.

🎯 1. Objetivo do Projeto

O objetivo principal é criar um sistema funcional que permita gerenciar clientes e diferentes tipos de contas bancárias (corrente e poupança). Este projeto serve como uma peça de portfólio para demonstrar habilidades em design de software, organização de código e aplicação prática de conceitos de POO em Python.

📂 2. Estrutura de Pastas e Arquivos

A organização do projeto é crucial para manter o código modular, legível e escalável. A estrutura adotada é a seguinte:

sistema_bancario_oo/
├── src/
│   ├── __init__.py      # Torna 'src' um pacote Python
│   ├── conta.py         # Contém as classes ContaBancaria, ContaCorrente, ContaPoupanca
│   ├── cliente.py       # Contém a classe Cliente
│   └── banco.py         # Contém a classe Banco
├── main.py              # Ponto de entrada do programa (interação com o usuário)
└── README.md            # Documentação do projeto

⚙️ 3. Implementação das Classes

A seguir, a descrição detalhada de cada classe e seus requisitos.

📄 Classe ContaBancaria (src/conta.py)

Esta é a classe base (superclasse) que define o comportamento e os atributos comuns a todas as contas do sistema.

    Atributos (privados/protegidos):

        _numero_conta: str ou int (Identificador único da conta).

        _titular: str (Nome do titular da conta).

        _saldo: float (Saldo atual da conta, inicializado em 0.0).

    Métodos:

        __init__(self, numero_conta, titular, saldo_inicial=0.0): Construtor da classe.

        depositar(self, valor): Adiciona um valor ao saldo, se for positivo.

        sacar(self, valor): Lógica de saque padrão. Este método será sobrescrito (polimorfismo) nas classes filhas.

        exibir_saldo(self): Mostra os detalhes da conta e o saldo atual.

        get_numero_conta(self), get_titular(self), get_saldo(self): Getters para acesso seguro aos atributos.

        __str__(self): Retorna uma representação textual formatada do objeto.

💳 Classe ContaCorrente (src/conta.py)

Herda de ContaBancaria e adiciona a funcionalidade de cheque especial.

    Herança: Herda de ContaBancaria.

    Atributos Adicionais:

        _limite_cheque_especial: float (Valor máximo que o saldo pode ficar negativo).

    Métodos:

        __init__(...): Chama o construtor da classe pai (super().__init__()) e inicializa o limite.

        sacar(self, valor): (Polimorfismo) Sobrescreve o método sacar, permitindo que o saque utilize o saldo mais o limite do cheque especial.

💰 Classe ContaPoupanca (src/conta.py)

Herda de ContaBancaria e adiciona a funcionalidade de rendimento de juros.

    Herança: Herda de ContaBancaria.

    Atributos Adicionais:

        _taxa_juros: float (Percentual de juros a ser aplicado).

    Métodos:

        __init__(...): Chama o construtor da classe pai e inicializa a taxa de juros.

        aplicar_juros(self): Calcula e adiciona os juros ao saldo da conta.

        sacar(self, valor): (Polimorfismo) Sobrescreve o método sacar, não permitindo que o saldo fique negativo.

👤 Classe Cliente (src/cliente.py)

Representa um cliente do banco, que pode possuir uma ou mais contas.

    Atributos:

        _nome: str.

        _cpf: str (Identificador único do cliente).

        _contas: list (Agregação de objetos ContaBancaria).

    Métodos:

        adicionar_conta(self, conta): Associa uma nova conta ao cliente.

        remover_conta(self, numero_conta): Remove uma conta da lista do cliente.

        listar_contas(self): Exibe os detalhes de todas as contas do cliente.

        encontrar_conta(self, numero_conta): Busca e retorna um objeto de conta específico.

🏛️ Classe Banco (src/banco.py)

Classe orquestradora que gerencia todo o sistema, clientes e contas.

    Atributos:

        _clientes: list (Agregação de objetos Cliente).

    Métodos:

        adicionar_cliente(self, cliente): Adiciona um novo cliente, evitando duplicidade de CPF.

        encontrar_cliente(self, cpf): Busca e retorna um objeto cliente pelo seu CPF.

        criar_conta_para_cliente(...): Cria e associa uma conta (ContaCorrente ou ContaPoupanca) a um cliente existente.

        realizar_operacao(self, numero_conta, tipo_operacao, valor): Centraliza as operações de depósito e saque.

        exibir_todos_clientes_e_contas(self): Gera um relatório de todos os clientes e suas respectivas contas.

▶️ 4. Lógica Principal (main.py)

Este é o ponto de entrada da aplicação. Ele fornece uma interface de linha de comando (CLI) simples para que o usuário possa interagir com o sistema bancário.

    Menu de Interação: Um loop while apresenta um menu com opções como:

        Adicionar Cliente

        Criar Conta

        Depositar

        Sacar

        Listar Contas de Cliente

        Aplicar Juros (Poupança)

        Listar Todos os Clientes

        Sair

    Fluxo de Operações: Captura a entrada do usuário e chama os métodos apropriados da instância do Banco para executar a ação desejada.

    Tratamento de Entrada: Inclui validações básicas para garantir que os dados inseridos pelo usuário sejam consistentes.

📖 5. Documentação e Execução

    Título: Sistema Bancário Simples com Python e POO

    Descrição: O que o projeto faz e seus objetivos.

    Tecnologias:

    Conceitos de POO Aplicados:

        Encapsulamento: Proteção dos atributos com _ e acesso via métodos (getters).

        Herança: ContaCorrente e ContaPoupanca herdam de ContaBancaria.

        Polimorfismo: O método sacar se comporta de maneiras diferentes em cada tipo de conta.

    Como Executar:

        Clone o repositório: git clone <URL_DO_SEU_REPOSITORIO>

        Navegue até a pasta do projeto: cd sistema_bancario_oo

        Execute o programa principal: python main.py

    Autor: Seu Nome / Usuário do GitHub

✨ 6. Critérios de Avaliação e Refinamento

O código foi desenvolvido seguindo as melhores práticas e com foco nos seguintes pontos:

    ✅ Aplicação Correta dos Princípios de POO

    📂 Organização e Clareza do Código

    ✍️ Legibilidade (Nomes Significativos e Padrões)

    🛡️ Tratamento de Erros e Validações Básicas

    🚀 Funcionalidade Conforme o Esperado
