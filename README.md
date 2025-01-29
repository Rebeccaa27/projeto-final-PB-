


<h1 style="text-align: center;">Migração e Modernização da Infraestrutura para AWS</h1>

![Diagrama do contexto atual](./img/projeto%20final.webp)


### **Escopo Detalhado**
### **Contexto** 🌍

**Empresa:** Fast Engineering S/A

**Parceiro:** TI Soluções Incríveis

**Situação Atual:**
- Nosso eCommerce está crescendo rapidamente e a infraestrutura atual está sobrecarregada, não atendendo à alta demanda de acessos e compras.
- Infraestrutura atual:
  - **Servidor de Banco de Dados MySQL:** 💾
    - 500GB de dados
    - 10GB de RAM
    - 3 Core CPU
  - **Servidor para Aplicação (Frontend REACT):** 💻
    - 5GB de dados
    - 2GB de RAM
    - 1 Core CPU
  - **Servidor de Backend (3 APIs com Nginx como Balanceador):** 🔧
    - Armazena estáticos como fotos e links
    - 5GB de dados
    - 4GB de RAM
    - 2 Core CPU


![Diagrama do contexto atual](./img/situacaoatual.png)

# Migração da Infraestrutura de TI para AWS

## Visão Geral

O objetivo deste projeto é migrar a infraestrutura de TI da empresa Fast Engineering S/A para a AWS, com foco em modernização e escalabilidade. Essa migração permitirá atender à alta demanda de acessos e compras no e-commerce da empresa.

# Migração da Infraestrutura de TI para AWS

## Visão Geral

O objetivo deste projeto é migrar a infraestrutura de TI da empresa Fast Engineering S/A para a AWS, com foco em modernização e escalabilidade. Essa migração permitirá atender à alta demanda de acessos e compras no e-commerce da empresa.

---
## 🛠️ **Fases do Projeto** 🛠️

O projeto será realizado em duas etapas principais:

### **1️⃣ Etapa 1: Lift-and-Shift**
**Migração inicial da infraestrutura para a AWS, sem mudanças significativas, focada em melhorar a performance e escalabilidade, mantendo a estrutura atual.**

---

### **2️⃣ Etapa 2: Modernização com Kubernetes**
**Reestruturação da infraestrutura para adoção de Kubernetes, facilitando escalabilidade, automação e gerenciamento de contêineres.**

- **Ambiente Kubernetes**
- **Banco de dados gerenciado (PaaS e Multi AZ)**
- **Backup de dados**
- **Sistema para persistência de objetos (imagens, vídeos etc.)**
- **Segurança**

---


## Tecnologias Utilizadas  

Tecnologias Utilizadas
- ☁️ AWS – Serviços de nuvem para hospedagem, migração e segurança.
- 🐳 Kubernetes – Orquestração de contêineres para escalabilidade e automação.
- 🐙 GitHub – Controle de versão e colaboração no desenvolvimento.
- 🔧 Terraform – Infraestrutura como código (IaC) utilizada para provisionamento automatizado e criação da pipeline de CI/CD.
- 🔐 AWS WAF – Proteção contra ataques web, bloqueando tráfego malicioso e garantindo a segurança da aplicação.
- 📡 Amazon RDS – Banco de dados gerenciado com alta disponibilidade e backup automático.
- 💡 Helm – Gerenciamento de pacotes Kubernetes, facilitando a instalação e manutenção de recursos.
- 📦 Amazon ECR – Armazenamento e gerenciamento de imagens Docker do backend e frontend.
- 📶 Amazon EKS – Orquestração de containers no Kubernetes, proporcionando escalabilidade e alta disponibilidade para a aplicação.
- 📥 Amazon CloudWatch – Monitora logs e métricas de performance da infraestrutura e aplicação.
- 📤 AWS Secrets Manager – Armazenamento seguro de segredos e credenciais.

 
## Etapa 1: Lift-and-Shift  

