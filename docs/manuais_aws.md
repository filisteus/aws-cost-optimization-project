Manuais de Uso dos Serviços AWS
Este documento contém instruções detalhadas sobre o uso dos serviços AWS implementados no projeto de otimização de custos da Abstergo Industries. Os serviços abordados incluem EC2, S3 e Lambda.

1. AWS EC2 (Elastic Compute Cloud)
Descrição:
O Amazon EC2 fornece capacidade computacional escalável na nuvem. Neste projeto, usamos EC2 para substituir servidores físicos, utilizando instâncias sob demanda e spot instances para otimizar os custos.

Instruções de Uso:
1.1. Criar uma Instância EC2:
Acesse o Console AWS EC2.

Clique em Launch Instance.

Selecione a AMI (Amazon Machine Image) que deseja usar (ex: Amazon Linux 2).

Escolha o tipo de instância. Exemplo: t2.micro (elegível ao nível gratuito).

Configure a instância:

Configure o número de instâncias e escolha opções como VPC e sub-rede.
Configure o armazenamento (disco EBS).
Configure tags (opcional).
Configure o Security Group:

Defina regras de entrada, como SSH (porta 22) para acessar via SSH.
Revise e clique em Launch.

Escolha ou crie um par de chaves (Key Pair) para acesso SSH.

Acesse a instância via terminal:

bash
Copiar código
ssh -i "seu-arquivo-chave.pem" ec2-user@seu-endereco-publico-ec2
1.2. Spot Instances:
Para reduzir ainda mais os custos, é possível usar Spot Instances:

No EC2 Dashboard, clique em Spot Requests.
Clique em Request Spot Instances.
Siga os mesmos passos para escolher a AMI e o tipo de instância.
Defina o Maximum Price (preço máximo que você deseja pagar).
Revise e lance a instância.
1.3. Terminar uma Instância EC2:
Para parar ou terminar uma instância:

No console EC2, selecione a instância.
Clique em Actions > Instance State > Terminate ou Stop.
2. AWS S3 (Simple Storage Service)
Descrição:
O Amazon S3 fornece armazenamento escalável e acessível. Neste projeto, usamos o S3 para armazenar dados e backups, com arquivamento de dados antigos no S3 Glacier para redução de custos.

Instruções de Uso:
2.1. Criar um Bucket S3:
Acesse o Console AWS S3.
Clique em Create Bucket.
Escolha o nome do bucket (ex: meu-bucket-backups).
Selecione a região onde o bucket será criado.
Configure permissões e regras de acesso (por exemplo, quem pode ler/gravar no bucket).
Revise e clique em Create Bucket.
2.2. Upload de Arquivos para o S3:
No console do S3, selecione o bucket criado.
Clique em Upload.
Adicione os arquivos que deseja armazenar.
Configure permissões de acesso se necessário.
Clique em Upload.
2.3. Configurar Regras de Arquivamento (Glacier):
No bucket S3, vá até a aba Management.
Clique em Create Lifecycle Rule.
Nomeie a regra (ex: "Mover para Glacier").
Defina quando os arquivos devem ser movidos para Glacier (por exemplo, após 30 dias).
Revise e salve a regra.
2.4. Acessar Arquivos:
Para acessar arquivos, use o console S3 ou o AWS CLI:
bash
Copiar código
aws s3 cp s3://meu-bucket-backups/arquivo.txt ./local-arquivo.txt
3. AWS Lambda
Descrição:
O AWS Lambda permite executar código sem gerenciar servidores. Neste projeto, usamos Lambda para automatizar tarefas de manutenção e monitoramento.

Instruções de Uso:
3.1. Criar uma Função Lambda:
Acesse o Console AWS Lambda.
Clique em Create Function.
Selecione Author from scratch.
Nomeie a função (ex: ProcessarBackups).
Escolha o runtime (por exemplo, Python 3.8).
Defina ou crie uma role de execução com permissões necessárias (como acesso ao S3).
Clique em Create Function.
3.2. Escrever o Código da Função:
No editor da função, adicione seu código. Exemplo de função Lambda em Python para processar dados no S3:
python
Copiar código
import json
import boto3

def lambda_handler(event, context):
    s3 = boto3.client('s3')
    bucket = 'meu-bucket-backups'
    objeto = 'dados.txt'
    
    resposta = s3.get_object(Bucket=bucket, Key=objeto)
    conteudo = resposta['Body'].read().decode('utf-8')
    
    # Processar os dados (simples exemplo)
    print("Conteúdo do arquivo:", conteudo)
    
    return {
        'statusCode': 200,
        'body': json.dumps('Processamento concluído!')
    }
Clique em Deploy para salvar e publicar as alterações.
3.3. Configurar um Trigger:
No console Lambda, vá até a aba Triggers.
Clique em Add Trigger.
Escolha o serviço que ativará a função (ex: S3 para processar uploads de arquivos).
Configure os parâmetros e salve.
3.4. Testar a Função Lambda:
No console Lambda, clique em Test.
Crie um evento de teste (ex: um upload de arquivo no S3).
Clique em Test novamente para verificar a saída da função

Conclusão
Esses manuais cobrem as operações básicas para gerenciar instâncias EC2, armazenamento S3 e funções Lambda na AWS. Cada serviço pode ser configurado e expandido conforme as necessidades específicas da Abstergo Industries.

