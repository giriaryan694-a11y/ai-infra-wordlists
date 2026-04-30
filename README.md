# 🧠 AI Infrastructure Wordlists

A curated, high-signal collection of wordlists specifically built for **AI/ML infrastructure reconnaissance**.

This repo is designed for red-teamers, bug bounty hunters, and security researchers targeting **modern AI stacks** — not legacy web apps.

---

## 🚀 Why This Exists

Traditional wordlists (like SecLists) are:

* Focused on web apps (admin panels, CMS, etc.)
* Blind to AI-specific infrastructure

Modern targets expose:

* Model inference APIs
* Pipeline orchestration systems
* Vector databases (RAG backends)
* Experiment tracking platforms

👉 This repo fills that gap.

---

## 🧩 AI Attack Surface Layers

Understanding where these wordlists fit is key:

### 1. Model Serving Layer

* Triton, TensorFlow Serving, TorchServe, vLLM, Ollama
* Exposes inference APIs (`/predict`, `/infer`, `/v1/models`)

### 2. Pipeline & Orchestration

* Kubeflow, Airflow, Ray
* Controls jobs, pipelines, distributed workloads

### 3. Data & Vector Storage

* Qdrant, Weaviate, Milvus, Chroma
* Stores embeddings → critical for RAG data leakage

### 4. Experiment & Model Lifecycle

* MLflow, SageMaker
* Tracks runs, artifacts, deployed models

### 5. Dev & Interactive Environments

* Jupyter
* Often leads to **direct code execution**

### 6. Object Storage

* MinIO
* Stores datasets, model artifacts, backups

---

## 📂 Wordlists Overview

Each file targets a **specific AI component** with high-probability endpoints.

| File            | Target     | What You’re Looking For |
| --------------- | ---------- | ----------------------- |
| airflow.txt     | Airflow    | DAGs, scheduler APIs    |
| bentoml.txt     | BentoML    | Health + model APIs     |
| chroma.txt      | Chroma     | Vector collections      |
| kserve.txt      | KServe     | Inference + health      |
| jupyter.txt     | Jupyter    | Kernels, notebooks      |
| kubeflow.txt    | Kubeflow   | Pipelines, runs         |
| milvus.txt      | Milvus     | Vector DB endpoints     |
| minio.txt       | MinIO      | Buckets, console        |
| mlflow.txt      | MLflow     | Experiments, runs       |
| ollama.txt      | Ollama     | Local LLM APIs          |
| weaviate.txt    | Weaviate   | Schema + GraphQL        |
| vllm_openai.txt | vLLM       | OpenAI-compatible APIs  |
| triton.txt      | Triton     | Model inference         |
| torchserve.txt  | TorchServe | Model serving           |
| tfserving.txt   | TF Serving | Model endpoints         |
| seldon.txt      | Seldon     | Kubernetes inference    |
| sagemaker.txt   | SageMaker  | Managed inference       |
| ray.txt         | Ray        | Jobs + cluster APIs     |
| qdrant.txt      | Qdrant     | Collections             |

---

## 📦 All-in-One Wordlist

### `all-in-one.txt`

* Merges all component-specific lists
* Optimized for quick scanning
* Best for **initial recon sweeps**

---

## ⚡ Usage

### FFUF

```bash
ffuf -u http://target/FUZZ -w all-in-one.txt
```

### Gobuster

```bash
gobuster dir -u http://target -w all-in-one.txt
```

### Feroxbuster

```bash
feroxbuster -u http://target -w all-in-one.txt
```

---

## 🎯 Pro Tips (Real-World Recon)

### 1. Scan Common AI Ports

```
8000, 8080, 8265, 8501, 9000, 6333, 11434
```

### 2. Try POST Requests

Many AI endpoints **don’t respond to GET**

```bash
ffuf -u http://target/FUZZ -w list.txt -X POST
```

### 3. Hunt These First

* `/metrics` → leaks internal architecture
* `/models` → enumerate deployed models
* `/collections` → vector DB data
* `/api/jobs` → potential RCE
* `/lab` → Jupyter access

---

## 🔥 Common Misconfigs You’ll Find

* Exposed Jupyter → **Remote Code Execution**
* Open MLflow → **artifact/data leakage**
* Public vector DB → **embedding exfiltration**
* Ray dashboard → **cluster takeover**
* Open inference APIs → **prompt injection / abuse**

---

## ⚠️ Notes

* Placeholders (e.g., `<model>`) are removed for fuzzing compatibility
* Lists are **curated, not bloated** → high signal over noise
* Designed for **authorized testing only**

---

## 🧠 Roadmap

* [ ] Add GenAI agent frameworks (LangChain, LlamaIndex)
* [ ] Add cloud-specific AI endpoints (Azure ML, Vertex AI)
* [ ] Add GraphQL-specific wordlists
* [ ] Add wordlist scoring (confidence levels)

---

## 🤝 Contributing

Got a new AI infra surface?

* Add a new `<component>.txt`
* Keep it clean (no placeholders)
* Prefer real-world observed endpoints

---

## 🧬 Final Thought

AI infrastructure is the new attack surface.

Most defenders don’t even know it exists yet.

That’s your edge.
