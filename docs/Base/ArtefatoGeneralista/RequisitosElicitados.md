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

A versão **1.6** incorpora novas funcionalidades identificadas no diagrama de classes do sistema: **produtos e serviços além de ingressos**, **sistema de notificações detalhado**, **rastreamento de transações de cashback**, **check-in aprimorado com detecção de fraude** e **suporte a cartão de débito** nos pagamentos. Além disso, mantém todas as funcionalidades da versão **1.5** incluindo expansão significativa dos requisitos de **acessibilidade** para pessoas com deficiência:
* **Cobertura nacional** com ênfase em **busca, filtros por localização (cidade/UF) e categorização** de eventos;
* **Transferência de ingressos entre usuários** (carteira → transferência com aceite do destinatário e reemissão do QR);
* Manutenção das decisões anteriores: **evento criado exclusivamente pelo Administrador**, **lote encerra por tempo** ou **quantidade (o que vier primeiro)**, **cupom de influenciador**, **mensageria + cache**, **cashback destinado ao produtor** e **vinculação Produtor↔Evento** para acesso de leitura.
* **Acessibilidade ampliada**: Requisitos detalhados para conformidade WCAG 2.1 AA, suporte a leitores de tela, navegação por teclado, contraste e legibilidade, e acessibilidade específica para pessoas com deficiência visual, auditiva, motora e cognitiva.

## Visão Geral

Plataforma nacional para **venda e validação de ingressos e produtos/serviços** com pagamentos via **PIX, cartão de crédito e débito**, **QR Code antifraude**, **cupons de influenciadores**, **cashback ao produtor rastreável**, **busca e filtros nacionais (cidade/UF/categorias/data)**, **sistema de notificações completo** e **transferência de ingressos** controlada e auditável.

## Objetivos do Projeto

* Emitir, vender, **filtrar e descobrir** eventos no Brasil com **experiência de busca eficiente**.
* Garantir segurança: antifraude (QR assinado), check-in confiável (online/offline) e LGPD.
* Escalar via **mensageria** e **cache** para baixa latência em catálogos e relatórios.
* Potencializar aquisição (cupons) e retenção (boa UX e clareza).
* Isolar administração: Admin cria/edita/publica eventos e lotes; Produtor tem **somente leitura** dos eventos vinculados.
* Permitir **transferência de ingressos** com aceite do destinatário e reemissão de QR, preservando trilha de auditoria.

## Personas

* **Usuário Comprador** — busca por cidade/UF/categoria, filtra por data, compra ingressos e produtos via PIX/cartão, aplica cupom, transfere ingresso quando permitido, recebe notificações sobre suas compras e transferências.
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
* **Produtos e serviços** vendidos junto com eventos (merchandising, serviços adicionais).
* Vendas online; pagamentos PIX/cartão de crédito/débito.
* Emissão de **QR Code antifraude**; check-in web (online/offline) com detecção de fraude.
* Painel do **Produtor (somente leitura)**.
* **Cupom de influenciador** no checkout.
* **Cashback ao produtor** com rastreamento de transações (créditos/débitos/ajustes).
* **Transferência de ingressos** com aceite do destinatário (tempo-limite configurável).
* **Sistema de notificações** completo (e-mail/WhatsApp) com tipos específicos e controle de leitura.
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
| RF21 | Criação de Lotes (Admin) | Lote com nome, preço, quantidade total, janela de venda (início/fim) e status (SCHEDULED, ACTIVE, SOLD_OUT, EXPIRED, CANCELLED). | Alta |
| RF22 | Encerramento por Limite | Encerrar automaticamente quando ocorrer primeiro: **esgotar quantidade** ou atingir fim da janela de venda. | Alta |
| RF23 | Tipos de Ingressos | Inteira, meia, VIP, cortesia; sempre vinculados a um lote. | Alta |
| RF24 | Limite por CPF | Máximo de 5 ingressos por CPF por evento (configurável). | Alta |
| RF25 | Meia-entrada | Declarar no checkout; flag registrada para verificação no check-in. | Média |

