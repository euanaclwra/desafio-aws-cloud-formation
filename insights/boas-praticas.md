# Boas Práticas - AWS CloudFormation ✨
A AWS recomenda algumas práticas para otimizar nossa infraestrutura do CloudFormation:

## 💻 Princípios da IaC
A *IaC (Infrastructure as Code)* é a prática de gerenciar a infraestrutura de um sistema usando código, ao invés de processos manuais. Esse é exatamente o objetivo do CloudFormation.  

Por essa razão, é essencial que tratemos os *templates* como **código**, de fato: reutilizáveis, versionáveis e flexíveis.

### 🔄 Reutilização com Parâmetros
Valores como o nome do ambiente ou o tipo da instância EC2 **não** devem ser definidos diretamente no *template*, e sim informados como valores de entrada na seção `Parameters`.  

Isso garante que o mesmo *template* possa ser usado para criar ambientes de Desenvolvimento, Teste e Produção. Além de também possibilitar, por exemplo, a reutilização em outras filiais da empresa. ✅

### 🚩 Versionamento
É sempre bom armazenar nossos *templates* em sistemas de versionamento, como o próprio GitHub. Isso permite que você rastreie todas as alterações, e reverta a infraestrutura para uma versão anterior estável em caso de falhas. ✅  

## 🔒 Princípio do Menor Privilégio
Sendo de extrema importância quando falamos de segurança na nuvem, esse princípio implica que cada usuário e recurso só deve ter as **permissões mínimas necessárias** para cumprir seu papel.  

Por exemplo, se uma *AWS Lambda Function* só precisa ler um dado de um bucket s3, não conceda permissão de gravação para esse recurso. Isso minimiza muito as chances de erros humanos e de ataques externos. ✅  

## 📦 Stacks Aninhadas
Para arquiteturas grandes ou complexas, o ideal é dividir o projeto em vários arquivos menores.  

Podemos usar, por exemplo, um *template* para a rede (VPC), outro para o banco de dados (RDS) e outro para a camada de aplicação (EC2). 
Na *stack* principal, basta referenciar essas *stacks* secundárias.  

Dessa forma, garantimos a independência de cada camada da arquitetura, além de evitar alcançar a cota máxima de 500 recursos por *stack*. ✅
