# 🧠 Pinecone Semantic Search with Airflow

[![Python](https://img.shields.io/badge/Python-3.10+-blue.svg)](https://www.python.org/)
[![Airflow](https://img.shields.io/badge/Apache%20Airflow-2.7+-brightgreen.svg)](https://airflow.apache.org/)
[![Docker](https://img.shields.io/badge/Docker-Compose-blue.svg)](https://www.docker.com/)
[![Pinecone](https://img.shields.io/badge/Pinecone-Vector%20DB-orange.svg)](https://www.pinecone.io/)
[![License](https://img.shields.io/badge/License-Academic-lightgrey.svg)](LICENSE)

> 🚀 End-to-end **Semantic Search Engine** powered by **Sentence Transformers**, **Pinecone Vector Database**, and **Apache Airflow** — all containerized with **Docker Compose**.

---

## 📚 Table of Contents

- [🧭 Overview](#-overview)
- [🧩 Technologies Used](#-technologies-used)
- [📁 Project Structure](#-project-structure)
- [⚙️ Setup Instructions](#️-setup-instructions)
- [🧠 DAG Workflow](#-dag-workflow)
- [🧪 Running the Pipeline](#-running-the-pipeline)
- [🔍 Troubleshooting](#-troubleshooting)
- [📚 References](#-references)
- [👨‍🎓 Author & Course Info](#-author--course-info)
- [📜 License](#-license)

---

## 🧭 Overview

This project implements an **end-to-end data pipeline** that performs **semantic search** over text data.  
Using **Sentence Transformers** for embedding and **Pinecone** for vector storage, it allows you to search semantically similar texts.

The entire process is orchestrated by **Apache Airflow** and deployed using **Docker Compose**.

### ✅ Pipeline Tasks

1. **Download Dataset** (Medium articles)
2. **Preprocess & Clean Text**
3. **Create or Reset Pinecone Index**
4. **Generate Sentence Embeddings**
5. **Upsert Vectors to Pinecone**
6. **Run Search Query** – e.g., *"What is ethics in AI?"*

---

## 🧩 Technologies Used

| Technology | Purpose |
|-------------|----------|
| 🐍 **Python** | Core scripting language |
| 🧾 **Apache Airflow** | Workflow orchestration |
| 🐳 **Docker Compose** | Containerized setup for Airflow |
| 🌲 **Pinecone Vector DB** | Vector storage & similarity search |
| 🧠 **Sentence Transformers** | Generate dense text embeddings |
| 📦 **Requests / Pandas** | Data ingestion & manipulation |

---

## 📁 Project Structure

```
Pinecone-Search-Engine/
├── dags/
│   └── pinecone_search_dag.py     # Main Airflow DAG pipeline
├── docker-compose.yaml            # Airflow + dependencies setup
├── README.md                      # Project documentation (this file)
└── requirements.txt (optional)    # Python dependencies (if used)
```

---

## ⚙️ Setup Instructions

### 1️⃣ Clone the Repository
```bash
git clone https://github.com/pateldhruv1672/Pinecone-Search-Engine.git
cd Pinecone-Search-Engine
```

### 2️⃣ Configure Docker Compose
In your `docker-compose.yaml`, ensure the image includes:
```yaml
sentence-transformers
pinecone-client
```

Rebuild the containers:
```bash
docker compose down
docker compose up -d --build
```

### 3️⃣ Configure Pinecone in Airflow
1. Get your API key from [Pinecone Console](https://www.pinecone.io/).
2. Open Airflow UI → **Admin → Variables**
3. Add a new variable:
   - **Key:** `pinecone_api_key`
   - **Value:** `<YOUR_API_KEY>`

---

## 🧠 DAG Workflow

Each task in the DAG represents a pipeline stage:

| Task Name | Description |
|------------|--------------|
| `download_data()` | Downloads Medium dataset via HTTP |
| `preprocess_data()` | Cleans and prepares text for embedding |
| `create_pinecone_index()` | Initializes Pinecone index (dim=384, metric=dotproduct) |
| `generate_embeddings()` | Uses `all-MiniLM-L6-v2` model for sentence embeddings |
| `upsert_to_pinecone()` | Uploads embeddings + metadata to Pinecone |
| `test_search_query()` | Runs a semantic search to verify results |

---

## 🧪 Running the Pipeline

1. Start Airflow containers:
   ```bash
   docker compose up -d
   ```
2. Visit Airflow UI:  
   👉 [http://localhost:8080](http://localhost:8080)
3. Enable the DAG `pinecone_search_dag`
4. Trigger it manually
5. Monitor logs for search results, e.g.:

```
Search results for query: 'what is ethics in AI'
ID: 201, Score: 0.887, Title: 'Ethics of Artificial Intelligence'
```

---

## 🔍 Troubleshooting

| Issue | Possible Fix |
|--------|---------------|
| ❌ *Index not ready* | Check Pinecone console or API region |
| 🔑 *Invalid API key* | Re-enter Airflow Variable correctly |
| ⚙️ *Dimension mismatch* | Ensure index dimension = 384 |
| 🐳 *Package not found* | Rebuild Docker image with `--build` flag |
| 🌀 *Airflow not starting* | Try `docker compose down && docker compose up -d --build` |

---

## 📚 References

- 📘 [Pinecone Documentation](https://docs.pinecone.io/)
- 🧩 [Sentence Transformers Models](https://www.sbert.net/)
- ⚙️ [Apache Airflow Docs](https://airflow.apache.org/docs/)
- 🐋 [Docker Compose Reference](https://docs.docker.com/compose/)

---

## 👨‍🎓 Author & Course Info

**Name:** Patel Dhruvkumar Kamleshbhai  
**Subject:** DATA 226 – Data Warehousing  
**University:** San José State University  

---

## 📜 License

This repository is created for **academic use** as part of coursework for DATA 226.  
Feel free to reference or adapt for learning purposes.

---

⭐ *If you found this helpful, consider starring the repository on GitHub!* ⭐
