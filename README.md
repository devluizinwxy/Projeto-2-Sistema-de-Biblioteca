Projeto 2: Sistema de Biblioteca
Objetivo do Projeto

Gerenciar livros e empréstimos, praticando composição em Programação Orientada a Objetos (POO).

O projeto demonstra como classes podem conter outras classes, representando relações do mundo real:

Um empréstimo tem livros.

Cada livro tem título e autor.

Cada usuário pode ter vários empréstimos.

Classes e Objetivos
1. Livro

Atributos:

titulo – título do livro.

autor – nome do autor.

Objetivo:
Representar um livro da biblioteca.

Validações:

Título e autor não podem ser nulos ou vazios.

Nome do autor deve começar com letra maiúscula.

Exemplo de toString():

- O Pequeno Príncipe(Antoine de Saint-Exupéry)

2. Emprestimo

Atributos:

livros – lista de livros do empréstimo.

horario – data e hora do empréstimo.

Objetivo:
Representar um empréstimo, que pode ter múltiplos livros.

Métodos principais:

addLivro(Livro livro) / removeLivro(Livro livro)

getLivros() / getHorario()

toString() – lista todos os livros do empréstimo e a data do empréstimo.

Exemplo de toString() corrigido:

@Override
public String toString() {
    StringBuilder sb = new StringBuilder();
    for (Livro livro : livros) {
        sb.append(livro.toString()).append("\n");
    }
    sb.append("Data do empréstimo: ").append(getHorario()).append("\n");
    return sb.toString();
}

3. Usuario

Atributos:

nome – nome do usuário.

emprestimos – lista de empréstimos do usuário.

Objetivo:
Cada usuário pode ter vários empréstimos, mostrando a composição:
Usuário → Empréstimos → Livros.

Métodos principais:

addEmprestimo(Emprestimo emprestimo)

toString() – mostra todos os empréstimos do usuário, incluindo os livros de cada empréstimo.

Exemplo de toString() corrigido:

@Override
public String toString() {
    StringBuilder sb = new StringBuilder();
    sb.append("Emprestimos de ").append(getNome()).append(":\n");
    for (Emprestimo e : emprestimos) {
        sb.append(e.toString());
    }
    return sb.toString();
}

Diagrama UML Simplificado
+-----------+       1       *      +------------+       1       *      +-------+
|  Usuario  |---------------------|  Emprestimo |---------------------| Livro |
+-----------+                     +------------+                     +-------+
| - nome   |                       | - horario  |                     | - titulo |
| - emprestimos: List<Emprestimo> | - livros: List<Livro>            | - autor  |
+-----------+                     +------------+                     +-------+
| +addEmprestimo()                 | +addLivro()                       | +getTitulo()
| +getNome()                       | +removeLivro()                     | +getAutor()
| +toString()                      | +getLivros()                       | +toString()
+-----------+                     | +getHorario()                     
                                  | +toString()
                                  +------------+

Exemplo de Uso Interativo (Main.java)
Scanner sc = new Scanner(System.in);
try {
    System.out.print("Usuario: ");
    String nome = sc.nextLine();
    Usuario usuario = new Usuario(nome);

    System.out.print("Quantos livros no empréstimo? ");
    int qntLivros = sc.nextInt();
    sc.nextLine(); // Consumir a quebra de linha

    Emprestimo emprestimo = new Emprestimo();
    for (int i = 0; i < qntLivros; i++) {
        System.out.println("Livro " + (i + 1) + ": ");
        System.out.print("Titulo: ");
        String titulo = sc.nextLine();
        System.out.print("Autor: ");
        String autor = sc.nextLine();
        emprestimo.addLivro(new Livro(titulo, autor));
    }

    usuario.addEmprestimo(emprestimo);
    System.out.println(usuario);

} catch (IllegalArgumentException e) {
    System.out.println(e.getMessage());
}


Exemplo de Entrada:

Usuario: Luis
Quantos livros no empréstimo? 2
Livro 1:
Titulo: O Pequeno Príncipe
Autor: Antoine de Saint-Exupéry
Livro 2:
Titulo: Dom Quixote
Autor: Miguel de Cervantes


Saída Esperada:

Emprestimos de Luis:
- O Pequeno Príncipe(Antoine de Saint-Exupéry)
- Dom Quixote(Miguel de Cervantes)
Data do empréstimo: 14/11/2025 - 22:45:30
