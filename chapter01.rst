=================================
Capítulo 1: Introdução ao Django
=================================

Esse livro é sobre o Django, um framework para desenvolvimento web que salva seu tempo 
e faz o desenvolvimento web ser divertido. Usando Django, você pode criar e manter em alta qualidade 
aplicações web com mínimos exageros.

E o melhor, desenvolvimento web é excitante, um ato criativo, ao contrário pode ser 
repetitivo, e altamente frustrante. Django permite que você se foque na parte boa 
-- no ponto crucial de sua aplicação web -- facilitando alguns bits repetitivos. 
Usando-o, ele fornece abstrações de alto nível de desenvolvimento web normalmente utilizados, 
atalhos para tarefas frequentes de programação, e convenções claras de como resolver problemas.
Ao mesmo tempo, Django tenta ficar fora do seu caminho, permitindo-o trabalhar fora do escopo como
necessário.

O objetivo desse livro é tornar você um expert em Django. O foco é duplo. Primeiro, 
nós explicaremos, a fundo, o que o Django faz e como criar aplicações web com isso. 
Segundo, nós discutiremos conceitos de nível superior quando apropriados, respondendo a questão 
"Como eu posso aplicar essas ferramentas de efetivamente em meus projetos?" Lendo esse livro, 
você aprenderá as habilidades necessárias para criar poderoros web sites rapidamente, 
com código que seja limpo e fácil de se manter.

O que é um framework web?
========================

Django é proeminente membro de uma nova geração de frameworks web 
-- mas o que esse termo significa, precisamente?

