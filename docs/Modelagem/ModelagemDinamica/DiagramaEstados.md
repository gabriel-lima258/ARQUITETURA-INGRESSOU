# Diagrama de Estados

> **Versão:** 1.0  
> **Data:** Outubro de 2025  
> **Autor:** Gabriel Lima  
> **Projeto:** Ingressou — Plataforma Web de Venda e Gestão de Ingressos  

---

## Sumário

- [Introdução](#introdução)
- [Objetivos](#objetivos)
- [Metodologia](#metodologia)
- [Sobre o Diagrama de Estados](#sobre-o-diagrama-de-estados)
- [Ciclo de Vida do Evento](#ciclo-de-vida-do-evento)
- [Ciclo de Vida do Pedido](#ciclo-de-vida-do-pedido)
- [Ciclo de Vida da Transferência de Ingresso](#ciclo-de-vida-da-transferência-de-ingresso)
- [Conclusão](#conclusão)
- [Bibliografia](#bibliografia)
- [Histórico de versão](#histórico-de-versão)

---

## Introdução

O **diagrama de estados**, também conhecido como **diagrama de máquina de estados**, segundo [fonte: O que é um diagrama de máquina de estados?](https://www.lucidchart.com/pages/pt/o-que-e-diagrama-de-maquina-de-estados-uml) [1](#ref1), é um tipo de diagrama comportamental da UML (Unified Modeling Language) utilizado para representar o comportamento dinâmico de um objeto ao ilustrar os estados que ele pode assumir ao longo do tempo e as transições causadas por eventos específicos. Com isso, com base no artigo [State Machine Diagrams](https://www.uml-diagrams.org/state-machine-diagrams.html) [3](#ref3), esse tipo de modelagem é especialmente útil para descrever sistemas reativos e orientados a eventos em que as ações dependem das entradas recebidas e permite visualizar como o objeto responde a diferentes estímulos durante sua existência.

No contexto do projeto **Ingressou**, serão elaborados diagramas de estados para representar o ciclo de vida das principais entidades do sistema: **Evento**, **Pedido** e **Transferência de Ingresso**. Essas entidades possuem comportamentos dinâmicos complexos que influenciam diretamente o funcionamento da plataforma de venda e gestão de ingressos.

---

## Objetivos

O objetivo deste documento é representar, por meio de diagramas de estados, os comportamentos dinâmicos das principais entidades do sistema **Ingressou**. De forma mais específica, busca-se:

- Representar os diferentes estados que as entidades **Evento**, **Pedido** e **Transferência** podem assumir durante sua execução;
- Demonstrar as transições de estado com base em eventos, ações ou interações do usuário (Admin, Cliente, Sistema);
- Auxiliar na compreensão dos fluxos internos e das mudanças comportamentais dos componentes da plataforma;
- Apoiar a modelagem de sistemas reativos e orientados a eventos com uma representação visual clara e estruturada;
- Documentar as regras de negócio relacionadas às mudanças de estado, conforme definidas nos requisitos funcionais e regras de negócio.

---

## Metodologia

A elaboração dos diagramas de estados será realizada com base na integração de artefatos previamente desenvolvidos no projeto **Ingressou**, com o objetivo de representar visualmente os comportamentos dinâmicos das principais entidades do sistema. Assim, serão desenvolvidos **três diagramas principais**:

- **Ciclo de Vida do Evento**: Representa os estados desde a criação pelo Admin até o encerramento/cancelamento, incluindo publicação e lotes;
- **Ciclo de Vida do Pedido**: Modela o fluxo completo desde a criação do pedido até a conclusão com pagamento ou cancelamento;
- **Ciclo de Vida da Transferência de Ingresso**: Demonstra o processo de transferência entre usuários, incluindo aceite, pagamento de taxa e reemissão de QR Code.

Para a construção dos diagramas, serão seguidas as etapas abaixo:

1. Inicialmente, serão analisados os seguintes artefatos como base para definição dos estados e transições:
   - [Requisitos Funcionais e Não Funcionais elicitados](/Base/ArtefatoGeneralista/RequisitosElicitados.md);
   - [Diagrama de Classes](/Modelagem/ModelagemEstatica/DiagramaClasses.md);
   - [Diagrama de Componentes](/Modelagem/ModelagemEstatica/DiagramaComponentes.md);
   - [Diagrama de Casos de Uso](/Modelagem/ModelagemOrganizacional/DiagramaCasosUso.md);

2. Os diagramas serão desenvolvidos utilizando a ferramenta [Draw.io](https://www.drawio.com/blog/uml-component-diagrams), seguindo notação UML 2.0;

---

## Sobre o Diagrama de Estados

Os Diagramas de Máquina de Estados a seguir ilustram o ciclo de vida e o comportamento dinâmico das entidades **Evento**, **Pedido** e **Transferência** dentro da plataforma **Ingressou**. Sendo assim, com base em [State Machine Diagrams](https://www.uml-diagrams.org/state-machine-diagrams.html) [3](#ref3) e [UML 2 Tutorial - State Machine Diagram](https://sparxsystems.com/resources/tutorials/uml2/state-diagram.html) [2](#ref2), eles mapeiam os diversos estados possíveis para essas entidades e as transições (setas) que ocorrem entre eles. Essas mudanças de estado são acionadas por eventos específicos (ações do sistema, usuário ou tempo) e podem depender de condições de guarda (`[]`), frequentemente executando ações (`/`) durante a transição.

Para representar detalhadamente os fluxos, foram utilizados elementos como estados compostos (agrupando subestados), ações de entrada/saída/do (entry/exit/do) e condições de guarda, o que permite uma visualização clara das regras que governam o comportamento dessas entidades ao longo do tempo.

Para melhor compreensão dos diagramas, a figura 1 mostra a legenda:

<div align="center">
    <b>Figura 1:</b> Legenda do Diagrama de Estados
    <br>
    <img src="assets/Legendas/LegendaDiagramaEstados.drawio.png" width="500">
    <br>
    <b>Autor:</b> <a href="https://github.com/gabriel-lima258">Gabriel Lima</a>.
    <br>
</div>

**Observação Importante:** Com o intuito de elaborar melhor os diagramas, foram elaboradas tabelas contendo os estados com suas descrições e relação com os requisitos elicitados e com os componentes do diagrama de componentes **(Tabelas 1, 3 e 5)**. Da mesma forma, foram criadas tabelas que mostram as transições entre os estados **(Tabelas 2, 4 e 6)**.

---

## Ciclo de Vida do Evento

O Diagrama de Máquina de Estados para a entidade **Evento** ilustra as diversas fases pelas quais um evento pode passar ao longo de seu ciclo de vida na plataforma **Ingressou**. Conforme definido no **Diagrama de Classes**, o evento possui os seguintes estados: `RASCUNHO`, `AGUARDANDO_APROVACAO`, `PUBLICADO`, `ENCERRADO` e `CANCELADO`. Para detalhar e clarificar cada uma dessas fases, a Tabela 1 a seguir apresenta e descreve os diferentes estados definidos.

<details>
  <summary><strong>Tabela 1: Estados do Ciclo de Vida do Evento</strong></summary>

**Tabela 1: Estados do Ciclo de Vida do Evento**

| # | Estado | Descrição | Relação com Requisitos | Relação com Classes | Relação com Componentes |
|---|---|---|---|---|---|
| 1 | ⚫ (Estado Inicial) | Ponto de entrada quando um Admin inicia a criação de um novo evento. | CU-11 | Evento | EventAdminService, Painel Admin |
| 2 | `RASCUNHO` | Evento criado pelo Admin, mas ainda não publicado. Permite edição completa. | RF15, CU-11 | Evento | EventAdminService |
| 3 | `AGUARDANDO_APROVACAO` | Evento submetido para publicação, aguardando validação de pré-condições. | RF17, CU-12 | Evento | EventAdminService |
| 4 | `PUBLICADO` | **(Estado Composto)** Evento visível publicamente com vendas ativas. Contém subestados relacionados à disponibilidade de lotes. | RF17, RF18, CU-12 | Evento, Lote | EventAdminService, EventSearchService |
| 5 | `-> Com Lotes Disponíveis` | Subestado de PUBLICADO: Há lotes ativos e com estoque disponível. | RF21, RF22 | Lote | EventSearchService, CheckoutService |
| 6 | `-> Com Lotes Esgotados` | Subestado de PUBLICADO: Todos os lotes estão esgotados ou encerrados. | RF22 | Lote | EventSearchService |
| 7 | `ENCERRADO` | Evento concluído naturalmente após a data de fim. Não permite mais vendas. | RF15 | Evento | EventAdminService |
| 8 | `CANCELADO` | Evento cancelado pelo Admin ou automaticamente. Não permite vendas. | RF15 | Evento | EventAdminService |
| 9 | ⊚ (Estado Final) | Ciclo de vida do evento terminou (arquivado ou removido). | - | Evento | EventAdminService |

**Autor:** <a href="https://github.com/gabriel-lima258">Gabriel Lima</a>.

</details>

Para complementar a compreensão dos estados de um **Evento**, a Tabela 2 se aprofunda nas transições que governam as mudanças entre esses diferentes estágios, conforme representado no Diagrama de Máquina de Estados. Esta tabela visa especificar os eventos gatilho (triggers), as condições de guarda (guards) que devem ser satisfeitas e as ações (actions) que são executadas durante cada mudança de estado.

<details>
  <summary><strong>Tabela 2: Transições do Ciclo de Vida do Evento</strong></summary>

**Tabela 2: Transições do Ciclo de Vida do Evento**

| Elementos entre a transição | Rótulo da transição | Relação com Requisitos | Relação com Componentes (Evento / Ação) |
|---|---|---|---|
| ⚫ -> `RASCUNHO` | `adminCriaEvento / criarEventoBD(), definirStatusRASCUNHO()` | RF15, CU-11 | Painel Admin / EventAdminService via Evento Repository |
| `RASCUNHO` -> `AGUARDANDO_APROVACAO` | `adminTentaPublicar [semLotesValidados OU semCategoria] / validarPreCondicoes()` | RF17, CU-12 | Painel Admin / EventAdminService |
| `AGUARDANDO_APROVACAO` -> `PUBLICADO` | `preCondicoesAtendidas [lotesValidos>=1 AND categoria!=null] / publicarEvento(), invalidarCache(), notificarProdutores()` | RF17, CU-12 | EventAdminService / EventAdminService, Cache Service, NotificationService |
| `AGUARDANDO_APROVACAO` -> `RASCUNHO` | `preCondicoesNaoAtendidas / retornarParaRascunho()` | RF17 | EventAdminService / EventAdminService |
| `PUBLICADO` -> `Com Lotes Disponíveis` | *(implícito na publicação)* `lotesAtivosComEstoque() / atualizarDisponibilidade()` | RF21, RF22 | EventAdminService / EventSearchService |
| `Com Lotes Disponíveis` -> `Com Lotes Esgotados` | `todosLotesEsgotados [quantidadeVendida>=quantidadeTotal OR tempoExpirado] / marcarLotesEncerrados()` | RF22 | OrderLifecycleManager / EventAdminService |
| `Com Lotes Esgotados` -> `Com Lotes Disponíveis` | `novoLoteCriado [loteAtivo AND estoque>0] / atualizarDisponibilidade()` | RF21 | EventAdminService / EventSearchService |
| `PUBLICADO` -> `ENCERRADO` | `when(dataAtual >= dataFimEvento) / encerrarEvento(), calcularCashbackProdutor()` | RF15, RB02 | Timer / EventAdminService, CashbackService |
| `PUBLICADO` -> `CANCELADO` | `adminCancelaEvento / cancelarEvento(motivo), estornarPagamentos(), notificarClientes()` | RF15 | Painel Admin / EventAdminService |
| `RASCUNHO` -> `CANCELADO` | `adminCancelaRascunho / removerEvento()` | RF15 | Painel Admin / EventAdminService |
| `ENCERRADO` -> ⊚ (Final) | `arquivamentoConcluido [after(1 ano)] / moverParaHistorico()` | - | Timer / EventAdminService |
| `CANCELADO` -> ⊚ (Final) | `arquivamentoConcluido [after(6 meses)] / moverParaHistorico()` | - | Timer / EventAdminService |

**Autor:** <a href="https://github.com/gabriel-lima258">Gabriel Lima</a>.

</details>

A figura 2 apresenta o diagrama de estados do ciclo de vida do Evento:

<div align="center">
    <b>Figura 2:</b> Diagrama de Estados — Ciclo de Vida do Evento
    <br>
    <img src="assets/Modelagem/Dinamica/Estado1.pdf" width="1000">
    <br>
    <b>Autor:</b> <a href="https://github.com/gabriel-lima258">Gabriel Lima</a>.
    <br>
</div>

<p><strong>Observação:</strong> O diagrama será desenvolvido seguindo a estrutura descrita nas Tabelas 1 e 2, modelando o ciclo completo desde a criação do evento como rascunho até seu encerramento ou cancelamento.</p>

---

## Ciclo de Vida do Pedido

O Diagrama de Máquina de Estados para a entidade **Pedido** ilustra o fluxo completo desde a criação do pedido pelo cliente até sua conclusão com pagamento confirmado ou cancelamento. Conforme definido no **Diagrama de Classes**, o pedido possui os seguintes estados: `CRIADO`, `AGUARDANDO_PAGAMENTO`, `PAGO`, `CANCELADO` e `EXPIRADO`. Para detalhar e clarificar cada uma dessas fases, a Tabela 3 a seguir apresenta e descreve os diferentes estados definidos.

<details>
  <summary><strong>Tabela 3: Estados do Ciclo de Vida do Pedido</strong></summary>

**Tabela 3: Estados do Ciclo de Vida do Pedido**

| # | Estado | Descrição | Relação com Requisitos | Relação com Classes | Relação com Componentes |
|---|---|---|---|---|---|
| 1 | ⚫ (Estado Inicial) | Ponto de entrada quando cliente seleciona ingressos e inicia checkout. | CU-01 | Pedido | SPA Principal, CheckoutService |
| 2 | `CRIADO` | Pedido criado com itens selecionados, mas ainda não finalizado. Permite edição de itens e aplicação de cupom. | RF26, CU-01 | Pedido, ItemPedido | CheckoutService |
| 3 | `AGUARDANDO_PAGAMENTO` | **(Estado Composto)** Pedido finalizado, aguardando confirmação de pagamento. Contém subestados relacionados ao método de pagamento. | RF27, RF28, CU-01 | Pedido, Pagamento | PaymentOrchestrator, Gateway de Pagamento |
| 4 | `-> PIX Pendente` | Subestado de AGUARDANDO_PAGAMENTO: QR Code PIX gerado, aguardando pagamento (reserva de 10 min). | RF27, RB04 | Pagamento | PaymentOrchestrator, Gateway de Pagamento |
| 5 | `-> Cartão Autorizado` | Subestado de AGUARDANDO_PAGAMENTO: Transação cartão autorizada, aguardando confirmação via webhook. | RF28 | Pagamento | PaymentOrchestrator, Gateway de Pagamento |
| 6 | `PAGO` | Pagamento confirmado, ingressos emitidos e atribuídos à carteira do cliente. | RF29, CU-01 | Pedido, Pagamento, Ingresso | OrderLifecycleManager, TicketingService |
| 7 | `CANCELADO` | Pedido cancelado pelo cliente ou sistema (falha de pagamento, estoque insuficiente). | RF30, CU-01 | Pedido, Pagamento | OrderLifecycleManager |
| 8 | `EXPIRADO` | Reserva de pagamento PIX expirou (10 minutos) sem confirmação. | RF27, RB04 | Pedido | PaymentOrchestrator, OrderLifecycleManager |
| 9 | ⊚ (Estado Final) | Ciclo de vida do pedido terminou (pago, cancelado ou expirado). | - | Pedido | - |

**Autor:** <a href="https://github.com/gabriel-lima258">Gabriel Lima</a>.

</details>

Para complementar a compreensão dos estados de um **Pedido**, a Tabela 4 se aprofunda nas transições que governam as mudanças entre esses diferentes estágios.

<details>
  <summary><strong>Tabela 4: Transições do Ciclo de Vida do Pedido</strong></summary>

**Tabela 4: Transições do Ciclo de Vida do Pedido**

| Elementos entre a transição | Rótulo da transição | Relação com Requisitos | Relação com Componentes (Evento / Ação) |
|---|---|---|---|
| ⚫ -> `CRIADO` | `clienteAdicionaItens / criarPedidoBD(), reservarEstoqueTemporario()` | RF26, CU-01 | SPA Principal / CheckoutService |
| `CRIADO` -> `AGUARDANDO_PAGAMENTO` | `clienteFinalizaPedido [metodoPagamento= PIX OU Cartão] / iniciarPagamento(), criarPagamentoBD()` | RF26, RF27, RF28, CU-01 | CheckoutService / PaymentOrchestrator |
| `AGUARDANDO_PAGAMENTO` -> `PIX Pendente` | `metodoPagamento=PIX / gerarQRCodeDinamico(), definirReservaExpiraEm(10min)` | RF27, RB04 | PaymentOrchestrator / Gateway de Pagamento |
| `AGUARDANDO_PAGAMENTO` -> `Cartão Autorizado` | `metodoPagamento=Cartão AND autorizacaoOK / registrarAutorizacao()` | RF28 | PaymentOrchestrator / Gateway de Pagamento |
| `PIX Pendente` -> `PAGO` | `webhookConfirmaPagamentoPIX / confirmarPagamento(), emitirIngressos()` | RF27, RF29 | Gateway de Pagamento / PaymentOrchestrator, TicketingService |
| `PIX Pendente` -> `EXPIRADO` | `when(reservaExpiraEm < agora) / expirarPedido(), liberarEstoque()` | RF27, RB04 | Timer / OrderLifecycleManager |
| `Cartão Autorizado` -> `PAGO` | `webhookConfirmaPagamentoCartao / confirmarPagamento(), emitirIngressos()` | RF28, RF29 | Gateway de Pagamento / PaymentOrchestrator, TicketingService |
| `Cartão Autorizado` -> `CANCELADO` | `webhookRecusaPagamento / recusarPagamento(), liberarEstoque()` | RF28, RF30 | Gateway de Pagamento / PaymentOrchestrator, OrderLifecycleManager |
| `AGUARDANDO_PAGAMENTO` -> `CANCELADO` | `clienteCancelaPedido OU falhaPagamento / cancelarPedido(), liberarEstoque()` | RF30, CU-01 | Cliente ou PaymentOrchestrator / OrderLifecycleManager |
| `CRIADO` -> `CANCELADO` | `clienteCancela OU timeoutSessao / cancelarPedido(), liberarEstoque()` | RF30 | Cliente ou Sistema / CheckoutService |
| `EXPIRADO` -> ⊚ (Final) | *(implícito após expiração)* | - | OrderLifecycleManager |
| `PAGO` -> ⊚ (Final) | *(implícito após pagamento confirmado)* | - | OrderLifecycleManager |
| `CANCELADO` -> ⊚ (Final) | *(implícito após cancelamento)* | - | OrderLifecycleManager |

**Autor:** <a href="https://github.com/gabriel-lima258">Gabriel Lima</a>.

</details>

A figura 3 apresenta o diagrama de estados do ciclo de vida do Pedido:

<div align="center">
    <b>Figura 3:</b> Diagrama de Estados — Ciclo de Vida do Pedido
    <br>
    <img src="assets/Modelagem/Dinamica/Estado2.pdf" width="1000">
    <br>
    <b>Autor:</b> <a href="https://github.com/gabriel-lima258">Gabriel Lima</a>.
    <br>
</div>

<p><strong>Observação:</strong> O diagrama será desenvolvido seguindo a estrutura descrita nas Tabelas 3 e 4, modelando o fluxo completo desde a criação do pedido até a confirmação do pagamento ou cancelamento.</p>

---

## Ciclo de Vida da Transferência de Ingresso

O Diagrama de Máquina de Estados para a entidade **Transferência** ilustra o processo completo de transferência de ingressos entre usuários, incluindo aceite do destinatário, pagamento de taxa e reemissão de QR Code. Conforme definido no **Diagrama de Classes**, a transferência possui os seguintes estados: `CRIADA`, `AGUARDANDO_ACEITE`, `AGUARDANDO_PAGAMENTO_TAXA`, `CONCLUIDA`, `RECUSADA`, `EXPIRADA` e `CANCELADA`. Para detalhar e clarificar cada uma dessas fases, a Tabela 5 a seguir apresenta e descreve os diferentes estados definidos.

<details>
  <summary><strong>Tabela 5: Estados do Ciclo de Vida da Transferência de Ingresso</strong></summary>

**Tabela 5: Estados do Ciclo de Vida da Transferência de Ingresso**

| # | Estado | Descrição | Relação com Requisitos | Relação com Classes | Relação com Componentes |
|---|---|---|---|---|---|
| 1 | ⚫ (Estado Inicial) | Ponto de entrada quando remetente inicia transferência de ingresso. | CU-14 | Transferencia | TransferService, SPA Principal |
| 2 | `CRIADA` | Solicitação de transferência criada, aguardando envio do convite ao destinatário. | RF40, CU-14 | Transferencia | TransferService |
| 3 | `AGUARDANDO_ACEITE` | **(Estado Composto)** Convite enviado ao destinatário, aguardando aceite dentro da janela de tempo configurável. | RF40, RF41, CU-14 | Transferencia | TransferService, NotificationService |
| 4 | `-> Convite Enviado` | Subestado de AGUARDANDO_ACEITE: Notificação enviada, aguardando acesso do destinatário ao link. | RF40, RF47 | Transferencia | NotificationService |
| 5 | `-> Destinatário Visualizou` | Subestado de AGUARDANDO_ACEITE: Destinatário acessou o link, mas ainda não aceitou. | RF41 | Transferencia | TransferService |
| 6 | `AGUARDANDO_PAGAMENTO_TAXA` | Destinatário aceitou, mas ainda não pagou a taxa de transferência (10% do valor original). | RF45, CU-14 | Transferencia, Pagamento | TransferService, PaymentOrchestrator |
| 7 | `CONCLUIDA` | Taxa paga, ingresso transferido para carteira do destinatário, QR original invalidado e novo QR emitido. | RF42, RF45, CU-14 | Transferencia, Ingresso, QrCode | TransferService, TicketingService, QRSecurityService |
| 8 | `RECUSADA` | Destinatário recusou a transferência dentro da janela de tempo. | RF43, CU-14 | Transferencia | TransferService |
| 9 | `EXPIRADA` | Janela de tempo para aceite expirou sem resposta do destinatário. | RF43, CU-14 | Transferencia | TransferService |
| 10 | `CANCELADA` | Remetente cancelou a transferência antes do aceite ou após falha no pagamento da taxa. | RF43, CU-14 | Transferencia | TransferService |
| 11 | ⊚ (Estado Final) | Ciclo de vida da transferência terminou (concluída, recusada, expirada ou cancelada). | - | Transferencia | - |

**Autor:** <a href="https://github.com/gabriel-lima258">Gabriel Lima</a>.

</details>

Para complementar a compreensão dos estados de uma **Transferência**, a Tabela 6 se aprofunda nas transições que governam as mudanças entre esses diferentes estágios.

<details>
  <summary><strong>Tabela 6: Transições do Ciclo de Vida da Transferência de Ingresso</strong></summary>

**Tabela 6: Transições do Ciclo de Vida da Transferência de Ingresso**

| Elementos entre a transição | Rótulo da transição | Relação com Requisitos | Relação com Componentes (Evento / Ação) |
|---|---|---|---|
| ⚫ -> `CRIADA` | `remetenteIniciaTransferencia [ingressoValido AND eventoPermiteTransferencia] / criarTransferenciaBD(), invalidarQROriginal()` | RF40, RF44, CU-14 | SPA Principal / TransferService |
| `CRIADA` -> `AGUARDANDO_ACEITE` | `conviteEnviado / enviarNotificacaoDestinatario(), definirExpiraEm()` | RF40, RF47 | TransferService / NotificationService |
| `AGUARDANDO_ACEITE` -> `Convite Enviado` | *(implícito na criação)* `/ registrarMomentoEnvio()` | RF40 | NotificationService / TransferService |
| `Convite Enviado` -> `Destinatário Visualizou` | `destinatarioAcessaLink / registrarVisualizacao()` | RF41 | TransferService / TransferService |
| `Destinatário Visualizou` -> `AGUARDANDO_PAGAMENTO_TAXA` | `destinatarioAceita [dentroJanelaTempo] / aceitarTransferencia(), calcularTaxa()` | RF41, RF45 | TransferService / TransferService |
| `AGUARDANDO_ACEITE` -> `RECUSADA` | `destinatarioRecusa [dentroJanelaTempo] / recusarTransferencia(), retornarIngressoRemetente(), notificarRemetente()` | RF43, RF47 | TransferService / TransferService, NotificationService |
| `AGUARDANDO_ACEITE` -> `EXPIRADA` | `when(expiraEm < agora) / expirarTransferencia(), retornarIngressoRemetente()` | RF43 | Timer / TransferService |
| `AGUARDANDO_ACEITE` -> `CANCELADA` | `remetenteCancela / cancelarTransferencia(), retornarIngressoRemetente()` | RF43 | Remetente / TransferService |
| `AGUARDANDO_PAGAMENTO_TAXA` -> `CONCLUIDA` | `taxaPaga [pagamentoConfirmado] / transferirIngresso(), invalidarQROriginal(), gerarNovoQR(), notificarConclusao()` | RF42, RF45, RF47 | PaymentOrchestrator / TransferService, TicketingService, QRSecurityService, NotificationService |
| `AGUARDANDO_PAGAMENTO_TAXA` -> `CANCELADA` | `falhaPagamentoTaxa OU remetenteCancela / cancelarTransferencia(), retornarIngressoRemetente(), estornarTaxa()` | RF43 | PaymentOrchestrator ou Remetente / TransferService |
| `RECUSADA` -> ⊚ (Final) | *(implícito após recusa)* | - | TransferService |
| `EXPIRADA` -> ⊚ (Final) | *(implícito após expiração)* | - | TransferService |
| `CANCELADA` -> ⊚ (Final) | *(implícito após cancelamento)* | - | TransferService |
| `CONCLUIDA` -> ⊚ (Final) | *(implícito após conclusão)* | - | TransferService |

**Autor:** <a href="https://github.com/gabriel-lima258">Gabriel Lima</a>.

</details>

A figura 4 apresenta o diagrama de estados do ciclo de vida da Transferência de Ingresso:

<div align="center">
    <b>Figura 4:</b> Diagrama de Estados — Ciclo de Vida da Transferência de Ingresso
    <br>
    <img src="assets/Modelagem/Dinamica/Estado3.pdf" width="1000">
    <br>
    <b>Autor:</b> <a href="https://github.com/gabriel-lima258">Gabriel Lima</a>.
    <br>
</div>

<p><strong>Observação:</strong> O diagrama será desenvolvido seguindo a estrutura descrita nas Tabelas 5 e 6, modelando o fluxo completo desde a criação da solicitação de transferência até sua conclusão com reemissão do QR Code ou cancelamento.</p>

---

## Conclusão

Os Diagramas de Máquina de Estados detalhados nesta seção fornecem uma modelagem visual dos ciclos de vida das principais entidades do sistema **Ingressou**: **Evento**, **Pedido** e **Transferência de Ingresso**. Através da aplicação de elementos fundamentais e avançados da UML, como estados compostos, condições de guarda e ações específicas de estado (entry/exit/do), foi possível representar de forma clara e precisa as complexas sequências de estados, os eventos que disparam as transições e as regras que governam o comportamento dessas entidades.

Os três diagramas elaborados cobrem os processos críticos do MVP:

1. **Ciclo de Vida do Evento**: Demonstra o fluxo completo desde a criação pelo Admin até o encerramento ou cancelamento, incluindo validações de pré-condições para publicação e gestão de disponibilidade de lotes;
2. **Ciclo de Vida do Pedido**: Evidencia o processo completo de compra, desde a criação do pedido até a confirmação do pagamento ou cancelamento, incluindo suporte a PIX e cartão com comportamentos distintos;
3. **Ciclo de Vida da Transferência**: Mostra o fluxo completo de transferência de ingressos entre usuários, incluindo aceite do destinatário, pagamento de taxa e reemissão segura do QR Code.

Esses diagramas servem como base para implementação, documentação técnica e validação dos requisitos funcionais identificados nos casos de uso (CU-01, CU-11, CU-12, CU-14) e nos documentos de análise (5W2H, Diagrama de Classes, Diagrama de Componentes, Requisitos Elicitados).

---

## Bibliografia

<a name="ref1"></a>
[1] LUCIDCHART. O que é um diagrama de máquina de estados? Disponível em: https://www.lucidchart.com/pages/pt/o-que-e-diagrama-de-maquina-de-estados-uml. Acesso em: 30 out. 2025.

<a name="ref2"></a>
[2] SPARX SYSTEMS. UML 2 Tutorial – State Machine Diagram. Disponível em: https://sparxsystems.com/resources/tutorials/uml2/state-diagram.html. Acesso em: 30 out. 2025.

<a name="ref3"></a>
[3] UML-DIAGRAMS. State Machine Diagrams. Disponível em: https://www.uml-diagrams.org/state-machine-diagrams.html. Acesso em: 30 out. 2025.

<a name="ref4"></a>
[4] IBM. Máquinas de Estado. Disponível em: https://www.ibm.com/docs/pt-br/dmrt/9.5.0?topic=diagrams-state-machines. Acesso em: 30 out. 2025.

<a name="ref5"></a>
[5] LIMA, Gabriel. Diagrama de Classes — Projeto Ingressou (MVP). Outubro de 2025. Disponível em: [Modelagem/ModelagemEstatica/DiagramaClasses.md](/Modelagem/ModelagemEstatica/DiagramaClasses.md).

<a name="ref6"></a>
[6] LIMA, Gabriel. Diagrama de Componentes — Projeto Ingressou. Outubro de 2025. Disponível em: [Modelagem/ModelagemEstatica/DiagramaComponentes.md](/Modelagem/ModelagemEstatica/DiagramaComponentes.md).

<a name="ref7"></a>
[7] LIMA, Gabriel. Diagrama de Casos de Uso — Projeto Ingressou. Outubro de 2025. Disponível em: [Modelagem/ModelagemOrganizacional/DiagramaCasosUso.md](/Modelagem/ModelagemOrganizacional/DiagramaCasosUso.md).

<a name="ref8"></a>
[8] LIMA, Gabriel. Requisitos Elicitados — Ingressou v1.5. Outubro de 2025. Disponível em: [Base/ArtefatoGeneralista/RequisitosElicitados.md](/Base/ArtefatoGeneralista/RequisitosElicitados.md).

---

## Histórico de versão

| Versão | Alteração | Responsável | Data |
|---|---|---|---|
| 1.0 | Criação inicial do documento com três diagramas de estados principais (Evento, Pedido, Transferência) baseados nos documentos Diagrama de Classes, Diagrama de Componentes, Diagrama de Casos de Uso e Requisitos Elicitados | Gabriel Lima | 30/10/2025 |
