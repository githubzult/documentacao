# Github

## Passo 1: Atualize o sistema

`sudo yum update -y`


## Passo 2: Instale o Git

`sudo yum install git -y`



## Passo 3: Baixe o instalador do Git Bash

Acesse o site oficial do Git Bash (https://gitforwindows.org/) e baixe o instalador adequado para o seu sistema operacional CentOS. Por padrão, o instalador será salvo na pasta Downloads.

## Passo 4: Abra o terminal e vá para a pasta Downloads

`cd Downloads`


## Passo 5: Instale o Git Bash

`sh Git-2.31.1-64-bit.exe`


## Passo 6: Conclua a instalação

Siga as instruções do instalador do Git Bash para


# Criação de Repositório no GitHub

## Passo 1: Acesse o GitHub

Acesse o site oficial do GitHub (https://github.com/) e faça login na sua conta.

## Passo 2: Crie um Novo Repositório

Clique no botão "New" (Novo) na página principal do GitHub. 

![New Repository button](https://user-images.githubusercontent.com/70767722/131229699-7e98d9cc-7321-4883-a12e-5760da8d17b7.png)

## Passo 3: Preencha as Informações do Repositório

Preencha as informações do repositório na página de criação do repositório, incluindo:

* Nome do repositório: Escolha um nome para o seu repositório. Certifique-se de que o nome seja descritivo e fácil de lembrar.
* Descrição: Escreva uma descrição breve do seu repositório.
* Tipo de repositório: Selecione o tipo de repositório que você deseja criar. Você pode optar por criar um repositório público ou privado. Selecione "Public" para tornar o repositório público e "Private" para torná-lo privado.
* Inicialização do repositório: Selecione "Initialize this repository with a README" para criar um arquivo README.md vazio para o seu repositório.

![Create a new repository page](https://user-images.githubusercontent.com/70767722/131229754-bfd0684e-fd8d-4d48-a735-1b7a44e2f0a2.png)

## Passo 4: Confirme a Criação do Repositório

Verifique se as informações do seu repositório estão corretas e clique em "Create Repository" (Criar repositório).

![Confirm repository creation](https://user-images.githubusercontent.com/70767722/131229819-3b87664a-9df0-4d7f-a8a5-5e5debcddbe1.png)

## Passo 5: Acesse o Repositório Criado

Após a criação do repositório, você será redirecionado para a página do seu repositório. Você também pode acessar o repositório a qualquer momento a partir da página principal do GitHub, clicando no nome do repositório.

![Repository page](https://user-images.githubusercontent.com/70767722/131229882-b3d6d17f-7aa8-4c03-9ab2-4d4e7f34216f.png)

## Conclusão

Agora você criou com sucesso um repositório no GitHub. O repositório está pronto para receber arquivos e ser utilizado para o versionamento de código fonte, colaboração e gerenciamento de projetos.



# Criação e Configuração de Chave SSH para Conta GitHub

## Passo 1: Gerando uma Chave SSH

1. Abra o terminal do seu servidor e digite o seguinte comando para gerar uma nova chave SSH:


`ssh-keygen -t ed25519 -C "seu_email@exemplo.com"`


2. Quando solicitado, pressione "Enter" para aceitar o local padrão de armazenamento da chave ou digite um caminho diferente.

3. Digite uma senha para proteger a chave SSH, se desejar.

4. A chave SSH foi gerada com sucesso. Você pode ver o conteúdo da chave digitando o seguinte comando:


`cat ~/.ssh/id_ed25519.pub`


5. Copie o conteúdo da chave SSH gerada.

## Passo 2: Adicionando a Chave SSH à sua Conta GitHub

1. Faça login na sua conta GitHub e acesse as configurações de SSH.

2. Clique em "SSH and GPG keys" (Chaves SSH e GPG).

3. Clique em "New SSH key" (Nova chave SSH).

4. Cole a chave SSH gerada na seção "Key".

5. Digite um título para a chave SSH na seção "Title".

6. Clique em "Add SSH key" (Adicionar chave SSH).

7. A chave SSH foi adicionada à sua conta GitHub com sucesso.

## Passo 3: Testando a Chave SSH

1. Abra o terminal do seu servidor e digite o seguinte comando:

`ssh -T git@github.com`


2. Se você vir uma mensagem de confirmação, como "Hi {seu_nome_de_usuario}! You've successfully authenticated, but GitHub does not provide shell access" (Olá {seu_nome_de_usuario}! Você autenticou com sucesso, mas o GitHub não fornece acesso ao shell), significa que a chave SSH foi configurada com sucesso.

3. Agora você pode usar a chave SSH para se conectar à sua conta GitHub a partir do seu servidor, sem precisar inserir sua senha todas as vezes.

## Conclusão

Agora você criou com sucesso uma chave SSH e a adicionou à sua conta GitHub. Isso permitirá que você se conecte à sua conta GitHub a partir do seu servidor de forma segura e conveniente, sem precisar digitar sua senha todas as vezes.
