# Pipeline de Dados Serverless de Ponta a Ponta para Processamento de Notas Fiscais usando AWS e Streamlit

Este projeto consiste em um pipeline de engenharia de dados de ponta a ponta (End-to-End) totalmente Serverless e orientado a eventos para a ingestão, extração de texto, armazenamento e estruturação de dados de Notas Fiscais (PDF). 

O principal objetivo da solução é automatizar o fluxo de recebimento de documentos fiscais de forma resiliente, escalável e de baixo custo, utilizando o concept de Data Lake com camadas bem definidas.

## 🏗️ Arquitetura da Solução

O desenho técnico mapeia o fluxo completo dos dados desde o upload até a persistência no banco de dados NoSQL:

![Arquitetura do Pipeline](https://github.com/AndersonSarmento/aplicacao_nota_fiscal/raw/main/imagens/Pipeline%20de%20Dados%20Serverless%20de%20Ponta%20a%20Ponta%20para%20.jpg)

### 📝 Resumo Executivo do Fluxo

Use o Amazon API Gateway e o AWS Lambda para integrar o seu frontend em Streamlit a um pipeline de dados moderno, simplificando a ingestão e extração automatizada de notas fiscais em cenários serverless. O frontend realiza o upload seguro do arquivo PDF para o API Gateway, que engatilha uma função Lambda responsável por extrair os dados textuais e persistir o arquivo original em um bucket do Amazon S3, garantindo o armazenamento resiliente e isolado na camada Raw do seu Data Lake. Adicionalmente, com uma arquitetura desacoplada e orientada a eventos, o salvamento do arquivo de texto em uma camada posterior dispara automaticamente uma segunda função Lambda, permitindo que você faça o input e a indexação dos dados estruturados no Amazon DynamoDB de forma altamente escalável e sem a necessidade de gerenciar servidores.

---

## 🛠️ Tecnologias e Ferramentas Utilizadas

* **Frontend:** Streamlit (Python) para a interface de upload do usuário.
* **API Layer:** Amazon API Gateway para exposição de endpoints REST seguros.
* **Compute (Serverless):** AWS Lambda para processamento assíncrono e lógica de extração.
* **Storage (Data Lake):** Amazon S3 estruturado em camadas (*Raw/Bronze* e *Trusted/Silver*).
* **Database:** Amazon DynamoDB (NoSQL) para armazenamento rápido e flexível das notas fiscais estruturadas.

## 🚀 Principais Benefícios desta Arquitetura

1.  **Desacoplamento de Componentes:** A falha em um estágio (ex: lentidão no banco de dados) não interrompe a ingestão inicial dos PDFs.
2.  **Custo Eficiente (Serverless):** Cobrança estritamente sob demanda. Se nenhuma nota fiscal for enviada, o custo de computação é zero.
3.  **Persistência de Resgate:** Salvar o estado em formato de texto no S3 antes de enviar ao banco de dados garante que os dados extraídos nunca sejam perdidos.