Para responder essa questão, vamos considerar que o design de uma aplicação web 
escrita em Python sem um framework. Ao longo desse livro, nós iremos através dessa 
abordagem mostrar os caminhos básicos de fazer as coisas sem atalhos, na esperança 
que você reconhecerá o porquê de atalhos serem tão úteis. (Será valioso saber como 
ter as coisas feitas sem atalhos porque atalhos nem sempre poderão ser usados. 
E o mais importante, saber como as coisas trabalham o torna um desenvolvedor web melhor.

Uma das mais simples, mais diretas formas de criar uma aplicação Python do começo 
é usar a Common Gateway Interface(CGI) padrão, que foi uma popular técnica em 1998. 
Aqui está uma explicação alto-nível de como isso funciona: Apenas crie um script 
Python que libere HTML, então salve o código em um web server com a extensão ".cgi" 
e visite a página em seu navegador. É isso.

Este é um exemplo de código de Python CGI que mostra os dez livros mais recentes 
de uma base de dados. Não se preocupe com os detalhes da sintaxe; apenas sinta como funciona::

    #!/usr/bin/env python

    import MySQLdb

    print "Content-Type: text/html\n"
    print "<html><head><title>Books</title></head>"
    print "<body>"
    print "<h1>Books</h1>"
    print "<ul>"

    connection = MySQLdb.connect(user='me', passwd='letmein', db='my_db')
    cursor = connection.cursor()
    cursor.execute("SELECT name FROM books ORDER BY pub_date DESC LIMIT 10")

    for row in cursor.fetchall():
        print "<li>%s</li>" % row[0]

    print "</ul>"
    print "</body></html>"

    connection.close()

Primeiro, para preencher os requerimentos do CGI, esse código exibe a linha "Content-Type",
seguido por uma linha branca. Isto exibe algumas introduções de HTML, conectando a um banco
de dados e funcionando uma busca para recuperar os nomes dos últimos 10 livros. Circulando 
sobre esses livros, ele gera uma lista de títulos HTML. Finalmente, ele retorna o fechamento 
do HTML e fecha a conexão com o banco de dados.

Com uma simples página, o modo "escrevendo desde o início" não é necessáriamente ruim. Para 
apenas uma coisa, esse código é simples para compreender -- mesmo um desenvolvedor novato 
pode ler essas 15 linhas de Python e entender o que faz tudo, do começo ao final. Não há nada 
mais para aprender, nenhum outro código a ler. E também fácil de lançar: apenas salve esse 
código em um arquivo que termine com ".cgi", suba o arquivo em um servidor web, e visite a 
página com um navegador.

Mas apesar da simplicidade, essa abordagem contém uma série de contratempos e problemas. 
Pergunte a si mesmo essas questões:

* O que acontece quando múltiplas partes de sua aplicações precisarem conectar ao 
seu banco de dados? Certamente que o código da conexão da base de dados não precisa 
ser duplicado a cada código CGI. A forma pragmática de se fazer seria refatorá-lo 
em uma função compartilhada.

* Deveria um desenvolvedor realmente se preocupar sobre exibir a linha "Content-Type" 
e lembrando de fechá-la a conexão do banco de dados? Esses tipos de clichê reduzem a 
produtividade do programador e introduz algumas oportunidades para erros. Este setup- 
e tarefas desmontadas seriam melhores tratadas por algumas infra-estruturas comuns.

* O que acontece quando esse código é usado em diversos ambientes, cada um com uma base 
de dados separada e senha? Nesse ponto, algumas configurações de ambientes específicos 
se tornam essenciais.

* O que acontece quando um Web designer que não tem nenhuma experiência em escrever 
Python desejar redesenhar a página? Um simples caractere poderia quebrar a aplicação 
inteira. Idealmente, a lógica dessa página -- a recuperação dos títulos dos livros 
do banco de dados -- poderia ser separada da exibição HTML da página, então o designer
poderia editar este sem afetar o último.

Esses problemas são precisamente o que um framework web tende a resolver. Um framework 
web fornece uma infraestrutura de programação para suas aplicações, então forcar em 
escrever limpo, manutenível código sem reinventar a roda. Por cima, isso é o que o Django faz.


Os padrões de projeto MVC
======================

Vamos nos aprofundar com um rápido exemplo que demonstra a diferença entre a 
abordagem antiga e a abordagem de um web framework. Aqui está como você deveria 
escrever o código CGI usando Django. A primeira coisa a notar é que nós dividimos 
em 4 arquivos Python(``models.py``, ``views.py``, ``urls.py``) e um HTML 
template(``latest_books.html``)::

    # models.py (the database tables)

    from django.db import models

    class Book(models.Model):
        name = models.CharField(max_length=50)
        pub_date = models.DateField()


    # views.py (the business logic)

    from django.shortcuts import render
    from models import Book

    def latest_books(request):
        book_list = Book.objects.order_by('-pub_date')[:10]
        return render(request, 'latest_books.html', {'book_list': book_list})


    # urls.py (the URL configuration)

    from django.conf.urls.defaults import *
    import views

    urlpatterns = patterns('',
        (r'^latest/$', views.latest_books),
    )


    # latest_books.html (the template)

    <html><head><title>Books</title></head>
    <body>
    <h1>Books</h1>
    <ul>
    {% for book in book_list %}
    <li>{{ book.name }}</li>
    {% endfor %}
    </ul>
    </body></html>

Novamente, não se preocupe sobre as particularidades da sintaxe; apenas 
pegue a ideia de como é o design. A principal coisa a notar aqui é a *separação 
de interesses*:

* O arquivo ``models.py`` contém a descrição da tabela do banco de dados, 
representado por uma classe Python. Essa classe é chamada de *model*. 
Usando isso, você pode criar, recuperar, atualizar e deletar gravações 
em sua base de dados usando um simples código melhor do que escrever 
repetitivos SQL's.

* O arquivo ``views.py`` contém a lógica de negócio da página. A função 
``latest_books()`` é chamada de *view*.

* O arquivo ``urls.py`` especifica qual view é chamada quando for dada 
uma amostra de URL. Nesse caso, a URL ``/latest/`` será manipulada pela 
função ``latest_books()``. Em outras palavras, se seu domínio é example.com, 
qualquer visita a URL http://example.com/latest/ será chamada a função 
``latest_books()``.

* O arquivo ``latest_books.html`` é um HTML template que descreve o design da 
página. Isso usa uma linguagem de template com a lógica básica 
-- e.g. ``{% for book in book_list %}``.

Tendo-os juntos, essas peças formam o padrão chamado Model-View-Controller(MVC). 
Simples mas, MVC é um caminho de desenvolvimento de software que o código de 
definição e acesso de dados(o model) é separado da lógica de requisito de rotas
(o controller), que por sinal separado da interface do usuário(the view). 
(Nós iremos discutir MVC mais afundo no capítulo 5.)

A vantagem chave dessa forma são os componentes que são *fracamente aclopados*. 
Cada distinta peça de uma aplicação feita em Django teve uma simples proposta 
chave e pode ser mudada independente sem afetar as outras peças. Por exemplo, 
o desenvolvedor pode mudar a URL para outra parte da aplicação sem afetar a 
implementação subjacente. Um designer pode mudar a página HTML sem ter que 
tocar o código Python que o renderiza. O administrador do banco de dados pode 
renomear uma tabela da banco de dados e especificar a mudança em um simples local, 
melhor que ter que procurar e substituir através de diversos arquivos.

Nesse livro, cada componente do MVC tem seu próprio capítulo. Capítulo 3 cobre
as views, capítulo 4 cobre os templates, e o capítulo 5 cobre os models.

História do Django
================

Antes de mergulharmos em mais código, devemos ter um momento para explicar a história do Django. 
Já mencionamos que iremos mostrar a você como fazer as coisas sem atalhos para que você tenha maior 
compreensão sobre os atalhos. Igualmente, é muito útil entender porque Django foi criado, conhecendo
a história irá colocar você no contexto de como o Django trabalha e da maneira que ele faz.

Se você já esteve criando aplicações web por um tempo, provavelmente está familiarizado com os problemas
que foram apresentados anteriormente no exemplo CGI. O caminho clássico do desenvolvimento web é assim:


1. Escrever uma aplicação web desde o começo.
2. Escrever outra aplicação web desde o começo.
3. Se dar conta que a aplicação do primeiro exemplo tem muito em comum com a 
   aplicação do segundo exemplo.
4. Refatorar o código para que a aplicação 1 compartilhe o código com a aplicação 2.
5. Repetir os passos 2-4 algumas vezes.
6. Se dar conta que você criou um framework.

Isto é precisamente como o Django foi criado!

Django grew organically from real-world applications written by a Web
development team in Lawrence, Kansas, USA. It was born in the fall of 2003,
when the Web programmers at the *Lawrence Journal-World* newspaper, Adrian
Holovaty and Simon Willison, began using Python to build applications.

The World Online team, responsible for the production and maintenance of
several local news sites, thrived in a development environment dictated by
journalism deadlines. For the sites -- including LJWorld.com, Lawrence.com and
KUsports.com -- journalists (and management) demanded that features be added
and entire applications be built on an intensely fast schedule, often with only
days' or hours' notice. Thus, Simon and Adrian developed a time-saving Web
development framework out of necessity -- it was the only way they could build
maintainable applications under the extreme deadlines.

In summer 2005, after having developed this framework to a point where it was
efficiently powering most of World Online's sites, the team, which now included
Jacob Kaplan-Moss, decided to release the framework as open source software.
They released it in July 2005 and named it Django, after the jazz guitarist
Django Reinhardt.

Now, several years later, Django is a well-established open source project with
tens of thousands of users and contributors spread across the planet. Two of
the original World Online developers (the "Benevolent Dictators for Life,"
Adrian and Jacob) still provide central guidance for the framework's growth,
but it's much more of a collaborative team effort.

This history is relevant because it helps explain two key things. The first is
Django's "sweet spot." Because Django was born in a news environment, it offers
several features (such as its admin site, covered in Chapter 6) that are
particularly well suited for "content" sites -- sites like Amazon.com,
craigslist.org, and washingtonpost.com that offer dynamic, database-driven
information. Don't let that turn you off, though -- although Django is
particularly good for developing those sorts of sites, that doesn't preclude it
from being an effective tool for building any sort of dynamic Web site.
(There's a difference between being *particularly effective* at something and
being *ineffective* at other things.)

The second matter to note is how Django's origins have shaped the culture of
its open source community. Because Django was extracted from real-world code,
rather than being an academic exercise or commercial product, it is acutely
focused on solving Web development problems that Django's developers themselves
have faced -- and continue to face. As a result, Django itself is actively
improved on an almost daily basis. The framework's maintainers have a vested
interest in making sure Django saves developers time, produces applications
that are easy to maintain and performs well under load. If nothing else, the
developers are motivated by their own selfish desires to save themselves time
and enjoy their jobs. (To put it bluntly, they eat their own dog food.)

.. AH The following sections are the type of content that typically appears
.. AH in a book's Introduction section, but we include it here because this
.. AH chapter serves as an introduction.

How to Read This Book
=====================

In writing this book, we tried to strike a balance between readability and
reference, with a bias toward readability. Our goal with this book, as stated
earlier, is to make you a Django expert, and we believe the best way to teach is
through prose and plenty of examples, rather than providing an exhaustive
but bland catalog of Django features. (As the saying goes, you can't expect to
teach somebody how to speak a language merely by teaching them the alphabet.)

With that in mind, we recommend that you read Chapters 1 through 12 in order.
They form the foundation of how to use Django; once you've read them, you'll be
able to build and deploy Django-powered Web sites. Specifically, Chapters 1
through 7 are the "core curriculum," Chapters 8 through 11 cover more advanced
Django usage, and Chapter 12 covers deployment. The remaining chapters, 13
through 20, focus on specific Django features and can be read in any order.

The appendixes are for reference. They, along with the free documentation at
http://www.djangoproject.com/, are probably what you'll flip back to occasionally to
recall syntax or find quick synopses of what certain parts of Django do.

Conhecimentos de Programação Requeridos
------------------------------

Os leitores deste livro devem entender o basico da programação procedural e 
orientada a objetos: estruturas de controle (e.x., ``if``, ``while``,
``for``), estruturas de dados (listas, hashes/dicionarios), variáveis, classes
e objetos.

Experiência em desenvolvimento web é, como você espera, de grande ajuda, mas 
não é necessária para entender este livro. Ao longo do livro, tentaremos mostrar
as melhores praticas em desenvolvimento Web para os leitores que não tem essa 
experiência.

Required Python Knowledge
-------------------------

At its core, Django is simply a collection of libraries written in the Python
programming language. To develop a site using Django, you write Python code
that uses these libraries. Learning Django, then, is a matter of learning how
to program in Python and understanding how the Django libraries work.

If you have experience programming in Python, you should have no trouble diving
in. By and large, the Django code doesn't perform a lot of "magic" (i.e.,
programming trickery whose implementation is difficult to explain or
understand). For you, learning Django will be a matter of learning Django's
conventions and APIs.

