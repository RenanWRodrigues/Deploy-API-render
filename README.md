# Deploy-API-render

API simples em **FastAPI** para deploy no **Render**.

## O que essa API faz

- **Endpoint**: `GET /recursos`
- **Resposta**: retorna um número inteiro aleatório (entre 1 e 95)

## Requisitos

- **Python**: 3.12+

## Rodar localmente (Windows / PowerShell)

Crie e ative um ambiente virtual:

```bash
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

Instale as dependências:

```bash
pip install -r requirements.txt
```

Inicie o servidor:

```bash
uvicorn main:servidor --reload
```

Abra no navegador:

- `http://127.0.0.1:8000/recursos`
- `http://127.0.0.1:8000/docs` (Swagger UI)

## Deploy no Render

Crie um serviço **Web Service** apontando para este repositório.

- **Importante (erro do Python 3.14 no Render)**: para evitar build quebrando (ex.: `pydantic_core` compilando Rust), este repo inclui `.python-version` e `render.yaml` para fixar o **Python 3.12**. Se você não usar Blueprint, configure também a variável de ambiente `PYTHON_VERSION=3.12` no painel do Render.

- **Build Command**:

```bash
pip install -r requirements.txt
```

- **Start Command**:

```bash
uvicorn main:servidor --host 0.0.0.0 --port $PORT
```

## Estrutura

- `main.py`: aplicação FastAPI (objeto `servidor`)
- `requirements.txt`: dependências para instalação/Render
