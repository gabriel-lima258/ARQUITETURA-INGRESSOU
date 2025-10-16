# Diagramas de Ishikawa (Diagrama de Causa e Efeito) — Ingressou

## Sumário
- [Introdução](#introdução)
- [Objetivos](#objetivos)
- [Metodologia](#metodologia)
- [Foco no Projeto](#foco-no-projeto)
  - [Diagrama 6M — Projeto (Atrito no Checkout)](#diagrama-6m--projeto-atrito-no-checkout)
  - [Diagrama 4Ss — Projeto (Indisponibilidade em Picos)](#diagrama-4ss--projeto-indisponibilidade-em-picos)
- [Foco nos Usuários](#foco-nos-usuários)
  - [Diagrama 6M — Usuário (Baixa Conversão de Compra)](#diagrama-6m--usuário-baixa-conversão-de-compra)
  - [Diagrama 4Ss — Usuário 1 (Confiança e Segurança)](#diagrama-4ss--usuário-1-confiança-e-segurança)
  - [Diagrama 4Ss — Usuário 2 (Produtor com Dificuldade de Publicação)](#diagrama-4ss--usuário-2-produtor-com-dificuldade-de-publicação)
- [Conclusão](#conclusão)
- [Bibliografia](#bibliografia)
- [Histórico de versão](#histórico-de-versão)

---

## Introdução

O **Diagrama de Causa e Efeito** (Ishikawa/Espinha de Peixe) auxilia na identificação e organização das **causas potenciais** que levam a um **efeito/problema**. Nesta página, a técnica é aplicada ao **Ingressou**, plataforma de **venda e gestão de ingressos**, considerando desafios de **checkout/pagamento**, **picos de acesso**, **confiança** e **onboarding de produtores**.

---

## Objetivos

- Mapear causas-raiz dos problemas críticos do Ingressou.  
- Propor **ações preventivas** e **contramedidas** priorizadas.  
- Alinhar times de **produto, engenharia, operações e suporte**.

---

## Metodologia

Utilizam-se duas taxonomias:

- **6M**: *Mão de Obra, Método, Material, Máquina, Meio Ambiente, Medição*.  
- **4Ss**: *Ambiente (Surroundings), Fornecedores (Suppliers), Sistema (System), Habilidades (Skills)*.

---

## Foco no Projeto

### Diagrama 6M — Projeto (Atrito no Checkout)

**Problema (efeito):** *Atrito no checkout → abandono de carrinho / falhas de pagamento (PIX/cartão) / cupom não aplicado.*

<div align="center">
  <em>Figura 1 – Ishikawa 6M do problema “Atrito no Checkout”</em><br>
  <img src="assets/ArtefatosGeneralistas/atrasosEfeito.png" width="900">
</div>

#### Possíveis causas e ações preventivas

<details>
<summary><b>👥 Mão de Obra</b></summary>

| Causa | Ação Preventiva |
|---|---|
| Falta de alinhamento entre produto, engenharia e antifraude | Cerimônias semanais de alinhamento + SLAs de correção. |
| Suporte sem playbooks para erros de pagamento | Runbooks por gateway/retorno (3DS, soft-decline, reprocessamento). |
| Treinamento insuficiente sobre cupons | Guia de regras (escopo, validade, prioridade) + cenários de teste. |
</details>

<details>
<summary><b>🧭 Método</b></summary>

| Causa | Ação Preventiva |
|---|---|
| Passos desnecessários no fluxo | One-page checkout com validação in-line e auto-preenchimento. |
| Regras de cupom pouco claras | Resumo de regras no campo do cupom + mensagens de erro específicas. |
| Falta de retentativa inteligente | Retentativa com fallback (PIX→cartão; cartão soft-decline→retry). |
</details>

<details>
<summary><b>📦 Material (conteúdo/UI)</b></summary>

| Causa | Ação Preventiva |
|---|---|
| Textos genéricos de erro | Mensagens específicas por código do gateway. |
| Ausência de selos de segurança | Exibir 3DS, PCI, política de privacidade próximo ao CTA. |
| Confusão sobre taxas | Quebra do preço por item/taxa + destaque do benefício do cupom. |
</details>

<details>
<summary><b>🖥️ Máquina (tecnologia)</b></summary>

| Causa | Ação Preventiva |
|---|---|
| Latência alta no gateway | Timeout por etapa + fila assíncrona para callbacks de confirmação. |
| Falhas em webhooks | Reprocessamento idempotente + DLQ em mensageria. |
| Picos sem auto-scale | HPA/auto-scale + cache para catálogos e regras de preço. |
</details>

<details>
<summary><b>🌎 Meio Ambiente</b></summary>

| Causa | Ação Preventiva |
|---|---|
| Conectividade móvel instável | Persistência local do carrinho e retomada do checkout. |
| Sazonalidade (drops) | Pré-fila, limite por CPF/sessão, janelas por lote. |
</details>

<details>
<summary><b>📏 Medição</b></summary>

| Causa | Ação Preventiva |
|---|---|
| Falta de funil de conversão | Instrumentar eventos (view→add→pay→success) + dashboards. |
| Erros não rastreados por etapa | Observabilidade (logs/traces) por passo e por BIN/gateway. |
</details>

---

### Diagrama 4Ss — Projeto (Indisponibilidade em Picos)

**Problema (efeito):** *Fila/queda em datas de alta demanda; lentidão geral.*

<div align="center">
  <em>Figura 2 – Ishikawa 4Ss “Indisponibilidade em Picos”</em><br>
  <img src="assets/ArtefatosGeneralistas/picosEfeito.png" width="900">
</div>

#### Possíveis causas e ações preventivas

<details>
<summary><b>🌐 Ambiente (Surroundings)</b></summary>

| Causa | Ação Preventiva |
|---|---|
| Eventos muito concentrados | Janela escalonada por lotes e fila virtual. |
| Dependência de um único AZ/região | Multi-AZ, backups e testes de DR. |
</details>

<details>
<summary><b>🔗 Fornecedores (Suppliers)</b></summary>

| Causa | Ação Preventiva |
|---|---|
| Um único gateway de pagamento | Multi-gateway com failover e roteamento por BIN/issuer. |
| DNS sem health-check | DNS com health-check e baixa TTL. |
</details>

<details>
<summary><b>⚙️ Sistema (System)</b></summary>

| Causa | Ação Preventiva |
|---|---|
| Sem cache/circuit-breaker | Redis para catálogo/queries quentes + circuit-breaker/bulkheads. |
| Sem mensageria | RabbitMQ/Kafka para emissão de ingressos e e-mails. |
| DB write-heavy | Replicação (primário/leitura), índices e partição por evento. |
</details>

<details>
<summary><b>🧠 Habilidades (Skills)</b></summary>

| Causa | Ação Preventiva |
|---|---|
| Falta de caos engineering | Testes de carga e game days trimestrais. |
| On-call sem runbooks | Playbooks e simulações de incidentes. |
</details>

---

### Diagrama 4Ss — Usuário 1 (Confiança e Segurança)

**Problema (efeito):** *Usuários hesitam em pagar por dúvidas de segurança/privacidade.*

<div align="center">
  <em>Figura 4 – Ishikawa 4Ss “Confiança e Segurança”</em><br>
  <img src="assets/ArtefatosGeneralistas/segurancaEfeito.png" width="900">
</div>

#### Possíveis causas e ações preventivas

<details>
<summary><b>🌐 Ambiente</b></summary>

| Causa | Ação Preventiva |
|---|---|
| Notícias de golpes no setor | Página “Como evitamos fraudes” + validação de QR assinada. |
</details>

<details>
<summary><b>🔗 Fornecedores</b></summary>

| Causa | Ação Preventiva |
|---|---|
| Gateways desconhecidos | Exibir nomes dos parceiros/certificações. |
</details>

<details>
<summary><b>⚙️ Sistema</b></summary>

| Causa | Ação Preventiva |
|---|---|
| Falta de 3DS/anti-fraude | 3DS, device fingerprint e velocity checks. |
| Ausência de política de dados | Política LGPD clara e consentimento explícito. |
</details>

<details>
<summary><b>🧠 Habilidades</b></summary>

| Causa | Ação Preventiva |
|---|---|
| Atendimento não sabe explicar segurança | Script simples sobre TLS, tokenização e QR assinado. |
</details>

---

## Conclusão

Os diagramas evidenciam causas estruturais para os principais efeitos indesejados do **Ingressou** (atrito no checkout, quedas em picos, hesitação por segurança e onboarding difícil). As **ações preventivas** priorizam:
1. **UX fluida** (one-page checkout, mensagens claras, tour guiado).  
2. **Confiabilidade** (cache, mensageria, replicação, multi-gateway).  
3. **Observabilidade e dados** (funis, métricas, testes de carga).  
4. **Educação/atendimento** (playbooks, scripts e conteúdos de confiança).

---

## Bibliografia

1. APRENDENDO GESTÃO. *Diagrama de Ishikawa (Ferramenta da Qualidade): Teoria + Exemplo Prático*.  
2. FORLOGIC. *Diagrama de Ishikawa*.  
3. KIMIA CONSULTORIA. *Análise de causa raiz com o Diagrama de Ishikawa (6M)*.  
4. MINITAB. *Overview for Cause-and-Effect Diagram*.  
5. SOARES, Vitor. *Diagrama de Ishikawa: o que é, para que serve e como usar*.

---

## Histórico de versão

| Versão | Alteração | Responsável | Data |
|---|---|---|---|
| 1.0 | Adaptação dos Diagramas de Ishikawa para o Ingressou | Gabriel Lima | 16/10/2025 |