If you don't have experience programming in Python, you're in for a treat.
It's easy to learn and a joy to use! Although this book doesn't include a full
Python tutorial, it highlights Python features and functionality where
appropriate, particularly when code doesn't immediately make sense. Still, we
recommend you read the official Python tutorial, available online at
http://docs.python.org/tut/. We also recommend Mark Pilgrim's free book
*Dive Into Python*, available at http://www.diveintopython.net/ and published in
print by Apress.

Required Django Version
-----------------------

This book covers Django 1.4.

Django's developers maintain backwards compatibility as much as possible, but
occasionally introduce some backwards incompatible changes.  The changes in each
release are always covered in the release notes, which you can find here:
https://docs.djangoproject.com/en/dev/releases/1.X


Getting Help
------------

One of the greatest benefits of Django is its kind and helpful user community.
For help with any aspect of Django -- from installation, to application design,
to database design, to deployment -- feel free to ask questions online.

* The django-users mailing list is where thousands of Django users hang out
  to ask and answer questions. Sign up for free at http://www.djangoproject.com/r/django-users.

* The Django IRC channel is where Django users hang out to chat and help
  each other in real time. Join the fun by logging on to #django on the
  Freenode IRC network.

What's Next
-----------

In :doc:`chapter02`, we'll get started with Django, covering installation and
initial setup.
