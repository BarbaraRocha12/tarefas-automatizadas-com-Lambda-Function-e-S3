# Tarefas-automatizadas-com-Lambda-Function-e-AWS-S3

Este repositório documenta anotações e insights técnicos adquiridos durante a aula prática sobre **tarefas automatizadas com Amazon S3 e AWS Lambda**.

**Objetivos: 🎯**
* Aplicar os conceitos aprendidos em um ambiente prático (hands-on).
* Documentar processos técnicos de forma clara e estruturada.
* Utilizar o GitHub como ferramenta para compartilhamento de documentação técnica.

**Conceitos: 💡**

### ☁️ Amazon S3 (Simple Storage Service)
É o serviço de **armazenamento de objetos** (object storage) da AWS. Ele permite armazenar e recuperar qualquer quantidade de dados, de qualquer lugar, de forma segura e altamente escalável. É a base para muitas aplicações, servindo como repositório para backups, data lakes, sites estáticos e, neste projeto, como o **gatilho** (trigger) para nossa automação.

**Vantagens do Amazon S3:**
* **Durabilidade:** Projetado para 99.999999999% (11 noves) de durabilidade, protegendo dados contra falhas.
* **Disponibilidade:** Alta disponibilidade, garantindo acesso contínuo aos dados quando necessário.
* **Escalabilidade:** Capacidade de armazenamento virtualmente infinita, que se ajusta automaticamente.
* **Segurança:** Recursos robustos de criptografia, controle de acesso (IAM, Bucket Policies) e monitoramento.

### ⚡ AWS Lambda
É um serviço de computação **serverless** (sem servidor) que permite executar código **em resposta a eventos**, sem a necessidade de provisionar ou gerenciar servidores. Você simplesmente faz o upload do seu código (em Python, Node.js, etc.), e o Lambda cuida de toda a infraestrutura para executá-lo e escalá-lo conforme a demanda.

**Vantagens do AWS Lambda:**
* **Execução Orientada a Eventos:** O código é executado *apenas* quando um gatilho (trigger) ocorre (como um upload no S3, uma chamada de API ou uma alteração em um banco de dados).
* **Escalabilidade Automática:** O Lambda escala horizontalmente de forma instantânea para lidar com milhares de eventos por segundo.
* **Pagamento por Uso (Custo Eficiente):** Você paga apenas pelo tempo de computação que consome (em milissegundos) e pelo número de solicitações, e não por servidores ociosos.
* **Integração Nativa:** Funciona como a "cola" do ecossistema AWS, conectando facilmente diversos serviços.

---

### ⚙️ A Automação: S3 + Lambda
O objetivo deste projeto é usar os dois serviços juntos para criar um fluxo de trabalho automatizado. A lógica é a seguinte:

1.  **Gatilho (Trigger):** O **Amazon S3** é configurado para emitir um evento sempre que uma ação específica ocorre (por exemplo, `ObjectCreated:Put` - "um novo arquivo foi carregado no bucket").
2.  **Execução (Execution):** O **AWS Lambda** é inscrito para "escutar" esse evento específico do S3.
3.  **Ação (Action):** Assim que o S3 detecta o upload do arquivo, ele aciona automaticamente a Função Lambda, passando para ela os detalhes do evento (como o nome do bucket e a chave do objeto). O código dentro da Lambda então executa a tarefa desejada (ex: processar o arquivo, redimensionar uma imagem, analisar um log, etc.).

Essa arquitetura é a base de muitas automações serverless eficientes e de baixo custo na nuvem.
