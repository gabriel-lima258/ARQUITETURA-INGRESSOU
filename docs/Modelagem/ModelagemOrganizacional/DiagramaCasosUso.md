# Diagrama de Casos de Uso

## Sumário

- [Introdução](#Introdução)
- [Objetivos](#Objetivos)
- [Metodologia](#Metodologia)
- [Sobre o Diagrama de Casos de Uso](#Sobre-o-Diagrama-de-Casos-de-Uso)
- [Diagrama de Casos de Uso](#Diagrama-de-Casos-de-Uso)
- [Conclusão](#Conclusão)
- [Bibliografia](#Bibliografia)
- [Histórico de versão](#Histórico-de-versão)


## Introdução

O Diagrama de Casos de Uso é um dos diagramas comportamentais da UML (Unified Modeling Language), fundamental para capturar os requisitos funcionais de um sistema sob a perspectiva do usuário. Conforme descrito por [Diagrama de caso de uso UML: O que é, como fazer e exemplos](https://www.lucidchart.com/pages/pt/diagrama-de-caso-de-uso-uml) [3](#ref3) e [O que é UML e Diagramas de Caso de Uso: Introdução Prática à UML](https://www.devmedia.com.br/o-que-e-uml-e-diagramas-de-caso-de-uso-introducao-pratica-a-uml/23408) [2](#ref2), ele identifica quem interage com o sistema (Atores) e o que esses atores podem fazer (Casos de Uso) ao definir o escopo e as funcionalidades principais da aplicação de forma visual e intuitiva. Portanto, segundo a [IBM](https://www.ibm.com/docs/pt-br/rsm/7.5.0?topic=diagrams-use-case) [4](#ref4), este diagrama é essencial para comunicar o propósito e o comportamento esperado do sistema para diferentes stakeholders.

# Caso de Uso: Comprar Ingresso

Este documento detalha o caso de uso para a funcionalidade de compra de ingressos em uma plataforma de eventos.

##  Visão Geral

| Item | Descrição |
| --- | --- |
| **Identificador** | CU-01 |
| **Nome** | Comprar Ingresso |
| **Ator Principal** | Cliente (usuário final da plataforma) |
| **Atores Secundários** | - Sistema de Pagamento (Pagar.me, Mercado Pago)<br>- Sistema de Notificações (E-mail, WhatsApp)<br>- Gateway de API (Nginx)<br>- Serviço de Cupons (caso aplicável) |
| **Descrição** | Permitir que um cliente selecione um evento, escolha ingressos disponíveis, aplique cupom de desconto (se houver), realize o pagamento e receba seus ingressos digitais, com QR Code seguro, diretamente em sua carteira. |

## Condições e Requisitos

### Pré-condições

- O cliente deve estar autenticado (login com e-mail/senha ou Google/Apple).
- Deve haver eventos publicados com lotes disponíveis à venda.
- O cliente deve possuir um método de pagamento válido (cartão/Pix).
- Caso use cupom, ele deve estar ativo e válido.

### Pós-condições

- O pedido é registrado com status “Pago” ou “Aguardando Confirmação”.
- Os ingressos são gerados e atribuídos à carteira do cliente.
- As notificações são enviadas por e-mail e/ou WhatsApp.
- Os QR Codes são gerados e armazenados (com assinatura).
- O produtor recebe o valor bruto e a comissão é calculada (cashback e repasse ficam programados).

## Fluxos de Execução

### Fluxo Principal (Caminho Feliz)

1. O cliente acessa a página de um evento.
2. Seleciona o(s) lote(s) e a quantidade de ingressos desejada.
3. [Opcional] Insere um cupom de desconto.
4. O sistema aplica validações (disponibilidade de ingressos, validade do cupom, políticas de quantidade).
5. O cliente escolhe o método de pagamento (cartão de crédito, Pix).
6. O sistema integra-se com o gateway de pagamento, inicia a cobrança e aguarda a autorização.
7. Após a confirmação de pagamento, o sistema:
    - Cria o Pedido.
    - Gera os Ingressos com QR Code.
    - Atribui os ingressos à Carteira do cliente.
    - Envia notificações de confirmação (E-mail, WhatsApp).
8. O pedido fica disponível na tela “Meus Ingressos”.

### Fluxos Alternativos

- **3a. Cupom inválido ou expirado:**
    - O sistema rejeita o cupom e exibe a mensagem: “Cupom inválido ou expirado”.
- **6a. Pagamento pendente (Pix):**
    - O pedido é criado com status “Aguardando Pagamento”.
    - O sistema monitora o pagamento por webhook e, após a confirmação, o fluxo segue a partir do passo 7 do fluxo principal.
- **6b. Pagamento recusado:**
    - O sistema exibe uma mensagem de erro e permite uma nova tentativa.
    - Uma tentativa malsucedida é registrada para prevenção de fraude.

## Exceções

| Código | Situação | Tratamento |
| --- | --- | --- |
| EXC-01 | Evento ou lote expirado | Redirecionar o cliente para a página inicial com um alerta. |
| EXC-02 | Falha na API de pagamento | Exibir um erro amigável. Logar a falha e enviar um alerta para a equipe de suporte. |
| EXC-03 | Falha na geração do QR Code | Tentar um fallback ou gerar em um processo em batch posterior. Notificar o usuário sobre o atraso. |
| EXC-04 | Cliente tenta comprar mais do que o limite permitido | Exibir a mensagem: “Limite de ingressos por CPF excedido.” |

## Requisitos Relacionados

| Tipo | ID | Descrição |
| --- | --- | --- |
| RF | RF06 | Visualizar eventos |
| RF | RF11 | Comprar ingresso |
| RF | RF13 | Aplicar cupom |
| RF | RF15 | Receber ingresso por e-mail |
| RF | RF20 | Acessar ingressos adquiridos |
| RNF | RNF02 | Alta disponibilidade |
| RNF | RNF04 | Segurança de dados e transações |
| RNF | RNF05 | Observabilidade com métricas de compra |

## Regras de Negócio

- Um cliente só pode comprar até X ingressos por CPF (definido por lote).
- O cupom pode ser individual, acumulativo ou de influenciador, com limitações por tempo ou quantidade de usos.
- O QR Code é assinado digitalmente com chave privada e só pode ser validado uma vez.
- O cashback ao produtor pode ser retido parcialmente até o repasse final.

---

# Caso de Uso — Realizar Check-in de Ingresso

## Identificação

* **ID**: CU-02
* **Nome**: Realizar Check-in de Ingresso

## Descrição Geral

Permite que um operador de portaria (check-in) valide ingressos apresentados pelos clientes, através da leitura de um QR Code no aplicativo PWA de check-in, funcionando em modo online ou offline. A validação atualiza o status do ingresso e impede reutilização.

---

## Atores Envolvidos

* **Ator Principal**: Operador de Check-in (usuário com permissão CHECKIN)
* **Atores Secundários**:

  * Cliente (apresenta o ingresso)
  * Sistema de Ingressos / Carteira
  * Serviço de Check-in
  * Sistema de Sincronização

---

## Pré-condições

* Operador deve estar autenticado no app de check-in.
* Dispositivo deve estar sincronizado com a base de dados mais recente (em modo offline ou online).
* Cliente deve possuir ingresso válido e não utilizado.

## Pós-condições

* Ingresso é marcado como "utilizado" com data e hora do check-in.
* Evento é armazenado localmente (offline) ou enviado ao backend (online/sincronização).
* Histórico de validações é atualizado.

---

## Fluxo Principal (Online)

1. Cliente apresenta QR Code na portaria.
2. Operador abre o app de check-in e escaneia o QR.
3. Sistema valida assinatura digital do QR e verifica status do ingresso.
4. Se válido:

   * Marca o ingresso como utilizado
   * Armazena registro de check-in com timestamp, operador e local
5. Interface exibe mensagem "Check-in realizado com sucesso".
6. Cliente recebe confirmação visual e sonora.

---

## Fluxo Alternativo (Offline)

* Caso não haja internet:

  * Passos 1 e 2 ocorrem normalmente
  * Passo 3 usa base local para validação (dados sincronizados previamente)
  * Passo 4 registra o check-in em armazenamento local
  * Passo 5 exibe mensagem: "Check-in offline, será sincronizado"

---

## Exceções

| Código | Situação                              | Tratamento                                                                |
| ------ | ------------------------------------- | ------------------------------------------------------------------------- |
| EXC-01 | Ingresso já utilizado                 | Exibir mensagem "Ingresso já validado" com detalhes (data/hora anterior)  |
| EXC-02 | QR inválido ou adulterado             | Exibir "QR Code inválido ou não reconhecido"                              |
| EXC-03 | Dados locais desatualizados (offline) | Alerta: "Base desatualizada. Sincronize para garantir validação correta." |
| EXC-04 | Falha na sincronização                | Manter tentativa pendente e alertar operador                              |

---

## Requisitos Relacionados

| Tipo | Código | Descrição                                   |
| ---- | ------ | ------------------------------------------- |
| RF   | RF36   | Validar ingresso via QR Code                |
| RF   | RF37   | Operar modo offline                         |
| RF   | RF38   | Registro de histórico de check-ins          |
| RF   | RF39   | Sincronizar dados do app de check-in        |
| RNF  | RNF03  | Alta performance e resposta rápida          |
| RNF  | RNF04  | Segurança na validação (assinatura digital) |

---

## Regras de Negócio

* Um ingresso só pode ser validado **uma única vez**.
* O QR Code deve conter metadados e assinatura criptográfica para verificação de integridade.
* Operador pode realizar check-ins **sem internet**, mas deve sincronizar ao final do turno.
* Todos os registros devem ser auditáveis (data, hora, operador, localização).

---

## Observações Técnicas

* App de check-in é uma PWA, com suporte a cache local, IndexedDB e sincronização posterior.
* O sistema usa validação criptográfica com chave pública para autenticar os QR Codes.
* Estratégias de reconciliação são aplicadas na sincronização para evitar conflitos de estado (ex: mesmo ingresso validado duas vezes offline).


## Bibliografia

<a name="ref1"></a>**[1]** Creately. [*Tutorial do diagrama de caso de uso (guia com exemplos)*](https://creately.com/blog/pt/diagrama/tutorial-de-diagrama-de-caso-de-uso/). Acesso em: 05 mai. 2025.

<a name="ref2"></a>**[2]** DevMedia. [*O que é UML e Diagramas de Caso de Uso: Introdução Prática à UML*](https://www.devmedia.com.br/o-que-e-uml-e-diagramas-de-caso-de-uso-introducao-pratica-a-uml/23408). Acesso em: 05 mai. 2025.

<a name="ref3"></a>**[3]** IBM. [*Diagrama de caso de uso UML: O que é, como fazer e exemplos*](https://www.ibm.com/docs/pt-br/rsm/7.5.0?topic=diagrams-use-case). Acesso em: 04 mai. 2025.

<a name="ref4"></a>**[4]** IBM. [*Relacionamentos em Diagramas de Caso de Uso*](https://www.ibm.com/docs/pt-br/rsm/7.5.0?topic=diagrams-relationships-in-use-case). Acesso em: 04 mai. 2025.

<a name="ref5"></a>**[5]** Lucidchart. [*Diagrama de caso de uso UML: O que é, como fazer e exemplos*](https://www.lucidchart.com/pages/pt/diagrama-de-caso-de-uso-uml). Acesso em: 05 mai. 2025.

<a name="ref6"></a>**[6]** Lucid Software (YouTube). [*Tutorial de Caso de Uso UML - Lucid Software Português*](https://www.youtube.com/watch?v=ab6eDdwS3rA). Acesso em: 05 mai. 2025.

<a name="ref7"></a>**[7]** Microsoft. [*Criar um diagrama de caso de uso UML*](https://support.microsoft.com/pt-br/topic/criar-um-diagrama-de-caso-de-uso-uml-92cc948d-fc74-466c-9457-e82d62ee1298). Acesso em: 04 mai. 2025.

## Histórico de versão


| Versão | Alteração                                                                      | Responsável       | Data       |
| :----- | :----------------------------------------------------------------------------- | :---------------- | :--------- |
| 1.0    | Criação da estrutura inicial do documento                                      | Larissa Stéfane   | 04/05/2025 |
| 1.1    | Adição da seção de Metodologia                  | Larissa Stéfane   | 04/05/2025 |
| 1.2    | Adição da explicação         | Larissa Stéfane   | 04/05/2025 |
| 1.3    | Adição do Diagrama de Caso de Uso        | Larissa Stéfane   | 05/05/2025 |
| 1.4 | Ajustes no artefato| Larissa Stéfane | 06/05/2024 |
