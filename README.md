# Banco-de-dados-Inicial-

from sqlalchemy import create_engine, Colum, String, Integer, Boolean, Foreignkey
from sqlalchemy import sessionmaker, declarative_base   

db = create_engine("sqlite:///meubanco.db")
Session = sessionmaker(bind=db)
session = Session()


Base = declarative_base()

# as tabelas
class Usuario(Base):
    __tablename__ = "usuarios"

    id = Colum("id", Integer, primary_key=True, autoincrement=True)
    nome = Colum("nome", String)
    gmail = Colum("gmail", String)
    senha = Colum("senha", String)
    ativo = Colum("ativo", Boolean)
    def __init__(self, nome, gmail, senha, ativo=True):
        self.nome = nome
        self.gmail = gmail
        self.senha = senha
        self.ativo = ativo

# Livros
class Livro(Base):
    __tablename__ = "livros"

    id = Colum("id", Integer, primary_key=True, autoincrement=True)
    titulo = Colum("titulo", String)
    qtde_paginas = Colum("qtde_paginas", Integer)
    dono = Colum("dono", Foreignkey("usuarios.id"))

    def __init__(self, titulo, qtde_paginas, dono):
        self.id = id
        self.titulo = titulo
        self.qtde_paginas = qtde_paginas
        self.dono = dono



Base.metadata.create_all(bind=db)

#CRUD

usuario = Usuario(nome="Thamyres", gmail="thamy.rms@gmail.com", senha="Thamyres123")
session.add(usuario)
session.commit()
