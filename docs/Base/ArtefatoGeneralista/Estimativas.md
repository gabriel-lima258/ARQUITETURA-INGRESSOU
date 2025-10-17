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
| **Mão de obra MVP** (3 devs × 44 dias × R$400) | 3 × 44 × 400         | R$ 52.800     |
| **Margem de risco (10%)**                      | 10% de R$ 52.800     | R$ 5.280      |
| **Infraestrutura AWS (6 meses)**               | R$ 800/mês         | R$ 4.800      |
| **Designer + Gestão leve (fixo)**              | Valor estimado       | R$ 2.000      |
| **Manutenção pós-MVP (1 dev por 3 meses)**     | 3 × 22 dias × R$ 400 | R$ 23.500     |
|                                                | **Total estimado:**  | **R$ 92.280** |

---

## 🗓️ Cronograma por Semanas (MVP - 2 meses)

| Semana | Atividades                                                             | Responsáveis | Entregáveis                                        |
| ------ | ---------------------------------------------------------------------- | ------------ | -------------------------------------------------- |
| **1**  | Kickoff, arquitetura, setup AWS, CI/CD                                 | Todos        | Infra pronta, CI/CD funcional, repositórios ativos |
| **2**  | Protótipo UI/UX, modelagem banco, endpoints auth e usuários            | Front + Back | Login/cadastro funcional, protótipos               |
| **3**  | CRUD de eventos, lógica de compra e persistência de ingressos          | Back-end     | API de eventos e compras operante                  |
| **4**  | Telas de listagem e compra de ingressos, integração inicial front-back | Todos        | MVP inicial funcional (sem carteira)               |
| **5**  | Carteira de ingressos (visualização e QR), edição de perfil            | Back + Front | Acesso a ingressos, edição funcional               |
| **6**  | Transferência de ingressos, aceite e notificação                       | Back + Front | API de transferência, aceitação                    |
| **7**  | Filtros de eventos (cidade, categoria), responsividade                 | Front-end    | Filtros aplicados                                  |
| **8**  | Testes automatizados, revisão de performance e segurança               | Todos        | Validações, segurança básica                       |
| **9**  | Deploy do MVP em produção na AWS                                       | DevOps leve  | MVP no ar                                          |
| **10** | Documentação técnica, repasse para manutenção, check final             | Todos        | Docs técnicos, diagrama, instruções de deploy      |

---

## ✅ Considerações Finais

* O projeto considera um **MVP profissional escalável**, com boa arquitetura desde o início.
* A estimativa contempla **manutenção inicial por 3 meses** após entrega.
* A infraestrutura na AWS foi prevista para escalar com cache (Redis), banco (RDS) e backup automático.
* Custos de QA foram absorvidos na etapa de testes automatizados e revisão entre devs.
* A margem de risco de 10% cobre atrasos ou tarefas inesperadas.
