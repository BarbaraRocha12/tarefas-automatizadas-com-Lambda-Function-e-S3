## 🏥 Projeto Serverless: Portal de Resultados de Exames

Este projeto implementa um fluxo de trabalho serverless completo na AWS para processar e consultar resultados de exames hospitalares.

---

## 🏛️ Arquitetura do Projeto

A arquitetura do projeto é 100% serverless e dividida em dois fluxos independentes, como ilustrado abaixo:

![Diagrama do Projeto](link-para-sua-imagem.png)

### Fluxo de Ingestão de Dados (Lado do Hospital)

1.  Um **Hospital** faz o upload de um arquivo de exame (`.json`) para um **Bucket S3**.
2.  O upload no S3 dispara automaticamente (via *trigger*) uma **Função Lambda (Python)**.
3.  Esta Lambda lê o arquivo `.json`, extrai as informações do paciente e salva o resultado formatado em uma tabela do **DynamoDB**.

### Fluxo de Consulta de Dados (Lado do Paciente)

1.  O **Paciente** faz uma solicitação (via HTTP GET) para um endpoint do **Amazon API Gateway**, passando seu ID de paciente (ex: `/exame/P12345`).
2.  O API Gateway aciona uma **segunda Função Lambda**.
3.  Esta Lambda consulta o **DynamoDB** pelo ID do paciente, recupera o resultado do exame e o retorna ao paciente através do API Gateway.

### Resumo

Em resumo, é uma arquitetura desacoplada que usa o S3 para armazenamento de arquivos brutos, o DynamoDB como banco de dados de resultados, e o AWS Lambda como a computação "cola" que processa os dados e responde às solicitações, tudo conectado por eventos e APIs.
