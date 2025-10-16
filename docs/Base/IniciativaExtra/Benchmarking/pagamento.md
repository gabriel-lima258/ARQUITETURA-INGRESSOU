# Benchmarking em Relação a Pagamentos e Split Financeiro

## Sumário

* [Stripe Connect](#stripe-connect)
* [Pagar.me](#pagarme)
* [Requisitos Elicitados](#requisitos-elicitados)
  * [Requisitos Funcionais](#requisitos-funcionais)
  * [Requisitos Não-Funcionais](#requisitos-não-funcionais)

---

### [Stripe Connect](https://stripe.com/connect)

<div align="center">
    Figura 5: Stripe Connect — Split de Pagamentos (ilustrativo)
    <br>
    <img src="assets/Benchmarking/stripe.png" width="560" alt="Stripe Connect - split de pagamentos">
    <br>
    <b>Fonte:</b> <a href="https://stripe.com/connect">Stripe Connect</a>.
    <br>
</div>

#### Foco observado
Infraestrutura global para **pagamentos com split automático** e **compliance KYC/AML** para marketplaces.

#### Recursos-chave
- Split automático e dinâmico (comissões, múltiplos recebedores).
- API completa para repasses, estornos e taxas.
- Dashboard e webhook de eventos financeiros.
- Suporte a pagamentos instantâneos (Instant Payouts).
- Mecanismos antifraude e verificação de identidade (KYC).

#### Pontos positivos
- Altíssima confiabilidade e flexibilidade.
- APIs bem documentadas.
- Conformidade internacional e suporte regulatório.

#### Pontos a observar
- Custos de transação maiores que gateways locais.

---

### [Pagar.me](https://pagar.me)

<div align="center">
    Figura 6: Pagar.me — Split e Marketplace (ilustrativo)
    <br>
    <img src="assets/Benchmarking/pagarme.png" width="560" alt="Pagar.me - split e marketplace">
    <br>
    <b>Fonte:</b> <a href="https://pagar.me">Pagar.me</a>.
    <br>
</div>

#### Foco observado
Gateway brasileiro com suporte nativo a **split de pagamentos**, **antecipações** e **boletos**.

#### Recursos-chave
- Split de pagamentos com repasse automático.
- PIX, cartão e boleto integrados.
- Antecipação de recebíveis.
- Dashboard de vendas, taxas e repasses.

#### Pontos positivos
- Excelente opção para o mercado nacional.
- Flexível para integrações com APIs REST.
- Split e conciliação bem estruturados.

#### Pontos a observar
- Demanda integração técnica para uso avançado.

---

## Requisitos Elicitados

> Requisitos derivados das plataformas analisadas com foco em **Pagamentos e Split Financeiro** para a **Ingressou**.

### Requisitos Funcionais

| Código | Requisito Funcional                                                                 | Objetivo                                                                 | Origem (referência)          |
|--------|--------------------------------------------------------------------------------------|--------------------------------------------------------------------------|------------------------------|
| RF-PG-01 | Permitir múltiplos métodos de pagamento (PIX, cartão, boleto).                      | Aumentar conversão e acessibilidade.                                     | Sympla, Pagar.me             |
| RF-PG-02 | Implementar split automático entre plataforma e produtor.                          | Automação e transparência de receitas.                                   | Sympla, Stripe Connect       |
| RF-PG-03 | Permitir repasse automático via PIX após o evento.                                 | Reduzir atrasos e erros manuais.                                         | Ingresse, Pagar.me           |
| RF-PG-04 | Exibir dashboard financeiro com vendas, taxas, estornos e repasses.                 | Transparência e controle financeiro.                                     | Sympla, Ingresse             |
| RF-PG-05 | Gerar relatórios financeiros exportáveis (CSV, PDF).                               | Permitir conciliação e auditoria.                                        | Sympla, Bilheteria Digital   |
| RF-PG-06 | Permitir política de antecipação de recebíveis.                                    | Flexibilizar o fluxo de caixa do produtor.                               | Pagar.me                     |
| RF-PG-07 | Registrar logs de transações (criação, sucesso, falha, estorno).                   | Auditoria e rastreabilidade.                                             | Stripe Connect               |
| RF-PG-08 | Suportar cupons e descontos que alteram o valor total.                             | Compatibilidade com promoções.                                           | Eventbrite                   |
| RF-PG-09 | Gerar comprovante de compra com QR Code e resumo financeiro.                       | Transparência ao comprador.                                              | Sympla, Ingresse             |
| RF-PG-10 | Permitir rateio entre múltiplos organizadores (multi-receiver split).               | Atender eventos colaborativos e festivais.                              | Stripe Connect               |
| RF-PG-11 | Implementar módulo antifraude em pagamentos online.                                | Garantir segurança e confiabilidade.                                    | Ingresse, Stripe             |
| RF-PG-12 | Exibir histórico de repasses e status de cada transação.                           | Facilitar controle e conferência.                                        | Bilheteria Digital           |

---

### Requisitos Não-Funcionais

| Código | Requisito Não-Funcional                                                              | Objetivo                                                            | Origem (referência)     |
|--------|---------------------------------------------------------------------------------------|---------------------------------------------------------------------|--------------------------|
| RNF-PG-01 | Cumprir requisitos de segurança PCI DSS.                                            | Garantir proteção de dados de cartão.                               | Stripe, Pagar.me        |
| RNF-PG-02 | Utilizar HTTPS/TLS e criptografia de dados sensíveis.                              | Prevenir interceptação e fraudes.                                   | Padrão do setor          |
| RNF-PG-03 | Adotar autenticação de dois fatores (2FA) para produtores.                         | Evitar acessos indevidos a informações financeiras.                 | Boas práticas            |
| RNF-PG-04 | Integrar verificação KYC/AML para produtores.                                      | Cumprir legislações financeiras e antifraude.                       | Stripe Connect           |
| RNF-PG-05 | Disponibilidade mínima de 99,9% para o módulo de pagamentos.                        | Garantir estabilidade em períodos críticos de venda.                | Pagar.me, Stripe         |
| RNF-PG-06 | Tempo médio de resposta das APIs de pagamento < 2 segundos (P90).                   | Minimizar abandono no checkout.                                     | Stripe, Sympla           |
| RNF-PG-07 | Registrar e armazenar logs de pagamento por 365 dias.                              | Rastreabilidade e auditoria.                                        | Boas práticas            |
| RNF-PG-08 | Permitir fallback entre gateways (ex.: Stripe → Pagar.me) em caso de falha.         | Redundância e continuidade do serviço.                              | Boas práticas            |

---

## Histórico de versão

| Versão | Alteração                                      | Responsável  | Data       |
|-------:|------------------------------------------------|--------------|------------|
| 1.0    | Criação do benchmarking “Pagamentos e Split Financeiro” | Gabriel Lima | 15/10/2025 |