## Quais atividades são necessárias para a migração?

#### 🔹 1. Preparação do Ambiente AWS
**Configuração da VPC (Virtual Private Cloud):**  
Criar uma rede privada para hospedar as instâncias EC2 e outros recursos necessários.

#### 🔹 2. Configuração de Subnets

**Subnet Pública**  
Hospeda as instâncias de réplica, permitindo comunicação entre a AWS e os servidores de origem.  
As réplicas terão acesso à internet para:
- Comunicação com o servidor de origem.
- Acesso à API do AWS Application Migration Service (MGN).

**Subnets Privadas**  
Destinadas a instâncias EC2 e banco de dados RDS, sem acesso direto à internet.  
Exemplos de recursos alocados:
- Frontend
- Backend
- Banco de dados

#### 🔹 3. Portas de Comunicação para Replicação
A migração exige a abertura de portas específicas para comunicação entre os servidores de origem e a AWS:

| Porta (TCP) | Uso |
| --- | --- |
| 443 | Comunicação entre o servidor de replicação e a API do AWS MGN. |
| 1500 | Transferência segura de dados do servidor de origem para a AWS (comprimido e criptografado). |

#### 🔹 4. Configuração das Ferramentas de Migração

**AWS Application Migration Service (MGN)**  
Criação do serviço AWS MGN, responsável pela replicação contínua dos servidores de origem para a AWS.  
Configuração de EBS para armazenamento de discos replicados, garantindo criptografia (EBS Encryption).

**Criação de Usuário IAM para Replicação**  
Criar um usuário IAM para o AWS Replication Agent.  
Anexar a política AWSApplicationMigrationAgentPolicy.  
(Opcional) Adicionar tags para rastreamento de custos.  
Salvar as credenciais geradas.

**Configuração de Launch Templates**  
Criar um Launch Template para definir as instâncias EC2 replicadas.  
Configurar:

- **AMI (Amazon Machine Image):** Definir a imagem base para as instâncias.
- **Tipo de instância:** Escolher o tipo da instância, como t2.micro
- **VPC e Subnets:** Configurar a rede virtual e subnets para as instâncias.
- **Grupos de segurança:** Definir regras para proteger as instâncias.
- **Chaves SSH:** Adicionar chaves SSH para permitir acesso remoto seguro (se necessário).

#### Execução da Migração
- Instalação do AWS Replication Agent nas máquinas de origem.
- Configuração do AWS DMS (Database Migration Service) para migração do banco de dados MySQL → Amazon RDS.
- Replicação contínua dos servidores para a AWS.

#### Testes Pós-Migração
- Validação de integridade dos dados replicados.
- Testes de desempenho das instâncias EC2 e banco de dados RDS.
- Verificação do funcionamento das aplicações no novo ambiente.

#### Finalização e Otimização
- Desativação dos recursos locais após a validação do sucesso da migração.

## Quais as ferramentas vão ser utilizadas?

A migração será realizada com os seguintes serviços AWS:

| **Serviço**                | **Função**                                                                                  |
|----------------------------|---------------------------------------------------------------------------------------------|
| **AWS MGN**                | Automação para migrar as aplicações locais para a nuvem AWS.                                |
| **AWS Replication Agent**  | Captura e transfere dados para o **Replication Server**.                                   |
| **AWS EC2**                | Computação para replicação dos servidores locais e para testes com servidores migrados.    |
| **AWS S3**                 | O **MGN** se conecta com buckets **S3** para baixar softwares e arquivos de configuração.   |
| **AWS EBS**                | Armazena volumes persistentes durante e após a migração.                                    |
| **AWS RDS**                | Para gerenciar o novo banco de dados na AWS.                                                |
| **AWS DMS**                | Migração do banco de dados MySQL para Amazon **RDS**.                                       |
| **AWS Route 53**           | Gerencia DNS, facilitando a troca de servidores durante a migração.                         |
| **AWS CloudWatch**         | Monitora a performance das instâncias durante a migração e após a conclusão.                |



