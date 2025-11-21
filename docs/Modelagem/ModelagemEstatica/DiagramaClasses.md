# Diagrama de Classes — Projeto Ingressou (MVP)

> **Versão:** 2.4  
> **Data:** 21 de Novembro de 2025  
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

A tabela abaixo apresenta as **23 classes** do sistema **Ingressou (MVP)** (sendo 18 entidades principais + 5 tabelas associativas), seus atributos e métodos, cobrindo todos os requisitos funcionais e regras de negócio identificados. O modelo contempla suporte a produtos e serviços além de ingressos, sistema de notificações e rastreamento de cashback de produtores.

> **Notação UML:**  
> - `+` = público (public)  
> - `-` = privado (private)  
> - `#` = protegido (protected)  
> - `<<pk>>` = chave primária (Primary Key)  
> - `<<fk>>` = chave estrangeira (Foreign Key)

**Tabela 1: Classes do Sistema.**

| # | Classe | Responsabilidade | Atributos (principais) | Métodos (principais) |
|---|---|---|---|---|
| 1 | **User** | Representar usuários do sistema com autenticação e controle de acesso baseado em papéis (RBAC). | `<<pk>>` id: Long<br>`-` name: String<br>`-` email: String (unique)<br>`-` cpf: String (unique)<br>`-` password: String<br>`-` phone: String<br>`-` createdAt: DateTime<br>`-` updatedAt: DateTime | `+` register(): Boolean<br>`+` login(email, password): Token<br>`+` verifyEmail(otp): Boolean<br>`+` resetPassword(token, newPassword): Boolean<br>`+` updateProfile(data): Boolean<br>`+` hasRole(role): Boolean |
| 2 | **Role** | Representar papéis de usuário no sistema (RBAC). | `<<pk>>` id: Long<br>`-` authority: String (unique)<br>`-` description: String<br>`-` createdAt: DateTime | `+` create(authority): Role<br>`+` update(description): Boolean |
| 3 | **Producer** | Representar produtores de eventos com dados de KYC e informações bancárias. | `<<pk>>` id: Long<br>`<<fk>>` userId: Long<br>`-` name: String<br>`-` cnpj: String (nullable)<br>`-` cpf: String<br>`-` pixKey: String<br>`-` bankAccount: String<br>`-` cashbackBalance: Decimal<br>`-` defaultCashbackPercent: Double<br>`-` createdAt: DateTime<br>`-` updatedAt: DateTime | `+` onboard(data): Boolean<br>`+` verifyKYC(): Boolean<br>`+` updateBankingInfo(data): Boolean<br>`+` getCashbackBalance(): Decimal |
| 4 | **Event** | Gerenciar eventos criados exclusivamente pelo Admin. | `<<pk>>` id: Long<br>`-` name: String<br>`-` description: Text<br>`-` imgUrl: String<br>`<<fk>>` locationId: Long (nullable)<br>`-` startDate: DateTime<br>`-` endDate: DateTime<br>`-` status: EventStatus (enum)<br>`-` isOnline: Boolean<br>`-` onlineUrl: String (nullable)<br>`-` producerCashbackPercent: Double<br>`-` published: Boolean<br>`-` createdAt: DateTime<br>`-` updatedAt: DateTime | `+` create(data): Event<br>`+` update(data): Boolean<br>`+` publish(): Boolean<br>`+` cancel(): Boolean<br>`+` isActive(): Boolean |
| 5 | **Location** | Representar locais físicos onde eventos ocorrem. | `<<pk>>` id: Long<br>`-` city: String<br>`-` address: String<br>`-` complement: String (nullable)<br>`-` postalCode: String<br>`-` state: String (UF)<br>`-` country: String<br>`-` latitude: Decimal (nullable)<br>`-` longitude: Decimal (nullable)<br>`-` photoUrl: String (nullable)<br>`-` createdAt: DateTime<br>`-` updatedAt: DateTime | `+` create(data): Location<br>`+` update(data): Boolean |
| 6 | **Category** | Representar taxonomia oficial de categorias de eventos. | `<<pk>>` id: Long<br>`-` name: String<br>`-` description: Text<br>`-` isActive: Boolean<br>`-` createdAt: DateTime<br>`-` updatedAt: DateTime | `+` create(name): Category<br>`+` update(data): Boolean |
| 7 | **TicketLot** | Gerenciar lotes de ingressos com controle de preço e quantidade. | `<<pk>>` id: Long<br>`<<fk>>` eventId: Long<br>`-` name: String<br>`-` price: Decimal<br>`-` totalQuantity: Integer<br>`-` soldQuantity: Integer<br>`-` salesStartDate: DateTime<br>`-` salesEndDate: DateTime<br>`-` status: BatchStatus (enum)<br>`-` createdAt: DateTime<br>`-` updatedAt: DateTime | `+` create(data): TicketLot<br>`+` checkAvailability(quantity): Boolean<br>`+` incrementSold(quantity): void<br>`+` isActive(): Boolean<br>`+` isSoldOut(): Boolean |
| 8 | **Ticket** | Representar ingresso digital. | `<<pk>>` id: Long<br>`<<fk>>` orderId: Long<br>`<<fk>>` orderItemId: Long<br>`<<fk>>` ticketLotId: Long<br>`<<fk>>` eventId: Long<br>`<<fk>>` ownerId: Long<br>`-` ticketType: TicketType (enum)<br>`-` status: TicketStatus (enum)<br>`-` qrCode: String (unique)<br>`-` price: Decimal<br>`-` isHalfPrice: Boolean<br>`-` isTransferable: Boolean<br>`-` validatedAt: DateTime (nullable)<br>`-` createdAt: DateTime | `+` generate(orderItemData): Ticket<br>`+` transfer(newOwnerId): Boolean<br>`+` validate(): Boolean<br>`+` canTransfer(): Boolean |
| 9 | **Order** | Gerenciar pedidos com reserva integrada. | `<<pk>>` id: Long<br>`<<fk>>` userId: Long<br>`-` totalAmount: Decimal<br>`-` discountAmount: Decimal<br>`-` status: OrderStatus (enum)<br>`<<fk>>` couponId: Long (nullable)<br>`-` expiresAt: DateTime<br>`-` confirmedAt: DateTime (nullable)<br>`-` cancelledAt: DateTime (nullable)<br>`-` createdAt: DateTime | `+` create(cartData): Order<br>`+` applyCoupon(code): Boolean<br>`+` calculateTotal(): Decimal<br>`+` confirm(): Boolean<br>`+` cancel(): Boolean<br>`+` expireReservation(): void |
| 10 | **OrderItem** | Detalhar itens individuais de um pedido (ingressos ou produtos). | `<<pk>>` id: Long<br>`<<fk>>` orderId: Long<br>`<<fk>>` eventId: Long<br>`<<fk>>` ticketLotId: Long (nullable)<br>`<<fk>>` productId: Long (nullable)<br>`-` itemType: OrderItemType (enum)<br>`-` quantity: Integer<br>`-` price: Decimal<br>`-` totalPrice: Decimal | `+` calculateSubtotal(): Decimal<br>`+` generateTickets(): List\<Ticket\> |
| 11 | **Payment** | Processar pagamentos (PIX, Cartão de Crédito, Cartão de Débito). | `<<pk>>` id: Long<br>`<<fk>>` orderId: Long<br>`-` status: PaymentStatus (enum)<br>`-` amount: Decimal<br>`-` gateway: String<br>`-` gatewayTransactionId: String<br>`-` method: MethodPayment (enum)<br>`-` pixQrCode: String (nullable)<br>`-` cardBrand: String (nullable)<br>`-` authorizationCode: String (nullable)<br>`-` installments: Integer (nullable)<br>`-` paidAt: DateTime (nullable)<br>`-` refundedAt: DateTime (nullable)<br>`-` createdAt: DateTime<br>`-` updatedAt: DateTime | `+` initiate(): Boolean<br>`+` confirm(): Boolean<br>`+` refund(): Boolean<br>`+` cancel(): Boolean<br>`+` generatePixQR(): String |
| 12 | **Cupom** | Gerenciar cupons de influenciadores. | `<<pk>>` id: Long<br>`-` code: String (unique)<br>`<<fk>>` influencerId: Long (nullable)<br>`-` discountType: String (PERCENT/FIXED)<br>`-` discountValue: Decimal<br>`-` maxUsed: Integer<br>`-` usageCount: Integer<br>`-` validFrom: DateTime<br>`-` validUntil: DateTime<br>`-` isActive: Boolean<br>`-` createdAt: DateTime<br>`-` updatedAt: DateTime | `+` validate(eventId): Boolean<br>`+` apply(orderAmount): Decimal<br>`+` incrementUsage(): void<br>`+` canUse(): Boolean<br>`+` isApplicableTo(eventId): Boolean |
| 13 | **TicketTransfer** | Gerenciar transferências de ingressos. | `<<pk>>` id: Long<br>`<<fk>>` ticketId: Long<br>`<<fk>>` senderId: Long<br>`<<fk>>` recipientId: Long (nullable)<br>`-` recipientEmail: String<br>`-` recipientCpf: String<br>`-` reason: String<br>`-` status: TransferStatus (enum)<br>`-` acceptToken: String (unique)<br>`-` tokenExpiresAt: DateTime<br>`-` acceptedAt: DateTime (nullable)<br>`-` cancelledAt: DateTime (nullable)<br>`-` createdAt: DateTime<br>`-` updatedAt: DateTime | `+` initiate(ticketId, recipient): TicketTransfer<br>`+` accept(token): Boolean<br>`+` cancel(): Boolean |
| 14 | **CheckIn** | Registrar validações de ingressos. | `<<pk>>` id: Long<br>`<<fk>>` ticketId: Long<br>`<<fk>>` eventId: Long<br>`<<fk>>` operatorId: Long<br>`-` status: CheckInStatus (enum)<br>`-` deviceId: String<br>`-` ipAddress: String<br>`-` location: String<br>`-` validatedAt: DateTime<br>`-` deviceInfo: String<br>`-` isOffline: Boolean<br>`-` createdAt: DateTime | `+` validate(qrCode): CheckIn |
| 15 | **Notification** | Gerenciar notificações assíncronas. | `<<pk>>` id: Long<br>`<<fk>>` userId: Long<br>`-` type: NotificationType (enum)<br>`-` channel: String (EMAIL/WHATSAPP)<br>`-` subject: String<br>`-` content: Text<br>`-` status: String<br>`-` sentAt: DateTime (nullable)<br>`-` readAt: Instant (nullable)<br>`-` read: Boolean<br>`-` createdAt: DateTime | `+` send(): Boolean<br>`+` markAsRead(): Boolean |
| 16 | **Product** | Gerenciar produtos e serviços vendidos junto com eventos. | `<<pk>>` id: Long<br>`<<fk>>` eventId: Long<br>`-` name: String<br>`-` description: String<br>`-` type: ProductType (enum)<br>`-` price: BigDecimal<br>`-` totalQuantity: Integer<br>`-` soldQuantity: Integer<br>`-` active: Boolean<br>`-` createdAt: DateTime<br>`-` updatedAt: DateTime | `+` create(data): Product<br>`+` update(data): Boolean<br>`+` checkAvailability(quantity): Boolean<br>`+` incrementSold(quantity): void |
| 17 | **ProducerCashbackTransaction** | Registrar transações de cashback de produtores. | `<<pk>>` id: Long<br>`<<fk>>` producerId: Long<br>`<<fk>>` orderId: Long (nullable)<br>`<<fk>>` eventId: Long (nullable)<br>`-` CashbackType: CashbackType (enum)<br>`-` amount: Decimal<br>`-` description: String<br>`-` balanceAfter: Double<br>`-` createdAt: DateTime<br>`-` updatedAt: DateTime | `+` create(producerId, amount, type): ProducerCashbackTransaction<br>`+` getBalance(producerId): Double |
| 18 | **UserRole** | Tabela associativa User-Role (RBAC). | `<<pk>>` id: Long<br>`<<fk>>` userId: Long<br>`<<fk>>` roleId: Long<br>`-` assignedAt: DateTime | `+` assign(userId, roleId): Boolean<br>`+` revoke(): void |
| 19 | **EventProducer** | Tabela associativa Event-Producer. | `<<pk>>` id: Long<br>`<<fk>>` eventId: Long<br>`<<fk>>` producerId: Long<br>`-` linkedAt: DateTime | `+` link(eventId, producerId): Boolean<br>`+` unlink(): void |
| 20 | **EventCategory** | Tabela associativa Event-Category. | `<<pk>>` id: Long<br>`<<fk>>` eventId: Long<br>`<<fk>>` categoryId: Long<br>`-` createdAt: DateTime | `+` assign(eventId, categoryId): Boolean<br>`+` remove(): void |
| 21 | **CouponEvent** | Tabela associativa Cupom-Event. | `<<pk>>` id: Long<br>`<<fk>>` couponId: Long<br>`<<fk>>` eventId: Long<br>`-` createdAt: DateTime | `+` assign(couponId, eventId): Boolean<br>`+` remove(): void |

