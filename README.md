# Bibliotecas Python para Conexão com Bancos de Dados

## 1. Introdução

Em projetos de desenvolvimento de software, é comum que as aplicações precisem armazenar, consultar, atualizar e excluir informações. Para realizar essas operações, é necessário estabelecer uma comunicação entre a aplicação e um banco de dados.

Na linguagem Python, existem diversas bibliotecas que facilitam essa comunicação. Algumas permitem executar comandos SQL diretamente, enquanto outras oferecem recursos de abstração e mapeamento objeto-relacional (ORM).

Este trabalho apresenta cinco bibliotecas utilizadas para conectar aplicações Python a bancos de dados relacionais: pyodbc, pymssql, psycopg2, SQLAlchemy e sqlite3.

## 2. Objetivo

Pesquisar e comparar bibliotecas Python utilizadas na conexão com bancos de dados, identificando suas finalidades, os bancos de dados compatíveis, suas vantagens, limitações, formas de instalação e exemplos práticos de conexão e consulta.

## 3. Bibliotecas pesquisadas

### 3.1. pyodbc

#### Objetivo principal

A biblioteca pyodbc permite que aplicações Python se conectem a bancos de dados por meio da interface ODBC (Open Database Connectivity). Ela possibilita executar comandos SQL e recuperar os resultados diretamente pela aplicação.

#### Tipo de banco de dados

Pode acessar diferentes bancos de dados que possuam um driver ODBC compatível, como:

* Microsoft SQL Server;
* MySQL;
* PostgreSQL;
* Oracle;
* outros bancos que disponibilizem drivers ODBC.

#### Banco relacional ou não relacional?

É utilizada principalmente para acessar bancos de dados relacionais. Sua compatibilidade depende da existência de um driver ODBC adequado.

#### SQL puro, ORM ou ambos?

A biblioteca trabalha diretamente com SQL. Ela não oferece um ORM próprio, mas pode ser utilizada em conjunto com ferramentas de abstração.

#### Instalação

```bash
pip install pyodbc
```

Além da biblioteca, pode ser necessário instalar e configurar o driver ODBC correspondente ao banco de dados utilizado.

#### Exemplo de conexão

Exemplo utilizando Microsoft SQL Server:

```python
import pyodbc

conexao = pyodbc.connect(
    "DRIVER={ODBC Driver 18 for SQL Server};"
    "SERVER=localhost;"
    "DATABASE=empresa;"
    "UID=usuario;"
    "PWD=senha;"
    "TrustServerCertificate=yes;"
)

print("Conexão realizada com sucesso!")
```

Os valores de servidor, banco, usuário e senha devem ser ajustados conforme o ambiente. O nome do driver também deve corresponder ao driver instalado.

#### Exemplo de consulta SELECT

```python
import pyodbc

conexao = pyodbc.connect(
    "DRIVER={ODBC Driver 18 for SQL Server};"
    "SERVER=localhost;"
    "DATABASE=empresa;"
    "UID=usuario;"
    "PWD=senha;"
    "TrustServerCertificate=yes;"
)

cursor = conexao.cursor()

cursor.execute("SELECT id, nome FROM clientes")

for linha in cursor.fetchall():
    print(linha)

cursor.close()
conexao.close()
```

#### Vantagens

* Permite acessar diferentes bancos por meio de drivers ODBC.
* Possibilita executar comandos SQL diretamente.
* É útil em ambientes corporativos que utilizam ODBC.

#### Limitações

* Depende da instalação e configuração de um driver compatível.
* A configuração da conexão pode variar conforme o sistema operacional e o banco utilizado.
* Não possui recursos próprios de ORM.

#### Cenários de uso

É indicado para aplicações que precisam acessar bancos de dados com suporte a ODBC, especialmente em ambientes corporativos que utilizam Microsoft SQL Server ou outros sistemas compatíveis.

---

### 3.2. pymssql

#### Objetivo principal

A biblioteca pymssql permite que aplicações Python se conectem ao Microsoft SQL Server, possibilitando a execução de comandos SQL e a manipulação dos dados armazenados.