## Qual o diagrama da infraestrutura na AWS?

Este diagrama ilustra o processo de migração de um servidor local para a infraestrutura da AWS Cloud, destacando as ferramentas e componentes envolvidos na transição, incluindo a migração de dados, aplicativos e a configuração de recursos na AWS.

![Diagrama infraestrutura de migração](./img/primierodiagrama.png)

## Como serão garantidos os requisitos de Segurança?  

1️⃣ **Controle de Acesso e Autenticação**  
-  **AWS IAM**: Uso de permissões mínimas necessárias (principle of least privilege).  

2️⃣ **Segurança na Replicação e Migração**  
-  **AWS Replication Agent**: Transmissão segura via canais criptografados.  
-  **AWS DMS**: Migração com criptografia ativada.  

3️⃣ **Configuração de Portas Seguras**  

| Porta | Uso |
| --- | --- |
| 443 | Comunicação do AWS MGN com servidores locais. |
| 1500 | Comunicação entre servidores locais e AWS. |
| 3306 | Acesso ao banco MySQL (Amazon RDS). |

4️⃣ **Segurança na Infraestrutura**  
- **VPC Security Groups**: Controle rigoroso de tráfego baseado em regras específicas de entrada e saída.  
- **Network ACLs**: Proteção adicional com regras de filtragem no nível da sub-rede.  

5️⃣ **Uso de CloudFront e Route 53 para Acesso Seguro**  
- **CloudFront**: Distribuição de conteúdo segura e otimizada para usuários finais.  
- **Route 53**: Gerenciamento seguro de DNS para resolução eficiente de nomes de domínio.  

## Como será realizado o processo de Backup?

### 🔹 Backup e Recuperação de Dados  

Garantir a segurança dos dados é essencial. Para isso, utilizamos soluções automatizadas da AWS que garantem a integridade e disponibilidade das informações.  

#### **1. Backup do Banco de Dados (Amazon RDS)**  
- O **Amazon RDS** realiza **backups automáticos**, sem necessidade de intervenção manual.  
- Os dados podem ser **restaurados para um ponto específico no tempo**, caso ocorra alguma falha.  
- A retenção dos backups pode ser configurada conforme a necessidade, garantindo a segurança dos dados a longo prazo.  

#### **2. Backup do Armazenamento (Amazon EBS e AWS Backup)**  
- O **Amazon EBS** gera **snapshots periódicos** dos volumes de armazenamento, permitindo uma rápida recuperação em caso de falhas ou corrupção de dados.  
- O **AWS Backup** automatiza e centraliza esses backups, garantindo maior organização e facilidade na restauração.  
- Com o **AWS Backup**, é possível criar **planos personalizados**, definindo regras de retenção e agendamentos para atender a requisitos de conformidade e recuperação.  


## Qual o custo da infraestrutura na AWS (AWS Calculator)?

![Diagrama pós migração](./img/custosprimeiro1.png)

![Diagrama pós migração](./img/custosprimeiro.png)
---

## **Etapa 2: Modernização com Kubernetes**

## Quais atividades são necessárias para a migração?

A migração utiliza **Terraform** para provisionar infraestrutura na **AWS**, gerenciando um ambiente baseado em **EKS** (Elastic Kubernetes Service) com suporte para **CI/CD via GitHub**. A arquitetura inclui:

## 🔹 **Fluxo da Infraestrutura**

### **IAM** (Identity and Access Management)
- Gerencia as permissões de acesso a todos os recursos da AWS.
- Permite provisionamento seguro e controlado da infraestrutura, garantindo que apenas usuários e sistemas autorizados possam realizar ações específicas.

### **GitHub**
- Plataforma de versionamento de código onde o código-fonte do projeto é armazenado e gerido.
- O **GitHub Actions** é usado para automação do deploy, permitindo que o código seja automaticamente construído, testado e enviado para a AWS a cada atualização no repositório.

