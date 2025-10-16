# Benchmarking em Relação a Comunicação e Engajamento com Usuários

## Sumário

* [Sympla](#sympla)
* [Eventbrite](#eventbrite)
* [Bilheteria Digital](#bilheteria-digital)
* [Hotmart](#hotmart)
* [Even3](#even3)
* [Requisitos Elicitados](#requisitos-elicitados)
  * [Requisitos Funcionais](#requisitos-funcionais)
  * [Requisitos Não-Funcionais](#requisitos-não-funcionais)

---

### [Sympla](https://www.sympla.com.br)

<div align="center">
    Figura 1: Sympla — Comunicação com Usuários (ilustrativo)
    <br>
    <img src="assets/Benchmarking/sympla.png" width="560" alt="Sympla - comunicação e engajamento">
    <br>
    <b>Fonte:</b> <a href="https://www.sympla.com.br">Sympla</a>.
    <br>
</div>

#### Foco observado
Canal direto entre plataforma, organizador e participante, com **notificações automatizadas** e **comunicação segmentada**.

#### Recursos-chave
- Envio automático de e-mails: confirmação, lembrete e pós-evento.
- Mensagens personalizadas por evento.
- Notificações sobre mudanças, cancelamentos ou reembolsos.
- Central de ajuda e chat de suporte automatizado.
- Push notifications no aplicativo Sympla.

#### Pontos positivos
- Fluxo automatizado e bem estruturado.
- Comunicação clara e padronizada.
- Canal direto entre organizador e comprador.

#### Pontos a observar
- Customização visual dos e-mails é limitada.

---

### [Eventbrite](https://www.eventbrite.com.br)

<div align="center">
    Figura 2: Eventbrite — E-mail Marketing e Engajamento (ilustrativo)
    <br>
    <img src="assets/Benchmarking/evenbrite.png" width="560" alt="Eventbrite - e-mail marketing e engajamento">
    <br>
    <b>Fonte:</b> <a href="https://www.eventbrite.com.br">Eventbrite</a>.
    <br>
</div>

#### Foco observado
Gestão de comunicação completa com **segmentação avançada** e **integrações de marketing** (Mailchimp, Meta, Hubspot).

#### Recursos-chave
- Envio de campanhas personalizadas por público.
- Segmentação de usuários com base em evento, data e status de compra.
- Integrações com CRMs e ferramentas de marketing.
- Automação de lembretes e pós-evento.

#### Pontos positivos
- Comunicação omnichannel (e-mail, SMS, notificações).
- Alta capacidade de personalização.
- Integrações poderosas com ferramentas externas.

#### Pontos a observar
- Ferramenta mais voltada para grandes eventos e produtores profissionais.

---

### [Bilheteria Digital](https://www.bilheteriadigital.com)

<div align="center">
    Figura 3: Bilheteria Digital — Central do Cliente (ilustrativo)
    <br>
    <img src="assets/Benchmarking/bilheteria.png" width="560" alt="Bilheteria Digital - suporte e comunicação">
    <br>
    <b>Fonte:</b> <a href="https://www.bilheteriadigital.com">Bilheteria Digital</a>.
    <br>
</div>

#### Foco observado
Canal de suporte prático e centralizado, com **e-mails automáticos** e **atendimento rápido**.

#### Recursos-chave
- Notificações automáticas por e-mail (compra, cancelamento, reembolso).
- Central de suporte via formulário e chatbot.
- Comunicação básica entre organizador e participante via painel.

#### Pontos positivos
- Simplicidade e eficiência no pós-venda.
- Tempo de resposta rápido.

#### Pontos a observar
- Falta de comunicação via push/app.
- E-mails com layout pouco personalizável.

---

### [Hotmart](https://www.hotmart.com/)

<div align="center">
    Figura 4: Hotmart — Comunicação e Automação (ilustrativo)
    <br>
    <img src="assets/Benchmarking/hotmart.png" width="560" alt="Hotmart - automação e suporte">
    <br>
    <b>Fonte:</b> <a href="https://www.hotmart.com">Hotmart</a>.
    <br>
</div>

#### Foco observado
Sistema de **automação de comunicação**, **integração com e-mail marketing** e **mensagens condicionais** por gatilho de ação.

#### Recursos-chave
- Automação de mensagens baseada em gatilhos (compra, login, visualização).
- Segmentação de público.
- Notificações dentro da plataforma.
- Chatbot inteligente de suporte.

#### Pontos positivos
- Automação eficiente.
- Alto nível de personalização.
- Comunicação humanizada e contextualizada.

#### Pontos a observar
- Requer configuração técnica inicial.

---

### [Even3](https://www.even3.com.br)

<div align="center">
    Figura 5: Even3 — Comunicação de Eventos Acadêmicos (ilustrativo)
    <br>
    <img src="assets/Benchmarking/even.png" width="560" alt="Even3 - comunicação acadêmica e notificações">
    <br>
    <b>Fonte:</b> <a href="https://www.even3.com.br">Even3</a>.
    <br>
</div>

#### Foco observado
Comunicação voltada à área acadêmica, com **e-mails personalizados**, **painel de notificações** e **mensagens em massa**.

#### Recursos-chave
- Envio de mensagens personalizadas a grupos (ex: autores, avaliadores).
- Histórico de comunicações enviadas.
- Central de notificações internas.
- Suporte integrado com base de conhecimento.

#### Pontos positivos
- Comunicação estruturada e segmentada.
- Central interna de mensagens eficiente.

#### Pontos a observar
- Sem integração direta com canais externos (SMS ou WhatsApp).

---

## Requisitos Elicitados

> Requisitos derivados com foco em **comunicação, engajamento e suporte ao usuário** da plataforma **Ingressou**.

### Requisitos Funcionais

| Código | Requisito Funcional                                                               | Objetivo                                                        | Origem (referência)          |
|--------|------------------------------------------------------------------------------------|-----------------------------------------------------------------|------------------------------|
| RF-CM-01 | Enviar notificações automáticas por e-mail (confirmação, lembrete, pós-evento).   | Garantir comunicação básica com o usuário.                      | Sympla, Bilheteria Digital   |
| RF-CM-02 | Permitir envio de mensagens personalizadas pelo produtor.                         | Engajamento direto com participantes.                           | Sympla, Even3                |
| RF-CM-03 | Criar campanhas de marketing segmentadas (data, cidade, tipo de evento).          | Aumentar engajamento e vendas.                                  | Eventbrite, Hotmart          |
| RF-CM-04 | Enviar notificações push pelo aplicativo mobile.                                 | Comunicação instantânea com usuários ativos.                    | Sympla                       |
| RF-CM-05 | Integrar com ferramentas externas de e-mail marketing (ex: Mailchimp, Brevo).     | Ampliar alcance e automação.                                    | Eventbrite, Hotmart          |
| RF-CM-06 | Disponibilizar histórico de comunicações enviadas por evento/usuário.             | Controle e rastreabilidade.                                     | Even3                        |
| RF-CM-07 | Oferecer central de suporte com chatbot e base de conhecimento.                   | Reduzir carga de atendimento humano.                            | Hotmart, Bilheteria Digital  |
| RF-CM-08 | Enviar mensagens automáticas com base em gatilhos (ex: carrinho abandonado).      | Recuperar conversões perdidas.                                  | Hotmart, Eventbrite          |
| RF-CM-09 | Permitir comunicação via painel entre organizador e comprador.                    | Resolver dúvidas específicas sobre o evento.                    | Sympla, Bilheteria Digital   |
| RF-CM-10 | Permitir desinscrição (opt-out) de comunicações promocionais.                     | Cumprir LGPD e boas práticas.                                   | Padrão do setor              |

---

### Requisitos Não-Funcionais

| Código | Requisito Não-Funcional                                                           | Objetivo                                                          | Origem (referência)     |
|--------|------------------------------------------------------------------------------------|-------------------------------------------------------------------|--------------------------|
| RNF-CM-01 | Garantir entrega de e-mails em até 2 minutos após disparo (P90).                 | Garantir comunicação em tempo hábil.                              | Sympla, Eventbrite       |
| RNF-CM-02 | Disponibilidade mínima de 99,5% no módulo de notificações.                       | Estabilidade de comunicação.                                      | Hotmart, Sympla          |
| RNF-CM-03 | Utilizar provedores com SPF, DKIM e DMARC configurados.                          | Garantir alta taxa de entrega de e-mails.                         | Boas práticas            |
| RNF-CM-04 | Armazenar logs de mensagens por no mínimo 90 dias.                               | Controle e auditoria.                                             | Even3, Bilheteria Digital|
| RNF-CM-05 | Painel e templates compatíveis com mobile e dark mode.                           | Melhorar experiência visual.                                      | Hotmart, Eventbrite      |
| RNF-CM-06 | Chatbot treinado com base nas FAQs dos eventos mais recentes.                    | Atendimento automatizado e eficiente.                             | Hotmart                 |
| RNF-CM-07 | Permitir envio simultâneo para até 10.000 usuários sem degradação de performance. | Escalabilidade em campanhas de grande porte.                      | Eventbrite, Hotmart      |
| RNF-CM-08 | Cumprir LGPD e normas de consentimento explícito.                                | Garantir privacidade e conformidade legal.                        | Padrão do setor          |

---


## Histórico de versão

| Versão | Alteração                                             | Responsável  | Data       |
|-------:|--------------------------------------------------------|--------------|------------|
| 1.0    | Criação do benchmarking “Comunicação e Engajamento com Usuários” | Gabriel Lima | 15/10/2025 |
