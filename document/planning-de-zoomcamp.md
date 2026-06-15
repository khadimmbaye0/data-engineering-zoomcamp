# Data Engineering Zoomcamp — Planning détaillé (3 mois)

> **Source** : [DataTalksClub/data-engineering-zoomcamp](https://github.com/khadimmbaye0/data-engineering-zoomcamp) — Cohort 2026  
> **Durée** : 3 mois (12 semaines) — version compressible à 2,5 mois (10 semaines, notes incluses)  
> **Rythme** : ~1h30–2h/jour en semaine, ~3–4h le week-end

---

## Vue d'ensemble — 3 mois

| Mois | Semaines | Modules |
|------|----------|---------|
| **Mois 1** | S1–S4 | Docker & Terraform → Kestra → dlt → BigQuery |
| **Mois 2** | S5–S8 | dbt → Bruin → Spark → Streaming |
| **Mois 3** | S9–S12 | Projet final + peer reviews + tampon |

---

## MOIS 1 — Fondations & Cloud

---

### SEMAINE 1 — Module 1 : Docker, PostgreSQL, Terraform

**Objectif** : Containerisation, infrastructure as code, premier pipeline ETL local.

#### Jour 1 — Introduction & Setup
- [ ] Regarder le [Launch stream](https://www.youtube.com/watch?v=JgspdlKXS-w) (vue d'ensemble du cours, ~30 min)
- [ ] Installer Docker Desktop / Docker Engine sur ta machine
- [ ] Lire le README du Module 1 : `01-docker-terraform/README.md`
- [ ] **Optionnel** : [Pre-launch Q&A](https://www.youtube.com/watch?v=WB6b1lcguaA)

#### Jour 2 — Docker & Postgres
- [ ] Regarder [Docker + Postgres workshop](https://youtu.be/lP8xXebHmuE) (~45 min)
- [ ] Suivre les instructions : `01-docker-terraform/docker-sql/`
- [ ] Lancer Postgres avec Docker, créer une base `ny_taxi`
- [ ] Ingérer les données taxi avec un script Python dans le container

#### Jour 3 — SQL Refresher
- [ ] Regarder [SQL refresher](https://youtu.be/QEcps_iskgg) (~30 min)
- [ ] Exécuter les requêtes : `01-docker-terraform/docker-sql/10-sql-refresher.md`
- [ ] Pratiquer : SELECT, JOIN, GROUP BY, window functions sur les données taxi

#### Jour 4 — Google Cloud Platform
- [ ] Regarder [Introduction à GCP](https://youtu.be/18jIzE41fJ4) (~20 min)
- [ ] Créer un compte GCP (essai gratuit avec $300 de crédits)
- [ ] Créer un projet GCP
- [ ] Installer `gcloud` CLI et s'authentifier
- [ ] Créer un service account, télécharger la clé JSON

#### Jour 5 — Terraform (Concepts & Base)
- [ ] Regarder [Terraform concepts](https://youtu.be/s2bOYDCKl_M) (~15 min)
- [ ] Regarder [Terraform basics](https://youtu.be/Y2ux7gq3Z0o) (~20 min)
- [ ] Installer Terraform
- [ ] Lire le code : `01-docker-terraform/terraform/`
- [ ] Lancer `terraform init`, `terraform plan`, `terraform apply`
- [ ] Créer un bucket GCS + dataset BigQuery avec Terraform

#### Jour 6 — Terraform Variables & Déploiement
- [ ] Regarder [Deployment avec variables](https://youtu.be/PBi0hHjLftk) (~15 min)
- [ ] Modifier les variables Terraform pour ton projet
- [ ] Pratiquer : `terraform destroy` → `terraform apply` en modifiant les variables
- [ ] Commencer le **Homework Module 1** (Q1–Q4 : Docker + SQL)

#### Jour 7 — Homework Module 1 (fin)
- [ ] Finir le **Homework Module 1** (Q5–Q7 : SQL + Terraform)
- [ ] Vérifier que GCS bucket + BigQuery dataset existent bien
- [ ] Soumettre via : `https://courses.datatalks.club/de-zoomcamp-2026/homework/hw1`
- [ ] **Résultat attendu** : Container Docker avec Postgres qui tourne, données ingérées, infrastructure GCP provisionnée via Terraform

---

### SEMAINE 2 — Module 2 : Workflow Orchestration (Kestra)

**Objectif** : Orchestrer des pipelines ETL/ELT avec Kestra, scheduling, backfill.

#### Jour 1 — Introduction à l'orchestration
- [ ] Regarder [What is Workflow Orchestration?](https://youtu.be/-JLnp-iLins) (~10 min)
- [ ] Regarder [What is Kestra?](https://youtu.be/ZvVN_NmB_1s) (~10 min)
- [ ] Lire le README du Module 2 : `02-workflow-orchestration/README.md`
- [ ] Comprendre le concept d'orchestrateur vs exécution manuelle

#### Jour 2 — Installation & Premiers Flows
- [ ] Regarder [Installing Kestra](https://youtu.be/wgPxC4UjoLM) (~15 min)
- [ ] Modifier le `docker-compose.yml` de la semaine 1 pour ajouter Kestra
- [ ] Lancer : `docker compose up -d` dans `02-workflow-orchestration/`
- [ ] Accéder à l'UI Kestra : `http://localhost:8080`
- [ ] Importer et exécuter `01_hello_world.yaml`

#### Jour 3 — Concepts Kestra & Python
- [ ] Regarder [Kestra Concepts](https://youtu.be/MNOKVx8780E) (~20 min)
- [ ] Regarder [Orchestrate Python Code](https://youtu.be/VAHm0R_XjqI) (~15 min)
- [ ] Importer et exécuter `02_python.yaml`
- [ ] Comprendre : Flow, Task, Input, Output, Trigger, Variable

#### Jour 4 — Pipeline ETL Local (Postgres)
- [ ] Regarder [Getting Started Pipeline](https://youtu.be/-KmwrCqRhic) (~15 min)
- [ ] Regarder [Load Taxi Data to Postgres](https://youtu.be/Z9ZmmwtXDcU) (~25 min)
- [ ] Importer `03_getting_started_data_pipeline.yaml` → l'exécuter
- [ ] Importer `04_postgres_taxi.yaml` → l'exécuter (yellow + green taxi)
- [ ] Vérifier les données dans Postgres via pgAdmin

#### Jour 5 — Scheduling & Backfill
- [ ] Regarder [Scheduling and Backfills](https://youtu.be/1pu_C_oOAMA) (~15 min)
- [ ] Importer `05_postgres_taxi_scheduled.yaml`
- [ ] Comprendre la syntaxe cron, les backfills
- [ ] Lancer un backfill manuellement depuis l'UI Kestra

#### Jour 6 — ELT dans le Cloud (GCS + BigQuery)
- [ ] Regarder [ETL vs ELT](https://youtu.be/E04yurp1tSU) (~10 min)
- [ ] Regarder [Setup GCP](https://youtu.be/TLGFAOHpOYM) (~20 min)
- [ ] Configurer les KV Store dans Kestra (GCP_PROJECT_ID, bucket, dataset)
- [ ] Importer `06_gcp_kv.yaml`, `07_gcp_setup.yaml`
- [ ] Regarder [Load Taxi Data to BigQuery](https://youtu.be/52u9X_bfTAo) (~25 min)
- [ ] Importer et exécuter `08_gcp_taxi.yaml` (yellow + green)
- [ ] Regarder [Schedule and Backfill](https://youtu.be/b-6KhfWfk2M) (~15 min)
- [ ] Importer `09_gcp_taxi_scheduled.yaml`, tester le backfill

#### Jour 7 — AI Copilot & Homework
- [ ] Regarder [AI for Data Engineering](https://youtu.be/GHPtRDAv044) (~10 min)
- [ ] Regarder [Context Engineering ChatGPT](https://youtu.be/LmnfjGKwnVU) (~15 min)
- [ ] Configurer Gemini API Key dans Kestra
- [ ] Tester l'AI Copilot de Kestra (section 2.5.3)
- [ ] **Optionnel** : Regarder [RAG bonus](https://youtu.be/XuPDQ1UcNyI) (~20 min)
- [ ] **Homework Module 2** : Backfill 2021 pour yellow + green taxi
- [ ] Répondre aux 6 questions du quiz
- [ ] Soumettre via : `https://courses.datatalks.club/de-zoomcamp-2026/homework/hw2`

---

### SEMAINE 3 — Workshop dlt + Début Module 3 (BigQuery)

**Objectif** : Ingestion via API avec dlt, puis introduction au data warehousing.

#### Jour 1 — Workshop dlt (Partie 1)
- [ ] Lire : `cohorts/2026/workshops/dlt.md`
- [ ] Regarder la [vidéo du workshop dlt](https://www.youtube.com/watch?v=5eMytPBgmVs) (~1h)
- [ ] Comprendre le concept : Extract → Normalize → Load
- [ ] Installer `dlt` : `pip install "dlt[duckdb]"`

#### Jour 2 — Workshop dlt (Partie 2) — Hands-on
- [ ] Suivre le guide : `cohorts/2026/workshops/dlt/README.md`
- [ ] Créer un projet : `dlt init dlthub:open_library duckdb`
- [ ] Configurer l'IDE agentic (Cursor/Windsurf)
- [ ] Lancer le pipeline Open Library API → DuckDB

#### Jour 3 — Workshop dlt (Partie 3) — Exploration
- [ ] Lancer le dashboard : `dlt pipeline open_library_pipeline show`
- [ ] Explorer les schémas, tables, colonnes
- [ ] **Optionnel** : Créer une visualisation marimo + ibis
- [ ] **Homework dlt** : Faire le `dlt_homework.md`
- [ ] Soumettre via : `https://courses.datatalks.club/de-zoomcamp-2026/homework/dlt`

#### Jour 4 — Module 3 : Data Warehouse & BigQuery
- [ ] Regarder [Data Warehouse and BigQuery](https://youtu.be/jrHljAoD6nM) (~20 min)
- [ ] Lire le README : `03-data-warehouse/README.md`
- [ ] Comprendre : columnar storage, DWH vs DB transactionnelle
- [ ] Explorer les slides : lien Google Slides dans le README

#### Jour 5 — BigQuery : SQL Pratique
- [ ] Exécuter le SQL de base : `03-data-warehouse/big_query.sql`
- [ ] Charger les données Yellow Taxi 2024 dans GCS
- [ ] Créer une external table dans BigQuery
- [ ] Comparer external table vs native table

#### Jour 6 — Partitioning & Clustering
- [ ] Regarder [Partitioning vs Clustering](https://youtu.be/-CqXf7vhhDs) (~15 min)
- [ ] Regarder [Best practices](https://youtu.be/k81mLJVX08w) (~15 min)
- [ ] Regarder [Internals of BigQuery](https://youtu.be/eduHi1inM4s) (~15 min)
- [ ] Créer une table partitionnée par `tpep_dropoff_datetime`
- [ ] Tester les performances : partitionnée vs non-partitionnée

#### Jour 7 — BigQuery ML & Homework
- [ ] Regarder [ML in BigQuery](https://youtu.be/B-WtpB0PuG4) (~20 min)
- [ ] Exécuter : `03-data-warehouse/big_query_ml.sql`
- [ ] Regarder [Deploying ML model from BigQuery](https://youtu.be/BjARzEWaznU) (~15 min)
- [ ] Suivre : `03-data-warehouse/extract_model.md`
- [ ] **Homework Module 3** : 9 questions sur BigQuery
- [ ] Soumettre via : `https://courses.datatalks.club/de-zoomcamp-2026/homework/hw3`

---

### SEMAINE 4 — Module 3 (fin) + Module 4 (dbt)

**Objectif** : Finaliser BigQuery ML, puis analytics engineering avec dbt.

#### Jour 1 — BigQuery ML (Approfondissement)
- [ ] Revoir les concepts ML dans BigQuery si nécessaire
- [ ] Créer un modèle de prédiction de tip avec BQML
- [ ] Exporter et déployer le modèle avec Docker (`extract_model.md`)
- [ ] Explorer les extras : `03-data-warehouse/extras/`

#### Jour 2 — Module 4 : Introduction à dbt
- [ ] Regarder [Introduction to Analytics Engineering](https://youtu.be/HxMIsPrIyGQ) (~10 min)
- [ ] Regarder [Introduction to data modeling](https://youtu.be/uF76d5EmdtU) (~10 min)
- [ ] Regarder [What is dbt?](https://youtu.be/gsKuETFJr54) (~15 min)
- [ ] Lire le README : `04-analytics-engineering/README.md`
- [ ] Choisir : **Cloud setup** (BigQuery + dbt Cloud) ou **Local setup** (DuckDB + dbt Core)

#### Jour 3 — Setup dbt
- [ ] Regarder [dbt Core vs Cloud](https://youtu.be/auzcdLRyEIk) (~10 min)
- [ ] **Cloud** : Suivre `setup/cloud_setup.md` → créer un compte dbt Cloud, connecter BigQuery
- [ ] **Local** : Suivre `setup/local_setup.md` → installer dbt-core + DuckDB
- [ ] Lancer `dbt init` et configurer la connexion

#### Jour 4 — dbt : Sources & Models
- [ ] Regarder [dbt Project Structure](https://youtu.be/2dYDS4OQbT0) (~10 min)
- [ ] Regarder [dbt Sources](https://youtu.be/7CrrXazV_8k) (~15 min)
- [ ] Regarder [dbt Models](https://youtu.be/JQYz-8sl1aQ) (~15 min)
- [ ] Créer les sources YAML pour les tables taxi
- [ ] Créer les premiers models (staging, intermediate, fact/dim)

#### Jour 5 — dbt : Seeds, Macros, Tests
- [ ] Regarder [Seeds and Macros](https://youtu.be/lT4fmTDEqVk) (~15 min)
- [ ] Regarder [dbt Tests](https://youtu.be/bvZ-rJm7uMU) (~15 min)
- [ ] Ajouter des seeds (zones taxi)
- [ ] Créer des macros de réutilisabilité
- [ ] Ajouter des tests : unique, not_null, accepted_values, relationships

#### Jour 6 — dbt : Documentation & Packages
- [ ] Regarder [Documentation](https://youtu.be/UqoWyMjcqrA) (~15 min)
- [ ] Regarder [dbt Packages](https://youtu.be/KfhUA9Kfp8Y) (~10 min)
- [ ] Regarder [dbt Commands](https://youtu.be/t4OeWHW3SsA) (~10 min)
- [ ] Générer la documentation : `dbt docs generate`
- [ ] Ajouter `dbt_utils` package
- [ ] Lancer `dbt build` (exécute models + tests)

#### Jour 7 — Homework Module 4
- [ ] Revoir les notes sur window functions : `04-analytics-engineering/refreshers/SQL.md`
- [ ] **Homework Module 4** : Questions sur dbt, window functions, CTEs
- [ ] Pratiquer : `dbt build`, `dbt test`, `dbt docs serve`
- [ ] Soumettre via : `https://courses.datatalks.club/de-zoomcamp-2026/homework/hw4`
- [ ] **Bilan Mois 1** : Vérifier que Docker, Kestra, dlt, BigQuery, dbt sont maîtrisés

---

## MOIS 2 — Plateformes, Batch & Streaming

---

### SEMAINE 5 — Module 4 (deep dive) + Début Module 5

**Objectif** : Consolider dbt, démarrer Bruin.

#### Jour 1 — dbt : Modélisation avancée
- [ ] Explorer le dbt project taxi : `04-analytics-engineering/taxi_rides_ny/`
- [ ] Comprendre l'architecture : staging → intermediate → fact/dim
- [ ] Ajouter des modèles incrementals
- [ ] Utiliser `ref()` et `source()` correctement

#### Jour 2 — dbt : Jinja & Macros
- [ ] Écrire des macros Jinja personnalisées
- [ ] Utiliser `generate_schema_name` pour la gestion d'environnements
- [ ] Comprendre les hooks : `on-run-start`, `on-run-end`

#### Jour 3 — dbt : Déploiement
- [ ] Mettre en place un environnement de dev/prod
- [ ] Configurer les cibles (target) dans `profiles.yml`
- [ ] Lancer `dbt run --target prod`
- [ ] Explorer les class notes : `04-analytics-engineering/class_notes/`

#### Jour 4 — Module 5 : Introduction à Bruin
- [ ] Regarder [5.1 Introduction to Bruin](https://youtu.be/f6vg7lGqZx0) (~15 min)
- [ ] Lire le README : `05-data-platforms/README.md`
- [ ] Lire les notes : `05-data-platforms/notes/01-introduction.md`
- [ ] Comprendre : ingestion + transformation + orchestration + quality + metadata

#### Jour 5 — Bruin : Getting Started
- [ ] Regarder [5.2 Getting Started](https://youtu.be/JJwHKSidX_c) (~20 min)
- [ ] Lire les notes : `05-data-platforms/notes/02-getting-started.md`
- [ ] Installer Bruin
- [ ] Lancer : `bruin init zoomcamp my-taxi-pipeline`
- [ ] Configurer les connexions (DuckDB)

#### Jour 6 — Bruin : Pipeline NYC Taxi
- [ ] Regarder [5.3 Building an End-to-End Pipeline](https://youtu.be/q0k_iz9kWsI) (~25 min)
- [ ] Lire les notes : `05-data-platforms/notes/03-nyc-taxi-pipeline.md`
- [ ] Construire le pipeline 3 couches (ingestion, staging, reports)
- [ ] Exécuter : `bruin run`

#### Jour 7 — Bruin : MCP & Homework
- [ ] Regarder [5.4 Using Bruin MCP](https://youtu.be/224xH7h8OaQ) (~15 min)
- [ ] Lire les notes : `05-data-platforms/notes/04-bruin-mcp.md`
- [ ] Configurer Bruin MCP dans Cursor/VS Code
- [ ] Regarder [5.5 Deploy to Bruin Cloud](https://youtu.be/uBqjLEwF8rc) (~15 min)
- [ ] Lire les notes : `05-data-platforms/notes/05-bruin-cloud.md`
- [ ] **Homework Module 5** : Compléter le pipeline Bruin
- [ ] Soumettre via : `https://courses.datatalks.club/de-zoomcamp-2026/homework/hw5`

---

### SEMAINE 6 — Module 5 (deep dive) + Début Module 6

**Objectif** : Approfondir Bruin concepts, démarrer Spark.

#### Jour 1 — Bruin Core Concepts
- [ ] Regarder [Projects](https://youtu.be/YWDjnSxbBtY) (~5 min)
- [ ] Regarder [Pipelines](https://youtu.be/uzp_DiR4Sok) (~5 min)
- [ ] Regarder [Assets](https://youtu.be/ZElY5SoqrwI) (~10 min)
- [ ] Regarder [Variables](https://youtu.be/XCx0nDmhhxA) (~5 min)
- [ ] Regarder [Commands](https://youtu.be/3nykPEs_V7E) (~10 min)
- [ ] Lire les notes : `05-data-platforms/notes/06-core-*.md`

#### Jour 2 — Bruin : Pipeline Complet Cloud
- [ ] Déployer le pipeline sur BigQuery (au lieu de DuckDB)
- [ ] Configurer Bruin Cloud
- [ ] Connecter GitHub → déploiement automatique
- [ ] Monitorer les runs

#### Jour 3 — Module 6 : Introduction à Spark
- [ ] Regarder [6.1.1 Intro to Batch Processing](https://youtu.be/dcHe5Fl3MF8) (~10 min)
- [ ] Regarder [6.1.2 Intro to Spark](https://youtu.be/FhaqbEOuQ8U) (~15 min)
- [ ] Lire le README : `06-batch/README.md`
- [ ] Comprendre : batch vs streaming, Spark vs MapReduce

#### Jour 4 — Installation Spark
- [ ] Suivre le guide d'installation selon ton OS :
  - [Linux](06-batch/setup/linux.md) | [MacOS](06-batch/setup/macos.md) | [Windows](06-batch/setup/windows.md)
- [ ] Regarder [Installing Spark (Linux)](https://youtu.be/hqUbB9c8sKg) (~15 min) — même si t'es pas sous Linux
- [ ] Vérifier : `pyspark` fonctionne dans le terminal
- [ ] **Alternative** : Google Colab si l'installation locale échoue

#### Jour 5 — PySpark : DataFrames & SQL
- [ ] Regarder [First Look at PySpark](https://youtu.be/r_Sf6fCB40c) (~20 min)
- [ ] Regarder [Spark DataFrames](https://youtu.be/ti3aC1m3rE8) (~25 min)
- [ ] Suivre le code : `06-batch/code/`
- [ ] Charger les données taxi avec PySpark
- [ ] Manipuler les DataFrames (select, filter, groupBy, join)

#### Jour 6 — Spark SQL & Préparation Données
- [ ] Regarder [Preparing Taxi Data](https://youtu.be/CI3P4tAtru4) (~15 min) — optionnel
- [ ] Regarder [SQL with Spark](https://youtu.be/uAlp2VuZZPY) (~15 min)
- [ ] Exécuter : `06-batch/code/download_data.sh`
- [ ] Créer des vues temporaires et faire du SQL dans Spark
- [ ] Comparer Spark SQL vs PySpark DataFrames API

#### Jour 7 — Spark Internals & Homework
- [ ] Regarder [Anatomy of a Spark Cluster](https://youtu.be/68CipcZt7ZA) (~15 min)
- [ ] Regarder [GroupBy in Spark](https://youtu.be/9qrDsY_2COo) (~20 min)
- [ ] Regarder [Joins in Spark](https://youtu.be/lu7TrqAWuH4) (~20 min)
- [ ] **Optionnel** : RDDs (sections 6.5)
- [ ] **Homework Module 6** : Questions Spark
- [ ] Soumettre via : `https://courses.datatalks.club/de-zoomcamp-2026/homework/hw6`

---

### SEMAINE 7 — Module 6 (Cloud) + Module 7 (Streaming)

**Objectif** : Spark dans le cloud, puis streaming avec Kafka/Flink.

#### Jour 1 — Spark : Cloud & GCS
- [ ] Regarder [Connecting to GCS](https://youtu.be/Yyz293hBVcQ) (~15 min)
- [ ] Configurer Spark pour lire/écrire dans GCS
- [ ] Lire les données taxi depuis GCS avec Spark

#### Jour 2 — Spark Cluster Local & Dataproc
- [ ] Regarder [Creating a Local Spark Cluster](https://youtu.be/HXBwSlXo5IA) (~15 min)
- [ ] Regarder [Setting up a Dataproc Cluster](https://youtu.be/osAiAYahvh8) (~20 min)
- [ ] Créer un cluster Dataproc dans GCP
- [ ] Soumettre un job Spark sur Dataproc

#### Jour 3 — Spark & BigQuery
- [ ] Regarder [Connecting Spark to BigQuery](https://youtu.be/HIm2BOj8C0Q) (~15 min)
- [ ] Lire depuis BigQuery avec le connecteur Spark-BQ
- [ ] Écrire les résultats Spark dans BigQuery
- [ ] Nettoyer le cluster Dataproc (`gcloud dataproc clusters delete`)

#### Jour 4 — Module 7 : Introduction au Streaming
- [ ] Regarder la [vidéo principale Module 7](https://youtu.be/YDUgFeHQzJU) (~1h — live stream)
- [ ] Lire le README : `07-streaming/README.md`
- [ ] Comprendre : Kafka, topic, producer, consumer, broker
- [ ] Lire la théorie Kafka : `07-streaming/theory/`

#### Jour 5 — Kafka Theory (Approfondissement)
- [ ] Parcourir les vidéos de théorie Kafka (section theory/)
- [ ] Comprendre : partitions, offsets, consumer groups, schema registry
- [ ] Lire sur Avro : `07-streaming/theory/` (schémas, évolution)

#### Jour 6 — PyFlink Workshop (Partie 1)
- [ ] Suivre le workshop : `07-streaming/workshop/`
- [ ] Installer Redpanda (Kafka-compatible) avec Docker
- [ ] Créer un producer Python
- [ ] Créer un consumer Python
- [ ] Vérifier la transmission de messages

#### Jour 7 — PyFlink Workshop (Partie 2) & Homework
- [ ] Mettre en place Flink avec PyFlink
- [ ] Créer un streaming pipeline : Redpanda → PyFlink → PostgreSQL
- [ ] Tester avec des données taxi en temps réel
- [ ] **Homework Module 7** : Questions streaming
- [ ] Soumettre via : `https://courses.datatalks.club/de-zoomcamp-2026/homework/hw7`

---

### SEMAINE 8 — Révision & Préparation Projet

**Objectif** : Consolider tous les modules, choisir son dataset de projet.

#### Jour 1 — Revue Module 1-2 (Docker, Terraform, Kestra)
- [ ] Refaire un pipeline complet : Docker → ingestion → Kestra orchestration
- [ ] Vérifier que les concepts sont clairs : container, image, volume, network
- [ ] Vérifier : `terraform plan/apply/destroy` sans erreur

#### Jour 2 — Revue Module 3-4 (BigQuery, dbt)
- [ ] Refaire une session dbt complète : `dbt build`, `dbt docs`
- [ ] Vérifier les partitions/clusters BQ
- [ ] Lire les class notes si besoin : `04-analytics-engineering/class_notes/`

#### Jour 3 — Revue Module 5-7 (Bruin, Spark, Streaming)
- [ ] Lancer un pipeline Bruin de bout en bout
- [ ] Faire un calcul Spark simple sur les données taxi
- [ ] Vérifier la compréhension Kafka (topic, producer, consumer)

#### Jour 4 — Choisir son Dataset de Projet
- [ ] Lire : `projects/datasets.md` — liste des datasets recommandés
- [ ] **Rappel** : Le dataset NYC taxi est **interdit** pour le projet
- [ ] Explorer les datasets : [NYC Open Data](https://opendata.cityofnewyork.us/), [Kaggle](https://kaggle.com/), etc.
- [ ] Définir la problématique : quelle question commerciale le projet répond-il ?

#### Jour 5 — Architecture du Projet
- [ ] Esquisser l'architecture : ingestion → datalake → warehouse → transformations → dashboard
- [ ] Choisir les outils (peuvent différer du cours) :
  - Cloud : GCP (recommandé) / AWS / Azure
  - IaC : Terraform
  - Orchestration : Kestra / Airflow / Prefect
  - DWH : BigQuery / Snowflake / Redshift
  - Transform : dbt / Spark
  - Dashboard : Looker / Streamlit
- [ ] Créer un dépôt GitHub dédié pour le projet

#### Jour 6 — Cahier des Charges
- [ ] Rédiger la description du problème
- [ ] Lister les datasets et sources de données
- [ ] Schématiser le pipeline (draw.io / Mermaid)
- [ ] Définir les livrables : 2 graphiques minimum (1 catégoriel + 1 temporel)

#### Jour 7 — Début du Projet
- [ ] Mettre en place l'infrastructure cloud avec Terraform
- [ ] Créer le bucket GCS et le dataset BigQuery
- [ ] Commencer l'ingestion des données
- [ ] **Bilan Mois 2** : Vérifier que Spark, Kafka et tous les outils sont maîtrisés

---

## MOIS 3 — Projet Final

---

### SEMAINE 9 — Ingestion & Data Lake

**Objectif** : Pipeline d'ingestion fonctionnel, données dans le datalake.

#### Jour 1-2 — Infrastructure as Code
- [ ] Finaliser le code Terraform (bucket, dataset, permissions)
- [ ] Ajouter les scripts d'automatisation (Makefile)
- [ ] Versionner le tout sur GitHub

#### Jour 3-4 — Ingestion Batch
- [ ] Écrire le pipeline d'extraction (API, CSV, Parquet, etc.)
- [ ] Utiliser Kestra (ou l'outil choisi) pour l'orchestration
- [ ] Charger les données brutes dans GCS
- [ ] Ajouter un scheduling (daily/hourly)

#### Jour 5-6 — Data Lake
- [ ] Organiser les données dans GCS (partition par date)
- [ ] Créer des external tables BigQuery pointant vers GCS
- [ ] Vérifier l'intégrité des données

#### Jour 7 — Validation & Tests
- [ ] Vérifier que le pipeline d'ingestion est reproductible
- [ ] Tester depuis un clone propre du dépôt
- [ ] Documenter les étapes dans le README

---

### SEMAINE 10 — Data Warehouse & Transformations

**Objectif** : Données transformées et prêtes pour le dashboard.

#### Jour 1-2 — Data Warehouse
- [ ] Créer les tables optimisées dans BigQuery
- [ ] Partitionner et clustering les tables
- [ ] Comparer les coûts avant/après optimisation

#### Jour 3-5 — Transformations (dbt / Spark)
- [ ] Créer les modèles de transformation
- [ ] Nettoyer, dédupliquer, agréger les données
- [ ] Ajouter des tests de qualité
- [ ] Documenter les transformations
- [ ] Générer la documentation dbt

#### Jour 6-7 — CI/CD
- [ ] Mettre en place GitHub Actions pour :
  - Terraform plan/apply automatique
  - dbt build automatique
  - Tests unitaires
- [ ] **Optionnel** : Conteneuriser avec Docker

---

### SEMAINE 11 — Dashboard & Finalisation

**Objectif** : Dashboard fonctionnel, documentation complète, soumission.

#### Jour 1-2 — Dashboard (Partie 1)
- [ ] Choisir l'outil : Looker Studio (recommandé) ou Streamlit
- [ ] Connecter la source BigQuery
- [ ] Créer le premier graphique (distribution catégorielle)

#### Jour 3-4 — Dashboard (Partie 2)
- [ ] Créer le second graphique (série temporelle)
- [ ] Ajouter des filtres et interactions
- [ ] Soigner le design : titres, légendes, couleurs

#### Jour 5 — README & Documentation
- [ ] Rédiger le README du projet :
  - Description du problème
  - Architecture (schéma)
  - Instructions d'exécution
  - Choix techniques justifiés
- [ ] Vérifier que tout est reproductible depuis `git clone`

#### Jour 6 — Soumission Attempt #1
- [ ] Vérifier les critères d'évaluation (voir : `projects/README.md`)
- [ ] Soumettre via : `https://courses.datatalks.club/de-zoomcamp-2026/project/project1`
- [ ] Partager le lien du dépôt GitHub

#### Jour 7 — Peer Reviews
- [ ] Trouver son hash dans la grille d'assignation
- [ ] Évaluer **3 projets de peers**
- [ ] Soumettre chaque évaluation via le formulaire dédié
- [ ] **Critères** : Problem description (4pt), Cloud (4pt), Ingestion (4pt), DWH (4pt), Transform (4pt), Dashboard (4pt), Reproducibility (4pt) = **28 points max**

---

### SEMAINE 12 — Tampon & Rattrapage

**Objectif** : Gérer les imprévus, 2e tentative si nécessaire.

#### Jour 1-3 — Corrections suite aux retours
- [ ] Lire les feedbacks des peers
- [ ] Corriger les problèmes identifiés
- [ ] Améliorer la documentation

#### Jour 4-5 — 2e Tentative (si nécessaire)
- [ ] Soumettre la version améliorée
- [ ] Formulaire : `https://courses.datatalks.club/de-zoomcamp-2026/project/project2`

#### Jour 6 — Finalisation
- [ ] Mettre à jour le nom du certificat : lien d'enrollment
- [ ] Partager son projet sur LinkedIn/Twitter
- [ ] Célébrer la fin du cours ! 🎉

#### Jour 7 — Bilan & Prochaines Étapes
- [ ] Explorer les ressources supplémentaires :
  - `awesome-data-engineering.md` (liste de ressources)
  - `workshop-best-practices.md` (best practices)
  - `certificates.md` (comment obtenir le certificat)
- [ ] Envisager les cours suivants : ML Zoomcamp, MLOps Zoomcamp

---

## Version compressée (2,5 mois — 10 semaines)

| Semaine | Modules | Changements |
|---------|---------|-------------|
| S1 | Module 1 | Idem |
| S2 | Module 2 | Idem (skip AI Copilot / RAG) |
| S3 | dlt + Module 3 | Jour 7 BQ ML en optionnel |
| S4 | Module 4 | Supprimer le deep dive Jinja |
| S5 | Module 5 | Core concepts en lecture rapide |
| S6 | Module 6 | Skip RDDs, cluster Dataproc en optionnel |
| S7 | Module 7 | Workshop PyFlink en accéléré |
| S8–S10 | Projet | 3 semaines au lieu de 4 |

---

## Notes importantes

- **Cohort 2026** : Début le 12 janvier 2026 — inscris-toi [ici](https://airtable.com/shr6oVXeQvSI5HuWD)
- **Slack** : Rejoins [#course-data-engineering](https://app.slack.com/client/T01ATQK62F8/C01FABYF2RG) pour poser des questions
- **Playlist YouTube** complète : [lien](https://www.youtube.com/playlist?list=PL3MmuxUbc_hJed7dXYoJw8DoCuVHhGEQb)
- **Certificat** : Obtenu en complétant tous les homeworks + projet + 3 peer reviews
- **Projet** : 2 tentatives max, dataset NYC taxi interdit, 28 pts max
- **Workshop 2** (AI-Assisted dlt) : Optionnel — à placer en S3 si tu as le temps
