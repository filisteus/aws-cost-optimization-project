# Projeto de Implementação de Serviços AWS para Otimização de Custos

Este repositório contém o projeto de implementação de serviços AWS na **Abstergo Industries**, com o objetivo de reduzir custos operacionais e melhorar a eficiência da infraestrutura.

## Objetivo
O projeto foi focado na implementação de três serviços AWS para otimizar a infraestrutura de TI e reduzir custos imediatamente.

## Serviços Implementados

### 1. AWS EC2 (Elastic Compute Cloud)
- **Foco**: Otimização e redução de custos de infraestrutura.
- **Caso de uso**: Migração de servidores físicos para instâncias EC2, utilizando instâncias sob demanda e spot instances para economizar nos custos de operação.

### 2. AWS S3 (Simple Storage Service)
- **Foco**: Armazenamento eficiente e escalável.
- **Caso de uso**: Armazenamento de arquivos e backups em S3 com políticas de arquivamento (Glacier) para reduzir custos de armazenamento.

### 3. AWS Lambda
- **Foco**: Execução de código sem necessidade de servidores.
- **Caso de uso**: Automação de processos de manutenção e monitoramento através de funções Lambda, eliminando a necessidade de servidores dedicados.

## Resultados
- **Redução de custos**: A implementação trouxe economia significativa em hardware e manutenção, com melhorias na eficiência.
- **Escalabilidade**: A utilização de S3 e EC2 permite escalar recursos conforme a demanda, sem custos adicionais fixos.

## Como Replicar a Implementação

### Pré-requisitos
- Conta na AWS.
- Permissões para criar instâncias EC2, buckets S3 e funções Lambda.
- AWS CLI configurada.

### Passo a Passo
1. **EC2**: Crie instâncias EC2 com as configurações de uso sob demanda ou spot instances.
   - Exemplo de comando AWS CLI:
     ```bash
     aws ec2 run-instances --image-id ami-0abcd1234 --count 1 --instance-type t2.micro --key-name my-key-pair
     ```

2. **S3**: Crie um bucket S3 e configure uma política de arquivamento para dados menos acessados.
   - Exemplo de comando AWS CLI:
     ```bash
     aws s3api create-bucket --bucket meu-bucket --region us-east-1
     ```

3. **Lambda**: Implemente funções Lambda para automatização de processos.
   - Exemplo de criação de função Lambda:
     ```bash
     aws lambda create-function --function-name MyLambdaFunction --runtime python3.8 --role arn:aws:iam::123456789012:role/lambda-execution-role --handler lambda_function.lambda_handler --zip-file fileb://function.zip
     ```

## Conclusão
A implementação destes serviços AWS trouxe uma redução imediata nos custos de operação da **Abstergo Industries** e melhorou a eficiência e flexibilidade da infraestrutura de TI.

## Anexos
- [Relatório completo de custos antes e depois da implementação](docs/relatorio_custos.md)
- [Manuais de uso das ferramentas](docs/manuais_aws.md)

Assinatura do Responsável pelo Projeto:

Paulo Evaristo Ferreira da Silva / pevaristo@msn.com
