# 🧠 Projet d'Analyse de Sentiments Aspectuels avec LLM

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.10+-blue.svg" />
  <img src="https://img.shields.io/badge/LangChain-LLM_Framework-green" />
  <img src="https://img.shields.io/badge/OpenAI-API-orange" />
  <img src="https://img.shields.io/badge/Status-Production-success" />
  <img src="https://img.shields.io/badge/License-MIT-lightgrey" />
</p>


## 📋 Informations Générales

| Élément        | Détail |
|---------------|--------|
| **Titre**     | Analyse de Sentiments Aspectuels sur Avis d'Ordinateurs Portables |
| **Auteur**    | [Votre Nom] |
| **Rôle**      | Ingénieur IA / Data Scientist |
| **Date**      | Mars 2026 |
| **Version**   | 1.0.0 |
| **Statut**    | En production |
| **Dépôt**     |  |

---

## 🎯 Objectif du Projet

  

### 🔍 Le système doit :

- ✔️ Identifier la présence des aspects cibles dans le texte  
- ✔️ Attribuer une polarité (**positive / négative / neutre**) à chaque aspect  
- ✔️ Gérer le **multilinguisme**  
- ✔️ Fournir une sortie structurée au format **JSON**  
- ✔️ Être testable avec différents fournisseurs de **LLM**

---

## 🏗️ Architecture Technique

### ⚙️ Stack Technologique

| Composant        | Technologie                  | Version    |
|------------------|-----------------------------|------------|
| **Langage**      | Python                      | 3.10+      |
| **Framework LLM**| LangChain                   | 0.1.0+     |
| **Tokenization** | tiktoken                    | 0.5.0+     |
| **Fournisseurs** | OpenAI / Ollama / Groq      | -          |
| **Notebook**     | Jupyter                     | -          |
| **Variables d'env** | python-dotenv           | 1.0.0+     |

---

## 📁 Structure du Projet

```bash
Agentic-Project/
├── .env                      # Variables d'environnement (clés API)
├── .gitignore                # Fichiers ignorés par git
├── .python-version           # Version Python utilisée
├── img.png                   # Image test pour analyse vision
├── main.py                   # Script principal
├── pyproject.toml            # Configuration du projet
├── README.md                 # Documentation
├── tp1.ipynb                 # Notebook principal
├── uv.lock                   # Lock file pour les dépendances
└── config.py                 # Configuration centralisée

⚙️ Configuration
🔐 1. Variables d’environnement

Créer un fichier .env à partir de .env.example :
OPENAI_API_KEY=sk-...
GROQ_API_KEY=gsk_...
ENVIRONMENT=development
DEFAULT_MODEL=gpt-4o
DEFAULT_TEMPERATURE=0

📦 2. Dépendances
Package	Version	Description
python-dotenv	>=1.0.0	Chargement des variables d'environnement
tiktoken	>=0.5.0	Tokenizer OpenAI
langchain	>=0.1.0	Framework LLM
langchain-openai	>=0.0.2	Intégration OpenAI
langchain-ollama	>=0.0.1	Intégration Ollama
langchain-groq	>=0.0.1	Intégration Groq
ipython	>=8.0.0	Environnement interactif
jupyter	>=1.0.0	Notebooks

🚀 3. Installation
📥 Cloner le dépôt
git clone 
cd analyse-sentiments-llm

⚡ Installation de uv
Linux / macOS : curl -LsSf https://astral.sh/uv/install.sh | sh
Windows : powershell -c "irm https://astral.sh/uv/install.ps1 | iex"
Créer un environnement virtuel
uv -m venv venv
Linux / Mac : source venv/bin/activate
Windows : venv\Scripts\activate
