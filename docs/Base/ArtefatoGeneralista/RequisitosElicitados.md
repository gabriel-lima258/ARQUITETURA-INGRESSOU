# Requisitos Elicitados

> Versão: 1.0  
> Data: Outubro de 2025  
> Autor: Gabriel Lima  
> Projeto: Ingressou — Plataforma Web de Venda e Gestão de Ingressos

---

## 📑 Sumário

* [Introdução](#introdução)
* [Visão Geral](#visão-geral)
* [Objetivos do Projeto](#objetivos-do-projeto)
* [Personas](#personas)
* [Escopo do Sistema](#escopo-do-sistema)
* [Requisitos Funcionais](#requisitos-funcionais)
* [Requisitos Não Funcionais](#requisitos-não-funcionais)
* [Regras de Negócio](#regras-de-negócio)
* [Critérios de Aceitação](#critérios-de-aceitação)
* [Requisitos Futuros e Extensões](#requisitos-futuros-e-extensões)
* [Considerações Finais](#considerações-finais)
* [Histórico de Versão](#histórico-de-versão)

---

## Introdução

O levantamento e a organização dos requisitos são etapas fundamentais no desenvolvimento do projeto Ingressou.  
Este documento apresenta, de forma estruturada e compreensível, os requisitos funcionais e não funcionais que orientam a construção da plataforma.

Os requisitos foram reunidos por meio de brainstorming, análises de benchmarking com plataformas semelhantes (por exemplo, Sympla) e pela identificação das necessidades de produtores de eventos, compradores e equipes de check-in.

O objetivo é garantir um entendimento claro e validável das funcionalidades essenciais e das regras de negócio, oferecendo uma base sólida para o desenvolvimento incremental do MVP e suas futuras evoluções.

---

## Visão Geral

O Ingressou é uma plataforma web que conecta produtores de eventos e usuários finais, permitindo a criação, venda e validação de ingressos digitais em todo o Brasil.

A solução busca ser moderna, segura e intuitiva, garantindo:
- Experiência fluida de compra e check-in.
- Pagamentos instantâneos (PIX e cartão).
- Transparência nos repasses financeiros.
- Controle antifraude com QR Codes únicos.
- Incentivos como cashback.

---

## Objetivos do Projeto

- Desenvolver um sistema completo de emissão, venda e gestão de ingressos digitais.  
- Oferecer pagamentos via PIX e cartões de forma segura e automatizada.  
- Garantir transparência e rapidez nos repasses aos produtores.  
- Fornecer controle antifraude e QR Codes assinados.  
- Promover cashback para incentivar retenção de usuários.  
- Atender múltiplos tipos de eventos: shows, palestras, teatros, igrejas e conferências.

---

## Personas

### 🎟️ Usuário Comprador
- Busca praticidade e segurança na compra de ingressos.  
- Prefere pagamentos rápidos e confiáveis (PIX, cartão).  
- Valoriza cashback, suporte imediato e QR Codes válidos.  

### 🧑‍💻 Produtor de Evento
- Deseja autonomia para criar e publicar eventos.  
- Precisa acompanhar vendas, repasses e lotes em tempo real.  
- Busca relatórios financeiros e métricas de desempenho.  

### 🧾 Staff (Equipe de Check-in)
- Responsável pela entrada e validação de ingressos.  
- Necessita de uma interface ágil e com modo offline.  
- Dev

---

## Escopo do Sistema

### Escopo Incluído (MVP)
- Cadastro e login de usuários e produtores.
- Criação e gerenciamento de eventos e lotes.
- Venda de ingressos online.
- Pagamento via PIX e cartão.
- Emissão automática de QR Codes antifraude.
- Painel do produtor com relatórios de vendas e repasses.
- Cashback de 2% no primeiro evento do usuário.
- Check-in via web (validação de QR).
- Envio de comprovante via e-mail e WhatsApp.
- Painel administrativo (monitoramento e auditoria).

### Escopo Futuro (fora do MVP)
- Revenda/transferência de ingressos (marketplace P2P).
- Programa de afiliados e influenciadores.
- Mapa de assentos/setorização visual.
- Aplicativo mobile nativo e carteiras (Apple/Google Wallet).
- White-label para grandes produtores.

---

# Requisitos Funcionais

Os requisitos a seguir foram organizados por **módulos de funcionalidades** para garantir clareza, rastreabilidade e precisão no desenvolvimento do sistema.

---

## 1. Módulo de Usuário e Autenticação

| ID | Requisito | Descrição Detalhada | Prioridade |
|----|------------|---------------------|-------------|
| RF01 | Cadastro de Usuário | O sistema deve permitir o cadastro de um novo usuário mediante o preenchimento obrigatório de nome completo, e-mail válido, CPF, telefone e senha. O sistema deve enviar um código de verificação (OTP) por e-mail para confirmar o cadastro antes de ativar a conta. | Alta |
| RF02 | Login de Usuário | O sistema deve permitir o login por e-mail e senha válidos. Em caso de erro, deve exibir mensagem “Credenciais inválidas”. | Alta |
| RF03 | Autenticação e Sessão | Após o login, o sistema deve gerar um token JWT com expiração de 1 hora e um token de atualização (refresh token) com validade de 7 dias. | Alta |
| RF04 | Recuperação de Senha | O sistema deve permitir a recuperação de senha via link enviado por e-mail válido. O link deve expirar em 30 minutos. | Média |
| RF05 | Edição de Perfil | O usuário deve poder atualizar suas informações pessoais (exceto CPF) mediante autenticação válida. | Média |

---

## 2. Módulo de Produtor de Eventos

| ID | Requisito | Descrição Detalhada | Prioridade |
|----|------------|---------------------|-------------|
| RF06 | Cadastro de Produtor | O sistema deve permitir o cadastro de produtores de eventos mediante CNPJ (ou CPF), razão social, chave PIX e aceite digital dos termos de serviço. | Alta |
| RF07 | Verificação de Produtor | O sistema deve validar a identidade do produtor mediante verificação de documento fiscal (CNPJ ativo ou CPF válido). | Alta |
| RF08 | Painel do Produtor | O produtor deve ter acesso a um painel com métricas em tempo real de vendas, status de ingressos e valores a repassar. | Alta |
| RF09 | Relatórios Financeiros | O painel deve permitir exportação em formato CSV contendo: nome do evento, lote, número de ingressos vendidos, valor bruto, taxa de serviço e valor líquido. | Alta |

---

## 3. Módulo de Eventos

| ID | Requisito | Descrição Detalhada | Prioridade |
|----|------------|---------------------|-------------|
| RF10 | Criação de Evento | O sistema deve permitir ao produtor criar eventos com os seguintes campos obrigatórios: nome, descrição, imagem (banner), local, cidade/UF, data e horário de início e fim, categoria (show, palestra, teatro, igreja, etc.) e status (rascunho, publicado ou encerrado). | Alta |
| RF11 | Edição e Exclusão de Evento | O sistema deve permitir que o produtor edite ou exclua eventos enquanto estiverem em status de “rascunho”. Após publicado, somente campos descritivos podem ser alterados. | Alta |
| RF12 | Publicação de Evento | O sistema deve permitir ao produtor publicar um evento apenas se houver pelo menos um lote de ingresso ativo e configurado. | Alta |
| RF13 | Visualização Pública | O sistema deve exibir os eventos publicados em página pública com nome, descrição, imagem, local, data, tipo e botão “Comprar”. | Alta |

---

## 4. Módulo de Lotes e Ingressos

| ID | Requisito | Descrição Detalhada | Prioridade |
|----|------------|---------------------|-------------|
| RF14 | Criação de Lotes | O produtor deve poder criar um ou mais lotes para o evento, definindo nome (Lote 1, 2, etc.), preço unitário, quantidade total e período de venda. | Alta |
| RF15 | Esgotamento de Lote | O sistema deve automaticamente marcar o lote como “esgotado” quando atingir o limite de ingressos vendidos. | Alta |
| RF16 | Tipos de Ingressos | O produtor deve poder criar ingressos do tipo inteira, meia-entrada, VIP ou cortesia, vinculados a um lote. | Alta |
| RF17 | Limite por CPF | O sistema deve restringir a compra de no máximo 5 ingressos por CPF para o mesmo evento. | Alta |
| RF18 | Política de Meia-Entrada | O sistema deve exigir declaração digital de estudante/beneficiário e registrar flag para verificação no check-in. | Média |

---

## 5. Módulo de Pagamentos e Checkout

| ID | Requisito | Descrição Detalhada | Prioridade |
|----|------------|---------------------|-------------|
| RF19 | Checkout de Compra | O sistema deve exibir um resumo da compra com itens, quantidades, valores, taxa de serviço e total antes do pagamento. | Alta |
| RF20 | Termos e Política | O usuário deve aceitar os termos de uso e política de reembolso antes de confirmar a compra. | Alta |
| RF21 | Pagamento via PIX | O sistema deve gerar QR Code dinâmico do PSP parceiro e reservar o ingresso por 10 minutos até confirmação automática. Após o prazo, a reserva expira. | Alta |
| RF22 | Pagamento via Cartão | O sistema deve processar pagamentos via gateway homologado (ex: Pagar.me), com autenticação 3DS e verificação antifraude. | Alta |
| RF23 | Confirmação de Pagamento | Após confirmação do pagamento, o sistema deve mudar o status do pedido para “Pago” e liberar o ingresso. | Alta |
| RF24 | Falha no Pagamento | Em caso de falha ou cancelamento, o pedido deve ser cancelado e a reserva liberada. | Alta |

---

## 6. Módulo de Ingressos e QR Code

| ID | Requisito | Descrição Detalhada | Prioridade |
|----|------------|---------------------|-------------|
| RF25 | Emissão de Ingressos | Após o pagamento confirmado, o sistema deve gerar um ingresso digital com ID único, código alfanumérico e QR Code assinado digitalmente. | Alta |
| RF26 | Validade do Ingresso | Cada QR Code deve ter validade única e expirar após o primeiro uso validado. | Alta |
| RF27 | Reenvio de Ingresso | O usuário deve poder solicitar reenvio do ingresso por e-mail autenticado. | Média |
| RF28 | Envio Automático | O sistema deve enviar e-mail e mensagem WhatsApp automáticos com o ingresso após pagamento confirmado. | Alta |

---

## 7. Módulo de Check-in e Validação

| ID | Requisito | Descrição Detalhada | Prioridade |
|----|------------|---------------------|-------------|
| RF29 | Validação de Ingressos | O sistema deve permitir a leitura do QR Code via câmera ou leitor e validar seu status (válido, duplicado, expirado). | Alta |
| RF30 | Registro de Check-in | O sistema deve registrar data, hora e operador que validou o ingresso. | Alta |
| RF31 | Modo Offline | O sistema deve permitir validação offline com sincronização posterior ao servidor central. | Média |
| RF32 | Relatórios de Check-in | O produtor deve visualizar a quantidade total de entradas validadas e exportar relatório CSV. | Média |

---

## 8. Módulo de Cashback

| ID | Requisito | Descrição Detalhada | Prioridade |
|----|------------|---------------------|-------------|
| RF33 | Cálculo de Cashback | O sistema deve calcular automaticamente 2% de cashback sobre o valor total da compra do primeiro evento do usuário. | Média |
| RF34 | Registro de Cashback | O valor de cashback deve ser armazenado no saldo de “Carteira do Usuário”. | Média |
| RF35 | Utilização de Cashback | O usuário deve poder aplicar o saldo disponível em novas compras até o limite total. | Baixa |

---

## 9. Módulo de Administração

| ID | Requisito | Descrição Detalhada | Prioridade |
|----|------------|---------------------|-------------|
| RF36 | Painel Administrativo | O administrador deve visualizar lista de usuários, produtores, eventos e vendas. | Alta |
| RF37 | Auditoria de Operações | O sistema deve registrar logs detalhados de criação, edição, cancelamento e validação de ingressos. | Alta |
| RF38 | Gerenciamento de Fraudes | O admin deve poder bloquear usuários ou eventos suspeitos. | Alta |
| RF39 | Parâmetros de Sistema | O admin deve poder configurar taxas, cashback, limites e mensagens institucionais. | Média |

---

# Requisitos Não Funcionais

| ID | Requisito Não Funcional | Descrição | Categoria |
|----|--------------------------|------------|------------|
| RNF01 | Desempenho | O sistema deve processar requisições em até 2 segundos em 90% das operações (P90). | Performance |
| RNF02 | Disponibilidade | O sistema deve garantir disponibilidade mínima de 99,5% mensal. | Confiabilidade |
| RNF03 | Segurança de Conexão | Todo o tráfego deve ser feito via HTTPS (TLS 1.2 ou superior). | Segurança |
| RNF04 | Proteção de Dados | Dados sensíveis devem ser criptografados com AES-256 e acessos auditados. | Segurança |
| RNF05 | Autenticação JWT | Tokens de sessão devem expirar em 1 hora, e refresh tokens em 7 dias. | Segurança |
| RNF06 | Antifraude QR | QR Codes devem ser gerados com assinatura digital única (JWT com nonce). | Segurança |
| RNF07 | Escalabilidade | O sistema deve suportar crescimento de usuários sem impacto perceptível no desempenho. | Arquitetura |
| RNF08 | Portabilidade | A interface deve ser responsiva e compatível com dispositivos móveis. | Usabilidade |
| RNF09 | Acessibilidade | O sistema deve seguir padrões WCAG 2.1 nível AA. | Usabilidade |
| RNF10 | Persistência | Banco de dados PostgreSQL com backup diário e retenção mínima de 30 dias. | Infraestrutura |
| RNF11 | Observabilidade | Logs, métricas e tracing devem seguir padrões OpenTelemetry e Sentry. | Engenharia |
| RNF12 | Compatibilidade | O sistema deve funcionar corretamente nos navegadores Chrome, Firefox, Edge e Safari (últimas duas versões). | Usabilidade |
| RNF13 | LGPD | O sistema deve cumprir a Lei Geral de Proteção de Dados (Lei 13.709/2018), garantindo consentimento e exclusão sob demanda. | Conformidade |

---

# Regras de Negócio

| ID | Regra de Negócio | Descrição |
|----|------------------|------------|
| RB01 | Taxa de Plataforma | A plataforma deve reter 8% do valor de cada ingresso vendido. |
| RB02 | Cashback | O cashback de 2% aplica-se apenas à primeira compra do usuário. |
| RB03 | Limite por CPF | Um mesmo CPF não pode adquirir mais de 5 ingressos por evento. |
| RB04 | Reserva PIX | A reserva expira em 10 minutos se o pagamento não for confirmado. |
| RB05 | Estorno | Estornos são permitidos até 7 dias antes do evento, conforme política. |
| RB06 | Meia-Entrada | A meia-entrada só é válida mediante documento comprobatório no check-in. |
| RB07 | Split de Pagamento | O sistema deve dividir automaticamente o valor entre plataforma e produtor. |
| RB08 | Nota Fiscal | A Ingressou deve emitir NFS-e apenas sobre o valor de sua taxa de serviço. |
| RB09 | Política de Privacidade | Todos os usuários devem aceitar os termos e políticas de uso antes de efetuar compras. |
| RB10 | Check-in Único | Cada ingresso (QR Code) pode ser validado apenas uma vez. Tentativas repetidas devem ser bloqueadas. |

---

## Critérios de Aceitação

- Publicação de evento: produtor cria evento com lotes e publica; status e estoque atualizam corretamente.  
- Compra concluída: usuário paga (PIX/cartão) e recebe comprovante + QR por e-mail/WhatsApp.  
- Validação única: QR é aceito na primeira leitura e recusado nas seguintes (anti-replay).  
- Cashback: 2% creditado automaticamente no primeiro evento e exibido em “Carteira”.  
- Relatórios: produtor exporta CSV com vendas por lote/período e visualiza métricas no dashboard.  
- Logs/Auditoria: ações críticas (criação, cancelamento, check-in) constam em trilha de auditoria.

---

## Requisitos Futuros e Extensões

- Integração com Google/Apple Wallet.  
- Revenda e transferência segura de ingressos.  
- Programa de afiliados e influenciadores.  
- Aplicativo mobile (React Native ou Flutter).  
- White-label para grandes organizadores.

---

## Considerações Finais

O projeto **Ingressou** busca revolucionar o mercado de eventos digitais no Brasil, aliando **tecnologia, confiança e experiência fluida**.  
Este documento consolida os requisitos essenciais para a **fase de desenvolvimento do MVP**, servindo como guia de referência técnica e estratégica para toda a equipe.

> “Ingressou — seu rolê começa aqui.” 🎫

---

## Histórico de Versão

| Versão | Alteração                                   | Responsável  | Data       |
|--------|---------------------------------------------|--------------|------------|
| 1.0    | Elaboração inicial do Documento de Requisitos | Gabriel Lima | 15/10/2025 |