---

## Tabela de Enums e Tipos

As enumerações (enums) são tipos especiais que definem um conjunto fixo de valores constantes. No sistema **Ingressou**, são utilizadas para garantir consistência e facilitar a validação de dados em campos críticos.

**Tabela 1.1: Enumerações do Sistema.**

| # | Enum | Valores | Descrição | Uso |
|---|---|---|---|---|
| 1 | **EventStatus** | `DRAFT`, `PUBLISHED`, `CANCELLED`, `FINISHED` | Status do ciclo de vida do evento | Campo `status` da classe `Event` |
| 2 | **BatchStatus** | `SCHEDULED`, `ACTIVE`, `SOLD_OUT`, `EXPIRED`, `CANCELLED` | Status do lote de ingressos | Campo `status` da classe `TicketLot` |
| 3 | **TicketType** | `FULL`, `HALF`, `VIP`, `COURTESY` | Tipos de ingresso | Campo `ticketType` da classe `Ticket` |
| 4 | **TicketStatus** | `ACTIVE`, `TRANSFERRED`, `VALIDATED`, `CANCELLED`, `EXPIRED` | Status do ingresso | Campo `status` da classe `Ticket` |
| 5 | **OrderStatus** | `PENDING`, `AWAITING_PAYMENT`, `PAID`, `CANCELLED`, `EXPIRED`, `REFUNDED` | Status do pedido | Campo `status` da classe `Order` |
| 6 | **PaymentStatus** | `PENDING`, `PROCESSING`, `APPROVED`, `REFUSED`, `CANCELLED`, `REFUNDED`, `EXPIRED` | Status do pagamento | Campo `status` da classe `Payment` |
| 7 | **MethodPayment** | `CREDIT_CARD`, `DEBIT_CARD`, `PIX` | Método de pagamento | Campo `method` da classe `Payment` |
| 8 | **TransferStatus** | `PENDING`, `ACCEPTED`, `REFUSED`, `CANCELLED`, `EXPIRED`, `COMPLETED` | Status da transferência | Campo `status` da classe `TicketTransfer` |
| 9 | **CheckInStatus** | `VALID`, `ALREADY_USED`, `INVALID`, `EXPIRED`, `FRAUD_ATTEMPT` | Status do check-in | Campo `status` da classe `CheckIn` |
| 10 | **NotificationType** | `ORDER_CONFIRMED`, `TICKET_ISSUED`, `TRANSFER_INVITED`, `TRANSFER_ACCEPTED`, `TRANSFER_CANCELLED`, `CHECKIN_SUCCESS`, `PASSWORD_RESET`, `EMAIL_VERIFICATION` | Tipo de notificação | Campo `type` da classe `Notification` |
| 11 | **OrderItemType** | `TICKET`, `PRODUCT` | Tipo de item do pedido | Campo `itemType` da classe `OrderItem` |
| 12 | **ProductType** | `SERVICE`, `MERCH` (e outros) | Tipo de produto ou serviço | Campo `type` da classe `Product` |
| 13 | **CashbackType** | `CREDIT`, `DEBIT`, `ADJUSTMENT` | Tipo de transação de cashback | Campo `CashbackType` da classe `ProducerCashbackTransaction` |



