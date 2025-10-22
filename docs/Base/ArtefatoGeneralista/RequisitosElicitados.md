# Requisitos Elicitados — Ingressou


## Sumário

1.  [Introdução](#introdução)
2.  [Visão Geral](#visão-geral)
3.  [Objetivos do Projeto](#objetivos-do-projeto)
4.  [Personas](#personas)
5.  [Escopo do Sistema](#escopo-do-sistema)
6.  [Requisitos Funcionais](#requisitos-funcionais)
7.  [Requisitos Não Funcionais](#requisitos-não-funcionais)
8.  [Regras de Negócio](#regras-de-negócio)
9.  [Critérios de Aceitação](#critérios-de-aceitação)
10. [Requisitos Futuros e Extensões](#requisitos-futuros-e-extensões)
11. [Considerações Finais](#considerações-finais)
12. [Histórico de Versão](#histórico-de-versão)

## Introdução

Este documento consolida os requisitos funcionais e não funcionais do **Ingressou**.

A versão **1.4** incorpora três alterações centrais:
* **Cobertura nacional** com ênfase em **busca, filtros por localização (cidade/UF) e categorização** de eventos;
* **Transferência de ingressos entre usuários** (carteira → transferência com aceite do destinatário e reemissão do QR);
* Manutenção das decisões anteriores: **evento criado exclusivamente pelo Administrador**, **lote encerra por tempo** ou **quantidade (o que vier primeiro)**, **cupom de influenciador**, **mensageria + cache**, **cashback destinado ao produtor** e **vinculação Produtor↔Evento** para acesso de leitura.

## Visão Geral

Plataforma nacional para **venda e validação de ingressos** com pagamentos via **PIX e cartão**, **QR Code antifraude**, **cupons de influenciadores**, **cashback ao produtor**, **busca e filtros nacionais (cidade/UF/categorias/data)** e **transferência de ingressos** controlada e auditável.

## Objetivos do Projeto

* Emitir, vender, **filtrar e descobrir** eventos no Brasil com **experiência de busca eficiente**.
* Garantir segurança: antifraude (QR assinado), check-in confiável (online/offline) e LGPD.
* Escalar via **mensageria** e **cache** para baixa latência em catálogos e relatórios.
* Potencializar aquisição (cupons) e retenção (boa UX e clareza).
* Isolar administração: Admin cria/edita/publica eventos e lotes; Produtor tem **somente leitura** dos eventos vinculados.
* Permitir **transferência de ingressos** com aceite do destinatário e reemissão de QR, preservando trilha de auditoria.

## Personas

* **Usuário Comprador** — busca por cidade/UF/categoria, filtra por data, compra via PIX/cartão, aplica cupom, transfere ingresso quando permitido.
* **Produtor** — não cria eventos; acompanha vendas, check-ins, repasses e cashback *apenas* dos eventos vinculados.
* **Staff (Check-in)** — valida ingressos com baixa latência, inclusive offline.
* **Administrador** — cadastra produtores, cria/publica eventos, define lotes, categorias, políticas, cupons e **vincula produtores a eventos**.

## Escopo do Sistema

### Incluído (MVP)

* Autenticação e perfis (usuário, produtor, admin).
* **Onboarding de Produtores pelo Admin** (KYC básico, chave PIX/split).
* Criação/publicação de eventos pelo Admin.
* **Taxonomia de categorias** (Admin mantém).
* Catálogo nacional com **busca** e **filtros por cidade, UF, categoria e faixa de data**.
* Lotes por evento; encerramento por **tempo** ou **quantidade**.
* Vendas online; pagamentos PIX/cartão.
* Emissão de **QR Code antifraude**; check-in web (online/offline).
* Painel do **Produtor (somente leitura)**.
* **Cupom de influenciador** no checkout.
* **Cashback ao produtor**.
* **Transferência de ingressos** com aceite do destinatário (tempo-limite configurável).
* **Mensageria** (e-mails/WhatsApp/webhooks/exports) e **cache** (catálogo/listagens/estatísticas).
* Painel administrativo e trilha de auditoria.

### Futuro (fora do MVP)

* Marketplace P2P (revenda), assentos/setorização visual, app nativo, Apple/Google Wallet, white-label.

## Requisitos Funcionais

Organização por módulos. Onde aplicável, reforça-se o `RBAC` (Admin/Produtor/Comprador/Staff).

### 1. Usuário e Autenticação

| ID | Requisito | Descrição | Prioridade |
| :--- | :--- | :--- | :--- |
| RF01 | Cadastro de Usuário | E-mail/senha e **login social** (Google/Apple); verificação por OTP/e-mail. | Alta |
| RF02 | Login | Entrar via e-mail/senha ou Google/Apple; bloquear em caso de múltiplas falhas (rate-limit). | Alta |
| RF03 | Sessão JWT | JWT (1h) e refresh (7d) com rotação e revogação. | Alta |
| RF04 | Recuperação de Senha | Link de redefinição por e-mail (expira em 30 min). | Média |
| RF05 | Perfil | Editar dados (exceto CPF); gerenciar provedores sociais vinculados. | Média |

### 2. Descoberta de Eventos (Busca & Filtros Nacionais)

| ID | Requisito | Descrição | Prioridade |
| :--- | :--- | :--- | :--- |
| RF06 | Busca Global | Campo de busca por nome do evento, local, artista/palavra-chave. | Alta |
| RF07 | Filtro por Localização | Filtrar por **cidade** e **UF** (autocompletar e seleção múltipla). | Alta |
| RF08 | Filtro por Categoria | Filtrar por **categoria** (ex.: Show, Teatro, Festa, Conferência, Esporte; mantidas pelo Admin). | Alta |
| RF09 | Filtro por Data | Filtrar por **faixa de datas** (ex.: este fim de semana, próxima semana, personalizada). | Alta |
| RF10 | Ordenação | Ordenar por data (asc/desc), popularidade e preço (asc/desc). | Média |
| RF11 | URLs Amigáveis | Páginas com **slug** SEO e parâmetros de filtro na URL (compartilhável). | Baixa |

### 3. Produtor (Onboarding e Painel – Leitura)

| ID | Requisito | Descrição | Prioridade |
| :--- | :--- | :--- | :--- |
| RF12 | Onboarding de Produtor (Admin) | Admin cadastra produtor (CNPJ/CPF, razão social, chave PIX, contrato/termos) e **habilita** acesso. | Alta |
| RF13 | Verificação/KYC | Validar CNPJ/CPF (ativos), dados bancários/PIX. | Alta |
| RF14 | Painel do Produtor — somente leitura | Métricas de vendas, check-ins, repasses e **cashback** para **eventos vinculados**; exportar CSV. | Alta |

### 4. Eventos (Criados pelo Administrador)

| ID | Requisito | Descrição | Prioridade |
| :--- | :--- | :--- | :--- |
| RF15 | Criação de Evento (Admin) | Admin cria eventos com: nome, descrição, banner, local, cidade/UF, datas início/fim, **categoria**, status (rascunho/publicado/encerrado). | Alta |
| RF16 | Edição/Exclusão (Admin) | Edição/remoção em rascunho; após publicar, apenas campos não críticos (ex.: descrição, banner). | Alta |
| RF17 | Publicação (Admin) | Publicar somente se houver pelo menos 1 **lote válido**. | Alta |
| RF18 | Página Pública do Evento | Exibir dados principais, categorias, localização, datas e botão “Comprar”. | Alta |
| RF19 | Vincular Produtor↔Evento | Admin vincula 1..N produtores ao evento para permitir painel de leitura. | Alta |
| RF20 | Gerenciar Categorias (Admin) | CRUD de categorias (nome, slug, ícone/opcional); impedir exclusão se houver eventos vinculados. | Média |

### 5. Lotes e Ingressos

| ID | Requisito | Descrição | Prioridade |
| :--- | :--- | :--- | :--- |
| RF21 | Criação de Lotes (Admin) | Lote com nome, preço, quantidade total, janela de venda (início/fim) e status. | Alta |
| RF22 | Encerramento por Limite | Encerrar automaticamente quando ocorrer primeiro: **esgotar quantidade** ou atingir fim da janela de venda. | Alta |
| RF23 | Tipos de Ingressos | Inteira, meia, VIP, cortesia; sempre vinculados a um lote. | Alta |
| RF24 | Limite por CPF | Máximo de 5 ingressos por CPF por evento (configurável). | Alta |
| RF25 | Meia-entrada | Declarar no checkout; flag registrada para verificação no check-in. | Média |

### 6. Pagamentos, Cupons e Checkout

| ID | Requisito | Descrição | Prioridade |
| :--- | :--- | :--- | :--- |
| RF26 | Checkout | Resumo de itens, taxas e total; aceite de termos e política de reembolso. | Alta |
| RF27 | PIX | QR dinâmico; **reserva 10 min**; confirmação via webhook; liberar estoque ao expirar/cancelar. | Alta |
| RF28 | Cartão | Gateway homologado (ex.: Pagar.me) com 3DS/antifraude; callbacks assíncronos. | Alta |
| RF29 | Confirmação | Em pagamento confirmado, pedido “Pago” e emissão de ingressos. | Alta |
| RF30 | Falha/Cancelamento | Cancelar pedido e liberar estoque. | Alta |
| RF31 | Cupom de Influenciador | Código por evento/lote (valor fixo/percentual), vigência, limite de uso, acúmulo configurável e **registro de atribuição** ao influenciador. | Alta |

### 7. Ingressos e QR Code

| ID | Requisito | Descrição | Prioridade |
| :--- | :--- | :--- | :--- |
| RF32 | Emissão | Após pagamento, gerar ingresso digital com ID único e **QR Code assinado digitalmente**. | Alta |
| RF33 | Validade | QR Code expira após o **primeiro uso validado**. | Alta |
| RF34 | Reenvio | Reenviar ingresso por e-mail (usuário autenticado). | Média |
| RF35 | Notificações | Enviar e-mail/WhatsApp com ingresso quando o pagamento for confirmado. | Alta |

### 8. Check-in e Validação

| ID | Requisito | Descrição | Prioridade |
| :--- | :--- | :--- | :--- |
| RF36 | Validação | Ler QR (câmera/leitor) e retornar status: válido/duplicado/expirado. | Alta |
| RF37 | Registro | Logar data, hora, operador e dispositivo da validação. | Alta |
| RF38 | Modo Offline | Validar ingressos offline com sincronização posterior. | Média |
| RF39 | Relatórios Check-in | Total de entradas validadas; exportar CSV. | Média |

### 9. Transferência de Ingressos (Carteira → Transferir)

| ID | Requisito | Descrição | Prioridade |
| :--- | :--- | :--- | :--- |
| RF40 | Iniciar Transferência (Remetente) | Usuário autenticado seleciona um ingresso **ainda não utilizado**, informa **e-mail/CPF** do destinatário e confirma; sistema cria **solicitação pendente** e envia convite ao destinatário. | Alta |
| RF41 | Aceite do Destinatário | Destinatário autentica-se/cria conta e **aceita** a transferência dentro da **janela configurável** (ex.: até 24h antes do evento, parâmetro por evento). | Alta |
| RF42 | Reemissão de Ingresso | Após aceite, o ingresso é **transferido** para a carteira do destinatário e o **QR original é invalidado**; um **novo QR assinado** é emitido; tudo registrado em auditoria. | Alta |
| RF43 | Recusa/Expiração | Em recusa ou expiração, a transferência é **cancelada** e o ingresso volta ao remetente. | Média |
| RF44 | Restrições de Transferência | Proibir transferência de ingressos **já validados**, de **meia-entrada** (opcional por política), ou quando o evento **desabilitar transferências**; respeitar **limite de quantidade e janela de tempo**. | Alta |
| RF45 | Taxa de Transferência | Ao confirmar a transferência, o sistema cobra **10% do valor original do ingresso**, como taxa de serviço. O valor é calculado automaticamente e exibido antes da confirmação. O pagamento pode ser feito via **PIX ou cartão de crédito**, e a transferência só é concluída após a compensação. | Alta |
| RF46 | Configuração da Taxa (Admin/Produtor) | O administrador ou produtor pode definir se o evento **permite ou não transferências**, bem como **ajustar o percentual da taxa** (padrão: 10%). Caso o produtor desative a cobrança, a transferência será gratuita. | Média |
| RF47 | Notificações | Envio de notificações (e-mail e/ou WhatsApp) para remetente e destinatário em cada etapa: **criada, aceita, concluída ou cancelada**. | Média |


### 10. Administração

| ID | Requisito | Descrição | Prioridade |
| :--- | :--- | :--- | :--- |
| RF48 | Painel Admin | Listar usuários, produtores, eventos, lotes, vendas, cupons, cashback e transferências. | Alta |
| RF49 | Auditoria | Registrar logs de criar/editar/publicar/cancelar/validar/transferir; trilha completa com usuário/timestamp. | Alta |
| RF50 | Fraudes | Bloquear usuários/eventos suspeitos; travar transferências quando necessário. | Alta |
| RF51 | Parâmetros Globais | Configurar taxas, **regras de cashback**, **política de transferência** (janela, restrições, taxa), limites, cupons, mensagens padrão. | Média |
| RF52 | Categorias (Taxonomia) | Manter categorias oficiais e atribuí-las aos eventos. | Média |

## Requisitos Não Funcionais

| ID | Requisito | Descrição | Categoria |
| :--- | :--- | :--- | :--- |
| RNF01 | Desempenho | P90 ≤ 2s nas páginas principais (home, catálogo, evento, carteira, painéis). | Performance |
| RNF02 | Disponibilidade | ≥ 99,5% mensal (MVP). | Confiabilidade |
| RNF03 | Segurança de Tráfego | HTTPS (TLS 1.2+) com HSTS e CSP; cookies HttpOnly/Secure/SameSite. | Segurança |
| RNF04 | Proteção de Dados | Criptografia at rest (AES-256); segredos em cofre; `RBAC` por perfis; PII minimizada. | Segurança |
| RNF05 | Sessões/JWT | Expiração 1h; refresh 7d; rotação e revogação; `device fingerprint` opcional. | Segurança |
| RNF06 | Antifraude QR | Assinatura digital (JWT + nonce) e `anti-replay`; invalidação imediata na transferência/uso. | Segurança |
| RNF07 | Escalabilidade | Horizontalização (containers/auto-scale) para picos de catálogo/checkout/check-in. | Arquitetura |
| RNF08 | Responsividade | Mobile-first; PWA para check-in. | Usabilidade |
| RNF09 | Acessibilidade | WCAG 2.1 AA. | Usabilidade |
| RNF10 | Persistência | PostgreSQL; backup diário; retenção ≥ 30 dias; testes de restauração. | Infraestrutura |
| RNF11 | Observabilidade | Logs estruturados, métricas e tracing (OpenTelemetry/Sentry). | Engenharia |
| RNF12 | Compatibilidade | Últimas 2 versões de Chrome, Firefox, Edge e Safari. | Usabilidade |
| RNF13 | LGPD | Consentimento, portabilidade e exclusão sob demanda; registro de propósito; `privacy by design`. | Conformidade |
| RNF14 | Mensageria/Filas | Broker (RabbitMQ/Kafka/SQS) para e-mails/WhatsApp, webhooks, emissão de QR, exportações, `transfer workflow`; idempotência, retries e DLQ. | Arquitetura |
| RNF15 | Cache | Redis para catálogo (busca/listas por cidade/UF/categoria/data), páginas públicas e agregações; **invalidação por evento/lote/transferência**. | Performance |
| RNF16 | Busca e Filtros | Índices por cidade, UF, data e categoria; paginação; resultados estáveis sob filtros; URLs parametrizadas. | Performance |
| RNF17 | Segurança de Transferência | Links de aceite **assinados e com expiração**; dupla confirmação; auditoria completa (quem, quando, IP/dispositivo). | Segurança |

## Regras de Negócio

| ID | Regra | Descrição |
| :--- | :--- | :--- |
| RB01 | Taxa da Plataforma | 8% sobre cada ingresso vendido. |
| RB02 | Cashback do Produtor | 2% do **líquido** das vendas (parâmetro) creditado como **saldo de cashback** ao produtor (exibido no painel). |
| RB03 | Limite por CPF | Máximo de 5 ingressos por CPF por evento (configurável). |
| RB04 | Reserva PIX | Reserva expira em 10 minutos sem confirmação. |
| RB05 | Estorno | Estornos até 7 dias antes do evento, conforme política do evento. |
| RB06 | Meia-entrada | Sujeita a comprovação no check-in; **opcionalmente não transferível** (configurável por evento). |
| RB07 | Split/Repasses | Repasses automáticos D+X conforme contrato e KYC. |
| RB08 | NFS-e | Emissão de NFS-e apenas sobre a **taxa de serviço** da plataforma. |
| RB09 | Termos/Privacidade | Aceite obrigatório dos termos e da política de privacidade (LGPD). |
| RB10 | Check-in Único | Cada ingresso (QR) pode ser validado uma única vez; tentativas repetidas são bloqueadas. |
| RB11 | Lote por Tempo/Quantidade | O lote encerra pelo primeiro limite atingido: esgotamento ou término da janela. |
| RB12 | Cupom de Influenciador | Desconto percentual/fixo com vigência e limites; registrar atribuição ao influenciador. |
| RB13 | Criação de Evento (Admin) | **Somente o Administrador** cria e publica eventos/lotes; produtores não criam. |
| RB14 | RBAC por Papel | **Admin** (CRUD global); **Produtor** (leitura dos eventos vinculados); **Comprador**(compra/carteira/transferência quando permitida); **Staff** (check-in). |
| RB15 | Política de Transferência | Transferência **permitida/negada** por evento; **janela-limite** (ex.: até 24h antes); pode haver **taxa**; requer aceite do destinatário; **meia-entrada pode ser bloqueada**. |
| RB16 | Taxonomia Oficial de Categorias | Eventos devem possuir **ao menos 1 categoria** válida (mantida pelo Admin). |
| RB17 | Localização Obrigatória | Eventos devem registrar **cidade e UF** válidas (p/ filtros nacionais). |

## Critérios de Aceitação

* **Busca & Filtros:** ao aplicar cidade=“São Paulo”, UF=“SP”, categoria=“Show” e data=“próximo fim de semana”, a lista retorna *apenas* eventos correspondentes; a URL preserva os parâmetros; limpar filtros restaura a listagem.
* **Publicação de evento (Admin):** publicar somente com ≥ 1 lote válido e categoria atribuída; página pública acessível via slug.
* **Encerramento de lote:** ao vender a última unidade *ou* atingir a hora final, o lote muda para **“encerrado”** e some do checkout.
* **Cupom de influenciador:** desconto aplicado quando código válido; registrar **atribuição**; respeitar vigência/limites e regras de acúmulo.
* **PIX com reserva:** se o webhook não confirmar em 10 min, pedido → **“cancelado”** e estoque retorna.
* **Transferência de ingresso:**
    * Remetente inicia; destinatário recebe link com expiração; ao **aceitar dentro da janela**, ingresso migra para a carteira do destinatário; **QR antigo invalida** e **novo QR** é emitido.
    * Se recusar/expirar, ingresso retorna ao remetente.
    * Ingresso já validado **não pode** ser transferido; se a política do evento bloquear meia-entrada, a tentativa falha com mensagem.
* **Cashback do produtor:** ao encerrar o período do evento, creditar 2% do líquido (ou parâmetro) no saldo do produtor; refletir em painel/extrato.
* **Mensageria:** e-mails/WhatsApp, emissão de QR, exportações e fluxo de transferência **assíncronos com retries e DLQ**; requisições síncronas não bloqueiam.
* **Cache:** listagens por cidade/UF/categoria/data com baixa latência; qualquer alteração relevante (evento/lote/transferência) **invalida** caches afetados.

## Requisitos Futuros e Extensões

App nativo; Apple/Google Wallet; afiliados avançado; **revenda P2P** (marketplace); assentos visuais; white-label.

## Considerações Finais

A versão **1.4** destaca a **descoberta nacional** (busca/filtros por cidade/UF/categoria/data) e introduz a **transferência de ingressos** com aceite e reemissão segura do QR, mantendo a governança (Admin cria/vincula), o controle de acesso (RBAC), a robustez (mensageria + cache) e o incentivo financeiro ao **produtor** (cashback).

## Histórico de Versão

| Versão | Alteração | Responsável | Data |
| :--- | :--- | :--- | :--- |
| 1.0 | Elaboração inicial | Gabriel Lima | 15/10/2025 |
| 1.1 | Eventos por Admin; lotes por tempo/quantidade; cupom; mensageria e cache | Gabriel Lima | 16/10/2025 |
| 1.2 | Cashback do produtor; remoção de cashback do usuário; ajustes em escopo, RF, RNF e regras | Gabriel Lima | 16/10/2025 |
| 1.3 | Onboarding de produtor pelo Admin; **vinculação Produtor↔Evento**; reforço de RBAC | Gabriel Lima | 16/10/2025 |
| 1.4 | Busca & filtros nacionais (cidade/UF/categoria/data), **taxonomia de categorias**, e **transferência de ingressos com aceite e reemissão segura de QR** | Gabriel Lima | 16/10/2025 |