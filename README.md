# Projeto de Cadastro de Usuários



# Índece

1. [Instalação do Django](#instalacao)
2. [Conceito básico](#basico)
3. [Gerando Banco de Dados/Migrations](#bancodados)
4. [To-do list](#todo)
5. [Referências](#referencias)

<div id="instalacao"/>

## Instalação do Django

1. Requisitos
2. Criando projeto
3. Utilizando variáveis de ambiente


<div id="basico" />

## Conceito Básico

Sempre que criamos uma nova página Web precisamos seguir os seguintes passos:

1. Garantir que o `app` que criamos está adicionado ao projeto:
    Vamos no arquivo `projeto/settings.py` e adicionar o `app` aos aplicativos instalados.
    ```python
    ...

    INSTALLED_APPS = [
        'django.contrib.admin',
        'django.contrib.auth',
        'django.contrib.contenttypes',
        'django.contrib.sessions',
        'django.contrib.messages',
        'django.contrib.staticfiles',
        'app'  # Adicionar o app no projeto.
    ]

    ...
    ```

2. Criar o rota para a página no arquivo `projeto/url.py` com o comando:
    ```python
    from django.urls import path
    from app import views  # Importar o arquivo views do meu app

    urlpatterns = [
        path('', views.home, name='home'),  # Criar uma rota passando(Caminho, Função, Nome do caminho)
    ]
    ```

3. Criar a função responsável pela renderização da página no arquivo `app/views.py`, como no exemplo:
    ```python
    def home(request):
        return render(request, 'usuarios/home.hmtl')
    ```

4. Criar o arquivo da página que será exibida dentro da pasta `app/templates/usuario/home.html`. obs: sempre crie sub pastas dentro da pasta templates para separar as diferentes partes do seu app.

<div id="bancodados"/>

## Gerando Banco de Dados/Migrations

1. Primeiro vamos criar a classe dentro do arquivo `app/models.py`
    ```python
    class Usuario(models.Model):
        id_usuario = models.AutoField(primary_key=True)
        nome = models.TextField(max_length=255)
        idade = models.IntegerField()
    ```

2. Para gerar o modelo no banco de dados usamos:
    ```bash
    $ python manage.py migrations

    $ python manage.py migrate
    ```
    Assim teremos a tabela de usuários no banco de dados.

3. Receber as informações dos usuários nos forms, lembrar de usar o CSRF_TOKEN:
    ```html
    <form action="{% url 'listagem_usuarios'%}" method="post">
        {% csrf_token %}
        <div class="container">
            <h1>Cadatro de Usuários</h1>
            Nome:<input type="text" name="nome">
            Idade:<input type="text" name="idade">
            <button type="">Enviar</button>
        </div>
    </form>
    ```

4. Para adicionar um registro no banco de dados:
    ```python
    def listagem_usuarios(request):
        # Instancia da classe usuario
        novo_usuario = Usuario()
        # Recebe as informações do post
        novo_usuario.nome = request.POST.get('nome')
        novo_usuario.idade = request.POST.get('idade')
        # Salva o registro no banco de dados
        novo_usuario.save()
        # Cria variavel usuarios com todos os registros
        usuarios = {
            'usuarios': Usuario.objects.all()
        }
        # Renderiza a página passando 'usuarios' como variavel
        return render(request, 'usuarios/usuarios.html', usuarios)
    ```

5. Para exibir as informações na página usuamos:
    ```html
    {% for usuario in usuarios %}
    <tr>
        <td>{{usuario.id_usuario}}</td>
        <td>{{usuario.nome}}</td>
        <td>{{usuario.idade}}</td>
    </tr>
    {% endfor %}
    ```

<div id="todo" />

## To-do list

- [x] Subir o projeto com o mínimo funcionando.
- [ ] Aprender a utilizar .env para Desenvolvimento/Produção.
- [ ] Alterar o Banco de Dados para MySQL.
- [ ] Encontrar uma melhor forma de estilar as páginas.
- [ ] Implementar os códigos no projeto integrador da faculdade. 

<div id="referencias"/>

## Referências

[DJANGO - Como criar um sistema de cadastro do zero!](https://youtu.be/-m5ywU8SW9E?si=oQPDXJPUFNoZpR6U)
