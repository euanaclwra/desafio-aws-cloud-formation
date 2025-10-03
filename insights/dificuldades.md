# Dificuldades, Dúvidas e Obstáculos - AWS CloudFormation ✨
Neste arquivo, veremos algumas dificuldades comuns que os usuários do CloudFormation costumam encontrar, e também algumas dúvidas pessoas com as quais me deparei durante os estudos.

## 😬 Obstáculos Comuns dos Usuários
#### Devo usar JSON ou YAML nos meus *templates*?
***Resposta:*** Pense na legibilidade e automatização 🧩  

O **YAML** é mais legível e suporta comentários, então a manutenção humana acaba sendo mais fácil. Num geral, é altamente recomendado!  
O **JSON**, apesar de ter uma manutenção mais chata, costuma ser melhor para trabalhar com automatizações via API, visto que elas geralmente recebem entradas JSON. 

#### Como devo nomear os meus recursos?
***Resposta:*** Use *CamelCase* e nomes descritivos 🔠  

No momento da manutenção do *template*, você ou as pessoas da sua equipe precisam ler o ID do recurso e saber exatamente do que se trata:
- **Exemplo Genérico ❌:** `Instance1`
- **Exemplo Descritivo ✅:** `WebServerEC2Instance`

## ❓Dúvidas Pessoais

#### Qual o perigo de liberar permissões excessivas a um recurso?
***Resposta:*** Criamos vulnerabilidades na nossa arquitetura 🔓  

Pense, por exemplo, em um desenvolvedor alterando uma instância EC2 de teste.  

Se, ao invés de liberarmos permissão para encerrar **somente essa** instância, liberarmos o encerramento de **qualquer** instância na conta, um script de automação
mal configurado poderia excluir servidores em produção de maneira irreversível.  

Pior ainda, se um invasor conseguisse acesso à essa instância de teste (supostamente inofensiva), poderia usar essa permissão excessiva para realizar um ataque *DDoS*.

#### Como é possível o StackSets gerenciar *stacks* de várias contas AWS? Isso não é perigoso?
***Resposta:*** Políticas de confiança explícita ✅  

O StackSets do CloudFormation exige que cada conta destino pré-configure uma *policy* para a conta administradora.  
É, basicamente, um: "Eu confio na Conta Administradora X para assumir a Role Y e criar recursos aqui."

Dessa forma, nada acontece nas contas gerenciadas sem que seus próprios usuários tenham delegado as devidas permissões. 
