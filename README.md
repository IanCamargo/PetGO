# PetGO - Plataforma de Serviços para Pets

![TypeScript](https://img.shields.io/badge/typescript-%23007ACC.svg?style=for-the-badge&logo=typescript&logoColor=white) ![Node.JS](https://img.shields.io/badge/node.js-6DA55F?style=for-the-badge&logo=node.js&logoColor=white) ![Express.js](https://img.shields.io/badge/express.js-%23404d59.svg?style=for-the-badge&logo=express&logoColor=%2361DAFB) ![SQLite](https://img.shields.io/badge/sqlite-%2307405e.svg?style=for-the-badge&logo=sqlite&logoColor=white)

PetGO é uma aplicação web full-stack completa que simula uma plataforma de marketplace para serviços de pets. O projeto conecta donos de pets a uma variedade de prestadores de serviços, como passeadores, hotéis, cuidadores (pet sitters) e veterinários. A aplicação foi construída com foco em uma arquitetura MVC (Model-View-Controller) e renderização no lado do servidor com EJS.

![Screenshot da Aplicação](https://i.imgur.com/uR1uQd6.png)
*(Sugestão: Tire um print da sua tela inicial e substitua o link acima)*

## ✨ Funcionalidades Principais

O projeto possui um conjunto robusto de funcionalidades para três tipos de usuários: Clientes, Parceiros e Administradores.

### Gerais
- **Páginas Públicas:** Homepage, Detalhes de Serviços, Resultados de Busca e Perfil de Parceiros.
- **Busca de Parceiros:** Sistema de busca público por tipo de serviço e localização.
- **Design Responsivo:** Interface adaptável para desktops, tablets e dispositivos móveis.

### Autenticação e Usuários
- **Cadastro Dinâmico:** Formulário de cadastro que se adapta para "Dono de Pet" ou "Parceiro".
- **Login Seguro:** Autenticação com senhas criptografadas (usando `bcrypt`).
- **Sessão com JWT:** Gerenciamento de sessão de usuário através de JSON Web Tokens, mantendo o usuário logado entre as páginas.
- **Header Dinâmico:** A barra de navegação muda, mostrando opções relevantes para usuários logados e visitantes.

### Painel do Cliente (Dono de Pet)
- **Gerenciamento de Pets:** Adicionar e visualizar os pets cadastrados.
- **Agendamento de Serviços:** Fluxo completo para agendar um serviço com um parceiro para um pet específico.
- **Visualização de Agendamentos:** Lista de todos os agendamentos feitos, com seus respectivos status.
- **Sistema de Avaliação:** Possibilidade de avaliar um parceiro com nota e comentário após a conclusão de um serviço.

### Painel do Parceiro
- **Gerenciamento de Perfil:** Parceiros podem criar e atualizar seu perfil público, incluindo título, descrição, localização e os serviços que oferecem.
- **Gerenciamento de Agendamentos:** Visualização de todos os agendamentos recebidos, com a opção de **Aceitar**, **Recusar** ou **Concluir** um serviço, atualizando seu status em tempo real.

### Painel do Administrador
- **Visão Geral da Plataforma:** Um dashboard exclusivo para o admin (acessado com um e-mail especial).
- **Gerenciamento de Usuários:** Visualização de todos os usuários cadastrados, com a opção de **excluir** um usuário ou **alterar sua senha**.
- **Monitoramento de Agendamentos:** Visualização de todos os agendamentos realizados na plataforma.

## 🛠️ Tecnologias Utilizadas

- **Front-end:**
  - **HTML5**
  - **CSS3** (com Variáveis Globais para um mini "Design System")
  - **EJS (Embedded JavaScript templates):** para renderização das páginas no lado do servidor.
  - **JavaScript (Vanilla JS):** para interatividade do lado do cliente (fetch API, manipulação de DOM).

- **Back-end:**
  - **Node.js:** ambiente de execução JavaScript no servidor.
  - **TypeScript:** para um código mais robusto, tipado e seguro.
  - **Express.js:** para o gerenciamento do servidor e das rotas da API.
  - **Bibliotecas Principais:**
    - `cors`: para permitir a comunicação entre domínios.
    - `bcrypt`: para criptografia de senhas.
    - `jsonwebtoken`: para criação e verificação de tokens de autenticação.
    - `sqlite` & `sqlite3`: para a comunicação com o banco de dados.

- **Banco de Dados:**
  - **SQLite:** um banco de dados SQL leve e baseado em arquivo, ideal para desenvolvimento e prototipagem.

## 🚀 Como Rodar o Projeto Localmente

Siga os passos abaixo para executar o PetGO na sua máquina.

### Pré-requisitos
- **Node.js:** É necessário ter o Node.js instalado. A versão LTS é recomendada. Você pode baixá-lo em [nodejs.org](https://nodejs.org/).

### Passos
1.  **Clone o repositório** (ou simplesmente tenha a pasta do projeto em sua máquina).
    ```bash
    git clone [https://github.com/seu-usuario/petgo.git](https://github.com/seu-usuario/petgo.git)
    ```

2.  **Navegue até a pasta do projeto.**
    ```bash
    cd PetGO
    ```

3.  **Instale todas as dependências** do projeto. Este comando irá ler o `package.json` e baixar tudo que é necessário.
    ```bash
    npm install
    ```

4.  **Configure o banco de dados.** Este comando executa o script que cria o arquivo `petgo.db` e todas as tabelas necessárias.
    ```bash
    npm run db:setup
    ```

5.  **Inicie o servidor.**
    ```bash
    npm start
    ```

6.  **Acesse a aplicação!** Abra seu navegador e vá para o endereço:
    [http://localhost:3000](http://localhost:3000)

## 🗺️ Rotas da API

O back-end expõe as seguintes rotas principais:

| Método | Rota                            | Descrição                                         | Protegida |
|--------|---------------------------------|-----------------------------------------------------|-----------|
| `POST` | `/api/cadastro`                 | Registra um novo usuário (cliente ou parceiro).     | Não       |
| `POST` | `/api/login`                    | Autentica um usuário e retorna um token JWT.        | Não       |
| `GET`  | `/api/parceiros/buscar`         | Busca parceiros por serviço e/ou localização.       | Não       |
| `GET`  | `/api/parceiros/:id`            | Busca os detalhes de um perfil de parceiro.         | Não       |
| `GET`  | `/api/parceiros/:id/avaliacoes` | Busca as avaliações de um parceiro específico.      | Não       |
| `GET`  | `/api/pets`                     | Lista os pets do usuário logado.                    | Sim (JWT) |
| `POST` | `/api/pets`                     | Adiciona um novo pet para o usuário logado.         | Sim (JWT) |
| `GET`  | `/api/perfil-parceiro`          | Busca o perfil do parceiro logado.                  | Sim (JWT) |
| `POST` | `/api/perfil-parceiro`          | Cria ou atualiza o perfil do parceiro logado.       | Sim (JWT) |
| `GET`  | `/api/agendamentos`             | Lista os agendamentos do usuário logado.            | Sim (JWT) |
| `POST` | `/api/agendamentos`             | Cria um novo agendamento.                           | Sim (JWT) |
| `PATCH`| `/api/agendamentos/:id/status`  | Atualiza o status de um agendamento.                | Sim (JWT) |
| `GET`  | `/api/admin/usuarios`           | (Admin) Lista todos os usuários.                    | Sim (Admin)|
| `DELETE`| `/api/admin/usuarios/:id`       | (Admin) Deleta um usuário.                          | Sim (Admin)|
| `PUT`  | `/api/admin/usuarios/:id/senha` | (Admin) Altera a senha de um usuário.               | Sim (Admin)|

## 🔮 Próximos Passos e Melhorias Futuras

O projeto tem uma base sólida para crescer. Algumas funcionalidades futuras poderiam incluir:
- **Sistema de Pagamentos:** Integrar um gateway de pagamento (Mercado Pago, Stripe) para processar os pagamentos dos serviços.
- **Calendário de Disponibilidade:** Permitir que os parceiros definam seus horários disponíveis.
- **Chat em Tempo Real:** Uma forma de comunicação direta entre clientes e parceiros via WebSockets.
- **Upload de Imagens:** Permitir que usuários e parceiros adicionem fotos de perfil e dos pets.
- **Refatoração Avançada:** Separar as rotas e a lógica de negócio em arquivos de `controllers` e `models` distintos dentro da pasta `src/`.