---

## Os Tipos de Relacionamentos

Os relacionamentos entre classes definem como as entidades do sistema se conectam e interagem. A UML 2.0 define vários tipos de relacionamentos, cada um com sua semântica específica e notação visual.

**Tabela 2: Tipos de Relacionamentos UML Utilizados no Sistema.**

| Tipo | Semântica | Notação UML | Multiplicidade | Exemplos no Sistema |
|---|---|---|---|---|
| **Associação Simples** | Relacionamento estrutural entre classes onde uma classe conhece e usa outra, mas ambas têm ciclos de vida independentes. | Linha sólida `───→`<br>Pode ter rótulo e multiplicidade | `1..1`, `1..*`, `0..*`, `*` | `User ───→ Order` (1..1 → 0..*)<br>`Ticket ───→ Event` (0..* → 1..1)<br>`Order ───→ Payment` (1..1 → 1..1) |
| **Agregação** | Tipo especial de associação que representa um relacionamento "todo-parte" onde as partes podem existir independentemente do todo. | Linha sólida com losango vazio `◇───→` | `1..1 ◇───→ 0..*` | `Event ◇───→ TicketLot`<br>Evento pode ter 0 ou vários lotes. Lotes podem existir temporariamente sem evento. |
| **Composição** | Relacionamento "todo-parte" forte onde as partes não podem existir sem o todo. Quando o todo é destruído, as partes também são. | Linha sólida com losango preenchido `◆───→` | `1..1 ◆───→ 1..*` | `Order ◆───→ OrderItem`<br>`Order ◆───→ Payment`<br>Se o pedido é deletado, os itens também são |
| **Dependência** | Relacionamento mais fraco onde uma classe usa outra temporariamente (parâmetro de método, variável local), sem manter referência permanente. | Linha tracejada com seta `⤏` | Não possui multiplicidade | `Order ⤏ Cupom` (usa para calcular desconto) |
| **Associação N:N** | Relacionamento muitos-para-muitos entre classes, geralmente representado por uma classe associativa intermediária. | Linha sólida com multiplicidade `*` em ambos os lados, ou classe intermediária | `* ←→ *` | `Event ←→ Producer` (via `EventProducer`)<br>`Event ←→ Category` (via `EventCategory`) |
| **Auto-associação** | Relacionamento de uma classe consigo mesma, útil para hierarquias ou relações reflexivas. | Linha que sai e volta para a mesma classe | `0..* → 1..1` | `User ───→ User` (remetente/destinatário em `TicketTransfer`) |