#### Tipo de banco de dados

É voltada principalmente para o Microsoft SQL Server.

#### Banco relacional ou não relacional?

É utilizada para bancos de dados relacionais.

#### SQL puro, ORM ou ambos?

Trabalha diretamente com SQL. Não possui um ORM próprio.

#### Instalação

```bash
pip install pymssql
```

#### Exemplo de conexão

```python
import pymssql

conexao = pymssql.connect(
    server="localhost",
    user="usuario",
    password="senha",
    database="empresa"
)

print("Conexão realizada com sucesso!")
```

Os dados de conexão devem ser substituídos pelos valores correspondentes ao ambiente utilizado.

#### Exemplo de consulta SELECT

```python
import pymssql

conexao = pymssql.connect(
    server="localhost",
    user="usuario",
    password="senha",
    database="empresa"
)

cursor = conexao.cursor()

cursor.execute("SELECT id, nome FROM clientes")

for linha in cursor.fetchall():
    print(linha)

cursor.close()
conexao.close()
```

#### Vantagens

* Possui uma interface simples para executar comandos SQL.
* É direcionada à comunicação com o Microsoft SQL Server.
* Permite consultar e manipular dados por meio de cursores.

#### Limitações

* É específica para o SQL Server, não sendo uma solução geral para diversos bancos.
* Pode exigir atenção à compatibilidade da versão da biblioteca e do ambiente.
* Não oferece recursos próprios de ORM.

#### Cenários de uso

É indicada para aplicações Python que precisam se comunicar diretamente com o Microsoft SQL Server e executar comandos SQL.

---

### 3.3. psycopg2

#### Objetivo principal

A biblioteca psycopg2 permite que aplicações Python se conectem ao PostgreSQL. Ela possibilita executar comandos SQL, recuperar resultados e realizar operações de manipulação de dados.

#### Tipo de banco de dados

É voltada para o PostgreSQL.

#### Banco relacional ou não relacional?

É utilizada para bancos de dados relacionais.

#### SQL puro, ORM ou ambos?

Trabalha diretamente com SQL. Não possui um ORM próprio, mas pode ser utilizada como camada de conexão em aplicações que utilizam outras ferramentas de abstração.

#### Instalação

```bash
pip install psycopg2-binary
```

O pacote `psycopg2-binary` facilita a instalação em ambientes de desenvolvimento. Em determinados ambientes de produção, pode ser preferível instalar o pacote `psycopg2` compilado conforme os requisitos do sistema.

#### Exemplo de conexão

```python
import psycopg2

conexao = psycopg2.connect(
    host="localhost",
    database="empresa",
    user="usuario",
    password="senha",
    port="5432"
)

print("Conexão realizada com sucesso!")
```

#### Exemplo de consulta SELECT

```python
import psycopg2

conexao = psycopg2.connect(
    host="localhost",
    database="empresa",
    user="usuario",
    password="senha",
    port="5432"
)

cursor = conexao.cursor()

cursor.execute("SELECT id, nome FROM clientes")

for linha in cursor.fetchall():
    print(linha)

cursor.close()
conexao.close()
```

#### Vantagens

* Possui integração consolidada com o PostgreSQL.
* Permite executar comandos SQL e utilizar parâmetros nas consultas.
* Oferece recursos para transações e tratamento de erros.

#### Limitações

* É direcionada ao PostgreSQL.
* A conexão depende de um servidor PostgreSQL acessível e corretamente configurado.
* Não possui um ORM próprio.

#### Cenários de uso

É indicada para aplicações Python que utilizam PostgreSQL e precisam executar consultas SQL, inserir informações e realizar outras operações no banco de dados.

---

### 3.4. SQLAlchemy

#### Objetivo principal

O SQLAlchemy é um conjunto de ferramentas Python para trabalhar com bancos de dados relacionais. Ele oferece recursos para executar SQL, construir consultas e mapear tabelas para classes Python por meio de ORM.