### 5.1. Produtos e Serviços

| ID | Requisito | Descrição | Prioridade |
| :--- | :--- | :--- | :--- |
| RF53 | Criação de Produtos (Admin) | Admin cria produtos/serviços vinculados a eventos com: nome, descrição, tipo (SERVICE, MERCH, etc.), preço, quantidade total, quantidade vendida e status ativo. | Alta |
| RF54 | Gestão de Produtos | Editar, ativar/desativar produtos; controlar estoque e vendas; produtos aparecem no checkout junto com ingressos. | Alta |
| RF55 | Tipos de Item no Pedido | Pedido pode conter itens do tipo **TICKET** (ingressos) ou **PRODUCT** (produtos/serviços); OrderItem diferencia entre ingressos e produtos. | Alta |
| RF56 | Estoque de Produtos | Controlar disponibilidade de produtos; impedir venda quando esgotado; sincronizar com pedidos. | Alta |

### 6. Pagamentos, Cupons e Checkout

| ID | Requisito | Descrição | Prioridade |
| :--- | :--- | :--- | :--- |
| RF26 | Checkout | Resumo de itens (ingressos e produtos), taxas e total; aceite de termos e política de reembolso. | Alta |
| RF27 | PIX | QR dinâmico; **reserva 10 min**; confirmação via webhook; liberar estoque ao expirar/cancelar. Status: PENDING, PROCESSING, APPROVED, REFUSED, CANCELLED, REFUNDED, EXPIRED. | Alta |
| RF28 | Cartão de Crédito | Gateway homologado (ex.: Pagar.me) com 3DS/antifraude; callbacks assíncronos; suporte a parcelamento. | Alta |
| RF28.1 | Cartão de Débito | Suporte a pagamento via cartão de débito; processamento via gateway homologado. | Alta |
| RF29 | Confirmação | Em pagamento confirmado, pedido muda para "PAID" e emissão de ingressos; produtos confirmados no pedido. | Alta |
| RF30 | Falha/Cancelamento | Cancelar pedido e liberar estoque de ingressos e produtos; status REFUNDED quando reembolsado. | Alta |
| RF31 | Cupom de Influenciador | Código por evento/lote (valor fixo/percentual), vigência, limite de uso (maxUsed), acúmulo configurável e **registro de atribuição** ao influenciador. | Alta |

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
| RF36 | Validação | Ler QR (câmera/leitor) e retornar status: **VALID**, **ALREADY_USED**, **INVALID**, **EXPIRED**, **FRAUD_ATTEMPT**. | Alta |
| RF37 | Registro Detalhado | Logar data, hora, operador (operatorId), dispositivo (deviceId), IP address, localização geográfica (location), informações do dispositivo (deviceInfo) e modo (online/offline). | Alta |
| RF38 | Modo Offline | Validar ingressos offline com sincronização posterior; flag isOffline para indicar validações offline. | Média |
| RF39 | Relatórios Check-in | Total de entradas validadas; exportar CSV com detalhes completos (dispositivo, IP, localização). | Média |
| RF57 | Detecção de Fraude | Sistema deve identificar tentativas suspeitas (mesmo IP, dispositivo diferente, múltiplas tentativas) e marcar como FRAUD_ATTEMPT. | Média |

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


### 10. Notificações

| ID | Requisito | Descrição | Prioridade |
| :--- | :--- | :--- | :--- |
| RF58 | Sistema de Notificações | Gerenciar notificações com tipos específicos: ORDER_CONFIRMED, TICKET_ISSUED, TRANSFER_INVITED, TRANSFER_ACCEPTED, TRANSFER_CANCELLED, CHECKIN_SUCCESS, PASSWORD_RESET, EMAIL_VERIFICATION. | Alta |
| RF59 | Canais de Notificação | Enviar notificações via EMAIL ou WHATSAPP conforme preferência do usuário; suporte a múltiplos canais. | Alta |
| RF60 | Status de Notificação | Rastrear status de envio (pending, sent, failed) e leitura (read/unread) com timestamps (sentAt, readAt). | Média |
| RF61 | Histórico de Notificações | Usuário pode visualizar histórico de notificações recebidas; marcar como lidas/não lidas. | Média |

