# 🗺️ Projeto 04 — Cloud Data Architecture & Serverless Web App: WeekPlanner T1 Topografia

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)
![Vercel](https://img.shields.io/badge/Vercel-000000?style=for-the-badge&logo=vercel&logoColor=white)
![Render](https://img.shields.io/badge/Render-46E3B7?style=for-the-badge&logo=render&logoColor=white)
![Status](https://img.shields.io/badge/Status-Concluído-1A9C3E?style=for-the-badge)

---

## 📌 Sobre o Projeto

Este projeto prático consistiu no desenvolvimento de uma aplicação web completa (Full-Stack) voltada para a gestão de agendamentos e acompanhamento de pendências operacionais de uma equipe técnica de topografia.

O objetivo principal foi substituir controles locais isolados por uma **arquitetura de dados centralizada em nuvem (Serverless)**. A aplicação atua como a principal fonte de ingestão de dados de campo, estabelecendo uma fundação relacional sólida e íntegra para habilitar futuras modelagens analíticas (Cloud Data Analytics).

---

## 🏗️ Arquitetura da Solução

A engenharia da aplicação foi estruturada no modelo de **Monorepo** com arquitetura desacoplada, dividindo as camadas de apresentação, computação e persistência em provedores de nuvem especializados (*Free Tier Optimization*).

```text
       [ Engenheiro / Topógrafo no Campo ]
                       │
                       ▼
       [ Portal Web (Frontend) ] ────────► Hospedado na Vercel
                       │ (HTTP Requests JSON)
                       ▼
 ┌─────────────────────────────────────────────────────────┐
 │                     Nuvem Serverless                    │
 │                                                         │
 │  [ API REST Backend ] ◄──────── Hospedado no Render     │
 │                       │         (Engine Python/FastAPI) │
 │                       │ (ORM / SQLAlchemy)              │
 │                       ▼                                 │
 │  [ Banco de Dados ]   ◄──────── Hospedado no Neon.tech  │
 │                                 (PostgreSQL 18)         │
 └─────────────────────────────────────────────────────────┘
