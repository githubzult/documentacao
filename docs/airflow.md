# Apache Airflow
## Preparando ambiente

Em primeiro lugar, é altamente recomendável criar um usuário específico para o Airflow:

`useradd airflow`

### Pacotes de desenvolvimento necessários:

`yum instalar gcc`

`yum instalar python3-devel`

`yum instalar mysql-devel`


### Vamos instalar o Airflow e pacotes extras se necessários:

`pip3 instalar apache-airflow`

`pip3 instalar 'apache-airflow[crypto]' `

`pip3 instalar 'apache-airflow[mysql]'`

### Preparação do Daemon do Airflow

Antes de podermos configurar nosso `systemd` serviço para o Airflow, precisamos fazer alguns preparativos. A primeira etapa será baixar os arquivos de definição de serviço do Airflow GitHub Repo.

<https://github.com/apache/airflow/tree/master/scripts/systemd>

**Baixe os arquivos do serviço daemon**

Vamos criar uma pasta temporária para os arquivos de download.

`mkdir /tmp/airflow-daemon `

`cd /tmp/airflow-daemon`


**Em seguida, baixe os arquivos para esta pasta temporária.**

`wget https://raw.githubusercontent.com/apache/airflow/master/scripts/systemd/airflow`

`wget https://raw.githubusercontent.com/apache/airflow/master/scripts/systemd/airflow-scheduler.service` 

`wget https://raw.githubusercontent.com/apache/airflow/master/scripts/systemd/airflow-webserver.service` 

`wget https://raw.githubusercontent.com/apache/airflow/master/scripts/systemd/airflow.conf` 

*Os arquivos systemd neste diretório são testados em sistemas baseados em RedHat. Copie (ou vincule-os) para /usr/lib/systemd/system
e copie o airflow.conf para /etc/tmpfiles.d/ ou /usr/lib/tmpfiles.d/. Copiar airflow.conf garante que /run/airflow seja
criado com o proprietário e as permissões corretos (0755 airflow airflow)*

*Você pode então iniciar os diferentes servidores usando systemctl start <service>. A habilitação de serviços pode ser feita emitindo
systemctl enable <service>.*

*Por padrão, a configuração do ambiente aponta para /etc/sysconfig/airflow . Você pode copiar o arquivo “airflow” neste
diretório e ajustá-lo ao seu gosto.*

*Com algumas pequenas alterações, eles provavelmente funcionam em outros sistemas systemd.*


Bem, acho que para a maioria daqueles que não têm experiência em Linux, a documentação acima pode ser muito vaga e enganosa. Então, desenhei este diagrama para mostrar qual arquivo deve ser colocado em qual caminho.

![estrutura](/docs/assets/img/scripts-systemd.jpg)


De acordo com o caminho indicado no diagrama, vamos copiar os arquivos para o local correto.

*Crie os diretórios necessários*
Também precisamos criar alguns diretórios que o daemon requer. Em primeiro lugar, ele precisa de um diretório dedicado para armazenar informações de tempo de execução, como o arquivo pid. Vamos criar o diretório sob o /rundiretório e alterar a permissão.

`mkdir /run/airflow`

`chown airflow:airflow /run/airflow`

`chmod 0755 airflow -R`

Observe que a permissão está definida como `0755` praticamente porque podemos ter vários outros usuários para desenvolver DAGs (fluxos de trabalho) no Airflow. Com `0755` permissão, garante que todos os outros usuários tenham seu grupo secundário, pois `airflow` terão permissões suficientes.

Outro diretório que precisamos criar é o diretório inicial do Airflow, que inclui:

* configurações de fluxo de ar
* SQLite que é usado pelo Airflow
* DAG
* Registros de DAGs

Normalmente, se não houver `export AIRFLOW_HOME=...`, eles serão gerados automaticamente no diretório inicial do usuário atual, como `/home/airflow/airflow/`. 

Isso é bom se você estiver testando o Airflow ou desenvolvendo alguns DAGs. No entanto, não é recomendado e também não é conveniente em produção, porque outros usuários não acessarão facilmente airflowo diretório inicial do usuário.

No meu caso, gostaria de colocar o diretório inicial do Airflow em `/opt`, então vamos criá-lo.

Novamente, altere a permissão para permitir que todos os usuários do `airflow` grupo possam não apenas ler, mas também gravar no diretório porque precisam modificar os DAGs.

*Inicializando o diretório inicial do Airflow*
Tudo está preparado. Precisamos inicializar o diretório inicial do Airflow. É importante exportar o diretório inicial para a `AIRFLOW_HOME` variável de ambiente. Caso contrário, o diretório inicial será gerado automaticamente na pasta pessoal do usuário conforme mencionado acima.

`export AIRFLOW_HOME=/opt/airflow `

`airflow initdb`

### Configurar o Daemon do Airflow

Agora, todos os arquivos de serviço, arquivos de configuração e diretórios necessários estão prontos. Precisamos configurar o daemon para garantir que tudo esteja apontando para os caminhos corretos antes que o daemon possa ser executado corretamente.

Em primeiro lugar, vamos verificar novamente o caminho do `airflow` arquivo binário porque ele precisa ser especificado na definição do serviço posteriormente.

`$ which airflow`

`/usr/local/bin/airflow`

Então, vamos modificar a definição do `airflow-webserver`.

`nano /usr/lib/systemd/system/airflow-scheduler.service`

Da mesma forma, vamos alterá-lo o `airflow-scheduler`, também.

`nano /usr/lib/systemd/system/airflow-webserver.service`

note que o `pid` precisa ser escrito no diretório que acabamos de criar `/run/airflow`.

`ExecStart=/usr/local/bin/airflow servidor web --pid /run/airflow/webserver.pid`

Então, precisamos modificar a configuração do sistema do Airflow. Caso contrário, os serviços não saberão onde está o diretório inicial do Airflow.

`nano /etc/sysconfig/airflow`

As duas configurações abaixo precisam ser modificadas da seguinte forma, com base no que acabamos de preparar.

`AIRFLOW_CONFIG=/opt/airflow/airflow.cfg`

`AIRFLOW_HOME=/opt/airflow`

Como última etapa da configuração dos serviços, precisamos habilitá-los antes de executá-los.

`systemctl enable airflow-scheduler`

`systemctl enable airflow-webserver`