### **Terraform**
- Ferramenta de **Infrastructure as Code (IaC)** que permite provisionamento e gerenciamento da infraestrutura de forma automatizada e versionada.
- Com arquivos `.tf`, o Terraform cria, modifica e destrói recursos na AWS conforme configurado.

### **Amazon ECR** (Elastic Container Registry)
- Serviço de registro de contêineres Docker usado para armazenar as imagens Docker do **Frontend (React)** e **Backend (Node.js, APIs, Nginx)**.
- Facilita a integração com o **Amazon EKS** e outras ferramentas da AWS, simplificando o processo de implantação de contêineres.

### **Amazon EKS** (Elastic Kubernetes Service)
- Serviço gerenciado de Kubernetes que simplifica a criação e gerenciamento de clusters Kubernetes.
- Distribui os recursos em múltiplas zonas de disponibilidade, oferecendo alta disponibilidade e escalabilidade.

#### **Zonas de Disponibilidade**
- 🔹 **Zona 1** → **Ambiente de Desenvolvimento (Dev)** e **Qualidade (QA)**.
- 🔹 **Zona 2** → **Ambiente de Produção (Prod)**.
- 🔹 **Zona 3** → **Ambiente de Produção (Failover)**.

---

## 🔹 **Componentes da Infraestrutura**

### 🔸 **Rede e Distribuição**

#### **Subnets Públicas**
- Contém os pods do **React (Frontend)** em cada zona de disponibilidade.
- Permite que o tráfego de entrada seja acessado diretamente pela internet.
- Cada zona tem uma instância do frontend para garantir a disponibilidade.

#### **Subnets Privadas**
- Usadas para hospedar o **Backend (Node.js, APIs e Nginx)**.
- O backend é isolado da internet, acessível apenas internamente dentro da infraestrutura do Kubernetes.

### 🔸 **Arquitetura dos Pods**

#### **Backend (Distribuído por Zona de Disponibilidade)**

- **1 Node com 3 Pods:**
  - 📌 **2 Pods** → Contêm as APIs do Backend, com balanceamento de carga interno para garantir alta disponibilidade.
  - 📌 **1 Pod** → Contém o **Nginx**, atuando como proxy reverso para distribuir o tráfego entre os pods do backend.

- **1 Pod para Prometheus** → Monitoramento da performance dos pods, coletando métricas para observabilidade.
- **1 Pod para Grafana** → Painel de visualização das métricas coletadas pelo Prometheus, permitindo visualização em tempo real dos dados de performance e saúde da aplicação.

---

### 🔸 **Serviços de Alta Disponibilidade**

- **EKS Control Plane** → Gerencia o cluster Kubernetes, garantindo eficiência na comunicação entre nós e pods, alocando recursos conforme necessário.
- **HPA (Horizontal Pod Autoscaler)** → Escalonamento automático dos pods do backend e frontend com base na carga, garantindo que a infraestrutura cresça ou diminua conforme a demanda.
- **AWS Backup** → Automatiza a criação de backups dos dados em serviços como o RDS, garantindo recuperação em caso de falhas ou desastres.
- **Amazon RDS** → Banco de dados relacional gerenciado, com instâncias distribuídas em cada zona de disponibilidade para redundância e failover automático.

---

### 🔸 **Balanceamento de Carga e Segurança**

- **Amazon Load Balancer** → Distribui o tráfego entre os pods do Kubernetes, garantindo que a carga seja balanceada e evitando sobrecarga de um único pod.
- **CloudFront** → Serviço de **CDN (Content Delivery Network)** para entrega de conteúdo com baixa latência, acelerando a entrega de ativos estáticos como imagens, scripts e estilos do frontend.
- **AWS WAF** → **Web Application Firewall**, protege a aplicação contra ataques de segurança comuns, como SQL injection, Cross-site Scripting (XSS), entre outros. Configurado para proteger o Load Balancer e as aplicações web.
- **AWS Route 53** → Gerenciamento de DNS, com alta disponibilidade. Também gerencia o failover entre zonas de disponibilidade.

