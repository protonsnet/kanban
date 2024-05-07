Aplicação Kanban em PHP com SQLite e Bootstrap
Devido à complexidade de criar uma aplicação web completa dentro desta resposta, vou fornecer um guia passo a passo e exemplos de código para te auxiliar na construção da sua aplicação Kanban.
1. Ambiente e Dependências:
PHP: Certifique-se de ter o PHP instalado e configurado no seu ambiente de desenvolvimento.
SQLite: Baixe e instale o SQLite para o seu sistema operacional.
Bootstrap: Baixe o Bootstrap ou utilize um CDN para incluir os arquivos CSS e JavaScript em seu projeto.
2. Estrutura de Arquivos:
Crie a seguinte estrutura de pastas para sua aplicação:
kanban/
├── css/
│   └── style.css
├── js/
│   └── script.js
├── index.php
└── database.sqlite
Use code with caution.
3. Banco de Dados SQLite:
Crie um arquivo database.sqlite e execute o seguinte comando SQL para criar a tabela tasks:
CREATE TABLE tasks (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    nome TEXT NOT NULL,
    data DATE NOT NULL,
    descricao TEXT,
    usuario TEXT
);
Use code with caution.
SQL
4. Arquivo index.php:
Este arquivo conterá o HTML da sua aplicação Kanban. Utilize o Bootstrap para a estrutura e estilo.
<!DOCTYPE html>
<html>
<head>
    <title>Kanban Board</title>
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css">
    <link rel="stylesheet" href="css/style.css">
</head>
<body>
    <div class="container">
        <h1>Kanban Board</h1>
        <!-- Aqui você adicionará o código HTML para os cartões Kanban -->
    </div>

    <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/popper.js@1.16.1/dist/umd/popper.min.js"></script>
    <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/js/bootstrap.min.js"></script>
    <script src="js/script.js"></script>
</body>
</html>
Use code with caution.
PHP
5. Adicionando Tarefas (PHP e SQLite):
Crie um formulário em index.php para que os usuários adicionem novas tarefas. Utilize PHP para processar o formulário e inserir os dados no banco de dados SQLite.
Exemplo de código PHP para inserir dados:
<?php
// Conexão com o banco de dados
$db = new PDO('sqlite:database.sqlite');

// Processamento do formulário
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $nome = $_POST["nome"];
    $data = $_POST["data"];
    $descricao = $_POST["descricao"];
    $usuario = $_POST["usuario"];

    // Inserindo dados no banco
    $stmt = $db->prepare("INSERT INTO tasks (nome, data, descricao, usuario) VALUES (?, ?, ?, ?)");
    $stmt->execute([$nome, $data, $descricao, $usuario]);
}
?>
Use code with caution.
PHP
6. Exibindo Tarefas (PHP):
Utilize PHP para recuperar as tarefas do banco de dados e exibi-las na interface Kanban. Utilize o Bootstrap para criar cartões para cada tarefa.
Exemplo de código PHP para recuperar e exibir tarefas:
<?php
// ... (código de conexão com o banco de dados)

$stmt = $db->query("SELECT * FROM tasks");
while ($row = $stmt->fetch(PDO::FETCH_ASSOC)) {
    echo '<div class="card">';
    echo '  <div class="card-body">';
    echo '    <h5 class="card-title">' . $row['nome'] . '</h5>';
    echo '    <p class="card-text">' . $row['descricao'] . '</p>';
    echo '    <p class="card-text">Usuário: ' . $row['usuario'] . '</p>';
    echo '    <p class="card-text">Data: ' . $row['data'] . '</p>';
    echo '  </div>';
    echo '</div>';
}
?>
Use code with caution.
PHP
7. Estilizando com CSS:
Utilize o arquivo style.css para customizar a aparência do seu Kanban. Você pode usar o Bootstrap grid system para organizar os cartões em colunas (ex: "A Fazer", "Em Andamento", "Concluído").
8. Interações com JavaScript:
Utilize o arquivo script.js para adicionar interações à sua aplicação, como arrastar e soltar cartões entre colunas, atualizar o status das tarefas, etc. Você pode utilizar bibliotecas JavaScript como jQuery UI para facilitar o desenvolvimento dessas funcionalidades.
9. Segurança:
Lembre-se de implementar medidas de segurança para proteger sua aplicação contra ataques, como validação de dados e prevenção de injeção SQL.
Observações:
Este é um exemplo básico. Você pode adicionar mais funcionalidades, como editar e excluir tarefas, filtrar por usuário ou data, etc.
Considere utilizar um framework PHP como Laravel ou Symfony para projetos mais complexos.
Com este guia e exemplos de código, você pode começar a construir sua aplicação Kanban em PHP com SQLite e Bootstrap. Lembre-se de pesquisar e adaptar o código de acordo com suas necessidades.
