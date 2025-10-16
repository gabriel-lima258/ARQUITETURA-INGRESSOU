# Design Sprint – Esboçar (Sketch)

**Versão:** 1.0  
**Data:** Outubro de 2025  
**Autor:** Gabriel Lima  
**Projeto:** Ingressou — Plataforma Web de Venda e Gestão de Ingressos

---

## Sumário

- [Introdução](#introdução)
- [Objetivos](#objetivos)
- [Referências Visuais e Inspirações](#referências-visuais-e-inspirações)
- [Esboço Detalhado da Solução](#esboço-detalhado-da-solução)
  - [Páginas Públicas](#páginas-públicas)
  - [Fluxo de Checkout](#fluxo-de-checkout)
  - [Painéis Internos](#painéis-internos)
  - [Check-in (PWA)](#check-in-pwa)
- [Análise do Rich Picture](#análise-do-rich-picture)
- [Ideias para a Etapa de Decidir](#ideias-para-a-etapa-de-decidir)
- [Bibliografia](#bibliografia)
- [Histórico de Versão](#histórico-de-versão)

---

## Introdução

A etapa **Esboçar (Sketch)** do Design Sprint transforma os aprendizados da fase **[Entender (Unpack)](Base/DesignSprint/Entender.md)** em **representações visuais rápidas** (wireframes de baixa fidelidade, fluxos e componentes).  
Nesta fase exploramos múltiplas soluções para, na etapa seguinte (**Decidir**), selecionar o caminho mais promissor para o **MVP** do **Ingressou**.

---

## Objetivos

- Converter requisitos e regras de negócio em **fluxos visuais claros**.  
- Antecipar **interações críticas** (checkout, validação de QR, criação/publicação de eventos).  
- Usar o **[Rich Picture](Base/ArtefatoGeneralista/RichPicture.md)** como referência de contexto e atores.  
- Preparar **material base** (wireframes + critérios) para a etapa **Decidir**.

---

## Referências Visuais e Inspirações

**Benchmarking (setor de ingressos e eventos):**  
- Sympla, Eventbrite, Ingresse, Bilheteria Digital, BlueTicket, Shotgun.

**Elementos inspiradores aplicados à Ingressou:**
- **Home orientada à conversão** (busca, filtros por cidade/data/categoria).  
- **Página de evento enxuta** (banner, datas, mapa, lotes e CTA fixo).  
- **Checkout em passos curtos** com resumo financeiro e aplicação de **cupom**.  
- **Painel do produtor** com métricas em tempo quase real e **saldo de cashback**.  
- **Check-in PWA** com **modo offline** e feedback instantâneo (válido/duplicado/expirado).  
- **Painel Admin** para **criar/publicar eventos** e **configurar lotes** (tempo/quantidade).

> Premissas de negócio incorporadas: **Admin cria/publica eventos**; **lote encerra pelo primeiro limite (tempo/quantidade)**; **cupom é do influenciador para o comprador**; **cashback é do produtor**; uso de **mensageria** e **cache**.

---

## Esboço Detalhado da Solução

> Abaixo estão descritos os **wireframes conceituais** (baixa fidelidade) para orientar prototipação.  
> As imagens poderão ser adicionadas futuramente em `assets/wireframes/*.png`.

### Páginas Públicas

**1) Home / Catálogo**  
- Cabeçalho com **busca**, **localização**, **datas** e **categorias**.  
- Lista de cards de eventos (banner, título, local, data, **a partir de R$**).  
- **Carrossel** “em alta”, **filtros rápidos** (Hoje / Este fim de semana / Gratuitos).  
- Rodapé com links institucionais (Termos, Privacidade, Suporte).

**2) Página do Evento**  
- **Banner + título + cidade/UF + data/hora**.  
- Seções: **Descrição**, **Local/Mapa**, **Lotes Disponíveis** (preço, janela, saldo), **FAQ**.  
- **CTA fixo** “Selecionar ingresso” (desktop e mobile).  
- **Regra visual**: Lote “Esgotado” ou “Encerrado por tempo” desabilita seleção.  
- Nota de **meia-entrada** com aviso de comprovação no check-in.

### Fluxo de Checkout

**3) Carrinho & Dados**  
- Resumo: itens, quantidade, taxas e total.  
- Campo **Cupom de Influenciador** (validar/retornar mensagem).  
- Aceite de **Termos de Uso** e **Política de Reembolso**.

**4) Pagamento**  
- **PIX (QR dinâmico)** com **timer de 10 min** e instruções.  
- **Cartão** (com 3DS/antifraude) via gateway.  
- Estado “Aguardando confirmação…” com tratativa assíncrona (mensageria).

**5) Confirmação**  
- Pedido **Pago** → disparo de **ingressos** (e-mail/WhatsApp).  
- Link para **“Acessar meus ingressos”**.

### Painéis Internos

**6) Painel do Produtor**  
- **Dashboard**: vendas por período, lote, canal (cupom/influenciador), taxa, **saldo de cashback**.  
- Relatórios (CSV), extrato de repasses, status de webhooks.  
- Observação: **Produtor não cria eventos** — visualiza os seus e acompanha desempenho.

**7) Painel do Administrador**  
- **CRUD de eventos** (rascunho/publicado/encerrado).  
- **Lotes**: nome, preço, quantidade, janela de venda; **encerra por primeiro limite**.  
- **Cupons**: escopo (evento/lote), valor %, valor fixo, vigência, limite de uso, influenciador.  
- **Parâmetros**: taxas, política de **cashback do produtor**, textos institucionais.

### Check-in (PWA)

**8) Validação de Ingressos**  
- Tela de **scanner** (câmera) com estados: **Válido / Duplicado / Expirado** (cores e toasts).  
- **Modo offline**: indicador de sincronização pendente; contador de validações locais.  
- Log de auditoria (operador, data/hora, dispositivo).

---

## Análise do Rich Picture

O **Rich Picture** sintetiza **atores**, **limites** e **interações** do ecossistema Ingressou, guiando os esboços acima:  
- Atores centrais: **Administrador, Produtor, Comprador, Staff**.  
- Operações críticas: **publicar evento (Admin)**, **vender** (checkout), **validar** (check-in).  
- Limites/sistemas externos: **PSP/gateway**, **provedor de e-mail/WhatsApp**.  
- Problemas mapeados: **filas**, **fraude**, **carga em picos**, **comunicação**.  

> Artefato completo: [Rich Picture](Base/ArtefatoGeneralista/RichPicture.md)

---

## Ideias para a Etapa de Decidir

**1) Storyboard do MVP (recomendado):**  
- Cena 1: **Home → Evento** (descoberta + micro-conversão).  
- Cena 2: **Seleção de lote/tipo** (regra de encerramento por tempo/quantidade).  
- Cena 3: **Checkout com cupom** (validação e resumo transparente).  
- Cena 4: **Pagamento PIX** (reserva 10 min) e **confirmação assíncrona**.  
- Cena 5: **Envio de ingressos** e **check-in** (PWA offline).  
- Cena 6: **Painel do Produtor** (métricas + **saldo de cashback**) e **Painel Admin** (governança).

**2) Critérios para seleção (Decidir):**  
- **Tempo de implementação** no MVP.  
- **Impacto em conversão** (menos cliques, menos erro).  
- **Risco técnico** (PSP, filas, cache).  
- **Aderência às regras**: admin cria eventos; lote encerra por primeiro limite; cupom x cashback do produtor.

**3) Materiais para prototipar (alta fidelidade):**  
- Protótipos: **Home, Evento, Checkout, Confirmação, Painel Produtor, Painel Admin, Check-in PWA**.  
- Conteúdo estático de exemplo + casos de lote esgotado/encerrado.  
- Estados vazios/erro (ex.: cupom inválido, webhook atrasado).

---

## Bibliografia

1. PM3. **O que é Design Sprint e como aplicar o método para testar e validar ideias.** 10 mar. 2025. Disponível em: https://pm3.com.br/blog/design-sprint/.  
2. The Open University. **Rich pictures.** OpenLearn, 21 jun. 2021. Disponível em: https://www.open.edu/openlearn/science-maths-technology/engineering-technology/rich-pictures.

---

## Histórico de Versão

| Versão | Alteração                                | Responsável   | Data       |
|------:|-------------------------------------------|---------------|------------|
| 1.0   | Adaptação da etapa **Sketch** para MVP    | Gabriel Lima  | 16/10/2025 |