### 11. Cashback e Transações

| ID | Requisito | Descrição | Prioridade |
| :--- | :--- | :--- | :--- |
| RF62 | Transações de Cashback | Registrar todas as transações de cashback (CREDIT, DEBIT, ADJUSTMENT) vinculadas a pedidos ou eventos; manter saldo atualizado (balanceAfter). | Alta |
| RF63 | Extrato de Cashback | Produtor pode visualizar extrato completo de transações com descrição, data, valor e saldo acumulado; filtrar por evento ou período. | Alta |
| RF64 | Configuração de Percentual | Admin/Produtor pode configurar percentual de cashback por evento (producerCashbackPercent); usar percentual padrão do produtor (defaultCashbackPercent) quando não especificado. | Média |

### 12. Administração

| ID | Requisito | Descrição | Prioridade |
| :--- | :--- | :--- | :--- |
| RF48 | Painel Admin | Listar usuários, produtores, eventos, lotes, produtos, vendas, cupons, cashback, transações e transferências. | Alta |
| RF49 | Auditoria | Registrar logs de criar/editar/publicar/cancelar/validar/transferir; trilha completa com usuário/timestamp. | Alta |
| RF50 | Fraudes | Bloquear usuários/eventos suspeitos; travar transferências quando necessário; identificar tentativas de fraude no check-in. | Alta |
| RF51 | Parâmetros Globais | Configurar taxas, **regras de cashback**, **política de transferência** (janela, restrições, taxa), limites, cupons, mensagens padrão, percentual de cashback por evento. | Média |
| RF52 | Categorias (Taxonomia) | Manter categorias oficiais e atribuí-las aos eventos. | Média |
| RF65 | Gestão de Localização | CRUD de localizações com foto (photoUrl), complemento, CEP (postalCode) e coordenadas geográficas; reutilizar localizações entre eventos. | Média |

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
| RNF09 | Acessibilidade Web (WCAG 2.1 AA) | Conformidade com **WCAG 2.1 nível AA** nas diretrizes de Percebível, Operável, Compreensível e Robusto. Critérios essenciais: contraste mínimo 4.5:1 (texto normal) e 3:1 (texto grande); textos alternativos descritivos em imagens; estrutura semântica HTML5; navegação por teclado completa; foco visível e indicadores de estado; labels e instruções claras em formulários; mensagens de erro acessíveis. | Usabilidade |
| RNF10 | Persistência | PostgreSQL; backup diário; retenção ≥ 30 dias; testes de restauração. | Infraestrutura |
| RNF11 | Observabilidade | Logs estruturados, métricas e tracing (OpenTelemetry/Sentry). | Engenharia |
| RNF12 | Compatibilidade | Últimas 2 versões de Chrome, Firefox, Edge e Safari. | Usabilidade |
| RNF13 | LGPD | Consentimento, portabilidade e exclusão sob demanda; registro de propósito; `privacy by design`. | Conformidade |
| RNF14 | Mensageria/Filas | Broker (RabbitMQ/Kafka/SQS) para e-mails/WhatsApp, webhooks, emissão de QR, exportações, `transfer workflow`; idempotência, retries e DLQ. | Arquitetura |
| RNF15 | Cache | Redis para catálogo (busca/listas por cidade/UF/categoria/data), páginas públicas e agregações; **invalidação por evento/lote/transferência**. | Performance |
| RNF16 | Busca e Filtros | Índices por cidade, UF, data e categoria; paginação; resultados estáveis sob filtros; URLs parametrizadas. | Performance |
| RNF17 | Segurança de Transferência | Links de aceite **assinados e com expiração**; dupla confirmação; auditoria completa (quem, quando, IP/dispositivo). | Segurança |
| RNF18 | Suporte a Leitores de Tela | Compatibilidade total com leitores de tela (NVDA, JAWS, VoiceOver, TalkBack). Implementação de **ARIA labels**, **aria-live regions** para atualizações dinâmicas, **landmarks** para navegação por pontos de referência, **roles semânticos** e estados acessíveis (aria-expanded, aria-selected, aria-hidden). Feedback sonoro em ações críticas (compra confirmada, erro). | Usabilidade |
| RNF19 | Navegação por Teclado | Funcionalidade completa via teclado sem dependência de mouse. Tab order lógico e sequencial; atalhos de teclado para ações principais (p.ex.: Enter para comprar, Esc para fechar modais); suporte a teclas de navegação (setas, Page Up/Down, Home/End); **skip links** para pular conteúdo repetitivo; foco visível em todos os elementos interativos. | Usabilidade |
| RNF20 | Contraste e Legibilidade | Taxa de contraste mínimo **4.5:1** para texto normal e **3:1** para texto grande (≥18pt ou ≥14pt bold). Texto não deve depender apenas de cor para transmitir informação. Opção de **modo de alto contraste** ou tema escuro/claro customizável. Tipografia legível com tamanho mínimo de 12pt e espaçamento adequado entre linhas (≥1.5). | Usabilidade |
| RNF21 | Acessibilidade em Formulários | Labels associados a todos os campos; instruções claras antes ou dentro dos campos; mensagens de erro específicas e posicionadas próximo ao campo; agrupamento lógico de campos relacionados; indicação de campos obrigatórios via texto e símbolo; validação em tempo real com feedback acessível; autocomplete quando aplicável. | Usabilidade |
| RNF22 | Mídia e Conteúdo Multimodal | **Textos alternativos descritivos** para todas as imagens informativas; **legendas** para vídeos; **transcrições** para conteúdo de áudio; **descrições de áudio** para vídeos importantes; controle de reprodução (play/pause) em todos os conteúdos multimídia; opção de pausar/parar animações automáticas. | Usabilidade |
| RNF23 | Navegação e Estrutura | Estrutura semântica clara com cabeçalhos hierárquicos (h1-h6); breadcrumbs para orientação; menu de navegação consistente e previsível; múltiplas formas de encontrar conteúdo (busca, filtros, categorias); indicação clara da página atual; links descritivos (evitar "clique aqui"). | Usabilidade |
| RNF24 | Acessibilidade Mobile e Touch | Áreas de toque mínimas de **44x44 pixels**; espaçamento adequado entre elementos interativos; gestos alternativos para ações complexas (swipe, pinch); suporte a VoiceOver (iOS) e TalkBack (Android); rotação de tela funcional; zoom até 200% sem perda de funcionalidade; teclado virtual apropriado conforme o tipo de campo. | Usabilidade |
| RNF25 | Acessibilidade de Conteúdo Dinâmico | Atualizações dinâmicas (Ajax, SPA) anunciadas via **aria-live** sem interromper o usuário; loading states acessíveis; erros exibidos de forma não intrusiva; confirmações de ação claras; mudanças de contexto só quando solicitadas pelo usuário; tempo adequado para ler e interagir com conteúdo temporário. | Usabilidade |
| RNF26 | Acessibilidade em Pagamentos e Checkout | Processo de checkout acessível passo a passo com indicação clara de progresso; resumo de compra acessível antes da confirmação; campos de pagamento com labels e máscaras apropriadas; confirmação de ações críticas (tampar confirmação com Enter); mensagens de erro de pagamento claras e acionáveis; QR Code com descrição textual alternativa. | Usabilidade |
| RNF27 | Acessibilidade para Pessoas com Deficiência Motora | Suporte a tecnologias assistivas de entrada alternativa (teclados adaptativos, switches, controle por voz); tolerância a erros de clique/toque; tempo suficiente para completar ações; possibilidade de desfazer ações acidentais; formulários com auto-save quando apropriado; atalhos de teclado para todas as ações principais. | Usabilidade |
| RNF28 | Acessibilidade para Pessoas com Deficiência Cognitiva | Linguagem clara e simples; instruções passo a passo para processos complexos; ajuda contextual disponível; prevenção de erros com validação proativa; possibilidade de cancelar ou revisar antes de confirmar; layout consistente e previsível; ícones acompanhados de texto. | Usabilidade |

