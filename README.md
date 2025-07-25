# Flipkart Product Recommender System

A small RAG-based chatbot that answers product-related questions using Flipkart product reviews. The project uses LangChain with Groq’s Llama model, AstraDB for vector storage, and a Flask web UI. Prometheus and Grafana provide monitoring options.

## Features
- Converts Flipkart review data into vector embeddings (`flipkart/data_converter.py`)
- Stores embeddings in Astra DB (`flipkart/data_ingestion.py`)
- Retrieval Augmented Generation chain built with LangChain (`flipkart/rag_chain.py`)
- Flask UI (`app.py` and `templates/index.html`)
- Prometheus metrics exposed at `/metrics`
- Dockerfile and Kubernetes manifests for deployment
- Optional Grafana/Prometheus monitoring

## Requirements
- Python 3.10
- Dependencies listed in `requirements.txt`:
  - langchain
  - langchain-astradb
  - langchain-huggingface
  - langchain-groq
  - langchain-community
  - datasets, pypdf, pandas, flask, prometheus_client

## Environment Variables
Create a `.env` file or supply the following variables:
```
ASTRA_DB_API_ENDPOINT=...
ASTRA_DB_APPLICATION_TOKEN=...
ASTRA_DB_KEYSPACE=...
GROQ_API_KEY=...
```

## Running Locally
1. Install dependencies:
   ```bash
   pip install -e .
   ```
2. Ensure `.env` contains the above variables.
3. Start the Flask app:
   ```bash
   python app.py
   ```
4. Open `http://localhost:5000` to chat with the bot. Metrics are available at `http://localhost:5000/metrics`.

## Docker
Build and run:
```bash
docker build -t flask-app .
docker run -p 5000:5000 flask-app
```

## Kubernetes
Deploy with:
```bash
kubectl apply -f flask-deployment.yaml
kubectl apply -f prometheus/
kubectl apply -f grafana/
```

## Monitoring
Prometheus scrapes `/metrics` from the Flask service. Grafana can visualize these metrics.

## License
MIT License – see `LICENSE` for details.
