# 🛰️ SatGuard — Backend

> API REST desenvolvida com Java 17 e Spring Boot 4, consumindo dados reais de terremotos (USGS) e asteroides próximos da Terra (NASA NeoWs). FIAP Global Solution 2026 — Space Connect.

---

## 📋 Índice

- [Sobre](#sobre)
- [Tecnologias](#tecnologias)
- [Pré-requisitos](#pré-requisitos)
- [Como Executar](#como-executar)
- [Endpoints](#endpoints)
- [APIs Externas](#apis-externas)
- [Estrutura](#estrutura)
- [Integrantes](#integrantes)

---

## 📖 Sobre

Backend do SatGuard — plataforma de monitoramento em tempo real de desastres naturais e ameaças espaciais. Consome dados reais da USGS e NASA, persiste no banco H2 e expõe uma API REST para o frontend Angular.

---

## 🛠️ Tecnologias

| Tecnologia | Versão |
|---|---|
| Java | 17 |
| Spring Boot | 4.0.6 |
| Spring Data JPA | — |
| Spring Web | — |
| H2 Database | — |
| Lombok | — |
| Maven | — |

---

## ⚙️ Pré-requisitos

- **Java 17** instalado
  ```bash
  java -version
  ```

> ℹ️ Não é necessário instalar nenhum banco de dados. O H2 roda em memória automaticamente.

---

## 🚀 Como Executar

**1. Clone o repositório:**
```bash
git clone https://github.com/luisbmotta/satguard-api.git
cd satguard-api
```

**2. Execute o projeto:**

Windows:
```bash
./mvnw spring-boot:run
```

Linux/macOS:
```bash
./mvnw spring-boot:run
```

> Na primeira execução o Maven baixa as dependências automaticamente. Aguarde alguns minutos.

**3. Confirme que está rodando:**

Acesse: `http://localhost:8080/api/eventos`

Deve retornar `[]` (lista vazia antes de sincronizar).

**4. Popule o banco com dados reais:**

Windows (PowerShell):
```powershell
Invoke-RestMethod -Method POST -Uri http://localhost:8080/api/eventos/sincronizar
```

Linux/macOS:
```bash
curl -X POST http://localhost:8080/api/eventos/sincronizar
```

Retorno esperado: `Sincronização concluída!`

---

## 🗄️ Console H2

Para visualizar o banco de dados:

1. Acesse: `http://localhost:8080/h2-console`
2. Preencha:
   - **JDBC URL:** `jdbc:h2:mem:satguarddb`
   - **User Name:** `sa`
   - **Password:** *(vazio)*
3. Clique em **Connect**
4. Execute: `SELECT * FROM EVENTOS`

---

## 🔌 Endpoints

Base URL: `http://localhost:8080`

| Método | Endpoint | Descrição |
|---|---|---|
| `GET` | `/api/eventos` | Lista todos os eventos |
| `GET` | `/api/eventos?tipo=TERREMOTO` | Filtra por tipo |
| `GET` | `/api/eventos?tipo=ASTEROIDE` | Filtra por tipo |
| `GET` | `/api/eventos/favoritos` | Lista favoritos |
| `PATCH` | `/api/eventos/{id}/favorito` | Alterna favorito |
| `POST` | `/api/eventos/sincronizar` | Atualiza dados das APIs |

---

## 🌐 APIs Externas

### USGS Earthquake API
- Sem necessidade de chave de API
- URL: `https://earthquake.usgs.gov/fdsnws/event/1/query`
- Dados: terremotos com magnitude ≥ 2.0 na região da América do Sul

### NASA NeoWs API
- Usa `DEMO_KEY` (30 req/hora)
- URL: `https://api.nasa.gov/neo/rest/v1/feed/today`
- Dados: asteroides próximos da Terra com diâmetro e nível de perigo

> Para aumentar o limite da NASA, obtenha uma chave gratuita em [api.nasa.gov](https://api.nasa.gov/) e substitua `DEMO_KEY` em `EventoApiClient.java`.

---

## 📁 Estrutura

```
satguard-api/
├── src/main/java/br/com/satguard/api/
│   ├── controller/
│   │   └── EventoController.java
│   ├── service/
│   │   └── EventoService.java
│   ├── client/
│   │   └── EventoApiClient.java
│   ├── model/
│   │   └── Evento.java
│   ├── repository/
│   │   └── EventoRepository.java
│   └── dto/
│       └── EventoDTO.java
└── src/main/resources/
    └── application.properties
```

---

## ❗ Solução de Problemas

**Backend não inicia:**
- Verifique se Java 17 está instalado: `java -version`
- Use `./mvnw` e não `mvn`
- Verifique se a porta 8080 está livre

**Dados não aparecem:**
- Verifique sua conexão com a internet
- A NASA DEMO_KEY tem limite de 30 req/hora — aguarde antes de sincronizar novamente

---

## 👥 Integrantes

| Nome | RM | Turma |
|---|---|---|
| Luis Fernando de Barros Motta | 95664 | 4SIOA |
| Eduardo Lucca Dias da Costa | 95415 | 4SIOA |

---

*FIAP Global Solution 2026 — Space Connect*
