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

1. O diagrama foi elaborado com base na **versão 1.4 dos Requisitos Elicitados do Ingressou (Outubro de 2025)**.  
2. As classes foram identificadas a partir dos **casos de uso e requisitos funcionais principais**, como:
   - Cadastro e autenticação de usuários (clientes e produtores);
   - Criação e gestão de eventos;
   - Compra e transferência de ingressos;
   - Processamento de pagamentos e notificações.
3. A modelagem foi realizada utilizando a ferramenta **[LucidChat](https://lucid.app/lucidchart/)**, seguindo as normas da **UML 2.0**.
4. A estrutura foi validada com base nos princípios de **coesão, baixo acoplamento e reuso**.

---

## Investigação das Classes Necessárias

A tabela abaixo apresenta as principais classes do sistema **Ingressou (MVP)**, seus atributos e métodos essenciais.

<strong>Tabela 1: Classes do Sistema.</strong>

| # | Classe | Responsabilidade | Atributos (principais) | Métodos (principais) |
|---|---|---|---|---|
| 01 | **Usuario** | Identidade/autorização (RBAC). | `id: UUID`, `nome: String`, `email: String {único}`, `senhaHash: String`, `status: StatusUsuario`, `criadoEm: DateTime`, `updatedAt: Instant`, `roles: Set<Role>` | `ativar()`, `desativar()`, `possuiRole(r: Role): boolean`, `atualizarPerfil(dados: Map)`, `definirSenha(nova: String)` |
| 02 | **Cliente** *(subclasse)* | Consumidor; dono de **Carteira**. | *(herda de Usuario)* | `visualizarIngressos(): List<Ingresso>` |
| 03 | **Produtor** *(subclasse)* | Gestão e relatórios dos próprios eventos. | *(herda de Usuario)* | `podeVerRelatoriosDe(e: Evento): boolean`, `isKycVerificado(): boolean` |
| 04 | **Administrador** *(subclasse)* | Governança global via serviços de aplicação. | *(herda de Usuario)* | — *(opera por serviços com RBAC/transactions)* |
| 05 | **Carteira** | Guarda os ingressos do cliente. | `id: UUID`, `dono: Cliente` | `adicionar(i: Ingresso)`, `remover(i: Ingresso)`, `listar(): List<Ingresso>` |
| 06 | **Evento** | Núcleo de venda; agrega lotes e política de transferência. | `id: UUID`, `produtor: Produtor`, `titulo: String`, `slug: String {único}`, `descricao: String`, `inicio: DateTime`, `fim: DateTime`, `local: Localizacao`, `status: StatusEvento`, `publicadoEm?: DateTime`, `transferenciasHabilitadas: boolean`, `policy?: TransferPolicy`, `categorias: List<Categoria>`, `limitePorCpf: Int=5`, `popularidadeScore?: Int` | `publicar()`, `encerrar()`, `cancelar(motivo: String)`, `podeTransferir(ingresso: Ingresso, agora: DateTime): boolean` |
| 07 | **Localizacao** *(VO)* | Endereço/geo do evento. | `endereco: String`, `cidade: String`, `uf: UF`, `cep: String`, `lat?: String`, `lng?: String` | *(validações internas de CEP/UF/geo)* |
| 08 | **Categoria** | Taxonomia e filtros. | `id: UUID`, `nome: String`, `slug: String {único}`, `ativo: boolean` | `gerarSlug(): void`, `ativar(): void`, `desativar():void` |
| 09 | **Lote** | Preço/estoque/janelas. | `id: UUID`, `evento: Evento`, `nome: String`, `preco: BigDecimal (≥0)`, `quantidadeTotal: Int (≥0)`, `quantidadeVendida: Int (≥0)`, `abreEm: DateTime`, `fechaEm: DateTime`, `ativo: boolean`, `tipo: TipoLote` | `disponivel(agora: DateTime): boolean`, `reservar(qtd: Int): void`, `liberar(qtd: Int): void` |
| 10 | **Pedido** | Intenção de compra; agrega itens. | `id: UUID`, `comprador: Cliente`, `status: StatusPedido`, `criadoEm: DateTime`, `total: BigDecimal`, `reservaExpiraEm?: DateTime`, `atribuicoes: List<AtribuicaoInfluenciador>` | `adicionarItem(l: Lote, qtd: Int): void`, `fechar(): void`, `aplicarCupom(c: Cupom): void` |
| 11 | **ItemPedido** | Linha do pedido. | `id: Long`, `pedido: Pedido`, `lote: Lote`, `quantidade: Int (>0)`, `precoUnitario: BigDecimal`, `subtotal: BigDecimal` | `calcularSubtotal(): void` |
| 12 | **Pagamento** | Cobrança (pedido ou taxa de transferência). | `id: UUID`, `pedido?: Pedido`, `transferencia?: Transferencia`, `valor: BigDecimal`, `meio: MeioPagamento`, `status: StatusPagamento`, `transacaoIdGateway?: String`, `autorizadoEm?: DateTime`, `confirmadoEm?: DateTime` | `autorizar(idGw: String): void`, `confirmar(): void`, `recusar(motivo: String): void`, `estornar(): void` |
| 13 | **Ingresso** | Título digital com QR assinado. | `id: UUID`, `carteira: Carteira`, `evento: Evento`, `lote: Lote`, `codigo: String {único}`, `qr: QrCode`, `status: StatusIngresso`, `emitidoEm: DateTime`, `validadoEm?: DateTime`, `meiaEntrada: boolean` | `emitirNovoQr(assinador: QrSigner): void`, `validarEntrada(): void` *(idempotente)*, `invalidarQr(): void` |
| 14 | **QrCode** *(VO)* | Autenticação do ingresso. | `payloadAssinado: String`, `hash: String`, `expiraEm?: DateTime` | `gerarHash(): String`, `verificarHash(): boolean`, `estaExpirado(agora: DateTime): boolean`, `isValido(agora: DateTime): boolean` |
| 15 | **TransferPolicy** | Regras de transferência por evento. | `habilitada: boolean`, `taxaPercentual: BigDecimal (=0.10)`, `taxaFixa?: BigDecimal`, `janelaMinima: Duration`, `bloquearMeiaEntrada: boolean` | `calcularTaxa(valor: BigDecimal): BigDecimal`, `permite(ingresso: Ingresso, agora: DateTime): boolean` |
| 16 | **Transferencia** | Fluxo de transferência (taxa, novo QR, auditoria). | `id: UUID`, `ingresso: Ingresso`, `remetente: Cliente`, `destinatario?: Cliente`, `destinatarioLookup: String`, `status: StatusTransferencia`, `taxaCobrada: BigDecimal`, `criadaEm: DateTime`, `aceitaEm?: DateTime`, `concluidaEm?: DateTime`, `expiraEm?: DateTime`, `pagamentoTransferId?: String` | `criar(ing: Ingresso, rem: Cliente, lookup: String): void`, `aceitar(dest: Cliente): void`, `registrarPagamentoTaxa(txId: String): void`, `concluir(novaCarteira: Carteira, novoQr: QrCode): void`, `recusar(): void`, `expirar(): void`, `cancelar(): void` |
| 17 | **Notificacao** | Mensagens transacionais. | `id: UUID`, `destinatario: Usuario`, `canal: CanalNotificacao`, `template: String`, `params: Map<String,String>`, `enviadaEm?: DateTime`, `status: StatusNotificacao` | `enviar(): void`, `marcarComoEnviada(): void`, `registrarFalha(msg: String): void` |
| 18 | **Auditoria** | Trilha de ações críticas. | `id: Long`, `entidade: String`, `entidadeId: String`, `acao: String`, `usuario?: Usuario`, `momento: DateTime`, `detalheJson: String` | `registrar(...): void` |
| 19 | **Cupom** | Desconto aplicado em pedido (inclui influenciador). | `id: UUID`, `codigo: String {único}`, `tipo: TipoCupom`, `valor: BigDecimal`, `valorMaximo?: BigDecimal`, `minimoPedido?: BigDecimal`, `ativo: boolean`, `expiraEm?: DateTime`, `limiteUso?: Int`, `usos: Int`, `influenciadorId?: UUID`, `cumulativo: boolean=false` | `validar(pedido: Pedido, cliente: Cliente, agora: DateTime): boolean`, `calcularDesconto(pedido: Pedido): BigDecimal` |
| 20 | **AtribuicaoInfluenciador** | Rastreia atribuição de cupom em um pedido. | `id: UUID`, `pedido: Pedido`, `cupom: Cupom`, `influenciadorId: UUID`, `valorDesconto: BigDecimal`, `criadoEm: DateTime` | — |
| 21 | **CashbackProdutor** | **Crédito pós-venda** do produtor (abatimento no repasse). | `id: UUID`, `produtor: Produtor`, `origemPagamento?: Pagamento`, `origemEvento?: Evento`, `valor: BigDecimal (>0)`, `dataCredito: DateTime`, `status: StatusCashbackProdutor`, `descricao?: String`, `repasse?: Repasse (0..1)` | `creditar(): void`, `vincularAoRepasse(r: Repasse): void`, `estornar(motivo: String): void` |
| 22 | **CheckinRegistro** | Log de validações de QR (online/offline). | `id: UUID`, `ingresso: Ingresso`, `operador: Usuario`, `dispositivoId: String`, `modo: ModoCheckin`, `dataHora: DateTime`, `resultado: ResultadoCheckin` | — |
| 23 | **ProdutorKyc** | Dados cadastrais/financeiros verificados (KYC). | `id: UUID`, `produtor: Produtor`, `tipoPessoa: TipoPessoa`, `cpf?: String`, `cnpj?: String`, `razaoSocial?: String`, `chavePix: String`, `banco?: String`, `agencia?: String`, `conta?: String`, `contaDigito?: String`, `verificado: boolean`, `verificadoEm?: DateTime`, `atualizadoEm: DateTime` | `verificar(verificadorId: UUID, motivo?: String): void`, `atualizarDados(cmd): void`, `documentoPrincipal(): String`, `estaCompleto(): boolean`, `validarInvariantes(): void` |
| 24 | **PlatformFeePolicy** | Política de taxas da plataforma (**versionada**). | `id: UUID`, `versao: Int`, `vigenciaInicio: DateTime`, `vigenciaFim?: DateTime`, `percentualPadrao: BigDecimal`, `faixas?: List<Faixa{ateValor, percentual}>`, `teto?: BigDecimal`, `piso?: BigDecimal`, `isencoesPorCategoria?: Set<CategoriaEvento>`, `canaisElegiveis?: Set<CanalVenda>`, `outrasTaxas?: Map<String, BigDecimal>`, `criadoEm: DateTime` | `vigenteEm(data: DateTime): boolean`, `calcular(valor: BigDecimal, ctx: ContextoTaxa): BigDecimal`, `taxaAntifraude(ctx): BigDecimal`, `efetivar(valor, ctx): BigDecimal` |
| 25 | **Repasse** | Payout para produtor (D+X). | `id: UUID`, `produtor: Produtor`, `periodoInicio: DateTime`, `periodoFim: DateTime`, `valorBruto: BigDecimal`, `taxas: BigDecimal`, `totalCashbackAbatido?: BigDecimal`, `valorLiquido: BigDecimal`, `dataAgendada?: DateTime`, `status: StatusRepasse`, `comprovanteUrl?: String`, `criadoEm: DateTime` | `agendar(data: DateTime): void`, `marcarPago(comprovanteUrl?: String): void`, `calcularLiquido(): BigDecimal`, `abaterCashbacks(lista: List<CashbackProdutor>): void`, `saldo(): BigDecimal`, `alterarAgendamento(novaData: DateTime): void` |
| 26 | **Nfse** | Nota fiscal da **taxa de serviço**. | `id: UUID`, `numero?: String`, `serie?: String`, `competencia: YearMonth`, `tomadorTipo: TomadorTipo`, `valorServico: BigDecimal`, `imposto: BigDecimal`, `chaveAcesso?: String`, `xmlUrl?: String`, `emitidaEm?: DateTime`, `status: StatusNfse`, `erroUltimo?: String`, `criadoEm: DateTime` | `marcarGerada(dados): void`, `registrarErro(msg: String): void`, `total(): BigDecimal`, `podeEmitir(): boolean` |
| 27 | **ParametroSistema** | Flags/limites configuráveis (**versionados**). | `id: UUID`, `chave: String`, `tipo: TipoParametro`, `valor: String/JSON`, `escopo: EscopoParametro`, `alvoId?: UUID`, `versao: Int`, `vigenciaInicio: DateTime`, `vigenciaFim?: DateTime`, `atualizadoEm: DateTime`, `atualizadoPor?: UUID` | `vigenteEm(data: DateTime): boolean`, `valorComoBoolean(): boolean`, `valorComoInt(): Int`, `valorComoDecimal(): BigDecimal`, `valorComoJson<T>(): T` |
| 28 | **GatewayPagamento** *(interface)* | Contrato com o provedor de pagamento. | — | `iniciarCobranca(pag: Pagamento): Autorizacao`, `confirmar(pag: Pagamento): Confirmacao`, `estornar(pag: Pagamento): void` |
| 29 | **NfsePagamento** | **Entidade de junção** N:N entre `Nfse` e `Pagamento`. | `id: UUID`, `nfseId: UUID`, `pagamentoId: UUID`, `valorAlocado: BigDecimal`, `competencia: YearMonth`, `criadoEm: DateTime` | `alocar(valor: BigDecimal): void`, `desalocar(): void`, `validarSaldos(pagamento: Pagamento, nfse: Nfse): void` |

**Invariantes-chave**  
- `Repasse.valorLiquido = valorBruto − taxas − (totalCashbackAbatido || 0)` e **não pode ser negativo**.  
- `CashbackProdutor.repasse` é **0..1**: um cashback só pode constar em **um** repasse.  
- Em `NfsePagamento`:  
  - `Σ(valorAlocado) por nfseId ≤ nfse.valorServico`;  
  - `Σ(valorAlocado) por pagamentoId ≤ pagamento.valor`;  
  - `competencia` coerente com `nfse.competencia`.


## Tabela  — Enums (separados)


`Role { ADMIN, PRODUTOR, CLIENTE, CHECKIN }`  
`StatusUsuario { ATIVO, SUSPENSO, DESATIVADO }`  
`StatusEvento { RASCUNHO, AGUARDANDO_APROVACAO, PUBLICADO, ENCERRADO, CANCELADO }`  
`UF { AC, AL, AM, AP, BA, CE, DF, ES, GO, MA, MG, MS, MT, PA, PB, PE, PI, PR, RJ, RN, RO, RR, RS, SC, SE, SP, TO }`  
`TipoLote { INTEIRA, MEIA, PROMOCIONAL, VIP }`  
`StatusPedido { CRIADO, AGUARDANDO_PAGAMENTO, PAGO, CANCELADO, EXPIRADO }`  
`MeioPagamento { PIX, CARTAO }`  
`StatusPagamento { INICIADO, AUTORIZADO, CONFIRMADO, RECUSADO, ESTORNADO }`  
`StatusIngresso { EMITIDO, TRANSFERENCIA_PENDENTE, TRANSFERIDO, VALIDADO, CANCELADO }`  
`StatusTransferencia { CRIADA, AGUARDANDO_ACEITE, AGUARDANDO_PAGAMENTO_TAXA, CONCLUIDA, RECUSADA, EXPIRADA, CANCELADA }`  
`CanalNotificacao { EMAIL, WHATSAPP }`  
`StatusNotificacao { PENDENTE, ENVIADA, FALHA }`  
`TipoCupom { PERCENTUAL, VALOR_FIXO }`  
`EscopoCupom { GLOBAL, EVENTO, PRODUTOR }`  
`StatusCashbackProdutor { CREDITADO, UTILIZADO_EM_REPASSE, ESTORNADO }`  
`ModoCheckin { ONLINE, OFFLINE }`  
`ResultadoCheckin { VALIDO, DUPLICADO, EXPIRADO }`  
`TipoPessoa { PF, PJ }`  
`StatusKyc { PENDENTE, APROVADO, REPROVADO }`  
`StatusRepasse { AGENDADO, PROCESSANDO, PAGO, FALHOU, CANCELADO }`  
`TomadorTipo { PRODUTOR, PLATAFORMA }`  
`StatusNfse { PENDENTE, GERADA, ERRO }`  
`AmbienteFiscal { HOMOLOGACAO, PRODUCAO }`  
`TipoParametro { INT, DECIMAL, BOOL, STRING, JSON }`  
`EscopoParametro { GLOBAL, PRODUTOR, EVENTO }`

---

## Os Tipos de Relacionamentos

**Tabela 2:** Tipos de relacionamentos entre as classes do sistema Ingressou.

| Tipo | Semântica | Notação UML | Exemplos |
|---|---|---|---|
| **Generalização** | Herança (“é-um”). | Linha contínua com triângulo vazio. | `Cliente/Produtor/Administrador` → `Usuario`. |
| **Associação** | Vínculo estrutural (pode ter multiplicidades). | Linha contínua. | `Pedido—Cliente`, `Ingresso—Evento`, `Repasse—Produtor`. |
| **Composição** | Parte-todo **forte** (parte não existe sem o todo). | Linha com **losango preto** no “todo”. | `Pedido—ItemPedido`, `Carteira—Ingresso`, `Ingresso—QrCode`, `Evento—Localizacao`. |
| **Agregação** | Parte-todo **fraco**. | Linha com **losango branco**. | *(Opcional)* `Evento—Categoria`. |
| **Dependência** | Uso pontual/consulta (sem FK). | Linha tracejada `..>`. | Serviços → `PlatformFeePolicy`/`ParametroSistema`, `Pagamento` → `GatewayPagamento`. |
| **Realização** | Implementação de interface. | Tracejada com triângulo vazio. | Adaptadores de pagamento → `GatewayPagamento`. |


---

## Os Relacionamentos no Diagrama de Classes

Além da definição individual de cada classe, a representação de como elas se interconectam é um aspecto vital do Diagrama de Classes, uma vez que ilustra a dinâmica e as dependências estruturais do sistema. Dessa maneira, para elucidar a natureza e as implicações de cada tipo de ligação (como Associação, Agregação, Composição, Generalização e Dependência) utilizada no diagrama visual, elaborou-se também a tabela 3 específica para os relacionamentos. Esta tabela 3 auxiliar tem o objetivo de detalhar mostra os relacionamentos de cada uma das classes da tabela 1.

**Tabela 3:** Relacionamentos entre as classes do sistema Ingressou.

- `Usuario` ⟶ `Cliente/Produtor/Administrador` (**Generalização**)  
- `Cliente 1 ⟷ 1 Carteira` (**Composição**)  
- `Carteira 1 ⟶ 0..* Ingresso` (**Composição**)  
- `Produtor 1 ⟶ 0..* Evento` (**Associação**)  
- `Evento 1 ⟶ 1 Localizacao` (**Composição**)  
- `Evento 0..* ⟷ 0..* Categoria` (**Associação N:N**, via join table)  
- `Evento 1 ⟶ 1..* Lote` (**Composição**)  
- `Cliente 1 ⟷ 0..* Pedido` (**Associação**)  
- `Pedido 1 ⟶ 1..* ItemPedido` (**Composição**)  
- `ItemPedido 0..* ⟶ 1 Lote` (**Associação**)  
- `Pedido 1 ⟷ 0..1 Pagamento` (**Associação**)  
- `Pagamento 1 ⟷ 0..1 Transferencia` (**Associação**, taxa de transferência)  
- `Ingresso 1 ⟶ 1 QrCode` (**Composição**)  
- `Ingresso 1 ⟷ 0..* CheckinRegistro` (**Associação**)  
- `Transferencia 1 ⟶ 1 Ingresso` e `Ingresso 1 ⟷ 0..* Transferencia` (**Associação**, histórico)  
- `Transferencia 1 ⟶ 1 Cliente (remetente)` · `Transferencia 1 ⟶ 0..1 Cliente (destinatário)` (**Associação**)  
- `Evento 1 ⟷ 0..1 TransferPolicy` (**Associação**)  
- `CashbackProdutor 0..* ⟶ 1 Produtor` (**Associação**)  
- `CashbackProdutor 0..* ⟶ 0..1 Pagamento` (**Associação**, origem do crédito)  
- `Repasse 1 ⟶ 0..* CashbackProdutor` (**Associação**)  
- `Produtor 1 ⟶ 0..* Repasse` (**Associação**)  
- `Produtor 1 ⟶ 0..1 ProdutorKyc` (**Associação**)  
- **Faturamento (N:N)**: `Nfse 1 ⟶ 0..* NfsePagamento` e `Pagamento 1 ⟶ 0..* NfsePagamento` (**entidade de junção**)  
- **Dependências (sem FK)**: serviços de domínio `..>` `PlatformFeePolicy` e `ParametroSistema`; `Pagamento ..>` `GatewayPagamento`.



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
4. LIMA, Gabriel. *Requisitos Elicitados — Ingressou v1.4.* Outubro de 2025.

---

## Histórico de Versão

| Versão | Alteração | Responsável | Data |
| - | - | - | - |
| 1.0 | Elaboração inicial do documento e modelagem do MVP | Gabriel Lima | 17/10/2025 |