---

## Os Relacionamentos no Diagrama de Classes

Além da definição individual de cada classe, a representação de como elas se interconectam é um aspecto vital do Diagrama de Classes, uma vez que ilustra a dinâmica e as dependências estruturais do sistema. 

Para elucidar a natureza e as implicações de cada tipo de ligação (Associação, Agregação, Composição e Dependência) utilizada no diagrama visual, elaborou-se a **Tabela 3** específica para os relacionamentos. Esta tabela auxiliar tem o objetivo de detalhar os relacionamentos entre as **23 classes** da Tabela 1, incluindo multiplicidades, tipos de relacionamento e rastreabilidade aos requisitos funcionais e casos de uso.

**Tabela 3: Relacionamentos entre as Classes do Sistema Ingressou.**

| # | Classe Origem | Relacionamento | Classe Destino | Tipo | Multiplicidade | Descrição | Justificativa (Requisitos) |
|---|---|---|---|---|---|---|---|
| 1 | **User** | possui | **Role** | Associação N:N (via UserRole) | 1..* ←→ 1..* | Usuário deve ter pelo menos um papel no sistema (RBAC). | RF01-RF05, RB14 |
| 2 | **User** | realiza | **Order** | Associação | 1..1 → 0..* | Usuário pode realizar múltiplos pedidos ao longo do tempo. | RF26-RF30, CU-01 |
| 3 | **User** | possui | **Ticket** (owner) | Associação | 1..1 → 0..* | Usuário possui ingressos (pode mudar por transferência). | RF40-RF42, CU-14 |
| 4 | **User** | cria (Admin) | **Event** | Associação | 1..1 → 0..* | Apenas usuários com papel ADMIN podem criar eventos. | RF15, RB13, CU-11 |
| 5 | **User** | realiza (Staff) | **CheckIn** | Associação | 1..1 → 0..* | Usuários com papel STAFF realizam validações de check-in. | RF36-RF39, CU-02 |
| 6 | **Producer** | estende | **User** | Associação | 1..1 → 1..1 | Producer é um perfil especializado vinculado a um User. | RF12-RF14, CU-09, CU-10 |
| 7 | **Producer** | vincula-se a | **Event** | Associação N:N (via EventProducer) | 0..* ←→ 0..* | Produtores vinculados a eventos através da tabela EventProducer. | RF19, RB14, CU-13 |
| 8 | **Event** | ocorre em | **Location** | Associação | 0..* → 0..1 | Evento pode ter localização física ou ser online. | RF07, RF15, RF18, RB17, CU-07, CU-08 |
| 9 | **Event** | contém | **TicketLot** | Agregação | 1..1 → 0..* | Evento pode ter zero ou vários lotes de ingressos. Eventos em rascunho podem não ter lotes ainda. | RF21-RF23, RB11, CU-15 |
| 10 | **Event** | pertence a | **Category** | Associação N:N (via EventCategory) | 1..* ←→ 1..* | Eventos com categorias através da tabela EventCategory. | RF08, RF20, RB16, CU-07 |
| 11 | **Event** | permite | **Cupom** | Associação N:N (via CouponEvent) | 0..* ←→ 0..* | Cupons podem ser aplicados a múltiplos eventos específicos ou serem globais (sem vinculação). Relacionamento através da tabela CouponEvent. | RF31, RB12, CU-16 |
| 12 | **Event** | possui | **Product** | Associação | 1..1 → 0..* | Evento pode ter produtos e serviços associados. | CU-01 |
| 13 | **TicketLot** | referenciado por | **OrderItem** | Associação | 1..1 → 0..* | Itens de pedido referenciam lotes específicos. | CU-01 |
| 14 | **Product** | referenciado por | **OrderItem** | Associação | 1..1 → 0..* | Itens de pedido podem referenciar produtos. | CU-01 |
| 15 | **Order** | feito por | **User** | Associação | 0..* → 1..1 | Pedido sempre pertence a um usuário. | RF26, CU-01 |
| 16 | **Order** | contém | **OrderItem** | Composição | 1..1 → 1..* | Pedido composto por um ou mais itens. | RF26, CU-01 |
| 17 | **Order** | possui | **Payment** | Composição | 1..1 → 0..1 | Pedido pode ter pagamento associado. | RF27-RF30, CU-01 |
| 18 | **Order** | aplica | **Cupom** | Dependência | 0..* → 0..1 | Pedido pode aplicar cupom de desconto. | RF31, RB12, CU-16 |
| 19 | **OrderItem** | pertence a | **Order** | Composição | 0..* → 1..1 | Item de pedido sempre pertence a um pedido. | RF26, CU-01 |
| 20 | **OrderItem** | referencia | **Event** | Associação | 0..* → 1..1 | Item de pedido sempre referencia um evento. | CU-01 |
| 21 | **OrderItem** | gera | **Ticket** | Associação | 1..1 → 0..* | Item do pedido pode gerar ingressos conforme quantidade (se itemType = TICKET). | RF29, RF32, CU-01 |
| 22 | **Ticket** | pertence a | **Order** | Associação | 0..* → 1..1 | Ingresso gerado a partir de um pedido. | RF32, CU-01 |
| 23 | **Ticket** | pertence a | **OrderItem** | Associação | 0..* → 1..1 | Ingresso pertence a um item específico do pedido. | RF32, CU-01 |
| 24 | **Ticket** | referencia | **Event** | Associação | 0..* → 1..1 | Ingresso vinculado a um evento específico. | RF32, CU-01 |
| 25 | **Ticket** | gerado de | **TicketLot** | Associação | 0..* → 1..1 | Ingresso gerado de um lote específico. | RF32, CU-01 |
| 26 | **Ticket** | pode ter | **TicketTransfer** | Associação | 1..1 → 0..1 | Ingresso pode ter transferência associada. | RF40-RF44, CU-14 |
| 27 | **Ticket** | validado por | **CheckIn** | Associação | 1..1 → 0..1 | Ingresso validado uma única vez no check-in. | RF36, RB10, CU-02 |
| 28 | **TicketTransfer** | envolve | **Ticket** | Associação | 0..1 ← 1..1 | Transferência envolve um ingresso específico. | RF40, CU-14 |
| 29 | **TicketTransfer** | enviado por | **User** (sender) | Associação | 0..* → 1..1 | Usuário que inicia a transferência. | RF40, CU-14 |
| 30 | **TicketTransfer** | recebido por | **User** (recipient) | Associação | 0..* → 0..1 | Usuário que aceita a transferência. | RF41, CU-14 |
| 31 | **CheckIn** | valida | **Ticket** | Associação | 0..1 ← 1..1 | Check-in valida um ingresso. | RF36, RB10, CU-02 |
| 32 | **CheckIn** | ocorre em | **Event** | Associação | 0..* → 1..1 | Check-in vinculado a um evento. | RF36, CU-02 |
| 33 | **Cupom** | criado por | **User** (influencer) | Associação | 0..* → 0..1 | Cupom de influenciador para rastreamento. | RF31, RB12, CU-16 |
| 34 | **User** | recebe | **Notification** | Associação | 1..1 → 0..* | Usuário pode receber múltiplas notificações. | RF35, RF47 |
| 35 | **Producer** | possui | **ProducerCashbackTransaction** | Associação | 1..1 → 0..* | Produtor possui transações de cashback. | RB02 |
| 36 | **ProducerCashbackTransaction** | referencia | **Order** | Associação | 0..* → 0..1 | Transação de cashback pode referenciar um pedido. | RB02 |
| 37 | **ProducerCashbackTransaction** | referencia | **Event** | Associação | 0..* → 0..1 | Transação de cashback pode referenciar um evento. | RB02 |
| 38 | **UserRole** | associa | **User** + **Role** | Associação N:N | 1..* ←→ 1..* | Vincula usuários a papéis (RBAC). | RF01-RF05, RB14 |
| 39 | **EventProducer** | associa | **Event** + **Producer** | Associação N:N | 0..* ←→ 0..* | Vincula produtores a eventos. | RF19, CU-13 |
| 40 | **EventCategory** | associa | **Event** + **Category** | Associação N:N | 1..* ←→ 1..* | Vincula categorias a eventos. | RF08, RF20, CU-07 |
| 41 | **CouponEvent** | associa | **Cupom** + **Event** | Associação N:N | 0..* ←→ 0..* | Vincula cupons a eventos específicos. Cupons sem vinculação são globais (aplicáveis a qualquer evento). | RF31, RB12, CU-16 |