## Regras de Negócio

| ID | Regra | Descrição |
| :--- | :--- | :--- |
| RB01 | Taxa da Plataforma | 8% sobre cada ingresso vendido. |
| RB02 | Cashback do Produtor | 2% do **líquido** das vendas (parâmetro) creditado como **saldo de cashback** ao produtor; percentual configurável por evento (producerCashbackPercent) ou usa padrão do produtor (defaultCashbackPercent); todas as transações são registradas (ProducerCashbackTransaction). |
| RB03 | Limite por CPF | Máximo de 5 ingressos por CPF por evento (configurável). |
| RB04 | Reserva PIX | Reserva expira em 10 minutos sem confirmação; pedido muda para status EXPIRED. |
| RB05 | Estorno | Estornos até 7 dias antes do evento, conforme política do evento; pagamento muda para status REFUNDED. |
| RB06 | Meia-entrada | Sujeita a comprovação no check-in; **opcionalmente não transferível** (configurável por evento). |
| RB07 | Split/Repasses | Repasses automáticos D+X conforme contrato e KYC. |
| RB08 | NFS-e | Emissão de NFS-e apenas sobre a **taxa de serviço** da plataforma. |
| RB09 | Termos/Privacidade | Aceite obrigatório dos termos e da política de privacidade (LGPD). |
| RB10 | Check-in Único | Cada ingresso (QR) pode ser validado uma única vez; tentativas repetidas retornam status ALREADY_USED ou FRAUD_ATTEMPT; registro detalhado (deviceId, IP, location, deviceInfo). |
| RB11 | Lote por Tempo/Quantidade | O lote encerra pelo primeiro limite atingido: esgotamento ou término da janela; status: SCHEDULED, ACTIVE, SOLD_OUT, EXPIRED, CANCELLED. |
| RB12 | Cupom de Influenciador | Desconto percentual/fixo com vigência e limites (maxUsed); registrar atribuição ao influenciador. |
| RB13 | Criação de Evento (Admin) | **Somente o Administrador** cria e publica eventos/lotes/produtos; produtores não criam. Eventos podem ter status DRAFT, PUBLISHED, CANCELLED, FINISHED. |
| RB14 | RBAC por Papel | **Admin** (CRUD global); **Produtor** (leitura dos eventos vinculados); **Comprador**(compra/carteira/transferência quando permitida); **Staff** (check-in). |
| RB15 | Política de Transferência | Transferência **permitida/negada** por evento; **janela-limite** (ex.: até 24h antes); pode haver **taxa**; requer aceite do destinatário; **meia-entrada pode ser bloqueada**. Status: PENDING, ACCEPTED, REFUSED, CANCELLED, EXPIRED, COMPLETED. |
| RB16 | Taxonomia Oficial de Categorias | Eventos devem possuir **ao menos 1 categoria** válida (mantida pelo Admin). |
| RB17 | Localização Obrigatória | Eventos devem registrar **cidade e UF** válidas (p/ filtros nacionais); localização pode incluir foto, complemento e CEP. |
| RB18 | Produtos em Eventos | Produtos/serviços podem ser vendidos junto com ingressos; OrderItem diferencia entre TICKET e PRODUCT; produtos têm controle de estoque (totalQuantity, soldQuantity). |
| RB19 | Status de Pedido | Pedido pode ter status: PENDING, AWAITING_PAYMENT, PAID, CANCELLED, EXPIRED, REFUNDED. |
| RB20 | Status de Pagamento | Pagamento pode ter status: PENDING, PROCESSING, APPROVED, REFUSED, CANCELLED, REFUNDED, EXPIRED. Método: CREDIT_CARD, DEBIT_CARD, PIX. |
| RB21 | Status de Ticket | Ingresso pode ter status: ACTIVE, TRANSFERRED, VALIDATED, CANCELLED, EXPIRED. |
| RB22 | Notificações | Todas as ações críticas geram notificações (ORDER_CONFIRMED, TICKET_ISSUED, TRANSFER_INVITED, TRANSFER_ACCEPTED, TRANSFER_CANCELLED, CHECKIN_SUCCESS, PASSWORD_RESET, EMAIL_VERIFICATION); suporte a EMAIL e WHATSAPP; rastreamento de leitura (read/unread). |

