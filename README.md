# 🤖 LLM Benchmark Studio - Analyse Comparative de Modèles de Langage

## 🎯 Sujet & Problématique

**"Développement d'une plateforme comparative unifiée pour l'évaluation et l'analyse multi-plateforme de grands modèles de langage (LLMs) avec capacités multimodales et analyse sémantique avancée"**

Ce projet ingénieux propose une architecture modulaire permettant d'interagir de manière uniforme avec trois écosystèmes majeurs de LLMs : **OpenAI (cloud)**, **Ollama (local)** et **Groq (ultra-rapide)**. L'approche se distingue par :
- L'intégration de capacités **multimodales** (vision par IA, génération d'images)
- Un système d'**analyse de sentiments aspectuels** par prompt engineering avancé
- Une **visualisation token-by-token** pour comprendre le mécanisme de tokenisation
- L'utilisation du **pattern Bridge** via LangChain pour abstraire les différences d'API

## ✨ Fonctionnalités principales

### 🎨 **Gestion de Tokenisation**
- Visualisation détaillée de la segmentation textuelle en tokens
- Compteur précis de tokens avec `tiktoken`
- Support du tokenizer `o200k_base` pour GPT-4o

### 🔄 **Multi-Plateforme LLM**
| Plateforme | Modèle | Avantage |
|------------|--------|----------|
| **OpenAI** | GPT-4o, GPT-5.2 | Cloud, haute capacité |
| **Ollama** | Llama 3.2 | Local, confidentialité |
| **Groq** | GPT-OSS-120B | Ultra-rapide, open source |

### 🖼️ **Capacités Multimodales**
- **Vision par IA** : Analyse d'images encodées en base64
- **Génération d'images** : Binding d'outils pour création d'images haute qualité
- Interface unifiée texte/image dans les conversations

### 📊 **Analyse de Sentiments Aspectuels**
- Extraction multi-aspects (screen, keyboard, pad)
- Classification polarité (positive/négative/neutre)
- Sortie structurée en JSON pour exploitation automatisée
- Gestion intelligente des aspects absents

## 🗂️ Structure du projet
📦 llm-benchmark-studio/
┣ 📂 notebooks/
┃ ┗ 📜 main.ipynb # Notebook principal d'exploration
┣ 📂 src/
┃ ┣ 📜 config.py # Configuration API (variables d'environnement)
┃ ┣ 📜 tokenizer_utils.py # Utilitaires de tokenisation
┃ ┣ 📜 sentiment_analyzer.py # Module d'analyse aspectuelle
┃ ┗ 📜 multimodal_handler.py # Gestion des images et vision
┣ 📂 assets/
┃ ┗ 📜 img.png # Image de test pour la vision
┣ 📜 .env.example # Template des variables d'environnement
┣ 📜 requirements.txt # Dépendances Python
┗ 📜 README.md # Ce fichier


## 🚀 Installation & Lancement

