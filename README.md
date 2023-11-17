
# Descrição das atividades solicitadas.

Uma documetação sobre a sprint 5.


# Instalar uma VM com OL8, instalar o ANSIBLE e criar um YAML de ping para o IP do seu desktop

## 1. Crie um Inventario (Inventory)
 
 Crie um arquivo YAML para o inventário (inventory.yml). Este arquivo especifica os hosts que serão gerenciados pelo Ansible.

```bash
  # inventory.yml
all:
  hosts:
    desktop:
      ansible_host: SEU_IP_AQUI

```
Substitua SEU_IP_AQUI pelo endereço IP real do seu desktop.
    
## 2. Crie um Playbook YAML

Crie um playbook YAML (ping.yml) para executar o ping no seu desktop usando o módulo ping do Ansible.

```bash
  # ping.yml
---
- name: Executar ping no desktop
  hosts: desktop
  gather_facts: false  # Desativa a coleta de informações sobre o host

  tasks:
    - name: Ping para o desktop
      ping:

```
## 3. Configure suas chaves ssh.
 
Certifique-se de que cada máquina tenha uma chave ssh configurada, usando o comando ssh-keygen.

```bash
ssh-keygen
```
Passe sua chave pública para a máquina, usando o comando ssh-copy-id.

```bash
ssh-copy-id -i <location of id_rsa.pub> <ip-address of host>

```
Substitua o <location of id_rsa.pub> pela caminho do arquivo onde está salvo o .pub e substitua o <ip-address of host> pelo endereço do seu host.

Exemplo:

```bash
ssh-copy-id -i /root/.ssh/id_rsa.pub 192.168.0.106
```

## 4. Execute o Playbook
 
Abra um terminal e navegue até o diretório onde os arquivos inventory.yml e ping.yml estão localizados. Execute o seguinte comando para executar o playbook:

```bash
ansible-playbook -i inventory.yml ping.yml

```

# Instalar o terraform no seu desktop e criar o deploy de uma instancia EC t2.micro na AWS.

## 1. Preparativos Iniciais

Antes de começar, certifique-se de ter:

Acesso a uma conta da AWS com as credenciais adequadas.
Seu desktop com um sistema operacional compatível (por exemplo, Windows, macOS, Linux).
 
Abra um terminal e navegue até o diretório onde os arquivos inventory.yml e ping.yml estão localizados. Execute o seguinte comando para executar o playbook:

## 2. Instalação do Terraform no Seu Desktop

2.1. Faça o Download do Terraform
Acesse o site oficial do Terraform e baixe a versão mais recente para o seu sistema operacional.

2.2. Extraia o Arquivo
Extraia o arquivo baixado para um diretório de sua escolha.

2.3. Configure o PATH
Adicione o diretório que contém o executável do Terraform ao seu PATH. Isso pode ser feito editando o arquivo de perfil do seu sistema operacional ou configurando variáveis de ambiente.

##  3. Configuração das Credenciais da AWS

3.1. Configure as Credenciais da AWS
Certifique-se de ter as credenciais da AWS configuradas. Você pode fazer isso configurando o AWS CLI:

```bash
aws configure

```


Precisamos fornecer algumas informações para o console como nosso Acess Key ID, Acess Key, região e formato de saida dos logs
Após fazer seu login, crie um diretorio para executar nosso projeto. crie uma pasta com o nome de sua preferencia na area de trabalho.
Dentro desse diretorio criei um arquivo chamado "main.tf" esse arquivo será o responsável por executar nossos codigos para criação da ec2

## 5. Configuração do Projeto Terraform

Crie o arquivo main.tf e adicione o seguinte código para configurar uma instância EC2.

Abra um terminal e navegue até o diretório onde os arquivos inventory.yml e ping.yml estão localizados. Execute o seguinte comando para executar o playbook:

```bash
provider "aws" {
  region = "us-east-1" # substitua pela sua região desejada
}

resource "aws_instance" "minha_instancia" {
  ami           = "ami-xxxxxxxxxxxxxxxxx" # substitua pela AMI desejada
  instance_type = "t2.micro"
}


```

## 6. Inicialização e Aplicação
 
6.1. Navegue até a pasta criada.
Abra um terminal e navegue até o diretório do seu projeto Terraform.

6.2. Inicialize o Diretório Terraform

```bash
terraform init


```

```bash
terraform plan


```
```bash
terraform apply

```