# Diagrama de Pacotes

> **Versão:** 1.0  
> **Data:** Outubro de 2025  
> **Autor:** Gabriel Lima  
> **Projeto:** Ingressou — Plataforma Web de Venda e Gestão de Ingressos  

---

## Sumário

- [Introdução](#Introdução)
- [Objetivos](#Objetivos)
- [Metodologia](#Metodologia)
- [Sobre o Diagrama de Pacotes](#Sobre-o-Diagrama-de-Pacotes)
- [Elaboração do Diagrama](Elaboração-do-Diagrama)
- [Diagrama de Pacotes](#Diagrama-de-Pacotes)
- [Conclusão](#Conclusão)
- [Bibliografia](#Bibliografia)
- [Histórico de versão](#Histórico-de-versão)

## Introdução

O Diagrama de Pacotes é um dos diagramas estruturais da UML (Unified Modeling Language) utilizado para representar, de forma hierárquica e organizada, os agrupamentos lógicos dos elementos de um sistema, como classes, casos de uso, componentes, entre outros. Conforme definido na APOSTILA UML [1](#ref1), o pacote é um mecanismo de propósito geral que permite reunir elementos semanticamente relacionados, o que facilita a visualização e o gerenciamento modular de grandes sistemas.

Segundo o [Diagrama de Pacotes: Definição, Componentes](https://gitmind.com/pt/diagrama-de-pacotes.html#:~:text=Um%20diagrama%20de%20pacotes%20pode,outros%20campos%20em%20pacotes%20simplificados.) [2](#ref2) , o diagrama de pacotes simplifica a leitura de sistemas complexos e torna visíveis suas dependências e relacionamentos de alto nível. Cada pacote pode conter elementos empacotáveis, como diagramas, documentos e outros pacotes, e relaciona-se a outros por meio de dependências, importações e extensões.

Neste artefato, procura-se apresentar o Diagrama de Pacotes da plataforma Galáxia Conectada, que visa ilustrar os principais agrupamentos funcionais e estruturais do sistema.

## Objetivos

Com o intuito de apresentar o Diagrama de Pacotes e destacar a estrutura modular do sistema, busca-se:

- Representar a organização lógica dos elementos do sistema em pacotes distintos;
- Evidenciar relações de dependência entre pacotes;
- Facilitar a compreensão da arquitetura em camadas da plataforma;
- Contribuir para a manutenibilidade, escalabilidade e reutilização dos componentes do software;

## Metodologia

Para a construção do diagrama, serão seguidas as etapas abaixo:

1. Serão analisados os seguintes artefatos para agrupamento e análise de informações:

- [Requisitos Funcionais e Não Funcionais elicitados - Elaborados na entrega 1](/Base/ArtefatoGeneralista/RequisitosElicitados.md);
- [Diagrama de Classe](/Modelagem/ModelagemEstatica/DiagramaClasses.md);
- [Diagrama de Componentes](/Modelagem/ModelagemEstatica/DiagramaComponentes.md);
- [Diagrama de Casos de Uso](/Modelagem/ModelagemOrganizacional/DiagramaCasosUso.md).

Após a análise dos dados, serão feitas as seguintes etapas:

1. Organização dos elementos identificados em pacotes temáticos.
2. Organização e compreensão das tependências entre os pacotes.
3. Modelagem do diagrama no Draw.io.

## Sobre o Diagrama de Pacotes

O Diagrama de Pacotes a seguir, elaborado com base nos princípios de [Diagrama de Pacotes: Definição, Componentes](https://gitmind.com/pt/diagrama-de-pacotes.html#:~:text=Um%20diagrama%20de%20pacotes%20pode,outros%20campos%20em%20pacotes%20simplificados.) [2](#ref2) e [Diagrama de Pacotes](https://docentes.ifrn.edu.br/diegooliveira/disciplinas/pds/aula-14-diagrama-de-pacotes) [5](#ref5), apresenta a organização arquitetural do sistema em módulos lógicos (Pacotes) e as suas interconexões. Com isso, a estrutura adota uma abordagem em camadas, separando Apresentacao (frontend) do Servidor (backend), o qual é subdividido em pacotes como Aplicacao, Dominio (regras de negócio/entidades), Infraestrutura (detalhes técnicos) e ServicosCompartilhados. Além disso, as Dependências são clarificadas por Estereótipos (<`<verbo>`>), como <`<usar>`> ou <`<chamar>`>, o qual declara a natureza das interações.

Para melhor compreensão dos diagramas, a figura 1 mostra a legenda;

<div align="center">
    Figura 1: Legenda do Diagrama de Estados
    <br>
    <img src="assets/Legendas/LegendaDiagramaPacote.drawio.png" width="500">
    <br>
    <b>Autor:</b> <a href="https://github.com/gab rile-lima258">Gabriel Lima</a>.
    <br>
</div>

## Elaboração do Diagrama

A estruturação da plataforma "Ingressou" em uma arquitetura modular e organizada é fundamental para sua compreensão e manutenibilidade, sendo o Diagrama de Pacotes a representação visual dessa organização lógica. Para fornecer um inventário claro e uma descrição detalhada de cada agrupamento funcional e técnico apresentado no referido diagrama, a Tabela 1 subsequente lista cada Pacote, sua Descrição concisa.

<summary><strong>Tabela 1:  Pacotes do Diagrama</strong></summary>

**Tabela 1:** Pacotes do Diagrama

# Diagrama de Pacotes - Sistema Ingressou

Esta tabela descreve a organização lógica do sistema em pacotes de altoível, seus subsistemas e as principais dependências entre eles, com base no diagrama de componentes fornecido.

| Pacote                          | Descrição                                                          | Rastreabilidade (Componentes / RFs / Classes-chave)                                                                                                                              |
| :------------------------------ | :------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **`Ingressou`**         | **Pacote raiz que engloba toda a aplicação.**                | **Aplicação completa.**                                                                                                                                                  |
| `  Apresentacao`              | Camada de interface com o usuário (SPA/PWA web).                    | Componente:`WebUI`/`CheckinPWA`. RNF01 Acesso via browser; RNF09 Offline. Classes: *ViewModels*, *DTOs*.                                                                 |
| `  Servidor`                  | Agrupa todos os pacotes do backend (aplicação, domínio, infra).   | Pacote:`Backend`.                                                                                                                                                              |
| `    GatewayAPI`              | Borda HTTP (roteia/valida, CORS, auth básica), entrada do frontend. | Componente:`APIGateway`. Suporta indiretamente todos RFs via endpoints.                                                                                                        |
| `    Aplicacao`               | Orquestra casos de uso, coordena Domínio ↔ Infra/Serviços.        | Serviços:`AuthService`, `UserService`, `EventService`, `OrderService`, `PaymentService`, `TicketService`, `CheckinService`, `CouponService`, `ReportService`. |
| `      Aplicacao.Auth`        | Casos de uso de cadastro/login/sessão.                              | RF01–RF04. Classes:`CadastrarUsuario`, `Login`, `GerarOTP`, `RenovarToken`.                                                                                             |
| `      Aplicacao.Usuarios`    | Casos de uso de perfil/conta/roles.                                  | RF05. Classes:`AtualizarPerfil`, `VincularSocial`.                                                                                                                           |
| `      Aplicacao.Eventos`     | Casos de uso de catálogo/lotes/exibição.                          | (Catálogo/descoberta). Classes:`CriarEvento`, `PublicarEvento`, `GerirLotes`.                                                                                             |
| `      Aplicacao.Pedidos`     | Orquestra carrinho/checkout/pedido.                                  | RF de compra. Classes:`AdicionarAoCarrinho`, `Checkout`, `ConfirmarPedido`.                                                                                                |
| `      Aplicacao.Pagamentos`  | Inicia/consulta/confirma pagamento; processa webhooks.               | RF de pagamento. Classes:`IniciarPagamento`, `ConciliaTransacao`, `WebhookPagamentoHandler`.                                                                               |
| `      Aplicacao.Ingressos`   | Emissão/carteira/transferência de ingresso.                        | Classes:`EmitirIngressos`, `TransferirIngresso`.                                                                                                                             |
| `      Aplicacao.Checkin`     | Validação em portaria (online/offline, sincronização).           | **RF36–RF39**. Classes: `ValidarQR`, `SincronizarCheckins`.                                                                                                           |
| `      Aplicacao.Cupons`      | Gestão/aplicação de cupons e atribuição de influenciador.       | Classes:`CriarCupom`, `AplicarCupom`.                                                                                                                                        |
| `      Aplicacao.Relatorios`  | Consultas e KPIs operacionais.                                       | Classes:`RelatorioVendas`, `KPIEventos`.                                                                                                                                     |
| `    Dominio`                 | Entidades, VOs, regras de negócio e*ports* (interfaces).          | Núcleo do modelo.                                                                                                                                                               |
| `      Dominio.Compartilhado` | Tipos/VOs/utilitários comuns.                                       | Classes:`Money`, `Email`, `CPF`, `Id`, `Clock`, `Result`.                                                                                                            |
| `      Dominio.Auth`          | Usuário/autenticação/credenciais/tokens.                          | Classes:`Usuario`, `Credencial`, `TokenRefresh`.                                                                                                                           |
| `      Dominio.Usuarios`      | Perfil, preferências.                                               | Classes:`UsuarioPerfil`, `Preferencias`.                                                                                                                                     |
| `      Dominio.Eventos`       | Evento, lote, setor, preço.                                         | Classes:`Evento`, `Lote`, `Setor`, `Preco`.                                                                                                                              |
| `      Dominio.Pedidos`       | Pedido, item, estados do ciclo de vida.                              | Classes:`Pedido`, `ItemPedido`.                                                                                                                                              |
| `      Dominio.Pagamentos`    | Pagamento, transação, repasse.                                     | Classes:`Pagamento`, `Transacao`, `Repasse`.                                                                                                                               |
| `      Dominio.Ingressos`     | Ingresso, carteira, assinatura de QR.                                | Classes:`Ingresso`, `Carteira`, `QrSignature`.                                                                                                                             |
| `      Dominio.Checkin`       | Registro e regras de validação de entrada.                         | Classes:`CheckinRegistro`, `ValidadorQr`.                                                                                                                                    |
| `      Dominio.Cupons`        | Cupom e atribuição a pedido/influenciador.                         | Classes:`Cupom`, `AtribuicaoInfluenciador`.                                                                                                                                  |
| `      Dominio.Relatorios`    | Agregados de leitura/modelos de consulta.                            | Classes:*Views* de leitura.                                                                                                                                                    |
| `    ServicosCompartilhados`  | Serviços transversais reutilizáveis.                               | Componentes:`ServicoNotificacoes`, `ServicoBusca`, `ServicoLocalizacao`, `ServicoConfiguracao`, `ServicoMonitoramento`, `ServicoCache`.                              |
| `      Notificacoes`          | Envio de e-mail/WhatsApp/WebPush.                                    | Classes:`Mensagem`, `Template`.                                                                                                                                              |
| `      Busca`                 | Indexação/consulta.                                                | Classes:`Indexador`, `BuscaConteudo`.                                                                                                                                        |
| `      Localizacao`           | i18n/idiomas.                                                        | RNF (internacionalização).                                                                                                                                                     |
| `      Configuracao`          | Leitura de*feature flags* e parâmetros.                           | RNF.                                                                                                                                                                             |
| `      Monitoramento`         | Logs, métricas, tracing.                                            | RNF05 Observabilidade.                                                                                                                                                           |
| `      Cache`                 | Abstração de cache.                                                | RNF02 Performance.                                                                                                                                                               |
| `    Infraestrutura`          | Implementações técnicas (DB, filas, storage, gateways).           | Adapters:`Persistencia`, `Mensageria`, `Storage`, `Pagamentos`, `Email`, `Whatsapp`, `NFSe`, `Seguranca`.                                                        |
| `      Persistencia`          | Repositórios/ORM/consultas.                                         | Repositórios:`UserRepo`, `OrderRepo`, `TicketRepo`, …                                                                                                                    |
| `      Mensageria`            | Publicação/consumo de eventos internos/externos.                   | Filas/tópicos de `Pedido/Notificação/Webhook`.                                                                                                                              |
| `      Storage`               | Arquivos/objetos (QR, imagens, comprovantes).                        | `S3Files`, `QrStore`, `ImageStore`.                                                                                                                                        |
| `      Pagamentos`            | Gateways (Pagar.me/Mercado Pago).                                    | `PaymentGatewayAdapter`.                                                                                                                                                       |
| `      Email`                 | Provedor de e-mail (SES/SendGrid).                                   | `EmailAdapter`.                                                                                                                                                                |
| `      Whatsapp`              | Provedor WhatsApp (Twilio/Zenvia).                                   | `WhatsappAdapter`.                                                                                                                                                             |
| `      NFSe`                  | Emissão/consulta de nota fiscal.                                    | `NFSeClientAdapter`.                                                                                                                                                           |
| `      Seguranca`             | Cripto/JWT/hashing.                                                  | `JwtProvider`, `PasswordHasher`.                                                                                                                                             |
| `    Observabilidade`         | Configuração de métricas/log/trace.                               | Integrações com Prometheus/Grafana/ELK.                                                                                                                                        |

`<b>` Autor: `</b>` `<a href="https://github.com/gabriel-lima258">`Gabriel Lima`</a>`.

<summary><strong>Tabela 2:  Pacotes de Dependência</strong></summary>

**Tabela 2:** Pacotes de Dependência

# Dependência de Pacotes - Sistema Ingressou

Esta tabela descreve a organização lógica do sistema em pacotes de altoível, seus subsistemas e as principais dependências entre eles, com base no diagrama de componentes fornecido.

| Pacote Dependente (Cliente)                       | Estereótipo        | Pacote Fornecedor (Destino)                       | Justificativa / Explicação                                           |
| :------------------------------------------------ | :------------------ | :------------------------------------------------ | :--------------------------------------------------------------------- |
| `Apresentacao`                                  | `<<chamar>>`      | `Servidor.GatewayAPI`                           | SPA/PWA consome endpoints REST/HTTP do gateway.                        |
| `Servidor.GatewayAPI`                           | `<<rotear>>`      | `Servidor.Aplicacao.*`                          | Controladores da borda encaminham para casos de uso.                   |
| `Servidor.Aplicacao.*`                          | `<<usar>>`        | `Servidor.Dominio.*`                            | Casos de uso manipulam entidades e regras de negócio.                 |
| `Servidor.Aplicacao.Auth`                       | `<<usar>>`        | `ServicosCompartilhados.Monitoramento`          | Auditar logins/erros; métricas.                                       |
| `Servidor.Aplicacao.Pedidos`                    | `<<orquestrar>>`  | `Aplicacao.Pagamentos`, `Aplicacao.Ingressos` | Checkout → pagamento → emissão de ingressos.                        |
| `Servidor.Aplicacao.Checkin`                    | `<<usar>>`        | `Dominio.Checkin`                               | Validação e registro de entradas.                                    |
| `Servidor.Aplicacao.Cupons`                     | `<<usar>>`        | `Dominio.Cupons`                                | Aplicação/validação de cupom.                                      |
| `Servidor.Aplicacao.Relatorios`                 | `<<consultar>>`   | `Dominio.Relatorios`                            | Consultas e agregações de leitura.                                   |
| `Servidor.Aplicacao.*`                          | `<<persistir>>`   | `Infraestrutura.Persistencia`                   | Repositórios implementam*ports* de acesso a dados.                  |
| `Servidor.Aplicacao.*`                          | `<<publicar>>`    | `Infraestrutura.Mensageria`                     | Eventos de domínio/integração (notificação, webhooks).            |
| `Servidor.Aplicacao.Ingressos`                  | `<<armazenar>>`   | `Infraestrutura.Storage`                        | Armazenar QR codes/arquivos.                                           |
| `Servidor.Aplicacao.Pagamentos`                 | `<<integrar>>`    | `Infraestrutura.Pagamentos`                     | Solicitar autorizações/estornos e receber webhooks.                  |
| `Servidor.Aplicacao`                            | `<<notificar>>`   | `ServicosCompartilhados.Notificacoes`           | Envio de e-mails/WhatsApp/push.                                        |
| `ServicosCompartilhados.Busca`                  | `<<indexar>>`     | `Infraestrutura.Persistencia`                   | Indexar/consultar dados.                                               |
| `ServicosCompartilhados.Localizacao`            | `<<ler>>`         | `Infraestrutura.Persistencia`                   | Textos/idiomas armazenados.                                            |
| `ServicosCompartilhados.Monitoramento`          | `<<coletar>>`     | `Observabilidade`                               | Logs/métricas/traces exportados.                                      |
| `Dominio.*`                                     | `<<usar>>`        | `Dominio.Compartilhado`                         | VOs/utilitários comuns (`Money`, `CPF`, `Email`, `Id`, etc.). |
| `Infraestrutura.Persistencia`                   | `<<implementar>>` | `Dominio.*`                                     | Implementa interfaces de repositório definidas no domínio.           |
| `Infraestrutura.Pagamentos/Email/Whatsapp/NFSe` | `<<implementar>>` | `ServicosCompartilhados`/`Aplicacao`          | Adaptadores concretos de*ports* outbound (gateways externos).        |
| `Infraestrutura.Seguranca`                      | `<<fornecer>>`    | `Aplicacao.Auth`                                | JWT/hashing/cripto para autenticação/sessão.                        |
| `Apresentacao.CheckinPWA`                       | `<<sincronizar>>` | `Aplicacao.Checkin`                             | Envia pacotes de validação offline → online; recebe atualizações. |

`<b>` Autor: `</b>` `<a href="https://github.com/gabriel-lima258">`Gabriel Lima`</a>`.

## Diagrama de Pacotes Simplificado

Para complementar a visão detalhada e oferecer uma compreensão mais rápida da estrutura de alto nível, apresenta-se também um Diagrama de Pacotes simplificado. Esta versão foca nos principais agrupamentos lógicos (como as camadas Apresentacao, Servidor, e os subsistemas principais dentro do backend) e nas dependências mais críticas.

**Observação:** Para visualizar a imagem em mamior definição, clique nela.

<div align="center">
    <b>Figura 2:</b> o Diagrama de Pacotes - Simplificado
    <br>
    <img src="assets/Modelagem/Estatica/pacotes.pdf" width="1000">
    <br>
    <b>Autor:</b> <a href="https://github.com/gabriel-lima258">Gabriel Lima</a>.
</div>

<p><strong>Observação:</strong> Caso deseje visualizar ou baixar em PDF, clique aqui: 
<a href="assets/Modelagem/Estatica/pacotes.pdf">PDF do Diagrama de Pacotes - Simplificado</a></p>

## Conclusão

Em suma, o Diagrama de Pacotes detalhado oferece um mapa estruturado da arquitetura lógica da plataforma "Ingressou". Desse modo, a organização modular em pacotes com responsabilidades bem definidas, como Apresentacao, Aplicacao, Dominio e Infraestrutura, juntamente com a visualização explícita das dependências entre eles é fundamental para gerenciar a complexidade do sistema. Essa abordagem facilita a compreensão da estrutura geral e a localização de funcionalidades como também promove um guia essencial para o desenvolvimento e a evolução coesa do código-fonte.

## Bibliografia

`<a name="ref1"></a>`
[1] APOSTILA UML. Seção sobre representação de Pacotes. Disponibilizada pela professora. Acesso em: 5 maio 2025.

`<a name="ref2"></a>`
[2] Diagrama de Pacotes: Definição, Componentes e Exemplos. Disponível em: https://gitmind.com/pt/diagrama-de-pacotes.html. Acesso em: 5 maio 2025.

`<a name="ref3"></a>`
[3] LUCIDCHART. Tudo sobre diagramas de pacotes UML. Disponível em: https://www.lucidchart.com/pages/pt/diagrama-de-pacotes-uml. Acesso em: 5 maio 2025.

`<a name="ref4"></a>`
[4] VISUAL PARADIGM. What is Package Diagram? Disponível em: https://www.visual-paradigm.com/guide/uml-unified-modeling-language/what-is-package-diagram/. Acesso em: 5 maio 2025.

`<a name="ref5"></a>`
[5] OLIVEIRA, Diego. Projeto de Desenvolvimento de Software – Aula 14: Diagrama de Pacotes. Disponível em: https://docentes.ifrn.edu.br/diegooliveira/disciplinas/pds/aula-14-diagrama-de-pacotes. Acesso em: 5 maio 2025.

## Histórico de versão

| Versão | Alteração               | Responsável | Data       |
| ------- | ------------------------- | ------------ | ---------- |
| 1.0     | Elaboração do documento | Gabriel Lima | 22/10/2024 |
