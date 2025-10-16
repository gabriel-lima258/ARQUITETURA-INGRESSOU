# Requisitos Elicitados — Ingressou

> **Versão:** 1.2  
> **Data:** Outubro de 2025  
> **Autor:** Gabriel Lima  
> **Projeto:** Ingressou — Plataforma Web de Venda e Gestão de Ingressos

---

## Sumário

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

Este documento consolida os requisitos funcionais e não funcionais do Ingressou.  
A versão 1.2 aplica as seguintes decisões: **eventos são criados exclusivamente pelo Administrador**, **lotes encerram pelo primeiro limite atingido (tempo ou quantidade)**, **checkout aceita cupom de influenciador**, uso de **mensageria** e **cache** e, principalmente, **cashback destinado ao produtor (não ao usuário comprador)**.

---

## Visão Geral

Plataforma que conecta administradores e produtores a usuários finais para venda e validação de ingressos em todo o Brasil, com pagamentos via PIX e cartão, QR Code antifraude, cupons de influenciadores e cashback financeiro para produtores.

---

## Objetivos do Projeto

- Emitir, vender e gerenciar ingressos digitais com segurança e desempenho.  
- Oferecer pagamentos via PIX e cartões com split e repasses transparentes.  
- Garantir antifraude (QR assinado) e check-in confiável.  
- Adotar mensageria e cache para robustez, escalabilidade e performance.  
- Potencializar aquisição via cupons de influenciadores.  
- Incentivar oferta de eventos via **cashback ao produtor**.

---

## Personas

**Usuário Comprador** — compra rápida via PIX/cartão, quer confirmação imediata e QR confiável.  
**Produtor de Evento** — acompanha vendas, repasses, lotes e check-ins; beneficia-se de cashback no painel.  
**Staff (Check-in)** — valida ingressos com baixa latência, inclusive offline.  
**Administrador** — cria/publica eventos, define lotes, políticas, cupons e parâmetros do sistema.

---

## Escopo do Sistema

### Incluído (MVP)
- Autenticação e perfis (usuário, produtor, admin).  
- **Criação/publicação de eventos pelo Administrador.**  
- Lotes por evento, com janela de venda e quantidade.  
- Vendas online; pagamentos via PIX e cartão.  
- Emissão de QR Code antifraude.  
- Painel do produtor (vendas, repasses, relatórios).  
- **Cupom de influenciador** no checkout.  
- **Cashback financeiro para o produtor**.  
- Check-in via web (online/offline).  
- Mensageria para e-mails/WhatsApp/webhooks/exports.  
- Cache para páginas, listagens e estatísticas.  
- Painel administrativo.

### Futuro
- Marketplace P2P (revenda/transferência).  
- Assentos/setorização visual.  
- App nativo; Apple/Google Wallet.  
- White-label.

---

# Requisitos Funcionais

> Organização por módulos. Itens atualizados ou novos foram incorporados.

## 1. Usuário e Autenticação

| ID   | Requisito            | Descrição                                                                                         | Prioridade |
|------|----------------------|---------------------------------------------------------------------------------------------------|------------|
| RF01 | Cadastro de Usuário  | Nome, e-mail, CPF, telefone e senha; confirmação por OTP enviado ao e-mail antes de ativação.    | Alta       |
| RF02 | Login                | Autenticação por e-mail e senha; em erro exibir “Credenciais inválidas”.                         | Alta       |
| RF03 | Sessão JWT           | Gerar JWT (expira em 1h) e refresh token (7 dias).                                                | Alta       |
| RF04 | Recuperação de Senha | Redefinição via link enviado por e-mail; link expira em 30 minutos.                              | Média      |
| RF05 | Edição de Perfil     | Atualização de dados pessoais (exceto CPF) mediante autenticação.                                | Média      |

## 2. Produtor (Perfil e Painel)

| ID   | Requisito             | Descrição                                                                                          | Prioridade |
|------|-----------------------|----------------------------------------------------------------------------------------------------|------------|
| RF06 | Cadastro de Produtor  | CNPJ/CPF, razão social, chave PIX e aceite dos termos.                                             | Alta       |
| RF07 | Verificação           | Validar CNPJ ativo/CPF válido (KYC básico).                                                        | Alta       |
| RF08 | Painel do Produtor    | Exibir métricas de vendas, check-ins, repasses e **saldo de cashback** em tempo quase real.       | Alta       |
| RF09 | Relatórios CSV        | Exportar por evento/lote com bruto, taxas, descontos, líquido e repasses.                         | Alta       |

