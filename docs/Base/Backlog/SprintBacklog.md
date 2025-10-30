# Sprint Backlog — Ingressou

> **Versão:** 2.0  
> **Data:** Outubro de 2025  
> **Autor:** Gabriel Lima  
> **Projeto:** Ingressou — Plataforma Web de Venda e Gestão de Ingressos  

---

## Sumário

- [Introdução](#introdução)
- [Metodologia Scrum](#metodologia-scrum)
- [Definição de Pronto (DoD)](#definição-de-pronto-dod)
- [Sprints do MVP](#sprints-do-mvp)
  - [Sprint 1: Fundação e Infraestrutura Base](#sprint-1-fundação-e-infraestrutura-base)
  - [Sprint 2: Mensageria, Cache e Frontend Base](#sprint-2-mensageria-cache-e-frontend-base)
  - [Sprint 3: Gestão de Produtores e Eventos](#sprint-3-gestão-de-produtores-e-eventos)
  - [Sprint 4: Busca e Catálogo de Eventos](#sprint-4-busca-e-catálogo-de-eventos)
  - [Sprint 5: Checkout e Pagamentos](#sprint-5-checkout-e-pagamentos)
  - [Sprint 6: Ingressos e Check-in](#sprint-6-ingressos-e-check-in)
  - [Sprint 7: Transferências e Painéis](#sprint-7-transferências-e-painéis)
  - [Sprint 8: Acessibilidade e Finalização](#sprint-8-acessibilidade-e-finalização)
- [Tabela Consolidada de Sprints](#tabela-consolidada-de-sprints)
- [Dependências entre Sprints](#dependências-entre-sprints)
- [Histórico de Versão](#histórico-de-versão)

---

## Introdução

Este documento apresenta o **Sprint Backlog** do projeto **Ingressou**, detalhando as tarefas técnicas específicas de cada sprint para implementação do MVP. O backlog foi derivado do [Backlog de Produto](/Base/Backlog/BacklogProduto.md), organizando as features em **8 sprints de 2 semanas cada = 16 semanas (4 meses)**.

Cada sprint contém:
- **Objetivo da Sprint**
- **Features do Product Backlog** relacionadas
- **Tarefas técnicas** detalhadas com estimativas
- **Critérios de aceitação** por tarefa
- **Definição de pronto** para a sprint

---

## Metodologia Scrum

**Duração das Sprints:** 2 semanas (10 dias úteis)  
**Cerimônias:**
- **Sprint Planning:** Início da sprint (2h)
- **Daily Scrum:** Diariamente (15min)
- **Sprint Review:** Final da sprint (1h)
- **Sprint Retrospective:** Final da sprint (1h)

**Estimativa:** Story Points (Fibonacci: 1, 2, 3, 5, 8, 13, 21)  
**Velocidade Esperada:** 30-40 story points por sprint (equipe de 4-5 desenvolvedores)

---

## Definição de Pronto (DoD)

Para uma tarefa ser considerada **"Pronta"**, deve atender:

- [ ] Código desenvolvido e revisado (code review aprovado)
- [ ] Testes unitários escritos e passando (cobertura ≥ 70%)
- [ ] Testes de integração passando
- [ ] Documentação atualizada (se aplicável)
- [ ] Deploy em ambiente de homologação
- [ ] Validação de QA (se aplicável)
- [ ] Sem bugs críticos conhecidos
- [ ] Critérios de aceitação atendidos

---

## Sprints do MVP

**Total de Sprints:** 8 sprints de 2 semanas cada = **16 semanas (4 meses)**

### Sprint 1: Fundação e Infraestrutura Base

**Objetivo:** Estabelecer infraestrutura técnica base, autenticação e segurança fundamental.

**Duração:** 2 semanas (10 dias úteis)  
**Story Points:** ~38 pontos

#### Features do Product Backlog
- E1-F1: Cadastro de Usuário (8 pts)
- E1-F2: Login e Sessão (5 pts)
- E10-F3: Segurança (13 pts)

#### Tarefas Técnicas

| ID | Tarefa | Tipo | Story Points | Prioridade | Dependências |
|---|---|---|---|---|---|
| **S1-T1** | **Setup do Projeto** | Infraestrutura | 5 | 🔴 Crítica | - |
| | - Configurar repositório Git e estrutura de pastas<br>- Setup Docker Compose (PostgreSQL, Redis, RabbitMQ)<br>- Configurar CI/CD básico (GitHub Actions)<br>- Definir padrões de código (ESLint, Prettier) | | | |
| **S1-T2** | **Modelagem do Banco de Dados** | Backend | 8 | 🔴 Crítica | S1-T1 |
| | - Criar schema de banco (PostgreSQL)<br>- Tabelas: Usuario, Cliente, Produtor, Administrador<br>- Migrations com Flyway<br>- Índices básicos<br>- Seed de dados iniciais (roles, categorias) | | | |
| **S1-T3** | **API Gateway e Autenticação JWT** | Backend | 8 | 🔴 Crítica | S1-T2 |
| | - Implementar Gateway Service (Nginx/Express)<br>- Middleware de autenticação JWT<br>- Refresh token (7d) com rotação<br>- Rate limiting básico<br>- Revogação de tokens | | | |
| **S1-T4** | **Cadastro e Login de Usuário** | Backend | 8 | 🔴 Crítica | S1-T3 |
| | - Endpoint POST /auth/register (e-mail/senha)<br>- Endpoint POST /auth/login<br>- Hash de senha (bcrypt)<br>- Validação de e-mail único<br>- Verificação por OTP/e-mail | | | |
| **S1-T5** | **Login Social (Google/Apple)** | Backend | 5 | 🔴 Crítica | S1-T4 |
| | - Integração OAuth2 com Google<br>- Integração OAuth2 com Apple<br>- Callback handlers<br>- Vinculação de contas sociais | | | |
| **S1-T6** | **Configuração de Segurança** | Infraestrutura | 5 | 🔴 Crítica | S1-T3 |
| | - HTTPS/TLS 1.2+<br>- HSTS e CSP headers<br>- Cookies HttpOnly/Secure/SameSite<br>- CORS configurado<br>- Secrets em cofre (Vault/Secrets Manager) | | | |
| **S1-T7** | **Frontend Base (SPA)** | Frontend | 8 | 🔴 Crítica | S1-T4 |
| | - Setup React/Next.js<br>- Estrutura de rotas<br>- Componentes de autenticação (Login/Cadastro)<br>- Integração com API Gateway<br>- Gerenciamento de estado (Redux/Zustand) | | | |

**Definição de Pronto Sprint 1:**
- [ ] Usuários podem se cadastrar e fazer login
- [ ] JWT e refresh token funcionando
- [ ] Segurança básica implementada
- [ ] Frontend base operacional

---

### Sprint 2: Mensageria, Cache e Frontend Base

**Objetivo:** Completar infraestrutura com mensageria e cache, e avançar no frontend.

**Duração:** 2 semanas (10 dias úteis)  
**Story Points:** ~35 pontos

#### Features do Product Backlog
- E10-F5: Mensageria e Cache (13 pts)

#### Tarefas Técnicas

| ID | Tarefa | Tipo | Story Points | Prioridade | Dependências |
|---|---|---|---|---|---|
| **S2-T1** | **Setup de Mensageria (RabbitMQ)** | Infraestrutura | 8 | 🟠 Alta | S1-T1 |
| | - Configurar RabbitMQ com exchanges topic<br>- Filas: emails, whatsapp, qr-generation, exports<br>- DLQ configurada<br>- Workers básicos (consumers)<br>- Retry com backoff exponencial | | | |
| **S2-T2** | **Setup de Cache (Redis)** | Infraestrutura | 5 | 🟠 Alta | S1-T1 |
| | - Configurar Redis<br>- Service de cache com TTL<br>- Estratégias de invalidação<br>- Cache para sessões de usuário | | | |
| **S2-T3** | **Painel Administrativo (Frontend)** | Frontend | 8 | 🔴 Crítica | S1-T7 |
| | - Layout base do painel admin<br>- Menu de navegação<br>- Dashboard com métricas básicas<br>- Componentes reutilizáveis | | | |
| **S2-T4** | **Testes de Infraestrutura** | QA | 5 | 🟠 Alta | S2-T1, S2-T2 |
| | - Testes de integração RabbitMQ<br>- Testes de cache Redis<br>- Testes de carga básicos<br>- Validação de segurança (OWASP Top 10) | | | |
| **S2-T5** | **Gestão de Categorias** | Backend | 5 | 🟡 Média | S1-T2 |
| | - CRUD de categorias<br>- Validação de exclusão (eventos vinculados)<br>- Slug automático<br>- Endpoint GET /categorias (público) | | | |
| **S2-T6** | **Observabilidade Básica** | Infraestrutura | 5 | 🟠 Alta | S1-T1 |
| | - Logs estruturados (JSON)<br>- Correlação (traceId/spanId)<br>- Integração Sentry<br>- Níveis de log apropriados | | | |

**Definição de Pronto Sprint 2:**
- [ ] Mensageria e cache operacionais
- [ ] Painel admin base funcional
- [ ] Testes de infraestrutura passando
- [ ] Observabilidade básica configurada

---

### Sprint 3: Gestão de Produtores e Eventos

**Objetivo:** Permitir cadastro de produtores e criação/públicação de eventos e lotes.

**Duração:** 2 semanas (10 dias úteis)  
**Story Points:** ~42 pontos

#### Features do Product Backlog
- E3-F1: Onboarding de Produtor (13 pts)
- E4-F1: Criação de Evento (13 pts)
- E4-F2: Criação de Lotes (13 pts)
- E4-F3: Publicação de Evento (8 pts)

#### Tarefas Técnicas

| ID | Tarefa | Tipo | Story Points | Prioridade | Dependências |
|---|---|---|---|---|---|
| **S3-T1** | **Cadastro de Produtor (Admin)** | Backend | 8 | 🔴 Crítica | S1-T2 |
| | - Endpoint POST /admin/produtores<br>- Validação de CNPJ/CPF (API Receita Federal)<br>- Validação de chave PIX<br>- KYC básico<br>- Envio de credenciais por e-mail | | | |
| **S3-T2** | **Formulário de Cadastro de Produtor** | Frontend | 5 | 🔴 Crítica | S2-T3, S3-T1 |
| | - Formulário completo com validação<br>- Máscaras de CPF/CNPJ<br>- Validação em tempo real<br>- Upload de documentos (opcional)<br>- Feedback de sucesso/erro | | | |
| **S3-T3** | **Criação de Eventos (Admin)** | Backend | 8 | 🔴 Crítica | S1-T2 |
| | - Endpoint POST /admin/eventos<br>- Validação de dados obrigatórios<br>- Upload de banner (S3)<br>- Criação de localização<br>- Status inicial: RASCUNHO | | | |
| **S3-T4** | **Formulário de Criação de Evento** | Frontend | 8 | 🔴 Crítica | S2-T3, S3-T3 |
| | - Formulário multi-step<br>- Upload de imagem<br>- Seleção de categoria<br>- Validação de datas<br>- Preview de evento | | | |
| **S3-T5** | **Criação de Lotes** | Backend | 8 | 🔴 Crítica | S3-T3 |
| | - Endpoint POST /admin/eventos/:id/lotes<br>- Validação de janela de venda<br>- Encerramento automático por tempo/quantidade<br>- Tipos de ingresso (inteira, meia, VIP, cortesia) | | | |
| **S3-T6** | **Interface de Gestão de Lotes** | Frontend | 5 | 🔴 Crítica | S3-T5 |
| | - CRUD de lotes<br>- Validação de conflitos de datas<br>- Visualização de disponibilidade<br>- Encerramento manual (opcional) | | | |
| **S3-T7** | **Publicação de Eventos** | Backend | 5 | 🔴 Crítica | S3-T5 |
| | - Validação de pré-condições (≥1 lote válido + categoria)<br>- Endpoint POST /admin/eventos/:id/publicar<br>- Invalidação de cache<br>- Notificação aos produtores<br>- Registro de auditoria | | | |
| **S3-T8** | **Vinculação Produtor-Evento** | Backend | 3 | 🟠 Alta | S3-T1 |
| | - Endpoint POST /admin/eventos/:id/produtores<br>- Validação de produtor existente<br>- Notificação ao produtor<br>- Atualização de permissões | | | |

**Definição de Pronto Sprint 3:**
- [ ] Admin pode cadastrar produtores com validação KYC
- [ ] Admin pode criar eventos e lotes
- [ ] Eventos podem ser publicados (com validações)
- [ ] Produtores podem ser vinculados a eventos
- [ ] Cache invalidado após publicação

---

### Sprint 4: Busca e Catálogo de Eventos

**Objetivo:** Implementar busca e filtros para descoberta de eventos.

**Duração:** 2 semanas (10 dias úteis)  
**Story Points:** ~34 pontos

#### Features do Product Backlog
- E2-F1: Busca Global (8 pts)
- E2-F2: Filtros por Localização (8 pts)
- E2-F3: Filtros por Categoria (5 pts)
- E2-F4: Filtros por Data (5 pts)
- E4-F4: Página Pública do Evento (5 pts)
- E2-F5: Ordenação e URLs (5 pts)

#### Tarefas Técnicas

| ID | Tarefa | Tipo | Story Points | Prioridade | Dependências |
|---|---|---|---|---|---|
| **S4-T1** | **Backend de Busca Global** | Backend | 8 | 🟠 Alta | S3-T7 |
| | - Endpoint GET /eventos/busca?q={termo}<br>- Busca full-text em nome, local, artista, descrição<br>- Índices otimizados no PostgreSQL<br>- Paginação de resultados<br>- Cache de consultas frequentes | | | |
| **S4-T2** | **Backend de Filtros** | Backend | 8 | 🟠 Alta | S3-T7 |
| | - Endpoint GET /eventos com query params<br>- Filtros: cidade, UF, categoria, data<br>- Índices por cidade, UF, data, categoria<br>- Combinação de filtros<br>- URLs parametrizadas e compartilháveis | | | |
| **S4-T3** | **Interface de Busca e Filtros** | Frontend | 8 | 🟠 Alta | S4-T1, S4-T2 |
| | - Campo de busca com autocompletar<br>- Filtros por localização, categoria e data<br>- Persistência de filtros na URL<br>- Botão "limpar filtros"<br>- Debounce para otimização | | | |
| **S4-T4** | **Página de Listagem de Eventos** | Frontend | 5 | 🟠 Alta | S4-T2 |
| | - Grid/Lista de eventos<br>- Cards com informações principais<br>- Paginação<br>- Ordenação (data, popularidade, preço)<br>- Loading states e skeleton screens | | | |
| **S4-T5** | **Página Pública do Evento** | Frontend | 5 | 🟠 Alta | S3-T7 |
| | - Endpoint GET /eventos/:slug<br>- Exibição completa de dados<br>- Lista de lotes disponíveis<br>- Botão "Comprar Ingressos"<br>- Compartilhamento social | | | |
| **S4-T6** | **Otimização de Cache** | Backend | 5 | 🟠 Alta | S4-T2 |
| | - Cache de listagens por chave semântica<br>- TTL de 60-300s<br>- Invalidação por evento/lote<br>- Warm-up de cache para consultas frequentes | | | |

**Definição de Pronto Sprint 4:**
- [ ] Usuários podem buscar eventos por termo
- [ ] Filtros por localização, categoria e data funcionando
- [ ] Página pública do evento acessível
- [ ] Cache otimizado para performance
- [ ] URLs amigáveis e compartilháveis

---

### Sprint 5: Checkout e Pagamentos

**Objetivo:** Implementar fluxo completo de checkout e integração com gateway de pagamento.

**Duração:** 2 semanas (10 dias úteis)  
**Story Points:** ~50 pontos

#### Features do Product Backlog
- E5-F1: Checkout (8 pts)
- E5-F2: Pagamento PIX (13 pts)
- E5-F3: Pagamento Cartão (13 pts)
- E5-F4: Cupom de Influenciador (8 pts)
- E5-F5: Confirmação/Cancelamento (8 pts)

#### Tarefas Técnicas

| ID | Tarefa | Tipo | Story Points | Prioridade | Dependências |
|---|---|---|---|---|---|
| **S5-T1** | **Modelagem de Pedidos e Pagamentos** | Backend | 8 | 🔴 Crítica | S4-T5 |
| | - Tabelas: Pedido, ItemPedido, Pagamento<br>- Estados: CRIADO, AGUARDANDO_PAGAMENTO, PAGO, CANCELADO, EXPIRADO<br>- Relacionamentos e constraints<br>- Reserva temporária de estoque | | | |
| **S5-T2** | **Backend de Checkout** | Backend | 8 | 🔴 Crítica | S5-T1 |
| | - Endpoint POST /checkout/criar<br>- Validação de disponibilidade<br>- Aplicação de cupom<br>- Cálculo de taxas (8% plataforma)<br>- Limite por CPF (5 ingressos)<br>- Criar pedido com status CRIADO | | | |
| **S5-T3** | **Sistema de Cupons** | Backend | 8 | 🟠 Alta | S5-T2 |
| | - Tabela Cupom<br>- Validação de vigência, limites, acúmulo<br>- Cálculo de desconto (percentual/fixo)<br>- Registro de atribuição ao influenciador<br>- Endpoint POST /cupons/validar | | | |
| **S5-T4** | **Interface de Checkout** | Frontend | 8 | 🔴 Crítica | S5-T2 |
| | - Resumo do pedido<br>- Seleção de quantidade<br>- Campo de cupom<br>- Cálculo de total em tempo real<br>- Aceite de termos LGPD<br>- Botão "Finalizar Compra" | | | |
| **S5-T5** | **Integração Gateway Pagar.me** | Backend | 13 | 🔴 Crítica | S5-T2 |
| | - Cliente SDK Pagar.me<br>- Configuração de credenciais (sandbox/prod)<br>- Endpoints de pagamento PIX e Cartão<br>- Webhooks configurados<br>- Idempotência de transações | | | |
| **S5-T6** | **Pagamento PIX** | Backend | 8 | 🔴 Crítica | S5-T5 |
| | - Geração de QR Code dinâmico<br>- Reserva de 10 minutos<br>- Webhook de confirmação<br>- Expiração automática<br>- Liberação de estoque ao expirar | | | |
| **S5-T7** | **Pagamento Cartão** | Backend | 8 | 🔴 Crítica | S5-T5 |
| | - Tokenização de cartão<br>- 3DS (3D Secure)<br>- Antifraude<br>- Autorização e confirmação<br>- Tratamento de recusas | | | |
| **S5-T8** | **Interface de Pagamento** | Frontend | 8 | 🔴 Crítica | S5-T6, S5-T7 |
| | - Seleção de método (PIX/Cartão)<br>- Exibição de QR Code PIX<br>- Formulário de cartão<br>- Validação de dados<br>- Loading states<br>- Redirecionamento após pagamento | | | |
| **S5-T9** | **Processamento de Webhooks** | Backend | 8 | 🔴 Crítica | S5-T5 |
| | - Worker para processar webhooks<br>- Validação de assinatura<br>- Idempotência por chave<br>- Atualização de status do pagamento<br>- Emissão de ingressos (próxima sprint) | | | |
| **S5-T10** | **Gestão de Estoque** | Backend | 5 | 🔴 Crítica | S5-T2 |
| | - Reserva temporária no checkout<br>- Liberação ao expirar/cancelar<br>- Bloqueio definitivo ao confirmar<br>- Validação de disponibilidade | | | |

**Definição de Pronto Sprint 5:**
- [ ] Clientes podem fazer checkout completo
- [ ] Pagamentos PIX e cartão funcionando
- [ ] Cupons de influenciador aplicáveis
- [ ] Webhooks processados corretamente
- [ ] Estoque gerenciado automaticamente

---

### Sprint 6: Ingressos e Check-in

**Objetivo:** Emitir ingressos digitais e implementar validação via QR Code.

**Duração:** 2 semanas (10 dias úteis)  
**Story Points:** ~45 pontos

#### Features do Product Backlog
- E6-F1: Emissão de Ingressos (13 pts)
- E6-F3: Notificações de Ingresso (8 pts)
- E7-F1: Validação de Ingressos (13 pts)
- E6-F2: Validade e Reenvio (5 pts)

#### Tarefas Técnicas

| ID | Tarefa | Tipo | Story Points | Prioridade | Dependências |
|---|---|---|---|---|---|
| **S6-T1** | **Modelagem de Ingressos e QR Codes** | Backend | 5 | 🔴 Crítica | S5-T9 |
| | - Tabelas: Ingresso, QrCode, Carteira, CheckinRegistro<br>- Relacionamentos<br>- Estados: EMITIDO, VALIDADO, CANCELADO<br>- Código único por ingresso | | | |
| **S6-T2** | **Serviço de Assinatura QR** | Backend | 8 | 🔴 Crítica | S6-T1 |
| | - Geração de QR Code assinado (JWT + nonce)<br>- Chave privada para assinatura<br>- Validação de assinatura<br>- Anti-replay (nonce único)<br>- Expiração após primeiro uso | | | |
| **S6-T3** | **Emissão de Ingressos** | Backend | 8 | 🔴 Crítica | S6-T2 |
| | - Worker para processar pagamentos confirmados<br>- Geração de ingressos por item do pedido<br>- Atribuição à carteira do cliente<br>- Processamento assíncrono via mensageria<br>- Endpoint GET /ingressos (carteira do usuário) | | | |
| **S6-T4** | **Carteira Digital** | Frontend | 5 | 🟠 Alta | S6-T3 |
| | - Página "Meus Ingressos"<br>- Listagem de ingressos por status<br>- Visualização de QR Code<br>- Filtros por evento<br>- Botão "Reenviar por E-mail" | | | |
| **S6-T5** | **Reenvio de Ingressos** | Backend | 3 | 🟡 Média | S6-T4 |
| | - Endpoint POST /ingressos/:id/reenviar<br>- Validação de propriedade<br>- Envio via mensageria<br>- Log de reenvio | | | |
| **S6-T6** | **Notificações de Ingresso** | Backend | 5 | 🟠 Alta | S6-T3 |
| | - Template de e-mail com QR Code<br>- Envio via WhatsApp (opcional)<br>- Worker assíncrono<br>- Retry em caso de falha | | | |
| **S6-T7** | **PWA de Check-in** | Frontend | 13 | 🔴 Crítica | S6-T2 |
| | - Setup PWA (service worker, manifest)<br>- Interface de leitura de QR Code<br>- Câmera do dispositivo<br>- Feedback visual/sonoro<br>- Modo offline básico (IndexedDB) | | | |
| **S6-T8** | **Backend de Validação** | Backend | 8 | 🔴 Crítica | S6-T7 |
| | - Endpoint POST /checkin/validar<br>- Validação de assinatura QR<br>- Verificação de status (válido/duplicado/expirado)<br>- Registro de check-in<br>- Latência P95 < 150ms | | | |
| **S6-T9** | **Sincronização Offline** | Backend | 3 | 🟡 Média | S6-T7 |
| | - Endpoint GET /checkin/sincronizar/:eventoId<br>- Lista compacta de ingressos válidos<br>- Sincronização posterior de registros<br>- Reconciliação básica de conflitos | | | |
| **S6-T10** | **Relatórios de Check-in** | Backend | 3 | 🟡 Média | S6-T8 |
| | - Endpoint GET /checkin/relatorio/:eventoId<br>- Agregações de validações<br>- Exportação CSV<br>- Filtros por período | | | |

**Definição de Pronto Sprint 6:**
- [ ] Ingressos emitidos após pagamento confirmado
- [ ] QR Codes assinados digitalmente
- [ ] PWA de check-in funcional (online)
- [ ] Validação com baixa latência
- [ ] Notificações enviadas por e-mail/WhatsApp

---

### Sprint 7: Transferências e Painéis

**Objetivo:** Implementar transferência de ingressos e painéis de visualização.

**Duração:** 2 semanas (10 dias úteis)  
**Story Points:** ~42 pontos

#### Features do Product Backlog
- E8-F1: Iniciar Transferência (13 pts)
- E8-F2: Aceite e Conclusão (13 pts)
- E8-F3: Recusa e Expiração (5 pts)
- E8-F4: Notificações de Transferência (5 pts)
- E3-F2: Painel do Produtor (8 pts)
- E9-F1: Painel Admin (13 pts)

#### Tarefas Técnicas

| ID | Tarefa | Tipo | Story Points | Prioridade | Dependências |
|---|---|---|---|---|---|
| **S7-T1** | **Modelagem de Transferências** | Backend | 5 | 🟠 Alta | S6-T3 |
| | - Tabela Transferencia<br>- Estados: CRIADA, AGUARDANDO_ACEITE, AGUARDANDO_PAGAMENTO_TAXA, CONCLUIDA, RECUSADA, EXPIRADA, CANCELADA<br>- Relacionamentos com Ingresso e Pagamento<br>- Política de transferência por evento | | | |
| **S7-T2** | **Iniciar Transferência** | Backend | 8 | 🟠 Alta | S7-T1 |
| | - Endpoint POST /ingressos/:id/transferir<br>- Validação de elegibilidade<br>- Criar solicitação pendente<br>- Invalidar QR original<br>- Enviar convite ao destinatário<br>- Link assinado com expiração | | | |
| **S7-T3** | **Interface de Transferência** | Frontend | 5 | 🟠 Alta | S7-T2 |
| | - Seleção de ingresso<br>- Campo de e-mail/CPF do destinatário<br>- Exibição de taxa (10%)<br>- Confirmação de transferência<br>- Feedback de sucesso | | | |
| **S7-T4** | **Aceite e Conclusão** | Backend | 13 | 🟠 Alta | S7-T2 |
| | - Endpoint POST /transferencias/:id/aceitar<br>- Validação de janela de tempo<br>- Autenticação/criação de conta do destinatário<br>- Cálculo e cobrança de taxa<br>- Pagamento da taxa (PIX/Cartão)<br>- Transferir ingresso para carteira do destinatário<br>- Invalidar QR original definitivamente<br>- Emitir novo QR assinado<br>- Registrar auditoria completa | | | |
| **S7-T5** | **Recusa e Expiração** | Backend | 3 | 🟡 Média | S7-T2 |
| | - Endpoint POST /transferencias/:id/recusar<br>- Job para expiração automática<br>- Retornar ingresso ao remetente<br>- Revalidar QR original<br>- Notificações | | | |
| **S7-T6** | **Notificações de Transferência** | Backend | 3 | 🟡 Média | S7-T2 |
| | - Templates de e-mail/WhatsApp<br>- Notificações: criada, aceita, concluída, cancelada<br>- Processamento assíncrono | | | |
| **S7-T7** | **Backend do Painel do Produtor** | Backend | 8 | 🟠 Alta | S6-T10 |
| | - Endpoint GET /produtor/dashboard<br>- Métricas: vendas, check-ins, repasses, cashback<br>- Filtros por evento e período<br>- Agregações otimizadas<br>- Cache de métricas | | | |
| **S7-T8** | **Interface do Painel do Produtor** | Frontend | 8 | 🟠 Alta | S7-T7 |
| | - Dashboard com gráficos<br>- Lista de eventos vinculados<br>- Métricas por evento<br>- Exportação CSV<br>- Visualização de cashback | | | |
| **S7-T9** | **Backend do Painel Admin** | Backend | 8 | 🟠 Alta | S5-T9 |
| | - Endpoint GET /admin/dashboard<br>- Visão geral: usuários, eventos, vendas<br>- Listagens filtradas e paginadas<br>- Gestão de cupons, cashback<br>- Exportações | | | |
| **S7-T10** | **Interface do Painel Admin** | Frontend | 8 | 🟠 Alta | S7-T9 |
| | - Dashboard principal<br>- Módulos: usuários, produtores, eventos, vendas<br>- Filtros e buscas<br>- Ações administrativas<br>- Exportações | | | |

**Definição de Pronto Sprint 7:**
- [ ] Transferência de ingressos funcionando end-to-end
- [ ] Taxa de transferência cobrada corretamente
- [ ] Painel do produtor com métricas
- [ ] Painel admin completo
- [ ] Notificações enviadas em todas as etapas

---

### Sprint 8: Acessibilidade e Finalização

**Objetivo:** Garantir acessibilidade WCAG 2.1 AA e finalizar funcionalidades restantes.

**Duração:** 2 semanas (10 dias úteis)  
**Story Points:** ~38 pontos

#### Features do Product Backlog
- E10-F4: Acessibilidade WCAG 2.1 AA (21 pts)
- E9-F2: Auditoria (8 pts)
- E10-F6: Observabilidade (8 pts)

#### Tarefas Técnicas

| ID | Tarefa | Tipo | Story Points | Prioridade | Dependências |
|---|---|---|---|---|---|
| **S8-T1** | **Acessibilidade - Estrutura Semântica** | Frontend | 5 | 🟠 Alta | S1-T7 |
| | - HTML5 semântico (header, nav, main, footer)<br>- Cabeçalhos hierárquicos (h1-h6)<br>- Landmarks ARIA<br>- Breadcrumbs<br>- Skip links | | | |
| **S8-T2** | **Acessibilidade - Formulários e Navegação** | Frontend | 8 | 🟠 Alta | S8-T1 |
| | - Labels associados a todos os campos<br>- Instruções claras<br>- Mensagens de erro específicas<br>- Tab order lógico<br>- Foco visível em todos os elementos<br>- Atalhos de teclado (Enter, Esc)<br>- Áreas de toque ≥ 44x44px | | | |
| **S8-T3** | **Acessibilidade - Leitores de Tela** | Frontend | 5 | 🟠 Alta | S8-T1 |
| | - ARIA labels descritivos<br>- aria-live regions para atualizações<br>- Roles semânticos<br>- Estados acessíveis (aria-expanded, aria-selected)<br>- Testes com NVDA/JAWS/VoiceOver | | | |
| **S8-T4** | **Acessibilidade - Contraste e Mobile** | Frontend | 5 | 🟠 Alta | S1-T7 |
| | - Contraste mínimo 4.5:1 (texto normal)<br>- Contraste mínimo 3:1 (texto grande)<br>- Modo de alto contraste<br>- Tema escuro/claro<br>- VoiceOver (iOS) e TalkBack (Android)<br>- Zoom até 200% funcional | | | |
| **S8-T5** | **Acessibilidade - Conteúdo Dinâmico** | Frontend | 3 | 🟠 Alta | S8-T2 |
| | - aria-live para atualizações Ajax<br>- Loading states acessíveis<br>- Mensagens de erro não intrusivas<br>- Tempo adequado para ler conteúdo temporário | | | |
| **S8-T6** | **Sistema de Auditoria** | Backend | 8 | 🟠 Alta | S7-T4 |
| | - Tabela Auditoria<br>- Registro de ações críticas<br>- Endpoint GET /admin/auditoria<br>- Filtros: usuário, ação, período<br>- Exportação de logs<br>- Retenção de dados | | | |
| **S8-T7** | **Interface de Auditoria** | Frontend | 5 | 🟠 Alta | S8-T6 |
| | - Visualização de trilha de auditoria<br>- Filtros e buscas<br>- Detalhes de cada ação<br>- Exportação<br>- Timeline de eventos | | | |
| **S8-T8** | **Observabilidade Completa** | Infraestrutura | 8 | 🟠 Alta | S2-T6 |
| | - Prometheus/Grafana configurado<br>- Métricas de negócio (conversão, pagamentos)<br>- Métricas técnicas (latência, erros)<br>- Dashboards customizados<br>- Alertas configurados<br>- OpenTelemetry para tracing distribuído | | | |
| **S8-T9** | **Testes de Acessibilidade** | QA | 5 | 🟠 Alta | S8-T4 |
| | - Testes automatizados (axe-core, Pa11y)<br>- Testes manuais com leitores de tela<br>- Validação WCAG 2.1 AA<br>- Relatório de conformidade | | | |
| **S8-T10** | **Documentação Final** | Documentação | 3 | 🟡 Média | - |
| | - README atualizado<br>- Guia de deploy<br>- Documentação de APIs<br>- Runbook de operações<br>- Guia de acessibilidade | | | |

**Definição de Pronto Sprint 8:**
- [ ] Plataforma em conformidade WCAG 2.1 AA
- [ ] Sistema de auditoria completo
- [ ] Observabilidade implementada
- [ ] Testes de acessibilidade passando
- [ ] Documentação completa

---

## Tabela Consolidada de Sprints

| Sprint | Objetivo | Story Points | Features | Status |
|---|---|---|---|---|
| **Sprint 1** | Fundação e Infraestrutura Base | 38 | E1-F1, E1-F2, E10-F3 | Backlog |
| **Sprint 2** | Mensageria, Cache e Frontend Base | 35 | E10-F5 | Backlog |
| **Sprint 3** | Gestão de Produtores e Eventos | 42 | E3-F1, E4-F1, E4-F2, E4-F3 | Backlog |
| **Sprint 4** | Busca e Catálogo de Eventos | 34 | E2-F1, E2-F2, E2-F3, E2-F4, E4-F4, E2-F5 | Backlog |
| **Sprint 5** | Checkout e Pagamentos | 50 | E5-F1, E5-F2, E5-F3, E5-F4, E5-F5 | Backlog |
| **Sprint 6** | Ingressos e Check-in | 45 | E6-F1, E6-F3, E7-F1, E6-F2 | Backlog |
| **Sprint 7** | Transferências e Painéis | 42 | E8-F1, E8-F2, E8-F3, E8-F4, E3-F2, E9-F1 | Backlog |
| **Sprint 8** | Acessibilidade e Finalização | 38 | E10-F4, E9-F2, E10-F6 | Backlog |

**Total:** 324 Story Points | **Duração:** 16 semanas (4 meses) | **Features:** 27 features do MVP

---

## Dependências entre Sprints

### Dependências Críticas

1. **Sprint 1** → **Sprint 2**: Infraestrutura e autenticação necessárias para mensageria e frontend
2. **Sprint 2** → **Sprint 3**: Frontend base e painel admin necessários para gestão de eventos
3. **Sprint 3** → **Sprint 4**: Eventos precisam estar criados/publicados para busca
4. **Sprint 4** → **Sprint 5**: Página pública do evento necessária para checkout
5. **Sprint 5** → **Sprint 6**: Pagamentos confirmados necessários para emissão de ingressos
6. **Sprint 6** → **Sprint 7**: Ingressos emitidos necessários para transferência
7. **Sprint 5** → **Sprint 7**: Métricas de vendas necessárias para painéis

### Dependências Paralelas (Podem ser desenvolvidas em paralelo)

- Sprint 6 e Sprint 7 podem ter sobreposição (check-in vs transferências - backend separado)
- Sprint 8 pode começar parcialmente durante Sprint 7 (acessibilidade frontend)

---

## Histórico de Versão

| Versão | Alteração | Responsável | Data |
|---|---|---|---|
| 1.0 | Criação inicial do sprint backlog com 7 sprints (14 semanas), detalhando tarefas técnicas, estimativas e dependências baseadas no backlog de produto | Gabriel Lima | 30/10/2025 |
| 2.0 | Reorganização para 8 sprints (16 semanas = 4 meses), otimizando distribuição de tarefas e priorizando MVP crítico | Gabriel Lima | 30/10/2025 |