## Critérios de Aceitação

* **Busca & Filtros:** ao aplicar cidade="São Paulo", UF="SP", categoria="Show" e data="próximo fim de semana", a lista retorna *apenas* eventos correspondentes; a URL preserva os parâmetros; limpar filtros restaura a listagem.
* **Publicação de evento (Admin):** publicar somente com ≥ 1 lote válido e categoria atribuída; página pública acessível via slug; evento pode ter status DRAFT, PUBLISHED, CANCELLED, FINISHED.
* **Encerramento de lote:** ao vender a última unidade *ou* atingir a hora final, o lote muda para status **SOLD_OUT** ou **EXPIRED** e some do checkout.
* **Produtos em eventos:** Admin pode criar produtos/serviços vinculados ao evento; produtos aparecem no checkout junto com ingressos; OrderItem diferencia entre TICKET e PRODUCT.
* **Cupom de influenciador:** desconto aplicado quando código válido; registrar **atribuição**; respeitar vigência/limites (maxUsed) e regras de acúmulo.
* **PIX com reserva:** se o webhook não confirmar em 10 min, pedido → status **EXPIRED** e estoque retorna; pagamento muda para EXPIRED.
* **Pagamentos:** suporte a CREDIT_CARD, DEBIT_CARD e PIX; status: PENDING, PROCESSING, APPROVED, REFUSED, CANCELLED, REFUNDED, EXPIRED.
* **Transferência de ingresso:**
    * Remetente inicia; destinatário recebe link com expiração; ao **aceitar dentro da janela**, ingresso migra para a carteira do destinatário; **QR antigo invalida** e **novo QR** é emitido; status muda para COMPLETED.
    * Se recusar/expirar, ingresso retorna ao remetente; status CANCELLED ou EXPIRED.
    * Ingresso já validado **não pode** ser transferido; se a política do evento bloquear meia-entrada, a tentativa falha com mensagem.
