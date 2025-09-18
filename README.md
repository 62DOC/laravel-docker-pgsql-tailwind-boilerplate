# Boilerplate e Tutorial: Laravel, Docker, PostgreSQL & TailwindCSS

![Status](https://img.shields.io/badge/status-conclu%C3%ADdo-brightgreen?style=for-the-badge)

![Laravel](https://img.shields.io/badge/Laravel-12-FF2D20?style=for-the-badge&logo=laravel)
![PHP](https://img.shields.io/badge/PHP-8.2-777BB4?style=for-the-badge&logo=php)
![Docker](https://img.shields.io/badge/Docker-24-2496ED?style=for-the-badge&logo=docker)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-17-336791?style=for-the-badge&logo=postgresql)
![TailwindCSS](https://img.shields.io/badge/TailwindCSS-3-06B6D4?style=for-the-badge&logo=tailwindcss)
![Nginx](https://img.shields.io/badge/Nginx-1.25-009639?style=for-the-badge&logo=nginx)

## 📋 Índice

- [🎯Sobre o Projeto](#-sobre-o-projeto)
- [🚀Para que Serve esta Stack?](#-para-que-serve-esta-stack)
- [🛠️Tecnologias Utilizadas](#-tecnologias-utilizadas)
- [✅ Pré-requisitos na Sua Máquina](#-pré-requisitos-na-sua-máquina)
- [🏁 Guia de Instalação Completo](#-guia-de-instalação-completo)
- [🐳 Comandos Úteis do Dia a Dia](#-comandos-úteis-do-dia-a-dia)
- [💡 Acessando o Banco de Dados](#-acessando-o-banco-de-dados)
- [⚡ Otimização de Performance](#-otimização-de-performance)
- [✍️ Autor e Motivação](#️-autor-e-motivação)
- [📄 Licença](#-licença)
- [🙏 Agradecimentos](#-agradecimentos)

## 🎯 Sobre o Projeto

Este repositório é um **template inicial (`boilerplate`) e um tutorial completo** para criar um ambiente de desenvolvimento robusto e moderno com a stack Laravel, Docker, PostgreSQL e TailwindCSS.

O objetivo principal é ser um recurso didático e prático, projetado para que até mesmo um desenvolvedor iniciante possa configurar um ambiente de desenvolvimento profissional sem erros. Todos os passos foram testados e refinados para prevenir problemas comuns de configuração, como permissões de arquivos, dependências ausentes e inconsistências de ambiente.

Este projeto serve tanto como um guia de aprendizado quanto como uma base sólida e confiável para iniciar novos projetos.

## 🚀 Para que Serve esta Stack?

Esta combinação de tecnologias é extremamente poderosa e adequada para uma vasta gama de projetos web, tais como:

* **Sistemas SaaS (Software as a Service):** Aplicações complexas com painéis administrativos, gerenciamento de usuários e assinaturas.
* **APIs RESTful ou GraphQL:** Para servir dados a aplicativos mobile ou front-ends modernos (React, Vue, etc.).
* **Plataformas de E-commerce:** Lojas virtuais customizadas que exigem um banco de dados relacional robusto como o PostgreSQL.
* **Sistemas de Gerenciamento de Conteúdo (CMS):** Portais, blogs e plataformas de cursos com áreas administrativas complexas.
* **Ferramentas Internas para Empresas:** CRMs, ERPs e dashboards de BI para gerenciamento de operações.

## 🛠️ Tecnologias Utilizadas

Este ambiente utiliza as seguintes tecnologias, a maioria delas rodando de forma isolada dentro de containers Docker:

* **[Laravel 12](https://laravel.com/):** O framework PHP que serve como base para a aplicação.
* **[Docker](https://www.docker.com/):** Orquestra todos os nossos serviços em containers isolados.
* **[PostgreSQL 17](https://www.postgresql.org/):** Nosso banco de dados relacional, rodando em seu próprio container.
* **[TailwindCSS](https://tailwindcss.com/):** Framework CSS para o front-end, gerenciado pelo Node.js.
* **[Nginx](https://www.nginx.com/):** Servidor web que recebe as requisições e as direciona para a aplicação PHP.
* **[PHP 8.2](https://www.php.net/):** A linguagem de programação, rodando dentro do container da aplicação.
* **[Node.js 20](https://nodejs.org/):** Usado para gerenciar e compilar os assets de front-end, também dentro do container da aplicação.
* **[Composer](https://getcomposer.org/):** Gerenciador de dependências para o PHP, utilizado dentro do container.

## ✅ Pré-requisitos na Sua Máquina

A grande vantagem de usar Docker é que você **não precisa** instalar PHP, Node.js, PostgreSQL ou Composer na sua máquina! O Docker cuida de tudo isso para você. Os únicos pré-requisitos reais na sua máquina são:

1.  **[Git](https://git-scm.com/downloads)**
    * Necessário para clonar este repositório.

2.  **[Docker Desktop](https://www.docker.com/products/docker-desktop/)**
    * A ferramenta principal que gerencia tudo. Ela já inclui o **Docker Engine** e o **Docker Compose**.
    * > **IMPORTANTE:** Certifique-se de que o **Docker Desktop esteja em execução** antes de iniciar o processo de instalação.

3.  **Um Editor de Código (Fortemente Recomendado)**
    * Recomendamos o **[Visual Studio Code](https://code.visualstudio.com/)** com a extensão **[WSL](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-wsl)** (para uma melhor performance no Windows).

---

## 🏁 Guia de Instalação Completo

Siga estes passos para ter o ambiente 100% funcional.

#### 1. Clonar o Repositório

Primeiro, clone este repositório para a sua máquina local.

```bash
git clone [https://github.com/seu-usuario/seu-repositorio.git](https://github.com/seu-usuario/seu-repositorio.git)
cd seu-repositorio
```

#### 2. Configurar Variáveis de Ambiente

O projeto precisa de um arquivo `.env` com as "senhas" e configurações da aplicação.

```bash
# Copie o arquivo de exemplo para criar o seu
cp src/.env.example src/.env
```

O arquivo `src/.env` já vem pré-configurado para se conectar ao banco de dados Docker. Nenhuma alteração é necessária para o ambiente de desenvolvimento.

#### 3. Subir os Containers Docker

Este comando vai construir as imagens (se for a primeira vez) e iniciar todos os serviços (`app`, `nginx`, `db`).

```bash
docker-compose up -d --build
```

#### 4. Instalar Dependências do Laravel (Composer)

Com os containers no ar, vamos instalar as dependências do PHP com o Composer.

```bash
docker-compose exec app composer install
```

#### 5. Gerar a Chave da Aplicação

O Laravel precisa de uma chave de encriptação única para segurança.

```bash
docker-compose exec app php artisan key:generate
```

#### 6. Ajustar Permissões (Passo Crucial)

Para evitar erros de "Permission Denied", precisamos garantir que o Laravel possa escrever em suas pastas de `storage` e `cache`.

```bash
docker-compose exec app chown -R www-data:www-data /var/www/storage
docker-compose exec app chown -R www-data:www-data /var/www/bootstrap/cache
```

#### 7. Rodar as Migrations

Este comando cria as tabelas do banco de dados (como a de usuários).

```bash
docker-compose exec app php artisan migrate
```

#### 8. Instalar o Laravel Breeze (TailwindCSS)

Primeiro, baixamos o pacote com o Composer. Depois, rodamos o comando de instalação.

```bash
# 1. Baixar o pacote
docker-compose exec app composer require laravel/breeze --dev

# 2. Instalar (siga as instruções, pressionando Enter para os padrões)
docker-compose exec app php artisan breeze:install
```

#### 9. Instalar Dependências e Compilar o Front-end

Finalmente, instalamos os pacotes NPM e compilamos os arquivos CSS e JS.

```bash
# 1. Instalar pacotes NPM
docker-compose exec app npm install

# 2. Compilar assets para produção
docker-compose exec app npm run build
```

🎉 **PRONTO!** Sua aplicação está no ar. Acesse **[http://localhost:8000](http://localhost:8000)** no seu navegador.

---

## 🐳 Comandos Úteis do Dia a Dia

* **Ligar o ambiente:** `docker-compose up -d`
* **Desligar o ambiente:** `docker-compose down`
* **Executar qualquer comando Artisan:** `docker-compose exec app php artisan <comando>`
* **Acessar o terminal do container da aplicação:** `docker-compose exec app bash`
* **Rodar os testes:** `docker-compose exec app php artisan test`
* **Ver os logs de um container em tempo real:** `docker-compose logs -f app`

## 💡 Acessando o Banco de Dados

Seu banco de dados PostgreSQL está acessível a partir da sua máquina (host) através da porta `5432`. Você pode usar uma ferramenta gráfica como **DBeaver**, **DataGrip** ou **pgAdmin** com as seguintes credenciais:

* **Host:** `localhost`
* **Porta:** `5432`
* **Banco de Dados:** `laravel_db`
* **Usuário:** `sail`
* **Senha:** `password`

## ⚡ Otimização de Performance

É comum notar uma lentidão no carregamento das páginas ao usar Docker no Windows ou macOS devido à sincronização de arquivos. Para melhorar a performance, você pode:

1.  **Usar os Caches do Laravel:** Reduz a leitura de arquivos a cada requisição.
    * **Ligar:** `docker-compose exec app php artisan optimize`
    * **Desligar:** `docker-compose exec app php artisan optimize:clear`

2.  **Habilitar o OPcache do PHP:** Este repositório já inclui um arquivo de configuração (`.docker/php/custom.ini`) que habilita o OPcache, uma extensão do PHP que melhora drasticamente a performance guardando scripts pré-compilados na memória.

<h4 align="right">

[Voltar para o Índice](#-índice)

</h4>

### ✍️ Autor e Motivação

<img src="https://github.com/angelluzk.png" width="100px;" alt="Foto de Angel Luz"/>

> Desenvolvido com 💛 por **Angel Luz**.

📬 E-mail: [contatoangelluz@gmail.com](mailto:contatoangelluz@gmail.com)  
🐙 GitHub: [@angelluzk](https://github.com/angelluzk)  
💼 LinkedIn: [linkedin.com/in/angelitaluz](https://www.linkedin.com/in/angelitaluz/)  
🗂️Website / Portfólio: [meu_portfolio/](https://angelluzk.github.io/meu_portfolio/)  

A motivação para este projeto nasceu do desejo de solidificar o conhecimento nesta stack moderna e, ao mesmo tempo, criar um recurso didático que pudesse ajudar outros desenvolvedores. A jornada para construir este boilerplate envolveu a solução de diversos problemas reais de configuração, e o resultado é este guia, que busca ser o mais claro e à prova de falhas possível.

Espero que este repositório seja tão útil para você em seus projetos quanto foi gratificante para mim construí-lo.

## 📄 Licença

Este projeto está sob a licença MIT.

## 🙏 Agradecimentos

Este projeto foi construído sobre o trabalho incrível de comunidades e indivíduos talentosos. Agradecimentos especiais a:

* Taylor Otwell e todos os contribuidores do ecossistema Laravel.
* À equipe do Docker por transformar o desenvolvimento de software.
* À comunidade global do PostgreSQL.
* À equipe do Tailwind Labs por revolucionar o CSS.