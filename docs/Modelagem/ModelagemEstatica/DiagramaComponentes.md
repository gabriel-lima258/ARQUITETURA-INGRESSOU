# Diagrama de Componentes

> **Versão:** 1.0  
> **Data:** Outubro de 2025  
> **Autor:** Gabriel Lima  
> **Projeto:** Ingressou — Plataforma Web de Venda e Gestão de Ingressos  

---

## Sumário

- [Introdução](#introdução)  
- [Objetivos](#objetivos)  
- [Metodologia](#metodologia)  
- [Investigação dos Componentes Necessários](#investigação-dos-componentes-necessários)  
- [Diagrama de Componentes](#diagrama-de-componentes)  
- [Conclusão](#conclusão)  
- [Bibliografia](#bibliografia)  
- [Histórico de versão](#histórico-de-versão)  

## Introdução

Segundo a Apostila UML – Linguagem de Modelagem Unificada [1](#ref1) e o guia da [plataforma UML Diagrams](https://www.uml-diagrams.org/component-diagrams.html) [2](#ref2), um **componente** é uma unidade física de software (código-fonte, biblioteca, executável) que encapsula um conjunto de funcionalidades. Com base nisso, o **Diagrama de Componentes** representa visualmente esses módulos e suas dependências, e assim mostra quais artefatos (ex.: arquivos .jar, .dll, .py) são necessários para executar cada parte do sistema. No **Ingressou** — plataforma web para **venda e gestão de ingressos** — este diagrama torna explícitos módulos como **Interface Web, API Gateway/BFF, Catálogo (Eventos/Lotes), Cupons/Influenciadores, Checkout/Pedidos/Pagamentos (PIX/Cartão), Carteira & Ingressos (QR/Transferência), Check-in, Repasses/CashbackProdutor, Notificações**, além de **Infraestrutura** (PostgreSQL, Redis, Mensageria, S3) e **Integrações Externas** (Gateway de Pagamento, Antifraude, Validação de CPF, E-mail/WhatsApp).

## Objetivos

Tem em base o conceito de componentes e diagrama de componentes, busca-se os seguintes objetivos: 

- Apresentar com clareza os componentes físicos do Ingressou;
- Evidenciar interfaces providas e requeridas por cada módulo;
- Documentar dependências e artefatos para suportar implementação e deploy (CI/CD, infraestrutura);
- Servir de base para evolução do monólito modular para microserviços. 

## Metodologia

A metodologia adotada para a elaboração do Diagrama de Componentes do projeto **Ingressou** será estruturada em quatro etapas principais, com o objetivo de garantir consistência com os artefatos previamente desenvolvidos:

1. inicialmente será realizado o levantamento arquitetural, no qual serão identificados os módulos centrais do sistema a partir de:
    - [Rich Picture](Base/ArtefatoGeneralista/RichPicture.md)  elaborado na etapa inicial do projeto;
    - [Requisitos elicitados e documentados na primeira etapa](Base/ArtefatoGeneralista/RequisitosElicitados.md);
    - [Modelo HW2H (How, What, Why, How much)](Base/ArtefatoGeneralista/5W2H.md);
    - [Protótipo de alta fidelidade](Base/DesignSprint/Prototipo.md);
    - [Diagrama de Classes](/Modelagem/ModelagemEstatica/DiagramaClasses.md) construído na modelagem estática;

2. O diagrama será desenvolvido utilizando a plataforma Draw.io.
3. Será aplicada uma [verificação por meio de um checklist](https://unbarqdsw2025-1-turma02.github.io/2025.1_T02_G9_GalaxiaConectada_Entrega02/#/Modelagem/IniciativasExtras/Verificacao/VerificacaoDiagramaComponentes) de boas práticas de UML;, 


## Investigação dos Componentes Necessários

Antes da modelagem visual do Diagrama de Componentes na ferramenta Draw.io, foi realizada a identificação e a definição de todos os componentes chave e subsistemas que constituiriam a arquitetura da plataforma "**Ingressou**". Com isso, a Tabela 1 detalha os componentes identificados para a plataforma, especificando seus tipos, descrições, interfaces e dependências.

<strong>Tabela 1: Componentes e suas dependências.</strong>

**Observação:** Varios componentes foram pensados de acordo com os requisitos elicitados, então suas refeRências estão na coluna de observações.

**Tabela 1:** Componentes

### Tabela de Arquitetura de Componentes "Ingressou" 

| # | **Camada/Subsistema** | **Componente** | **Tipo** | **Descrição** | **Interfaces Providas** | **Interfaces Requeridas** | **Dependências** | **Requisitos Suportados** | **Artefato** |
|---|---|---|---|---|---|---|---|---|---|
| **CAMADA DE APRESENTAÇÃO** |
| 1 | **Frontend Web** | **SPA Principal** | Componente | Interface web responsiva para compradores (descoberta, compra, carteira, transferências) | `IWebAppUI` | `IGatewayAPI`, `IAuthAPI` | Gateway API, Auth Service | RF06-RF11, RF18, RF26, RF40-RF47 | `ingressou-web.js` |
| 2 | **Frontend Web** | **PWA Check-in** | Componente | Aplicativo PWA para validação de ingressos (online/offline) | `ICheckinUI` | `IGatewayAPI`, `ICheckinAPI` | Gateway API, Checkin Service | RF36-RF38, RNF08 | `checkin-pwa.js` |
| 3 | **Frontend Web** | **Painel Admin** | Componente | Interface administrativa para gestão completa do sistema | `IAdminUI` | `IGatewayAPI`, `IAdminAPI` | Gateway API, Admin Services | RF12, RF15-RF20, RF48-RF52 | `admin-panel.js` |
| 4 | **Frontend Web** | **Painel Produtor** | Componente | Interface de visualização (somente leitura) para produtores | `IProdutorUI` | `IGatewayAPI`, `IProducerAPI` | Gateway API, Producer Services | RF14 | `producer-panel.js` |
| **CAMADA DE APLICAÇÃO - GATEWAY** |
| 5 | **API Gateway** | **Gateway Service** | Componente | Ponto de entrada único, roteamento, autenticação JWT, rate limiting | `IGatewayAPI` | `IAuthService`, `IEventSearch`, `ICheckout`, `ITicketing`, `ICheckin`, `IAdminServices`, `IProducerDashboard` | Auth Service, Event Search, Checkout, Ticketing, Checkin, Admin, Producer Services | RNF02, RNF05 | `gateway-service.jar` |
| **CAMADA DE APLICAÇÃO - SUBSISTEMAS** |
| **SUBSISTEMA: GESTÃO DE IDENTIDADE (IAM)** |
| 6 | **IAM** | **AuthService** | Componente | Autenticação, autorização, sessões JWT, recuperação de senha | `IAuthService` | `IUsuarioRepository`, `ISocialProvider`, `INotificationService` | Usuario Repository, Social Provider, Notification Service | RF01-RF04, RNF05 | `auth-service.jar` |
| 7 | **IAM** | **ProfileService** | Componente | Gestão de perfis de usuário, dados pessoais, provedores sociais | `IProfileService` | `IUsuarioRepository` | Usuario Repository | RF05 | `profile-service.jar` |
| **SUBSISTEMA: CATÁLOGO & DESCOBERTA** |
| 8 | **Catálogo** | **EventSearchService** | Componente | Busca global, filtros (localização, categoria, data), ordenação | `IEventSearch` | `IEventoRepository`, `ICategoriaRepository`, `ILocalizacaoRepository`, `ICacheService` | Evento Repository, Categoria Repository, Localizacao Repository, Cache Service | RF06-RF11, RNF15, RNF16 | `catalog-service.jar` |
| **SUBSISTEMA: GESTÃO ADMINISTRATIVA** |
| 9 | **Admin** | **EventAdminService** | Componente | Criação, edição, publicação de eventos e lotes pelo Admin | `IAdminServices` | `IEventoRepository`, `ILoteRepository`, `ICategoriaRepository`, `IProdutorRepository` | Evento Repository, Lote Repository, Categoria Repository, Produtor Repository | RF15-RF17, RF19-RF20 | `admin-service.jar` |
| 10 | **Admin** | **ProducerOnboardingService** | Componente | Cadastro e KYC de produtores pelo Admin | `IProducerOnboarding` | `IProdutorRepository`, `IKYCService` | Produtor Repository, KYC Service | RF12-RF13 | `producer-onboarding.jar` |
| 11 | **Admin** | **CouponAdminService** | Componente | Gestão de cupons de influenciador | `ICouponAdmin` | `ICupomRepository` | Cupom Repository | RF31 | `coupon-admin.jar` |
| **SUBSISTEMA: PEDIDOS & PAGAMENTOS** |
| 12 | **Pedidos** | **CheckoutService** | Componente | Processo de checkout, aplicação de cupons, reserva de estoque | `ICheckout` | `IPedidoRepository`, `ILoteRepository`, `ICupomRepository`, `IPaymentOrchestrator` | Pedido Repository, Lote Repository, Cupom Repository, Payment Orchestrator | RF26, RF31, RF27 | `checkout-service.jar` |
| 13 | **Pedidos** | **PaymentOrchestrator** | Componente | Orquestração de pagamentos PIX e cartão, processamento de webhooks | `IPaymentOrchestrator` | `IGatewayPagamento`, `IMessageBus` | Gateway Pagamento, Message Bus | RF27-RF28, RNF14 | `payment-service.jar` |
| 14 | **Pedidos** | **OrderLifecycleManager** | Componente | Gestão do ciclo de vida dos pedidos (pago/cancelado), liberação de estoque | `IOrderEvents` | `IPedidoRepository`, `ILoteRepository`, `IMessageBus` | Pedido Repository, Lote Repository, Message Bus | RF29-RF30, RNF14 | `order-lifecycle.jar` |
| **SUBSISTEMA: INGRESSOS & TRANSFERÊNCIAS** |
| 15 | **Ingressos** | **TicketingService** | Componente | Emissão de ingressos e QR Codes assinados após confirmação de pagamento | `ITicketing` | `IIngressoRepository`, `IQRSecurityService`, `IMessageBus` | Ingresso Repository, QR Security Service, Message Bus | RF32, RF35, RNF06, RNF14 | `ticketing-service.jar` |
| 16 | **Ingressos** | **QRSecurityService** | Componente | Geração e validação de assinaturas digitais dos QR Codes | `IQRSecurityService` | *(Interno: Lib Criptográfica)* | --- | RNF06 | `qr-security.jar` |
| 17 | **Ingressos** | **TransferService** | Componente | Gestão de transferências de ingressos (iniciar, aceitar, reemitir, taxa) | `ITransferService` | `ITransferenciaRepository`, `IIngressoRepository`, `INotificationService`, `IPaymentOrchestrator` | Transferencia Repository, Ingresso Repository, Notification Service, Payment Orchestrator | RF40-RF47, RNF17 | `transfer-service.jar` |
| **SUBSISTEMA: CHECK-IN** |
| 18 | **Check-in** | **CheckinValidator** | Componente | Validação de QR Codes (válido/duplicado/expirado), registro de uso | `ICheckin` | `IIngressoRepository`, `ICheckinRegistroRepository`, `IQRSecurityService` | Ingresso Repository, Checkin Registro Repository, QR Security Service | RF33, RF36-RF37, RB10 | `checkin-validator.jar` |
| 19 | **Check-in** | **CheckinOfflineSync** | Componente | Sincronização de dados de check-in capturados offline | `IOfflineSync` | `IIngressoRepository`, `ICheckinRegistroRepository` | Ingresso Repository, Checkin Registro Repository | RF38 | `checkin-sync.jar` |
| **SUBSISTEMA: FINANÇAS & PRODUTOR** |
| 20 | **Finanças** | **ProducerDashboardService** | Componente | Agregação de dados para painel do produtor (vendas, check-ins, repasses, cashback) | `IProducerDashboard` | `IEventoRepository`, `ICheckinRegistroRepository`, `IRepasseRepository`, `ICashbackRepository` | Evento Repository, Checkin Registro Repository, Repasse Repository, Cashback Repository | RF14 | `producer-dashboard.jar` |
| 21 | **Finanças** | **CashbackService** | Componente | Cálculo e registro de cashback do produtor | `ICashbackService` | `IPagamentoRepository`, `ICashbackProdutorRepository`, `ICarteiraRepository` | Pagamento Repository, Cashback Produtor Repository, Carteira Repository | RB02 | `cashback-service.jar` |
| 22 | **Finanças** | **PayoutService** | Componente | Gestão de split de pagamento, repasses ao produtor, emissão de NFS-e | `IPayoutService` | `IRepasseRepository`, `ICarteiraRepository`, `IProdutorRepository`, `INFSeService` | Repasse Repository, Carteira Repository, Produtor Repository, NFS-e Service | RB07-RB08 | `payout-service.jar` |
| **SUBSISTEMA: COMUNICAÇÃO (CROSS-CUTTING)** |
| 23 | **Comunicação** | **NotificationService** | Componente | Envio de e-mails e WhatsApp de forma assíncrona | `INotificationService` | `IGatewayEmail`, `IGatewayWhatsApp`, `IMessageBus` | Gateway Email, Gateway WhatsApp, Message Bus | RF35, RF47, RNF14 | `notification-service.jar` |
| 24 | **Comunicação** | **AuditLogger** | Componente | Registro de trilhas de auditoria de operações críticas | `IAuditLog` | `IAuditRepository`, `IMessageBus` | Audit Repository, Message Bus | RF49 | `audit-service.jar` |
| **CAMADA DE INFRAESTRUTURA** |
| **SUBSISTEMA: PERSISTÊNCIA** |
| 25 | **Persistência** | **PostgreSQL Database** | Componente | Banco de dados principal para armazenamento relacional | `IDbConnection` | --- | --- | RNF10 | `postgres-db` |
| 26 | **Persistência** | **Data Access Layer** | Componente | Camada de abstração (Repository Pattern) para acesso aos dados | `IUsuarioRepository`, `IEventoRepository`, `ILoteRepository`, `ICategoriaRepository`, `ILocalizacaoRepository`, `IPedidoRepository`, `ICupomRepository`, `IPagamentoRepository`, `IIngressoRepository`, `ITransferenciaRepository`, `ICheckinRegistroRepository`, `IProdutorRepository`, `ICashbackProdutorRepository`, `IRepasseRepository`, `ICarteiraRepository`, `IAuditRepository` | `IDbConnection` | PostgreSQL Database | --- | `data-access.jar` |
| **SUBSISTEMA: MENSAGERIA** |
| 27 | **Mensageria** | **Message Broker** | Componente | Broker para comunicação assíncrona (RabbitMQ/SQS) | `IMessageBus` | --- | --- | RNF14 | `rabbitmq-broker` |
| **SUBSISTEMA: CACHE** |
| 28 | **Cache** | **Redis Cache** | Componente | Cache de alta velocidade para dados de catálogo e agregações | `ICacheService` | --- | --- | RNF15 | `redis-cache` |
| **SERVIÇOS EXTERNOS** |
| 29 | **Integrações** | **Gateway de Pagamento** | Componente | Processador externo para transações PIX e cartão (Pagar.me) | `IGatewayPagamento` | *(API Externa)* | --- | RF27-RF28 | `pagar-me-gateway` |
| 30 | **Integrações** | **Provedor Social** | Componente | Autenticação social (Google/Apple) | `ISocialProvider` | *(API Externa)* | --- | RF01 | `social-provider` |
| 31 | **Integrações** | **KYC Service** | Componente | Validação de documentos (CNPJ/CPF) | `IKYCService` | *(API Externa)* | --- | RF13 | `kyc-service` |
| 32 | **Integrações** | **NFS-e Service** | Componente | Emissão de Nota Fiscal de Serviço | `INFSeService` | *(API Externa)* | --- | RB08 | `nfse-service` |
| 33 | **Integrações** | **Gateway de E-mail** | Componente | Entrega de e-mails transacionais (SendGrid) | `IGatewayEmail` | *(API Externa)* | --- | RF35 | `email-gateway` |
| 34 | **Integrações** | **Gateway de WhatsApp** | Componente | Envio de notificações via WhatsApp | `IGatewayWhatsApp` | *(API Externa)* | --- | RF35 | `whatsapp-gateway` |
| 35 | **Componente** | **ServicoMonitoramento** | Componente | Coleta dados de uso, erros, saúde da aplicação para análise. | `IMonitoramento` | --- | --- | --- | --- |
| 36 | **Componente** | **GestorAssetsS3** | Componente | Armazena e entrega arquivos estáticos (CSS, JS, Imagens, sitemaps, robots.txt). | `IAssetDelivery` | Acesso a Artefato static-files/, Acesso a Artefato generated-seo-files/ | Artefato static-files/, Artefato generated-seo-files/ | --- | --- |
| 37 | **Artefato** | **<<artifact>> generated-seo-files/** | Artefato | Representa o local físico onde os arquivos estáticos residem. | --- | --- | --- | --- | --- |
| 38 | **Artefato** | **<<artifact>> static-files/** | Artefato | Local para arquivos gerados relacionados a SEO (sitemap.xml, etc.). | --- | --- | --- | --- | --- |


<div align="center">
    <br>
    <b>Autor:</b> <a href="https://github.com/gabriel-lima258">Gabriel Lima</a>.
    <br>
</div>


Além disso, a Tabela 1, apresentada acima, desempenha um outro papel fundamental: além de catalogar formalmente cada componente com seu tipo, nome, descrição, interfaces providas e requeridas, e observações, ela também detalha suas dependências. Assim, serve como um guia complementar para facilitar a leitura e a compreensão precisa da estrutura e das conexões representadas no diagrama.

---

## Diagrama de Componentes

Para melhor compreensão do diagrama, a figura 1 mostra a legenda;

<div align="center">
    <b>Figura 1:</b> Legenda do Diagrama de Componentes  
    <br>
    <img src="https://raw.githubusercontent.com/UnBArqDsw2025-1-Turma02/2025.1_T02_G9_GalaxiaConectada_Entrega02/refs/heads/main/docs/Modelagem/Imagens/LegendaDiagramaComponentes.png" width="500">
    <br>
    <b>Autor:</b> <a href="https://github.com/gabriel-lima258">Gabriel Lima</a>.
</div>

<p>
Para facilitar a leitura e a compreensão da estrutura do sistema, o diagrama de componentes será apresentado em três partes: inicialmente, o componentes — Camada de Frontedn da **Ingressou**; em seguida, o pacote do backend, o pacote de infra e serviços externos; e, por fim, o diagrama completo que reúne ambos os pacotes em uma visão unificada.
</p>

---

<div align="center">
    <b>Figura 1:</b> Diagrama de Componentes Completo  
    <br>
    <img src="assets/Modelagem/Estatica/componentes.pdf" width="1000">
    <br>
    <b>Autor:</b> <a href="https://github.com/gabriel-lima258">Gabriel Lima</a>.
</div>

<p><strong>Observação:</strong> Caso deseje visualizar ou baixar em PDF, clique aqui: 
<a href="assets/Modelagem/Estatica/componentes.pdf">PDF do Diagrama Completo</a></p>


## Conclusão

O Diagrama de Componentes do Ingressou evidencia, de forma prática, quem fornece o quê (interfaces/artefatos) e quem depende de quem (requisições, eventos), facilitando deploy, observabilidade e uma evolução segura do monólito modular para serviços independentes quando necessário (ex.: extrair Pagamentos e Checkin).

## Bibliografia

<a name="ref1"></a>  
[1]APOSTILA UML. *Linguagem de Modelagem Unificada*. Disponibilizado pela professora. Acesso em: 25 abr. 2025.  

<a name="ref2"></a>  
[2]UML DIAGRAMS. *Component Diagrams Overview*. Disponível em: https://www.uml-diagrams.org/component-diagrams.html. Acesso em: 25 abr. 2025. 

<a name="ref3"></a>  
[3] IBM CORPORATION. *Component diagrams*. IBM Documentation, 2023. Disponível em: https://www.ibm.com/docs/en/dmrt/9.5.0?topic=diagrams-component. Acesso em: 25 abr. 2025.  

<a name="ref4"></a>  
[4] LUCID SOFTWARE INC. *UML Component Diagram*. Lucidchart, 2024. Disponível em: https://www.lucidchart.com/pages/uml-component-diagram. Acesso em: 25 abr. 2025.

<a name="ref5"></a>  
[5] VISUAL PARADIGM INTERNATIONAL. *UML Component Diagram Guide*. Visual Paradigm, 2024. Disponível em: https://www.visual-paradigm.com/guide/uml-unified-modeling-language/uml-component-diagram/. Acesso em: 25 abr. 2025.  

<a name="ref6"></a>
[6] IBM CORPORATION. Diagrama de componentes. IBM Documentation. Disponível em: https://www.ibm.com/docs/pt-br/rsas/7.5.0?topic=services-component-diagrams. Acesso em: 27 abr. 2025.

<a name="ref7"></a>
[7] LUCID SOFTWARE INC. Diagrama de componentes UML. Lucidchart. Disponível em: https://www.lucidchart.com/pages/pt/diagrama-de-componentes-uml. Acesso em: 27 abr. 2025.

<a name="ref8"></a>
[8] CREATELY. Tutorial de Diagrama de Componentes UML. Disponível em: https://creately.com/blog/pt/diagrama/tutorial-de-diagrama-de-componentes-2/. Acesso em: 27 abr. 2025.

## Histórico de versão

| Versão | Alteração | Responsável | Data |
| - | - | - | - |
| 1.0 | Adaptação do documento para o projeto Ingressou (componentes, interfaces, PlantUML)| Gabriel Lima | 19/10/2025 |