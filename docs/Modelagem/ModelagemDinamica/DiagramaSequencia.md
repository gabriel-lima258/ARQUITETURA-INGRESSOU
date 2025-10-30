# Diagrama de Sequência

> **Versão:** 1.0  
> **Data:** Outubro de 2025  
> **Autor:** Gabriel Lima  
> **Projeto:** Ingressou — Plataforma Web de Venda e Gestão de Ingressos  

---

## Sumário

- [Introdução](#Introdução)
- [Objetivos](#Objetivos)
- [Metodologia](#Metodologia)
- [Sobre o Diagrama de Sequência](#Sobre-o-Diagrama-de-Sequência)
- [Cenário 1: Compra de Ingresso](#Cenário-1-Compra-de-Ingresso)
- [Cenário 2: Check-in de Ingresso](#Cenário-2-Check-in-de-Ingresso)
- [Guia Completo: Como Criar e Conectar Classes no Diagrama de Sequência](#Guia-Completo-Como-Criar-e-Conectar-Classes-no-Diagrama-de-Sequência)
- [Conclusão](#Conclusão)
- [Bibliografia](#Bibliografia)
- [Histórico de versão](#Histórico-de-versão)

---

## Introdução

Ao se desenvolver diagramas de sequência, é essencial compreender que eles representam uma das formas de modelar o comportamento dinâmico de um sistema. Sendo assim, de acordo com a Apostila UML - Unified Modeling Language - Linguagem de Modelagem Unificada em Português [1](#ref1), esse tipo de diagrama descreve, de maneira visual e cronológica, a troca de mensagens entre diferentes objetos envolvidos em uma interação, no caso deste documento, sobre **a compra de ingressos** e **o check-in de ingressos** na plataforma Ingressou. Assim, um ponto importante sobre a estrutura básica do diagrama de sequência é composta por dois eixos: o eixo vertical, que representa o tempo (de cima para baixo), e o eixo horizontal, que representa os objetos envolvidos, cada um com sua respectiva linha de vida, como é descrito em [IBM - Diagramas de Sequência](https://www.ibm.com/docs/pt-br/rsm/7.5.0?topic=uml-sequence-diagrams) [3](#ref3).

Para o projeto Ingressou, a elaboração dos diagramas de sequência será baseada nas interações pensadas previamente nos diagramas de classes e de componentes, com o intuito de garantir uma coerência com a estrutura lógica e modular da aplicação.

---

## Objetivos

O objetivo deste documento é apresentar dois diagramas de sequência que representam duas das interações fundamentais na plataforma Ingressou. Com isso, a partir desses diagramas, busca-se:

  - Modelar visualmente os fluxos de mensagens entre os objetos do sistema e os usuários;
  - Especificar a ordem das interações e responsabilidades envolvidas em dois dos módulos principais da plataforma;
  - Ilustrar o comportamento interno da aplicação durante a execução de casos de uso específicos;
  - Apoiar o entendimento do fluxo dinâmico e temporal das funcionalidades com base nas mensagens trocadas.

De forma mais específica, os diagramas desenvolvidos visam representar os seguintes cenários:

1. **Compra de Ingresso**: O fluxo completo de compra de ingressos, desde a seleção do evento até a confirmação do pagamento e emissão do ingresso digital;
2. **Check-in de Ingresso**: A validação de ingressos através de QR Code, tanto em modo online quanto offline.

---

## Metodologia 

A elaboração dos diagramas de sequência seguirá uma abordagem iterativa, com base em alguns dos artefatos previamente construídos no desenvolvimento da plataforma Ingressou. Com base nisso, o processo adotado visa observar o comportamento do sistema por meio da representação temporal das interações.

Os módulos trabalhados são:

- **Compra de Ingresso**: O fluxo principal de negócio da plataforma, envolvendo seleção de evento, escolha de lotes, aplicação de cupons, processamento de pagamento e emissão de ingressos digitais;
- **Check-in de Ingresso**: O processo de validação de ingressos na entrada do evento, com suporte a operação offline e sincronização posterior.

Para isso, foram realizadas as seguintes etapas:

1. Análise dos seguintes artefatos de apoio ao entendimento comportamental:
  - Fluxo do [protótipo de alta fidelidade](/Base/DesignSprint/Prototipo.md);
   - [Diagrama de Classes](/Modelagem/ModelagemDinamica/ModelagemEstatica/DiagramaClasses.md);
   - [Diagrama de Componentes](/Modelagem/ModelagemDinamica/ModelagemEstatica/DiagramaComponentes.md)

2. Após a análise, foram construídos dois diagramas de sequência na ferramenta Draw.io.

---

## Sobre o Diagrama de Sequência

Como foi mencionado na introdução, o diagrama de sequência é uma ferramenta da UML utilizada para representar a interação entre objetos ao longo do tempo durante a execução de um processo específico do sistema. Assim, os elementos e componentes da "linha da vida" serão feitos a partir dos componentes do [diagrama de componentes](/Modelagem/ModelagemDinamica/ModelagemEstatica/DiagramaComponentes.md).

Com base nisso, o diagrama de sequência é composto por diversos elementos fundamentais que permitem representar de forma clara a comunicação entre os objetos de um sistema. Assim, com base em [O que é um diagrama de sequência UML?](https://www.lucidchart.com/pages/pt/o-que-e-diagrama-de-sequencia-uml) [4](#ref4), os atores e objetos participantes são dispostos horizontalmente, cada um com uma linha de vida vertical que indica sua existência ao longo do tempo. As mensagens trocadas entre eles são representadas por setas horizontais, podendo ser síncronas, assíncronas ou de retorno, com ou sem rótulos descritivos.

Para melhor compreensão dos elementos, a figura 1 abaixo funciona como uma legenda para os diagramas elaborados.

<div align="center">
    Figura 1: Legenda do Diagrama de Sequência
    <br>
    <img src="assets/Legendas/LegendaDiagramaSequência.drawio.png" width="500">
    <br>
    <b>Autor:</b> <a href="https://github.com/gabriel-lima258">Gabriel Lima</a>.
    <br>
</div>

---

## Cenário 1: Compra de Ingresso

**Cenário:** Cliente autenticado navega pelo catálogo de eventos, seleciona um evento, escolhe lotes de ingressos, aplica cupom de desconto (opcional), realiza o pagamento e recebe o ingresso digital com QR Code.

A tabela 1 mostra os elementos e as sequências no diagrama em relação à compra de ingressos.

<details>
  <summary><strong>Tabela 1: Sequência da compra de ingressos</strong></summary>

**Tabela 1: Sequência da compra de ingressos**

| Elemento do Diagrama de Sequência | Descrição na Sequência | Relação com Diagrama de Classes | Relação com Requisitos (RFs) | Relação com Diagrama de Componentes |
| :-------------------------------- | :--------------------- | :------------------------------ | :---------------------------- | :---------------------------------- |
| **Lifelines / Participantes** | | | | |
| `Cliente` (Ator) | O usuário final interagindo com a plataforma para comprar ingressos. | Representa uma instância de `Cliente` (herança de `Usuario`). | [RF11](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rf11), [RF13](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rf13), [RF15](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rf15), [RF20](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rf20) | (Externo) Interage com `SPA Principal`. |
| `:SPA Principal` | A interface web responsiva que renderiza o catálogo e processa a compra. | (Implementação) Classes/frameworks de frontend. | [RF06](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rf06), [RF11](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rf11), [RF18](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rf18) | Componente `SPA Principal`. Requer `IGatewayAPI`. |
| `:Gateway Service` | Ponto de entrada para as requisições do backend, roteia para os serviços apropriados. | (Implementação) Framework de API Gateway. | [RNF02](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rnf02), [RNF05](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rnf05) | Componente `Gateway Service`. Provê `IGatewayAPI`. |
| `:EventSearchService` | Responsável pela busca e filtros de eventos. | Classes: `Evento`, `Categoria`, `Localizacao`. | [RF06](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rf06), [RF07](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rf07), [RF08](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rf08), [RF09](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rf09), [RF10](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rf10) | Componente `EventSearchService`. Provê `IEventSearch`. |
| `:CheckoutService` | Gerencia o processo de checkout e aplicação de cupons. | Classes: `Pedido`, `ItemPedido`, `Cupom`, `Lote`. | [RF26](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rf26), [RF31](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rf31), [RF27](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rf27) | Componente `CheckoutService`. Provê `ICheckout`. |
| `:PaymentOrchestrator` | Orquestra o processamento de pagamentos. | Classes: `Pagamento`, `GatewayPagamento`. | [RF27](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rf27), [RF28](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rf28) | Componente `PaymentOrchestrator`. Provê `IPaymentOrchestrator`. |
| `:TicketingService` | Emite ingressos e gera QR Codes após confirmação de pagamento. | Classes: `Ingresso`, `QrCode`, `Carteira`. | [RF32](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rf32), [RF35](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rf35) | Componente `TicketingService`. Provê `ITicketing`. |
| `:NotificationService` | Envia notificações de confirmação por e-mail/WhatsApp. | Classes: `Notificacao`. | [RF35](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rf35) | Componente `NotificationService`. Provê `INotificationService`. |
| `:BancoDeDados` | Armazena os dados persistentes da aplicação. | Todas as classes persistentes e seus relacionamentos. | [RNF10](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rnf10) | Componente `PostgreSQL Database`. |
| **Mensagens / Interações Chave** | | | | |
| `1: navegarCatalogo()` ... `5: ...` | Cliente acessa catálogo, sistema busca e exibe eventos com filtros. | Métodos `listarEventos`, `buscarEventos` (`EventSearchService`). | [RF06](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rf06), [RF07](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rf07), [RF08](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rf08), [RF09](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rf09), [RF10](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rf10) | `SPA Principal`->`IGatewayAPI`, `Gateway Service`->`IEventSearch`. |
| `6: selecionarEvento(...)` ... `10: ...` | Cliente seleciona evento, sistema exibe detalhes e lotes disponíveis. | Métodos `buscarEvento`, `listarLotes` (`EventSearchService`). | [RF18](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rf18) | Similar ao anterior, focado em evento específico. |
| `11: adicionarAoCarrinho(...)` ... `15: ...` | Cliente adiciona ingressos ao carrinho, sistema valida disponibilidade. | Métodos `adicionarItem` (`CheckoutService`), `reservar` (`Lote`). | [RF26](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rf26) | `Gateway Service`->`ICheckout`. |
| `16: aplicarCupom(...)` ... `20: ...` | Cliente aplica cupom, sistema valida e calcula desconto. | Métodos `aplicarCupom` (`Pedido`), `validar` (`Cupom`). | [RF13](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rf13), [RF31](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rf31) | `CheckoutService`->`ICupomRepository`. |
| `21: finalizarPedido()` ... `25: ...` | Cliente finaliza pedido, sistema cria reserva temporária. | Métodos `fechar` (`Pedido`), `criarPedido` (`CheckoutService`). | [RF26](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rf26) | `CheckoutService`->`IPedidoRepository`. |
| `26: processarPagamento(...)` ... `30: ...` | Sistema inicia processamento de pagamento via gateway. | Métodos `iniciarCobranca` (`GatewayPagamento`), `autorizar` (`Pagamento`). | [RF27](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rf27), [RF28](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rf28) | `PaymentOrchestrator`->`IGatewayPagamento`. |
| `31: confirmarPagamento()` ... `35: ...` | Pagamento confirmado, sistema atualiza status e libera estoque. | Métodos `confirmar` (`Pagamento`), `confirmar` (`GatewayPagamento`). | [RF29](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rf29), [RF30](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rf30) | `PaymentOrchestrator`->`IMessageBus`. |
| `36: emitirIngressos()` ... `40: ...` | Sistema emite ingressos digitais com QR Code assinado. | Métodos `emitirNovoQr` (`Ingresso`), `adicionar` (`Carteira`). | [RF32](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rf32), [RF35](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rf35) | `TicketingService`->`IQRSecurityService`. |
| `41: enviarNotificacao()` ... `45: ...` | Sistema envia confirmação por e-mail/WhatsApp. | Métodos `enviar` (`Notificacao`). | [RF35](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rf35) | `NotificationService`->`IGatewayEmail`, `IGatewayWhatsApp`. |

<b> Autor: </b> <a href="https://github.com/gabriel-lima258">Gabriel Lima</a>.

</details>

Com base na tabela 1, abaixo, na figura 2, há o diagrama de Sequência - Compra de Ingresso

<div align="center">
    Figura 2: Diagrama de Sequência - Compra de Ingresso
    <br>
    <img src="assets/Modelagem/Dinamica/Sequencia1.png" width="1000">
    <br>
    <b>Autor:</b> <a href="https://github.com/gabriel-lima258">Gabriel Lima</a>.
    <br>
</div>

---

## Cenário 2: Check-in de Ingresso

**Cenário:** Operador de check-in utiliza o PWA para validar ingressos apresentados pelos clientes, através da leitura de QR Code, funcionando em modo online ou offline.

A tabela 2 mostra os elementos e as sequências no diagrama em relação ao check-in de ingressos.

<details>
  <summary><strong>Tabela 2: Sequência do check-in de ingressos</strong></summary>

**Tabela 2: Sequência do check-in de ingressos**

| Elemento do Diagrama de Sequência | Descrição na Sequência | Relação com Diagrama de Classes | Relação com Requisitos (RFs) | Relação com Diagrama de Componentes |
| :-------------------------------- | :--------------------- | :------------------------------ | :---------------------------- | :---------------------------------- |
| **Lifelines / Participantes** | | | | |
| `Operador` (Ator) | O usuário com permissão CHECKIN que valida ingressos na portaria. | Representa uma instância de `Usuario` com role `CHECKIN`. | [RF36](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rf36), [RF37](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rf37), [RF38](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rf38) | (Externo) Interage com `PWA Check-in`. |
| `:PWA Check-in` | Aplicativo PWA para validação de ingressos (online/offline). | (Implementação) Classes/frameworks de frontend PWA. | [RF36](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rf36), [RF37](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rf37), [RF38](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rf38), [RNF08](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rnf08) | Componente `PWA Check-in`. Requer `ICheckinAPI`. |
| `:Gateway Service` | Ponto de entrada para as requisições do backend. | (Implementação) Framework de API Gateway. | [RNF02](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rnf02), [RNF05](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rnf05) | Componente `Gateway Service`. Provê `IGatewayAPI`. |
| `:CheckinValidator` | Valida QR Codes e registra check-ins. | Classes: `CheckinRegistro`, `Ingresso`, `QrCode`. | [RF33](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rf33), [RF36](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rf36), [RF37](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rf37), [RB10](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rb10) | Componente `CheckinValidator`. Provê `ICheckin`. |
| `:QRSecurityService` | Valida assinaturas digitais dos QR Codes. | Classes: `QrCode`. | [RNF06](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rnf06) | Componente `QRSecurityService`. Provê `IQRSecurityService`. |
| `:CheckinOfflineSync` | Sincroniza dados capturados offline. | Classes: `CheckinRegistro`. | [RF38](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rf38) | Componente `CheckinOfflineSync`. Provê `IOfflineSync`. |
| `:BancoDeDados` | Armazena registros de check-in e dados de ingressos. | Classes: `CheckinRegistro`, `Ingresso`, `QrCode`. | [RNF10](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rnf10) | Componente `PostgreSQL Database`. |
| **Mensagens / Interações Chave** | | | | |
| `1: abrirAppCheckin()` ... `5: ...` | Operador abre PWA, sistema verifica conectividade e sincroniza dados. | Métodos `sincronizarDados` (`CheckinOfflineSync`). | [RF38](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rf38) | `PWA Check-in`->`ICheckinAPI`, `Gateway Service`->`IOfflineSync`. |
| `6: escanearQR(...)` ... `10: ...` | Operador escaneia QR Code, sistema captura e valida formato. | Métodos `capturarQR` (`PWA Check-in`). | [RF36](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rf36) | `PWA Check-in`->`ICheckinAPI`. |
| `11: validarQR(...)` ... `15: ...` | Sistema valida assinatura digital e verifica status do ingresso. | Métodos `verificarHash` (`QrCode`), `validar` (`Ingresso`). | [RF33](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rf33), [RNF06](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rnf06) | `CheckinValidator`->`IQRSecurityService`. |
| `16: verificarStatus(...)` ... `20: ...` | Sistema verifica se ingresso já foi utilizado e se está válido. | Métodos `validarEntrada` (`Ingresso`), `buscarCheckins` (`CheckinRegistro`). | [RF33](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rf33), [RB10](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rb10) | `CheckinValidator`->`IIngressoRepository`. |
| `21: registrarCheckin(...)` ... `25: ...` | Sistema registra check-in e marca ingresso como utilizado. | Métodos `registrar` (`CheckinRegistro`), `validarEntrada` (`Ingresso`). | [RF37](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rf37), [RF38](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rf38) | `CheckinValidator`->`ICheckinRegistroRepository`. |
| `26: sincronizarOffline(...)` ... `30: ...` | Se offline, sistema armazena localmente para sincronização posterior. | Métodos `armazenarLocal` (`CheckinOfflineSync`). | [RF38](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rf38) | `CheckinOfflineSync`->`IIngressoRepository`. |
| `31: exibirResultado(...)` ... `35: ...` | Sistema exibe resultado da validação para o operador. | Métodos `exibirResultado` (`PWA Check-in`). | [RF36](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rf36), [RF37](/Base/ArtefatoGeneralista/RequisitosElicitados.md#rf37) | `PWA Check-in`->`ICheckinUI`. |

<b> Autor: </b> <a href="https://github.com/gabriel-lima258">Gabriel Lima</a>.

</details>

Com base na tabela 2, abaixo, na figura 3, há o diagrama de Sequência - Check-in de Ingresso

<div align="center">
    Figura 3: Diagrama de Sequência - Check-in de Ingresso
    <br>
    <img src="assets/Modelagem/Dinamica/Sequencia2.png" width="1000">
    <br>
    <b>Autor:</b> <a href="https://github.com/gabriel-lima258">Gabriel Lima</a>.
    <br>
</div>

---

## Conclusão

A elaboração dos diagramas de sequência permitiu representar com clareza os fluxos de interação entre os usuários e o sistema da plataforma Ingressou, o que permitiu uma compreensão maior sobre a dinâmica de funcionamento das funcionalidades de compra de ingressos e validação de check-in.

Os diagramas desenvolvidos demonstram a arquitetura modular do sistema, evidenciando como os diferentes componentes se comunicam para atender aos requisitos funcionais e não funcionais da plataforma. A separação clara entre as responsabilidades dos componentes facilita a manutenção e evolução do sistema.

---

## Bibliografia

<a name="ref1"></a>
[1] APOSTILA UML. Unified Modeling Language – Linguagem de Modelagem Unificada em Português. Seção sobre diagrama de sequência. Disponibilizada pela professora. Acesso em: 30 abr. 2025.

<a name="ref2"></a>
[2] CREATELY. Tutorial do Diagrama de Sequência: Guia completo com exemplos. Disponível em: https://creately.com/blog/pt/diagrama/tutorial-do-diagrama-de-sequencia/. Acesso em: 30 abr. 2025.

<a name="ref3"></a>
[3] IBM. Diagramas de Sequência. Atualizado pela última vez em: 5 mar. 2021. Disponível em: https://www.ibm.com/docs/pt-br/rsm/7.5.0?topic=uml-sequence-diagrams. Acesso em: 30 abr. 2025.

<a name="ref4"></a>
[4] LUCIDCHART. O que é um diagrama de sequência UML? Disponível em: https://www.lucidchart.com/pages/pt/o-que-e-diagrama-de-sequencia-uml. Acesso em: 30 abr. 2025.

---

## Histórico de versão

| Versão | Alteração | Responsável | Data |
| - | - | - | - |
| 1.0 | Elaboração do documento e diagramas de sequência para o projeto Ingressou | Gabriel Lima | 27/10/2025 |
| 1.1 | Adição do guia completo para criação e conexão de classes baseado no diagrama de sequência | Gabriel Lima | 27/10/2025 |