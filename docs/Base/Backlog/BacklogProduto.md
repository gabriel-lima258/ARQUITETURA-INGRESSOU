# Backlog de Produto — Ingressou

> **Versão:** 1.0  
> **Data:** Outubro de 2025  
> **Autor:** Gabriel Lima  
> **Projeto:** Ingressou — Plataforma Web de Venda e Gestão de Ingressos  

---

## Sumário

- [Introdução](#introdução)
- [Visão Geral do Backlog](#visão-geral-do-backlog)
- [Legenda de Priorização](#legenda-de-priorização)
- [Épicos e Features](#épicos-e-features)
  - [Épico 1: Autenticação e Gestão de Usuários](#épico-1-autenticação-e-gestão-de-usuários)
  - [Épico 2: Descoberta e Busca de Eventos](#épico-2-descoberta-e-busca-de-eventos)
  - [Épico 3: Gestão de Produtores](#épico-3-gestão-de-produtores)
  - [Épico 4: Criação e Gestão de Eventos](#épico-4-criação-e-gestão-de-eventos)
  - [Épico 5: Venda e Checkout](#épico-5-venda-e-checkout)
  - [Épico 6: Ingressos e QR Code](#épico-6-ingressos-e-qr-code)
  - [Épico 7: Check-in e Validação](#épico-7-check-in-e-validação)
  - [Épico 8: Transferência de Ingressos](#épico-8-transferência-de-ingressos)
  - [Épico 9: Administração e Auditoria](#épico-9-administração-e-auditoria)
  - [Épico 10: Infraestrutura e Não Funcionais](#épico-10-infraestrutura-e-não-funcionais)
- [Roadmap MVP](#roadmap-mvp)
- [Tabela Consolidada do Backlog](#tabela-consolidada-do-backlog)
- [Métricas de Sucesso](#métricas-de-sucesso)
- [Histórico de Versão](#histórico-de-versão)

---

## Introdução

Este documento apresenta o **Backlog de Produto** do **Ingressou**, organizando os requisitos funcionais e não funcionais em **Épicos**, **Features** e **User Stories**, priorizados conforme a importância estratégica para o MVP.

O backlog foi estruturado com base nos documentos:
- [Requisitos Elicitados](/Base/ArtefatoGeneralista/RequisitosElicitados.md)
- [Diagrama de Casos de Uso](/Modelagem/ModelagemOrganizacional/DiagramaCasosUso.md)
- [5W2H](/Base/ArtefatoGeneralista/5W2H.md)

---

## Visão Geral do Backlog

O backlog está organizado em **10 Épicos principais**, totalizando **52 Requisitos Funcionais (RF)** e **28 Requisitos Não Funcionais (RNF)** identificados na versão 1.5 dos Requisitos Elicitados.

**Distribuição por Prioridade:**
- **Alta:** 32 RFs (MVP crítico)
- **Média:** 20 RFs (Importante para MVP)
- **Baixa:** 1 RF (Melhorias futuras)

---

## Legenda de Priorização

| Prioridade | Descrição | Exemplos |
|---|---|---|
| **🔴 Crítica** | Bloqueante para MVP; sem isso o sistema não funciona | Autenticação, Pagamento, Emissão de Ingressos |
| **🟠 Alta** | Essencial para MVP; funcionalidade principal | Busca de Eventos, Checkout, Check-in |
| **🟡 Média** | Importante mas não bloqueante; pode ser simplificado | Recuperação de Senha, Meia-entrada |
| **🟢 Baixa** | Nice-to-have; melhoria futura | URLs Amigáveis, Recursos avançados |

---

## Épicos e Features

### Épico 1: Autenticação e Gestão de Usuários

**Objetivo:** Permitir que usuários se cadastrem, autentiquem e gerenciem seus perfis na plataforma.

| ID | Feature | User Story | Prioridade | Story Points | RF Relacionado |
|---|---|---|---|---|---|
| **E1-F1** | **Cadastro de Usuário** | **US-001:** Como **usuário não cadastrado**, eu quero **me cadastrar com e-mail/senha ou login social (Google/Apple)** para **acessar a plataforma**. | 🔴 Crítica | 8 | RF01 |
| | | **Critérios de Aceitação:**<br>- Formulário com validação de e-mail<br>- Opção de login social (Google/Apple)<br>- Verificação por OTP/e-mail<br>- Aceite obrigatório de termos LGPD | | | |
| **E1-F2** | **Login e Sessão** | **US-002:** Como **usuário cadastrado**, eu quero **fazer login via e-mail/senha ou social** para **acessar minha conta**. | 🔴 Crítica | 5 | RF02, RF03 |
| | | **Critérios de Aceitação:**<br>- Login com e-mail/senha ou Google/Apple<br>- Rate limiting após 5 tentativas<br>- JWT (1h) e refresh token (7d)<br>- Rotação e revogação de tokens | | | |
| **E1-F3** | **Recuperação de Senha** | **US-003:** Como **usuário**, eu quero **recuperar minha senha** para **acessar minha conta quando esquecer a senha**. | 🟡 Média | 5 | RF04 |
| | | **Critérios de Aceitação:**<br>- Link de redefinição por e-mail<br>- Expiração em 30 minutos<br>- Cooldown entre solicitações | | | |
| **E1-F4** | **Gestão de Perfil** | **US-004:** Como **usuário autenticado**, eu quero **editar meus dados pessoais (exceto CPF)** para **manter minhas informações atualizadas**. | 🟡 Média | 5 | RF05 |
| | | **Critérios de Aceitação:**<br>- Edição de nome, e-mail, telefone<br>- CPF não editável<br>- Gerenciamento de provedores sociais<br>- Validação de dados | | | |

---

### Épico 2: Descoberta e Busca de Eventos

**Objetivo:** Permitir que usuários descubram e encontrem eventos através de busca, filtros e navegação.

| ID | Feature | User Story | Prioridade | Story Points | RF Relacionado |
|---|---|---|---|---|---|
| **E2-F1** | **Busca Global** | **US-005:** Como **usuário**, eu quero **buscar eventos por nome, local ou artista** para **encontrar eventos de interesse**. | 🟠 Alta | 8 | RF06 |
| | | **Critérios de Aceitação:**<br>- Campo de busca com autocompletar<br>- Busca em nome, local, artista, descrição<br>- Resultados paginados<br>- Cache para consultas frequentes | | | |
| **E2-F2** | **Filtros por Localização** | **US-006:** Como **usuário**, eu quero **filtrar eventos por cidade e UF** para **encontrar eventos próximos**. | 🟠 Alta | 8 | RF07 |
| | | **Critérios de Aceitação:**<br>- Autocompletar de cidades<br>- Seleção múltipla de UFs<br>- Persistência de filtros na URL<br>- Índices otimizados por cidade/UF | | | |
| **E2-F3** | **Filtros por Categoria** | **US-007:** Como **usuário**, eu quero **filtrar eventos por categoria** para **encontrar tipos específicos de eventos**. | 🟠 Alta | 5 | RF08 |
| | | **Critérios de Aceitação:**<br>- Lista de categorias disponíveis<br>- Seleção múltipla<br>- Filtro combinado com outros critérios | | | |
| **E2-F4** | **Filtros por Data** | **US-008:** Como **usuário**, eu quero **filtrar eventos por faixa de datas** para **planejar minha participação**. | 🟠 Alta | 5 | RF09 |
| | | **Critérios de Aceitação:**<br>- Períodos pré-definidos (hoje, fim de semana, próxima semana)<br>- Faixa personalizada<br>- Filtro combinado | | | |
| **E2-F5** | **Ordenação e URLs Amigáveis** | **US-009:** Como **usuário**, eu quero **ordenar eventos por data, popularidade ou preço** e **compartilhar URLs** para **facilitar descoberta**. | 🟡 Média | 5 | RF10, RF11 |

---

### Épico 3: Gestão de Produtores

**Objetivo:** Permitir que administradores cadastrem produtores e que produtores acompanhem seus eventos.

| ID | Feature | User Story | Prioridade | Story Points | RF Relacionado |
|---|---|---|---|---|---|
| **E3-F1** | **Onboarding de Produtor** | **US-010:** Como **administrador**, eu quero **cadastrar produtores com CNPJ/CPF e dados bancários** para **habilitar gestão de eventos**. | 🔴 Crítica | 13 | RF12, RF13 |
| | | **Critérios de Aceitação:**<br>- Formulário de cadastro completo<br>- Validação de CNPJ/CPF (Receita Federal)<br>- Validação de chave PIX<br>- KYC básico<br>- Envio de credenciais por e-mail | | | |
| **E3-F2** | **Painel do Produtor** | **US-011:** Como **produtor**, eu quero **visualizar métricas dos meus eventos vinculados** para **acompanhar desempenho**. | 🟠 Alta | 8 | RF14 |
| | | **Critérios de Aceitação:**<br>- Dashboard com vendas, check-ins, repasses<br>- Cashback acumulado<br>- Exportação CSV<br>- Somente leitura dos eventos vinculados | | | |

---

### Épico 4: Criação e Gestão de Eventos

**Objetivo:** Permitir que administradores criem, editem e publiquem eventos e lotes.

| ID | Feature | User Story | Prioridade | Story Points | RF Relacionado |
|---|---|---|---|---|---|
| **E4-F1** | **Criação de Evento** | **US-012:** Como **administrador**, eu quero **criar eventos com dados completos** para **disponibilizar eventos na plataforma**. | 🔴 Crítica | 13 | RF15 |
| | | **Critérios de Aceitação:**<br>- Formulário com nome, descrição, banner<br>- Localização (endereço, cidade, UF)<br>- Datas início/fim<br>- Seleção obrigatória de categoria<br>- Status inicial: RASCUNHO | | | |
| **E4-F2** | **Criação de Lotes** | **US-013:** Como **administrador**, eu quero **criar lotes para eventos** para **definir preços e disponibilidade**. | 🔴 Crítica | 13 | RF21, RF22, RF23 |
| | | **Critérios de Aceitação:**<br>- Nome, preço, quantidade total<br>- Janela de venda (início/fim)<br>- Tipo de ingresso (inteira, meia, VIP, cortesia)<br>- Encerramento automático por tempo ou quantidade | | | |
| **E4-F3** | **Publicação de Evento** | **US-014:** Como **administrador**, eu quero **publicar eventos** para **disponibilizar vendas**, desde que **haja pelo menos 1 lote válido**. | 🔴 Crítica | 8 | RF17 |
| | | **Critérios de Aceitação:**<br>- Validação de pré-condições (lote + categoria)<br>- Invalidação de cache<br>- Notificação aos produtores<br>- Registro de auditoria | | | |
| **E4-F4** | **Página Pública do Evento** | **US-015:** Como **usuário**, eu quero **visualizar detalhes completos do evento** para **decidir sobre compra**. | 🟠 Alta | 5 | RF18 |
| **E4-F5** | **Vinculação Produtor-Evento** | **US-016:** Como **administrador**, eu quero **vincular produtores a eventos** para **permitir acesso ao painel**. | 🟠 Alta | 5 | RF19 |
| **E4-F6** | **Gestão de Categorias** | **US-017:** Como **administrador**, eu quero **gerenciar categorias** para **organizar eventos**. | 🟡 Média | 5 | RF20 |

---

### Épico 5: Venda e Checkout

**Objetivo:** Permitir que clientes comprem ingressos com segurança e transparência.

| ID | Feature | User Story | Prioridade | Story Points | RF Relacionado |
|---|---|---|---|---|---|
| **E5-F1** | **Checkout** | **US-018:** Como **cliente**, eu quero **visualizar resumo completo do pedido** para **confirmar compra**. | 🔴 Crítica | 8 | RF26 |
| | | **Critérios de Aceitação:**<br>- Resumo de itens, taxas e total<br>- Aceite de termos e política de reembolso<br>- Limite por CPF (5 ingressos)<br>- Validações em tempo real | | | |
| **E5-F2** | **Pagamento PIX** | **US-019:** Como **cliente**, eu quero **pagar via PIX** para **comprar ingressos**. | 🔴 Crítica | 13 | RF27 |
| | | **Critérios de Aceitação:**<br>- QR Code dinâmico gerado<br>- Reserva de 10 minutos<br>- Confirmação via webhook<br>- Liberação de estoque ao expirar | | | |
| **E5-F3** | **Pagamento Cartão** | **US-020:** Como **cliente**, eu quero **pagar via cartão de crédito** para **comprar ingressos**. | 🔴 Crítica | 13 | RF28 |
| | | **Critérios de Aceitação:**<br>- Integração com gateway (Pagar.me)<br>- 3DS e antifraude<br>- Callbacks assíncronos<br>- Tratamento de recusas | | | |
| **E5-F4** | **Cupom de Influenciador** | **US-021:** Como **cliente**, eu quero **aplicar cupom de desconto** para **obter desconto na compra**. | 🟠 Alta | 8 | RF31 |
| | | **Critérios de Aceitação:**<br>- Campo para inserir código<br>- Validação de vigência e limites<br>- Desconto percentual ou fixo<br>- Registro de atribuição ao influenciador | | | |
| **E5-F5** | **Confirmação e Cancelamento** | **US-022:** Como **sistema**, eu quero **processar confirmação de pagamento** para **emitir ingressos**. | 🔴 Crítica | 8 | RF29, RF30 |

---

### Épico 6: Ingressos e QR Code

**Objetivo:** Emitir ingressos digitais seguros com QR Code antifraude.

| ID | Feature | User Story | Prioridade | Story Points | RF Relacionado |
|---|---|---|---|---|---|
| **E6-F1** | **Emissão de Ingressos** | **US-023:** Como **sistema**, eu quero **emitir ingressos digitais após pagamento confirmado** para **entregar acesso ao evento**. | 🔴 Crítica | 13 | RF32 |
| | | **Critérios de Aceitação:**<br>- ID único por ingresso<br>- QR Code assinado digitalmente<br>- Atribuição à carteira do cliente<br>- Processamento assíncrono via mensageria | | | |
| **E6-F2** | **Validade e Reenvio** | **US-024:** Como **cliente**, eu quero **reenviar ingresso por e-mail** para **acessar quando necessário**. | 🟡 Média | 5 | RF33, RF34 |
| **E6-F3** | **Notificações de Ingresso** | **US-025:** Como **cliente**, eu quero **receber ingresso por e-mail/WhatsApp** para **ter acesso facilitado**. | 🟠 Alta | 8 | RF35 |

---

### Épico 7: Check-in e Validação

**Objetivo:** Validar ingressos no evento com segurança e eficiência.

| ID | Feature | User Story | Prioridade | Story Points | RF Relacionado |
|---|---|---|---|---|---|
| **E7-F1** | **Validação de Ingressos** | **US-026:** Como **operador de check-in**, eu quero **validar ingressos via QR Code** para **controlar acesso ao evento**. | 🔴 Crítica | 13 | RF36, RF37 |
| | | **Critérios de Aceitação:**<br>- Leitura por câmera/leitor<br>- Validação de assinatura digital<br>- Status: válido/duplicado/expirado<br>- Registro completo (data, hora, operador, dispositivo) | | | |
| **E7-F2** | **Modo Offline** | **US-027:** Como **operador de check-in**, eu quero **validar ingressos offline** para **funcionar sem internet**. | 🟡 Média | 13 | RF38 |
| | | **Critérios de Aceitação:**<br>- PWA com sincronização prévia<br>- Base local para validação<br>- Sincronização posterior<br>- Reconciliação de conflitos | | | |
| **E7-F3** | **Relatórios de Check-in** | **US-028:** Como **produtor/admin**, eu quero **visualizar relatórios de check-in** para **acompanhar comparecimento**. | 🟡 Média | 5 | RF39 |

---

### Épico 8: Transferência de Ingressos

**Objetivo:** Permitir transferência segura de ingressos entre usuários.

| ID | Feature | User Story | Prioridade | Story Points | RF Relacionado |
|---|---|---|---|---|---|
| **E8-F1** | **Iniciar Transferência** | **US-029:** Como **cliente**, eu quero **transferir ingresso para outro usuário** para **ceder acesso quando necessário**. | 🟠 Alta | 13 | RF40, RF44 |
| | | **Critérios de Aceitação:**<br>- Seleção de ingresso não utilizado<br>- Informar e-mail/CPF do destinatário<br>- Validação de elegibilidade<br>- Criar solicitação pendente<br>- Enviar convite ao destinatário | | | |
| **E8-F2** | **Aceite e Conclusão** | **US-030:** Como **destinatário**, eu quero **aceitar transferência de ingresso** para **receber acesso ao evento**. | 🟠 Alta | 13 | RF41, RF42, RF45 |
| | | **Critérios de Aceitação:**<br>- Autenticação/criação de conta<br>- Aceite dentro da janela configurável<br>- Pagamento de taxa (10% padrão)<br>- Invalidação do QR original<br>- Emissão de novo QR assinado<br>- Transferência para carteira do destinatário | | | |
| **E8-F3** | **Recusa e Expiração** | **US-031:** Como **sistema**, eu quero **tratar recusa/expiração de transferência** para **retornar ingresso ao remetente**. | 🟡 Média | 5 | RF43 |
| **E8-F4** | **Notificações de Transferência** | **US-032:** Como **cliente**, eu quero **receber notificações sobre transferências** para **acompanhar status**. | 🟡 Média | 5 | RF47 |

---

### Épico 9: Administração e Auditoria

**Objetivo:** Permitir gestão completa e auditoria do sistema.

| ID | Feature | User Story | Prioridade | Story Points | RF Relacionado |
|---|---|---|---|---|---|
| **E9-F1** | **Painel Administrativo** | **US-033:** Como **administrador**, eu quero **visualizar visão geral do sistema** para **gerenciar a plataforma**. | 🟠 Alta | 13 | RF48 |
| | | **Critérios de Aceitação:**<br>- Dashboard com métricas principais<br>- Listagem de usuários, produtores, eventos<br>- Gestão de vendas, cupons, cashback<br>- Filtros e exportações | | | |
| **E9-F2** | **Auditoria** | **US-034:** Como **administrador**, eu quero **visualizar trilha de auditoria** para **rastrear ações críticas**. | 🟠 Alta | 8 | RF49 |
| | | **Critérios de Aceitação:**<br>- Logs de criar/editar/publicar/cancelar<br>- Logs de validação e transferência<br>- Usuário, timestamp, IP/dispositivo<br>- Consultas filtradas e exportáveis | | | |
| **E9-F3** | **Gestão de Fraudes** | **US-035:** Como **administrador**, eu quero **bloquear usuários/eventos suspeitos** para **prevenir fraudes**. | 🟠 Alta | 8 | RF50 |
| **E9-F4** | **Parâmetros Globais** | **US-036:** Como **administrador**, eu quero **configurar parâmetros globais** para **personalizar comportamento do sistema**. | 🟡 Média | 8 | RF51 |

---

### Épico 10: Infraestrutura e Não Funcionais

**Objetivo:** Garantir performance, segurança, acessibilidade e confiabilidade.

| ID | Feature | User Story | Prioridade | Story Points | RNF Relacionado |
|---|---|---|---|---|---|
| **E10-F1** | **Performance e Escalabilidade** | **US-037:** Como **sistema**, eu quero **garantir P90 ≤ 2s** para **oferecer experiência rápida**. | 🟠 Alta | 13 | RNF01, RNF07 |
| **E10-F2** | **Disponibilidade** | **US-038:** Como **sistema**, eu quero **manter disponibilidade ≥ 99,5%** para **garantir operação contínua**. | 🟠 Alta | 13 | RNF02 |
| **E10-F3** | **Segurança** | **US-039:** Como **sistema**, eu quero **garantir segurança de dados** para **proteger informações sensíveis**. | 🔴 Crítica | 13 | RNF03, RNF04, RNF05, RNF06, RNF17 |
| **E10-F4** | **Acessibilidade WCAG 2.1 AA** | **US-040:** Como **usuário com deficiência**, eu quero **acessar a plataforma** para **usar todos os recursos**. | 🟠 Alta | 21 | RNF09-RNF28 |
| **E10-F5** | **Mensageria e Cache** | **US-041:** Como **sistema**, eu quero **processar tarefas assíncronas** para **garantir performance**. | 🟠 Alta | 13 | RNF14, RNF15 |
| **E10-F6** | **Observabilidade** | **US-042:** Como **equipe técnica**, eu quero **monitorar o sistema** para **garantir operação saudável**. | 🟠 Alta | 8 | RNF11 |
| **E10-F7** | **LGPD** | **US-043:** Como **sistema**, eu quero **conformidade com LGPD** para **proteger dados pessoais**. | 🟠 Alta | 8 | RNF13 |

---

## Roadmap MVP

### Sprint 1-2: Fundação (Sprint 0)
- E1-F1, E1-F2: Autenticação básica
- E10-F3: Segurança básica
- E10-F5: Mensageria e Cache (infraestrutura)

### Sprint 3-4: Gestão de Eventos
- E3-F1: Onboarding de Produtores
- E4-F1, E4-F2: Criação de Eventos e Lotes
- E4-F3: Publicação

### Sprint 5-6: Catálogo e Busca
- E2-F1, E2-F2, E2-F3, E2-F4: Busca e Filtros
- E4-F4: Página Pública do Evento

### Sprint 7-8: Checkout e Pagamentos
- E5-F1: Checkout
- E5-F2, E5-F3: Pagamentos PIX e Cartão
- E5-F4: Cupons

### Sprint 9-10: Ingressos e Check-in
- E6-F1: Emissão de Ingressos
- E7-F1: Validação de Check-in
- E6-F3: Notificações

### Sprint 11-12: Transferências e Painéis
- E8-F1, E8-F2: Transferência de Ingressos
- E3-F2: Painel do Produtor
- E9-F1: Painel Admin

### Sprint 13-14: Acessibilidade e Finalização
- E10-F4: Acessibilidade WCAG 2.1 AA
- E9-F2: Auditoria
- E10-F6: Observabilidade

---

## Tabela Consolidada do Backlog

| ID | Épico | Feature | Prioridade | Story Points | Status |
|---|---|---|---|---|---|
| E1-F1 | Autenticação | Cadastro de Usuário | 🔴 Crítica | 8 | Backlog |
| E1-F2 | Autenticação | Login e Sessão | 🔴 Crítica | 5 | Backlog |
| E1-F3 | Autenticação | Recuperação de Senha | 🟡 Média | 5 | Backlog |
| E1-F4 | Autenticação | Gestão de Perfil | 🟡 Média | 5 | Backlog |
| E2-F1 | Descoberta | Busca Global | 🟠 Alta | 8 | Backlog |
| E2-F2 | Descoberta | Filtros por Localização | 🟠 Alta | 8 | Backlog |
| E2-F3 | Descoberta | Filtros por Categoria | 🟠 Alta | 5 | Backlog |
| E2-F4 | Descoberta | Filtros por Data | 🟠 Alta | 5 | Backlog |
| E2-F5 | Descoberta | Ordenação e URLs | 🟡 Média | 5 | Backlog |
| E3-F1 | Produtores | Onboarding | 🔴 Crítica | 13 | Backlog |
| E3-F2 | Produtores | Painel do Produtor | 🟠 Alta | 8 | Backlog |
| E4-F1 | Eventos | Criação de Evento | 🔴 Crítica | 13 | Backlog |
| E4-F2 | Eventos | Criação de Lotes | 🔴 Crítica | 13 | Backlog |
| E4-F3 | Eventos | Publicação | 🔴 Crítica | 8 | Backlog |
| E4-F4 | Eventos | Página Pública | 🟠 Alta | 5 | Backlog |
| E4-F5 | Eventos | Vinculação Produtor | 🟠 Alta | 5 | Backlog |
| E4-F6 | Eventos | Gestão de Categorias | 🟡 Média | 5 | Backlog |
| E5-F1 | Venda | Checkout | 🔴 Crítica | 8 | Backlog |
| E5-F2 | Venda | Pagamento PIX | 🔴 Crítica | 13 | Backlog |
| E5-F3 | Venda | Pagamento Cartão | 🔴 Crítica | 13 | Backlog |
| E5-F4 | Venda | Cupom de Influenciador | 🟠 Alta | 8 | Backlog |
| E5-F5 | Venda | Confirmação/Cancelamento | 🔴 Crítica | 8 | Backlog |
| E6-F1 | Ingressos | Emissão | 🔴 Crítica | 13 | Backlog |
| E6-F2 | Ingressos | Validade e Reenvio | 🟡 Média | 5 | Backlog |
| E6-F3 | Ingressos | Notificações | 🟠 Alta | 8 | Backlog |
| E7-F1 | Check-in | Validação | 🔴 Crítica | 13 | Backlog |
| E7-F2 | Check-in | Modo Offline | 🟡 Média | 13 | Backlog |
| E7-F3 | Check-in | Relatórios | 🟡 Média | 5 | Backlog |
| E8-F1 | Transferência | Iniciar Transferência | 🟠 Alta | 13 | Backlog |
| E8-F2 | Transferência | Aceite e Conclusão | 🟠 Alta | 13 | Backlog |
| E8-F3 | Transferência | Recusa/Expiração | 🟡 Média | 5 | Backlog |
| E8-F4 | Transferência | Notificações | 🟡 Média | 5 | Backlog |
| E9-F1 | Administração | Painel Admin | 🟠 Alta | 13 | Backlog |
| E9-F2 | Administração | Auditoria | 🟠 Alta | 8 | Backlog |
| E9-F3 | Administração | Gestão de Fraudes | 🟠 Alta | 8 | Backlog |
| E9-F4 | Administração | Parâmetros Globais | 🟡 Média | 8 | Backlog |
| E10-F1 | Infraestrutura | Performance | 🟠 Alta | 13 | Backlog |
| E10-F2 | Infraestrutura | Disponibilidade | 🟠 Alta | 13 | Backlog |
| E10-F3 | Infraestrutura | Segurança | 🔴 Crítica | 13 | Backlog |
| E10-F4 | Infraestrutura | Acessibilidade | 🟠 Alta | 21 | Backlog |
| E10-F5 | Infraestrutura | Mensageria/Cache | 🟠 Alta | 13 | Backlog |
| E10-F6 | Infraestrutura | Observabilidade | 🟠 Alta | 8 | Backlog |
| E10-F7 | Infraestrutura | LGPD | 🟠 Alta | 8 | Backlog |

**Total de Story Points:** ~420 pontos  
**Total de Features:** 43 features

---

## Métricas de Sucesso

### Métricas de Negócio
- **Taxa de conversão:** % de visitantes que completam compra
- **Taxa de abandono no checkout:** % de pedidos abandonados
- **Tempo médio de confirmação de pagamento:** P95 < 2 minutos
- **Taxa de sucesso de check-in:** > 99% (online), > 95% (offline)

### Métricas Técnicas
- **Disponibilidade:** ≥ 99,5% mensal
- **Latência P90:** ≤ 2s nas páginas principais
- **Latência de check-in:** P95 < 150ms (online)
- **Taxa de erro:** < 0,1% em endpoints críticos

### Métricas de Experiência
- **Tempo de carregamento:** < 3s na primeira carga
- **Taxa de uso de cupons:** % de pedidos com cupom aplicado
- **Taxa de transferência:** % de ingressos transferidos
- **Satisfação de acessibilidade:** Conformidade WCAG 2.1 AA

---

## Histórico de Versão

| Versão | Alteração | Responsável | Data |
|---|---|---|---|
| 1.0 | Criação inicial do backlog de produto organizado em 10 épicos e 43 features, com priorização baseada nos requisitos funcionais e não funcionais do projeto Ingressou | Gabriel Lima | 30/10/2025 |