#### Tipo de banco de dados

Pode trabalhar com diversos bancos relacionais, dependendo do dialeto e do driver utilizado. Entre eles:

* PostgreSQL;
* MySQL;
* SQLite;
* Microsoft SQL Server;
* Oracle.

#### Banco relacional ou não relacional?

É voltado principalmente para bancos de dados relacionais. Não é um ORM universal para bancos NoSQL.

#### SQL puro, ORM ou ambos?

Oferece ambos:

* **SQLAlchemy Core:** permite construir comandos e expressões SQL utilizando uma camada de abstração.
* **SQLAlchemy ORM:** permite representar tabelas como classes Python e trabalhar com objetos.

#### Instalação

```bash
pip install sqlalchemy
```

Para utilizar SQLite, não é necessário instalar um driver adicional na instalação padrão do Python, pois o módulo sqlite3 já está incluído.

#### Exemplo de conexão

Exemplo utilizando SQLite:

```python
from sqlalchemy import create_engine

engine = create_engine("sqlite:///empresa.db")

with engine.connect() as conexao:
    print("Conexão realizada com sucesso!")
```

Nesse exemplo, o SQLAlchemy cria ou acessa o arquivo `empresa.db`.

#### Exemplo de consulta SELECT

```python
from sqlalchemy import create_engine, text

engine = create_engine("sqlite:///empresa.db")

with engine.connect() as conexao:
    resultado = conexao.execute(
        text("SELECT id, nome FROM clientes")
    )

    for linha in resultado:
        print(linha)
```

A tabela `clientes` precisa existir no banco para que a consulta seja executada.

#### Vantagens

* Permite trabalhar com SQL e ORM.
* Facilita a organização do acesso a dados em aplicações maiores.
* Suporta diferentes bancos relacionais por meio de dialetos e drivers.
* Ajuda a reduzir a dependência de comandos específicos de um único banco em determinadas operações.

#### Limitações

* Possui uma curva de aprendizado maior que bibliotecas mais simples.
* O ORM pode adicionar complexidade quando a aplicação precisa apenas executar consultas pequenas.
* A conexão com determinados bancos exige a instalação de um driver específico.

#### Cenários de uso

É indicada para aplicações que precisam de uma camada organizada de acesso a dados, especialmente sistemas maiores que utilizam modelos de objetos, relacionamentos entre tabelas e possibilidade de trabalhar com diferentes bancos relacionais.

---

### 3.5. sqlite3

#### Objetivo principal

A biblioteca sqlite3 permite que aplicações Python utilizem bancos de dados SQLite. Ela possibilita criar e acessar bancos armazenados em arquivos, executar comandos SQL e manipular informações.

#### Tipo de banco de dados

É utilizada com o SQLite, um banco de dados relacional que normalmente armazena suas informações em um arquivo local.

#### Banco relacional ou não relacional?

É utilizada para bancos de dados relacionais.

#### SQL puro, ORM ou ambos?

Trabalha diretamente com SQL. Não possui um ORM próprio.

#### Instalação

O módulo sqlite3 já faz parte da biblioteca padrão do Python. Portanto, normalmente não é necessário instalar um pacote adicional.

#### Exemplo de conexão

```python
import sqlite3

conexao = sqlite3.connect("empresa.db")

print("Conexão realizada com sucesso!")
```

Se o arquivo `empresa.db` ainda não existir, o SQLite poderá criá-lo automaticamente.

#### Exemplo de consulta SELECT

```python
import sqlite3

conexao = sqlite3.connect("empresa.db")

cursor = conexao.cursor()

cursor.execute("SELECT id, nome FROM clientes")

for linha in cursor.fetchall():
    print(linha)

cursor.close()
conexao.close()
```

A tabela `clientes` precisa existir no arquivo do banco para que a consulta funcione.

#### Vantagens

* Já está incluída na biblioteca padrão do Python.
* Não exige, normalmente, a instalação de um servidor de banco de dados separado.
* É simples de configurar e utilizar.
* É útil para protótipos, testes e aplicações locais.

