# 🚀 Mini Tutorial: Criando uma API com Flask

Neste tutorial, você vai aprender a criar uma **API simples** em Flask que trabalha com dados em **JSON**.  
A ideia é mostrar o básico dos métodos **GET, POST, PUT e DELETE**.

---

## 📌 1. Preparando o ambiente
1. Instale o Flask (se ainda não tiver):
   ```bash
   pip install flask
   ```

2. Crie um arquivo chamado **app.py**.

---

## 📌 2. Estrutura básica do Flask
```python
from flask import Flask, jsonify, request

app = Flask(__name__)

# dados fictícios para nossa API
carros = [
    {"id": 1, "marca": "Ford", "modelo": "Fiesta"},
    {"id": 2, "marca": "Chevrolet", "modelo": "Onix"}
]

# rota inicial
@app.route("/")
def home():
    return "🚀 API de Carros funcionando!"
```

---

## 📌 3. Método GET (listar dados)
```python
@app.route("/carros", methods=["GET"])
def listar_carros():
    return jsonify(carros)
```
👉 Acesse no navegador: [http://127.0.0.1:5000/carros](http://127.0.0.1:5000/carros)

---

## 📌 4. Método POST (adicionar dados)
```python
@app.route("/carros", methods=["POST"])
def adicionar_carro():
    novo_carro = request.get_json()
    carros.append(novo_carro)
    return jsonify({"mensagem": "Carro adicionado com sucesso!", "carro": novo_carro})
```

📌 Envie um JSON pelo Postman ou outro cliente HTTP:
```json
{
  "id": 3,
  "marca": "Volkswagen",
  "modelo": "Gol"
}
```

---

## 📌 5. Método PUT (atualizar dados)
```python
@app.route("/carros/<int:id>", methods=["PUT"])
def atualizar_carro(id):
    for carro in carros:
        if carro["id"] == id:
            dados = request.get_json()
            carro.update(dados)
            return jsonify({"mensagem": "Carro atualizado!", "carro": carro})
    return jsonify({"erro": "Carro não encontrado!"}), 404
```

---

## 📌 6. Método DELETE (remover dados)
```python
@app.route("/carros/<int:id>", methods=["DELETE"])
def deletar_carro(id):
    for carro in carros:
        if carro["id"] == id:
            carros.remove(carro)
            return jsonify({"mensagem": "Carro removido!"})
    return jsonify({"erro": "Carro não encontrado!"}), 404
```

---

## 📌 7. Rodando a aplicação
```python
if __name__ == "__main__":
    app.run(debug=True)
```

---

# 🎯 Desafio crie uma API de alunos


👉 Crie uma **API de alunos** usando Flask que atenda os seguintes pontos:

1. Tenha um **GET** para listar todos os alunos.  
2. Tenha um **POST** para adicionar um novo aluno (JSON com `id`, `nome` e `idade`).  
3. Tenha um **PUT** para atualizar os dados de um aluno pelo `id`.  
4. Tenha um **DELETE** para remover um aluno pelo `id`.  


---

✅ Pronto! Você já consegue criar APIs REST simples com Flask.
