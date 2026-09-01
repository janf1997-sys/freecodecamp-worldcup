# World Cup Database

A relational database and automated ETL pipeline built with **PostgreSQL** and **Bash** as part of the freeCodeCamp **Relational Database Certification**.

The project automates the ingestion of FIFA World Cup match records from a CSV file into a normalized PostgreSQL database and executes analytical SQL queries to extract statistical insights.

---

## 📌 Project Architecture & Data Flow

```text
┌───────────────────────┐
│       games.csv       │  (Raw Match Data: Year, Round, Teams, Goals)
└───────────┬───────────┘
            │
            ▼
┌───────────────────────┐
│    insert_data.sh     │  (Bash Script: Dynamic Parsing, Deduplication & Ingestion)
└───────────┬───────────┘
            │
            ▼
┌─────────────────────────────────────────────────────────────┐
│                     PostgreSQL Database                     │
│                        (worldcup)                           │
│                                                             │
│   ┌───────────────┐              ┌──────────────────────┐   │
│   │     teams     │ ◄───────────┤        games         │   │
│   │ (team_id, PK) │ ◄───────────┤ (winner_id, FK)      │   │
│   │               │             │ (opponent_id, FK)    │   │
│   └───────────────┘             └──────────────────────┘   │
└─────────────────────────────────────────────────────────────┘
            ▲
            │
┌───────────┴───────────┐
│      queries.sh       │  (Statistical Aggregations & Analytical Queries)
└───────────────────────┘
