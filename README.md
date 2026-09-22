RAG Finance & Banque — Pipeline de Recherche Augmentée

Pipeline RAG (Retrieval-Augmented Generation) appliqué à des documents financiers, avec une architecture pensée pour évoluer vers un système multi-agents.

Objectif

Permettre d'interroger un corpus de documents financiers (rapports, filings) en langage naturel et d'obtenir des réponses ancrées dans les sources, plutôt que générées uniquement à partir des connaissances internes du modèle. L'objectif est de limiter les hallucinations et de rendre les réponses traçables jusqu'au document source.

Dataset

sujet-ai/Sujet-Financial-RAG-EN-Dataset — corpus de paires questions/réponses/contextes extraites de documents financiers réels, conçu spécifiquement pour l'évaluation de systèmes RAG.

Architecture

Le pipeline suit une approche RAG classique en 6 étapes :

Chargement des données — récupération du dataset via la librairie datasets de Hugging Face
Préparation des chunks — extraction des contextes uniques servant de base documentaire
Embeddings — vectorisation des chunks avec sentence-transformers (modèle all-MiniLM-L6-v2)
Indexation vectorielle — stockage des vecteurs dans un index FAISS (recherche par similarité cosinus)
Retrieval — récupération des k passages les plus pertinents pour une question donnée
Génération — synthèse de la réponse par un LLM (via OpenRouter), à partir de la question et des passages récupérés
Stack technique
Composant	Outil
Dataset	Hugging Face datasets
Embeddings	sentence-transformers
Base vectorielle	FAISS
Génération	LLM via OpenRouter (API compatible OpenAI)
Environnement	Google Colab
Évolution prévue : architecture multi-agents

La prochaine itération du projet ajoutera une couche agentique au-dessus du pipeline RAG basique :

Orchestrateur — décide si une requête nécessite du retrieval ou peut être traitée directement
Agents spécialisés — un agent recherche, un agent calcul/analyse, un agent synthèse
Mémoire persistante — conservation du contexte entre les échanges
Suivi du coût en tokens — optimisation des appels au LLM
Utilisation
bash
pip install datasets sentence-transformers faiss-cpu openai

Le notebook rag_banque_pipeline.ipynb contient l'implémentation complète, exécutable directement dans Google Colab sans installation locale.
