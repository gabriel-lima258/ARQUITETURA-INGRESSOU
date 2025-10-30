# Diagrama de Atividades

> **Versão:** 1.0  
> **Data:** Outubro de 2025  
> **Autor:** Gabriel Lima  
> **Projeto:** Ingressou — Plataforma Web de Venda e Gestão de Ingressos  

---

## Sumário

- [Introdução](#introdução)
- [Objetivos](#objetivos)
- [Metodologia](#metodologia)
- [Sobre o Diagrama de Atividades](#sobre-o-diagrama-de-atividades)
- [Comprar Ingresso](#comprar-ingresso)
- [Realizar Check-in de Ingresso](#realizar-check-in-de-ingresso)
- [Criar e Publicar Evento (Admin)](#criar-e-publicar-evento-admin)
- [Conclusão](#conclusão)
- [Bibliografia](#bibliografia)
- [Histórico de versão](#histórico-de-versão)

---

## Introdução

O **Ingressou** é uma plataforma web para **venda e gestão de ingressos** desenvolvida na disciplina. Para organizar e representar o comportamento e os fluxos de processos do sistema, foram elaborados diagramas de atividade conforme a notação UML (Unified Modeling Language), focando nos principais processos de negócio identificados nos artefatos de análise e modelagem.

Segundo a Apostila UML - Unified Modeling Language - Linguagem de Modelagem Unificada em Português [1](#ref1), os diagramas de atividade são uma forma de representar o fluxo sequencial das ações realizadas por uma operação do sistema ao evidenciar as mudanças de estado dos objetos envolvidos, a ordem de execução e a responsabilidade pelas tarefas por meio de raias (swimlanes). Sendo assim, eles são especialmente úteis para modelar fluxos de trabalho, decisões, execuções paralelas e resultados esperados. Além disso, conforme destaca a [IBM](https://www.ibm.com/docs/pt-br/rational-soft-arch/9.7.0?topic=diagrams-activity) [2](#ref2), esses diagramas são semelhantes a fluxogramas, mas com maior capacidade de representar fluxos paralelos e alternativos.

---

## Objetivos

O objetivo deste documento é apresentar os principais fluxos funcionais e comportamentais do sistema **Ingressou** através de diagramas de atividades. De forma mais específica, busca-se:

- Ilustrar os principais processos internos da plataforma, especialmente relacionados à **venda de ingressos**, **check-in** e **gestão administrativa**;
- Demonstrar a responsabilidade dos atores e componentes por meio das raias;
- Evidenciar os pontos de decisão, bifurcação e encerramento dos fluxos;
- Apoiar a modelagem comportamental dos casos de uso com uma representação visual precisa;
- Documentar a integração entre componentes do sistema (frontend, API Gateway, serviços de domínio, infraestrutura).

---

## Metodologia

A elaboração dos diagramas de atividade seguirá uma abordagem baseada na integração entre diferentes artefatos desenvolvidos anteriormente no projeto **Ingressou**. Com isso, será representado visualmente o fluxo das ações executadas pelos usuários e pelo sistema nos principais processos de negócio:

- **Comprar Ingresso**: Fluxo completo desde a seleção do evento até a confirmação do pagamento e emissão do ingresso digital;
- **Realizar Check-in**: Processo de validação de ingressos via QR Code, incluindo modo offline;
- **Criar e Publicar Evento (Admin)**: Fluxo administrativo de criação de eventos e lotes, com publicação para o público.

 Para isso, serão feitas as seguintes etapas:

1. Inicialmente serão realizadas análises dos seguintes artefatos:
   - [5W2H](/Base/ArtefatoGeneralista/5W2H.md) — definição dos módulos e processos-chave;
   - [Diagrama de Classes](/Modelagem/ModelagemEstatica/DiagramaClasses.md) — estrutura de entidades e relacionamentos;
   - [Diagrama de Componentes](/Modelagem/ModelagemEstatica/DiagramaComponentes.md) — arquitetura de componentes e interfaces;
   - [Diagrama de Casos de Uso](/Modelagem/ModelagemOrganizacional/DiagramaCasosUso.md) — casos de uso CU-01, CU-02, CU-11, CU-12;
2. Os diagramas serão desenvolvidos na ferramenta Draw.io, seguindo notação UML 2.0;
3. Será aplicada verificação por meio de checklist de boas práticas de UML;

---

## Sobre o Diagrama de Atividades

Ao se desenvolver os diagramas de atividade, é necessário levar em consideração que esse tipo de representação tem como objetivo principal demonstrar o fluxo de ações dentro de um processo ao ilustrar como as atividades ocorrem e se conectam. Com base nisso, no projeto do **Ingressou**, foram elaborados três diagramas de atividades principais:

1. **Comprar Ingresso**: Representa o fluxo completo de compra, desde a seleção até a emissão do ingresso;
2. **Realizar Check-in de Ingresso**: Demonstra o processo de validação e registro de uso do ingresso;
3. **Criar e Publicar Evento (Admin)**: Mostra o fluxo administrativo de criação e publicação de eventos.

Todos foram estruturados para refletir a sequência das operações esperadas no sistema, conforme as funcionalidades previamente definidas nos diagramas de classes e de componentes, e alinhados com os casos de uso documentados.

A estrutura do diagrama de atividades utiliza elementos visuais específicos para representar os passos e decisões envolvidos em um fluxo. Entre eles, destaca-se o nó inicial, que marca o ponto de partida da atividade, e o nó final, que encerra o fluxo, segundo [UML Activity Diagram Controls](https://www.uml-diagrams.org/activity-diagrams-controls.html) [5](#ref5). As ações são representadas por retângulos arredondados e indicam as tarefas a serem executadas. Para melhor compreensão dos elementos, a figura 1 abaixo funciona como uma legenda para os diagramas elaborados.

<div align="center">
    <b>Figura 1:</b> Legenda do Diagrama de Atividades
    <br>
    <img src="assets/Legendas/LegendaDiagramaAtividade.drawio.png" width="500">
    <br>
    <b>Autor:</b> <a href="https://github.com/gabriel-lima258">Gabriel Lima</a>.
    <br>
</div>

---

## Comprar Ingresso

Este diagrama representa o fluxo completo de compra de ingressos, baseado no **CU-01 (Comprar Ingresso)** e nos componentes identificados no **Diagrama de Componentes**. O processo envolve múltiplos componentes: **SPA Principal**, **Gateway Service**, **EventSearchService**, **CheckoutService**, **PaymentOrchestrator**, **TicketingService** e **NotificationService**, além de integrações externas com **Gateway de Pagamento**.

Para complementar a representação visual do fluxo de compra, a Tabela 1 a seguir detalha cada uma das principais ações, decisões e estados presentes no diagrama correspondente. Esta tabulação foi elaborada com o intuito de facilitar a leitura e a compreensão sequencial do processo, indicando a ordem de execução, condições e próximos passos.

<details>
  <summary><strong>Tabela 1: Fluxo Completo de Compra de Ingresso (Início ao Fim)</strong></summary>

**Tabela 1: Fluxo Completo de Compra de Ingresso (Início ao Fim)**

| # | Atividade | Responsável | Condição/Decisão | Próximo Passo | Caso de Uso | Classes Envolvidas | Componentes |
|---|---|---|---|---|---|---|---|
| **1** | **INÍCIO** | - | Cliente inicia processo | Passo 2 | CU-01 | - | SPA Principal |
| **2** | Acessar Plataforma | Cliente | - | Passo 3 | CU-01 | Cliente | SPA Principal |
| **3** | Verificar Autenticação | Sistema | **Decisão:** Usuário autenticado? | Se não: Passo 3a<br>Se sim: Passo 4 | CU-01 | Usuario, Cliente | AuthService, Gateway Service |
| **3a** | Autenticar Usuário | Sistema | Login realizado | Passo 4 | CU-01 | Usuario, Cliente | AuthService, Gateway Service |
| **4** | Buscar Eventos Disponíveis | Cliente → Sistema | Cliente navega ou busca | Passo 5 | CU-07, CU-08 | Evento, Categoria | EventSearchService, Cache (Redis) |
| **5** | Selecionar Evento | Cliente | Cliente escolhe evento | Passo 6 | CU-08 | Evento | SPA Principal |
| **6** | Visualizar Detalhes do Evento | Sistema | Exibe informações | Passo 7 | CU-08 | Evento, Localizacao, Lote | EventSearchService |
| **7** | Selecionar Lote e Quantidade | Cliente | Cliente escolhe ingresso(s) | Passo 8 | CU-01 | Lote | SPA Principal |
| **8** | Verificar Aplicação de Cupom | Cliente → Sistema | **Decisão:** Cliente deseja aplicar cupom? | Se sim: Passo 8a<br>Se não: Passo 9 | CU-16 | Cupom | SPA Principal |
| **8a** | Inserir Código do Cupom | Cliente | - | Passo 8b | CU-16 | Cupom | SPA Principal |
| **8b** | Validar Cupom | Sistema | **Decisão:** Cupom válido? | Se válido: Passo 8c<br>Se inválido: Passo 8d | CU-16 | Cupom | CheckoutService |
| **8c** | Aplicar Desconto | Sistema | Cupom aplicado | Passo 9 | CU-16 | Cupom, AtribuicaoInfluenciador | CheckoutService |
| **8d** | Exibir Erro de Cupom | Sistema | Cupom inválido/expirado | Passo 8a (retry) ou Passo 9 | CU-16 | - | SPA Principal |
| **9** | Criar Pedido | Sistema | - | Passo 10 | CU-01 | Pedido, ItemPedido | CheckoutService |
| **10** | Calcular Total com Desconto | Sistema | Aplica desconto se cupom válido | Passo 11 | CU-01, CU-16 | Pedido, Cupom | CheckoutService |
| **11** | Escolher Método de Pagamento | Cliente | Cliente seleciona PIX ou Cartão | Passo 12 | CU-01 | - | SPA Principal |
| **12** | Iniciar Pagamento | Sistema | - | **Decisão:** Método escolhido? | CU-01 | Pagamento | PaymentOrchestrator |
| **13** | Processar Pagamento PIX | Sistema | **Se PIX:** Gera QR Code dinâmico | Passo 14 | CU-01 | Pagamento | PaymentOrchestrator, Gateway de Pagamento |
| **13a** | Processar Pagamento Cartão | Sistema | **Se Cartão:** Autoriza transação | Passo 14 | CU-01 | Pagamento | PaymentOrchestrator, Gateway de Pagamento |
| **14** | Aguardar Confirmação | Sistema | Monitora via webhook | **Decisão:** Pagamento confirmado? | CU-01 | Pagamento | PaymentOrchestrator, Message Bus |
| **15** | Confirmar Pagamento | Gateway → Sistema | Webhook recebido | Passo 16 | CU-01 | Pagamento | Gateway de Pagamento, PaymentOrchestrator |
| **16** | Atualizar Status do Pedido | Sistema | Marca como "PAGO" | Passo 17 | CU-01 | Pedido, Pagamento | OrderLifecycleManager |
| **17** | Reservar Ingressos | Sistema | Bloqueia estoque | Passo 18 | CU-01 | Lote | CheckoutService, OrderLifecycleManager |
| **18** | Gerar Ingressos e QR Codes | Sistema | **Paralelo:** Cria ingressos e QR assinados | Passo 19 | CU-01 | Ingresso, QrCode | TicketingService, QRSecurityService |
| **19** | Atribuir Ingressos à Carteira | Sistema | Adiciona à carteira do cliente | Passo 20 | CU-01 | Ingresso, Carteira | TicketingService |
| **20** | Registrar Atribuição de Cupom | Sistema | **Se cupom aplicado:** Registra uso | Passo 21 | CU-16 | AtribuicaoInfluenciador | CheckoutService |
| **21** | Calcular Cashback Produtor | Sistema | **Paralelo:** Calcula crédito futuro | Passo 22 | RB02 | CashbackProdutor | CashbackService |
| **22** | Enviar Notificações | Sistema | **Paralelo:** E-mail e WhatsApp | Passo 23 | CU-01 | Notificacao | NotificationService, Message Bus |
| **23** | Exibir Confirmação | Sistema → Cliente | Mostra confirmação na tela | **FIM** | CU-01 | - | SPA Principal |
| **24** | **FIM** | - | Processo concluído | - | CU-01 | - | - |

**Autor:** <a href="https://github.com/gabriel-lima258">Gabriel Lima</a>.

</details>

A figura 2 apresenta o diagrama de atividades do fluxo de compra de ingressos.

<div align="center">
    <b>Figura 2:</b> Diagrama de Atividade — Comprar Ingresso
    <br>
    <img src="assets/Modelagem/Dinamica/Atividades1.pdf" width="1000">
    <br>
    <b>Autor:</b> <a href="https://github.com/gabriel-lima258">Gabriel Lima</a>.
    <br>
</div>

<p><strong>Observação:</strong> O diagrama será desenvolvido seguindo a estrutura descrita na Tabela 1, modelando o fluxo completo desde a seleção do evento até a confirmação da compra e emissão dos ingressos digitais.</p>

---

## Realizar Check-in de Ingresso

Este diagrama representa o fluxo de validação de ingressos durante o evento, baseado no **CU-02 (Realizar Check-in de Ingresso)**. O processo envolve o **PWA Check-in**, o **CheckinValidator**, **QRSecurityService** e suporte para modo offline com sincronização posterior.

Para complementar a representação visual do fluxo de check-in, a Tabela 2 a seguir detalha cada uma das principais ações, decisões e estados presentes no diagrama correspondente, indicando a ordem de execução completa do processo.

<details>
  <summary><strong>Tabela 2: Fluxo Completo de Check-in (Início ao Fim)</strong></summary>

**Tabela 2: Fluxo Completo de Check-in (Início ao Fim)**

| # | Atividade | Responsável | Condição/Decisão | Próximo Passo | Caso de Uso | Classes Envolvidas | Componentes |
|---|---|---|---|---|---|---|---|
| **1** | **INÍCIO** | - | Operador inicia processo | Passo 2 | CU-02 | - | PWA Check-in |
| **2** | Acessar PWA Check-in | Operador | Operador abre aplicativo | Passo 3 | CU-02 | Usuario (Role: CHECKIN) | PWA Check-in |
| **3** | Autenticar Operador | Sistema | Valida credenciais e permissões | Passo 4 | CU-02 | Usuario | AuthService, Gateway Service |
| **4** | Verificar Conectividade Inicial | Sistema | **Decisão:** Está online? | Se não: Passo 4a<br>Se sim: Passo 5 | CU-02 | - | PWA Check-in |
| **4a** | Sincronizar Dados Offline | Sistema | Baixa dados para modo offline | Passo 5 | CU-02 | Ingresso | CheckinOfflineSync |
| **5** | Preparar para Escaneamento | Operador | Sistema pronto para receber QR | Passo 6 | CU-02 | - | PWA Check-in |
| **6** | Apresentar QR Code | Cliente | Cliente apresenta ingresso | Passo 7 | CU-02 | Ingresso, QrCode | Cliente |
| **7** | Escanear QR Code | Operador | Câmera lê código QR | Passo 8 | CU-02 | QrCode | PWA Check-in |
| **8** | Verificar Conectividade | Sistema | **Decisão:** Está online agora? | Se online: Passo 9<br>Se offline: Passo 10 | CU-02 | - | PWA Check-in |
| **9** | Validar Assinatura QR (Online) | Sistema | Verifica assinatura digital | Passo 11 | CU-02 | QrCode | QRSecurityService, CheckinValidator |
| **10** | Validar Assinatura QR (Offline) | Sistema | Verifica contra base local | Passo 11 | CU-02 | QrCode | QRSecurityService, CheckinOfflineSync |
| **11** | **Decisão:** Assinatura Válida? | Sistema | QR assinado corretamente? | Se válido: Passo 12<br>Se inválido: Passo 20 | CU-02 | QrCode | QRSecurityService |
| **12** | Buscar Ingresso no Banco | Sistema | **Decisão:** Modo online ou offline? | Se online: Passo 12a<br>Se offline: Passo 12b | CU-02 | Ingresso | CheckinValidator, Ingresso Repository |
| **12a** | Buscar no Banco (Online) | Sistema | Busca em tempo real | Passo 13 | CU-02 | Ingresso | CheckinValidator, Ingresso Repository |
| **12b** | Buscar na Base Local (Offline) | Sistema | Busca em dados sincronizados | Passo 13 | CU-02 | Ingresso | CheckinOfflineSync |
| **13** | Verificar Status do Ingresso | Sistema | **Decisão:** Já foi utilizado? | Se não utilizado: Passo 14<br>Se utilizado: Passo 19 | CU-02 | Ingresso | CheckinValidator |
| **14** | Verificar Expiração | Sistema | **Decisão:** QR ainda válido? | Se válido: Passo 15<br>Se expirado: Passo 21 | CU-02 | QrCode | CheckinValidator |
| **15** | Registrar Check-in | Sistema | Marca como validado | **Decisão:** Modo? | CU-02 | Ingresso, CheckinRegistro | CheckinValidator |
| **16** | Salvar Registro Localmente | Sistema | **Se offline:** Armazena localmente | Passo 17 | CU-02 | CheckinRegistro | CheckinOfflineSync |
| **17** | Enviar Registro ao Backend | Sistema | **Se online:** Envia imediatamente | Passo 18 | CU-02 | CheckinRegistro | CheckinValidator |
| **18** | Exibir Resultado de Sucesso | Sistema → Operador | "Check-in realizado com sucesso" | **FIM** | CU-02 | - | PWA Check-in |
| **19** | Registrar Check-in Duplicado | Sistema | Ingresso já utilizado | Passo 22 | CU-02 | CheckinRegistro | CheckinValidator |
| **20** | Registrar QR Inválido | Sistema | Assinatura inválida ou adulterada | Passo 22 | CU-02 | CheckinRegistro | CheckinValidator |
| **21** | Registrar QR Expirado | Sistema | QR Code expirado | Passo 22 | CU-02 | CheckinRegistro | CheckinValidator |
| **22** | Exibir Mensagem de Erro | Sistema → Operador | Motivo da rejeição | **FIM** | CU-02 | - | PWA Check-in |
| **23** | Sincronizar Dados Pendentes | Sistema | **Ao voltar online:** Sincroniza registros | **FIM** | CU-02 | CheckinRegistro | CheckinOfflineSync |
| **24** | **FIM** | - | Processo concluído | - | CU-02 | - | - |

**Autor:** <a href="https://github.com/gabriel-lima258">Gabriel Lima</a>.

</details>

A figura 3 apresenta o diagrama de atividades do fluxo de check-in.

<div align="center">
    <b>Figura 3:</b> Diagrama de Atividade — Realizar Check-in de Ingresso
    <br>
    <img src="assets/Modelagem/Dinamica/Atividades2.pdf" width="1000">
    <br>
    <b>Autor:</b> <a href="https://github.com/gabriel-lima258">Gabriel Lima</a>.
    <br>
</div>

<p><strong>Observação:</strong> O diagrama será desenvolvido seguindo a estrutura descrita na Tabela 2, incluindo os fluxos paralelos de validação online e offline, bem como o processo de sincronização posterior.</p>

---

## Criar e Publicar Evento (Admin)

Este diagrama representa o fluxo administrativo de criação e publicação de eventos, baseado nos casos de uso **CU-11 (Criar Evento - Admin)** e **CU-12 (Publicar Evento - Admin)**. O processo envolve o **Painel Admin**, **EventAdminService** e integração com **Cache** para invalidação após publicação.

Para complementar a representação visual do fluxo administrativo, a Tabela 3 a seguir detalha cada uma das principais ações, decisões e estados presentes no diagrama correspondente, indicando a ordem de execução completa do processo.

<details>
  <summary><strong>Tabela 3: Fluxo Completo de Criação e Publicação de Evento (Início ao Fim)</strong></summary>

**Tabela 3: Fluxo Completo de Criação e Publicação de Evento (Início ao Fim)**

| # | Atividade | Responsável | Condição/Decisão | Próximo Passo | Caso de Uso | Classes Envolvidas | Componentes |
|---|---|---|---|---|---|---|---|
| **1** | **INÍCIO** | - | Admin inicia processo | Passo 2 | CU-17 | - | Painel Admin |
| **2** | Acessar Painel Admin | Administrador | Admin acessa painel | Passo 3 | CU-17 | Administrador | Painel Admin |
| **3** | Autenticar Admin | Sistema | Valida credenciais e permissões ADMIN | Passo 4 | CU-17 | Usuario, Administrador | AuthService, Gateway Service |
| **4** | Navegar para Gestão de Eventos | Admin | Seleciona seção de eventos | Passo 5 | CU-11 | - | Painel Admin |
| **5** | Criar Novo Evento | Admin | Clica em "Criar Novo Evento" | Passo 6 | CU-11 | Evento | Painel Admin |
| **6** | Preencher Dados Básicos | Admin | Insere nome, descrição, datas início/fim | Passo 7 | CU-11 | Evento | EventAdminService |
| **7** | Definir Localização | Admin | Insere endereço completo, cidade, UF | Passo 8 | CU-11 | Evento, Localizacao | EventAdminService |
| **8** | Selecionar Categorias | Admin | **Obrigatório:** Escolhe pelo menos 1 categoria | Passo 9 | CU-11 | Evento, Categoria | EventAdminService |
| **9** | Fazer Upload de Banner | Admin | Upload de imagem do evento | Passo 10 | CU-11 | - | GestorAssetsS3 |
| **10** | Configurar Transferência | Admin | **Opcional:** Define política de transferência | Passo 11 | CU-11 | Evento, TransferPolicy | EventAdminService |
| **11** | Validar Dados do Evento | Sistema | Verifica dados obrigatórios preenchidos | **Decisão:** Dados válidos? | CU-11 | Evento | EventAdminService |
| **12** | Salvar Evento como Rascunho | Sistema | Cria evento com status "RASCUNHO" | Passo 13 | CU-11 | Evento | EventAdminService, Evento Repository |
| **13** | Verificar Necessidade de Lotes | Admin → Sistema | **Decisão:** Admin deseja criar lotes agora? | Se sim: Passo 14<br>Se não: Passo 22 | CU-15 | Lote | EventAdminService |
| **14** | Criar Novo Lote | Admin | Inicia criação de lote | Passo 15 | CU-15 | Lote | EventAdminService, Lote Repository |
| **15** | Definir Preço e Quantidade | Admin | Insere preço unitário e quantidade total | Passo 16 | CU-15 | Lote | EventAdminService |
| **16** | Configurar Janela de Venda | Admin | Define data/hora início e fim da venda | Passo 17 | CU-15 | Lote | EventAdminService |
| **17** | Definir Tipo de Ingresso | Admin | Escolhe tipo (inteira, meia, VIP, etc.) | Passo 18 | CU-15 | Lote, TipoLote | EventAdminService |
| **18** | Validar Dados do Lote | Sistema | Verifica janela dentro do período do evento | **Decisão:** Lote válido? | CU-15 | Lote | EventAdminService |
| **19** | Salvar Lote | Sistema | Persiste lote vinculado ao evento | Passo 20 | CU-15 | Lote | EventAdminService |
| **20** | Verificar Mais Lotes | Admin → Sistema | **Decisão:** Admin deseja criar mais lotes? | Se sim: Passo 14<br>Se não: Passo 21 | CU-15 | - | EventAdminService |
| **21** | Vincular Produtor ao Evento | Admin | Associa produtor responsável | Passo 22 | CU-13 | Evento, Produtor | EventAdminService |
| **22** | Decidir Publicação | Admin | **Decisão:** Admin deseja publicar agora? | Se sim: Passo 23<br>Se não: **FIM** (rascunho salvo) | CU-12 | Evento | Painel Admin |
| **23** | Verificar Pré-condições | Sistema | Valida condições para publicação | **Decisão:** Pré-condições atendidas? | CU-12 | Evento, Lote | EventAdminService |
| **24** | Pré-condição: Pelo menos 1 lote válido | Sistema | Verifica existência de lotes | Passo 25 | CU-12 | Lote | EventAdminService |
| **25** | Pré-condição: Categoria atribuída | Sistema | Verifica categoria obrigatória | Passo 26 | CU-12 | Evento, Categoria | EventAdminService |
| **26** | Pré-condição: Dados obrigatórios | Sistema | Verifica dados completos | Passo 27 | CU-12 | Evento | EventAdminService |
| **27** | Exibir Erros de Pré-condição | Sistema → Admin | Lista pendências que impedem publicação | Passo 22 (correção) | CU-12 | - | Painel Admin |
| **28** | Publicar Evento | Admin | Confirma publicação | Passo 29 | CU-12 | Evento | EventAdminService |
| **29** | Atualizar Status para PUBLICADO | Sistema | Altera status do evento | Passo 30 | CU-12 | Evento | EventAdminService |
| **30** | Atualizar Data de Publicação | Sistema | Registra timestamp de publicação | Passo 31 | CU-12 | Evento | EventAdminService |
| **31** | Invalidar Cache | Sistema | **Paralelo:** Limpa cache de eventos e busca | Passo 32 | CU-12 | - | Cache Service (Redis) |
| **32** | Enviar Notificações | Sistema | **Paralelo:** Notifica produtor(es) vinculado(s) | Passo 33 | CU-12 | Notificacao | NotificationService, Message Bus |
| **33** | Registrar Auditoria | Sistema | **Paralelo:** Registra log de ação administrativa | Passo 34 | CU-12 | Auditoria | AuditLogger |
| **34** | Disponibilizar para Venda | Sistema | Evento fica visível no catálogo público | Passo 35 | CU-12 | Evento | EventSearchService |
| **35** | Exibir Confirmação | Sistema → Admin | Mostra confirmação de publicação | **FIM** | CU-12 | - | Painel Admin |
| **36** | **FIM** | - | Processo concluído | - | CU-12 | - | - |

**Autor:** <a href="https://github.com/gabriel-lima258">Gabriel Lima</a>.

</details>

A figura 4 apresenta o diagrama de atividades do fluxo de criação e publicação de evento.

<div align="center">
    <b>Figura 4:</b> Diagrama de Atividade — Criar e Publicar Evento (Admin)
    <br>
    <img src="assets/Modelagem/Dinamica/Atividades3.pdf" width="1000">
    <br>
    <b>Autor:</b> <a href="https://github.com/gabriel-lima258">Gabriel Lima</a>.
    <br>
</div>

<p><strong>Observação:</strong> O diagrama será desenvolvido seguindo a estrutura descrita na Tabela 3 e será disponibilizado após a elaboração na ferramenta Draw.io.</p>

---

## Conclusão

A conclusão do desenvolvimento desses diagramas de atividade para a plataforma **Ingressou** oferece uma representação clara e estruturada dos principais fluxos de trabalho do sistema, possibilitando uma compreensão aprofundada das interações entre usuários (clientes, operadores de check-in, administradores) e os componentes do sistema.

Os três diagramas elaborados cobrem os processos críticos do MVP:

1. **Comprar Ingresso**: Demonstra o fluxo completo desde a descoberta do evento até a emissão do ingresso digital, incluindo integração com gateway de pagamento, aplicação de cupons e notificações;
2. **Realizar Check-in**: Evidencia o processo de validação de ingressos, com suporte a modo offline e sincronização posterior, garantindo funcionamento mesmo em locais com conectividade limitada;
3. **Criar e Publicar Evento (Admin)**: Mostra o fluxo administrativo completo, desde a criação do evento e lotes até a publicação pública, incluindo validações, cache e notificações.

Esses diagramas servem como base para implementação, documentação técnica e validação dos requisitos funcionais identificados nos casos de uso (CU-01, CU-02, CU-11, CU-12) e nos documentos de análise (5W2H, Diagrama de Classes, Diagrama de Componentes).

---

## Bibliografia

<a name="ref1"></a>
[1] APOSTILA UML. Unified Modeling Language – Linguagem de Modelagem Unificada em Português. Seção sobre diagrama de atividades. Disponibilizada pela professora. Acesso em: 30 out. 2025.

<a name="ref2"></a>
[2] IBM. Diagramas de Atividades. Atualizado pela última vez: 02 mar. 2021. Disponível em: https://www.ibm.com/docs/pt-br/rational-soft-arch/9.7.0?topic=diagrams-activity. Acesso em: 30 out. 2025.

<a name="ref3"></a>
[3] LUCIDCHART. O que é diagrama de atividades UML? Disponível em: https://www.lucidchart.com/pages/pt/o-que-e-diagrama-de-atividades-uml. Acesso em: 30 out. 2025.

<a name="ref4"></a>
[4] LIMA, Gabriel. 5W2H — Ingressou. Outubro de 2025. Disponível em: [Base/ArtefatoGeneralista/5W2H.md](/Base/ArtefatoGeneralista/5W2H.md).

<a name="ref5"></a>
[5] UML DIAGRAMS. UML Activity Diagram Controls. Disponível em: https://www.uml-diagrams.org/activity-diagrams-controls.html. Acesso em: 30 out. 2025.

<a name="ref6"></a>
[6] LIMA, Gabriel. Diagrama de Classes — Projeto Ingressou (MVP). Outubro de 2025. Disponível em: [Modelagem/ModelagemEstatica/DiagramaClasses.md](/Modelagem/ModelagemEstatica/DiagramaClasses.md).

<a name="ref7"></a>
[7] LIMA, Gabriel. Diagrama de Componentes — Projeto Ingressou. Outubro de 2025. Disponível em: [Modelagem/ModelagemEstatica/DiagramaComponentes.md](/Modelagem/ModelagemEstatica/DiagramaComponentes.md).

<a name="ref8"></a>
[8] LIMA, Gabriel. Diagrama de Casos de Uso — Projeto Ingressou. Outubro de 2025. Disponível em: [Modelagem/ModelagemOrganizacional/DiagramaCasosUso.md](/Modelagem/ModelagemOrganizacional/DiagramaCasosUso.md).

---

## Histórico de versão

| Versão | Alteração | Responsável | Data |
|---|---|---|---|
| 1.0 | Criação inicial do documento com três diagramas de atividades principais (Comprar Ingresso, Check-in, Criar/Publicar Evento) baseados nos documentos 5W2H, Diagrama de Classes, Diagrama de Componentes e Diagrama de Casos de Uso | Gabriel Lima | 30/10/2025 |
| 1.1 | Refatoração das tabelas de fluxo com estrutura completa do início ao fim, incluindo numeração sequencial, condições/decisões, responsáveis e próximos passos para cada módulo | Gabriel Lima | 30/10/2025 |
