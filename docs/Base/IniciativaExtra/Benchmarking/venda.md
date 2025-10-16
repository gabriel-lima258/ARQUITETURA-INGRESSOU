# Benchmarking em Relação a Venda de Ingressos e Eventos

## Sumário

* [Sympla](#sympla)
* [Eventbrite](#eventbrite)
* [Ingresse](#ingresse)
* [BlueTicket](#blueticket)
* [Shotgun](#shotgun)
* [Bilheteria Digital](#bilheteria-digital)
* [Requisitos Elicitados](#requisitos-elicitados)
  * [Requisitos Funcionais](#requisitos-funcionais)
  * [Requisitos Não-Funcionais](#requisitos-não-funcionais)

---

### [Sympla](https://www.sympla.com.br)

<div align="center">
    Figura 1: Sympla (exemplo ilustrativo)
    <br>
    <img src="assets/Benchmarking/sympla.png" width="560" alt="Sympla - captura ilustrativa">
    <br>
    <b>Fonte:</b> <a href="https://www.sympla.com.br">Sympla</a>.
    <br>
</div>

#### Descrição
Plataforma brasileira de **criação e venda de ingressos** com foco em autonomia do produtor, vitrine pública e experiência de compra simplificada. Forte presença em **eventos culturais e educacionais**.

#### Recursos-chave observados
- Criação rápida de evento (nome, data, local, banner).
- **Gestão de lotes** (nome, preço, quantidade, período de venda).
- Tipos de ingresso (inteira, meia, VIP, cortesia).
- Página de evento com vitrine amigável e CTA de compra.
- Emissão de ingresso digital com **QR Code**.
- Painel do organizador com relatórios e exportação CSV.

#### Pontos positivos
- UX de criação de evento bem guiada.
- Vitrine com SEO forte e fácil descoberta de eventos.
- Relatórios e exportação de dados acessíveis ao produtor.

#### Pontos negativos
- Personalização avançada de checkout limitada em planos básicos.
- Regras e taxas nem sempre transparentes no primeiro contato (percepção comum).

---

### [Eventbrite](https://www.eventbrite.com.br)

<div align="center">
    Figura 2: Eventbrite (exemplo ilustrativo)
    <br>
    <img src="assets/Benchmarking/evenbrite.png" width="560" alt="Eventbrite - captura ilustrativa">
    <br>
    <b>Fonte:</b> <a href="https://www.eventbrite.com.br">Eventbrite</a>.
    <br>
</div>

#### Descrição
Plataforma internacional de **ticketing** e promoção de eventos, com foco em **divulgação global**, integrações e widgets de incorporação.

#### Recursos-chave observados
- Editor de eventos com módulos reutilizáveis.
- Ferramentas de promoção (códigos de desconto, widgets).
- **Integrações** com e-mail marketing e redes sociais.
- Relatórios multi-moeda e base internacional de usuários.
- APIs e widgets para incorporação em sites próprios.

#### Pontos positivos
- Ecossistema de integrações amplo (marketing, CRM).
- Ferramentas de divulgação robustas.

#### Pontos negativos
- Algumas features e cobranças atreladas ao mercado internacional.
- Onboarding do produtor pode ser mais complexo para iniciantes.

---

### [Ingresse](https://www.ingresse.com)

<div align="center">
    Figura 3: Ingresse (exemplo ilustrativo)
    <br>
    <img src="assets/Benchmarking/ingresse.png" width="560" alt="Ingresse - captura ilustrativa">
    <br>
    <b>Fonte:</b> <a href="https://www.ingresse.com">Ingresse</a>.
    <br>
</div>

#### Descrição
Foco em **eventos de entretenimento** (shows, festas, festivais) com ênfase em **mobile** e operação de **acesso/portaria**.

#### Recursos-chave observados
- Página de evento visual, com destaque para atrações.
- **Check-in** por QR Code e app de portaria.
- Gestão de lotes e tipos de ingresso.
- Operação em alto volume (picos de venda).

#### Pontos positivos
- Experiência mobile forte para o público final.
- Operação de validação reconhecida no mercado.

#### Pontos negativos
- Menos voltada a conteúdos adicionais (ex.: mentorias).
- Flexibilidade de customização varia por parceria.

---

### [BlueTicket](https://www.blueticket.com.br)

<div align="center">
    Figura 4: BlueTicket (exemplo ilustrativo)
    <br>
    <img src="assets/Benchmarking/blue.png" width="560" alt="BlueTicket - captura ilustrativa">
    <br>
    <b>Fonte:</b> <a href="https://www.blueticket.com.br">BlueTicket</a>.
    <br>
</div>

#### Descrição
Bilheteria online com forte atuação regional e **operações de acesso**. Destaque para **organização por cidades/regiões**.

#### Recursos-chave observados
- Catálogo por cidades.
- Gestão de lotes/estoque e setorização por tipo.
- Relatórios para produtores e app de check-in.

#### Pontos positivos
- Boa curadoria regional (descoberta por localização).
- Confiabilidade na validação de ingressos.

#### Pontos negativos
- Interface menos “customizável” na vitrine para alguns nichos.
- Menor foco em produtos extras vinculados ao evento.

---

### [Bilheteria Digital](https://www.bilheteriadigital.com)

<div align="center">
    Figura 6: Bilheteria Digital (exemplo ilustrativo)
    <br>
    <img src="assets/Benchmarking/bilheteria.png" width="560" alt="Bilheteria Digital - captura ilustrativa">
    <br>
    <b>Fonte:</b> <a href="https://www.bilheteriadigital.com">Bilheteria Digital</a>.
    <br>
</div>

#### Descrição
Plataforma focada em **simplicidade** e alcance nacional, contemplando eventos diversos (culturais, esportivos, religiosos).

#### Recursos-chave observados
- Criação de evento e lotes.
- Vitrine com filtros básicos (cidade, data, categoria).
- Emissão de ingressos digitais e check-in por QR.

#### Pontos positivos
- Abordagem direta e fácil para novos produtores.
- Amplo mix de categorias.

#### Pontos negativos
- Menor profundidade em automações de marketing.
- Customizações de página variam conforme evento/parceria.

---

## Requisitos Elicitados

> Abaixo, os requisitos foram **derivados das observações** nas plataformas analisadas, priorizando o escopo de **venda de ingressos e eventos** para o projeto **Ingressou**.

### Requisitos Funcionais

| Código | Requisito Funcional                                                                 | Objetivo                                                                 | Origem (referência)         |
|--------|--------------------------------------------------------------------------------------|--------------------------------------------------------------------------|-----------------------------|
| RF01   | Criar evento com campos obrigatórios (nome, data/hora, local, banner, categoria).   | Publicar eventos com informações mínimas e consistentes.                 | Sympla, Eventbrite          |
| RF02   | Configurar lotes (nome, preço, quantidade, janela de venda).                         | Controlar disponibilidade e precificação por fase.                       | Sympla, Ingresse, BlueTicket|
| RF03   | Definir tipos de ingresso (inteira, meia, VIP, cortesia).                           | Atender legislações e diferenciação de valor/benefício.                  | Sympla, BlueTicket          |
| RF04   | Exibir página pública do evento com CTA “Comprar”.                                  | Facilitar a descoberta e a conversão.                                    | Sympla, Eventbrite          |
| RF05   | Realizar checkout com resumo claro de itens, taxas e total.                          | Transparência e redução de abandono.                                     | Eventbrite, Sympla          |
| RF06   | Emitir ingresso digital com QR Code único por item.                                  | Garantir controle de acesso e antifraude.                                | Ingresse, BlueTicket        |
| RF07   | Disponibilizar painel do produtor com vendas em tempo real e exportação CSV.         | Apoiar tomada de decisão e conciliação financeira.                       | Sympla, Bilheteria Digital  |
| RF08   | Permitir cancelamento de evento e políticas de estorno configuráveis.                | Adequar operação a imprevistos e compliance.                              | Sympla, Eventbrite          |
| RF09   | Suportar catálogo de **produtos vinculados ao evento** (mentorias, workshops).       | Vender itens adicionais e aumentar receita por pedido.                   | Observação de mercado       |
| RF10   | Oferecer cupons de desconto e códigos promocionais.                                  | Alavancar divulgação e campanhas.                                        | Eventbrite                  |
| RF11   | Exibir listagens por cidade, data e categoria.                                       | Melhorar a descoberta e filtragem.                                       | BlueTicket                  |
| RF12   | Disponibilizar check-in (web/app) com leitura de QR e logs de auditoria.             | Agilidade na portaria e rastreabilidade.                                 | Ingresse, BlueTicket        |

### Requisitos Não-Funcionais

| Código | Requisito Não-Funcional                                                              | Objetivo                                                            | Origem (referência)   |
|--------|---------------------------------------------------------------------------------------|---------------------------------------------------------------------|-----------------------|
| RNF01  | Interface **responsiva** (mobile-first).                                             | Garantir experiência consistente em dispositivos móveis.            | Sympla, Eventbrite    |
| RNF02  | Páginas com **tempo médio de resposta ≤ 2 s** (P90).                                 | Reduzir abandono e aumentar conversão.                              | Ingresse              |
| RNF03  | **HTTPS/TLS** em toda a navegação.                                                    | Segurança de dados em trânsito.                                     | Padrão do setor       |
| RNF04  | **LGPD**: consentimentos, portabilidade e exclusão sob demanda.                       | Conformidade legal e confiança do usuário.                          | Padrão do setor       |
| RNF05  | **Disponibilidade ≥ 99,5%** mensal no MVP.                                            | Confiabilidade para vendas em janelas críticas.                     | Sympla (prática comum)|
| RNF06  | **Logs e auditoria** para operações críticas (criar/publicar/validar/cancelar).       | Rastreamento de incidentes e compliance.                            | Stripe (boa prática)  |
| RNF07  | **SEO** para páginas públicas de evento e **Open Graph** para redes sociais.          | Aumento de descoberta e compartilhamento orgânico.                  | Eventbrite            |
| RNF08  | **Acessibilidade** (WCAG 2.1 AA: contraste, foco, leitores de tela).                  | Inclusão e conformidade.                                            | Padrão do setor       |
| RNF09  | **Backup diário** do banco e testes de restauração periódicos.                         | Continuidade e recuperação de desastres.                            | Boa prática           |

---

## Histórico de versão

| Versão | Alteração                                           | Responsável | Data       |
|-------:|------------------------------------------------------|-------------|------------|
| 1.0    | Criação do benchmarking “Venda de Ingressos e Eventos” | Gabriel Lima | 15/10/2025 |