#### Limitações

* É mais adequada para aplicações que não exigem uma infraestrutura de banco cliente-servidor.
* Pode não atender tão bem a sistemas com muitos acessos concorrentes de escrita.
* O banco é armazenado em arquivo, o que pode exigir planejamento adicional para aplicações distribuídas.

#### Cenários de uso

É indicada para aplicações pequenas, protótipos, testes automatizados, ferramentas locais e projetos que precisam armazenar informações sem administrar um servidor de banco de dados separado.

---

## 4. Comparação entre as bibliotecas

| Biblioteca | Banco de dados principal    | Tipo       | SQL puro      | ORM próprio | Instalação                    |
| ---------- | --------------------------- | ---------- | ------------- | ----------- | ----------------------------- |
| pyodbc     | Bancos com driver ODBC      | Relacional | Sim           | Não         | `pip install pyodbc`          |
| pymssql    | Microsoft SQL Server        | Relacional | Sim           | Não         | `pip install pymssql`         |
| psycopg2   | PostgreSQL                  | Relacional | Sim           | Não         | `pip install psycopg2-binary` |
| SQLAlchemy | Diversos bancos relacionais | Relacional | Sim, por Core | Sim         | `pip install sqlalchemy`      |
| sqlite3    | SQLite                      | Relacional | Sim           | Não         | Já incluído no Python         |

**Observação:** nenhuma das cinco bibliotecas apresentadas tem como finalidade principal fornecer um mapeamento ORM nativo para bancos de dados não relacionais. Todas estão relacionadas ao acesso a bancos relacionais, embora o pyodbc possa alcançar diferentes sistemas por meio de drivers compatíveis.

## 5. Cuidados importantes ao executar consultas

Nos exemplos apresentados, os nomes dos bancos, usuários, senhas e servidores são fictícios e devem ser substituídos pelos dados do ambiente utilizado.

Além disso, a tabela `clientes`, utilizada nas consultas, precisa existir no banco de dados e conter as colunas `id` e `nome`.

Em aplicações reais, recomenda-se utilizar consultas parametrizadas quando houver valores fornecidos pelo usuário. Isso ajuda a evitar problemas como a injeção de SQL.

Exemplo de consulta parametrizada com sqlite3:

```python
import sqlite3

conexao = sqlite3.connect("empresa.db")
cursor = conexao.cursor()

nome_cliente = "Maria"

cursor.execute(
    "SELECT id, nome FROM clientes WHERE nome = ?",
    (nome_cliente,)
)

for linha in cursor.fetchall():
    print(linha)

cursor.close()
conexao.close()
```

Nesse exemplo, o valor é enviado como parâmetro, em vez de ser concatenado diretamente ao comando SQL.

## 6. Conclusão

As bibliotecas pesquisadas apresentam diferentes formas de realizar a comunicação entre aplicações Python e bancos de dados relacionais.

O pyodbc permite acessar bancos que possuem drivers ODBC compatíveis. O pymssql é direcionado ao Microsoft SQL Server, enquanto o psycopg2 oferece integração com PostgreSQL. O SQLAlchemy disponibiliza recursos de construção de consultas e ORM, sendo útil para organizar o acesso a dados em aplicações maiores. Já o sqlite3 oferece uma alternativa simples para trabalhar com bancos SQLite, sem a necessidade habitual de instalar um servidor separado.

Portanto, a escolha da biblioteca depende do banco de dados utilizado, da complexidade da aplicação, da necessidade de utilizar ORM e das características do ambiente em que o sistema será executado.

## 7. Referências

* pyodbc — documentação oficial: https://github.com/mkleehammer/pyodbc
* pymssql — documentação oficial: https://pymssql.readthedocs.io/
* psycopg2 — documentação oficial: https://www.psycopg.org/docs/
* SQLAlchemy — documentação oficial: https://docs.sqlalchemy.org/
* sqlite3 — documentação oficial do Python: https://docs.python.org/3/library/sqlite3.html
