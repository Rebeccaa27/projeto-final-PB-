


<h1 style="text-align: center;">Migração e Modernização da Infraestrutura para AWS</h1>



<div style="text-align: center;">
  <img src="./img/projeto%20final.webp" alt="Minha Imagem" style="max-width: 50%; height: 50%;">
</div>


### **Escopo Detalhado**
O objetivo deste projeto é migrar a infraestrutura de TI da empresa **Fast Engineering S/A** para a AWS, com foco em modernização e escalabilidade, atendendo à alta demanda de acessos e compras no eCommerce. O projeto será realizado em duas etapas:

- **Etapa 1: Lift-and-Shift ("As-Is")**: Migração inicial da infraestrutura para a AWS, sem mudanças significativas, com o intuito de melhorar a performance e escalabilidade, mantendo a estrutura atual.
  
- **Etapa 2: Modernização com Kubernetes**: Modernização da infraestrutura, utilizando Kubernetes para gerenciar os contêineres e facilitar a escalabilidade e automação.

---

### **Etapa 1: Lift-and-Shift ("As-Is")**

#### **Quais atividades são necessárias para a migração?**
- **Levantamento da infraestrutura atual:** Identificação e mapeamento dos servidores, banco de dados e componentes utilizados pela aplicação.
- **Planejamento da migração:** Definição do plano de ação para a migração dos servidores de banco de dados, backend e frontend para a AWS.
- **Transferência de dados e configuração:** 
  - Migração do banco de dados MySQL para AWS RDS.
  - Transferência de arquivos estáticos (imagens, vídeos) para o S3.
  - Instância de servidores EC2 para os serviços de backend e frontend.
- **Configuração de balanceamento de carga:** Implementação de Elastic Load Balancer (ELB) para distribuir o tráfego de rede entre as instâncias.
- **Testes de validação:** Realização de testes para garantir que a infraestrutura na AWS atenda às necessidades de escalabilidade.

#### **Quais as ferramentas vão ser utilizadas?**
- **AWS Application Migration Service (MGN):** Para facilitar a migração dos servidores.
- **Amazon EC2:** Para instâncias de computação que hospedam as aplicações.
- **Amazon RDS:** Para gerenciar o banco de dados de forma escalável e resiliente.
- **Amazon S3:** Para armazenar arquivos estáticos de forma segura e escalável.
- **Elastic Load Balancer (ELB):** Para distribuir o tráfego de forma equilibrada entre as instâncias.
- **AWS CloudWatch:** Para monitoramento da infraestrutura e logs.

#### **Qual o diagrama da infraestrutura na AWS?**
- **Instâncias EC2:** Hospedagem de servidores de frontend e backend.
- **RDS (MySQL):** Banco de dados gerenciado e escalável.
- **S3:** Armazenamento de objetos (imagens, vídeos, etc.).
- **ELB (Elastic Load Balancer):** Balanceamento de carga entre instâncias EC2.
- **CloudWatch:** Monitoramento de logs e métricas de performance.

#### **Como serão garantidos os requisitos de Segurança?**
- **IAM (Identity and Access Management):** Controle de permissões de acesso para recursos da AWS.
- **Grupos de Segurança (Security Groups):** Definição de regras para controlar o tráfego de entrada e saída nas instâncias.
- **Criptografia:** Ativação de criptografia de dados em trânsito (SSL/TLS) e em repouso (RDS e S3).
- **Monitoramento com AWS CloudTrail:** Registro e auditoria de todas as ações feitas na AWS.

#### **Como será realizado o processo de Backup?**
- **Backup no RDS:** Ativação de backups automáticos no Amazon RDS para garantir a persistência dos dados.
- **Snapshots EC2 e EBS:** Criação de snapshots periódicos das instâncias EC2 e volumes EBS.
- **Armazenamento de backups no S3:** Backup de dados adicionais e snapshots armazenados no S3 com versionamento ativado.

#### **Qual o custo da infraestrutura na AWS (AWS Calculator)?**
- Estimativa de custos será realizada utilizando o **AWS Pricing Calculator**, que incluirá os custos para instâncias EC2, RDS, S3, ELB, e serviços de monitoramento.

---

### **Etapa 2: Modernização com Kubernetes**

#### **Quais atividades são necessárias para a migração?**
- **Refatoração para Contêineres:** Modificação das aplicações para que possam ser executadas em contêineres Docker.
- **Configuração do Kubernetes (EKS):** Criação do cluster Kubernetes no Amazon EKS (Elastic Kubernetes Service) para orquestrar os contêineres.
- **Automação de Deploy (CI/CD):** Implementação de pipelines de CI/CD com **AWS CodePipeline** e **AWS CodeBuild**.
- **Escalabilidade automática:** Implementação de auto scaling para aumentar ou diminuir o número de pods de acordo com a carga.

#### **Quais as ferramentas vão ser utilizadas?**
- **Amazon EKS (Elastic Kubernetes Service):** Para orquestração de contêineres no Kubernetes.
- **Docker:** Para criar e empacotar as aplicações em contêineres.
- **AWS CodePipeline e CodeBuild:** Para automação do deployment contínuo (CI/CD).
- **AWS S3:** Para armazenamento de objetos persistentes.
- **AWS CloudWatch e CloudTrail:** Para monitoramento e logs da infraestrutura.

#### **Qual o diagrama da infraestrutura na AWS?**
- **EKS:** Para orquestração de contêineres com pods e serviços.
- **RDS:** Banco de dados gerenciado.
- **S3:** Armazenamento de arquivos persistentes.
- **ELB:** Balanceamento de carga entre instâncias e pods do Kubernetes.
- **CloudWatch e CloudTrail:** Monitoramento e auditoria.

#### **Como serão garantidos os requisitos de Segurança?**
- **IAM (Identity and Access Management):** Controle de permissões e funções para usuários e serviços no Kubernetes.
- **SSL/TLS:** Criptografia de dados em trânsito e repouso.
- **AWS GuardDuty e CloudTrail:** Monitoramento proativo de segurança e auditoria de eventos.
- **Pod Security Policies:** Implementação de políticas de segurança para os pods no Kubernetes.

#### **Como será realizado o processo de Backup?**
- **Backup no RDS:** Backups automáticos e snapshots diários.
- **Backup de contêineres e volumes EBS:** Uso de snapshots EBS e backups de dados no S3.
- **Armazenamento de logs:** Armazenamento de logs de aplicações e sistemas no S3.

#### **Qual o custo da infraestrutura na AWS (AWS Calculator)?**
- Estimativa de custos será realizada novamente com o **AWS Pricing Calculator**, levando em consideração a utilização de **EKS**, **RDS**, **S3**, **ELB**, **CloudWatch**, e outros serviços necessários para a modernização da infraestrutura.

---

### **Conclusão**
A migração para a AWS e a modernização com Kubernetes trarão maior escalabilidade, flexibilidade e segurança para a **Fast Engineering S/A**. A implementação de uma infraestrutura moderna na nuvem permitirá que a empresa atenda à crescente demanda de acessos e compras de forma eficiente e segura. O uso de práticas de DevOps com pipelines de CI/CD, contêineres, e Kubernetes garantirá um ambiente ágil e escalável, pronto para suportar o crescimento do eCommerce no futuro.


