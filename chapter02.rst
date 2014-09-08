======================
Capítulo 2: Começando
======================

Instalar o Django é um processo de vários passos, em função das múltiplas partes que
envolve os cenários de desenvolvimento web hoje em dia. Neste capítulo, vamos leva-los através de 
como se instalar o framework e as suas dependencias.

Como o Django é "apenas" código Python, ele é executado em qualquer lugar que rode Python -- incluindo
alguns telefones celulares! Mas este capítulo abrange apenas os cenários comums para se 
instalar o Django. Vamos assumir que você esteje instalando em uma máquina desktop/laptop ou um servidor.

Depois, no Capítulo 12, nós iremos cobrir como fazer o deploy do Django para um site em produção.

Instalando o Django
====================

Django é puramente escrito em Python, então o primeiro passo para instalar o 
framework é ter certeza de que você tem o Python instalado.

Versões do Python
------------------

O núcleo do framework Django (versão 1.4) trabalha com qualquer versão do Python da 2.5
até a 2.7. O GIS(Geographic Information Systems) do Django exige o Python 2.5 até o 2.7.

Se você não tem certeza da versão do Python que que tem instalada e você tem
completa liberdade para tomar essa decisão, escolha a última versão da série 2.x: versão 2.7.
Embora Django funcione igualmente bem com qualquer versão 2.5 até 2.7, a ultima 
versão do Python tem boa performace de desempenho e idiomas adicionais
características que talvez você deseje ultilizar em suas aplicações. Além disso, 
add-ons de terceiros que você possa querer ultilizar talvez nescessite da mais recente que 
o Python 2.5, então ultilize a ultima versnao do Python mantendo o leque de opções em aberto.

.. admonition:: Django and Python 3.0

    No momento em que este livro estava sendo escrito, o Python 3.0 estava sendo lançado, mas Django
    foi testado apenas de experimentalmente. Python 3.0 intruduziu a 
    um número substancial de incompatibilidades com as versões anteriores, mundando 
    a si mesmo, e, como resultado, muita das principais bibliotecas Python e
    frameworks, incluindo Django, ainda não tinha pego.

    Django 1.5 dará suporte para o Python 2.6, 2.7, e 3.2. Entretando,
    suporte para o Python 3.2 é considerado um "preview", o que significa que
    os desenvolvedores Django não estão confiantes o suficiente para prometer
    estabilidade da produção. Para isso sugiro que você espere até a versão do Django 1.6 

Instalação
-----------

Se você estiver no Linux ou no Mac OS X, você provavelmente tem o Python instalado.
Escreva ``python`` no prompt de comando (ou em Applications/Utilities/Terminal, no Mac OS X).
Se você vê algo como isso, é porque o Python está instalado::

    Python 2.7.3rc2 (default, Apr 22 2012, 22:30:17)
    [GCC 4.6.3] on linux2
    Type "help", "copyright", "credits" or "license" for more information.
    >>>

Caso contrário, você prescisa fazer o download e instalar o Python. Isso é fácil e rápido
instruções detalhadas poderão ser encontradas em http://www.python.org/download/

Instalando Django
=================

Em um determinado momento, duas dinstintas versões dinstintas do Django estão disponíveis para você:
a última versão oficial e a versão de desenvolvimento. A versão que você decidir instalar 
depende das suas prioridades. Se você quer uma versão testada e estável, ou se você quer uma
versão contendo os recursos mais recentes. Talvez você possa contribuir para o Django, á custa de
estabilidade?

Nós recomendamos trabalhar com um lançamento oficial, mas é importante saber que a versão 
de desenvolvimento existe, porque você irá encontrar menções na documentação e pelos 
membros da comunidade.

Instalando um lançamento oficial
------------------------------

Um lançamento oficial tem um número de versão, como 1.4.2, 1.4.1 ou 1.4, 
um lançamento não oficial tem um número de versão, como 1.4.2, 1.4.1 ou 1.4, e a última 
estará sempre disponível em http://www.djangoproject.com/download/.