## 3. Eventos (Criados pelo Administrador)

| ID   | Requisito                   | Descrição                                                                                                                                 | Prioridade |
|------|-----------------------------|-------------------------------------------------------------------------------------------------------------------------------------------|------------|
| RF10 | Criação de Evento (Admin)   | Somente Administrador cria eventos com: nome, descrição, banner, local, cidade/UF, datas de início/fim, categoria e status (rascunho/publicado/encerrado). | Alta       |
| RF11 | Edição/Exclusão (Admin)     | Edição/remoção permitidas em rascunho. Após publicar, apenas campos não críticos (ex.: descrição, banner).                               | Alta       |
| RF12 | Publicação (Admin)          | Publicar somente se houver pelo menos 1 lote válido (ver Módulo 4).                                                                      | Alta       |
| RF13 | Página Pública do Evento    | Exibir evento publicado com nome, descrição, imagem, local, data e botão “Comprar”.                                                      | Alta       |

## 4. Lotes e Ingressos

| ID   | Requisito                        | Descrição                                                                                                                        | Prioridade |
|------|----------------------------------|----------------------------------------------------------------------------------------------------------------------------------|------------|
| RF14 | Criação de Lotes (Admin)         | Lote com nome, preço, quantidade total, janela de venda (início/fim) e status.                                                  | Alta       |
| RF15 | Encerramento de Lote por Limite  | Encerrar automaticamente quando qualquer limite ocorrer primeiro: esgotar quantidade **ou** atingir o fim da janela de venda.   | Alta       |
| RF16 | Tipos de Ingressos               | Inteira, meia, VIP, cortesia; sempre vinculados a um lote.                                                                       | Alta       |
| RF17 | Limite por CPF                   | Máximo de 5 ingressos por CPF por evento (configurável).                                                                         | Alta       |
| RF18 | Política de Meia-entrada         | Exigir declaração digital e registrar flag para verificação no check-in.                                                         | Média      |

## 5. Pagamentos, Cupons e Checkout

| ID   | Requisito                | Descrição                                                                                                                                                          | Prioridade |
|------|--------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|
| RF19 | Checkout                 | Exibir resumo de itens, quantidades, taxas e total antes do pagamento.                                                                                             | Alta       |
| RF20 | Termos e Políticas       | Exigir aceite dos termos de uso e política de reembolso antes do pagamento.                                                                                        | Alta       |
| RF21 | Pagamento via PIX        | Gerar QR dinâmico; reservar itens por 10 minutos; confirmação via webhook do PSP; expirada a reserva, liberar estoque.                                            | Alta       |
| RF22 | Pagamento via Cartão     | Processar via gateway homologado (ex.: Pagar.me) com 3DS/antifraude; tratar callbacks assíncronos.                                                                 | Alta       |
| RF23 | Confirmação de Pagamento | Ao confirmar, pedido “Pago” e liberação de emissão dos ingressos.                                                                                                  | Alta       |
| RF24 | Falha no Pagamento       | Em falha/cancelamento, cancelar pedido e liberar reserva/estoque.                                                                                                  | Alta       |
| RF25 | Cupom de Influenciador   | Aplicar código por evento/lote, com valor fixo ou percentual, vigência, limite de uso, acúmulo configurável com outras promoções e registro de atribuição ao influenciador. | Alta       |

## 6. Ingressos e QR Code

| ID   | Requisito         | Descrição                                                                                   | Prioridade |
|------|-------------------|-----------------------------------------------------------------------------------------------|------------|
| RF26 | Emissão           | Após pagamento, gerar ingresso digital com ID único e QR Code assinado digitalmente.         | Alta       |
| RF27 | Validade          | QR Code expira após o primeiro uso validado.                                                 | Alta       |
| RF28 | Reenvio           | Permitir reenvio de ingresso por e-mail mediante autenticação.                               | Média      |
| RF29 | Envio Automático  | Enviar e-mail e WhatsApp com ingresso quando o pagamento for confirmado.                     | Alta       |

## 7. Check-in e Validação

