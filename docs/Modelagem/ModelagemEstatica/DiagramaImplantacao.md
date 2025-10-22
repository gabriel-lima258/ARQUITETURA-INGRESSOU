# Diagrama de Implantação


> **Versão:** 1.0  
> **Data:** Outubro de 2025  
> **Autor:** Gabriel Lima  
> **Projeto:** Ingressou — Plataforma Web de Venda e Gestão de Ingressos  

---

## Sumário

- [Introdução](#introdução)  
- [Objetivos](#objetivos)  
- [Metodologia](#metodologia)  
- [Tabela de Análise](#Tabela-de-Análise)  
- [Diagrama de Implantação](#Diagrama-de-Implantação)  
- [Conclusão](#conclusão)  
- [Bibliografia](#bibliografia)  
- [Histórico de versão](#histórico-de-versão)  

## Introdução

O diagrama de implantação, segundo o artigo [O que é um diagrama de implementação?](https://www.lucidchart.com/pages/pt/o-que-e-diagrama-de-implementacao-uml) [2](#ref2), é um tipo de diagrama estrutural da UML que representa a implementação física de artefatos de software sobre os componentes de hardware. Neste diagrama, utilizam-se elementos gráficos como nódulos (caixas tridimensionais) para representar dispositivos ou ambientes de execução de software, e os artefatos são os produtos gerados pelo desenvolvimento, como arquivos executáveis, bibliotecas ou scripts. 

Com base nisso, o artigo [O Guia Fácil de Diagramas de Implantação UML](https://creately.com/blog/pt/diagrama/tutorial-do-diagrama-de-implantacao/#:~:text=Um%20diagrama%20de%20implanta%C3%A7%C3%A3o%20%C3%A9,software%20f%C3%ADsico%20de%20um%20sistema.) [1](#ref1) fala que esse tipo de diagrama é essencial para entender a arquitetura de execução do sistema ao evidenciar tanto o hardware necessário quanto o middleware que interliga os elementos da solução. Assim, no contexto do projeto **Ingressou**, o diagrama de implantação é importante pois permite visualizar de forma clara como a plataforma será distribuída fisicamente — por exemplo, o servidor onde será hospedado os serviços.

## Objetivos

Com isso, ao elaborar o diagrama de implantação, busca-se os seguintes objetivos:

- Representar a arquitetura física de execução do sistema **Ingressou**.

- Evidenciar os ambientes de hardware e software onde os componentes serão implantados.

- Demonstrar a distribuição dos artefatos e os canais de comunicação entre os nódulos.

## Metodologia:

A elaboração do diagrama de implantação será conduzida com o apoio da ferramenta Draw.io ao utilizar como base os materiais previamente desenvolvidos ao longo do projeto. Com isso, a construção seguirá uma abordagem sistemática, a partir da análise dos requisitos, diagramas e estrutura do sistema. Assim, as etapas da metodologia:

1. Inicialmente será realizada uma análise do material base a partir de:

  - [Requisitos elicitados e documentados na primeira etapa](Base/ArtefatoGeneralista/RequisitosElicitados.md);
  - [Diagrama de Classes](Modelagem/ModelagemEstatica/DiagramaClasses.md);
  - [Diagrama de Componentes](Modelagem/ModelagemEstatica/DiagramaComponentes.md);

2. Com base nessa análise, será criada uma tabela de apoio organizando os tipos de nós (hardware, software, containers etc.) necessários para a modelagem.
3. Ao utilizar a ferramenta **Draw.io**, será elaborada a versão inicial do diagrama de implantação, com identificação dos nós, artefatos e relações.
4. Após a construção, o diagrama passará por uma fase de [verificação](Modelagem/IniciativasExtras/Verificacao/VerificacaoDiagramaImplantacao.md), com o objetivo de garantir sua coerência.

## Tabela de Análise

A tabela 1 abaixo foi elaborada para auxiliar na análise dos tipos de nós necessários para a construção do Diagrama de Implantação do projeto **Ingressou**. 


<details>
  <summary><strong>Tabela 1: Base para Diagrama de Implantação</strong></summary>

**Tabela 1**: Base para Diagrama de Implantação

# Diagrama de Implantação - Sistema Ingressou

Esta tabela descreve os nós de hardware e software onde os artefatos (componentes) do sistema "Ingressou" serão implantados.

| # | Tipo de Nó | Nome do Nó | <<Estereótipo>> / Ícone Usado | Descrição / Responsabilidade | Artefatos / Componentes Implantados | Ambiente de Execução / Software Chave | Comunicação Principal (Para/De, Protocolo) | Requisitos Atendidos |
|---|:---|:---|:---|:---|:---|:---|:---|:---|
| 01 | Dispositivo Usuário | `Navegador Web (Cliente/Produtor)` | `<<device>>` | Acessa a SPA (Single Page Application) para compra de ingressos e o painel do produtor para gestão de eventos. | `ingressou-webapp.js` (SPA)<br>`Busca.js`<br>`Dashboard.js` | Navegador Web (Chrome, Firefox, Safari, etc.) | [Para] API Gateway (HTTPS) | (Não fornecidos) |
| 02 | Dispositivo Usuário | `Dispositivo Móvel (Staff)` | `<<device>>` | Executa o PWA (Progressive Web App) dedicado para a equipe de staff realizar o check-in dos ingressos no evento. | `CheckinApp.js` (PWA) | Navegador Web Móvel (Suporte a PWA) | [Para] API Gateway (HTTPS) | (Não fornecidos) |
| 03 | Servidor / Rede | `API Gateway` | `<<gateway>>` | Ponto de entrada único para todas as requisições. Aplica segurança, roteia para os microsserviços corretos e limita a taxa de tráfego. | `api-gateway-config.yml` | Nginx / Kong / Spring Cloud Gateway | [De] Dispositivos de Usuário (HTTPS)<br>[Para] Firewall (TCP/IP) | (Não fornecidos) |
| 04 | Rede / Segurança | `Firewall` | `<<firewall>>` | Controla e filtra o tráfego de rede entre a zona pública (Gateway) e a zona privada (Serviços Internos e Banco de Dados). | - | Software de Firewall (iptables, WAF) | [De] API Gateway (TCP/IP)<br>[Para] Cluster de Microsserviços (TCP/IP)<br>[Para] SGBD (TCP/IP) | (Não fornecidos) |
| 05 | Servidor | `Cluster de Microsserviços` | `<<executionEnvironment>>` | Ambiente orquestrado (ex: Kubernetes) que executa os contêineres dos microsserviços com a lógica de negócio da aplicação. | `user-service.jar`<br>`auth-service.jar`<br>`jwt-service.jar`<br>`event-service.jar`<br>`ticket-service.jar`<br>`category-service.jar`<br>`payment-service.jar`<br>`order-service.jar`<br>`coupon-service.jar`<br>`checkin-service.jar`<br>`notification-service.jar`<br>`qrcode-service.jar` | Docker / Kubernetes + JRE (Java Runtime Environment) | [De] Firewall (TCP/IP)<br>[Para] SGBD (TCP/IP)<br>[Para] Cache (TCP/IP)<br>[Para] Broker de Mensagens (AMQP)<br>[Para] Serviços Externos (HTTPS) | (Não fornecidos) |
| 06 | Servidor | `SGBD (Principal)` | `<<database>>` | Armazena e gerencia os dados relacionais principais: usuários, eventos, pedidos, ingressos, pagamentos, etc. | `ingressou-db-schema.sql` (Schema do Banco) | PostgreSQL | [De] Firewall (TCP/IP)<br>[De] Cluster de Microsserviços (TCP/IP) | (Não fornecidos) |
| 07 | Servidor | `Servidor de Cache` | `<<database>>` | Armazena dados de acesso muito frequente ou temporários (ex: sessões de usuário, dados públicos de eventos) para acelerar consultas. | `redis-config` | Redis | [De] Cluster de Microsserviços (TCP/IP) | (Não fornecidos) |
| 08 | Servidor | `Broker de Mensagens` | `<<server>>` | Gerencia filas e tópicos para comunicação assíncrona entre microsserviços (ex: confirmação de pedido, envio de notificações). | `rabbitmq-config` | RabbitMQ | [De/Para] Cluster de Microsserviços (AMQP) | (Não fornecidos) |
| 09 | Serviço Externo | `Gateway de Pagamento` | `<<external>>` | Nó externo responsável pelo processamento seguro de transações financeiras (cartão de crédito, PIX, etc.). | N/A (API Externa) | Serviço de Terceiro (Ex: Stripe, PagSeguro, etc.) | [De] payment-service.jar (HTTPS/API) | (Não fornecidos) |
| 10 | Serviço Externo | `Serviços de Notificação` | `<<external>>` | Nós externos responsáveis pelo envio de comunicações aos usuários. | N/A (API Externa) | Provedor de Email (Ex: SendGrid)<br>Provedor de WhatsApp (Ex: Twilio) | [De] notification-service.jar (HTTPS/API) | (Não fornecidos) |


<b> Autor: </b> <a href="https://github.com/gabriel-lima258">Gabriel Lima</a>.

</details>

## Diagrama de Implantação

Para melhor compreensão do diagrama, a figura 1 mostra a legenda;

<div align="center">
    Figura 1: Legenda do Diagrama de Implantação
    <br>
    <img src="https://raw.githubusercontent.com/UnBArqDsw2025-1-Turma02/2025.1_T02_G9_GalaxiaConectada_Entrega02/75556a84c6b754819462bcc143af4787c4a62dde/docs/Modelagem/Imagens/LegendaDiagramaImplantacao.drawio.png" width="500">
    <br>
    <b>Autor:</b> <a href="https://github.com/gabriel-lima258">Gabriel Lima</a>.
    <br>
</div>

--- 

<div align="center">
    Figura 2: o Diagrama de Implantação
    <br>
    <img src="assets/Modelagem/Estatica/Implantação.pdf" width="1000">
    <br>
    <b>Autor:</b> <a href="https://github.com/gabriel-lima258">Gabriel Lima</a>.
    <br>
</div>

**Observação:** Caso deseje visualizar ou baixar em PDF, clique aqui [PDF](assets/Modelagem/Estatica/Implantação.pdf)


## Conclusão

A construção do Diagrama de Implantação para o projeto **Ingressou** teve como base a Tabela 1, a qual sistematizou os principais nós da infraestrutura de execução da aplicação e incluiu dispositivos de usuário, servidores, rede e banco de dados. Portanto, esse mapeamento permitiu representar, de forma estruturada, como os componentes do sistema são distribuídos fisicamente em seus respectivos ambientes de execução. 

## Bibliografia

<a name="ref1"></a>
[1] CREATELY. O Guia Fácil de Diagramas de Implantação UML. Creately Blog, 2024. Disponível em: https://creately.com/blog/pt/diagrama/tutorial-do-diagrama-de-implantacao/. Acesso em: 6 mai. 2025.

<a name="ref2"></a>
[2] EDRAWSOFT. Exemplos de Diagrama de Implantação UML. Edraw, 2024. Disponível em: https://www.edrawsoft.com/pt/deployment-chart-example.html. Acesso em: 28 abr. 2025.

<a name="ref3"></a>
[3] IBM CORPORATION. Diagramas de implantação. IBM Documentation, 2024. Disponível em: https://www.ibm.com/docs/pt-br/rsas/7.5.0?topic=topologies-deployment-diagrams. Acesso em: 28 abr. 2025.

<a name="ref4"></a>
[4] LUCID SOFTWARE INC. O que é diagrama de implementação UML. Lucidchart, 2024. Disponível em: https://www.lucidchart.com/pages/pt/o-que-e-diagrama-de-implementacao-uml. Acesso em: 28 abr. 2025.

<a name="ref5"></a>
[5] MAURO DE BONI. Tutorial Draw.io: Como Fazer Diagrama de Implantação da UML. YouTube, 2023. Disponível em: https://www.youtube.com/watch?v=eFFq3SLMQJ4. Acesso em: 30 abr. 2025.

<a name="ref6"></a>
[6] PROFESSOR PAIVA. Curso de UML - Diagrama de Implantação. YouTube, 2022. Disponível em: https://www.youtube.com/watch?v=DgERD0HgggQ. Acesso em: 30 abr. 2025.

<a name="ref7"></a>
[7] UML-DIAGRAMS. Deployment Diagrams Overview. UML Diagrams.org, 2024. Disponível em: https://www.uml-diagrams.org/deployment-diagrams-overview.html. Acesso em: 28 abr. 2025.

<a name="ref8"></a>
[8] VISUAL PARADIGM. What is Deployment Diagram?. Visual Paradigm Guide, 2024. Disponível em: https://www.visual-paradigm.com/guide/uml-unified-modeling-language/what-is-deployment-diagram/. Acesso em: 28 abr. 2025.


## Histórico de versão

| Versão | Alteração | Responsável | Data |
| - | - | - | - |
| 1.0 | Elaboração do documento| Gabriel Lima | 22/10/2025 |