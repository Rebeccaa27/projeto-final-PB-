


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



**O objetivo deste projeto é migrar a infraestrutura de TI da empresa **Fast Engineering S/A** para a AWS, com foco em modernização e escalabilidade, atendendo à alta demanda de acessos e compras no eCommerce. O projeto será realizado em duas etapas:**



- **Etapa 1: Lift-and-Shift**: Migração inicial da infraestrutura para a AWS, sem mudanças significativas, com o intuito de melhorar a performance e escalabilidade, mantendo a estrutura atual.
  
- **Etapa 2: Modernização com Kubernetes**: Modernização da infraestrutura, utilizando Kubernetes para gerenciar os contêineres e facilitar a escalabilidade e automação.

---

### **Etapa 1: Lift-and-Shift**

### Quais atividades são necessárias para a migração? 

1. **Planejamento e Avaliação**
   - **Análise do ambiente atual:** Avaliar as instâncias de servidores (frontend, backend), banco de dados e dependências no ambiente local.
   - **Escolha da abordagem de migração:** Decidir se a migração será feita com a abordagem "Lift-and-Shift", replatforming, ou redesign.
   - **Identificação dos requisitos de segurança e conformidade:** Avaliar as políticas de segurança, normas e regulamentações que devem ser atendidas.
   - **Planejamento de backup:** Garantir que todos os dados críticos sejam respaldados antes da migração.

2. **Preparação do Ambiente AWS**
   - **Configuração de VPC (Virtual Private Cloud):** Criar a rede privada para hospedar as instâncias EC2 e outros recursos.
   - **Configuração de subnets:** Definir subnets públicas e privadas dentro da VPC, dependendo dos requisitos de rede e segurança.
     - **Subnets públicas:** Para instâncias EC2 que precisam de acesso à internet (frontend).
     - **Subnets privadas:** Para instâncias EC2 e banco de dados RDS que não devem ter acesso direto à internet (backend, banco de dados).
   - **Configuração de rotas e gateways:** Configurar tabelas de rotas, Internet Gateway e/ou NAT Gateway, dependendo do acesso necessário para suas instâncias.
   - **Criação de instâncias EC2:** Provisionar instâncias EC2 nas subnets públicas ou privadas, conforme necessário, para os servidores de frontend, backend e instâncias de replicação.
   - **Configuração de Amazon RDS:** Criar e configurar o banco de dados RDS para hospedar o banco de dados migrado, associando-o a uma subnet privada.

3. **Configuração das Ferramentas de Migração**
   - **Instalação do AWS MGN (Application Migration Service):** Configurar o MGN para replicação contínua dos servidores de origem para as instâncias EC2.
   - **Instalação do AWS Replication Agent:** Instalar o Replication Agent nas máquinas de origem para capturar e transferir dados para a AWS.
   - **Configuração do AWS DMS (Database Migration Service):** Configurar o DMS para migrar o banco de dados de origem (por exemplo, MySQL) para o Amazon RDS.

4. **Execução da Migração**
   - **Replicação de dados com AWS MGN e Replication Agent:** Iniciar o processo de replicação contínua dos dados dos servidores de origem para a AWS.
   - **Migração de banco de dados com AWS DMS:** Migrar os dados do banco de dados MySQL para o RDS, garantindo a integridade dos dados.
   - **Sincronização de dados:** Continuar a replicação para garantir que a versão mais recente dos dados esteja disponível no ambiente da AWS.

5. **Testes Pós-Migração**
   - **Verificação de integridade:** Validar se todos os dados foram replicados corretamente e garantir que a integridade dos dados esteja intacta.
   - **Testes de desempenho:** Testar o desempenho das instâncias EC2 e do banco de dados RDS para garantir que atendem aos requisitos de carga.
   - **Testes de aplicação:** Verificar se as aplicações estão funcionando corretamente no novo ambiente.

6. **Finalização e Otimização**
   - **Desativação de recursos locais:** Desativar ou desligar servidores e bancos de dados no ambiente local após a confirmação de sucesso na migração.

### **Quais as ferramentas vão ser utilizadas?**  

A migração será realizada utilizando os seguintes serviços da AWS:  

- **AWS MGN (Application Migration Service):** Responsável pela replicação contínua dos servidores de origem para instâncias **EC2** na AWS, utilizando a abordagem **Lift-and-Shift**.  
- **AWS Replication Agent:** Agente instalado nos servidores de origem para capturar e transferir dados para o **Replication Server**, que processa e armazena temporariamente em volumes **EBS**.  
- **AWS EBS (Elastic Block Store):** Serviço de armazenamento utilizado para manter dados persistentes durante o processo de replicação e nas instâncias finais.  
- **AWS DMS (Database Migration Service):** Serviço utilizado para migrar o banco de dados **MySQL** para **Amazon RDS (MySQL)**, garantindo a integridade dos dados durante a transição.  


#### **Qual o diagrama da infraestrutura na AWS?**

![Diagrama do contexto atual](./img/diagrama1.png)

### **Como serão garantidos os requisitos de Segurança?**  

#### **1. Controle de Acesso e Autenticação**  
- **AWS IAM (Identity and Access Management):** Uso de políticas de permissões com o princípio de menor privilégio para restringir acessos desnecessários.   
  
#### **2. Segurança na Replicação e Migração**  
- **AWS Replication Agent:** Transmissão segura dos dados através de canais criptografados.  
- **AWS DMS:** Configuração de migração com criptografia ativada para proteger os dados do banco durante a transferência.  
- **Web Proxy Server:** Implementado para controlar e monitorar as conexões de saída, garantindo maior segurança e visibilidade do tráfego de rede.  

##### **3. Configuração de Portas**  
As seguintes portas foram configuradas para garantir a comunicação segura entre os serviços:  
- **Porta 443:** Comunicação do **AWS MGN** com a Web Proxy Server.  
- **Porta 1500:** Comunicação entre servidores locaos e as instâncias de réplica do **AWS MGN**.  
- **Porta 3306:** Acesso ao banco de dados local MySQL com o **(Amazon RDS)**.  

#### **4. Segurança na Infraestrutura** 
- **VPC Security Groups e Network ACLs:** Controle de tráfego de entrada e saída para limitar acessos não autorizados.  

### Como será realizado o processo de Backup?

- **AWS MGN:** Realiza a replicação contínua dos servidores, criando cópias exatas dos dados e permitindo reverter a migração, se necessário.
- **AWS Replication Agent:** Captura e transfere dados dos servidores de origem para volumes **EBS**, mantendo a integridade dos dados replicados.
- **AWS EBS:** Oferece armazenamento persistente, com a possibilidade de criar **snapshots** para backup e recuperação de dados.
- **AWS DMS:** Garante a migração segura do banco de dados **MySQL** para **Amazon RDS**, mantendo a consistência dos dados durante o processo.

Com essas ferramentas em conjunto, o processo de backup estará protegido durante toda a migração, garantindo que os dados estejam seguros e prontos para serem restaurados se necessário.

#### **Qual o custo da infraestrutura na AWS (AWS Calculator)?**
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


