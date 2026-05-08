# ODA_PROCESS
Descreve os objetivos do projeto

<img width="5780" height="4300" alt="Arquitetura do ODC" src="https://github.com/user-attachments/assets/060464ec-0608-4104-ae0e-bb516aeb277f" />


# Observatório de Dados de Alagoinhas (ODA) 📊

[![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)](https://www.python.org/)
[![Google Cloud](https://img.shields.io/badge/GCP-4285F4?style=flat-square&logo=google-cloud&logoColor=white)](https://cloud.google.com/)
[![BigQuery](https://img.shields.io/badge/BigQuery-669DF6?style=flat-square&logo=google-cloud&logoColor=white)](https://cloud.google.com/bigquery)
[![GitHub Actions](https://img.shields.io/badge/CI%2FCD-GitHub_Actions-2088FF?style=flat-square&logo=github-actions&logoColor=white)](https://github.com/features/actions)

## 📌 Sobre o Projeto
O **Observatório de Dados de Alagoinhas (ODA)** é uma plataforma analítica desenvolvida para centralizar, estruturar e visualizar dados públicos do município de Alagoinhas - BA. O objetivo do projeto é apoiar a gestão pública municipal através da inteligência de dados, transformando informações brutas de diversas fontes (notificações epidemiológicas, clima, infraestrutura e finanças) em conhecimento acionável para a tomada de decisão.

Este projeto foi arquitetado e é mantido pela **TERRITÓRIO Inteligência de Dados**, com foco em governança, escalabilidade e transparência.

## 🛠️ Stack Tecnológico
O projeto foi construído utilizando uma arquitetura moderna e *serverless*, priorizando performance e otimização de custos:

* **Linguagem Principal:** Python 3.9+
* **Provedor de Nuvem:** Google Cloud Platform (GCP)
* **Data Warehouse:** Google BigQuery
* **Orquestração e Computação:** Google Cloud Run (Jobs)
* **Governança de Dados:** Google Cloud Knowledge Catalog (Dataplex)
* **CI/CD:** GitHub Actions
* **Business Intelligence (BI):** Power BI / Looker Studio

## 🏗️ Arquitetura de Dados
O fluxo de dados do ODA segue as melhores práticas de Engenharia de Dados, dividido nas seguintes camadas:

1. **Ingestão (Extract & Load):** * Scripts em Python são executados periodicamente via **Cloud Run Jobs** (ex: `oda-dengue-sync`).
   * Os dados são extraídos de APIs governamentais (como o DATASUS/InfoDengue) e carregados na camada *Landing* (bronze) do BigQuery.

2. **Armazenamento e Transformação (Transform):**
   * Os dados brutos são limpos, tratados (anonimização de PII) e modelados no **BigQuery**.
   * Utiliza-se modelagem dimensional (Tabelas Fato e Dimensão) para garantir alta performance nas consultas da camada *Serving* (gold).

3. **Governança e Catálogo:**
   * O **Knowledge Catalog** atua sobre o BigQuery mapeando metadados, gerando dicionários de dados automáticos através de IA e rastreando a linhagem dos dados (*Data Lineage*).

4. **Visualização (DataViz):**
   * Ferramentas de BI conectam-se diretamente às tabelas agregadas do BigQuery para alimentar os painéis interativos utilizados pelos gestores públicos.

5. **Automação e Deploy:**
   * O pipeline de CI/CD via **GitHub Actions** garante que qualquer alteração nos scripts de extração seja testada e implementada automaticamente na nuvem, sem necessidade de intervenção manual.


## 📥 Como Rodar a Ingestão de Dados

A ingestão de dados do ODA é projetada para ser flexível, permitindo a execução manual durante o desenvolvimento ou a execução em nuvem para produção. 

### 1. Execução Local (Desenvolvimento e Testes)
Para rodar os pipelines na sua máquina, certifique-se de que o ambiente virtual está ativo, as dependências do `requirements.txt` estão instaladas e o seu terminal está autenticado no GCP (via `gcloud auth application-default login`).

Execute o script correspondente ao conjunto de dados que deseja sincronizar. Exemplo com os dados epidemiológicos:

```bash
# Executa o pipeline de extração da API e carga no BigQuery
python scripts/sync_dengue_data.py
```

Execução na nuvem:

# Dispara o job de ingestão de dados epidemiológicos diretamente no GCP
gcloud run jobs execute oda-dengue-sync --region southamerica-east1



# PAINÉIS


<img width="1065" height="601" alt="Captura de tela 2026-05-03 154933" src="https://github.com/user-attachments/assets/4e81462a-0943-4bdb-8db7-2d22b8ca3479" />

----

<img width="1070" height="604" alt="Captura de tela 2026-05-03 154903" src="https://github.com/user-attachments/assets/cd66cf1c-9f38-4ec8-8056-728783590994" />

----

<img width="1073" height="602" alt="Captura de tela 2026-05-03 154836" src="https://github.com/user-attachments/assets/18754506-a80e-4d34-acc1-fb313b001dd8" />



