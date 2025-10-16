# Benchmarking em Relação a Cashback e Fidelização

## Sumário

* [Sympla Rewards](#sympla-rewards)
* [Shopee Cashback](#shopee-cashback)
* [PicPay](#picpay)
* [Hotmart Club](#hotmart-club)
* [Requisitos Elicitados](#requisitos-elicitados)
  * [Requisitos Funcionais](#requisitos-funcionais)
  * [Requisitos Não-Funcionais](#requisitos-não-funcionais)

---

### [Sympla Rewards](https://www.sympla.com.br)

<div align="center">
    Figura 1: Sympla Rewards — Sistema de Fidelização
    <br>
    <img src="assets/Benchmarking/sympla.png" width="560" alt="Sympla Rewards - fidelização e pontos">
    <br>
    <b>Fonte:</b> <a href="https://www.sympla.com.br">Sympla</a>.
    <br>
</div>

#### Foco observado
Embora ainda experimental, a Sympla testa programas de fidelização voltados a **usuários recorrentes**, com **descontos progressivos** e **benefícios de cashback** em eventos selecionados.

#### Recursos-chave
- Recompensas em pontos por compras frequentes.  
- Benefícios exclusivos para quem participa de vários eventos.  
- Parcerias com produtoras e patrocinadores.  
- E-mails promocionais personalizados com base no histórico de eventos.  

#### Pontos positivos
- Incentiva recorrência e retenção.  
- Personalização com base em comportamento real do usuário.  
- Integração nativa com eventos e categorias.  

#### Pontos a observar
- Programa ainda restrito a alguns organizadores parceiros.  

---

### [Shopee Cashback](https://shopee.com.br/)

<div align="center">
    Figura 3: Shopee — Sistema de Cashback
    <br>
    <img src="assets/Benchmarking/shoppe.png" width="560" alt="Shopee - sistema de cashback">
    <br>
    <b>Fonte:</b> <a href="https://shopee.com.br/">Shopee</a>.
    <br>
</div>

#### Foco observado
Um dos sistemas de cashback mais populares do mercado, voltado à **retenção e recompra**. Usa **mecanismos gamificados** e **saldo real** reaplicável em futuras transações.

#### Recursos-chave
- Cashback instantâneo creditado na carteira virtual.  
- Uso automático do saldo em compras futuras.  
- Ofertas diárias com valores promocionais.  
- Sistema de gamificação com missões e bônus semanais.  

#### Pontos positivos
- Forte engajamento e recorrência.  
- Experiência gamificada que estimula o retorno.  
- Cashback simples e transparente.  

#### Pontos a observar
- Dependência de campanhas para manter engajamento.  

---

### [PicPay](https://www.picpay.com/)

<div align="center">
    Figura 4: PicPay — Cashback e Pagamentos
    <br>
    <img src="assets/Benchmarking/picpay.png" width="560" alt="PicPay - cashback e pagamentos">
    <br>
    <b>Fonte:</b> <a href="https://www.picpay.com/">PicPay</a>.
    <br>
</div>

#### Foco observado
Referência nacional em **cashback financeiro real**, usado como **saldo para pagamentos**.

#### Recursos-chave
- Cashback automático em promoções selecionadas.  
- Saldo utilizável em qualquer operação da conta.  
- Notificações automáticas sobre créditos e vencimentos.  
- Estatísticas mensais sobre ganhos acumulados.  

#### Pontos positivos
- Clareza e transparência do saldo.  
- Facilidade de uso e controle.  
- Ampla integração com outros serviços.  

#### Pontos a observar
- Cashback depende de campanhas específicas e limites de valor.  

---

### [Hotmart Club](https://www.hotmart.com/)

<div align="center">
    Figura 5: Hotmart Club — Fidelização por Engajamento
    <br>
    <img src="assets/Benchmarking/hotmart.png" width="560" alt="Hotmart Club - fidelização e gamificação">
    <br>
    <b>Fonte:</b> <a href="https://www.hotmart.com/">Hotmart</a>.
    <br>
</div>

#### Foco observado
Sistema de **fidelização por engajamento**, que premia interações e consumo contínuo de conteúdo.

#### Recursos-chave
- Pontos por login, interação e conclusão de atividades.  
- Recompensas automáticas conforme o nível de engajamento.  
- Gamificação com selos e níveis.  
- Dashboard de progresso e histórico.  

#### Pontos positivos
- Aumenta retenção e participação do usuário.  
- Reforça vínculo emocional com a plataforma.  

#### Pontos a observar
- Mais voltado a produtos digitais do que a eventos físicos.  

---

## Requisitos Elicitados

> Requisitos derivados com foco em **programas de fidelidade e cashback** para a plataforma **Ingressou**.

### Requisitos Funcionais

| Código | Requisito Funcional                                                        | Objetivo                                                          | Origem (referência)         |
|--------|---------------------------------------------------------------------------|-------------------------------------------------------------------|-----------------------------|
| RF-CB-01 | Implementar sistema de cashback em percentual das compras.                | Incentivar recompra e fidelização.                               | Sympla Rewards, PicPay      |
| RF-CB-02 | Exibir saldo de cashback na conta do usuário.                            | Tornar o benefício visível e motivacional.                       | Shopee, Ingressos.com       |
| RF-CB-03 | Permitir uso do saldo em novas compras de ingressos.                     | Estimular o ciclo de recompra.                                   | Shopee, PicPay              |
| RF-CB-04 | Enviar notificações sobre cashback recebido e expiração de saldo.         | Melhorar engajamento e reduzir perda de saldo.                   | PicPay, Ingressos.com       |
| RF-CB-05 | Implementar sistema de pontos com níveis de fidelidade (ex: Bronze, Ouro).| Recompensar usuários recorrentes.                                | Hotmart Club, Sympla Rewards|
| RF-CB-06 | Permitir resgate de benefícios ou descontos com base em pontos.           | Aumentar o engajamento contínuo.                                 | Ingressos.com Club, Hotmart |
| RF-CB-07 | Oferecer campanhas sazonais de cashback (ex: 5% em lançamentos).          | Gerar picos de engajamento em datas específicas.                  | Shopee, PicPay              |
| RF-CB-08 | Disponibilizar histórico detalhado de cashback e pontos.                  | Garantir transparência e controle.                               | Sympla, PicPay              |
| RF-CB-09 | Exibir ranking de usuários mais engajados (gamificação).                  | Reforçar comunidade e competição saudável.                       | Hotmart Club                |
| RF-CB-10 | Integrar sistema de cashback ao painel do produtor (para campanhas próprias). | Permitir que organizadores criem incentivos próprios.         | Sympla, Hotmart             |

---

### Requisitos Não-Funcionais

| Código | Requisito Não-Funcional                                                  | Objetivo                                                  | Origem (referência)     |
|--------|---------------------------------------------------------------------------|-----------------------------------------------------------|--------------------------|
| RNF-CB-01 | Atualização de saldo e pontos em tempo real após transação.             | Garantir consistência e confiabilidade.                   | Shopee, PicPay          |
| RNF-CB-02 | Armazenar logs de cashback e pontos por no mínimo 180 dias.             | Rastreabilidade e auditoria.                              | Boas práticas            |
| RNF-CB-03 | Painel de fidelidade responsivo e com indicadores visuais de progresso. | Melhorar experiência e engajamento.                       | Hotmart Club             |
| RNF-CB-04 | Tempo máximo de atualização de notificações ≤ 5 segundos (P90).         | Garantir feedback imediato.                               | Sympla, Shopee           |
| RNF-CB-05 | Sistema de cashback deve operar mesmo em alta carga de transações.      | Escalabilidade e resiliência.                             | PicPay, Shopee           |
| RNF-CB-06 | Garantir conformidade com LGPD em dados de comportamento e marketing.   | Proteger privacidade do usuário.                          | Padrão do setor          |
| RNF-CB-07 | Permitir expiração automática de pontos após período configurável.      | Manter sustentabilidade do programa.                      | Ingressos.com, Sympla    |
| RNF-CB-08 | Integração segura com módulo de pagamentos via API autenticada (JWT).   | Evitar inconsistências entre saldo e pagamentos.           | PicPay, Sympla           |

---

## Histórico de versão

| Versão | Alteração                                      | Responsável  | Data       |
|-------:|------------------------------------------------|--------------|------------|
| 1.0    | Criação do benchmarking “Cashback e Fidelização” | Gabriel Lima | 15/10/2025 |