---

## Diagrama de Classes 

O diagrama visual abaixo representa graficamente todas as classes, seus atributos, métodos e relacionamentos descritos nas tabelas anteriores. A visualização facilita a compreensão da arquitetura do sistema e serve como referência para desenvolvedores e arquitetos.

### Legenda do Diagrama

Para melhor compreensão do diagrama, a **Figura 1** mostra a legenda com os símbolos e convenções utilizadas:

<div align="center">
    <strong>Figura 1: Legenda do Diagrama de Classes</strong>
    <br>
    <img src="assets/Legendas/LegendaDiagramaClasses.drawio.png" width="500">
    <br>
    <b>Autor:</b> <a href="https://github.com/gabriel-lima258">Gabriel Lima</a>.
    <br>
</div>

---

### Diagrama Completo

O diagrama completo abaixo representa a estrutura estática do sistema **Ingressou (MVP)**, incluindo todas as 23 classes (18 entidades principais + 5 tabelas associativas), 13 enumerações e os relacionamentos mapeados:

<div align="center">
    <strong>Figura 2: Diagrama de Classes — MVP do Ingressou</strong>
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

### Observações sobre o Diagrama

- **Classes essenciais:** O diagrama apresenta **23 classes** organizadas por domínio, incluindo 5 tabelas associativas (UserRole, EventProducer, EventCategory, CouponEvent) e suporte a produtos além de ingressos (Product, OrderItemType).
- **Enumerações completas:** As **13 enumerações** cobrem todos os aspectos do sistema, incluindo tipos de pagamento (MethodPayment), status de check-in (CheckInStatus), tipos de notificação (NotificationType), tipos de item de pedido (OrderItemType) e tipos de produto (ProductType).
- **Relacionamentos otimizados:** Os relacionamentos incluem composição, agregação, associações e dependências. Payment agora é uma classe única com enum MethodPayment ao invés de herança.
- **Tipos de dados:** Utiliza Long para IDs (chaves primárias) e tipos específicos conforme necessário (Decimal, BigDecimal, DateTime, Boolean, etc.).
- **Chaves:** As chaves primárias (`<<pk>>`) e estrangeiras (`<<fk>>`) são indicadas nos atributos.
- **Visibilidade:** Atributos privados (`-`) e métodos públicos (`+`).
- **RBAC:** Classe **Role** separada com tabela associativa **UserRole** para controle de acesso.
- **Notificações:** Classe **Notification** para gerenciamento de notificações assíncronas.
- **Cashback:** Classe **ProducerCashbackTransaction** para rastreamento de transações de cashback de produtores.

