###DESAFIO PYTHON

# Sistema de Coleta de Dados de Fóruns de Discussão

## Descrição

Este projeto implementa um sistema de coleta e armazenamento de dados de um fórum de discussões. O sistema utiliza **web scraping** para coletar dados de um post, incluindo informações sobre o post original, suas respostas e comentários, e armazena esses dados em um banco de dados **MongoDB**.

## Funcionalidades

- Coleta de dados do post, incluindo:
  - Título do post
  - Conteúdo do post
  - Autor do post
  - Data do post
  - URL do post
  - Respostas
  - Comentários nas respostas
- Armazenamento de dados em um banco de dados **MongoDB**.
- Recuperação de dados do banco de dados usando diferentes métodos de consulta.

## Instalação

### Requisitos

1. Python 3.x
2. MongoDB instalado e rodando no seu sistema (ou você pode usar um MongoDB em nuvem, como o Atlas).

### Instalar dependências

Clone o repositório e instale as dependências necessárias:

```bash
git clone <URL_do_repositório>
cd <diretório_do_repositório>
pip install -r requirements.txt
```

Crie um arquivo `requirements.txt` com as seguintes dependências:

```txt
requests
beautifulsoup4
pymongo
```

Ou instale diretamente usando:

```bash
pip install requests beautifulsoup4 pymongo
```

### Configuração do MongoDB

Certifique-se de que o MongoDB está rodando no seu sistema, ou configure a URL de conexão com o MongoDB no código para usar uma instância na nuvem (como MongoDB Atlas).

```python
client = MongoClient('mongodb://localhost:27017/')  # URL do MongoDB local
# ou
client = MongoClient('<URL_de_Conexão_do_Atlas>')
```

## Como Usar

1. **Rodando o Script de Coleta**

O código principal para coletar os dados de um fórum está no arquivo `main.py`. Basta rodá-lo passando a URL de um post de fórum:

```bash
python main.py
```

2. **Estrutura de Dados Coletados**

O sistema coleta os seguintes dados de cada post:

- **Post**:
  - Título
  - Conteúdo
  - Autor
  - Data do Post
  - URL
  - Respostas:
    - Autor da Resposta
    - Conteúdo da Resposta
    - Comentários na Resposta:
      - Autor do Comentário
      - Conteúdo do Comentário
      - Data do Comentário
      - Quantidade de Reações

3. **Consultas no MongoDB**

Depois de coletar os dados e armazená-los no banco de dados, você pode fazer consultas no MongoDB. Aqui estão três formas de consulta possíveis:

- **Consulta 1: Recuperar todos os posts armazenados**
  
```python
# Recupera todos os posts
posts = posts_collection.find()
for post in posts:
    print(post)
```

- **Consulta 2: Recuperar posts de um usuário específico**

```python
# Recupera posts de um usuário específico
usuario_posts = posts_collection.find({"usuario": "nome_do_usuario"})
for post in usuario_posts:
    print(post)
```

- **Consulta 3: Recuperar posts com um título específico**

```python
# Recupera posts com um título específico
titulo_posts = posts_collection.find({"titulo_post": "Título do post"})
for post in titulo_posts:
    print(post)
```

## Modelagem dos Dados no MongoDB

O banco de dados **MongoDB** foi escolhido devido à flexibilidade no armazenamento de dados não estruturados e à capacidade de escalar horizontalmente. A modelagem dos dados foi feita utilizando coleções para armazenar os posts e suas respectivas respostas e comentários.

### Estrutura da Coleção `posts`

Cada documento na coleção `posts` contém os seguintes campos:

- `data_coleta`: Data e hora da coleta dos dados.
- `url_post`: URL do post no fórum.
- `data_post`: Data do post original.
- `usuario`: Usuário que criou o post.
- `titulo_post`: Título do post.
- `conteudo_post`: Conteúdo do post.
- `respostas`: Lista de respostas, cada uma com:
  - `autor_resposta`: Autor da resposta.
  - `conteudo_resposta`: Conteúdo da resposta.
  - `data_resposta`: Data da resposta.
  - `comentarios`: Lista de comentários, cada um com:
    - `autor_comentario`: Autor do comentário.
    - `conteudo_comentario`: Conteúdo do comentário.
    - `data_comentario`: Data do comentário.
    - `quantidade_reacoes`: Número de reações ao comentário.

## Considerações Finais

O sistema de coleta foi implementado com foco na simplicidade e eficiência, utilizando **BeautifulSoup** para scraping e **MongoDB** para armazenamento. O próximo passo será analisar os dados coletados, utilizando **análise de sentimentos** e outras técnicas de **NLP** para prever tendências de comportamento e interações em fóruns de discussão.