* **Check-in:** validação retorna status VALID, ALREADY_USED, INVALID, EXPIRED ou FRAUD_ATTEMPT; registra deviceId, IP address, location, deviceInfo, modo online/offline.
* **Cashback do produtor:** ao encerrar o período do evento, creditar percentual configurável (producerCashbackPercent ou defaultCashbackPercent) do líquido no saldo do produtor; criar transação tipo CREDIT; refletir em painel/extrato com histórico completo (ProducerCashbackTransaction).
* **Notificações:** ações críticas geram notificações específicas (ORDER_CONFIRMED, TICKET_ISSUED, TRANSFER_INVITED, TRANSFER_ACCEPTED, TRANSFER_CANCELLED, CHECKIN_SUCCESS, PASSWORD_RESET, EMAIL_VERIFICATION); envio via EMAIL ou WHATSAPP; rastreamento de status (sentAt, readAt, read).
* **Mensageria:** e-mails/WhatsApp, emissão de QR, exportações e fluxo de transferência **assíncronos com retries e DLQ**; requisições síncronas não bloqueiam.
* **Cache:** listagens por cidade/UF/categoria/data com baixa latência; qualquer alteração relevante (evento/lote/transferência/produto) **invalida** caches afetados.

## Requisitos Futuros e Extensões

