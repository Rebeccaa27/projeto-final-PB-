


<h1 style="text-align: center;">Migração e Modernização da Infraestrutura para AWS</h1>



<div style="text-align: center;">
  <img src="./img/projeto%20final.webp" alt="Minha Imagem" style="max-width: 50%; height: 50%;">
</div>




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

## Fases do Projeto

O projeto será realizado em duas etapas principais:

### Etapa 1: Lift-and-Shift
Migração inicial da infraestrutura para a AWS, sem mudanças significativas, focada em melhorar a performance e escalabilidade, mantendo a estrutura atual.

### Etapa 2: Modernização com Kubernetes
Reestruturação da infraestrutura para adoção de Kubernetes, facilitando escalabilidade, automação e gerenciamento de contêineres.

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

| Serviço | Função |
| --- | --- |
| AWS MGN | Replicação contínua dos servidores para a AWS. |
| AWS Replication Agent | Captura e transfere dados para o Replication Server. |
| AWS EBS | Armazena volumes persistentes durante e após a migração. |
| AWS DMS | Migração do banco de dados MySQL para Amazon RDS. |



## Qual o diagrama da infraestrutura na AWS?

![Diagrama do contexto atual](./img/diagrama.m.png)

## Como serão garantidos os requisitos de Segurança?

1️⃣ **Controle de Acesso e Autenticação**  
- AWS IAM: Uso de permissões mínimas necessárias (principle of least privilege).

2️⃣ **Segurança na Replicação e Migração**  
- AWS Replication Agent: Transmissão segura via canais criptografados.
- AWS DMS: Migração com criptografia ativada.

3️⃣ **Configuração de Portas Seguras**

| Porta | Uso |
| --- | --- |
| 443 | Comunicação do AWS MGN com servidores locais. |
| 1500 | Comunicação entre servidores locais e AWS. |
| 3306 | Acesso ao banco MySQL (Amazon RDS). |

4️⃣ **Segurança na Infraestrutura**  
- VPC Security Groups e Network ACLs para controle de tráfego e limitação de acessos indevidos.

## Como será realizado o processo de Backup?


1. **Backup de Banco de Dados (Amazon RDS):**
   - O **RDS** fará **backups automáticos** do banco de dados, sem necessidade de intervenção manual.
   - Os dados serão salvos regularmente e poderão ser **restaurados** para um ponto específico, caso ocorra alguma falha.
   - A retenção dos backups pode ser configurada para garantir a segurança dos dados por um tempo definido.

2. **Backup de Armazenamento (Amazon EBS):**
   - O **EBS** realizará **snapshots periódicos** dos volumes de dados.
   - Esses backups ajudam na recuperação rápida de dados caso algo dê errado com as instâncias ou dados corrompidos.


## Qual o custo da infraestrutura na AWS (AWS Calculator)?


---

### **Etapa 2: Modernização com Kubernetes**

#### **Quais atividades são necessárias para a migração?**

#### **Quais as ferramentas vão ser utilizadas?**

#### **Qual o diagrama da infraestrutura na AWS?**

#### **Como serão garantidos os requisitos de Segurança?**

#### **Como será realizado o processo de Backup?**


#### **Qual o custo da infraestrutura na AWS (AWS Calculator)?**

---

### **Conclusão**
A migração para a AWS e a modernização com Kubernetes trarão maior escalabilidade, flexibilidade e segurança para a **Fast Engineering S/A**. A implementação de uma infraestrutura moderna na nuvem permitirá que a empresa atenda à crescente demanda de acessos e compras de forma eficiente e segura. O uso de práticas de DevOps com pipelines de CI/CD, contêineres, e Kubernetes garantirá um ambiente ágil e escalável, pronto para suportar o crescimento do eCommerce no futuro.


