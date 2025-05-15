# Ambiente Docker para Laravel com PHP 8.3 e Nginx

Este é um ambiente de desenvolvimento Docker otimizado para projetos Laravel, utilizando PHP 8.3 e Nginx. Esta configuração oferece um ambiente completo e personalizável, ideal tanto para desenvolvimento quanto para produção.

## 🚀 Características

- PHP 8.3 com FPM (Alpine Linux)
- Nginx como servidor web
- MySQL 8.0 e PostgreSQL 15
- Redis e Memcached para cache
- Composer para gerenciamento de dependências PHP
- Node.js e NPM inclusos
- Healthchecks em todos os containers
- Volumes nomeados para persistência
- Configuração flexível via variáveis de ambiente
- Ambiente otimizado e leve

## 📋 Pré-requisitos

- Docker
- Docker Compose
- Git

## 🛠️ Estrutura do Projeto

```
.
├── .env                    # Variáveis de ambiente
├── dockerfiles/
│   ├── nginx/
│   │   └── default.conf   # Configuração do Nginx
│   └── php/
│       └── Dockerfile     # Configuração do PHP
├── docker-compose.yml     # Configuração dos serviços
└── src/                   # Código fonte do Laravel
```

## 🔧 Configuração

1. Clone seu projeto Laravel:

```bash
git clone https://github.com/laravel/laravel.git src
```

2. Configure o arquivo de ambiente do projeto:

```bash
cp src/.env.example src/.env
```

3. Configure as variáveis de ambiente do Docker:

```bash
cp .env.example .env
```

4. Ajuste as variáveis no arquivo `.env` conforme necessário:

- Configurações do MySQL (MYSQL\_\*)
- Configurações do PostgreSQL (POSTGRES\_\*)
- Configurações do Redis (REDIS\_\*)
- Configurações do Memcached (MEMCACHED\_\*)
- Portas dos serviços

## ⚡ Inicialização

1. Construa e inicie os containers:

```bash
docker compose up -d
```

2. Instale as dependências do Laravel:

```bash
docker compose exec application composer install
```

3. Gere a chave da aplicação:

```bash
docker compose exec application php artisan key:generate
```

4. Configure as permissões:

```bash
docker compose exec application chown -R www-data:www-data /var/www/storage
```

5. Execute as migrações do banco de dados (escolha um):

```bash
# Para MySQL
docker compose exec application php artisan migrate

# Para PostgreSQL
DB_CONNECTION=pgsql docker compose exec application php artisan migrate
```

6. Instale as dependências do Node.js (se necessário):

```bash
docker compose exec application npm install
```

## 🌐 Acesso aos Serviços

- Aplicação: http://localhost
- MySQL: localhost:3306
- PostgreSQL: localhost:5432
- Redis: localhost:6379
- Memcached: localhost:11211

## 💾 Persistência de Dados

Os seguintes volumes nomeados são criados para garantir a persistência dos dados:

- `app-source`: Arquivos da aplicação
- `mysql-data`: Dados do MySQL
- `postgres-data`: Dados do PostgreSQL
- `redis-data`: Dados do Redis

## 🏥 Healthchecks

Todos os serviços incluem healthchecks para monitoramento:

- **PHP-FPM**: Verifica a sintaxe do PHP a cada 30 segundos
- **Nginx**: Verifica a configuração a cada 30 segundos
- **MySQL**: Verifica a conectividade a cada 30 segundos
- **PostgreSQL**: Verifica a disponibilidade do banco a cada 30 segundos
- **Redis**: Verifica a resposta do servidor a cada 30 segundos
- **Memcached**: Verifica a porta do serviço a cada 30 segundos

## 📝 Notas

- Todos os serviços usam Alpine Linux quando possível para manter as imagens leves
- As configurações podem ser facilmente ajustadas através do arquivo `.env`
- Os healthchecks garantem o monitoramento da saúde dos serviços
- Os volumes nomeados garantem a persistência dos dados mesmo após a recriação dos containers

## 🤝 Contribuições

Sinta-se à vontade para contribuir com melhorias nesta configuração através de Pull Requests.
