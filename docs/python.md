# Instalando o Python 3.8 no CentOS 8.0

Este guia irá ajudá-lo a instalar o Python 3.8 no CentOS 8.0. Este processo envolve o uso do gerenciador de pacotes padrão do CentOS 8.0, o DNF.

## Passo 1: Atualizando o sistema

Antes de começar, é recomendado atualizar o sistema operacional para garantir que você esteja usando a versão mais recente do CentOS 8.0. Para atualizar o sistema, execute o seguinte comando:

`sudo dnf update`


Este comando irá atualizar o sistema e instalar as atualizações disponíveis.

## Passo 2: Instalando o Python 3.8

Após a atualização do sistema, o próximo passo é instalar o Python 3.8. O CentOS 8.0 possui o Python 3.x instalado por padrão, mas não inclui a versão 3.8. Para instalá-lo, execute o seguinte comando:

`sudo dnf install python38`


Este comando irá instalar o Python 3.8 e suas dependências.

## Passo 3: Verificando a instalação

Após a instalação, verifique se o Python 3.8 está instalado e funcionando corretamente. Para fazer isso, execute o seguinte comando:

`python3.8 --version`


Isso deve exibir a versão do Python 3.8 instalada no seu servidor.

## Passo 4: Instalando pacotes adicionais via arquivo

Se você precisar instalar pacotes adicionais no seu servidor CentOS 8.0, é possível fazê-lo através de um arquivo que contém uma lista dos pacotes a serem instalados. Isso é especialmente útil se você precisar instalar vários pacotes de uma só vez.

Para instalar pacotes adicionais via arquivo, siga os seguintes passos:

1. Crie um arquivo de texto chamado `pacotes.txt` e adicione os nomes dos pacotes que você deseja instalar. Cada pacote deve estar em uma linha separada. Por exemplo, se você quiser instalar o pacote `numpy` e o pacote `scipy`, o arquivo `pacotes.txt` deve ser semelhante a este:

numpy
scipy


2. Salve o arquivo `pacotes.txt` em um diretório de sua escolha.

3. No terminal, navegue até o diretório onde você salvou o arquivo `pacotes.txt`.

4. Execute o seguinte comando para instalar os pacotes listados no arquivo `pacotes.txt`:

`sudo dnf install -y $(cat pacotes.txt)`


O sinal `$` é usado para substituir o conteúdo do arquivo `pacotes.txt` como argumentos para o comando `dnf install`. O sinal `-y` é usado para confirmar a instalação sem exigir interação do usuário.

Após a execução deste comando, todos os pacotes listados no arquivo `pacotes.txt` serão instalados no seu servidor CentOS 8.0.

## Conclusão

Agora você sabe como instalar o Python 3.8 e pacotes adicionais via arquivo em um servidor CentOS 8.0. Com esta instalação, você pode prosseguir com o