### Prérequis
- Python 3.10+
- [Ollama](https://ollama.ai/) installé et en cours d'exécution (pour les modèles locaux)
- Clés API pour OpenAI et Groq

### Configuration

1. **Cloner le repository**
```bash
git clone https://github.com/Ramadiaw12/agentic_project1
cd llm-benchmark-studio

📚 Exemples d'utilisation
1. Visualisation de tokenisation
python

from tokenizer_utils import tokens_count, visualize_tokens

prompt = "Vous êtes un assistant expert dans l'analyse"
print(f"Nombre de tokens: {tokens_count(prompt)}")
visualize_tokens(prompt)  # Affiche la segmentation token par token

Résultat attendu :
text

Nombre de tokens: 8
Vous| êtes| un| assistant| expert| dans| l'|analyse|

2. Benchmark cross-plateforme
python

from langchain_openai import ChatOpenAI
from langchain_ollama import ChatOllama
from langchain_groq import ChatGroq

models = {
    "OpenAI GPT-4o": ChatOpenAI(model="gpt-4o"),
    "Ollama Llama 3.2": ChatOllama(model="llama3.2"),
    "Groq GPT-OSS": ChatGroq(model="openai/gpt-oss-120b")
}

for name, model in models.items():
    response = model.invoke("Qu'est-ce qu'un agent AI ?")
    print(f"\n=== {name} ===\n{response.content[:200]}...")

3. Analyse d'image par IA vision
python

from multimodal_handler import analyze_image, generate_image

# Analyse d'une image existante
description = analyze_image("assets/screenshot.png")
print(f"L'IA voit : {description}")

# Génération d'une image par IA
generated_img = generate_image("Femme ingénieure informatique dans son bureau")
display(generated_img)

4. Analyse de sentiments aspectuels
python

from sentiment_analyzer import analyze_aspect_sentiment

review = "J'ai beaucoup aimé l'écran! La souris n'est pas bonne et le clavier ma fih tchah"
result = analyze_aspect_sentiment(review)

print(f"Catégories: {result['category']}")
print(f"Polarités: {result['polarity']}")

Résultat attendu :
json

{
  "category": ["screen", "keyboard", "pad"],
  "polarity": ["positive", "negative", "neutral"]
}

🛠️ Architecture Technique
Design Patterns implémentés

    Bridge Pattern : LangChain agit comme une couche d'abstraction entre notre application et les différentes APIs LLM

    Strategy Pattern : Tokenisation adaptative selon le modèle utilisé (tiktoken pour OpenAI, fallback pour autres)

    Factory Pattern : Initialisation dynamique des clients LLM selon la plateforme choisie

    Prompt Engineering :

        System messages pour contrôler le comportement de l'assistant

        Few-shot prompting dans l'analyse de sentiments

        Structured output avec format JSON

Flux de données
text

┌─────────────┐     ┌──────────────┐     ┌─────────────────┐
│   Prompt    │────▶│  Tokenizer   │────▶│   LLM Bridge    │
│  Utilisateur│     │   (tiktoken) │     │   (LangChain)   │
└─────────────┘     └──────────────┘     └────────┬────────┘
                                                   │
                    ┌──────────────────────────────┼──────────────────────────────┐
                    ▼                              ▼                              ▼
            ┌───────────────┐              ┌──────────────┐              ┌─────────────┐
            │  OpenAI Cloud │              │ Ollama Local │              │  Groq Ultra │
            │   (GPT-4o)    │              │  (Llama 3.2) │              │   (120B)    │
            └───────┬───────┘              └──────┬───────┘              └──────┬──────┘
                    │                              │                              │
                    └──────────────────────────────┼──────────────────────────────┘
                                                   ▼
                                          ┌─────────────────┐
                                          │  Post-processing│
                                          │ • JSON parsing  │
                                          │ • Image decode  │
                                          │ • Visualisation │
                                          └─────────────────┘

📈 Résultats & Comparaisons
Critère	GPT-4o (OpenAI)	Llama 3.2 (Ollama)	GPT-OSS (Groq)
Latence	~2s	~3s (dépend hardware)	~0.5s
Coût	Payant	Gratuit (local)	Payant (volume)
Confidentialité	Données cloud	Données locales	Données cloud
Multimodal	✅ Vision + Génération	❌	❌
Tokenisation	tiktoken	Propriétaire	Propriétaire
🚧 Axes d'amélioration envisagés

    Système de cache intelligent : Mettre en cache les réponses fréquentes pour réduire coûts/latence

    Benchmark automatisé : Métriques objectives (BLEU, ROUGE) pour évaluer qualité des réponses

    Fine-tuning : Adapter un modèle local avec des données spécifiques au domaine

    Interface Streamlit : Remplacer Jupyter par une application web interactive

    Support multimodal étendu : Ajouter analyse vidéo et audio

    Base de données vectorielle : RAG (Retrieval-Augmented Generation) pour contexte enrichi

    Monitoring temps réel : Dashboard des coûts API et temps de réponse

    Pipeline CI/CD : Tests automatisés des prompts et validation des sorties JSON

📦 Dépendances principales
python

# requirements.txt
langchain>=0.1.0
langchain-openai>=0.1.0
langchain-groq>=0.1.0
langchain-ollama>=0.1.0
tiktoken>=0.5.0
python-dotenv>=1.0.0
jupyter>=1.0.0
ipython>=8.0.0
pillow>=10.0.0  # Pour traitement d'images

🔐 Sécurité & Bonnes pratiques

    Les clés API sont stockées dans .env (ignoré par git)

    Validation des entrées avant envoi aux modèles

    Gestion des erreurs avec try/except pour résilience

    Rate limiting implicite via la gestion des tokens

📖 Références

    LangChain Documentation

    OpenAI API

    Groq Documentation

    Ollama Models

    tiktoken - OpenAI Tokenizer

👨‍💻 Auteur : DIAWANE Ramatoulaye
📅 Date : Mars 2026
🎓 Projet : Benchmark et Analyse de Modèles de Langage

Ce projet démontre une maîtrise avancée des LLMs, de l'ingénierie des prompts, et de l'intégration multi-plateforme, avec une approche pragmatique et orientée résultats.
