# Instalação do MySQL Server no CentOS 8.0

O MySQL Server é um sistema gerenciador de banco de dados relacionais amplamente utilizado. O CentOS 8.0 é um sistema operacional baseado em Linux popular que é compatível com o MySQL Server. Neste guia, você aprenderá como instalar o MySQL Server no CentOS 8.0 usando o gerenciador de pacotes yum.

### Pré-requisitos

Antes de começar, certifique-se de que o CentOS 8.0 esteja atualizado com os pacotes mais recentes. Para fazer isso, execute o seguinte comando:

`sudo yum update`


### Passo 1: Adicione o repositório MySQL

O MySQL Server não está disponível nos repositórios padrão do CentOS 8.0. Você precisará adicionar o repositório oficial do MySQL para instalar o servidor.

Para fazer isso, crie um arquivo chamado `mysql.repo` no diretório `/etc/yum.repos.d/` usando o editor de texto de sua preferência. No exemplo a seguir, usaremos o editor de linha de comando nano:

`sudo nano /etc/yum.repos.d/mysql.repo`


Adicione o seguinte conteúdo ao arquivo `mysql.repo`:


Salve e feche o arquivo.

### Passo 2: Instale o MySQL Server

Agora que você adicionou o repositório MySQL, pode instalar o MySQL Server usando o gerenciador de pacotes yum. Execute o seguinte comando para instalar o MySQL Server:

`sudo yum install mysql-server`


O comando acima instalará o MySQL Server e suas dependências.

### Passo 3: Inicie o MySQL Server

Após a instalação, inicie o serviço do MySQL Server executando o seguinte comando:

`sudo systemctl start mysqld`


Você também pode verificar o status do serviço MySQL Server usando o seguinte comando:

`sudo systemctl status mysqld`


Se o serviço estiver em execução, você verá uma saída semelhante a esta:

● mysqld.service - MySQL 8.0 database server
Loaded: loaded (/usr/lib/systemd/system/mysqld.service; enabled; vendor preset: disabled)
Active: active (running) since Sat 2023-03-13 16:30:00 UTC; 10s ago
Docs: man:mysqld(8)
http://dev.mysql.com/doc/refman/en/using-systemd.html
Process: 22005 ExecStart=/usr/sbin/mysqld --daemonize --pid-file=/var/run/mysqld/mysqld.pid $MYSQLD_OPTS (code=exited, status=0/SUCCESS)
Process: 21982 ExecStartPre=/usr/bin/mysqld_pre_systemd (code=exited, status=0/SUCCESS)
Main PID: 22007 (mysqld)
Status: "Server is operational"
Tasks: 38 (limit: 32768)
Memory