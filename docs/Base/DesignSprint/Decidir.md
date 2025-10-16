# Design Sprint – Decisão (Decision)

> **Versão:** 1.0  
> **Data:** Outubro de 2025  
> **Autor:** Gabriel Lima  
> **Projeto:** Ingressou — Plataforma Web de Venda e Gestão de Ingressos

---

## 🎯 Objetivo

Representar visualmente, em sequência narrativa, o **fluxo principal de interação do usuário** dentro do sistema **Ingressou**, desde a descoberta de um evento até o check-in no dia do show.

O storyboard orienta a próxima fase do Design Sprint (**Decidir**), servindo como base para a prototipação de telas de alta fidelidade.

---

## 📑 Estrutura das Cenas

Cada cena apresenta:
- **Título** – O momento da jornada.  
- **Contexto visual** – O que aparece na tela / ambiente.  
- **Ação do usuário** – O que ele faz.  
- **Resposta do sistema** – O que acontece após a ação.  
- **Objetivo da cena** – O propósito dessa etapa.

---

## 🧩 Cenas do Storyboard

### 🖥️ Cena 1 — Descoberta do Evento

| Elemento | Descrição |
|-----------|------------|
| **Contexto visual** | Tela inicial da plataforma, com eventos em destaque e filtros por cidade e data. |
| **Ação do usuário** | O usuário pesquisa “Festival de Brasília” e clica no evento desejado. |
| **Resposta do sistema** | Página do evento é carregada com banner, descrição, datas e ingressos disponíveis. |
| **Objetivo** | Permitir que o usuário encontre facilmente o evento de interesse. |

---

### 🎟️ Cena 2 — Escolha do Ingresso

| Elemento | Descrição |
|-----------|------------|
| **Contexto visual** | Página do evento com seções: “Lotes disponíveis”, “Local”, “Descrição” e botão “Comprar ingresso”. |
| **Ação do usuário** | Seleciona o lote “2º Lote – R$120” e clica em “Comprar”. |
| **Resposta do sistema** | Sistema adiciona o ingresso ao carrinho e exibe o resumo da compra. |
| **Objetivo** | Demonstrar o comportamento da seleção de lotes e transparência no preço. |

---

### 💳 Cena 3 — Checkout e Pagamento

| Elemento | Descrição |
|-----------|------------|
| **Contexto visual** | Tela de checkout com formulário de dados pessoais, campo para cupom de influenciador e métodos de pagamento (PIX / Cartão). |
| **Ação do usuário** | Insere o cupom “@JOAOSHOW” e paga via PIX. |
| **Resposta do sistema** | Sistema valida o cupom, aplica o desconto e gera QR Code de pagamento com tempo limite de 10 minutos. |
| **Objetivo** | Garantir experiência de compra simples e segura, com comunicação clara de taxa e tempo de reserva. |

---

### 📩 Cena 4 — Confirmação e Envio do Ingresso

| Elemento | Descrição |
|-----------|------------|
| **Contexto visual** | Tela de sucesso com mensagem “Pagamento confirmado!” e botões “Ver ingressos” e “Compartilhar no WhatsApp”. |
| **Ação do usuário** | Clica em “Ver ingressos”. |
| **Resposta do sistema** | Sistema exibe QR Code do ingresso e envia cópia por e-mail e WhatsApp. |
| **Objetivo** | Reforçar segurança e rastreabilidade; automatizar comunicação pós-compra. |

---

### 📱 Cena 5 — Check-in no Evento (PWA)

| Elemento | Descrição |
|-----------|------------|
| **Contexto visual** | Tela do staff no modo PWA, com câmera ativada e contador de ingressos validados. |
| **Ação do usuário (staff)** | Escaneia o QR Code do participante. |
| **Resposta do sistema** | Exibe alerta “✅ Ingresso válido” e registra a hora e operador. |
| **Objetivo** | Agilizar a entrada e garantir antifraude via assinatura digital do QR. |

---

### 💼 Cena 6 — Painel do Produtor

| Elemento | Descrição |
|-----------|------------|
| **Contexto visual** | Dashboard com métricas de vendas, gráficos de desempenho por lote e saldo de cashback. |
| **Ação do usuário** | O produtor acessa “Relatórios” e visualiza o repasse financeiro. |
| **Resposta do sistema** | Mostra extrato do evento e saldo atualizado. |
| **Objetivo** | Demonstrar controle e transparência para o produtor. |

---

### 🧮 Cena 7 — Painel do Administrador

| Elemento | Descrição |
|-----------|------------|
| **Contexto visual** | Painel administrativo com cards de eventos, status (rascunho, publicado, encerrado) e configurações de cashback e taxas. |
| **Ação do usuário (Admin)** | Cria novo evento, define lotes e publica. |
| **Resposta do sistema** | Evento é disponibilizado no catálogo público e começa a gerar vendas. |
| **Objetivo** | Reforçar a centralização da governança e a regra “Admin cria e publica eventos”. |

---

## 📘 Histórico de Versão

| Versão | Alteração | Responsável | Data |
| - | - | - | - |
| 1.0 | Criação do Storyboard do fluxo principal | Gabriel Lima | 16/10/2025 |
