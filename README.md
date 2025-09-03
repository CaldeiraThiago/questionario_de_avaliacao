# Questionário de Avaliação | Bucket S3

## Visão Geral
Este é um projeto de um website estático hospedado na AWS utilizando a arquitetura serverless, com foco em baixo custo e alta disponibilidade. O projeto foi criado como parte do meu portfólio de arquiteto de soluções.

## Arquitetura
A arquitetura foi projetada para ser simples e eficiente, seguindo os princípios de segurança e otimização de custos da AWS.

- **Amazon S3**: O bucket `questionario-s3` armazena todos os arquivos do site (HTML, CSS, imagens). O S3 é usado para "Static Website Hosting".
- **Amazon CloudFront**: A CDN acelera a entrega do conteúdo e protege o bucket do S3 de acesso direto.

## Passo a Passo da Implementação
1.  **Criação do Bucket S3**:

**Bucket questionario-s3:**

<img width="1650" height="433" alt="image" src="https://github.com/user-attachments/assets/73160bdd-ad1d-4a37-a978-203d2b061984" />

<br>**Versionamento e Tags:** Como boas práticas, deixei o versionamento ativado e inseri Tag para melhor rastreamento do projeto:

<img width="1628" height="431" alt="image" src="https://github.com/user-attachments/assets/aab25fcf-a2ee-4122-ab2a-7ee67930a8da" />

<br>**Hospedagem de Site Estático**: Habilitei a hospedagem e defini o documento de indice "index.html" para o funcionamento do site estatico:

<img width="1639" height="624" alt="image" src="https://github.com/user-attachments/assets/b1d3951f-b423-4770-9bce-23d58fb4198e" />

<br> 2.  **Upload dos Arquivos**:

Realizei o upload dos arquivos do meu site estatico:

<img width="1641" height="644" alt="image" src="https://github.com/user-attachments/assets/e6f48641-a7f4-487f-9d38-99aa824a258b" />

<br>3.  **Configuração do CloudFront**: 

**Distribution Name:**

<img width="1357" height="671" alt="image" src="https://github.com/user-attachments/assets/0cf65775-02fb-4bb0-b0d8-0fa4fd9ea672" /><br>

- **Origin type:** Amazon S3
- **S3 Origin:** questionario-s3.s3.us-east-1.amazonaws.com

<img width="1354" height="686" alt="image" src="https://github.com/user-attachments/assets/3bf19ebb-0118-4040-811b-55c4f2034ce1" />

<br>**Origin access:**
- **Origin access control settings (recommended):** Seguindo as recomendações de segurança para origem de acesso.

**Default cache behavior:**

<img width="662" height="573" alt="image" src="https://github.com/user-attachments/assets/bd9d477c-4f98-48e9-96f6-60a39de4c3df" />


<img width="1640" height="399" alt="image" src="https://github.com/user-attachments/assets/c71591d6-0ccf-4c71-b76c-7302f473a914" /><br>

**Copiei as politicas após as configurações de criação do CloudFront**

<img width="1645" height="739" alt="image" src="https://github.com/user-attachments/assets/30f4e471-9a11-48a1-a0ac-948fe7301085" />


**Politica bucket S3**: Editei as politicas do **bucket questionario-s3** conforme modelo do CloudFront:

<img width="1245" height="704" alt="image" src="https://github.com/user-attachments/assets/3423298f-1c00-4305-9fab-6446255c53be" />

##Observações

**Hospedagem de site estático**: Precisei desabilitar a Hospedagem estática de sites do S3:

<img width="1590" height="257" alt="image" src="https://github.com/user-attachments/assets/36f8eb03-52fd-44d5-b1ba-e6232020215f" /><br>

**Default root object:** Precisei definir no CloudFront o "objeto raiz padrão" para o index.html para que reconheça o arquivo do html:








## Desafios e Soluções
- **Desafio**: Como garantir que o bucket S3 não seja acessado diretamente, apenas pelo CloudFront?
- **Solução**: Utilizei uma "Origin Access Control" (OAC) no CloudFront e bloqueei o acesso público ao bucket do S3. Isso garante que o conteúdo seja acessado apenas pela CDN.

## Custos
Este projeto foi implementado utilizando a **Free Tier** da AWS, com custos estimados em zero dólares.
