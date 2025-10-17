# 💼 Estimativa de Custo e Cronograma – Projeto Ingressou (MVP + Melhorias + Manutenção)

> **Versão:** 3.2  
> **Data:** Outubro de 2025  
> **Autor:** Gabriel Lima  
> **Projeto:** Ingressou — Plataforma Web de Venda e Gestão de Ingressos  

---

## 📊 Metodologia Utilizada

### Abordagem Híbrida — *Bottom-Up + Delphi (Planning Poker leve)*

A estimativa foi construída com base em duas técnicas:
- **Bottom-Up:** decomposição funcional do sistema em módulos técnicos.
- **Delphi/Planning Poker:** consenso entre desenvolvedores sobre esforço relativo e complexidade.

---

## 📌 Premissas Gerais

| Item | Valor |
|------|--------|
| **Duração total** | 4 meses (≈ 88 dias úteis) |
| **MVP (Desenvolvimento Base)** | 2 meses (≈ 44 dias úteis) |
| **Melhorias e refino** | 2 meses (≈ 44 dias úteis) |
| **Equipe** | 4 desenvolvedores (3 back-end + 1 front-end) |
| **Carga horária** | 8h/dia |
| **Custo diário por dev** | **R$ 200,00** |
| **Margem de risco** | 10% |
| **Infraestrutura** | AWS (EC2, RDS, S3, CloudFront, Redis) |

---

## 💸 Estimativa de Custo Total

| Item | Cálculo | Valor (R$) |
|------|----------|-------------|
| **Mão de obra MVP (4 devs × 44 dias × 200)** | 4 × 44 × 200 | **R$ 35.200** |
| **Melhorias e refino (4 devs × 44 dias × 200)** | 4 × 44 × 200 | **R$ 35.200** |
| **Margem de risco (10%)** | 10% de R$ 70.400 | **R$ 7.040** |
| **Infraestrutura AWS (4 meses)** | 800 × 4 | **R$ 3.200** |
| | **💰 Total estimado:** | **R$ 80.640** |

---

## 🗓️ Cronograma Detalhado

### 🧱 **Fase 1 — MVP (2 Meses / 44 dias úteis)**  
**Objetivo:** entregar o produto mínimo viável com as principais funcionalidades do sistema.

#### **Mês 1 — Fundação e Estrutura Base**
- Kickoff e definição técnica  
- Setup de repositórios, CI/CD e infraestrutura AWS  
- Modelagem de dados (usuários, eventos, ingressos, lotes)  
- Módulo de autenticação (cadastro, login, JWT)  
- Protótipo de interface (Figma)  
- CRUD de eventos (back + front básico)

#### **Mês 2 — Funcionalidades Principais**
- Fluxo completo de compra de ingressos  
- Geração de QR Code único por ingresso  
- Painel do produtor (criação e visualização de eventos)  
- Carteira de ingressos (meus ingressos + QR Code)  
- Listagem pública de eventos  
- Testes automatizados básicos e deploy do MVP  

---

### 🚀 **Fase 2 — Melhorias e Estabilização (2 Meses / 44 dias úteis)**  
**Objetivo:** refinar a experiência, performance e segurança do sistema.

#### **Mês 3 — Refinamento e UX**
- Filtros avançados (categoria, cidade, data)  
- Transferência de ingressos entre usuários  
- Ajustes de UI/UX e responsividade (mobile-first)  
- Cache com Redis e otimização de queries SQL  
- Polimento visual e padronização de componentes  

#### **Mês 4 — Performance, Monitoramento e Entrega Final**
- Monitoramento (CloudWatch, logs, alertas)  
- Otimizações de performance e imagens  
- Revisão de segurança (rate limit, autenticação, SQL injection)  
- Documentação técnica e de APIs  
- Testes integrados e stress testing  
- Deploy final em produção  
- Retrospectiva e encerramento do ciclo de melhorias  

---

### 🔧 **Fase 3 — Manutenção Leve (2 Meses Pós-Entrega)**
**Objetivo:** manter o sistema estável, corrigir falhas e aplicar pequenos ajustes.  

**Atividades previstas:**
- Monitoramento e logs contínuos  
- Correção de bugs e falhas operacionais  
- Ajustes de layout e responsividade  
- Suporte a usuários iniciais e produtores cadastrados  
- Preparação para novas versões (v2.0)  

---

## ⚙️ Distribuição de Esforço

| Área | Percentual | Responsável |
|------|-------------|--------------|
| Back-end (API, banco, segurança, QR) | 45% | 3 devs |
| Front-end (UI/UX, integração) | 35% | 1 dev |
| Infraestrutura (AWS, CI/CD, logs) | 10% | 1 dev parcial |
| Testes e revisões | 5% | Todos |
| Gestão e documentação | 5% | Gabriel Lima |

---

## ✅ Considerações Finais

- A nova estimativa inclui **2 meses adicionais de manutenção leve**, garantindo estabilidade e suporte inicial.  
- O custo total de **R$ 85.640** cobre todo o ciclo: MVP, melhorias, gestão, infraestrutura e suporte.  
- O projeto mantém um **escopo realista**, com entregas contínuas e escalabilidade técnica.  
- A infraestrutura AWS está configurada para **crescimento seguro**, com cache, backups automáticos e monitoramento.  
- A estimativa final reflete um investimento **profissional e sustentável**, com base em boas práticas de engenharia de software.  

---
