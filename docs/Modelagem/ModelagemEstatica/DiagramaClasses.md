# Diagrama de Classes — Projeto Ingressou (MVP)

> **Versão:** 1.0  
> **Data:** Outubro de 2025  
> **Autor:** Gabriel Lima  
> **Projeto:** Ingressou — Plataforma Web de Venda e Gestão de Ingressos  

---

## Sumário

- [Introdução](#introdução)
- [Objetivos](#objetivos)
- [Metodologia](#metodologia)
- [Investigação das Classes Necessárias](#investigação-das-classes-necessárias)
- [Os Tipos de Relacionamentos](#os-tipos-de-relacionamentos)
- [Diagrama de Classes](#diagrama-de-classes)
- [Conclusão](#conclusão)
- [Bibliografia](#bibliografia)
- [Histórico de Versão](#histórico-de-versão)

---

## Introdução

O **Diagrama de Classes** é um dos principais artefatos da UML e tem como objetivo estruturar o sistema de forma estática, descrevendo suas **entidades (classes)**, seus **atributos e métodos** e os **relacionamentos** entre elas.  

No contexto do **Ingressou — Plataforma Web de Venda e Gestão de Ingressos**, o diagrama de classes representa a estrutura lógica do MVP, incluindo as principais entidades responsáveis por suportar o ciclo completo de compra, gestão e transferência de ingressos digitais.  

Essa modelagem serve como base para o design das APIs, persistência de dados e lógica de negócios, permitindo uma visão clara da arquitetura do software e dos papéis de cada componente.

---

## Objetivos

Os principais objetivos deste artefato são:

- Representar de forma visual e estruturada a arquitetura lógica do **MVP do Ingressou**.  
- Mapear as classes essenciais que sustentam as funcionalidades de **venda, compra e transferência de ingressos**.  
- Facilitar a comunicação entre desenvolvedores, analistas e stakeholders.  
- Servir como **documentação base** para o desenvolvimento e futuras expansões do sistema.

---

## Metodologia

1. O diagrama foi elaborado com base na **versão 1.5 dos Requisitos Elicitados do Ingressou (Outubro de 2025)**, que incorpora todos os requisitos funcionais, não funcionais (incluindo acessibilidade) e regras de negócio do MVP.
2. As classes foram identificadas através de **análise criteriosa dos 18 casos de uso** (CU-01 a CU-18) e **52 requisitos funcionais** (RF01 a RF52), mapeando:
   - Cadastro e autenticação de usuários com RBAC (clientes, produtores, admin, staff)
   - Onboarding e vinculação de produtores a eventos
   - Criação e gestão de eventos com categorização e localização
   - Busca e filtros nacionais (cidade/UF/categoria/data)
   - Gestão de lotes com encerramento por tempo ou quantidade
   - Compra de ingressos com pagamentos PIX/Cartão e aplicação de cupons
   - Transferência de ingressos com aceite e reemissão de QR Code
   - Validação de check-in (online/offline)
   - Sistema de notificações assíncronas e auditoria completa
3. A modelagem seguiu as normas da **UML 2.0**, priorizando:
   - **Alta coesão**: cada classe tem responsabilidade única e bem definida
   - **Baixo acoplamento**: relacionamentos claros sem dependências desnecessárias
   - **Rastreabilidade**: todos os relacionamentos são justificados por requisitos específicos
4. Os tipos de relacionamento (Associação, Agregação, Composição, Dependência) foram aplicados conforme a **semântica do domínio** e **ciclo de vida das entidades**.
5. A estrutura foi validada para suportar todos os fluxos principais, alternativos e de exceção descritos nos casos de uso.

---

## Investigação das Classes Necessárias

A tabela abaixo apresenta as principais classes do sistema **Ingressou (MVP)**, seus atributos e métodos essenciais.

<strong>Tabela 1: Classes do Sistema.</strong>

| # | Classe | Responsabilidade | Atributos (principais) | Métodos (principais) |
|---|---|---|---|---|
| 1 | **User** | Representar usuários do sistema (Cliente, Produtor, Admin, Staff) com autenticação e controle de acesso baseado em papéis (RBAC). | - id: UUID<br>- name: String<br>- email: String (unique)<br>- cpf: String (unique)<br>- passwordHash: String<br>- phone: String<br>- role: UserRole (enum)<br>- emailVerified: Boolean<br>- isActive: Boolean<br>- socialProviders: List\<SocialProvider\><br>- createdAt: DateTime<br>- updatedAt: DateTime | + register(): Boolean<br>+ login(email, password): Token<br>+ logout(): void<br>+ verifyEmail(otp): Boolean<br>+ resetPassword(token, newPassword): Boolean<br>+ updateProfile(data): Boolean<br>+ linkSocialProvider(provider): Boolean<br>+ unlinkSocialProvider(provider): Boolean<br>+ hasRole(role): Boolean |
| 2 | **Producer** | Representar produtores de eventos com dados de KYC e informações bancárias para recebimento de repasses e cashback. | - id: UUID<br>- userId: UUID (FK)<br>- legalName: String<br>- cnpj: String (nullable)<br>- cpf: String<br>- pixKey: String<br>- bankAccount: String<br>- isVerified: Boolean<br>- kycStatus: String<br>- cashbackBalance: Decimal<br>- contractUrl: String<br>- createdAt: DateTime<br>- updatedAt: DateTime | + onboard(data): Boolean<br>+ verifyKYC(): Boolean<br>+ updateBankingInfo(data): Boolean<br>+ calculateCashback(eventId): Decimal<br>+ exportReport(filters): File<br>+ getLinkedEvents(): List\<Event\><br>+ getCashbackBalance(): Decimal |
| 3 | **Event** | Gerenciar eventos criados exclusivamente pelo Admin, com categorias, datas e controle de publicação. | - id: UUID<br>- name: String<br>- slug: String (unique)<br>- description: Text<br>- bannerUrl: String<br>- locationId: UUID (FK, nullable)<br>- startDate: DateTime<br>- endDate: DateTime<br>- status: EventStatus (enum)<br>- isOnline: Boolean<br>- onlineUrl: String (nullable)<br>- allowTransfers: Boolean<br>- transferWindowHours: Integer<br>- transferFeePercent: Decimal<br>- publishedAt: DateTime<br>- createdBy: UUID (FK User/Admin)<br>- createdAt: DateTime<br>- updatedAt: DateTime | + create(data): Event<br>+ update(data): Boolean<br>+ publish(): Boolean<br>+ cancel(): Boolean<br>+ linkProducer(producerId): Boolean<br>+ unlinkProducer(producerId): Boolean<br>+ addCategory(categoryId): Boolean<br>+ removeCategory(categoryId): Boolean<br>+ setLocation(locationId): Boolean<br>+ canPublish(): Boolean<br>+ isActive(): Boolean<br>+ canTransfer(): Boolean |
| 4 | **Location** | Representar locais físicos onde eventos ocorrem, permitindo reutilização de venues e enriquecimento de dados geográficos. | - id: UUID<br>- venueName: String<br>- address: String<br>- complement: String (nullable)<br>- postalCode: String<br>- city: String<br>- state: String (UF)<br>- country: String<br>- latitude: Decimal (nullable)<br>- longitude: Decimal (nullable)<br>- capacity: Integer (nullable)<br>- accessibility: Text (nullable)<br>- photoUrl: String (nullable)<br>- isActive: Boolean<br>- createdAt: DateTime<br>- updatedAt: DateTime | + create(data): Location<br>+ update(data): Boolean<br>+ setCoordinates(lat, lng): void<br>+ getEventsByLocation(): List\<Event\><br>+ calculateDistance(otherLocation): Decimal<br>+ deactivate(): Boolean<br>+ canDelete(): Boolean |
| 5 | **Category** | Representar taxonomia oficial de categorias de eventos mantida pelo Admin para filtros e organização. | - id: UUID<br>- name: String<br>- slug: String (unique)<br>- icon: String (nullable)<br>- description: Text<br>- isActive: Boolean<br>- createdAt: DateTime<br>- updatedAt: DateTime | + create(name, slug): Category<br>+ update(data): Boolean<br>+ deactivate(): Boolean<br>+ canDelete(): Boolean<br>+ getEvents(): List\<Event\> |
| 6 | **Batch** | Gerenciar lotes de ingressos com controle de preço, quantidade e janela de venda, encerrando por tempo ou quantidade. | - id: UUID<br>- eventId: UUID (FK)<br>- name: String<br>- price: Decimal<br>- totalQuantity: Integer<br>- soldQuantity: Integer<br>- availableQuantity: Integer<br>- salesStartDate: DateTime<br>- salesEndDate: DateTime<br>- status: BatchStatus (enum)<br>- createdAt: DateTime<br>- updatedAt: DateTime | + create(data): Batch<br>+ update(data): Boolean<br>+ reserveTickets(quantity): Boolean<br>+ releaseReservation(quantity): void<br>+ incrementSold(quantity): void<br>+ checkAvailability(quantity): Boolean<br>+ autoClose(): void<br>+ isActive(): Boolean<br>+ isSoldOut(): Boolean |
| 7 | **Ticket** | Representar ingresso digital com QR Code assinado, controle de uso e suporte a transferências. | - id: UUID<br>- orderId: UUID (FK)<br>- batchId: UUID (FK)<br>- eventId: UUID (FK)<br>- ownerId: UUID (FK User)<br>- originalBuyerId: UUID (FK User)<br>- ticketType: TicketType (enum)<br>- status: TicketStatus (enum)<br>- qrCode: String (unique)<br>- qrSignature: String<br>- price: Decimal<br>- isHalfPrice: Boolean<br>- isTransferable: Boolean<br>- validatedAt: DateTime<br>- createdAt: DateTime<br>- updatedAt: DateTime | + generate(orderData): Ticket<br>+ generateQRCode(): String<br>+ validateQRSignature(): Boolean<br>+ transfer(newOwnerId): Boolean<br>+ invalidateQR(): void<br>+ reissueQR(): String<br>+ validate(): Boolean<br>+ resendByEmail(): Boolean<br>+ canTransfer(): Boolean<br>+ isValid(): Boolean |
| 8 | **Order** | Gerenciar pedidos de compra com itens, pagamentos e ciclo de vida completo. | - id: UUID<br>- userId: UUID (FK)<br>- eventId: UUID (FK)<br>- totalAmount: Decimal<br>- discountAmount: Decimal<br>- netAmount: Decimal<br>- platformFee: Decimal<br>- status: OrderStatus (enum)<br>- couponId: UUID (FK, nullable)<br>- expiresAt: DateTime<br>- confirmedAt: DateTime<br>- cancelledAt: DateTime<br>- createdAt: DateTime<br>- updatedAt: DateTime | + create(cartData): Order<br>+ addItem(batchId, quantity, type): Boolean<br>+ applyCoupon(couponCode): Boolean<br>+ removeCoupon(): void<br>+ calculateTotal(): Decimal<br>+ confirm(): Boolean<br>+ cancel(): Boolean<br>+ expire(): void<br>+ generateTickets(): List\<Ticket\><br>+ canCancel(): Boolean |
| 9 | **OrderItem** | Detalhar itens individuais de um pedido (lotes, quantidades e tipos de ingresso). | - id: UUID<br>- orderId: UUID (FK)<br>- batchId: UUID (FK)<br>- ticketType: TicketType (enum)<br>- quantity: Integer<br>- unitPrice: Decimal<br>- subtotal: Decimal<br>- createdAt: DateTime | + calculateSubtotal(): Decimal<br>+ getTicketType(): TicketType |
| 10 | **Payment** | Processar pagamentos via PIX/Cartão com integração a gateways e controle de status. | - id: UUID<br>- orderId: UUID (FK)<br>- method: PaymentMethod (enum)<br>- status: PaymentStatus (enum)<br>- amount: Decimal<br>- gatewayTransactionId: String<br>- pixQrCode: String (nullable)<br>- pixExpiresAt: DateTime (nullable)<br>- gatewayResponse: JSON<br>- paidAt: DateTime<br>- refundedAt: DateTime<br>- createdAt: DateTime<br>- updatedAt: DateTime | + initiate(method, amount): Payment<br>+ generatePixQR(): String<br>+ processWebhook(data): Boolean<br>+ confirm(): Boolean<br>+ fail(): void<br>+ refund(): Boolean<br>+ expire(): void<br>+ isApproved(): Boolean<br>+ isPending(): Boolean |
| 11 | **Coupon** | Gerenciar cupons de influenciadores com descontos, vigência e limites de uso. | - id: UUID<br>- code: String (unique)<br>- eventId: UUID (FK, nullable)<br>- influencerId: UUID (FK User, nullable)<br>- discountType: String (PERCENT/FIXED)<br>- discountValue: Decimal<br>- usageLimit: Integer<br>- usageCount: Integer<br>- validFrom: DateTime<br>- validUntil: DateTime<br>- isActive: Boolean<br>- createdAt: DateTime<br>- updatedAt: DateTime | + create(data): Coupon<br>+ validate(eventId): Boolean<br>+ apply(orderAmount): Decimal<br>+ incrementUsage(): void<br>+ deactivate(): void<br>+ canUse(): Boolean<br>+ isExpired(): Boolean<br>+ getUsageRemaining(): Integer |
| 12 | **Transfer** | Gerenciar transferências de ingressos com aceite do destinatário e reemissão de QR Code. | - id: UUID<br>- ticketId: UUID (FK)<br>- senderId: UUID (FK User)<br>- recipientId: UUID (FK User)<br>- recipientEmail: String<br>- recipientCpf: String<br>- status: TransferStatus (enum)<br>- feeAmount: Decimal<br>- feePaymentId: UUID (FK Payment, nullable)<br>- acceptToken: String (unique)<br>- tokenExpiresAt: DateTime<br>- acceptedAt: DateTime<br>- cancelledAt: DateTime<br>- createdAt: DateTime<br>- updatedAt: DateTime | + initiate(ticketId, recipient): Transfer<br>+ calculateFee(): Decimal<br>+ sendInvitation(): Boolean<br>+ accept(token): Boolean<br>+ refuse(): Boolean<br>+ cancel(): Boolean<br>+ expire(): void<br>+ reissueTicketQR(): Boolean<br>+ canAccept(): Boolean<br>+ isExpired(): Boolean |
| 13 | **CheckIn** | Registrar validações de ingressos no evento (online/offline) com auditoria completa. | - id: UUID<br>- ticketId: UUID (FK)<br>- eventId: UUID (FK)<br>- operatorId: UUID (FK User/Staff)<br>- status: CheckInStatus (enum)<br>- deviceId: String<br>- ipAddress: String<br>- location: String<br>- validatedAt: DateTime<br>- syncedAt: DateTime (nullable)<br>- isOffline: Boolean<br>- createdAt: DateTime | + validate(qrCode): CheckIn<br>+ sync(): Boolean<br>+ getHistory(ticketId): List\<CheckIn\><br>+ exportReport(filters): File |
| 14 | **QRCode** | Gerenciar QR Codes assinados digitalmente com validação antifraude. | - id: UUID<br>- ticketId: UUID (FK)<br>- content: String<br>- signature: String<br>- algorithm: String<br>- isValid: Boolean<br>- invalidatedAt: DateTime<br>- createdAt: DateTime | + generate(ticketData): QRCode<br>+ sign(privateKey): String<br>+ verify(publicKey): Boolean<br>+ invalidate(): void<br>+ regenerate(): QRCode |
| 15 | **Wallet** | Representar carteira digital do usuário contendo todos os ingressos ativos. | - id: UUID<br>- userId: UUID (FK)<br>- createdAt: DateTime<br>- updatedAt: DateTime | + getActiveTickets(): List\<Ticket\><br>+ getTicketsByEvent(eventId): List\<Ticket\><br>+ getPastTickets(): List\<Ticket\><br>+ getTransferableTickets(): List\<Ticket\> |
| 16 | **Notification** | Gerenciar envio de notificações por e-mail/WhatsApp de forma assíncrona. | - id: UUID<br>- userId: UUID (FK)<br>- type: NotificationType (enum)<br>- channel: String (EMAIL/WHATSAPP)<br>- subject: String<br>- content: Text<br>- metadata: JSON<br>- status: String<br>- sentAt: DateTime<br>- readAt: DateTime<br>- createdAt: DateTime | + send(userId, type, data): Notification<br>+ retry(): Boolean<br>+ markAsRead(): void<br>+ getUnread(userId): List\<Notification\> |
| 17 | **AuditLog** | Registrar trilha de auditoria completa de todas as ações críticas do sistema. | - id: UUID<br>- userId: UUID (FK)<br>- action: String<br>- entityType: String<br>- entityId: UUID<br>- oldValue: JSON<br>- newValue: JSON<br>- ipAddress: String<br>- userAgent: String<br>- createdAt: DateTime | + log(action, entity, data): AuditLog<br>+ query(filters): List\<AuditLog\><br>+ export(filters): File |
| 18 | **EventProducer** | Representar vinculação N:N entre Eventos e Produtores (tabela associativa). | - id: UUID<br>- eventId: UUID (FK)<br>- producerId: UUID (FK)<br>- linkedAt: DateTime<br>- linkedBy: UUID (FK User/Admin) | + link(eventId, producerId): Boolean<br>+ unlink(): void |
| 19 | **EventCategory** | Representar vinculação N:N entre Eventos e Categorias (tabela associativa). | - id: UUID<br>- eventId: UUID (FK)<br>- categoryId: UUID (FK)<br>- createdAt: DateTime | + assign(eventId, categoryId): Boolean<br>+ remove(): void |

---

## Tabela de Enums e Tipos

<strong>Tabela 1.1: Enumerações do Sistema.</strong>

| # | Enum | Valores | Descrição |
|---|---|---|---|
| 1 | **UserRole** | CUSTOMER, PRODUCER, ADMIN, STAFF | Papéis de usuário no sistema (RBAC) |
| 2 | **EventStatus** | DRAFT, PUBLISHED, CANCELLED, FINISHED | Status do ciclo de vida do evento |
| 3 | **BatchStatus** | SCHEDULED, ACTIVE, SOLD_OUT, EXPIRED, CANCELLED | Status do lote de ingressos |
| 4 | **TicketType** | FULL, HALF, VIP, COURTESY | Tipos de ingresso disponíveis |
| 5 | **TicketStatus** | ACTIVE, TRANSFERRED, VALIDATED, CANCELLED, EXPIRED | Status do ingresso |
| 6 | **OrderStatus** | PENDING, AWAITING_PAYMENT, PAID, CANCELLED, EXPIRED, REFUNDED | Status do pedido |
| 7 | **PaymentMethod** | PIX, CREDIT_CARD, DEBIT_CARD | Métodos de pagamento aceitos |
| 8 | **PaymentStatus** | PENDING, PROCESSING, APPROVED, REFUSED, CANCELLED, REFUNDED, EXPIRED | Status do pagamento |
| 9 | **TransferStatus** | PENDING, ACCEPTED, REFUSED, CANCELLED, EXPIRED, COMPLETED | Status da transferência de ingresso |
| 10 | **CheckInStatus** | VALID, ALREADY_USED, INVALID, EXPIRED, FRAUD_ATTEMPT | Status da validação de check-in |
| 11 | **NotificationType** | ORDER_CONFIRMED, TICKET_ISSUED, TRANSFER_INVITED, TRANSFER_ACCEPTED, TRANSFER_CANCELLED, CHECKIN_SUCCESS, PASSWORD_RESET, EMAIL_VERIFICATION | Tipos de notificações |



---

## Os Tipos de Relacionamentos

**Tabela 2:** Tipos de relacionamentos entre as classes do sistema Ingressou.

| Tipo | Semântica | Notação UML | Exemplos |
|---|---|---|---|
| **Associação Simples** | Relacionamento estrutural entre classes onde uma classe conhece e usa outra, mas ambas têm ciclos de vida independentes. | Linha sólida →<br>Pode ter multiplicidade (1..1, 1..*, 0..*, etc.) | `User → Wallet`<br>`Order → Payment`<br>`Ticket → QRCode` |
| **Agregação** | Tipo especial de associação que representa um relacionamento "todo-parte" onde as partes podem existir independentemente do todo. | Linha sólida com losango vazio no lado do "todo" ◇→ | `Event ◇→ Batch`<br>Evento contém lotes, mas lotes podem existir temporariamente sem evento |
| **Composição** | Relacionamento "todo-parte" forte onde as partes não podem existir sem o todo. Quando o todo é destruído, as partes também são. | Linha sólida com losango preenchido no lado do "todo" ◆→ | `Order ◆→ OrderItem`<br>`Ticket ◆→ QRCode`<br>Se o pedido é deletado, os itens também são |
| **Generalização (Herança)** | Relacionamento de especialização onde uma classe filha herda atributos e métodos de uma classe pai. | Linha sólida com triângulo vazio apontando para a classe pai △→ | Não aplicável no MVP<br>(Futuro: `PaymentMethod` especializações) |
| **Dependência** | Relacionamento mais fraco onde uma classe usa outra temporariamente (parâmetro de método, variável local), sem manter referência permanente. | Linha tracejada com seta → | `CheckIn ⤏ QRCode` (usa para validar)<br>`Order ⤏ Coupon` (usa para calcular desconto) |
| **Associação N:N** | Relacionamento muitos-para-muitos entre classes, geralmente representado por uma classe associativa intermediária. | Linha sólida com multiplicidade * em ambos os lados, ou classe intermediária | `Event ←→ Producer` (via EventProducer)<br>`Event ←→ Category` (via EventCategory) |
| **Auto-associação** | Relacionamento de uma classe consigo mesma, útil para hierarquias ou relações reflexivas. | Linha que sai e volta para a mesma classe | `User → User` (remetente/destinatário em Transfer) |



---

## Os Relacionamentos no Diagrama de Classes

Além da definição individual de cada classe, a representação de como elas se interconectam é um aspecto vital do Diagrama de Classes, uma vez que ilustra a dinâmica e as dependências estruturais do sistema. Dessa maneira, para elucidar a natureza e as implicações de cada tipo de ligação (como Associação, Agregação, Composição, Generalização e Dependência) utilizada no diagrama visual, elaborou-se também a tabela 3 específica para os relacionamentos. Esta tabela 3 auxiliar tem o objetivo de detalhar mostra os relacionamentos de cada uma das classes da tabela 1.

**Tabela 3:** Relacionamentos entre as classes do sistema Ingressou.

| # | Classe Origem | Relacionamento | Classe Destino | Tipo | Multiplicidade | Descrição | Justificativa (Requisitos) |
|---|---|---|---|---|---|---|---|
| 1 | **User** | possui | **Wallet** | Composição | 1..1 → 1..1 | Todo usuário possui uma carteira digital onde seus ingressos são armazenados. A carteira é criada junto com o usuário e destruída com ele. | RF20, CU-01 - Acesso aos ingressos adquiridos |
| 2 | **User** | realiza | **Order** | Associação | 1..1 → 0..* | Usuário pode realizar múltiplos pedidos ao longo do tempo. | RF26-RF30, CU-01 - Compra de ingressos |
| 3 | **User** | recebe | **Notification** | Associação | 1..1 → 0..* | Usuário recebe notificações sobre ações no sistema (pedidos, transferências, check-in). | RF35, RF47, RNF14 |
| 4 | **User** | gera | **AuditLog** | Dependência | 1..1 → 0..* | Todas as ações críticas do usuário são registradas em log de auditoria. | RF49, RB14 |
| 5 | **User** | cria (Admin) | **Event** | Associação | 1..1 → 0..* | Apenas usuários com papel ADMIN podem criar eventos. | RF15, RB13, CU-11 |
| 6 | **User** | opera | **CheckIn** | Associação | 1..1 (Staff) → 0..* | Usuários com papel STAFF realizam validações de check-in. | RF36-RF39, CU-02 |
| 7 | **Producer** | estende | **User** | Associação | 1..1 → 1..1 | Producer é um perfil especializado vinculado a um User com papel PRODUCER. | RF12-RF14, CU-09, CU-10 |
| 8 | **Producer** | vincula-se a | **Event** | Associação N:N (via EventProducer) | 0..* ←→ 0..* | Produtores são vinculados a eventos pelo Admin para ter acesso de leitura no painel. | RF19, RB14, CU-13 |
| 9 | **Event** | ocorre em | **Location** | Associação | 0..* → 0..1 | Evento pode ter uma localização física (venue) ou ser online (locationId nullable). Permite reutilização de locais. | RF07, RF15, RF18, RB17, CU-07, CU-08 |
| 10 | **Event** | contém | **Batch** | Agregação | 1..1 → 1..* | Evento possui um ou mais lotes de ingressos. Lotes podem ser gerenciados independentemente. | RF21-RF23, RB11, CU-15 |
| 11 | **Event** | pertence a | **Category** | Associação N:N (via EventCategory) | 1..* ←→ 0..* | Eventos devem ter ao menos uma categoria. Categorias podem ter múltiplos eventos. | RF08, RF20, RB16, CU-07 |
| 12 | **Event** | gera | **Ticket** | Associação | 1..1 → 0..* | Cada ingresso está vinculado a um evento específico. | RF32-RF35, CU-01 |
| 13 | **Event** | permite | **Coupon** | Associação | 0..1 ← 0..* | Cupons podem ser aplicados a eventos específicos ou serem globais. | RF31, RB12, CU-16 |
| 14 | **Event** | registra | **CheckIn** | Associação | 1..1 → 0..* | Check-ins são registrados por evento para controle de entradas. | RF36-RF39, CU-02 |
| 15 | **Location** | hospeda | **Event** | Associação | 0..1 → 0..* | Um local pode hospedar múltiplos eventos ao longo do tempo. Facilita busca por venue. | RF07, RF18, CU-07 |
| 16 | **Category** | classifica | **Event** | Associação N:N (via EventCategory) | 0..* ←→ 1..* | Categorias organizam e classificam eventos para busca e filtros. | RF08, RF52, CU-07 |
| 17 | **Batch** | pertence a | **Event** | Agregação | 1..* → 1..1 | Lote sempre pertence a um evento. | RF21, CU-15 |
| 18 | **Batch** | gera | **Ticket** | Associação | 1..1 → 0..* | Ingressos são gerados a partir de lotes específicos. | RF21-RF23, CU-01 |
| 19 | **Batch** | compõe | **OrderItem** | Associação | 1..1 → 0..* | Itens de pedido referenciam lotes específicos. | CU-01 |
| 20 | **Order** | é feito por | **User** | Associação | 0..* → 1..1 | Pedido sempre pertence a um usuário. | RF26, CU-01 |
| 21 | **Order** | refere-se a | **Event** | Associação | 0..* → 1..1 | Pedido sempre está relacionado a um evento específico. | RF26, CU-01 |
| 22 | **Order** | contém | **OrderItem** | Composição | 1..1 → 1..* | Pedido é composto por um ou mais itens. Itens não existem sem o pedido. | RF26, CU-01 |
| 23 | **Order** | possui | **Payment** | Composição | 1..1 → 1..1 | Cada pedido possui um pagamento associado. | RF27-RF30, CU-01 |
| 24 | **Order** | aplica | **Coupon** | Dependência | 0..* → 0..1 | Pedido pode aplicar um cupom de desconto. | RF31, RB12, CU-16 |
| 25 | **Order** | gera | **Ticket** | Associação | 1..1 → 1..* | Após confirmação do pagamento, o pedido gera os ingressos. | RF29, RF32, CU-01 |
| 26 | **OrderItem** | pertence a | **Order** | Composição | 1..* → 1..1 | Item sempre pertence a um pedido. | RF26, CU-01 |
| 27 | **OrderItem** | referencia | **Batch** | Associação | 0..* → 1..1 | Item referencia um lote específico do evento. | RF26, CU-01 |
| 28 | **Payment** | processa | **Order** | Composição | 1..1 → 1..1 | Pagamento está fortemente acoplado ao pedido. | RF27-RF30, CU-01 |
| 29 | **Payment** | cobra taxa | **Transfer** | Associação | 0..1 ← 0..1 | Transferência pode ter um pagamento associado para taxa. | RF45, RF46, CU-14 |
| 30 | **Ticket** | pertence a | **Order** | Associação | 0..* → 1..1 | Ingresso é gerado a partir de um pedido confirmado. | RF32, CU-01 |
| 31 | **Ticket** | pertence a | **Event** | Associação | 0..* → 1..1 | Ingresso sempre está vinculado a um evento. | RF32, CU-01 |
| 32 | **Ticket** | pertence a | **Batch** | Associação | 0..* → 1..1 | Ingresso é gerado de um lote específico. | RF32, CU-01 |
| 33 | **Ticket** | pertence a | **User** (owner) | Associação | 0..* → 1..1 | Ingresso tem um dono atual (pode mudar por transferência). | RF40-RF42, CU-14 |
| 34 | **Ticket** | possui | **QRCode** | Composição | 1..1 → 1..1 | Cada ingresso possui um QR Code único e assinado. | RF32, RF33, RNF06, CU-01 |
| 35 | **Ticket** | está em | **Wallet** | Associação | 0..* → 1..1 | Ingressos ativos ficam na carteira do usuário. | RF20, CU-01 |
| 36 | **Ticket** | pode ter | **Transfer** | Associação | 0..1 ← 0..1 | Ingresso pode ser transferido para outro usuário. | RF40-RF44, CU-14 |
| 37 | **Ticket** | é validado em | **CheckIn** | Associação | 1..1 → 0..1 | Ingresso pode ser validado uma única vez no check-in. | RF36, RB10, CU-02 |
| 38 | **QRCode** | identifica | **Ticket** | Composição | 1..1 → 1..1 | QR Code está fortemente acoplado ao ingresso. | RF32, RF33, RNF06 |
| 39 | **QRCode** | é validado por | **CheckIn** | Dependência | * → * | QR Code é usado para validação no check-in. | RF36, CU-02 |
| 40 | **Transfer** | envolve | **Ticket** | Associação | 0..1 → 1..1 | Transferência sempre envolve um ingresso específico. | RF40, CU-14 |
| 41 | **Transfer** | tem remetente | **User** (sender) | Auto-associação | 0..* → 1..1 | Usuário que inicia a transferência. | RF40, CU-14 |
| 42 | **Transfer** | tem destinatário | **User** (recipient) | Auto-associação | 0..* → 0..1 | Usuário que aceita a transferência (nullable até aceitar). | RF41, CU-14 |
| 43 | **Transfer** | pode ter | **Payment** | Associação | 0..1 → 0..1 | Transferência pode exigir pagamento de taxa. | RF45, RF46, CU-14 |
| 44 | **CheckIn** | valida | **Ticket** | Associação | 0..1 ← 1..1 | Check-in valida um ingresso específico. | RF36, RB10, CU-02 |
| 45 | **CheckIn** | ocorre em | **Event** | Associação | 0..* → 1..1 | Check-in sempre está vinculado a um evento. | RF36, CU-02 |
| 46 | **CheckIn** | é feito por | **User** (operator) | Associação | 0..* → 1..1 | Staff que realiza a validação. | RF37, CU-02 |
| 47 | **Wallet** | pertence a | **User** | Composição | 1..1 → 1..1 | Carteira sempre pertence a um usuário. | RF20, CU-01 |
| 48 | **Wallet** | contém | **Ticket** | Associação | 1..1 → 0..* | Carteira armazena todos os ingressos do usuário. | RF20, CU-01 |
| 49 | **Notification** | é enviada para | **User** | Associação | 0..* → 1..1 | Notificação sempre é destinada a um usuário. | RF35, RF47, RNF14 |
| 50 | **Coupon** | pode ser aplicado a | **Event** | Associação | 0..* → 0..1 | Cupom pode ser específico de um evento ou global. | RF31, RB12, CU-16 |
| 51 | **Coupon** | é criado por | **User** (influencer) | Associação | 0..* → 0..1 | Cupom pode ser de influenciador para rastreamento. | RF31, RB12, CU-16 |
| 52 | **Coupon** | é usado em | **Order** | Dependência | * → * | Cupom é aplicado no momento do pedido. | RF31, CU-16 |
| 53 | **AuditLog** | registra ação de | **User** | Dependência | 0..* → 1..1 | Log sempre registra qual usuário realizou a ação. | RF49, RB14 |
| 54 | **EventProducer** | associa | **Event** + **Producer** | Associação N:N | * ←→ * | Tabela associativa para vincular produtores a eventos. | RF19, CU-13 |
| 55 | **EventCategory** | associa | **Event** + **Category** | Associação N:N | * ←→ * | Tabela associativa para vincular categorias a eventos. | RF08, RF20, CU-07 |





---

## Diagrama de Classes 

Para melhor compreensão do diagrama, a figura 1 mostra a legenda;

<div align="center">
    Figura 1: Legenda do Diagrama de Classes
    <br>
    <img src="assets/Legendas/LegendaDiagramaClasses.drawio.png" width="500">
    <br>
    <b>Autor:</b> <a href="https://github.com/gabriel-lima258">Gabriel Lima</a>.
    <br>
</div>

---

## Segue o diagrama de classes abaixo:

<div align="center">
    Figura 1: Diagrama de Classes — MVP do Ingressou  
    <br>
    <a href="assets/Modelagem/Estatica/classe.pdf" target="_blank">
        <img src="assets/Modelagem/Estatica/classe.pdf" width="900">
    </a>
    <br>
    <b>Autor:</b> Gabriel Lima  
    <br>
    <i>Clique na imagem para abrir o diagrama completo em nova aba.</i>
</div>

---

## Conclusão

A modelagem de classes do **Ingressou (MVP)** representa a estrutura fundamental da plataforma, abrangendo o ciclo completo do ingresso digital — da criação do evento até a transferência entre usuários.  

O modelo prioriza **baixo acoplamento e alta coesão**, garantindo flexibilidade para futuras expansões, como módulos de relatórios, automação de marketing e integrações externas.  
Esta estrutura servirá como base sólida para o desenvolvimento da API e do banco de dados relacional.

---

## Bibliografia

1. GEEKSFORGEEKS. *Unified Modeling Language (UML) Class Diagrams.* Disponível em: [https://www.geeksforgeeks.org/unified-modeling-language-uml-class-diagrams/](https://www.geeksforgeeks.org/unified-modeling-language-uml-class-diagrams/).  
2. UML DIAGRAMS. *Class Diagrams Overview.* Disponível em: [https://www.uml-diagrams.org/class-diagrams-overview.html](https://www.uml-diagrams.org/class-diagrams-overview.html).  
3. TOTVS. *BPMN e UML: como modelar processos de negócio e sistemas.* 2023.  
4. LIMA, Gabriel. *Requisitos Elicitados — Ingressou v1.5.* Outubro de 2025.
5. LIMA, Gabriel. *Diagrama de Casos de Uso — Ingressou v1.0.* Outubro de 2025.

---

## Histórico de Versão

| Versão | Alteração | Responsável | Data |
|---|---|---|---|
| 1.0 | Elaboração inicial do documento e estrutura base | Gabriel Lima | 17/10/2025 |
| 1.1 | Preenchimento completo da Tabela 1 (18 classes + atributos e métodos), Tabela 1.1 (11 enums), Tabela 2 (7 tipos de relacionamentos UML) e Tabela 3 (53 relacionamentos mapeados com rastreabilidade aos requisitos RF e casos de uso CU) | Gabriel Lima | 04/11/2025 |
| 1.2 | Refatoração: Criação da entidade **Location** (classe #4) para isolar dados de localização, permitindo reutilização de venues, enriquecimento geográfico (coordenadas, capacidade, acessibilidade) e suporte a eventos online. Event agora possui relacionamento com Location (locationId nullable). Atualização da Tabela 1 (agora 19 classes), Tabela 3 (agora 55 relacionamentos) e ajuste na metodologia | Gabriel Lima | 04/11/2025 |