App nativo; Apple/Google Wallet; afiliados avançado; **revenda P2P** (marketplace); assentos visuais; white-label.

## Considerações Finais

A versão **1.6** incorpora novas funcionalidades identificadas no diagrama de classes do sistema: **produtos e serviços além de ingressos** (RF53-RF56), **sistema de notificações completo** (RF58-RF61), **rastreamento detalhado de transações de cashback** (RF62-RF64), **check-in aprimorado com detecção de fraude** (RF57), **suporte a cartão de débito** (RF28.1) e **gestão de localizações** (RF65). 

Além disso, mantém todas as funcionalidades da versão **1.5**, incluindo expansão significativa dos **requisitos de acessibilidade** (RNF09-RNF28), garantindo que a plataforma Ingressou seja acessível para pessoas com deficiência visual, auditiva, motora e cognitiva, em conformidade com WCAG 2.1 nível AA. 

O modelo contempla ainda: **descoberta nacional** (busca/filtros por cidade/UF/categoria/data), **transferência de ingressos** com aceite e reemissão segura do QR, governança (Admin cria/vincula), controle de acesso (RBAC), robustez (mensageria + cache) e incentivo financeiro ao **produtor** com rastreamento completo de cashback (transações CREDIT/DEBIT/ADJUSTMENT).

## Histórico de Versão

| Versão | Alteração | Responsável | Data |
| :--- | :--- | :--- | :--- |
| 1.0 | Elaboração inicial | Gabriel Lima | 15/10/2025 |
| 1.1 | Eventos por Admin; lotes por tempo/quantidade; cupom; mensageria e cache | Gabriel Lima | 16/10/2025 |
| 1.2 | Cashback do produtor; remoção de cashback do usuário; ajustes em escopo, RF, RNF e regras | Gabriel Lima | 16/10/2025 |
| 1.3 | Onboarding de produtor pelo Admin; **vinculação Produtor↔Evento**; reforço de RBAC | Gabriel Lima | 16/10/2025 |
| 1.4 | Busca & filtros nacionais (cidade/UF/categoria/data), **taxonomia de categorias**, e **transferência de ingressos com aceite e reemissão segura de QR** | Gabriel Lima | 16/10/2025 |
| 1.5 | Expansão significativa dos requisitos não funcionais de **acessibilidade** (RNF09-RNF28): especificações detalhadas para pessoas com deficiência visual, auditiva, motora e cognitiva; conformidade WCAG 2.1 AA; suporte a leitores de tela; navegação por teclado; contraste e legibilidade; acessibilidade mobile e de conteúdo dinâmico | Gabriel Lima | 27/10/2025 |
| 1.6 | **Nova funcionalidades baseadas no diagrama de classes**: (1) **Módulo de Produtos e Serviços** (RF53-RF56) - produtos/serviços vendidos junto com eventos, OrderItem suporta TICKET ou PRODUCT, controle de estoque; (2) **Sistema de Notificações Completo** (RF58-RF61) - tipos específicos (ORDER_CONFIRMED, TICKET_ISSUED, TRANSFER_INVITED, etc.), canais EMAIL/WHATSAPP, rastreamento de leitura; (3) **Transações de Cashback Rastreáveis** (RF62-RF64) - ProducerCashbackTransaction com tipos CREDIT/DEBIT/ADJUSTMENT, extrato completo, percentual configurável por evento; (4) **Check-in Aprimorado** (RF57) - status detalhados (VALID, ALREADY_USED, INVALID, EXPIRED, FRAUD_ATTEMPT), registro de deviceId/IP/location/deviceInfo; (5) **Suporte a Cartão de Débito** (RF28.1); (6) **Gestão de Localizações** (RF65) - foto, complemento, CEP; (7) Atualizações em status de pedidos, pagamentos, lotes e tickets conforme enums do diagrama | Gabriel Lima | 21/11/2025 |