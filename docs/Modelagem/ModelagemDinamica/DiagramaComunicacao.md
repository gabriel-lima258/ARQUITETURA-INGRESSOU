# Diagrama de Comunicação — Projeto Ingressou (MVP)

> **Versão:** 1.0  
> **Data:** Outubro de 2025  
> **Autor:** Gabriel Lima  
> **Projeto:** Ingressou — Plataforma Web de Venda e Gestão de Ingressos  

---

## Sumário

- [Introdução](#introdução)
- [Objetivos](#objetivos)
- [Metodologia](#metodologia)
- [Sobre o Diagrama de Comunicação](#sobre-o-diagrama-de-comunicação)
- [Cenário 1: Compra de Ingresso](#cenário-1-compra-de-ingresso)
- [Cenário 2: Transferência de Ingresso](#cenário-2-transferência-de-ingresso)
- [Conclusão](#conclusão)
- [Bibliografia](#bibliografia)
- [Histórico de versão](#histórico-de-versão)


## Introdução

O diagrama de colaboração (ou de comunicação), como é definido na Apostila UML - Unified Modeling Language - Linguagem de Modelagem Unificada em Português [1](#ref1), representa como os objetos de um sistema interagem entre si ao focar nos relacionamentos e nas trocas de mensagens mais do que na ordem temporal dessas ações. Segundo a [IBM: Diagramas de comunicação](https://www.ibm.com/docs/pt-br/radfws/9.6.0?topic=SSRTLW_9.6.0/com.ibm.xtools.sequence.doc/topics/ccommndiag.htm) [3](#ref3), esse tipo de diagrama permite analisar o comportamento dinâmico do sistema ao identificar objetos participantes, dados trocados e caminhos de mensagens.

Dessa forma, como o desenvolvimento de diagramas de comunicação é essencial para visualizar como os componentes e objetos do sistema interagem entre si, especialmente em áreas com maior troca de mensagens, esse artefato apresenta os diagramas de comunicação para os **cenários principais do Ingressou**: **compra de ingressos** e **transferência de ingressos**. 


## Objetivos

O objetivo deste documento é representar graficamente os principais fluxos de interação entre objetos do sistema Ingressou por meio de diagramas de comunicação (ou colaboração). De forma mais específica, busca-se:

- Ilustrar a troca de mensagens entre instâncias de classes nos cenários de **compra de ingressos** e **transferência de ingressos**;

- Demonstrar a organização estrutural das interações com foco nos relacionamentos entre os objetos;

- Evidenciar a ordem sequencial das mensagens numeradas para facilitar o rastreamento dos comportamentos do sistema;

- Apoiar a modelagem dinâmica da plataforma com base em dois cenários práticos: **processo de compra de ingresso** e **transferência de ingresso entre usuários**.


## Metodologia

A elaboração dos diagramas de comunicação seguirá uma abordagem fundamentada na análise integrada dos artefatos previamente desenvolvidos no projeto Ingressou. 

Sobre os cenários de foco neste artefato:

- **Cenário 1 - Compra de Ingresso**: Processo completo de compra de ingresso, desde a seleção do evento e lote até a confirmação do pagamento e emissão do ingresso digital com QR Code. Este cenário envolve validações de estoque, processamento de pagamento (PIX/cartão), aplicação de cupons e notificações ao usuário.

- **Cenário 2 - Transferência de Ingresso**: Fluxo de transferência de ingresso entre usuários, incluindo criação da solicitação, aceite do destinatário, pagamento da taxa de transferência, invalidação do QR original e emissão de novo QR Code para o destinatário.
 
Para a construção dos diagramas, serão seguidas as etapas abaixo:

1. Serão analisados os seguintes artefatos para embasamento dos diagramas:

- [Requisitos Funcionais e Não Funcionais elicitados](/Base/ArtefatoGeneralista/RequisitosElicitados.md);
- [5W2H](/Base/ArtefatoGeneralista/5W2H.md);
- [Brainstorming](/Base/ArtefatoGeneralista/BrainStorm.md);
- [Diagrama de Classes](/Modelagem/ModelagemEstatica/DiagramaClasses.md);
- [Diagrama de Componentes](/Modelagem/ModelagemEstatica/DiagramaComponentes.md);
- [Diagrama de Casos de Uso](/Modelagem/ModelagemOrganizacional/DiagramaCasosUso.md).

2. Dois diagramas serão desenvolvidos, sendo um para o cenário de **compra de ingresso** e outro para o cenário de **transferência de ingresso**;

3. Os diagramas serão criados utilizando a ferramenta [Draw.io](https://www.drawio.com/blog/uml-component-diagrams);


## Sobre o Diagrama de Comunicação

Conforme explicado em [Guia: Diagramas de colaboração UML](https://miro.com/pt/diagrama/o-que-e-diagrama-colaboracao-uml/) [5](#ref5), os Diagramas de Comunicação (também conhecidos como diagramas de Colaboração) apresentados a seguir ilustram as interações dinâmicas entre os diferentes objetos e componentes de sistema necessários para realizar cenários específicos da plataforma Ingressou. Diferente dos diagramas de sequência que enfatizam a ordem temporal, estes diagramas focam na estrutura da colaboração ao mostrar os Vínculos (linhas de conexão) que existem entre os participantes (objetos/componentes como :WebUI, :CheckoutService, :PaymentOrchestrator, cliente:Usuario, etc.) e como as Mensagens (as quais representam chamadas de métodos ou comunicação) trafegam por esses vínculos para executar uma tarefa, como comprar um ingresso ou transferir um ingresso entre usuários. Além disso, a sequência exata das interações é definida pela numeração anexada a cada mensagem, onde a notação decimal (ex: 1, 1.1, 1.2) indica o fluxo de controle e as chamadas aninhadas que ocorrem durante o processo, como é explicado em [Criar um diagrama de comunicação UML](https://support.microsoft.com/pt-br/topic/criar-um-diagrama-de-comunica%C3%A7%C3%A3o-uml-911956f4-5f19-4a58-97a3-bb14110a5ed1). [4](#ref4)

Com base no que foi explicado em [Criar um diagrama de comunicação UML](https://support.microsoft.com/pt-br/topic/criar-um-diagrama-de-comunica%C3%A7%C3%A3o-uml-911956f4-5f19-4a58-97a3-bb14110a5ed1) [4](#ref4), para construir estes diagramas e representar detalhadamente as interações, foram utilizados elementos chave da UML. Dessa forma, os participantes são mostrados como Objetos/Linhas de Vida (retângulos nomeados), conectados por Vínculos (linhas sólidas) que representam os caminhos de comunicação. As Mensagens, indicadas por setas ao longo dos vínculos, são rotuladas com números de sequência decimais para denotar a ordem e o aninhamento, nomes de operações e, ocasionalmente, parâmetros. Além desses fundamentos, para capturar a complexidade dos cenários, foram empregados elementos avançados: a notação <<create>> para indicar a criação de novas instâncias (como pedidoCriado : Pedido ou ingressoEmitido : Ingresso), Iteração (*) para mensagens repetidas (como na validação de estoque), Autochamadas (mensagens com setas em loop no mesmo objeto, ex: atualizações da :WebUI), e a notação <<destroy>> para indicar o fim do ciclo de vida de um objeto (como a sessaoTransferencia). 

Para melhor compreensão dos diagramas, a figura 1 mostra a legenda;

<div align="center">
    Figura 1: Legenda do Diagrama de Comunicação
    <br>
    <img src="assets/Legendas/LegendaDiagramaComunica%C3%A7%C3%A3o.drawio.png" width="500">
    <br>
    <b>Autora:</b> <a href="">Larissa Stéfane</a>.
    <br>
</div>


**Observação Importante:** Com o intuido de elaborar melhor os diagramas, foram elaboradas tabelas contendo os elementos/Participantes com suas descrições e relação com os requisitos elicitados e com os componentes do diagrama de componentes **(Tabelas 1 e 3)**. 
Da mesma forma, foram criadas tabelas que mostram os vínculos entre os objetos **(Tabelas 2 e 4)**

## Cenário 1: Compra de Ingresso

Para elucidar os elementos que interagem e colaboram no Diagrama de Comunicação referente ao processo de compra de ingresso na plataforma Ingressou, a Tabela 1 a seguir identifica e descreve cada participante (objetos ou instâncias de classes) envolvido. Esta tabela tem como objetivo fornecer uma visão detalhada de cada elemento que troca mensagens ao detalhar a sua funcionalidade no contexto específico das interações de compra. 

<details>
  <summary><strong>Tabela 1: Participantes do Diagrama de Comunicação (Compra de Ingresso)</strong></summary>

**Tabela 1:** Participantes do Diagrama de Comunicação (Compra de Ingresso)

| #  | Elemento/Participante      | Descrição/Funcionalidade                                          | Relação Requisitos (RFs)        | Relação Componentes (Nome e #)                                 | Relação Classes (# e Nome)                     |
|----|----------------------------|-------------------------------------------------------------------|---------------------------------|----------------------------------------------------------------|------------------------------------------------|
| 1  | `cliente : Usuario`        | O usuário final que realiza a compra do ingresso.                 | RF01, RF26, RF27, RF28         | (Ator Externo, interage com WebUI #1)                          | #01 Usuario                                    |
| 2  | `: WebUI`                  | Interface no navegador para interação do usuário com o checkout.  | (Suporte visual para RFs de Compra) | `SPA Principal` (#1)                                         | (Usa dados de várias classes)                  |
| 3  | `: GatewayService`         | Ponto de entrada API para requisições de checkout vindas da WebUI. | (Infraestrutura)                | `Gateway Service` (#5)                                         | (Orquestra chamadas a componentes/serviços)    |
| 4  | `: AuthService`            | Verifica autenticação e permissões do usuário.                   | (Suporte a regras RF01-RF05)    | `AuthService` (#6)                                             | #01 Usuario                                    |
| 5  | `: CheckoutService`        | Orquestrador principal da lógica de checkout (validação, reserva). | RF26, RF31                      | `CheckoutService` (#12)                                        | #10 Pedido, #11 ItemPedido, #19 Cupom         |
| 6  | `pedidoCriado : Pedido`    | Instância do Pedido sendo criado.                                 | RF26                            | (Gerenciado por `CheckoutService` #12)                         | #10 Pedido                                     |
| 7  | `: PaymentOrchestrator`    | Orquestra processamento de pagamentos PIX e cartão.              | RF27, RF28                      | `PaymentOrchestrator` (#13)                                    | #12 Pagamento                                  |
| 8  | `pagamentoCriado : Pagamento`| Instância do Pagamento sendo processado.                        | RF27, RF28                      | (Gerenciado por `PaymentOrchestrator` #13)                     | #12 Pagamento                                  |
| 9  | `: TicketingService`       | Emite ingressos e QR Codes após confirmação de pagamento.        | RF32, RF35                      | `TicketingService` (#15)                                       | #13 Ingresso, #14 QrCode                       |
| 10 | `ingressoEmitido : Ingresso`| Instância do Ingresso sendo emitido.                             | RF32                            | (Gerenciado por `TicketingService` #15)                        | #13 Ingresso                                   |
| 11 | `: NotificationService`    | Envia notificações de confirmação por e-mail/WhatsApp.           | RF35, RF47                      | `NotificationService` (#23)                                    | #17 Notificacao                                |
| 12 | `: CacheService`          | Armazena dados temporários para performance.                     | RNF15                           | `Redis Cache` (#28)                                            | (Cache de dados)                               |
| 13 | `: BancoDeDados`          | Armazena/Recupera dados persistentes do sistema.                 | (Suporte a todos RFs)           | `PostgreSQL Database` (#25)                                    | (Persiste instâncias de várias classes)        |

<b> Autor: </b> <a href="https://github.com/gabriel-lima258">Gabriel Lima</a>.

</details>

Para complementar a identificação dos participantes, a Tabela 2 se aprofunda na dinâmica das interações do processo de compra ao detalhar a sequência, o conteúdo e as características das mensagens trocadas e dos vínculos estabelecidos no Diagrama de Comunicação correspondente. O propósito desta tabela é servir como um guia para a leitura do diagrama.

<details>
  <summary><strong>Tabela 2: Mensagens e Vínculos do Diagrama de Comunicação (Compra de Ingresso)</strong></summary>

**Tabela 2:** Mensagens e Vínculos do Diagrama de Comunicação (Compra de Ingresso)

| Etapa        | Vínculo (Mensagem)                                                              | Tipo                                         | Origem -> Destino                           | Relação Requisitos (RFs) | Relação Componentes (Origem -> Destino)              | Relação Classes (Método/Dados)               |
|--------------|---------------------------------------------------------------------------------|----------------------------------------------|---------------------------------------------|--------------------------|------------------------------------------------------|----------------------------------------------|
| 1            | `selecionarEventoELote(...)`                                                    | Operação Lógica (Autochamada)                | :WebUI -> :WebUI                            | RF06, RF07, RF08         | #1 SPA Principal -> #1 SPA Principal                 | (Lógica UI)                                  |
| 2            | `iniciarCheckout(...)`                                                          | Operação Lógica                              | :WebUI -> :GatewayService                   | RF26                     | #1 SPA Principal -> #5 Gateway Service               | (Payload com dados do pedido)                |
| 2.1          | `logEvento('inicio_checkout')`                                                  | Operação Lógica                              | :GatewayService -> :ServicoMonitoramento    | RNF11                    | #5 Gateway Service -> #6 ServicoMonitoramento        | (Log)                                        |
| 2.2          | `verificarAutenticacao(...)`                                                    | Operação Lógica                              | :GatewayService -> :AuthService             | RF02, RF03               | #5 Gateway Service -> #6 AuthService                 | (Verifica dados de Usuario #01)              |
| [authOK] 2.3 | `processarCheckout(...)`                                                        | Operação Lógica                              | :GatewayService -> :CheckoutService         | RF26                     | #5 Gateway Service -> #12 CheckoutService            | (Orquestra criação de Pedido #10)            |
| 2.3.1        | `validarDisponibilidadeLote(...)`                                               | Operação Lógica                              | :CheckoutService -> :BancoDeDados           | RF21, RF22               | #12 CheckoutService -> #25 PostgreSQL Database       | (Verifica Lote #09)                          |
| 2.3.2        | `reservarIngressos(...)`                                                        | Operação Lógica                              | :CheckoutService -> :BancoDeDados           | RF21                     | #12 CheckoutService -> #25 PostgreSQL Database       | (Reserva estoque Lote #09)                   |
| 2.3.3        | `<<create>> criarPedido(...)`                                                   | Operação Lógica                              | :CheckoutService -> :BancoDeDados           | RF26                     | #12 CheckoutService -> #25 PostgreSQL Database       | (Cria/Persiste Pedido #10)                   |
| 2.3.4        | `aplicarCupom(codigoCupom)`                                                     | Operação Lógica                              | :CheckoutService -> :BancoDeDados           | RF31                     | #12 CheckoutService -> #25 PostgreSQL Database       | (Valida Cupom #19)                           |
| 2.3.5        | `calcularTotal(...)`                                                            | Operação Lógica (Autochamada)                | :CheckoutService -> :CheckoutService        | RF26                     | #12 CheckoutService -> #12 CheckoutService           | (Lógica de cálculo)                          |
| 3            | `processarPagamento(...)`                                                       | Operação Lógica                              | :CheckoutService -> :PaymentOrchestrator    | RF27, RF28               | #12 CheckoutService -> #13 PaymentOrchestrator       | (Inicia Pagamento #12)                       |
| 3.1          | `<<create>> criarPagamento(...)`                                                | Operação Lógica                              | :PaymentOrchestrator -> :BancoDeDados       | RF27, RF28               | #13 PaymentOrchestrator -> #25 PostgreSQL Database   | (Cria Pagamento #12)                         |
| 3.2          | `iniciarCobrancaPIX(...)`                                                       | Operação Lógica                              | :PaymentOrchestrator -> :GatewayPagamento   | RF27                     | #13 PaymentOrchestrator -> #29 Gateway de Pagamento  | (Integração externa)                         |
| 3.3          | `aguardarConfirmacao(...)`                                                      | Operação Lógica                              | :PaymentOrchestrator -> :PaymentOrchestrator| RF27                     | #13 PaymentOrchestrator -> #13 PaymentOrchestrator   | (Aguarda webhook)                            |
| [pagOK] 4    | `emitirIngressos(...)`                                                          | Operação Lógica                              | :PaymentOrchestrator -> :TicketingService   | RF32                     | #13 PaymentOrchestrator -> #15 TicketingService      | (Inicia emissão Ingresso #13)                |
| 4.1          | `<<create>> gerarIngresso(...)`                                                 | Operação Lógica                              | :TicketingService -> :BancoDeDados          | RF32                     | #15 TicketingService -> #25 PostgreSQL Database      | (Cria Ingresso #13)                          |
| 4.2          | `gerarQRCode(...)`                                                              | Operação Lógica                              | :TicketingService -> :QRSecurityService     | RF32, RNF06              | #15 TicketingService -> #16 QRSecurityService        | (Gera QrCode #14)                            |
| 4.3          | `atualizarStatusPedido('PAGO')`                                                 | Operação Lógica                              | :TicketingService -> :BancoDeDados          | RF29                     | #15 TicketingService -> #25 PostgreSQL Database      | (Atualiza Pedido #10)                        |
| 5            | `enviarNotificacaoConfirmacao(...)`                                             | Operação Lógica                              | :TicketingService -> :NotificationService   | RF35                     | #15 TicketingService -> #23 NotificationService      | (Cria Notificacao #17)                       |
| 6            | `exibirConfirmacaoCompra(...)`                                                  | Operação Lógica                              | :WebUI -> cliente: Usuario                  | RF26                     | #1 SPA Principal -> (Ator)                           | (Exibe dados do Pedido #10)                  |

<b> Autor: </b> <a href="https://github.com/gabriel-lima258">Gabriel Lima</a>.

</details>

A Figura 2 mostra o diagrama de comunicação do cenário de compra de ingresso

<div align="center">
    <b>Figura 2:</b> Diagrama de Comunicação – Compra de Ingresso
    <br>
    <img src="assets/Modelagem/Dinamica/Comunicacao1.pdf" width="1000">
    <br>
    <b>Autor:</b> <a href="https://github.com/gabriel-lima258">Gabriel Lima</a>.
</div>

<p><strong>Observação:</strong> Caso deseje visualizar ou baixar em PDF, clique aqui: 
<a href="assets/Modelagem/Dinamica/Comunicacao1.pdf">PDF do Diagrama de Comunicação – Compra de Ingresso</a></p>




## Cenário 2: Transferência de Ingresso

A fim de detalhar os colaboradores envolvidos nos cenários de interação da transferência de ingressos, conforme ilustrado no respectivo Diagrama de Comunicação, a Tabela 3 apresenta uma listagem descritiva de cada participante e seu papel funcional. Esta tabulação visa clarificar as responsabilidades de cada objeto ou instância dentro do fluxo de transferência, vinculando-os aos Requisitos Funcionais (RFs) específicos que implementam, aos Componentes arquiteturais relacionados e às Classes do modelo de domínio que lhes dão origem. 

<details>
  <summary><strong>Tabela 3: Participantes do Diagrama de Comunicação (Transferência de Ingresso)</strong></summary>

**Tabela 3:** Participantes do Diagrama de Comunicação (Transferência de Ingresso)

| #  | Elemento/Participante          | Descrição/Funcionalidade                                                      | Relação Requisitos (RFs)          | Relação Componentes (Nome e #)                                    | Relação Classes (# e Nome)                                   |
|----|--------------------------------|-------------------------------------------------------------------------------|-----------------------------------|-----------------------------------------------------------------|--------------------------------------------------------------|
| 01  | `remetente : Usuario`          | O usuário que inicia a transferência do ingresso.                             | RF40, RF41, RF42                  | (Ator Externo, interage com WebUI #1)                             | #01 Usuario                                                  |
| 02  | `destinatario : Usuario`       | O usuário que recebe o ingresso transferido.                                  | RF40, RF41, RF42                  | (Ator Externo, interage com WebUI #1)                             | #01 Usuario                                                  |
| 03  | `: WebUI`                      | Interface no navegador para gerenciar transferências.                         | (Suporte visual RFs de Transferência) | `SPA Principal` (#1)                                          | (Usa dados de várias classes)                                |
| 04  | `: GatewayService`             | Ponto de entrada API para requisições de transferência.                       | (Infraestrutura)                  | `Gateway Service` (#5)                                            | (Orquestra chamadas a componentes/serviços)                  |
| 05  | `: AuthService`                | Verifica autenticação dos usuários envolvidos.                               | RF02, RF03                        | `AuthService` (#6)                                                | #01 Usuario                                                   |
| 06  | `: TransferService`            | Lógica principal das transferências (criar, aceitar, reemitir).              | RF40-RF47                         | `TransferService` (#17)                                           | #16 Transferencia, #13 Ingresso                              |
| 07  | `transferenciaCriada : Transferencia`| Instância da transferência sendo processada.                            | RF40                              | (Gerenciado por `TransferService` #17)                            | #16 Transferencia                                             |
| 08  | `ingressoOriginal : Ingresso`  | Instância do ingresso sendo transferido.                                     | RF40, RF42                        | (Gerenciado por `TransferService` #17)                            | #13 Ingresso                                                  |
| 09  | `: PaymentOrchestrator`        | Processa pagamento da taxa de transferência.                                 | RF45                              | `PaymentOrchestrator` (#13)                                       | #12 Pagamento                                                 |
| 10  | `: TicketingService`           | Invalida QR original e gera novo QR para destinatário.                       | RF42                              | `TicketingService` (#15)                                          | #13 Ingresso, #14 QrCode                                      |
| 11  | `: NotificationService`        | Envia notificações sobre status da transferência.                            | RF47                              | `NotificationService` (#23)                                       | #17 Notificacao                                               |
| 12  | `: CacheService`              | Armazena dados temporários para performance.                                 | RNF15                             | `Redis Cache` (#28)                                               | (Cache de dados)                                              |
| 13  | `: BancoDeDados`              | Persistência de dados das transferências e ingressos.                        | (Suporte a todos RFs)             | `PostgreSQL Database` (#25)                                       | (Persiste instâncias de várias classes)                       |

<b> Autor: </b> <a href="https://github.com/gabriel-lima258">Gabriel Lima</a>.

</details>

Para uma análise minuciosa do fluxo de mensagens e das conexões representadas no Diagrama de Comunicação da Transferência de Ingressos, a Tabela 4 subsequente cataloga e explica cada interação fundamental entre os participantes. Através desta tabela, busca-se facilitar a compreensão do diagrama ao mapear a sequência da comunicação, ao identificar o conteúdo de cada mensagem (vínculo), seu tipo, o remetente e o destinatário. Para enriquecer o entendimento, a tabela também correlaciona essas trocas de mensagens com os Requisitos Funcionais (RFs) atendidos e as interações entre Componentes e os métodos/dados das Classes.

<details>
  <summary><strong>Tabela 4: Mensagens e Vínculos do Diagrama de Comunicação (Transferência de Ingresso)
</strong></summary>

**Tabela 4:** Mensagens e Vínculos do Diagrama de Comunicação (Transferência de Ingresso)


| Etapa        | Vínculo (Mensagem)                                                              | Tipo                                            | Origem -> Destino                        | Relação Requisitos (RFs) | Relação Componentes (Origem -> Destino)                     | Relação Classes (Método/Dados)                      |
|--------------|---------------------------------------------------------------------------------|-------------------------------------------------|------------------------------------------|--------------------------|-----------------------------------------------------------|-----------------------------------------------------|
| 1            | `iniciarTransferencia(ingressoId, emailDestinatario)`                          | Operação Lógica                                 | :WebUI -> :GatewayService                | RF40                     | #1 SPA Principal -> #5 Gateway Service                     | (Inicia fluxo de transferência)                         |
| 1.1          | `logEvento('inicio_transferencia')`                                             | Operação Lógica                                 | :GatewayService -> :ServicoMonitoramento | RNF11                    | #5 Gateway Service -> #6 ServicoMonitoramento             | (Log)                                                 |
| 1.2          | `verificarAutenticacao(...)`                                                    | Operação Lógica                                 | :GatewayService -> :AuthService          | RF02, RF03               | #5 Gateway Service -> #6 AuthService                       | (Verifica Usuario #01)                                |
| [authOK] 1.3 | `criarTransferencia(...)`                                                       | Operação Lógica                                 | :GatewayService -> :TransferService      | RF40                     | #5 Gateway Service -> #17 TransferService                  | (Orquestra criação Transferencia #16)                   |
| 1.3.1        | `validarElegibilidadeIngresso(...)`                                             | Operação Lógica                                 | :TransferService -> :BancoDeDados        | RF44                     | #17 TransferService -> #25 PostgreSQL Database            | (Verifica Ingresso #13)                               |
| 1.3.2        | `verificarPoliticaTransferencia(...)`                                           | Operação Lógica                                 | :TransferService -> :BancoDeDados        | RF44                     | #17 TransferService -> #25 PostgreSQL Database            | (Verifica TransferPolicy #15)                          |
| 1.3.3        | `<<create>> criarTransferencia(...)`                                            | Operação Lógica                                 | :TransferService -> :BancoDeDados        | RF40                     | #17 TransferService -> #25 PostgreSQL Database            | (Cria Transferencia #16)                               |
| 1.3.4        | `enviarConviteTransferencia(...)`                                               | Operação Lógica                                 | :TransferService -> :NotificationService | RF47                     | #17 TransferService -> #23 NotificationService            | (Cria Notificacao #17)                                |
| 2            | `aceitarTransferencia(tokenTransferencia)`                                      | Operação Lógica                                 | :WebUI -> :GatewayService                | RF41                     | #1 SPA Principal -> #5 Gateway Service                     | (Aceita transferência)                                 |
| 2.1          | `verificarTokenValido(...)`                                                     | Operação Lógica                                 | :GatewayService -> :TransferService      | RF41                     | #5 Gateway Service -> #17 TransferService                  | (Valida token Transferencia #16)                        |
| 2.2          | `processarPagamentoTaxa(...)`                                                   | Operação Lógica                                 | :TransferService -> :PaymentOrchestrator | RF45                     | #17 TransferService -> #13 PaymentOrchestrator            | (Inicia Pagamento #12)                                 |
| 2.2.1        | `calcularTaxaTransferencia(...)`                                                | Operação Lógica                                 | :PaymentOrchestrator -> :TransferService | RF45                     | #13 PaymentOrchestrator -> #17 TransferService            | (Calcula taxa TransferPolicy #15)                       |
| 2.2.2        | `<<create>> criarPagamentoTaxa(...)`                                            | Operação Lógica                                 | :PaymentOrchestrator -> :BancoDeDados    | RF45                     | #13 PaymentOrchestrator -> #25 PostgreSQL Database        | (Cria Pagamento #12)                                   |
| 2.2.3        | `processarCobrancaPIX(...)`                                                     | Operação Lógica                                 | :PaymentOrchestrator -> :GatewayPagamento| RF45                     | #13 PaymentOrchestrator -> #29 Gateway de Pagamento       | (Integração externa)                                   |
| [pagOK] 3    | `concluirTransferencia(...)`                                                    | Operação Lógica                                 | :PaymentOrchestrator -> :TransferService | RF42                     | #13 PaymentOrchestrator -> #17 TransferService            | (Finaliza transferência)                               |
| 3.1          | `invalidarQROriginal(...)`                                                      | Operação Lógica                                 | :TransferService -> :TicketingService    | RF42                     | #17 TransferService -> #15 TicketingService               | (Invalida QrCode #14)                                  |
| 3.2          | `gerarNovoQR(...)`                                                              | Operação Lógica                                 | :TicketingService -> :QRSecurityService  | RF42                     | #15 TicketingService -> #16 QRSecurityService             | (Gera novo QrCode #14)                                 |
| 3.3          | `transferirIngressoParaDestinatario(...)`                                       | Operação Lógica                                 | :TransferService -> :BancoDeDados        | RF42                     | #17 TransferService -> #25 PostgreSQL Database            | (Atualiza Ingresso #13)                                |
| 3.4          | `atualizarStatusTransferencia('CONCLUIDA')`                                     | Operação Lógica                                 | :TransferService -> :BancoDeDados        | RF42                     | #17 TransferService -> #25 PostgreSQL Database            | (Atualiza Transferencia #16)                            |
| 4            | `notificarTransferenciaConcluida(...)`                                          | Operação Lógica                                 | :TransferService -> :NotificationService | RF47                     | #17 TransferService -> #23 NotificationService            | (Cria Notificacao #17)                                 |
| 5            | `exibirConfirmacaoTransferencia(...)`                                           | Operação Lógica                                 | :WebUI -> destinatario: Usuario          | RF42                     | #1 SPA Principal -> (Ator)                                | (Exibe dados da Transferencia #16)                      |

<b> Autor: </b> <a href="https://github.com/gabriel-lima258">Gabriel Lima</a>.

</details>

A figura 3 apresenta o diagrama de Comunicação do Cenário de Transferência de Ingresso

<div align="center">
    <b>Figura 3:</b> Diagrama de Comunicação – Transferência de Ingresso
    <br>
    <img src="assets/Modelagem/Dinamica/Comunicacao2.pdf" width="1000">
    <br>
    <b>Autor:</b> <a href="https://github.com/gabriel-lima258">Gabriel Lima</a>.
</div>

<p><strong>Observação:</strong> Caso deseje visualizar ou baixar em PDF, clique aqui: 
<a href="assets/Modelagem/Dinamica/Comunicacao2.pdf">PDF do Diagrama de Comunicação – Transferência de Ingresso</a></p>




## Conclusão

Em conclusão, os Diagramas de Comunicação elaborados para os cenários de **Compra de Ingresso** e **Transferência de Ingresso** forneceram uma visão detalhada e estrutural das interações entre os diversos componentes e objetos da plataforma Ingressou. Ao mapear os participantes, seus vínculos de comunicação e, crucialmente, a sequência numerada das mensagens trocadas – ao incorporar elementos avançados como criação de objetos, condições e iterações – estes diagramas elucidam como as diferentes partes do sistema colaboram para realizar funcionalidades chave, como a compra de ingressos com processamento de pagamento e a transferência segura de ingressos entre usuários com reemissão de QR Code.

## Bibliografia

<a name="ref1"></a>
[1] APOSTILA UML. Seção sobre representação de Diagrama de Colaboração. Disponibilizada pela professora. Acesso em: 1 maio 2025.

<a name="ref2"></a>
[2] IBM. Criando Diagramas de Comunicação. Disponível em: https://www.ibm.com/docs/pt-br/dmrt/9.5.0?topic=diagrams-creating-communication. Acesso em: 2 maio 2025.

<a name="ref3"></a>
[3] IBM. Diagramas de comunicação. Disponível em: https://www.ibm.com/docs/pt-br/radfws/9.6.0?topic=SSRTLW_9.6.0/com.ibm.xtools.sequence.doc/topics/ccommndiag.htm. Acesso em: 1 maio 2025.

<a name="ref4"></a>
[4] MICROSOFT. Criar um diagrama de comunicação UML. Disponível em: https://support.microsoft.com/pt-br/topic/criar-um-diagrama-de-comunica%C3%A7%C3%A3o-uml-911956f4-5f19-4a58-97a3-bb14110a5ed1. Acesso em: 1 maio 2025.

<a name="ref5"></a>
[5] MIRO. Guia: Diagramas de colaboração UML. Disponível em: https://miro.com/pt/diagrama/o-que-e-diagrama-colaboracao-uml/. Acesso em: 2 maio 2025.

<a name="ref6"></a>
[6] OLIVEIRA, George. Diagrama de Comunicação. [Vídeo]. YouTube. Disponível em: https://www.youtube.com/watch?v=6feefuR-iqI. Acesso em: 1 maio 2025.

## Histórico de versão

| Versão | Alteração | Responsável | Data |
| - | - | - | - |
| 1.0 | Adaptação completa do documento para o projeto Ingressou com cenários de compra e transferência de ingressos | Gabriel Lima | 29/10/2025 |
