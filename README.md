🔐 Flask User Auth API

Uma API simples de autenticação e gerenciamento de usuários desenvolvida com Flask, Flask-Login e SQLAlchemy.
Permite criar, autenticar, atualizar e excluir usuários, com suporte a papéis (roles) e proteção de rotas via login.

🚀 Tecnologias utilizadas

🐍 Python 3.10+

🌶️ Flask

🧩 Flask-Login

🧱 Flask SQLAlchemy

🧂 bcrypt (para hash de senha)

🐬 MySQL (banco de dados)


📁 Estrutura do projeto
project/
│
├── app.py
├── models/
│   └── user.py
├── database.py
└── requirements.txt


⚙️ Configuração e execução

1️⃣ Clonar o repositório
git clone https://github.com/seu-usuario/flask-user-auth.git
cd flask-user-auth

2️⃣ Criar e ativar ambiente virtual
python -m venv venv
source venv/bin/activate # Linux/Mac
venv\Scripts\activate  # Windows

3️⃣ Instalar dependências
pip install flask flask_sqlalchemy flask_login bcrypt pymysql
(ou, se tiver um arquivo requirements.txt)
pip install -r requirements.txt

4️⃣ Configurar banco de dados
Edite a URI de conexão em app.py:
app.config['SQLALCHEMY_DATABASE_URI'] = 'mysql+pymysql://usuario:senha@localhost:3306/flask-crud'

Depois, inicialize o banco:

from app import db, app
with app.app_context():
    db.create_all()


🔑 Rotas da API
Método	Endpoint	Descrição	Autenticação
POST	/user	Cria um novo usuário	❌
POST	/login	Realiza login e autentica o usuário	❌
GET	/logout	Faz logout do usuário logado	✅
GET	/user/<id>	Retorna informações de um usuário específico	✅
PUT	/user/<id>	Atualiza senha do usuário	✅
DELETE	/user/<id>	Deleta um usuário (somente admin)	✅


🧠 Regras de negócio

Apenas usuários autenticados podem acessar rotas protegidas.

Apenas admins podem deletar outros usuários.

Um usuário não pode se auto-deletar.

Usuários comuns podem atualizar apenas a própria senha.

Senhas são armazenadas com bcrypt hash.


🧍‍♂️ Modelo User
class User(db.Model, UserMixin):
    id = db.Column(db.Integer, primary_key=True)
    username = db.Column(db.String(80), nullable=False, unique=True)
    password = db.Column(db.String(80), nullable=False)
    role = db.Column(db.String(80), nullable=False, default='user')


🧪 Testando a API

Use ferramentas como Postman ou Insomnia.

Exemplo de requisição:

POST /user

{
  "username": "admin",
  "password": "123456"
}


POST /login

{
  "username": "admin",
  "password": "123456"
}


Resposta:

{
  "Message": "Autenticação realizada com sucesso!"
}
