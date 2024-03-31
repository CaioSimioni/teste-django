# Projeto de Cadastro de Usuários

Vídeo original: [DJANGO - Como criar um sistema de cadastro do zero!](https://youtu.be/-m5ywU8SW9E?si=oQPDXJPUFNoZpR6U)

# Índece

1. [Conceito básico](#01-basico)


<div id="Básico" />

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