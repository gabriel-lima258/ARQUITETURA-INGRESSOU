# Benchmarking em Relação a Gestão de Produtores e Lotes

## Sumário

* [Sympla](#sympla)
* [Eventbrite](#eventbrite)
* [Ingresse](#ingresse)
* [BlueTicket](#blueticket)
* [Bilheteria Digital](#bilheteria-digital)
* [Hotmart (catálogo de produtos complementares)](#hotmart-catálogo-de-produtos-complementares)
* [Requisitos Elicitados](#requisitos-elicitados)
  * [Requisitos Funcionais](#requisitos-funcionais)
  * [Requisitos Não-Funcionais](#requisitos-não-funcionais)

---

### [Sympla](https://www.sympla.com.br)

<div align="center">
    Figura 1: Sympla — Gestão de Produtor e Lotes (ilustrativo)
    <br>
    <img src="assets/Benchmarking/sympla.png" width="560" alt="Sympla - gestão de produtor">
    <br>
    <b>Fonte:</b> <a href="https://www.sympla.com.br">Sympla</a>.
    <br>
</div>

#### Foco observado
Gestão autônoma pelo organizador, com **criação/edição de evento**, **configuração de lotes**, cupons e painel com **vendas e repasses**.

#### Recursos-chave
- Cadastro do **organizador** (dados fiscais e pagamentos).
- **Múltiplos lotes** por evento (nome, preço, quantidade, período).
- Tipos de ingresso (inteira, meia, VIP, cortesia).
- **Relatórios** e exportação CSV.
- Configuração de **políticas** (reembolso, meia-entrada).

#### Pontos positivos
- Fluxo de lotes intuitivo, com status e janelas de venda.
- Painel com métricas e exportação de dados.

#### Pontos a observar
- Customizações avançadas de regras podem depender de plano/atendimento.

---

### [Eventbrite](https://www.eventbrite.com.br)

<div align="center">
    Figura 2: Eventbrite — Painel do Organizador (ilustrativo)
    <br>
    <img src="assets/Benchmarking/evenbrite.png" width="560" alt="Eventbrite - painel do organizador">
    <br>
    <b>Fonte:</b> <a href="https://www.eventbrite.com.br">Eventbrite</a>.
    <br>
</div>

#### Foco observado
Ferramentas para **organizadores** com ênfase em **promoção**, **integrações** e **relatórios** avançados.

#### Recursos-chave
- Editor modular de evento.
- Gestão de ingressos/lotes e **códigos promocionais**.
- **Integrações** (CRM, e-mail marketing).
- Widgets de incorporação.

#### Pontos positivos
- Ecossistema de integrações que amplia a gestão do produtor.
- Relatórios com recortes e visualizações úteis.

#### Pontos a observar
- Onboarding e variedade de opções podem elevar a curva de aprendizado.

---

### [Ingresse](https://www.ingresse.com)

<div align="center">
    Figura 3: Ingresse — Operação e Acesso (ilustrativo)
    <br>
    <img src="assets/Benchmarking/ingresse.png" width="560" alt="Ingresse - operação de acesso">
    <br>
    <b>Fonte:</b> <a href="https://www.ingresse.com">Ingresse</a>.
    <br>
</div>

#### Foco observado
Ambiente para entretenimento com atenção a **operacionalização** (picos de venda e **portaria**).

#### Recursos-chave
- Lotes com controle de **estoque** e períodos.
- Operação de **check-in** e logs.
- Painel com acompanhamento de vendas.

#### Pontos positivos
- Capacidade de lidar com alto volume.
- Integração natural com o fluxo de acesso (QR).

#### Pontos a observar
- Customizações de catálogo extra (produtos) variam por parceria.

---

### [BlueTicket](https://www.blueticket.com.br)

<div align="center">
    Figura 4: BlueTicket — Gestão Regional e Lotes (ilustrativo)
    <br>
    <img src="assets/Benchmarking/blue.png" width="560" alt="BlueTicket - gestão de lotes">
    <br>
    <b>Fonte:</b> <a href="https://www.blueticket.com.br">BlueTicket</a>.
    <br>
</div>

#### Foco observado
Gestão com **curadoria por cidades/regiões**, controle de **lotes** e **check-in**.

#### Recursos-chave
- Lotes por categoria/tipo de acesso.
- **Relatórios** para organizador.
- Aplicativos/soluções de **portaria**.

#### Pontos positivos
- Organização por localização ajuda a descoberta.
- Confiabilidade de check-in em campo.

#### Pontos a observar
- Menor foco em produtos complementares acoplados ao ticket.

---

### [Bilheteria Digital](https://www.bilheteriadigital.com)

<div align="center">
    Figura 5: Bilheteria Digital — Produtor (ilustrativo)
    <br>
    <img src="assets/Benchmarking/bilheteria.png" width="560" alt="Bilheteria Digital - produtor">
    <br>
    <b>Fonte:</b> <a href="https://www.bilheteriadigital.com">Bilheteria Digital</a>.
    <br>
</div>

#### Foco observado
**Simplicidade operacional** e amplitude de categorias.

#### Recursos-chave
- Criação de evento/lotes.
- Painel de vendas e repasses.
- Filtros de listagem por cidade/data/categoria.

#### Pontos positivos
- Onboarding simples para produtores iniciantes.
- Amplo leque de categorias.

#### Pontos a observar
- Menos profundidade em automações e catálogo extra.

---

### [Hotmart (catálogo de produtos complementares)](https://www.hotmart.com/)

<div align="center">
    Figura 6: Hotmart — Produtos e Catálogo (ilustrativo)
    <br>
    <img src="assets/Benchmarking/hotmart.png" width="560" alt="Hotmart - catálogo de produtos">
    <br>
    <b>Fonte:</b> <a href="https://www.hotmart.com">Hotmart</a>.
    <br>
</div>

#### Foco observado
Gestão de **produtos** (digitais/serviços) com **regras de venda**, **entrega/fulfillment** e **comissionamento**.

#### Por que observar no contexto Ingressou
- **Produtos vinculados ao evento** (mentorias, workshops, meet & greet) exigem gestão similar a catálogo: **estoque**, **janela de venda**, **método de entrega** (link, voucher, agendamento), **regras de dependência** (ex.: só vender com ingresso).
- **Relatórios** e conciliação financeira por item.

---

## Requisitos Elicitados

> Requisitos derivados com foco em **Gestão de Produtores e Lotes** para a plataforma **Ingressou**.

### Requisitos Funcionais

| Código | Requisito Funcional                                                                                     | Objetivo                                                                                     | Origem (referência)                  |
|--------|----------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------|--------------------------------------|
| RF-GP-01 | Perfil de produtor com dados fiscais, KYC e chave de repasse (PIX).                                     | Habilitar vendas e repasses com conformidade.                                                | Sympla, práticas do setor            |
| RF-GP-02 | Painel do produtor com visão geral: eventos, status, vendas, lotes e repasses.                          | Facilitar gestão operacional e financeira.                                                   | Sympla, Bilheteria Digital           |
| RF-GP-03 | CRUD de eventos com estados (rascunho, publicado, encerrado).                                           | Controlar ciclo de vida do evento.                                                           | Sympla, Eventbrite                   |
| RF-GP-04 | Gestão de lotes: nome, preço, quantidade, janela de venda, status e prioridade de exibição.             | Orquestrar disponibilidade e precificação por fase.                                          | Sympla, Ingresse, BlueTicket         |
| RF-GP-5  | Regras de tipos de ingresso por lote (inteira, meia, VIP, cortesia) e limites por CPF.                  | Conformidade legal e controle de abuso.                                                      | Sympla, BlueTicket                   |
| RF-GP-06 | Edição restrita após publicação (campos críticos protegidos; preservar integridade das vendas).         | Evitar inconsistências em vendas em andamento.                                               | Boas práticas                        |
| RF-GP-07 | Duplicação de evento (gera novo rascunho sem vendas).                                                   | Acelerar criação de eventos recorrentes.                                                     | Padrão de mercado                    |
| RF-GP-08 | Políticas configuráveis (reembolso, meia-entrada, cancelamento).                                        | Adaptar operação a regras do produtor/legislação.                                            | Sympla, Eventbrite                   |
| RF-GP-09 | Cupons e promoções por evento/lote (código, %/R$, validade, limite).                                    | Suporte a campanhas de aquisição e alavancas de venda.                                       | Eventbrite                           |
| RF-GP-10 | Catálogo de produtos vinculados ao evento (mentorias, workshops etc.) com dependência de ingresso.      | Aumentar ticket médio e manter consistência de venda.                                        | Hotmart (analogia), observação setor |
| RF-GP-11 | Estoque de produto (fixo/ilimitado) e janela de venda (início/fim).                                      | Controlar disponibilidade e urgência.                                                        | Hotmart                              |
| RF-GP-12 | Relatórios exportáveis (CSV) por evento/lote/produto com bruto, taxa, líquido e quantidade.             | Conciliação e tomada de decisão.                                                             | Sympla, Bilheteria Digital           |
| RF-GP-13 | Auditoria: logar criação/edição/publicação/encerramento/ativação-inativação com usuário e timestamp.    | Rastreabilidade e compliance.                                                                | Boas práticas                        |
| RF-GP-14 | Encerramento de evento bloqueando novas vendas e check-in após a data final.                             | Controle operacional do ciclo de vida.                                                       | Padrão do setor                      |

### Requisitos Não-Funcionais

| Código | Requisito Não-Funcional                                                                 | Objetivo                                                                        | Origem (referência)         |
|--------|------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------|-----------------------------|
| RNF-GP-01 | Painel responsivo (mobile-first) com filtros e paginação eficientes.                    | Produtores gerirem do celular com boa usabilidade.                              | Sympla, Eventbrite          |
| RNF-GP-02 | Tempo de resposta P90 ≤ 2s para listagens e operações comuns do painel.                 | Rapidez operacional para decisões em tempo real.                                | Ingresse (boa prática)      |
| RNF-GP-03 | Controle de concorrência e travas de estoque (lotes/produtos) para evitar oversell.     | Integridade de estoque em picos de venda.                                       | Boas práticas               |
| RNF-GP-04 | Logs e auditoria estruturados com retenção mínima definida (ex.: 180 dias).             | Suporte a investigações e conformidade.                                         | Boas práticas               |
| RNF-GP-05 | Permissões por papel (produtor, staff de portaria, financeiro) com princípio de mínimo privilégio. | Segurança e segregação de funções.                                              | Padrão do setor             |
| RNF-GP-06 | Exportações CSV com limites e paginação para não afetar performance do sistema.         | Estabilidade sob alto volume de dados.                                          | Boas práticas               |
| RNF-GP-07 | Acessibilidade (WCAG 2.1 AA) no painel do produtor.                                     | Inclusão e conformidade.                                                        | Padrão do setor             |
| RNF-GP-08 | Disponibilidade mensal mínima de 99,5% no módulo de gestão.                             | Confiabilidade para operações críticas.                                         | Prática comum               |

---

## Histórico de versão

| Versão | Alteração                                             | Responsável  | Data       |
|-------:|--------------------------------------------------------|--------------|------------|
| 1.0    | Criação do benchmarking “Gestão de Produtores e Lotes” | Gabriel Lima | 15/10/2025 |
