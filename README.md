🎵 Sistema Musical

Gerenciador completo e responsivo de artistas, álbuns e catálogo de músicas desenvolvido em PHP Nativo e MySQL.

📸 Sobre o Projeto

O Sistema Musical é uma aplicação web para cadastro, organização e navegação em acervos musicais. Ele conta com controle de acesso por autenticação, gestão de artistas com upload e tratamento de imagens, gerenciamento de músicas integradas com links do YouTube e uma biblioteca com filtros de busca dinâmicos.

✨ Funcionalidades

🔐 Autenticação de Usuários: Login seguro utilizando controle de sessão ($_SESSION) e senhas criptografadas com bcrypt.

🎤 Gestão de Artistas (CRUD):

Cadastro, edição e listagem de artistas.

Exclusão protegida (impede apagar artistas que possuem músicas vinculadas).

Upload e redimensionamento automático de foto de perfil (JPG/PNG).

🎵 Gestão de Músicas (CRUD):

Vinculação com o artista correspondente.

Inserção de álbum, gênero musical e letra completa.

Suporte a links do YouTube com extração automática do ID do vídeo para reprodução.

Upload de capa do álbum.

🎼 Biblioteca Musical & Filtros:

Busca geral por palavra-chave (título, álbum ou artista).

Filtro individual por artista e por gênero musical.

Preservação dos filtros ativos na URL durante a navegação.

📱 Layout Responsivo: Interface limpa e adaptável desenvolvida em CSS moderno (Flexbox e Grid).

🛠️ Tecnologias Utilizadas

PHP 8.x (Nativo)

MySQL / MariaDB

Biblioteca GD do PHP (para redimensionamento e processamento das imagens)

HTML5 & CSS3 (Custom Properties, Flexbox e CSS Grid)

🚀 Como Executar o Projeto

1. Pré-requisitos

Instale um servidor local com suporte a PHP e MySQL (ex: XAMPP, WAMP, Laragon ou MAMP). Certifique-se de que a extensão GD do PHP está habilitada.

2. Clonar ou Copiar os Arquivos

Coloque a pasta do projeto no diretório raiz do seu servidor web (exemplo no XAMPP: htdocs/sistema-musical).

3. Configurar o Banco de Dados

Abra o phpMyAdmin (geralmente em http://localhost/phpmyadmin).

Vá na aba SQL e execute o script contido em bd.sql:

CREATE DATABASE sistema_musical_v2;
USE sistema_musical_v2;

CREATE TABLE usuarios (
    id INT AUTO_INCREMENT PRIMARY KEY,
    usuario VARCHAR(50) NOT NULL,
    senha VARCHAR(255) NOT NULL
);

CREATE TABLE artistas (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    genero VARCHAR(50),
    pais VARCHAR(50),
    imagem VARCHAR(255)
);

CREATE TABLE musicas (
    id INT AUTO_INCREMENT PRIMARY KEY,
    artista_id INT,
    titulo VARCHAR(100) NOT NULL,
    album VARCHAR(100),
    genero VARCHAR(50),
    youtube_link VARCHAR(255),
    letra TEXT,
    imagem_capa VARCHAR(255),
    FOREIGN KEY (artista_id) REFERENCES artistas(id)
);

INSERT INTO usuarios (usuario, senha) 
VALUES ('admin', '$2y$12$zw1c2aDgt4HHnAzXc3g3dOV6Mn96Dm2UaSIketIhYe1xmtuaJG6qa');


4. Ajustar Conexão com o Banco

Se necessário, altere as credenciais no arquivo conexao.php:

$servername = "localhost";
$username   = "root";
$password   = "SuaSenhaAqui";
$dbname     = "sistema_musical_v2";


5. Acessar no Navegador

Acesse no seu navegador:
http://localhost/sistema-musical/login.php

🔑 Credenciais de Acesso Padrão

Usuário: admin

Senha: 123

💡 Para criar novas senhas criptografadas, você pode rodar o script php geraSenha.php no terminal.

📂 Estrutura do Projeto

sistema-musical/
├── bd.sql               # Script de criação do banco de dados
├── conexao.php          # Conexão com o MySQL e criação do diretório img/
├── geraSenha.php        # Utilitário para geração de hash de senha (bcrypt)
├── valida_sessao.php    # Middleware de verificação de autenticação
├── login.php            # Tela de login e autenticação
├── logout.php           # Encerramento seguro de sessão
├── index.php            # Painel principal / Menu
├── cadastro_artista.php # CRUD de artistas e upload de foto
├── cadastro_musica.php  # CRUD de músicas, capa do álbum e link do YouTube
├── listagem_musicas.php # Biblioteca musical com busca e filtros dinâmicos
├── styles.css           # Estilização global do sistema
└── img/                 # Pasta de armazenamento das imagens (gerada automaticamente)


🛡️ Segurança Implementada

Prevenção contra SQL Injection: Uso consistente de Prepared Statements (mysqli::prepare) em todas as operações com o banco.

Proteção contra XSS: Sanitização de saídas com htmlspecialchars().

Armazenamento Seguro de Senhas: Algoritmo BCRYPT via password_hash() e password_verify().

Upload Seguro: Validação rigorosa de extensões (jpg, jpeg, png), limite de tamanho (5MB) e verificação via getimagesize().
