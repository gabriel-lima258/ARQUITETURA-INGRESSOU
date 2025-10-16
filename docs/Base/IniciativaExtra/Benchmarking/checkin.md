# Benchmarking em Relação a Check-in e Validação de Ingressos

## Sumário

* [Sympla](#sympla)
* [Ingresse](#ingresse)
* [BlueTicket](#blueticket)
* [Ticketmaster](#ticketmaster)
* [Eventick](#eventick)
* [Requisitos Elicitados](#requisitos-elicitados)
  * [Requisitos Funcionais](#requisitos-funcionais)
  * [Requisitos Não-Funcionais](#requisitos-não-funcionais)

---

### [Sympla](https://www.sympla.com.br)

<div align="center">
    Figura 1: Sympla — Check-in e Portaria (ilustrativo)
    <br>
    <img src="assets/Benchmarking/sympla.png" width="560" alt="Sympla - check-in">
    <br>
    <b>Fonte:</b> <a href="https://www.sympla.com.br">Sympla</a>.
    <br>
</div>

#### Foco observado
Sistema de controle de acesso com **app de portaria**, **QR Code dinâmico** e **modo offline**. Voltado para garantir **agilidade e segurança** na entrada de eventos.

#### Recursos-chave
- Aplicativo **Sympla Organizador** (Android/iOS) para leitura de ingressos.
- QR Code dinâmico antifraude.
- Sincronização em tempo real com painel web.
- Registro de hora, dispositivo e operador que validou o ingresso.
- Check-in manual e modo offline (caso sem internet).

#### Pontos positivos
- Solução completa e integrada.
- Painel em tempo real com total de entradas.
- Modo offline eficiente.

#### Pontos a observar
- Interface do app pode limitar operações em grandes volumes (> 20k pessoas).

---

### [Ingresse](https://www.ingresse.com)

<div align="center">
    Figura 2: Ingresse — Portaria e Validação (ilustrativo)
    <br>
    <img src="assets/Benchmarking/ingresse.png" width="560" alt="Ingresse - portaria e validação">
    <br>
    <b>Fonte:</b> <a href="https://www.ingresse.com">Ingresse</a>.
    <br>
</div>

#### Foco observado
Plataforma com **aplicativo dedicado de portaria**, autenticação segura e **sincronização em múltiplos dispositivos**.

#### Recursos-chave
- Leitura de ingressos via QR Code (com ou sem internet).
- Atualização instantânea do status de entrada.
- Painel com estatísticas de público.
- Logs de validação com horário e responsável.
- Mecanismo de **detecção de duplicidade**.

#### Pontos positivos
- Robustez e confiabilidade em grandes eventos.
- Mecanismo antifraude eficiente.
- Integração direta com módulo financeiro.

#### Pontos a observar
- Customização de interface e relatórios é limitada a grandes parceiros.

---

### [BlueTicket](https://www.blueticket.com.br)

<div align="center">
    Figura 3: BlueTicket — Controle de Acesso (ilustrativo)
    <br>
    <img src="assets/Benchmarking/blue.png" width="560" alt="BlueTicket - controle de acesso">
    <br>
    <b>Fonte:</b> <a href="https://www.blueticket.com.br">BlueTicket</a>.
    <br>
</div>

#### Foco observado
Controle de acesso **por leitor dedicado** e **validação em tempo real** via rede segura.

#### Recursos-chave
- QR Code fixo e leitura via app oficial.
- Registro automático no sistema central.
- Múltiplos pontos de entrada com sincronização de dados.
- Dashboard com **percentual de público presente**.

#### Pontos positivos
- Sistema estável e simples de operar.
- Integração direta com vendas e relatórios.

#### Pontos a observar
- Falta de API pública para integrações de terceiros.

---

### [Ticketmaster](https://www.ticketmaster.com)

<div align="center">
    Figura 4: Ticketmaster — Access Control System (ilustrativo)
    <br>
    <img src="assets/Benchmarking/ticketmaster.png" width="560" alt="Ticketmaster - access control">
    <br>
    <b>Fonte:</b> <a href="https://www.ticketmaster.com">Ticketmaster</a>.
    <br>
</div>

#### Foco observado
Solução corporativa para **acesso de alto volume**, com **QR Code rotativo**, **biometria** e **integração com hardware** de portaria.

#### Recursos-chave
- QR Code rotativo (válido por segundos).
- Validação via leitores NFC e scanners fixos.
- Registro de eventos de entrada com GPS e timestamp.
- Dashboards com mapas de calor de público.
- API de integração com sistemas de segurança.

#### Pontos positivos
- Segurança avançada (criptografia e QR dinâmico).
- Escalabilidade para estádios e arenas.
- Suporte a biometria facial.

#### Pontos a observar
- Custo elevado para eventos pequenos/médios.
- Infraestrutura complexa.

---

## Requisitos Elicitados

> Requisitos derivados das soluções analisadas, com foco em **check-in, controle de acesso e antifraude** da plataforma **Ingressou**.

### Requisitos Funcionais

| Código | Requisito Funcional                                                                     | Objetivo                                                          | Origem (referência)          |
|--------|------------------------------------------------------------------------------------------|-------------------------------------------------------------------|------------------------------|
| RF-CK-01 | Permitir leitura de ingressos via QR Code único e antifraude.                          | Garantir segurança e agilidade no acesso.                         | Sympla, Ingresse, Ticketmaster |
| RF-CK-02 | Suportar modo offline com sincronização posterior.                                    | Operar mesmo sem internet.                                        | Sympla, Eventick             |
| RF-CK-03 | Exibir painel em tempo real com total de check-ins.                                   | Permitir controle operacional do evento.                          | Sympla, Ingresse, BlueTicket |
| RF-CK-04 | Registrar logs de validação (hora, operador, dispositivo).                            | Rastreabilidade e auditoria.                                      | Sympla, Ingresse             |
| RF-CK-05 | Detectar e alertar tentativas de uso duplicado de ingressos.                          | Prevenir fraudes e reentrada.                                     | Ingresse, Ticketmaster       |
| RF-CK-06 | Permitir múltiplos pontos de entrada sincronizados.                                   | Escalabilidade em grandes eventos.                                | BlueTicket, Ticketmaster     |
| RF-CK-07 | Suportar autenticação de operador e controle por perfil.                              | Segregar permissões por função.                                   | Sympla, Eventick             |
| RF-CK-08 | Exibir mapa de calor de público em eventos de grande porte.                           | Fornecer insights operacionais.                                   | Ticketmaster                 |
| RF-CK-09 | Permitir exportação de relatórios pós-evento (CSV/PDF).                               | Geração de documentação e controle pós-evento.                    | Eventick, Sympla             |
| RF-CK-10 | Permitir integração com leitores externos via API REST/WebSocket.                     | Conectar dispositivos e apps de terceiros.                        | Ticketmaster, BlueTicket     |

---

### Requisitos Não-Funcionais

| Código | Requisito Não-Funcional                                                                | Objetivo                                                            | Origem (referência)     |
|--------|-----------------------------------------------------------------------------------------|---------------------------------------------------------------------|--------------------------|
| RNF-CK-01 | Tempo de leitura do QR Code ≤ 1s (P90).                                              | Garantir fluxo rápido na entrada.                                   | Sympla, Ticketmaster     |
| RNF-CK-02 | Sistema de validação deve funcionar com latência < 200ms por requisição.             | Evitar filas e lentidão.                                            | Ingresse                 |
| RNF-CK-03 | Módulo de portaria com disponibilidade ≥ 99,9% durante o evento.                     | Evitar indisponibilidade durante o uso.                             | Ticketmaster             |
| RNF-CK-04 | Armazenar logs de validação por no mínimo 180 dias.                                 | Garantir rastreabilidade.                                           | Boas práticas            |
| RNF-CK-05 | Sincronização automática e segura (TLS + autenticação JWT).                          | Proteger dados de validação.                                        | Sympla, Stripe padrões   |
| RNF-CK-06 | Aplicativo mobile deve suportar mínimo Android 8 / iOS 13.                           | Compatibilidade ampla.                                              | Eventick, Sympla         |
| RNF-CK-07 | Interface responsiva e intuitiva para operação rápida.                              | Facilidade de uso em campo.                                         | BlueTicket, Ingresse     |
| RNF-CK-08 | Capacidade de lidar com picos de 10.000 check-ins simultâneos sem falha.             | Escalabilidade para grandes eventos.                                | Ticketmaster             |
| RNF-CK-09 | Suporte a fallback de sincronização para evitar perdas de dados offline.             | Resiliência e continuidade de operação.                             | Sympla, Eventick         |

---

## Histórico de versão

| Versão | Alteração                                      | Responsável  | Data       |
|-------:|------------------------------------------------|--------------|------------|
| 1.0    | Criação do benchmarking “Check-in e Validação de Ingressos” | Gabriel Lima | 15/10/2025 |
