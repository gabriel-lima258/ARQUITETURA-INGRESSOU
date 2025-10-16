# Brainstorming

> Versão: 1.0  
> Data: Outubro de 2025  
> Autor: Gabriel Lima  
> Projeto: Ingressou — Plataforma Web de Venda e Gestão de Ingressos

---

## 📑 Sumário

* [Introdução](#Introdução)
* [Objetivos](#Objetivos)
* [Metodologia](#Metodologia)
* [Mapa Mental](#Mapa-Mental)
* [Quadro de Insights](#Quadro-de-Insights)
* [Conclusão](#Conclusão)
* [Bibliografia](#Bibliografia)
* [Histórico de versão](#Histórico-de-versão)

## Introdução

O brainstorming, ou "tempestade de ideias", é uma técnica amplamente utilizada em processos criativos e de levantamento de requisitos com o propósito de estimular a geração espontânea de ideias em um ambiente livre de julgamentos. Com isso, no artigo [The Journey of Brainstorming](https://www.regent.edu/journal/journal-of-transformative-innovation/the-history-of-brainstorming-alex-osborn/) [1](#ref1), segundo Osborn (1953), criador do método, a principal função do brainstorming é “**estimular o pensamento criativo e permitir a exploração de diferentes possibilidades de solução para um determinado problema**”¹. Atualmente, essa prática é aplicada tanto em contextos colaborativos quanto individuais no desenvolvimento de softwares, uma vez que servem como ferramenta para ampliar a compreensão sobre o escopo de um projeto e antecipar potenciais funcionalidades, oportunidades e desafios.

Desse modo, neste projeto, um brainstorming foi realizado na fase inicial para explorar as ideias iniciais sobre as funcionalidades, os conteúdos e as experiências que a plataforma poderá oferecer aos seus usuários. 

## Objetivos

O principal objetivo deste artefato é registrar e organizar as ideias geradas durante a sessão de brainstorming. Dessa maneira, a intenção é identificar possíveis funcionalidades, temas de conteúdo e experiências interativas que possam compor o escopo do sistema do site de astronomia. Além disso, busca-se utilizar esse brainstorming como um ponto de partida para a elicitação de requisitos e para a construção de uma visão mais clara do produto.

## Metodologia

A metodologia adotada para a realização desta etapa do projeto baseou-se na elaboração de um **mapa mental**, feito por meio da ferramenta [Draw.io](https://app.diagrams.net/), contendo as principais categorias e sugestões identificadas para o desenvolvimento da plataforma **Ingressou**. Para isso, foram utilizadas referências em sites e projetos já consolidados nas áreas de educação, divulgação científica e atividades lúdicas, como Khan Academy, Racha Cuca, Astronomia no Zênite e o programa audiovisual Um Minuto no Museu, entre outros. 

## Mapa Mental

Abaixo, há o mapa mental criado:

**Observação:** Para analisar o brainstorming de forma ampliada e em seus detalhes, clique com botão direito na imagem e abra em nova aba e ela será aberta, a qual lhe permitirá explorá-lo com um zoom.

<div align="center">
    Figura 1: Mapa Mental Brainstorming
    <br>
    <img src="assets/ArtefatosGeneralistas/brainstorming.png">
    <br>
     <b> Autor: </b> <a href="https://github.com/gabriel-lima258">Gabriel Lima</a>.
    <br>
</div>


##  Quadro de Insights

Para organizar os principais tópicos elencados no mapa mental, o quadro abaixo foi desenvolvido com o objetivo de agrupar as ideias de forma visual e temática, o que facilita a identificação de padrões, de oportunidades e de possíveis direções para o desenvolvimento da **Ingressou**.

---

## Modelo de Negócio

| **Insights Principais** | **Padrões e Oportunidades Identificadas** | **Direcionamento para o Projeto** |
|--------------------------|--------------------------------------------|-----------------------------------|
| - Taxa de 8% por venda de ingresso. <br> - Cashback de 2% no primeiro evento. <br> - Split automático de repasse ao produtor. <br> - Suporte a diferentes tipos de eventos (shows, palestras, igrejas, teatros). <br> - Venda de produtos extras (mentorias, workshops, pacotes). | - Falta de transparência em taxas e repasses nas plataformas atuais. <br> - Mercado desatendido para eventos pequenos e locais. <br> - Cashbacks e benefícios fidelizam o público. | - Manter modelo sustentável e competitivo. <br> - Posicionar a Ingressou como **acessível e justa** para produtores. <br> - Criar **planos diferenciados** (básico, premium, corporativo). |


## Produto e Funcionalidades

| **Insights Principais** | **Padrões e Oportunidades Identificadas** | **Direcionamento para o Projeto** |
|--------------------------|--------------------------------------------|-----------------------------------|
| - Cadastro de eventos e lotes. <br> - Tipos de ingressos (inteira, meia, VIP, cortesia). <br> - Pagamentos via PIX, crédito e débito. <br> - Check-in com QR Code antifraude. <br> - Painel do produtor com relatórios e estatísticas. <br> - Histórico de compras e cashback. | - Usuários e produtores valorizam **simplicidade e autonomia**. <br> - Automação e confiabilidade são essenciais. <br> - Check-in rápido evita filas e fraudes. | - Focar o MVP no fluxo essencial: **criar → vender → validar**. <br> - Incluir automações (e-mails, WhatsApp, controle de estoque). |

## Usuários e Personas

| **Insights Principais** | **Padrões e Oportunidades Identificadas** | **Direcionamento para o Projeto** |
|--------------------------|--------------------------------------------|-----------------------------------|
| - **Produtor:** quer vender fácil e receber rápido. <br> - **Usuário:** busca confiança e agilidade (PIX, QR, cashback). <br> - **Staff:** precisa de check-in rápido e offline. <br> - **Admin:** precisa monitorar fraudes e finanças. | - Todos valorizam **transparência, automação e simplicidade**. <br> - Há insatisfação com plataformas complexas e caras. | - Projetar fluxos claros e minimalistas por perfil. <br> - Criar dashboards personalizados (produtor, usuário, admin). |

## Experiência e Interface (UX/UI)

| **Insights Principais** | **Padrões e Oportunidades Identificadas** | **Direcionamento para o Projeto** |
|--------------------------|--------------------------------------------|-----------------------------------|
| - Interface intuitiva e leve (web). <br> - Páginas de evento com imagem e categorias. <br> - Checkout em poucos cliques. <br> - Envio automatizado de QR Code por e-mail e WhatsApp. <br> - PWA com modo offline. | - Expectativa por experiência moderna e fluida. <br> - Integração com WhatsApp e carteiras digitais aumenta engajamento. | - Criar identidade visual jovem, vibrante e brasileira. <br> - UX responsiva com microinterações e feedbacks claros. |

## Regras e Conformidade

| **Insights Principais** | **Padrões e Oportunidades Identificadas** | **Direcionamento para o Projeto** |
|--------------------------|--------------------------------------------|-----------------------------------|
| - LGPD: consentimento e segurança dos dados. <br> - Meia-entrada: validação de documentos no check-in. <br> - Política de reembolso configurável. <br> - Emissão automática de NFS-e sobre a taxa. | - Usuários valorizam proteção de dados e clareza nas regras. <br> - Produtores precisam de segurança jurídica e fiscal. | - Implementar processos automáticos de emissão fiscal. <br> - Criar políticas claras e acessíveis no checkout. |

## Diferenciais Estratégicos

| **Insights Principais** | **Padrões e Oportunidades Identificadas** | **Direcionamento para o Projeto** |
|--------------------------|--------------------------------------------|-----------------------------------|
| - Cashback promocional. <br> - Antifraude com QR dinâmico. <br> - Split de pagamento automático. <br> - Comunicação via e-mail e WhatsApp. <br> - Plataforma aberta a produtores de qualquer porte. | - Fidelização por recompensa financeira. <br> - Potencial de democratização de eventos locais. | - Fortalecer o branding em torno de **confiança, tecnologia e acessibilidade**. <br> - Criar campanhas de aquisição e retenção personalizadas. |

<div align="center">
    <br>
     <b> Autor: </b> <a href="https://github.com/gabriel-lima258">Gabriel Lima</a>.
    <br>
</div>

---

## Síntese dos Padrões e Direcionamentos

1. **Facilidade e agilidade** são valores centrais para todos os usuários.  
2. **Segurança e transparência** são fundamentais para a credibilidade do sistema.  
3. **Cashback e automação** podem gerar diferenciais competitivos.  
4. **Arquitetura modular** permitirá escalar o produto de forma sustentável.  
5. **UX responsiva e inclusiva** é essencial para adoção rápida.

---

## Caminho Estratégico Inicial

- Foco do MVP: fluxo completo de **criação → venda → validação**.  
- Prioridades técnicas: segurança, automação e UX fluida.  
- Evolução futura: revenda de ingressos, afiliados e white-label.  
- Identidade: **Ingressou — “Seu rolê começa aqui.”**

---

## Conclusão

Ao se colocar as ideias iniciais em um mapa mental e em um quadro de insights, foi possível visualizar de forma estruturada os principais elementos que podem compor o  projeto proposto. Assim, essa abordagem favoreceu a identificação de temas recorrentes, de algumas das funcionalidades desejadas e verificar oportunidades de inovação.

---

## Bibliografia

<a name="ref1"></a>  
[1] BESANT, Hanisha. *The journey of brainstorming*. *Journal of Transformative Innovation*, [S.l.], v. 2, n. 1, 2016. Disponível em: <https://www.regent.edu/journal/journal-of-transformative-innovation/the-history-of-brainstorming-alex-osborn/>. Acesso em: 4 abr. 2025.

## Histórico de versão

| Versão | Alteração | Responsável | Data |
| - | - | - | - |
| 1.0 | Elaboração do documento| Gabriel Lima | 15/10/2025 |