| ID   | Requisito            | Descrição                                                                                 | Prioridade |
|------|----------------------|-------------------------------------------------------------------------------------------|------------|
| RF30 | Validação            | Ler QR (câmera/leitor) e retornar status: válido/duplicado/expirado.                      | Alta       |
| RF31 | Registro             | Logar data, hora, operador e dispositivo da validação.                                    | Alta       |
| RF32 | Modo Offline         | Validar ingressos offline com sincronização posterior.                                    | Média      |
| RF33 | Relatórios Check-in  | Exibir total de entradas validadas e exportar CSV.                                        | Média      |

## 8. Financeiro do Produtor e Cashback

| ID   | Requisito              | Descrição                                                                                                                                         | Prioridade |
|------|------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------|------------|
| RF34 | Cálculo de Cashback    | Calcular automaticamente **2% de cashback** sobre o **valor líquido** das vendas do produtor por evento (parâmetro configurável).               | Média      |
| RF35 | Registro de Cashback   | Creditar o valor na **conta financeira do produtor** como saldo de repasse adicional; exibir no painel por evento/período, com extrato detalhado. | Média      |
| RF36 | Uso do Cashback        | Permitir ao produtor **abater taxas da plataforma** ou **destinar a campanhas promocionais** (ex.: destaque/push do evento) usando o saldo.     | Baixa      |

## 9. Administração

| ID   | Requisito          | Descrição                                                                                              | Prioridade |
|------|--------------------|--------------------------------------------------------------------------------------------------------|------------|
| RF37 | Painel Admin       | Listar usuários, produtores, eventos, vendas, cupons e cashback de produtores.                        | Alta       |
| RF38 | Auditoria          | Registrar logs de criar/editar/publicar/cancelar/validar; trilha completa com usuário e timestamp.    | Alta       |
| RF39 | Fraudes            | Bloquear usuários ou eventos suspeitos.                                                                | Alta       |
| RF40 | Parâmetros Globais | Configurar taxas, regras de cashback do produtor, limites, cupons de influenciador e mensagens padrão. | Média      |

---

# Requisitos Não Funcionais

| ID    | Requisito                    | Descrição                                                                                                                                     | Categoria       |
|-------|------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------|-----------------|
| RNF01 | Desempenho                   | P90 ≤ 2s nas operações do usuário e do painel.                                                                                                | Performance     |
| RNF02 | Disponibilidade              | Disponibilidade mensal ≥ 99,5% (MVP).                                                                                                         | Confiabilidade  |
| RNF03 | Segurança de Trânsito        | HTTPS (TLS 1.2+) com HSTS e CSP.                                                                                                             | Segurança       |
| RNF04 | Proteção de Dados            | Criptografia at rest (AES-256); segredos em cofre; RBAC por perfis.                                                                          | Segurança       |
| RNF05 | JWT Seguro                   | JWT expira em 1h; refresh em 7 dias; rotação e revogação de tokens.                                                                          | Segurança       |
| RNF06 | Antifraude QR                | Assinatura digital (JWT + nonce) com verificação anti-replay.                                                                                | Segurança       |
| RNF07 | Escalabilidade               | Horizontalização com containers e auto-scale para picos de tráfego.                                                                          | Arquitetura     |
| RNF08 | Responsividade               | Mobile-first; PWA para módulo de check-in.                                                                                                    | Usabilidade     |
| RNF09 | Acessibilidade               | Conformidade WCAG 2.1 AA.                                                                                                                     | Usabilidade     |
| RNF10 | Persistência                 | PostgreSQL; backup diário; retenção ≥ 30 dias; testes periódicos de restauração.                                                              | Infraestrutura  |
| RNF11 | Observabilidade              | Logs estruturados, métricas e tracing (OpenTelemetry/Sentry).                                                                                 | Engenharia      |
| RNF12 | Compatibilidade              | Suporte às duas últimas versões de Chrome, Firefox, Edge e Safari.                                                                            | Usabilidade     |
| RNF13 | LGPD                         | Consentimento, portabilidade e exclusão sob demanda (Lei 13.709/2018).                                                                        | Conformidade    |
| RNF14 | Mensageria/Filas             | Broker (RabbitMQ/Kafka/SQS) para jobs assíncronos: e-mails/WhatsApp, webhooks de pagamento, geração de QR, exportações; idempotência; retries; DLQ. | Arquitetura     |
| RNF15 | Cache                        | Redis para páginas públicas, listagens, estatísticas agregadas e disponibilidade de lotes; invalidação por evento/lote.                       | Performance     |
| RNF16 | Idempotência de Pagamentos   | Webhooks e criação de pedidos idempotentes com chave de deduplicação.                                                                         | Engenharia      |

