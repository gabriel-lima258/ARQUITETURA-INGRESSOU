# Benchmarking

## Sumário

* [Introdução](#Introdução)
* [Objetivos](#Objetivos)
* [Metodologia](#Metodologia)
* [Requisitos Elicitados](#Requisitos-Elicitados)
  * [Requisitos Funcionais](#Requisitos-Funcionais)
  * [Requisitos Não Funcionais](#Requisitos-Não-Funcionais)
* [Conclusão](#Conclusão)
* [Bibliografia](#Bibliografia)
* [Histórico de versão](#Histórico-de-versão)

---

## Introdução

O **benchmarking**, segundo Camp (1989), é um processo contínuo de análise comparativa entre produtos e serviços, com o propósito de **identificar boas práticas de mercado e adaptá-las para otimizar o desempenho de novos sistemas**.  

No contexto digital, essa técnica permite compreender **tendências tecnológicas, estratégias de usabilidade, políticas de cobrança e diferenciais competitivos** de plataformas consolidadas.  

Neste documento, foi conduzida uma **análise comparativa entre sistemas de venda e gestão de ingressos** a fim de **nortear o desenvolvimento da plataforma Ingressou**, que visa unir **tecnologia, segurança e experiência fluida** para produtores e consumidores de eventos.

---

## Objetivos

O principal objetivo deste benchmarking é **analisar criticamente as plataformas de venda de ingressos e eventos mais relevantes do mercado brasileiro e internacional**, identificando:

- Funcionalidades essenciais e diferenciais;
- Modelos de monetização e taxas de serviço;
- Experiências de usabilidade e fluxo de compra;
- Práticas de segurança, transparência e comunicação com o usuário;
- Estratégias de fidelização, como cashback e promoções.

A partir dessa análise, busca-se **extrair requisitos e boas práticas** que possam ser incorporadas à **arquitetura e ao design funcional da Ingressou**.

---

## Metodologia

A metodologia consistiu em uma **análise exploratória e comparativa** de plataformas concorrentes diretas e indiretas do mercado de ticketing e eventos, agrupadas conforme suas principais características.

Os critérios de comparação incluíram:
- **Fluxo de criação de evento e gestão de lotes;**
- **Métodos de pagamento e split financeiro;**
- **Segurança antifraude (QR Code, autenticação);**
- **Recursos de engajamento (cashback, notificações, cupons);**
- **Interface e experiência do usuário (UX/UI).**

---

## Plataformas Analisadas

<b>Plataformas de Venda de Ingressos e Eventos</b>

- [Sympla](https://www.sympla.com.br)  
- [Eventbrite](https://www.eventbrite.com.br)  
- [R2 Produções](https://www.r2.com.vc)  
- [Ingresse](https://www.ingresse.com)  
- [BlueTicket](https://www.blueticket.com.br)  
- [Shotgun](https://shotgun.live/br)  
- [Bilheteria Digital](https://www.bilheteriadigital.com)

<b>Plataformas Complementares (pagamentos e marketing)</b>

- [Mercado Pago](https://www.mercadopago.com.br) — referência em PIX e split de pagamentos.  
- [Stripe](https://stripe.com/br) — modelo internacional de APIs financeiras e antifraude.  
- [Mailchimp](https://mailchimp.com/) — modelo de automação de e-mails e notificações.  
- [Hotmart](https://www.hotmart.com/) — gestão de produtos digitais e comissões.  

---

## Requisitos Elicitados

<b>Requisitos Funcionais com o benchmarking</b>

| Código | Requisito Funcional | Rastreabilidade |
|--------|---------------------|-----------------|
| RF01 | Permitir cadastro de produtor e criação de eventos com banner, local, data e categoria. | Sympla, Eventbrite |
| RF02 | Oferecer gestão de lotes de ingressos com nome, preço, quantidade e período de venda. | Sympla, Ingresse |
| RF03 | Suportar múltiplos tipos de ingresso (inteira, meia, VIP, cortesia). | Sympla, BlueTicket |
| RF04 | Gerar QR Code antifraude único por ingresso. | Ingresse, BlueTicket |
| RF05 | Oferecer pagamentos via PIX, cartão de crédito e débito. | Mercado Pago, Stripe |
| RF06 | Implementar split automático de repasse ao produtor. | Sympla, Hotmart |
| RF07 | Enviar comprovante por e-mail e WhatsApp após confirmação. | Sympla, Mailchimp |
| RF08 | Exibir painel do produtor com vendas em tempo real, estatísticas e exportação CSV. | Sympla, Bilheteria Digital |
| RF09 | Permitir cancelamento de evento e estorno conforme política definida. | Sympla, Eventbrite |
| RF10 | Oferecer cashback de 2% no primeiro evento do usuário. | Hotmart, modelos de fidelização |
| RF11 | Exibir ranking de eventos mais vendidos e destaques. | Eventbrite |
| RF12 | Notificar o usuário sobre eventos próximos ou novos lançamentos. | Mailchimp |
| RF13 | Implementar login social (Google, Facebook, Gov.br). | Sympla, Hotmart |
| RF14 | Suportar catálogo de produtos vinculados a eventos (mentorias, workshops). | Hotmart |
| RF15 | Permitir check-in rápido por leitura de QR Code via câmera. | Ingresse |
| RF16 | Disponibilizar modo offline de validação de ingressos. | BlueTicket |
| RF17 | Permitir emissão de nota fiscal sobre taxa de serviço. | Sympla |
| RF18 | Integrar módulo administrativo com auditoria de fraudes e logs. | Stripe, Sympla |

<div align="center">
               <b> Autor: </b> <a href="https://github.com/gabriel-lima258">Gabriel Lima</a>.
              <br>
</div>

---

### Requisitos Não Funcionais

<b>Requisitos não funcionais elicitados com o benchmarking</b>

| Código | Requisito Não Funcional | Rastreabilidade |
|--------|--------------------------|-----------------|
| RNF01 | O sistema deve ser responsivo e adaptável a dispositivos móveis (mobile-first). | Sympla, Eventbrite |
| RNF02 | As requisições devem ser processadas em até 2 segundos em média. | Ingresse |
| RNF03 | Toda comunicação deve ocorrer via HTTPS e certificados TLS válidos. | Stripe, Mercado Pago |
| RNF04 | Os dados de pagamento devem ser criptografados (AES-256, PCI-DSS). | Stripe, Mercado Pago |
| RNF05 | O sistema deve suportar alta disponibilidade (99,5%) e escalabilidade elástica. | Sympla |
| RNF06 | Deve haver logs e auditorias de todas as ações críticas. | Stripe |
| RNF07 | A interface deve seguir boas práticas de UX/UI com foco em clareza e confiança. | Eventbrite, Sympla |
| RNF08 | O sistema deve seguir a LGPD (consentimento, exclusão e portabilidade). | Sympla, Hotmart |
| RNF09 | Deve existir tolerância a falhas e backup diário do banco de dados. | Eventbrite |
| RNF10 | O sistema deve operar com autenticação segura JWT e refresh tokens. | Sympla |
| RNF11 | A validação de QR Codes deve ser antifraude (nonce + assinatura digital). | Ingresse |
| RNF12 | O site deve ter SEO otimizado para eventos públicos e integração com Google Maps. | Eventbrite |
| RNF13 | O suporte técnico deve registrar tickets e tempo médio de resposta. | BlueTicket |

<div align="center">
               <b> Autor: </b> <a href="https://github.com/gabriel-lima258">Gabriel Lima</a>.
              <br>
</div>

---

## Conclusão

A análise comparativa entre as plataformas revelou que **a maioria das soluções prioriza segurança, automação e experiência do usuário**, mas ainda há **lacunas de personalização e transparência** — especialmente no relacionamento com pequenos produtores de eventos.

O **Ingressou** busca se diferenciar ao unir:
- **Transparência nas taxas e repasses**;  
- **Cashback como mecanismo de fidelização**;  
- **Check-in antifraude e modo offline**;  
- **Interface leve, intuitiva e responsiva**;  
- **Foco em automação e confiança.**

Dessa forma, o benchmarking forneceu base sólida para **definir requisitos técnicos e estratégicos** que alinham inovação, desempenho e confiabilidade.

---

## Bibliografia

- CAMP, Robert. *Benchmarking: The Search for Industry Best Practices That Lead to Superior Performance*. Quality Press, 1989.  
- IATA, Cristiane. *Benchmarking: muito além de uma simples comparação*. Revista Benchmarking, 2008. Disponível em: [pontogp.wordpress.com](https://pontogp.wordpress.com/2008/12/24/benchmarking-muito-alem-de-uma-simples-comparacao/).  
- SYMPLA. *Sobre a Sympla*. Disponível em: [https://www.sympla.com.br](https://www.sympla.com.br).  
- EVENTBRITE. *Eventbrite Features*. Disponível em: [https://www.eventbrite.com.br](https://www.eventbrite.com.br).  
- INGRESSE. *Política e Termos de Uso*. Disponível em: [https://www.ingresse.com](https://www.ingresse.com).  

---

## Histórico de versão

| Versão | Alteração | Responsável | Data |
| :-: | :-: | :-: | :-: |
| 1.0 | Elaboração do documento de benchmarking da Ingressou | [Gabriel Lima](https://github.com/gabriel-lima258) | 15/10/2025 |

---
