# Conceitos - AWS CloudFormation ✨
Esse serviço permite que gerenciemos vários recursos da AWS como uma **unidade**.  
Cada um desses conjuntos é chamado de *stack*.

## 📝 Templates 
São arquivos em JSON ou YAML que descrevem a estrutura da nossa infraestrutura na AWS. Eles descrevem todos os recursos que desejamos gerenciar na nossa *stack*, além de como esses recursos se relacionam entre si.  

O AWS CloudFormation conta com um recurso chamado *Infrastructure Composer*, que permite criar *templates* na base do arrasta e solta, gerando o código JSON/YAML automaticamente. ✨

Os *templates* são compostos por várias seções, aqui estão algumas:  

| Seção | Objetivo | Exemplo |
| ------------- | ------------- | ------------- |
| `Resources`  | Especifica cada um dos recursos da *stack*  | Cria uma instância EC2 e define a chave SSH |
| `Parameters`  | Recebe valores personalizados para serem usados | Recebe o tipo de ambiente (teste ou produção) |
| `Outputs` | Retorna valores úteis para serem aproveitados | Retorna o IP público da instância EC2 para possibilitar a conexão |
| `Mappings` | Cria pares chave-valor para definir valores condicionais | Se o ambiente for teste, cria uma instância de classe mais barata. Se for produção, usa uma classe mais cara
| `Conditions` | Define se um recurso deve ou não ser criado, a depender de uma condição | Cria um *Elastic IP* só se estiver em ambiente de produção

⚠️ **Atenção:** Somente a seção `Resources` é obrigatória, porque ela cria e define os recursos utilizados. As demais, são opcionais.

## ⚙️ Stacks
A *stack*, nada mais é do que nosso *template* convertido em um conjunto funcional dos nossos recursos.  
Ao criá-la, podemos:
- Usar um *template* já existente (indicando a URL, carregando um arquivo ou sincronizando do Git)
- Construir do zero usando o *Infrastructure Composer*

Também é possível agrupar *stacks* em conjuntos chamados ***StackSets***, dessa forma, podemos criar, atualizar e excluir várias *stacks* ao mesmo tempo, sem precisar fazer alterações individuais.

## ❗Cotas e Limites
Nossas contas AWS tem algumas limitações do CloudFormation. É importante conhecê-las para evitar falhas nas *stacks*:  

### Cotas de Templates 📝
- **Tamanho do Arquivo:** 51KB se carregado diretamente, 1MB se armazenado em um *bucket* S3
- **Parâmetros e Outputs:** 200 de cada por *template*
- **Recursos:** 500 por *template*

### Cotas de Stacks ⚙️
- **Quantidade por Conta:** 2.000 *stacks* por conta AWS
- **Tamanho do Nome:** 128 caracteres por *stack*
- **StackSets:** 1.000 conjuntos por conta AWS