---

# Regras de Negócio

| ID    | Regra                        | Descrição                                                                                                                    |
|-------|------------------------------|------------------------------------------------------------------------------------------------------------------------------|
| RB01  | Taxa da Plataforma           | 8% sobre cada ingresso vendido.                                                                                              |
| RB02  | Cashback do Produtor         | 2% do valor líquido de vendas (parâmetro) é revertido como saldo de cashback para o produtor e exibido no painel financeiro.|
| RB03  | Limite por CPF               | Máximo de 5 ingressos por CPF por evento (configurável).                                                                     |
| RB04  | Reserva PIX                  | Reserva expira em 10 minutos sem confirmação do pagamento.                                                                   |
| RB05  | Estorno                      | Estornos permitidos até 7 dias antes do evento, conforme política.                                                           |
| RB06  | Meia-entrada                 | Válida mediante comprovação no check-in.                                                                                     |
| RB07  | Split/Repasses               | Repasses automáticos D+X conforme contrato e KYC.                                                                            |
| RB08  | Nota Fiscal                  | Emissão de NFS-e apenas sobre a taxa de serviço da plataforma.                                                               |
| RB09  | Termos/Privacidade           | Aceite obrigatório dos termos de uso e política de privacidade (LGPD).                                                       |
| RB10  | Check-in Único               | Cada ingresso (QR Code) pode ser validado uma única vez; tentativas repetidas são bloqueadas.                                |
| RB11  | Lote por Tempo/Quantidade    | O lote encerra pelo primeiro limite atingido: esgotamento da quantidade ou término da janela de venda.                       |
| RB12  | Cupom de Influenciador       | Usuário pode aplicar cupom de influenciador no checkout; desconto percentual ou fixo; vigência e limites configuráveis.      |
| RB13  | Criação de Evento            | Somente o Administrador cria e publica eventos; produtores não criam eventos.                                                |

---

## Critérios de Aceitação

- **Publicação de evento (Admin):** publicar somente com ao menos 1 lote válido; páginas públicas ficam acessíveis após publicação.  
- **Encerramento de lote:** ao vender a última unidade **ou** atingir a hora final da janela, o lote muda para “esgotado” e sai do checkout.  
- **Cupom de influenciador:** aplicar desconto quando código válido; registrar atribuição ao influenciador; respeitar vigência e limites.  
- **PIX com reserva:** se o webhook não confirmar em 10 minutos, o pedido volta para “cancelado” e as unidades retornam ao estoque.  
- **Cashback do produtor:** ao encerrar o período do evento, calcular 2% do líquido (ou parâmetro) e creditar no saldo financeiro do produtor; refletir no painel e extrato.  
- **Mensageria:** e-mails/WhatsApp, geração de QR e exportações são enfileirados; com retries e DLQ; requests síncronos não bloqueiam.  
- **Cache:** respostas de eventos populares retornam com baixa latência; alterações invalidam caches afetados.

---

## Requisitos Futuros e Extensões

- Apple/Google Wallet, app nativo, afiliados/influenciadores avançado, marketplace P2P e assentos visuais.

---

## Considerações Finais

A versão 1.2 alinha governança (Admin cria eventos), políticas comerciais (cupom de influenciador), operação de vendas (lote por tempo/quantidade), arquitetura (mensageria e cache) e modelo de incentivo focado no **produtor** via **cashback financeiro**.

---

## Histórico de Versão

| Versão | Alteração                                                                                                     | Responsável  | Data       |
|-------:|---------------------------------------------------------------------------------------------------------------|--------------|------------|
| 1.0    | Elaboração inicial                                                                                            | Gabriel Lima | 15/10/2025 |
| 1.1    | Eventos por Admin; lotes por tempo/quantidade; cupom de influenciador; mensageria e cache                     | Gabriel Lima | 16/10/2025 |
| 1.2    | Cashback alterado para produtor; remoção de qualquer cashback do usuário; ajustes em escopo, RF, RNF e regras | Gabriel Lima | 16/10/2025 |