---

### 🔸 **Monitoramento e Observabilidade**

- **Amazon CloudWatch** → Coleta logs e métricas de performance de todos os recursos da AWS, incluindo **EKS**, **RDS**, **Load Balancer**, entre outros. Permite visibilidade em tempo real sobre o estado da infraestrutura e das aplicações.
- **Amazon SNS** → **Simple Notification Service**, envia alertas e eventos críticos para os administradores em tempo real, como falhas em recursos ou eventos de autoscaling.
- **Secrets Manager** → Armazena e gerencia segredos (como credenciais de banco de dados, chaves de API e dados sensíveis), garantindo que essas informações sejam seguras e acessíveis apenas aos recursos autorizados.


---

### **Quais as ferramentas vão ser utilizadas?**

A migração será realizada com os seguintes serviços AWS:

| **Serviço**                | **Função**                                                                                  |
|----------------------------|---------------------------------------------------------------------------------------------|
| **Terraform**               | Provisiona e gerencia a infraestrutura como código, criando e configurando os recursos na AWS. |
| **GitHub Actions**         | Automatiza o processo de CI/CD, integrando o GitHub para deploy contínuo na AWS.            |
| **Amazon ECR**              | Armazena e gerencia imagens Docker do backend e frontend.                                   |
| **Amazon EKS**              | Orquestra os containers no Kubernetes, proporcionando escalabilidade e alta disponibilidade. |
| **Helm**                    | Facilita a instalação e gerenciamento de recursos no Kubernetes, como Prometheus e Grafana. |
| **Prometheus**              | Monitora e coleta métricas de performance dos pods e recursos no Kubernetes.                |
| **Grafana**                 | Exibe métricas coletadas pelo Prometheus em dashboards visuais para facilitar o monitoramento. |
| **AWS RDS**                 | Gerencia bancos de dados relacionais com alta disponibilidade e backup automático.         |
| **AWS WAF**                 | Protege a aplicação contra ataques web, bloqueando tráfego malicioso.                      |
| **Amazon CloudFront**       | Distribui conteúdo estático com baixa latência, melhorando a performance do front-end.      |
| **AWS Route 53**            | Gerencia DNS, facilitando a troca de servidores e garantindo alta disponibilidade.          |
| **Amazon Load Balancer**    | Distribui o tráfego entre os pods, garantindo balanceamento de carga e escalabilidade.      |
| **AWS SNS**                 | Envia notificações automáticas sobre eventos críticos ou alertas no sistema.               |
| **AWS Secrets Manager**     | Armazena segredos e credenciais de forma segura, evitando exposição de informações sensíveis. |

### **Qual o diagrama da infraestrutura na AWS?**

![Diagrama pós migração](./img/2diagrama.png)

### **Como serão garantidos os requisitos de Segurança?**

Os requisitos de segurança serão garantidos com a implementação de várias práticas e ferramentas:

- **AWS WAF** (Web Application Firewall) protegerá a aplicação contra ataques web, como SQL injection e XSS, bloqueando tráfego malicioso.
- **AWS Secrets Manager** será utilizado para armazenar e gerenciar segredos e credenciais de forma segura, evitando a exposição de informações sensíveis.
- **IAM (Identity and Access Management)** controlará as permissões de acesso aos recursos da AWS, garantindo que apenas usuários autorizados possam interagir com a infraestrutura.
- A **encriptação de dados** será aplicada automaticamente nos serviços da AWS, como S3 e RDS, garantindo a proteção de dados.
- O **monitoramento com Amazon CloudWatch** será utilizado para gerar alertas de segurança e para fornecer visibilidade e controle sobre os recursos da infraestrutura.
- **EKS Security Groups** garantirá que apenas tráfego autorizado seja permitido dentro do cluster Kubernetes, através de regras de firewall configuradas. Os grupos de segurança serão utilizados para garantir a comunicação segura entre o frontend e o backend, dado que o frontend está na subnet pública e o backend na subnet privada.

