# Brainstorming — Ingressou

> **Versão:** 1.1  
> **Data:** Outubro de 2025  
> **Autor:** Gabriel Lima  
> **Projeto:** Ingressou — Plataforma Web de Venda e Gestão de Ingressos

---

## Sumário

* [Introdução](#introdução)
* [Objetivos](#objetivos)
* [Metodologia](#metodologia)
* [Mapa Mental](#mapa-mental)
* [Quadro de Insights](#quadro-de-insights)
  * [Modelo de Negócio](#modelo-de-negócio)
  * [Produto e Funcionalidades](#produto-e-funcionalidades)
  * [Usuários e Personas](#usuários-e-personas)
  * [Experiência e Interface (UX/UI)](#experiência-e-interface-uxui)
  * [Regras e Conformidade](#regras-e-conformidade)
  * [Diferenciais Estratégicos](#diferenciais-estratégicos)
* [Síntese dos Padrões e Direcionamentos](#síntese-dos-padrões-e-direcionamentos)
* [Caminho Estratégico Inicial](#caminho-estratégico-inicial)
* [Conclusão](#conclusão)
* [Bibliografia](#bibliografia)
* [Histórico de versão](#histórico-de-versão)

---

## Introdução

O brainstorming é uma técnica para **gerar e organizar ideias** sem julgamentos, útil para **explorar escopo, oportunidades e riscos** no início de projetos. Inspirado em Osborn (1953), seu objetivo é **estimular o pensamento criativo** e ampliar alternativas de solução.

Neste artefato, registramos o brainstorming inicial do **Ingressou**, já **adaptado** às decisões recentes do projeto:

- **Eventos criados exclusivamente pelo Administrador**.  
- **Lotes** encerram pelo **primeiro limite atingido** (tempo *ou* quantidade).  
- **Cupons de influenciadores** para o comprador (sem cashback ao usuário).  
- **Cashback financeiro destinado ao Produtor** (saldo no painel, abatimento de taxas/campanhas).  
- Uso de **mensageria/filas** para jobs assíncronos e **cache** para alto desempenho.

---

## Objetivos

- Registrar ideias e **agrupar temas** que compõem o MVP e evoluções.  
- **Alinhar** visão de produto aos **requisitos** e **regras de negócio** recém-definidas.  
- Servir de **base** para elicitação, priorização (MVP) e roadmap.

---

## Metodologia

- Sessão de **brainstorming individual** e **benchmarking setorial** (plataformas de ingressos e pagamentos).  
- Organização por **mapa mental** (Draw.io) e consolidação em **Quadro de Insights**.  
- Integração das **decisões arquiteturais** (mensageria, cache) e de **governança** (admin cria eventos).

---

## Mapa Mental

> **Observação:** Para visualizar em detalhes, clique com o botão direito na imagem e abra em nova aba para dar zoom.

<div align="center">
  Figura 1: Mapa Mental — Brainstorming Ingressou
  <br>
  <img src="assets/ArtefatosGeneralistas/brainstorming.png" alt="Mapa Mental do Brainstorming da Ingressou">
  <br>
  <b>Autor:</b> <a href="https://github.com/gabriel-lima258">Gabriel Lima</a>.
</div>

---

## Quadro de Insights

> O quadro agrupa tópicos do mapa mental em **seis eixos**, destacando **insights**, **oportunidades** e **direcionamentos** já **compatíveis** com as regras atualizadas do projeto.

### Modelo de Negócio

| **Insights Principais** | **Padrões e Oportunidades Identificadas** | **Direcionamento para o Projeto** |
|---|---|---|
| - **Taxa de 8%** sobre cada ingresso. <br> - **Cashback ao Produtor** (ex.: **2%** do líquido configurável) como incentivo. <br> - **Split automático** e repasse D+X. <br> - Suporte a múltiplos segmentos: **shows, palestras, teatro, igrejas, conferências**. <br> - Possibilidade de **venda de produtos** vinculados ao evento (mentorias, workshops, pacotes). | - Produtores valorizam **transparência** de taxas e **previsibilidade** de repasses. <br> - Há espaço para **pequenos e médios** organizadores. <br> - Incentivos financeiros ao **produtor** (cashback) favorecem adesão e retenção. | - Tornar **visível** no painel a composição de preço, taxas, split e saldo de cashback. <br> - Oferecer **planos** por porte (básico, premium, corporativo). <br> - **Política de cashback** configurável por contrato. |

### Produto e Funcionalidades

| **Insights Principais** | **Padrões e Oportunidades Identificadas** | **Direcionamento para o Projeto** |
|---|---|---|
| - **Admin cria/pública** eventos. <br> - **Lotes** com **janela de venda** e **quantidade máxima**; **encerra pelo primeiro limite**. <br> - Tipos de ingresso: **inteira, meia, VIP, cortesia**. <br> - **Checkout** com **PIX** e **cartão** (3DS/antifraude). <br> - **Cupom de influenciador** no checkout (percentual/fixo, vigência, limites). <br> - **Cashback do Produtor** no financeiro do painel (saldo/uso). <br> - **QR Code** antifraude e **check-in** online/offline. <br> - **Painel do Produtor** com vendas, repasses, relatórios CSV. | - Fluxo essencial: **publicar → vender → validar**. <br> - **Automação** reduz suporte (e-mails/WhatsApp, lembretes, confirmação, estorno). <br> - **Mensageria** evita gargalos; **cache** acelera páginas populares. | - MVP com foco em **conversão** (checkout claro, termos e resumo financeiro). <br> - **Filas** para e-mails/WhatsApp, webhooks, geração de QR e exportações. <br> - **Cache** (Redis) para listagens e páginas públicas de eventos. |

### Usuários e Personas

| **Insights Principais** | **Padrões e Oportunidades Identificadas** | **Direcionamento para o Projeto** |
|---|---|---|
| - **Usuário Comprador:** quer **agilidade, clareza** e **segurança**; usa **PIX**; aplica **cupom** (não recebe cashback). <br> - **Produtor:** precisa de **métricas em tempo real**, **previsibilidade** de repasse e **incentivo** (cashback). <br> - **Staff (Check-in):** validação **rápida** e **offline**. <br> - **Administrador:** **cria eventos**, define **lotes**, cuida de **políticas**, **cupons**, **fraudes**. | - Todos valorizam **simplicidade** e **transparência**. <br> - Produtores demandam **governança** e **confiabilidade**. | - Fluxos **separados por perfil**. <br> - **Dashboards** específicos (produtor/admin) com **indicadores práticos**. |

### Experiência e Interface (UX/UI)

| **Insights Principais** | **Padrões e Oportunidades Identificadas** | **Direcionamento para o Projeto** |
|---|---|---|
| - **UI responsiva** (mobile-first). <br> - Páginas de evento com **banner, descrição, locais, datas, lotes** e CTA claro. <br> - **Checkout** em poucos passos e **resumo** transparente (itens, taxas, total). <br> - **Envio automatizado** de ingresso por e-mail/WhatsApp. <br> - **PWA** para check-in. | - **Conversão** depende de clareza e velocidade. <br> - WhatsApp e carteiras digitais **aumentam confiança**. | - **Microfeedbacks** (loading, sucesso, erro). <br> - **Templates** consistentes e acessíveis (WCAG 2.1 AA). |

### Regras e Conformidade

| **Insights Principais** | **Padrões e Oportunidades Identificadas** | **Direcionamento para o Projeto** |
|---|---|---|
| - **LGPD**: consentimento, finalidade, exclusão sob demanda. <br> - **Meia-entrada**: **flag digital** e verificação no check-in. <br> - **Política de reembolso**: configurável e aplicada no checkout. <br> - **NFS-e**: emissão sobre **taxa da plataforma**. | - Clareza jurídica **reduz chargeback** e suporte. | - **Termos e políticas** visíveis no checkout. <br> - **Auditoria** de ações críticas (criar/publicar/cancelar/validar). |

### Diferenciais Estratégicos

| **Insights Principais** | **Padrões e Oportunidades Identificadas** | **Direcionamento para o Projeto** |
|---|---|---|
| - **Cashback para Produtor** (não ao usuário). <br> - **Cupons de influenciadores** para usuário (atribuição de vendas). <br> - **Antifraude** (QR assinado; anti-replay). <br> - **Split** automático e **mensageria** resiliente. <br> - **Cache** para alta performance. | - Produtor engaja com incentivos financeiros e **visibilidade de métricas**. | - **Painel financeiro** do produtor com **saldo de cashback**, **extratos** e **opções de uso** (abatimento de taxa/campanhas). |

---

## Síntese dos Padrões e Direcionamentos

1. **Governança:** **Administrador** centraliza a **criação/publicação** de eventos.  
2. **Oferta e demanda:** **Lotes** encerram por **tempo** ou **quantidade** — o que vier primeiro.  
3. **Comercial:** **Cupom de influenciador** direcionado ao comprador; **cashback** como **incentivo ao produtor**.  
4. **Arquitetura:** **Mensageria** para tarefas assíncronas críticas (webhooks, e-mails/WhatsApp, QR, exportações) e **cache** para leituras quentes.  
5. **Conversão & UX:** Checkout **rápido e transparente**; **páginas de evento** enxutas; **PWA** de check-in.  
6. **Conformidade & confiança:** **LGPD, auditoria, antifraude** e **políticas claras** no checkout.

---

## Caminho Estratégico Inicial

- **MVP** orientado ao fluxo **publicar (admin) → vender (checkout) → validar (check-in)**.  
- **Infra e performance:** mensageria (RabbitMQ/Kafka/SQS), cache (Redis), observabilidade (OTel/Sentry).  
- **Financeiro:** split, repasses e **cashback do produtor** visível e auditável.  
- **Crescimento:** aquisição por **influenciadores** (cupons e atribuição de vendas).  
- **Roadmap pós-MVP:** **revenda/transferência**, **assentos visuais**, **Wallets**, **white-label**.

---

## Conclusão

O brainstorming, **ajustado às decisões recentes**, consolidou uma visão de produto **coerente, enxuta e escalável**:  
governança por **Administrador**, **lotes** com suspensão por **tempo/quantidade**, **cupons** focados no comprador, **cashback** para **produtor**, e arquitetura com **mensageria** e **cache** para garantir **confiabilidade e desempenho**.

---

## Bibliografia

<a name="ref1"></a>  
[1] BESANT, Hanisha. *The journey of brainstorming*. *Journal of Transformative Innovation*, v. 2, n. 1, 2016. Disponível em: <https://www.regent.edu/journal/journal-of-transformative-innovation/the-history-of-brainstorming-alex-osborn/>. Acesso em: 4 abr. 2025.

---

## Histórico de versão

| Versão | Alteração | Responsável | Data |
|---:|---|---|---|
| 1.0 | Elaboração do documento | Gabriel Lima | 15/10/2025 |
| 1.1 | **Adequação às regras atualizadas** (admin cria eventos; lotes por tempo/quantidade; cupom de influenciador; cashback para produtor; mensageria e cache) | Gabriel Lima | 16/10/2025 |
