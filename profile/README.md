# Good Burguer 

## 📊 Visão Geral

O projeto Good Burger consiste em uma solução de self-service projetada para elevar a experiência do cliente em estabelecimentos do setor alimentício. Este ecossistema é composto por várias aplicações descentralizadas reunidas em uma única aplicação orquestradora utilizando uma infraestrutura de suporte altamente escalável. 
A imagem abaixo ilustra a iteração entre a infraestrutura e a aplicação.

<img width="937" height="638" alt="Captura de tela de 2025-11-16 19-23-40" src="https://github.com/user-attachments/assets/5cfc7f21-38ef-4ffb-9094-45f235f506cd" />

## 🛢️ Serviços

### 🖧 Orchestrator App

Gerencia a execução das aplicações, fazendo o controle das requisições de forma assíncrona. 

### 🪙 Payment App

Gerencia o fluxo de pagamento do pedido, utilizando MongoDB.
Recebe o pedido a ser pago e executa o webhook de pagamento.

### 🛒 Orders App

Gerencia o fluxo de pedidos, utilizando Postegresql.
Recebe o cliente e vários produtos.

### 🍔 Production App

[...]

📄 Repositórios Principais:

1. </> Infraestrutura:
* [Database](https://github.com/good-burguer/lanchonete-database) 
* [Terraform](https://github.com/good-burguer/lanchonete-infra) 
* [Lambda](https://github.com/good-burguer/lanchonete-auth)

2. 📚 Aplicação:
* [Orquestrador](https://github.com/good-burguer/lanchonete-orchestrator)
* [Pagamento](https://github.com/good-burguer/lanchonete-app-pagamento)

## 📋 Detalhes

### ⛁ Database
Infra de RDS Postgres via Terraform (state S3 + lock DynamoDB).

#### Estrutura
- `modules/rds-postgres` módulo do banco
- `environments/dev` ambiente

### ⚙️ Infra
Infra do EKS/VPC/ECR via Terraform.

#### Estrutura
- `modules/` módulos reutilizáveis
- `environments/dev` entrada do ambiente
- `.github/workflows/` pipelines

#### Como validar
1. Defina VARS no repo: `AWS_REGION`, `TF_STATE_BUCKET`, `TF_LOCK_TABLE`
2. O CI rodará `terraform init/validate/plan` em PR e `apply` no merge.

### 🔑 Auth (lambda)

Lambda exposta no API Gateway para autenticação por CPF (SAM).
