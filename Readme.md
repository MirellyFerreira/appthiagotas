---
## 🧩 **Importância do Padrão MVC**

O padrão **MVC (Model-View-Controller)** é uma forma de **organizar o código** em três camadas distintas, separando claramente as responsabilidades:

### 🔹 Model (Modelo)
- Lida com os **dados** e **regras de negócio**.
- Exemplo: acesso a banco de dados, validação, manipulação de dados.

### 🔹 View (Visão)
- Responsável pela **interface** com o usuário.
- Exemplo: HTML renderizado, resposta JSON para APIs.

### 🔹 Controller (Controlador)
- Atua como um **intermediário** entre Model e View.
- Interpreta as requisições do usuário e decide o que fazer com elas.

### ✅ **Por que é importante?**
- **Organização do código**: facilita leitura e manutenção.
- **Separação de responsabilidades**: cada parte tem uma função bem definida.
- **Escalabilidade**: fica mais fácil adicionar novas funcionalidades.
- **Facilidade para trabalhar em equipe**: front-end e back-end podem atuar em camadas diferentes.
- **Facilidade para testar**: lógica de negócio isolada em Models permite testes mais fáceis.

---

## 🛠️ **Instruções para Inicializar um Projeto Node.js com Padrão MVC**

### 📦 1. Pré-requisitos
- Ter o **Node.js** instalado.
- Ter um editor de código (como **VS Code**) e o terminal.

---

### 📁 2. Estrutura do Projeto

```
meu-projeto-mvc/
├── controllers/
│   └── produtoController.js
├── models/
│   └── produtoModel.js
├── views/
│   └── index.html (opcional)
├── routes/
│   └── produtoRoutes.js
├── app.js
└── package.json
```

---

### 🚧 3. Passo a Passo para Iniciar o Projeto

#### a) Crie o projeto e instale dependências

```bash
mkdir meu-projeto-mvc
cd meu-projeto-mvc
npm init -y
npm install express
```

---

#### b) Crie os arquivos com os seguintes conteúdos:

##### `app.js`

```js
const express = require('express');
const app = express();
const produtoRoutes = require('./routes/produtoRoutes');

app.use(express.json());
app.use('/produtos', produtoRoutes);

app.listen(3000, () => {
    console.log('Servidor rodando em http://localhost:3000');
});
```

---

##### `models/produtoModel.js`

```js
let produtos = [];

module.exports = {
    listarTodos: () => produtos,
    adicionar: (produto) => {
        produtos.push(produto);
        return produto;
    }
};
```

---

##### `controllers/produtoController.js`

```js
const Produto = require('../models/produtoModel');

exports.listar = (req, res) => {
    res.json(Produto.listarTodos());
};

exports.adicionar = (req, res) => {
    const novoProduto = req.body;
    const produto = Produto.adicionar(novoProduto);
    res.status(201).json(produto);
};
```

---

##### `routes/produtoRoutes.js`

```js
const express = require('express');
const router = express.Router();
const produtoController = require('../controllers/produtoController');

router.get('/', produtoController.listar);
router.post('/', produtoController.adicionar);

module.exports = router;
```

---

##### (opcional) `views/index.html`

```html
<!DOCTYPE html>
<html>
<head>
    <title>Produtos</title>
</head>
<body>
    <h1>Bem-vindo ao sistema de produtos</h1>
</body>
</html>
```

---

### ▶️ 4. Execute o servidor

```bash
node app.js
```

Acesse no navegador ou em ferramentas como Postman:
- **GET:** `http://localhost:3000/produtos`
- **POST:** `http://localhost:3000/produtos`

Exemplo de POST usando `curl`:
```bash
curl -X POST http://localhost:3000/produtos -H "Content-Type: application/json" -d '{"nome":"Mouse","preco":80}'
```

---