---

## Conclusão

A modelagem de classes do **Ingressou (MVP)** representa a estrutura fundamental da plataforma, abrangendo o ciclo completo do ingresso digital — da criação do evento até a transferência entre usuários.  

### Principais Características da Modelagem

1. **Modelo Otimizado e Completo:** O modelo contempla todas as funcionalidades do MVP através de **23 classes** (18 entidades principais + 5 tabelas associativas), **13 enumerações** e relacionamentos, garantindo rastreabilidade completa aos requisitos funcionais (RF01-RF52) e casos de uso (CU-01 a CU-18). O modelo suporta tanto ingressos quanto produtos/serviços adicionais vendidos junto com eventos.

2. **Arquitetura Robusta:** O modelo prioriza **baixo acoplamento e alta coesão**, garantindo flexibilidade para futuras expansões, como módulos de relatórios, automação de marketing e integrações externas.

3. **Padrões UML:** A modelagem segue rigorosamente as normas da **UML 2.0**, utilizando adequadamente os tipos de relacionamento (Associação, Agregação, Composição, Dependência) conforme a semântica do domínio e ciclo de vida das entidades. O modelo utiliza enumerações para MethodPayment ao invés de herança, simplificando a implementação.

4. **Rastreabilidade:** Todos os relacionamentos são justificados por requisitos específicos, facilitando a manutenção e evolução do sistema.