Se você está em uma distribuição Linux que inclui um pacote do Django, é uma boa ideia
usar a versão do distribuidor. Dessa forma você terá atualizações de segurança juntamente com
o resto dos pacotes do seu sistema.

Se você não tem acesso a uma versão pré-empacotada, você pode fazer o download e instalar
o framework manualmente. Para isso, primeiramente faça o do tarball, que será chamado
de algo como ``Django-1.4.2.tar.gz``. (Não importa em qual diretório local você tenha baixado
este arquivo inicial; O processo de instalação colocará os arquivos do Django no lugar correto.) 
Então, descompacte-o e e execute ``setup.py install``, como você faz com a maioria das bibliotecas
do Python.

Veja como esse processo se parece em sistemas Unix:

#. ``tar xzvf Django-1.4.2.tar.gz``
#. ``cd Django-*``
#. ``sudo python setup.py install``

No Windows, nós recomendamos o uso do 7-Zip (http://www.djangoproject.com/r/7zip/)
para descomprimir os arquivos ``.tar.gz``. Uma vez com os arquivos descompactados, inicie o DOS
shell (o "Prompt de Comando") com os privilégios de administrador e execute o comando seguinte 
dentro do diretório cujo nome começa com ``Django-``::

    python setup.py install

No caso de você estiver curioso: os arquivos do Django serão instalados no local da
instalação do seu Python no ``site-packages`` diretório -- um diretório aonde o o Python
procura por biblioteca de terceiros. Normalmente é um lugar como ``/usr/lib/python2.7/site-packages``.

Instalando a versão de "Desenvolvimento"
----------------------------------------

Django ultiliza o Git (http://git-scm.com) para o controle de versão. A mais
recente e maior versão de desenvolvimento do Django se encontra no seu oficial 
repositório do Git (https://github.com/django/django). Você deve considerar a 
instalação dessa versão se você quer trabalhar on the bleeding edge, ou se você quiser 
contribuir com o código do Django.

Git é gratuíto, um uma distribuição de código live de revisão de controle de sistema, e o
time do Django usa ele para controlar as mudanças no código fonte do Django. Você pode fazer
o download e instalar o Git no http://git-scm.com/download, mas é mas fácil instalar com
o controlador de pacots do seu sistema operacional. Você pode usar o Git para pegar a mais 
recente versão dos códigos do Django e, a qualquer momento, você pode atualizar os códigos 
da sua versão local do Django para obter as últimas alterações feitas pelos os desenvolvedores
Django.

Ao usar a versão de desenvolvimento, tenha em mente que não há coisas como garantias de que
não será quebrada a qualquer momento. Como dito, alguns membros do time do Django executa sites
de produção em versões de desenvolvimento, para que eles tenham um incentivo de mantê-los estáveis.

Para pegar a última versão do Django, siga esses passos:

#. Tenha certeza que você tenha o Git instalado. Você pode pegá-lo gratuitamente em http://git-scm.com/,
e você pode achar a excelente documentação em http://git-scm.com/documentation.

#. Clone o repositório usando o seguinte comando ``git clone https://github.com/django/django djmaster``

#. Localize na instalação do Python o diretório ``site-packages``. Normalmente
   fica localizada em um lugar como ``/usr/lib/python2.7/site-packages``. Se você não faz idéia,
   escreva isso no prompt de comando::

       python -c 'import sys, pprint; pprint.pprint(sys.path)'

    A saída resultante deverá incluir o diretório do seu ``site-packages``.

#. Dentro do diretório ``site-packages``, crie um arquivo chamado ``djmaster.pth``
  e edite ele para conter o caminho completo para o seu diretório ``djmaster``.
  Por exemplo, o arquivo poderia conter essa linha::

       /path/to/djmaster

#. Coloque ``djmaster/django/bin`` em seu PATH do sistema. Este diretório inclui
   inclui utilitários de administração, tais como o ``django-admin.py``.

.. admonition:: Dica:

    Se arquivos ``.pth`` são novos para você, você pode aprender mais sobre eles em
    http://www.djangoproject.com/r/python/site-module/.

Depois de baixar pelo Git e seguir os passos anteriores, não há nescessidade de 
executar ``python setup.py install``-- você acabou de fazer o trabalho manualmente!

Como o código do Django muda frequentemente com correção de bugs e adção de recurso,
você provavelmente queira atualiza-lo de vez em quando. Para atualizar o código, 
apenas execute o comando ``git pull origin master`` dentro do diretório ``djmaster``.
Quando você executar o comando, o Git entrará em contato com https://github.com/django/django,
determinando se algo código fonte foi mudado, e atualizando a sua versão local com as alterações
que tem sido feitas desde o último update. It's quite slick.

Finalmente, se você usa a versão de desenvolvimento do Django, você deve saber como 
qual a versão do Django está sendo executada. Conhecer o número da sua versão será importante
se você nescessitar correr até a comunidade para ajuda, ou se você apresentar melhorias 
para o framework. Nestes casos, você deverá dizer as pessoas que revisionam, também conhecido como "commit", 
o que você está usando. Para saber o seu atual "commit", digite "git log -1" de dentro de um diretório ``django``, e 
olhe para os identificadores depois de "commit". Este número muda toda vez que o Django é alterado,
seja por meio de uma correção de bug, adição de funcionalidade, documentação ou melhoria de qualquer coisa.

Testando a instalação do Django
================================

Para um feedback positivo de pós instalação, pare um instante para ver se a instalação
está funcionando. Em um shell de comando, mude para outro diretório (ex., *não* o diretório que que
contém o diretório ``django``) e inicie o interpretador interativo Python digitando ``python``. Se a 
instalação obteve exito, você podera importar o módulo ``django``:

    >>> import django
    >>> django.VERSION
    (1, 4, 2, 'final', 0)

.. admonition:: Exemplos do Interpretador Interativo

    O interpretador interativo do Python é um programa de linha de comando que permite que você escreva
    um programa Python interativamente. Para inicializa-lo, execute o comando ``python`` na linha de comando.

    Ao longo desse livro, apresentamos exemplos em sessões no interpretador interativo do Python. Você poderá
    reconhecer esses exemplos pelos três sinais de maior quê (``>>>``), que designam o interpretador no prompt. Se
    você está copiando exemplos deste livro, não copie estes sinais de maio-quê.

    Declarações de várias linhas nesse interpretador interativo são preenchidos com três pontos (``...``). Por exemplo::

        >>> print """This is a
        ... string that spans
        ... three lines."""
        This is a
        string that spans
        three lines.
        >>> def my_function(value):
        ...     print value
        >>> my_function('hello')
        hello

    Esses três pontos no inicio de linhas adicionais são inseridas pelo shell do Python -- eles não são parte
    daquilo que está sendo inserido. Nós incluimos aqui para ser fiel a saída real do interpretador. Se você copiar
    estes exemplos para acompanhar, não copie estes pontos.

Configurando um Banco de Dados
===============================

Neste ponto, você pode muito bem começar a escrever uma aplicação web com o Django, 
porque os pré-requisitos rápidos do Django é apenas estar trabalhando com uma instalação do Python.
No entanto, as probabilidades de que você irá desenvolver um Web site com um *banco de dados dirigido*, 
neste caso, você nescessitará de configurar um servidor de banco de dados.

Se você apenas quer começar a jogar com o Django, pule para a seção "Começando um Projeto" --
mas tenha em mente que todos os exemplos desse livro asumme que você tenha trabalhado configurado
um banco de dados.

Django suporta quatro tipo de banco de dados

* PostgreSQL (http://www.postgresql.org/)
* SQLite 3 (http://www.sqlite.org/)
* MySQL (http://www.mysql.com/)
* Oracle (http://www.oracle.com/)

Para a maior parte, todos esses bancos de dados trabalham igualmente bem com o núcleo do Django framework.
(Uma notável excessão é o opcional GIS suporte ao Django, que é muito mais poderoso que o PostgreSQL do que 
com outros bancos de dados.) Se você não estiver amarrado a nenhum sistema legado e tem a liberdade para 
escolher o banco de dados, nós recomendamos PostgreSQL, que alcança um bom equilibrio entre custo, recurso, 
velocidade e estabilidade.

Configurar o banco de dados é um processo de duas etapas:

* Primeiro, você prescisa instalar e configurar servidor de banco de dados em si.
  Este processo está além do escopo desse livro, mas cada um dos quatro banco de dados
  tem uma rica documentação em seus próprios websites. (Se, você está em um servidor
  de hospedagem compartilhado, provavelmente eles irão definiram isso para você.)

* Segundo, você prescisa instalar a biblioteca Python para o seu banco de dados em particular. 
  Isso é um pouco de código de terceiros que permite ao Python se comunicar com o banco de dados.
  Nós delineamos especificamente, por requerimentos de banco de dados nas seções seguintes.

Se você está apenas brincando um pouco com o Django e não quer instalar um servidor de 
banco de dados, considere então usar o SQLite. SQLite é o unico na lista de banco de dados suportados
é o único que não requere nenhum dos passos citados acima. Ele se limita em ler e escrever informações
em um único arquivo em seu sistema, e a versão 2.5 do Python ou superior inclui um suporte nativo para ele.

No Windows, a obtenção de drives binários do banco de dados pode ser algo frustante. Se você está ansioso para
saltar, nós recomendamos o uso do Python 2.7 e seu suporte nativo para o SQLite.

Usando Django com o PostgresSQL
--------------------------------

Se você esta usando o PostgreSQL, você nescessita instalar o pacote ``psycopg`` ou o ``psycopg2`` 
pelo endereço http://www.djangoproject.com/r/python-pgsql/. Nós recomendamos ``psycopg2``, como é mais novo, 
mais ativamente desenvolvido e pode ser fácilmente instalado. De qualquer forma, tome nota da versão que 
você está ultilizando, a versão 1 ou a 2; você irá nescessitar dessa informação posteriormente.

Se você está usando o PostgreSQL no Windows, se pode achar um precompilador de binários do ``psycopg``
no http://www.djangoproject.com/r/python-pgsql/windows/.

Se você estiver no Linux, verifique se a sua distribuição de gerenciamento de pacotes sistemas ofereçe
um pacote chamado "python-psycopg2", "psycopg2-python", "python-postgresql" ou alguma coisa similar.

Usando Django com SQLite 3
--------------------------

Você está com sorte: pois não é requerido especificidades de banco de dados, porque o Python vem com suporte
so SQLite. Pule para a próxima seção.

Usando Django com MySQL
-----------------------

Django requer MySQL 4.0 ou acima. As versões 3.x não suportam subconsultas aninhadas 
e algumas outras instruções SQL bastante comuns.

Será nescessário instalar também o pacote ``MySQLdb``: http://www.djangoproject.com/r/python-mysql/.

Se estiver no Linux, verifique se a sua distribuição de sistema de gerenciamento de pacotes
oferece um pacote chamado "python-mysql", "python-mysqldb", "mysql-python" ou algo parecida.

Using Django com Oracle
------------------------

Django trabalha com o Oracle Database Server verões 9i ou superior.

Se você está usando Oracle, você nescessita instalar a biblioteca ``cx_Oracle``,
no http://cx-oracle.sourceforge.net/. Use a verão 4.3.1 ou superior, mas evite a versão 5.0
devido a um bug nesta versão do driver. A versão 5.0.1 resolveu o bug, entretando, você pode escolher 
uma versão superior também.

Usando Django sem um Banco de Dados
------------------------------------

Como mencionado anteriormente, o Django atualmente não requer o uso de banco de dados. Se você quer apenas
usar ele como servidor de páginas dinâmicas que não ultilizam o banco de dados, está
tudo perfeitamente bem.

Como o que disse, tenha em mente que algumas das ferramentas extras juntas com o Django *ultilizam* um banco
de dados, então se você escolher não usar um banco de dados, você não poderá usufruir desses recursos.
(Destacamos esses recursos ao longo do livro.)

Começando um Projeto
=====================

Uma vez que o Python esteja instalado, Django e (opcionalmente) um servidor/biblioteca de banco de dados,
você pode pegar o primeiro passo no desenvolvimento de uma aplicação Django atravéz da criação de um *projeto*.

Um projeto é uma coleção de configurações para uma instância do Django, incluindo uma configuração de banco de
dados, opções específicas do Django e configurações de aplicações específicas.

Se esta é a sua primeira vez usando Django, você terá que cuidar de algumas configurações iniciais.
Criar um novo diretório para começar a trabalhar nele, talvez alguma coisa parecida como ``/home/username/djcode``.

.. admonition:: Aonde Coloco Esse Diretório Vivo?
    
    Se você já tem alguma experiência com PHP, você provavelmente está acostumado a colocar o código sobre a raiz do
    servidor (um lugar como ``/var/www``). Com Django, você não faz isso. Não é uma boa idéia colocar qualquer código
    Python dentro da raíz do seu servidor web. Porque ao fazê-lo você corre o risco das pessoas verem o seu código fonte.
    E isso não é bom.

    Coloque o seu código em algum diretório **fora** da raíz do documento.

Vá até o diretório que você criou, e execute o comando ``django-admin.py startproject mysite``. Isso irá criar um diretório
chamado``mysite`` no seu diretório corrente.

.. nota::
    ``django-admin.py`` deve estar no path do sistema se você instalou o Django via o utilitário ``setup.py``

    Se você estiver usando uma versão de desenvolvimento, você irá achar ``django-admin.py`` em ``djmaster/django/bin``.
    Por causa que você irá usar ``django-admin.py`` várias vezes, considere adicionar ao path do sistema. No Unix, você pode
    fazer isso usando links simbólicos de ``/usr/local/bin``, usando um comando como ``sudo ln -s /path/to/django/bin/django-admin.py
    /usr/local/bin/django-admin.py``. No Windows, você nescessitará atualizar o seu variávem de ambiente ``PATH``. 

    Se você instalou o Django de um pacote de versão para o sua distribuição Linux, ``django-admin.py`` pode ser chamado
    de ``django-admin``.

Se você ver uma mensagem de "permission denied" ao executar ``django-admin.py startproject``, você nescessitará mudar as 
permissões dos arquivos. Para isso, navegue até o diretório aonde ``django-admin.py`` está instalado (e.g., ``cd /usr/local/bin``)
e execute o comando ``chmod +x django-admin.py``.

O commando ``startproject``  cria um diretório contendo 5 arquivos::

    mysite/
        manage.py
        mysite/
            __init__.py
            settings.py
            urls.py
            wsgi.py

.. nota:: Não corresponde com você vê?
    
    O layout padrão do projeto recentemente mudado. Se você está vendo um layout "flat" (sem o diretório interior
    ``mysite/``), você provavelmente está usando uma versão do Django que não corresponde a versão do livro. Este 
    livro cobre Django 1.4 acima, então se você está usando uma versão antiga você provavelmente vai querer
    consultar o dacumentação oficial do Django.

    A documentação das versões Django 1.x está no endereço  https://docs.djangoproject.com/en/1.X/.

Estes arquivos são os seguintes

* ``mysite/``: O exterior do diretório ``mysite/`` é apenas um container para o seu projeto. Esse nome
  não importa para o Django; você pode renomear ele da maneira que desejar.

* ``manage.py``: Um utilitário de linha de comando que permite que você interaja com o projeto Django de várias formas.
  Escreva ``python manage.py help`` para entender o que ele é capaz de fazer. Você nunca deverá editar este arquivo;
  ele é criado nesse diretório puramente por conveniência.

* ``mysite/mysite/``: O interior do diretório ``mysite/`` é o atual pacote Python para o seu projeto. Este nome é o nome 
  do pacote Python que você nescessita usar para importar qualquer coisa dentro dele (e.g. ``import mysite.settings``).

*``__init__.py``: Um arquivo necessário para o Python tratar o diretório ``mysite`` como um pacote (i.e., um grupo de 
módulos Python). Ele é um arquivo vazio, e geralmente você não adiciona nada a ele.

* ``settings.py``: Definições/configurações para este projeto Django. Dê uma olhada nele para ter uma idéia dos tipos
  configurações avaliadas, juntamente com os seus valores padrões.

* ``urls.py``: As URLs para este projeto Django. Pense nisso como como uma "tabela de conteúdo" para o seu site em Django.  

* ``wsgi.py``: Um ponto de entrada para o WSGI compatíveis com servidores web para servir o seu projeto.
  Veja como fazer deploy com WSGI (https://docs.djangoproject.com/en/1.4/howto/deployment/wsgi/) para maiores detalhes.

Apesar do seu pequeno tamanho, estes arquivos já constituem uma aplicação de trabalho Django.

Executando o servidor de desenvolvimento
-----------------------------------------

Para mais alguns feedbacks positívos após a instalação, vamos executar o servidor de desenvolvimento do Django 
para ver a nossa aplicação em ação.

O servidor de desenvolvimento do Django (também chamado de "runserver") é um servidor interno, leve, que 
você poderá usar enquanto desenvolve o seu site. Ele é incluso com o Django então você pode desenvolver o seu 
seite rapidamente, sem ter que lidar com configuracão de servidor de produção (e.g., Apache) até que você esteja
realmente pronto para o ambiente de produção. O servidor de desenvolvimento observa o seu código e automáticamente
recarrega automáticamente, tornando fácil para você alterar o seu código sem a necessidade de de reiniciar qualquer coisa.

Para iniciar o servidor, mude para o seu diretório do container do projeto (``cd mysite``), se você não estiver, 
execute este commando::

    python manage.py runserver

You'll see something like this::

    Validating models...
    0 errors found.

    Django version 1.4.2, using settings 'mysite.settings'
    Development server is running at http://127.0.0.1:8000/
    Quit the server with CONTROL-C.

Isso inicia o servidor localmente, na porta 8000, acessível somente para conecções do seu próprio computador. Agora que 
está rodando visite http://127.0.0.1:8000/ com o seu web browser. Você vai ver um "Welcome to Django" em uma página sombreada 
com agradáveis tons de azul pastel. Está funcionando!!

Uma nota final importante sobre o servidor de desenvolvimento que é importante mencionar antes de prosseguir. Embora 
este servidor seja conveniente para o desenvolvimento, resistir a tentação de usá-lo em qualquer coisa parecida com um 
ambiente e produção. O servidor de desenvolvimento pode lidar com apenas um pedido de cada vez de maneira confiável, e 
não passou por nenhuma espécie de auditoria de segurança. Quando chegar a hora de lançar o seu site, consulte o Capítulo
12 para informações sobre como fazer o deploy do Django.

.. admonition:: Mudando o Host ou Porta do Servidor de Desenvolvimento
    Por padrão, o comando `runserver` inicializa o servidor de desenvolvimento na porta 8000, ouvindo somente para 
    conexões locais. Se você deseja mudar a porta do servidor, passe isso como argumento na linha de comando::

        python manage.py runserver 8080

    Ao especificar um endereço de IP, você pode dizer ao servidor para permitir conexões não locais. Isso é especificamente
    útil se você quisesse compartilhar um site de desenvolvimento com outros membros da sua equipe. O endereço de IP ``0.0.0.0``
    diz ao servidor atender qualquer interface de rede::

        python manage.py runserver 0.0.0.0:8000

    Quando você tiver feito isso, outros computadores da sua rede local poderão visualizar o seu site em Django visitando o seu
    endereço de IP no Web browser, e.g., http://192.168.1.103:8000/ .(Note que você terá que consutar as suas configurações de rede
    para determinar o seu endereço de IP em sua rede local. Usuários Unix, tentarão rodar "ifconfig" no prompt de comando para 
    pegar essa informação, usuários Windows, tentarão "ipconfig".)

O que vem em seguida?
=====================

Agora que você tem tudo instalado e o servidor de desenvolvimento rodando, você está pronto para o :doc:`aprendendo
o básico <cápitulo03>` de servir páginas Web com Django.