#### **Segurança no EKS**

Os grupos de segurança são utilizados para controlar o tráfego de rede dentro do cluster EKS:

- **Control Plane Security Group**: Controla o tráfego entre o plano de controle do EKS e os nós de trabalho.
- **Node Security Group**: Define as regras de tráfego para os nós de trabalho. Inclui controle de acesso para SSH, comunicação entre os nós e o plano de controle, e acesso aos serviços internos e externos.
- **Pod Security Group**: Associa grupos de segurança diretamente aos pods utilizando a funcionalidade AWS Security Groups for Pods, permitindo regras de tráfego específicas para pods individuais.

## Como será realizado o processo de Backup?

#### 1. 🔸 **AWS RDS Backup Automático**
- O **AWS RDS Backup Automático** vai fazer backups regulares do banco de dados **RDS** e podemos escolher por quanto tempo queremos guardar esses backups.
- Ele também vai permitir que a gente recupere o banco em um ponto específico no tempo, caso precise voltar a um estado anterior.

#### 2. 🔸 **Automação com CronJobs**
- Vamos usar **CronJobs** para fazer backups automáticos no **EKS** (Elastic Kubernetes Service).
- Isso vai garantir que os backups sejam feitos de forma contínua, sem precisar que alguém faça manualmente.

#### 3. 🔸 **EKS**
- No **EKS**, vamos usar o versionamento dos arquivos para registrar todas as mudanças feitas no cluster. O recurso de *rollout* vai aplicar as mudanças aos poucos, e se algo der errado, podemos voltar a uma versão anterior dos pods para restaurar os dados de forma segura.

#### 4. 🔸 **ECR**
- Vamos organizar os arquivos do **ECR** no **GitHub**. Um script vai ser criado para exportar esses arquivos de forma automática, garantindo que as imagens do **ECR** estejam sempre atualizadas e prontas para serem recuperadas caso seja necessário.



---

## **Qual o custo da infraestrutura na AWS (AWS Calculator)?**
![Diagrama pós migração](./img/custos.png)

![Diagrama pós migração](./img/1custos.png)

![Diagrama pós migração](./img/2custos.png)

---

## Conclusão
A migração para a AWS e a modernização com Kubernetes, utilizando o Amazon EKS, foram passos importantes no processo de aprendizagem e crescimento da Fast Engineering S/A. A mudança para a nuvem trouxe vantagens como maior escalabilidade, flexibilidade e segurança, permitindo que a empresa fosse capaz de lidar melhor com o aumento da demanda por acessos e compras. 🚀

O processo de lift-and-shift, que consistiu na migração direta para a nuvem sem grandes mudanças no sistema original, foi uma maneira eficiente de começar a transição para a AWS. Isso permitiu à empresa tirar proveito da nuvem de forma rápida e sem grandes riscos, o que me ajudou a entender a importância de uma migração bem planejada.

A implementação do Kubernetes no Amazon EKS foi um aprendizado crucial. O Kubernetes ajudou a otimizar o gerenciamento de contêineres e garantir que a infraestrutura fosse mais ágil e escalável, permitindo que a empresa crescesse de maneira mais tranquila no futuro. Além disso, entender as práticas de DevOps, como a criação de pipelines de CI/CD, me mostrou como automatizar processos e melhorar a eficiência nas entregas de software.

Com essa experiência, aprendi a importância de aplicar boas práticas de segurança, usar ferramentas como Docker e AWS, e garantir que a infraestrutura seja preparada para suportar crescimento e mudanças. Esse projeto não só me proporcionou uma visão mais ampla sobre infraestrutura em nuvem, mas também me ensinou como as empresas podem se beneficiar de uma arquitetura moderna e escalável. 🌐

