# Estimativa de Custo e Cronograma - Projeto Ingressou (MVP)

> **Versão:** 1.0
> **Data:** Outubro de 2025
> **Autor:** Gabriel Lima
> **Projeto:** Ingressou — Plataforma Web de Venda e Gestão de Ingressos

---

## 📊 Metodologia Utilizada

### Abordagem Híbrida: Bottom-Up + Delphi (Planning Poker leve)

A estimativa de custo, tempo e esforço do MVP do Ingressou baseou-se em duas técnicas complementares:

* **Bottom-Up Estimation**: decomposição funcional detalhada do escopo, considerando complexidade técnica e dependências.
* **Delphi/Planning Poker Leve**: estimativas consensuais feitas entre desenvolvedores experientes com base em discussão de esforço relativo.

### Premissas

* **Duração**: 2 meses úteis (44 dias de trabalho)
* **Carga horária**: 8h/dia por dev
* **Custo mão de obra**: R$ 400/dia (R$ 50/hora)
* **Equipe**: 3 desenvolvedores (2 back-end + 1 front-end)
* **Margem de risco**: 10%
* **Infraestrutura AWS com escalabilidade e cache (Redis, backups, etc)**
* **Sem equipe de QA dedicada (testes automatizados apenas)**
* **1 dev mantido após MVP para manutenção (3 meses)**

---

## 💸 Estimativa de Custo Total (MVP + Manutenção Inicial)

| Item                                           | Cálculo              | Valor (R$)    |
| ---------------------------------------------- | -------------------- | ------------- |
| **Mão de obra MVP** (3 devs × 45 dias × R$400) | 3 × 45 × 400         | R$ 52.800     |
| **Margem de risco (10%)**                      | 10% de R$ 52.800     | R$ 5.280      |
| **Infraestrutura AWS (6 meses)**               | R$ 800/mês           | R$ 4.800      |
| **Designer + Gestão leve (fixo)**              | Valor estimado       | R$ 2.000      |
| **Manutenção pós-MVP (1 dev por 3 meses)**     | 3 × 22 dias × R$ 400 | R$ 26.400     |
|                                                | **Total estimado:**  | **R$ 92.480** |

---

## 🗓️ Cronograma Detalhado por Dias (MVP - 2 meses úteis)

**Semana 1** (Dias 1–5):

* Kickoff do projeto
* Setup de repositórios, ambiente e CI/CD
* Provisionamento da AWS (EC2, S3, RDS, CloudFront)
* Definição de stack e arquitetura base
* Protótipos iniciais UI/UX (figma ou similar)

**Semana 2** (Dias 6–10):

* Modelagem do banco de dados (eventos, usuários, ingressos)
* Implementação da API de autenticação e cadastro/login
* Integração de autenticação no front-end
* Primeiros testes de login com feedback visual

**Semana 3** (Dias 11–15):

* CRUD de eventos no back-end (incluindo lotes)
* Estrutura da tela de criação e edição de eventos (admin)
* Começo da listagem pública de eventos com mock

**Semana 4** (Dias 16–20):

* Lógica de compra de ingressos no back-end (com vínculo ao lote)
* Geração de QR Code único por ingresso
* Integração com front: tela de compra e finalização

**Semana 5** (Dias 21–25):

* Criação da carteira de ingressos no front (tela de "meus ingressos")
* Edição de perfil do usuário
* Visualização dos QR Codes pela carteira

**Semana 6** (Dias 26–30):

* Transferência de ingressos: API de envio e aceite
* Atualização do QR após aceite
* Integração visual no front com feedback de aceite

**Semana 7** (Dias 31–35):

* Implementação dos filtros: cidade, estado, categorias de evento
* Ajustes de responsividade para mobile e tablets
* Polimento visual e estilização do front

**Semana 8** (Dias 36–40):

* Testes automatizados (unitários e integração)
* Validação de segurança básica (auth, rate limit, injeção)
* Revisão de performance (lazy load, otimização de imagens)

**Semana 9** (Dias 41–45):

* Deploy em produção (com CI/CD validado)
* Configuração final de DNS, HTTPS e backups
* Verificação de logs e métricas básicas (CloudWatch ou equivalente)

**Semana 10** (Dias 46–50):

* Documentação técnica (README, APIs, deploy, estrutura)
* Repasse para manutenção
* Retrospectiva final e encerramento do MVP

---

## ✅ Considerações Finais

* O projeto considera um **MVP profissional escalável**, com boa arquitetura desde o início.
* A estimativa contempla **manutenção inicial por 3 meses** após entrega.
* A infraestrutura na AWS foi prevista para escalar com cache (Redis), banco (RDS) e backup automático.
* Custos de QA foram absorvidos na etapa de testes automatizados e revisão entre devs.
* A margem de risco de 10% cobre atrasos ou tarefas inesperadas.

---
