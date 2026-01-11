# DataTrust API

**DataTrust API** é uma plataforma de **engenharia de dados** que valida, governa e expõe dados confiáveis como **Data Products**, utilizando **FastAPI** como camada de consumo.

O projeto foi desenhado para representar um cenário **real de mercado**, cobrindo ingestão, qualidade de dados, transformação e entrega via API — indo muito além de um CRUD.

---

## 🎯 Objetivo do Projeto

Demonstrar, de forma prática, habilidades essenciais de uma **Engenheira de Dados**, incluindo:

* Ingestão de dados de fontes públicas confiáveis
* Validação automática de qualidade de dados
* Criação de camadas de dados (raw → trusted)
* Governança básica e versionamento
* Exposição de dados tratados via FastAPI
* Estrutura pronta para escalar para Lakehouse / Data Mesh

---

## 🧠 Problema de Negócio

Em ambientes corporativos, dados frequentemente entram no Data Lake sem validação, resultando em:

* Dashboards inconsistentes
* Quebras de pipeline
* Falta de confiança nos dados
* Retrabalho constante

O **DataTrust API** resolve esse problema ao garantir que **apenas dados validados e confiáveis** sejam consumidos por BI, aplicações ou modelos de Machine Learning.

---

## 📊 Fonte de Dados

**Washington State Department of Labor & Industries**
Dataset público sobre acidentes de trabalho nos Estados Unidos.

Características:

* Dados reais
* Fonte governamental norte-americana
* Atualização periódica
* Estrutura adequada para análises analíticas

> A fonte é amplamente utilizada em estudos públicos e projetos de análise de dados nos EUA.

---

## 🏗️ Arquitetura Geral

```
[ Fonte Pública (EUA) ]
        |
        v
[ Ingestão - Raw Layer ]
        |
        v
[ Data Quality - Great Expectations ]
        |
        v
[ Trusted Layer - PostgreSQL ]
        |
        v
[ FastAPI - Data Product ]
```

---

## 🔧 Stack Tecnológica

### Backend & Dados

* Python 3.11
* FastAPI
* PostgreSQL
* SQLAlchemy
* Pydantic

### Engenharia de Dados

* Pandas
* Great Expectations
* Docker & Docker Compose

### Observações

* A arquitetura é **Spark-ready** e pode ser facilmente migrada para **Databricks / Delta Lake**.

---

## 📂 Estrutura do Projeto

```
data-trust-api/
│
├── ingestion/
│   └── load_raw.py
│
├── quality/
│   └── expectations.py
│
├── transformations/
│   └── trusted_layer.py
│
├── api/
│   ├── routers/
│   ├── schemas/
│   ├── services/
│   └── main.py
│
├── db/
├── tests/
├── docker-compose.yml
└── README.md
```

---

## 🔄 Pipeline de Dados

### 1️⃣ Ingestão (Raw Layer)

* Coleta de dados via download automatizado
* Persistência dos dados brutos
* Nenhuma transformação aplicada

Execução:

```bash
python ingestion/load_raw.py
```

---

### 2️⃣ Data Quality

Validações automáticas utilizando **Great Expectations**:

* Validação de schema
* Percentual máximo de valores nulos
* Verificação de duplicidade
* Validação de ranges (datas, IDs)

Resultado das validações:

| dataset | total_rows | failed_rules | quality_score |
| ------- | ---------- | ------------ | ------------- |

Esses metadados ficam disponíveis para consumo via API.

---

### 3️⃣ Transformações (Trusted Layer)

* Limpeza de dados
* Normalização de colunas
* Criação de agregações analíticas

Exemplos:

* Acidentes por ano
* Acidentes por setor industrial

---

## 🚀 FastAPI como Data Product

A API expõe **dados prontos para consumo**, com contratos bem definidos.

### Principais Endpoints

```http
GET /v1/accidents/summary?year=2023
GET /v1/accidents/by-industry
GET /v1/quality/latest
GET /health
```

Características:

* Versionamento da API
* Contratos via Pydantic
* Separação clara entre camada de serviço e roteamento

---

## 🛡️ Governança e Boas Práticas

* Versionamento de dados e API
* Contratos explícitos de dados
* Logs de execução
* Healthcheck para observabilidade

---

## 🧪 Testes

* Testes unitários para regras de qualidade
* Testes de contrato da API

---

## 📈 Possíveis Evoluções

* Autenticação JWT
* Cache com Redis
* Airflow / Prefect para orquestração
* Métricas com Prometheus + Grafana
* Delta Lake e arquitetura Lakehouse
* Implementação de conceitos de Data Mesh

---

## 👩‍💻 Autora

**Gabriela (Zuppardo)**
Engenheira de Dados

Projeto desenvolvido com foco em **engenharia de dados moderna**, **governança** e **entrega de valor via dados**.

---

## 📌 Observação Final

Este projeto foi construído com foco em **cenários reais de mercado**, priorizando clareza arquitetural, boas práticas e escalabilidade, sendo ideal para demonstração técnica em processos seletivos de Engenharia de Dados.
