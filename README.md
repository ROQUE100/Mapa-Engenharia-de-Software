# Mapa-Engenharia-de-Software

## Bibliotecário Chefe
Como bibliotecário chefe de uma grande biblioteca pública, tenho a visão de modernizar nossos serviços de empréstimo de livros e acesso a recursos educacionais. A biblioteca tem um vasto acervo de livros, revistas, e materiais multimídia que atualmente são gerenciados manualmente ou através de um sistema local defasado. Nosso objetivo é criar um Sistema de Biblioteca Online que possa ser acessado por nossos usuários de qualquer lugar, facilitando o acesso ao acervo, aos serviços de empréstimo e à administração de contas de usuário. Este sistema deve não apenas atender às necessidades atuais, mas também ser escalável para suportar futuras expansões e integrações.
### Necessidades do Sistema (Problemas a serem solucionados)

* NE001 - Acesso Remoto: Usuários devem poder acessar o sistema de qualquer lugar, utilizando dispositivos como computadores, tablets e smartphones.
* NE002 - Catálogo de Acervo: O sistema deve permitir a navegação, busca e visualização detalhada dos itens do acervo da biblioteca.
* NE003 - Gerenciamento de Empréstimos: Usuários devem poder reservar e renovar empréstimos de livros online.
* NE004 - Conta de Usuário: Cada usuário deve ter uma conta pessoal onde possa visualizar seu histórico de empréstimos, multas, e reservas
* NE005 - Administração do Sistema: Bibliotecários devem poder adicionar, remover e atualizar itens no acervo, gerenciar contas de usuários e monitorar empréstimos.

### Requisitos Funcionais

* RF001 - Cadastro de Usuários - O sistema deve permitir que novos usuários se registrem criando uma conta com informações pessoais básicas.
* RF002 - Autenticação de Usuários - O sistema deve fornecer opções de login para que os usuários possam acessar suas contas.
* RF003 - Catálogo de Livros - O sistema deve permitir que os usuários pesquisem livros por título, autor, gênero, ou ISBN.
* RF004 - Visualização de Detalhes do Livro - O sistema deve exibir informações detalhadas sobre um livro, como título, autor, sinopse, número de páginas, e disponibilidade.
* RF005 - Empréstimo de Livros - O sistema deve permitir que os usuários reservem livros para empréstimo, especificando a data de retirada.
* RF006 - Renovação de Empréstimos - O sistema deve permitir que os usuários renovem seus empréstimos, se o livro não estiver reservado por outro usuário.
* RF007 - Histórico de Empréstimos - O sistema deve fornecer um histórico de todos os empréstimos feitos por um usuário.
* RF008 - Gestão de Multas - O sistema deve calcular e exibir multas por atraso de devolução de livros.
* RF009 - Adição e Atualização de Livros (Admin) - Bibliotecários devem poder adicionar novos livros ao catálogo, bem como atualizar ou remover livros existentes.
* RF010 - Gerenciamento de Contas de Usuário (Admin) - Bibliotecários devem poder visualizar, suspender e excluir contas de usuários.

# Para esta atividade de mapa, crie um diagrama de classe considerando as seguintes classes: 
1. **Biblioteca**  
2. **Livro**
3. **Bibliotecario**
4. **Usuario**
5. **Emprestimo**

## Descrição dos Fluxos do Caso de Uso

### 1. Cadastro de Usuários
Ator: Novo Usuário
1. O novo usuário acessa a página de cadastro.
2. O usuário preenche suas informações pessoais (cpf, nome, email, senha).
3. O sistema valida as informações e cria uma nova conta de usuário.
4. O usuário recebe uma confirmação do cadastro via email.

### 2. Empréstimo de Livros
Ator: Usuário Registrado
1. O usuário faz login no sistema.
2. O usuário navega ou busca o catálogo de livros.
3. O usuário seleciona um livro e solicita o empréstimo.
4. O sistema verifica a disponibilidade do livro.
5. O sistema registra o empréstimo e atualiza o status do livro.
6. O usuário recebe uma confirmação do empréstimo e a data de devolução.

### 3. Adição de Livros (Admin)
Ator: Bibliotecário
1. O bibliotecário faz login no sistema com permissões administrativas.
2. O bibliotecário acessa a seção de gerenciamento de livros.
3. O bibliotecário preenche as informações do novo livro (ISBN, título, autor, sinopse.).
4. O sistema valida as informações e adiciona o novo livro ao catálogo.
5. O bibliotecário recebe uma confirmação da adição do livro.

classDiagram
    class Biblioteca {
        - List~Livro~ livros
        - List~Usuario~ usuarios
        - List~Emprestimo~ emprestimos
        + adicionarLivro(Livro)
        + removerLivro(Livro)
        + cadastrarUsuario(Usuario)
        + realizarEmprestimo(Usuario, Livro)
        + renovarEmprestimo(Emprestimo)
    }

    class Livro {
        - String ISBN
        - String titulo
        - String autor
        - String sinopse
        - int numeroPaginas
        - boolean disponivel
        + getDetalhes()
        + setDisponivel(boolean)
    }

    class Usuario {
        - String cpf
        - String nome
        - String email
        - String senha
        - List~Emprestimo~ historicoEmprestimos
        + realizarLogin(email, senha)
        + visualizarHistorico()
        + solicitarEmprestimo(Livro)
        + renovarEmprestimo(Emprestimo)
    }

    class Bibliotecario {
        - String id
        - String nome
        - String email
        - String senha
        + adicionarLivro(Livro)
        + removerLivro(Livro)
        + atualizarLivro(Livro)
        + gerenciarUsuario(Usuario)
    }

    class Emprestimo {
        - Date dataEmprestimo
        - Date dataDevolucao
        - Livro livro
        - Usuario usuario
        + calcularMulta()
        + renovarEmprestimo()
    }

    Biblioteca --> Livro : contém
    Biblioteca --> Usuario : contém
    Biblioteca --> Emprestimo : contém
    Usuario --> Emprestimo : realiza
    Livro --> Emprestimo : é emprestado em
    Bibliotecario --> Livro : gerencia
    Bibliotecario --> Usuario : gerencia



   