5. **Base para Implementação:** Esta estrutura servirá como base sólida para o desenvolvimento da API REST, persistência de dados em banco relacional (PostgreSQL) e implementação da lógica de negócios.

### Próximos Passos

Com esta modelagem concluída, o próximo passo é a implementação do banco de dados relacional seguindo esta estrutura, garantindo integridade referencial, índices apropriados e otimizações para as consultas mais frequentes (busca por cidade/UF/categoria, validação de QR Codes, gestão de notificações, etc.).

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
| 1.3 | Revisão completa baseada nos Requisitos Elicitados v1.5 e Casos de Uso v1.0. Principais correções: (1) Adicionados campos na classe **Event** para configuração de taxa de transferência (RF46), limite por CPF (RF24/RB03), políticas de meia-entrada (RB06) e percentuais de cashback/plataforma (RB01/RB02); (2) Expandida classe **Transfer** com campos para rastrear percentual e valor da taxa (RF45), preço original e data de recusa; (3) Criadas classes **CashbackTransaction** para registrar cashback do produtor (RB02) e **TicketReservation** para controlar reservas temporárias PIX (RF27/RB04); (4) Adicionado cashbackAmount em **Order**; (5) Atualizada Tabela 1 (agora 21 classes), Tabela 3 (agora 61 relacionamentos) | Gabriel Lima | 05/11/2025 |
| 1.4 | Melhorias na apresentação e organização do documento seguindo padrões UML formais: (1) Adicionada notação explícita de chaves primárias (`<<pk>>`) e estrangeiras (`<<fk>>`) em todos os atributos; (2) Incluída notação de visibilidade UML (`+` público, `-` privado) em atributos e métodos; (3) Expandida Tabela 1.1 (Enums) com coluna "Uso" indicando onde cada enum é utilizado; (4) Melhorada Tabela 2 (Tipos de Relacionamentos) com exemplos específicos do sistema e multiplicidades; (5) Aprimorada seção do Diagrama de Classes com legenda detalhada e observações; (6) Expandida seção de Conclusão com características principais e próximos passos | Gabriel Lima | 05/11/2025 |
| 1.5 | Simplificação do modelo: (1) Removida classe **AuditLog**; (2) Criada classe **Role** separada para RBAC (substituindo enum UserRole); (3) Simplificadas todas as classes reduzindo atributos e métodos não essenciais para o MVP; (4) Atualizada Tabela 1 (21 classes), Tabela 1.1 (10 enums após remoção de UserRole) e Tabela 3 (60 relacionamentos); (5) Ajustado relacionamento User-Role para associação N:N | Gabriel Lima | 05/11/2025 |
| 1.6 | Otimização e correção dos relacionamentos: (1) Eliminados relacionamentos redundantes e bidirecionais desnecessários (de 60 para 46); (2) Corrigidas multiplicidades incorretas; (3) Adicionada tabela associativa **UserRole** explicitamente; (4) Reorganizados relacionamentos por domínio lógico; (5) Atualizada Tabela 1 (agora 22 classes incluindo UserRole) e Tabela 3 (46 relacionamentos otimizados); (6) Removidos relacionamentos duplicados entre classes relacionadas (ex: User-Wallet, Ticket-QRCode, Order-Payment) | Gabriel Lima | 05/11/2025 |
| 1.7 | Correção crítica na rastreabilidade de ingressos: (1) Adicionado `orderItemId` (FK) na classe **Ticket** para rastreamento detalhado; (2) Adicionado relacionamento **OrderItem → Ticket** (1..1 → 1..*) - cada OrderItem gera múltiplos Tickets conforme quantidade; (3) Movida responsabilidade de gerar tickets de Order para OrderItem (método `generateTickets()` em OrderItem); (4) Atualizada Tabela 3 (agora 47 relacionamentos); (5) Corrigida lógica: OrderItem contém (batchId, ticketType, quantity) e cada Ticket herda essas informações do OrderItem que o gerou | Gabriel Lima | 05/11/2025 |
| 2.0 | **Simplificação drástica do modelo**: (1) **REMOVIDAS 5 classes desnecessárias**: QRCode (integrado em Ticket), Wallet (query direto em Ticket.ownerId), Notification (serviço externo), CashbackTransaction (apenas balance em Producer), TicketReservation (integrado em Order); (2) **Atributos integrados**: QR Code agora é atributo de Ticket (qrCode, qrSignature); Reserva PIX agora é campo em Order (reservationExpiresAt); (3) **Enums simplificados** de 10 para 8 (removidos valores intermediários); (4) **Relacionamentos otimizados** de 47 para 35; (5) Atualizada Tabela 1 (17 classes), Tabela 1.1 (8 enums) e Tabela 3 (35 relacionamentos) | Gabriel Lima | 21/11/2025 |
| 2.1 | Correções de multiplicidade e relacionamentos N:N: (1) Corrigida multiplicidade **Event → Batch** de `1..1 → 1..*` para `1..1 → 0..*` (evento em rascunho pode ter 0 lotes); (2) Corrigido relacionamento **Coupon ←→ Event** de `0..* → 0..1` para **N:N** (cupom pode ser aplicável a múltiplos eventos específicos ou ser global); (3) Criada tabela associativa **CouponEvent** para suportar cupons aplicáveis a múltiplos eventos; (4) Removido campo `eventId` de Coupon e adicionado campo `isGlobal` (Boolean); (5) Atualizada Tabela 1 (agora 18 classes incluindo CouponEvent) | Gabriel Lima | 21/11/2025 |
| 2.2 | Restauração da classe **QRCode**: (1) QRCode voltou a ser classe separada (removida de atributos de Ticket); (2) Adicionados atributos: id, ticketId, content, signature, isValid, invalidatedAt; (3) Métodos: generate(), sign(), verify(), invalidate(), regenerate(); (4) Relacionamento **Ticket ◆→ QRCode** (Composição 1:1) restaurado; (5) Adicionado relacionamento **CheckIn ⤏ QRCode** (Dependência) para validação; (6) Atualizada Tabela 1 (agora 19 classes: 15 entidades + 4 associativas) e Tabela 3 (42 relacionamentos) | Gabriel Lima | 21/11/2025 |
| 2.3 | **Implementação de Herança em Payment**: (1) Payment transformada em classe **abstrata**; (2) Criadas classes especializadas **PixPayment** (com pixQrCode, pixExpiresAt) e **CreditCardPayment** (com cardToken, installments, authorizationCode); (3) Removido enum **PaymentMethod** (substituído por herança); (4) Adicionados 2 relacionamentos de herança (PixPayment △→ Payment, CreditCardPayment △→ Payment); (5) Métodos específicos por tipo de pagamento (generatePixQR(), validate3DS()); (6) Atualizada Tabela 1 (21 classes: 17 entidades + 4 associativas), Tabela 1.1 (7 enums) e Tabela 3 (39 relacionamentos incluindo herança) | Gabriel Lima | 21/11/2025 |
| 2.4 | **Refatoração completa baseada no novo diagrama PDF**: (1) **Removida herança de Payment** - Payment voltou a ser classe única com enum MethodPayment (CREDIT_CARD, DEBIT_CARD, PIX); (2) **Removida classe QRCode** - QR Code integrado como atributo (qrCode) em Ticket; (3) **Renomeado Batch para TicketLot**; (4) **Adicionadas 3 classes**: Notification (notificações assíncronas), Product (produtos/serviços), ProducerCashbackTransaction (transações de cashback); (5) **Atualizado OrderItem** para suportar produtos além de ingressos (itemType: OrderItemType, product?, event); (6) **Renomeado Transfer para TicketTransfer**; (7) **Atualizados tipos de dados** de UUID para Long; (8) **Atualizados enums**: novos valores em OrderStatus, PaymentStatus, TransferStatus, BatchStatus, EventStatus, TicketStatus, TicketType; adicionados CheckInStatus, NotificationType, OrderItemType, ProductType, CashbackType, MethodPayment; (9) **Atualizados atributos** em várias classes conforme PDF (ex: Producer.bankAccount, Event.producerCashbackPercent, Location.photoUrl, CheckIn.status/deviceId/ipAddress, etc.); (10) Atualizada Tabela 1 (23 classes: 18 entidades + 5 associativas), Tabela 1.1 (13 enums) e Tabela 3 (39 relacionamentos atualizados, removida herança) | Gabriel Lima | 21/11/2025 |
