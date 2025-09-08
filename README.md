# MCP_FastApi

MCP_FastApi is a professional template for building scalable API backends with [FastAPI](https://fastapi.tiangolo.com/) and a powerful, pluggable MCP (Modular Control Program) command system.

---

## 🚀 Overview

- **Backend:** Python 3.11+, FastAPI, SQLAlchemy, Pydantic
- **MCP:** Register & run dynamic command functions via API
- **Frontend:** Integrate with any client (React, Vue, mobile, etc.) using OpenAPI/Swagger docs
- **Deployment:** Docker-ready, CI-ready, portable

---

## 📁 Directory Structure

```plaintext
MCP_FastApi/
├── app/
│   ├── api/v1/user.py                 # User API endpoints (example)
│   ├── core/config.py                 # App settings/env config
│   ├── core/logger.py                 # Logging setup
│   ├── core/security.py               # JWT auth utils
│   ├── db/base.py                     # SQLAlchemy base
│   ├── db/models.py                   # Example User model
│   ├── main.py                        # FastAPI entrypoint
│   ├── mcp/registry.py                # MCP registry/decorator
│   ├── mcp/commands.py                # Example MCP commands
│   ├── mcp/router.py                  # MCP API router
│   └── services/user_service.py       # User business logic
├── tests/test_user.py                 # Example API tests
├── requirements.txt                   # Python dependencies
├── .env.example                       # Env var template
├── Dockerfile                         # Docker build/run
├── .gitignore                         # Ignore files
├── README.md                          # Project docs (this file)
├── CONTRIBUTING.md                    # Contributing guide
├── docs/architecture.md               # System/extension docs
└── .github/workflows/ci.yml           # GitHub Actions CI
```

---

## 🌐 Backend Details

- **FastAPI** is used for blazing-fast, async Python APIs and auto-generates interactive OpenAPI docs at `/docs`.
- **MCP** (Modular Control Program) lets you add command functions to the backend and call them by name with parameters via API. Example use cases:
    - Custom admin/admin ops (clear cache, stats, batch jobs)
    - Business automation, one-off workflows, or integrations
- **User CRUD**: Example endpoints show how to structure models, services, and routers.
- **Security**: JWT token generation/verification built in (`core/security.py`).
- **Config**: Environment-driven (`core/config.py` + `.env.example`).
- **Docker**: Production-ready image and config.
- **CI/CD**: Example GitHub Actions for tests.

---

## 🖥 Environment/Deployment

- **Python 3.11+** (see `requirements.txt`)
- **.env** file for config (see `.env.example`)
- **Database:** Defaults to SQLite for dev (`DATABASE_URL`), but can use PostgreSQL, MySQL, etc.
- **Docker:** Run everything in a container—production-ready!
- **CI:** Auto-checks with GitHub Actions (`.github/workflows/ci.yml`)

---

## 🧑‍💻 Frontend Integration

- **OpenAPI/Swagger docs:** Visit `/docs` after running to see/call all APIs (great for frontend devs!)
- **Any client:** Easily connect from React, Vue, Angular, Android/iOS, CLI tools, etc.
- **How to call MCP:**  
    - `POST /api/v1/mcp/run` with JSON:
        ```json
        {
          "command": "say_hello",
          "params": {"name": "Anand"}
        }
        ```
    - Response:
        ```json
        {"result": "Hello, Anand!"}
        ```

---

## 🛠️ Quick Start

1. **Clone and enter the repo**
    ```sh
    git clone https://github.com/anandn13/MCP_FastApi.git
    cd MCP_FastApi
    ```
2. **Set up Python environment**
    ```sh
    python3 -m venv venv
    source venv/bin/activate
    pip install -r requirements.txt
    ```
3. **Environment variables**
    ```sh
    cp .env.example .env
    # Edit `.env` as needed
    ```
4. **Run locally**
    ```sh
    uvicorn app.main:app --reload
    ```
5. **Open with your browser**  
    - API: http://localhost:8000/docs

6. **Run in Docker**
    ```sh
    docker build -t mcp_fastapi .
    docker run -p 8000:8000 mcp_fastapi
    ```

7. **Run tests**
    ```sh
    pytest
    ```

---

## 🛡️ How to Extend MCP System

1. **Add a command** to `app/mcp/commands.py`:
    ```python
    @mcp_registry.register("reverse_text")
    def reverse_text(text: str):
        return text[::-1]
    ```
2. **Call it via API**:
    ```http
    POST /api/v1/mcp/run
    {
      "command": "reverse_text",
      "params": {"text": "hello"}
    }
    # -> {"result": "olleh"}
    ```

---

## 🏗️ Architecture

See [`docs/architecture.md`](docs/architecture.md) for diagrams, explanations, and best practices for extending MCP, securing commands, and integrating with real-world production systems.

---

## 🤝 Contributing

See [`CONTRIBUTING.md`](CONTRIBUTING.md)

---

## 📄 License

MIT

---