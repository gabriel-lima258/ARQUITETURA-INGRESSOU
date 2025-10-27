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

---

# Caso de Uso — Cadastrar Usuário

## Identificação

* **ID**: CU-03
* **Nome**: Cadastrar Usuário

## Descrição Geral

Permite que um novo usuário se cadastre na plataforma Ingressou através de e-mail/senha ou login social (Google/Apple), com verificação por OTP/e-mail para garantir a autenticidade da conta.

## Atores Envolvidos

* **Ator Principal**: Usuário não cadastrado
* **Atores Secundários**:
  * Sistema de Autenticação
  * Provedores de Login Social (Google/Apple)
  * Sistema de Notificações (E-mail)
  * Sistema de Verificação OTP

## Pré-condições

* O usuário deve ter acesso à internet
* Deve possuir um e-mail válido ou conta social (Google/Apple)
* Não deve possuir conta já cadastrada com o mesmo e-mail

## Pós-condições

* Conta de usuário é criada no sistema
* E-mail de verificação é enviado (se cadastro por e-mail)
* Usuário recebe acesso limitado até verificação completa
* Dados são armazenados de forma segura conforme LGPD

## Fluxo Principal

1. Usuário acessa a página de cadastro
2. Escolhe método de cadastro (e-mail/senha ou login social)
3. **Se e-mail/senha:**
   - Preenche dados pessoais (nome, e-mail, senha, CPF)
   - Aceita termos de uso e política de privacidade
   - Sistema valida dados e cria conta pendente
   - Envia e-mail de verificação com OTP
4. **Se login social:**
   - Redireciona para provedor (Google/Apple)
   - Autoriza acesso aos dados básicos
   - Sistema cria conta automaticamente verificada
5. **Para cadastro por e-mail:**
   - Usuário acessa e-mail e insere código OTP
   - Sistema valida código e ativa conta
6. Usuário é redirecionado para página inicial autenticado

## Fluxos Alternativos

* **3a. E-mail já cadastrado:**
  - Sistema exibe mensagem: "E-mail já possui conta cadastrada"
  - Oferece opção de recuperação de senha
* **3b. Dados inválidos:**
  - Sistema exibe erros específicos para cada campo
  - Permite correção sem perder dados preenchidos
* **4a. Falha na autorização social:**
  - Usuário é redirecionado de volta com erro
  - Oferece opção de cadastro por e-mail como alternativa

## Exceções

| Código | Situação | Tratamento |
| --- | --- | --- |
| EXC-05 | Falha no envio de e-mail | Tentar reenvio; notificar usuário sobre possível atraso |
| EXC-06 | OTP expirado | Permitir solicitação de novo código |
| EXC-07 | CPF inválido | Exibir mensagem específica e solicitar correção |

## Requisitos Relacionados

| Tipo | Código | Descrição |
| ---- | ------ | --------- |
| RF | RF01 | Cadastro de Usuário |
| RF | RF02 | Login |
| RNF | RNF04 | Proteção de Dados |
| RNF | RNF13 | LGPD |

---

# Caso de Uso — Realizar Login

## Identificação

* **ID**: CU-04
* **Nome**: Realizar Login

## Descrição Geral

Permite que um usuário autentique-se na plataforma através de e-mail/senha ou login social (Google/Apple), com controle de rate-limit para prevenir ataques de força bruta.

## Atores Envolvidos

* **Ator Principal**: Usuário cadastrado
* **Atores Secundários**:
  * Sistema de Autenticação
  * Provedores de Login Social
  * Sistema de Rate Limiting
  * Sistema de Sessão JWT

## Pré-condições

* Usuário deve possuir conta cadastrada e verificada
* Deve ter acesso à internet
* Conta não deve estar bloqueada por tentativas excessivas

## Pós-condições

* Sessão JWT é criada (1h) com refresh token (7d)
* Usuário é autenticado e redirecionado
* Log de acesso é registrado para auditoria
* Rate-limit é aplicado para prevenir abuso

## Fluxo Principal

1. Usuário acessa página de login
2. Escolhe método de autenticação (e-mail/senha ou social)
3. **Se e-mail/senha:**
   - Insere credenciais
   - Sistema valida e verifica rate-limit
   - Gera JWT e refresh token
4. **Se login social:**
   - Redireciona para provedor
   - Autoriza acesso aos dados
   - Sistema valida e cria sessão
5. Usuário é redirecionado para página inicial autenticado
6. Sistema registra log de acesso

## Fluxos Alternativos

* **3a. Credenciais inválidas:**
  - Sistema incrementa contador de tentativas
  - Exibe mensagem genérica de erro
  - Após 5 tentativas, bloqueia temporariamente
* **3b. Conta bloqueada:**
  - Exibe tempo restante para desbloqueio
  - Oferece opção de recuperação de senha

## Exceções

| Código | Situação | Tratamento |
| --- | --- | --- |
| EXC-08 | Rate-limit excedido | Bloquear por 15 minutos; notificar usuário |
| EXC-09 | Falha na geração de JWT | Tentar novamente; logar erro crítico |
| EXC-10 | Refresh token inválido | Solicitar novo login |

## Requisitos Relacionados

| Tipo | Código | Descrição |
| ---- | ------ | --------- |
| RF | RF02 | Login |
| RF | RF03 | Sessão JWT |
| RNF | RNF05 | Sessões/JWT |

---

# Caso de Uso — Recuperar Senha

## Identificação

* **ID**: CU-05
* **Nome**: Recuperar Senha

## Descrição Geral

Permite que um usuário recupere o acesso à sua conta através de um link de redefinição enviado por e-mail, com expiração de 30 minutos para segurança.

## Atores Envolvidos

* **Ator Principal**: Usuário com conta cadastrada
* **Atores Secundários**:
  * Sistema de Autenticação
  * Sistema de Notificações (E-mail)
  * Sistema de Tokens Temporários

## Pré-condições

* Usuário deve possuir conta cadastrada
* Deve ter acesso ao e-mail cadastrado
* Não deve ter solicitado recuperação recentemente (cooldown)

## Pós-condições

* Link de recuperação é enviado por e-mail
* Token temporário é gerado (expira em 30 min)
* Log de solicitação é registrado
* Senha é alterada após confirmação

## Fluxo Principal

1. Usuário acessa página "Esqueci minha senha"
2. Insere e-mail cadastrado
3. Sistema valida e-mail e verifica cooldown
4. Gera token temporário único
5. Envia e-mail com link de redefinição
6. Usuário acessa link no e-mail
7. Insere nova senha (duas vezes para confirmação)
8. Sistema valida e atualiza senha
9. Invalida token temporário
10. Redireciona para login com mensagem de sucesso

## Fluxos Alternativos

* **3a. E-mail não encontrado:**
  - Sistema exibe mensagem genérica (por segurança)
  - Não revela se e-mail existe ou não
* **3b. Cooldown ativo:**
  - Informa tempo restante para nova tentativa
  - Sugere verificar spam/lixo eletrônico

## Exceções

| Código | Situação | Tratamento |
| --- | --- | --- |
| EXC-11 | Token expirado | Solicitar nova recuperação |
| EXC-12 | Link já utilizado | Exibir erro e solicitar nova recuperação |
| EXC-13 | Falha no envio de e-mail | Tentar reenvio; notificar possível atraso |

## Requisitos Relacionados

| Tipo | Código | Descrição |
| ---- | ------ | --------- |
| RF | RF04 | Recuperação de Senha |
| RNF | RNF04 | Proteção de Dados |

---

# Caso de Uso — Gerenciar Perfil

## Identificação

* **ID**: CU-06
* **Nome**: Gerenciar Perfil

## Descrição Geral

Permite que um usuário autenticado visualize e edite seus dados pessoais, exceto CPF, e gerencie provedores sociais vinculados à sua conta.

## Atores Envolvidos

* **Ator Principal**: Usuário autenticado
* **Atores Secundários**:
  * Sistema de Perfil
  * Provedores de Login Social
  * Sistema de Validação de Dados

## Pré-condições

* Usuário deve estar autenticado
* Deve ter sessão válida
* Dados devem estar atualizados

## Pós-condições

* Dados do perfil são atualizados
* Alterações são registradas em auditoria
* Provedores sociais são vinculados/desvinculados conforme solicitado

## Fluxo Principal

1. Usuário acessa página "Meu Perfil"
2. Visualiza dados atuais (nome, e-mail, telefone, endereço)
3. Clica em "Editar Perfil"
4. Modifica campos permitidos (exceto CPF)
5. **Se alterar e-mail:**
   - Sistema solicita confirmação por e-mail atual
   - Envia código de verificação para novo e-mail
   - Usuário confirma alteração
6. **Se gerenciar provedores sociais:**
   - Visualiza provedores vinculados
   - Pode vincular novos ou desvincular existentes
7. Confirma alterações
8. Sistema valida e salva dados
9. Exibe mensagem de sucesso

## Fluxos Alternativos

* **5a. Falha na confirmação de e-mail:**
  - Mantém e-mail original
  - Notifica sobre falha na alteração
* **6a. Tentativa de desvincular último provedor:**
  - Impede ação se não houver senha cadastrada
  - Solicita criação de senha primeiro

## Exceções

| Código | Situação | Tratamento |
| --- | --- | --- |
| EXC-14 | Dados inválidos | Exibir erros específicos por campo |
| EXC-15 | E-mail já em uso | Solicitar outro e-mail |
| EXC-16 | Falha na vinculação social | Tentar novamente; exibir erro específico |

## Requisitos Relacionados

| Tipo | Código | Descrição |
| ---- | ------ | --------- |
| RF | RF05 | Perfil |
| RNF | RNF04 | Proteção de Dados |
| RNF | RNF13 | LGPD |

---

# Caso de Uso — Buscar e Filtrar Eventos

## Identificação

* **ID**: CU-07
* **Nome**: Buscar e Filtrar Eventos

## Descrição Geral

Permite que usuários (autenticados ou não) descubram eventos através de busca global por palavras-chave e filtros por localização (cidade/UF), categoria e faixa de datas, com ordenação e URLs amigáveis para compartilhamento.

## Atores Envolvidos

* **Ator Principal**: Usuário (autenticado ou visitante)
* **Atores Secundários**:
  * Sistema de Busca
  * Sistema de Cache (Redis)
  * Sistema de Geolocalização
  * Sistema de URLs Amigáveis

## Pré-condições

* Deve haver eventos publicados no sistema
* Sistema de busca deve estar operacional
* Cache deve estar sincronizado

## Pós-condições

* Lista de eventos filtrados é exibida
* Parâmetros de busca são preservados na URL
* Cache é atualizado para próximas consultas
* Métricas de busca são registradas

## Fluxo Principal

1. Usuário acessa página inicial ou catálogo de eventos
2. **Busca por texto:**
   - Digita palavras-chave no campo de busca
   - Sistema busca em nome, local, artista e descrição
3. **Filtros por localização:**
   - Seleciona UF e cidade (autocompletar)
   - Sistema filtra eventos da região
4. **Filtros por categoria:**
   - Escolhe categoria(ies) desejada(s)
   - Sistema aplica filtro categórico
5. **Filtros por data:**
   - Seleciona faixa de datas ou período pré-definido
   - Sistema filtra eventos no período
6. **Ordenação:**
   - Escolhe critério (data, popularidade, preço)
   - Sistema ordena resultados
7. Exibe lista paginada de eventos
8. URL é atualizada com parâmetros para compartilhamento

## Fluxos Alternativos

* **2a. Busca sem resultados:**
  - Exibe mensagem "Nenhum evento encontrado"
  - Sugere filtros alternativos ou termos similares
* **3a. Localização não encontrada:**
  - Sugere cidades próximas
  - Oferece busca por UF apenas
* **4a. Múltiplas categorias:**
  - Permite seleção múltipla
  - Aplica filtro OR entre categorias

## Exceções

| Código | Situação | Tratamento |
| --- | --- | --- |
| EXC-17 | Sistema de busca indisponível | Exibir eventos em ordem cronológica |
| EXC-18 | Cache expirado | Buscar diretamente no banco |
| EXC-19 | Parâmetros inválidos na URL | Usar valores padrão |

## Requisitos Relacionados

| Tipo | Código | Descrição |
| ---- | ------ | --------- |
| RF | RF06 | Busca Global |
| RF | RF07 | Filtro por Localização |
| RF | RF08 | Filtro por Categoria |
| RF | RF09 | Filtro por Data |
| RF | RF10 | Ordenação |
| RF | RF11 | URLs Amigáveis |
| RNF | RNF15 | Cache |
| RNF | RNF16 | Busca e Filtros |

---

# Caso de Uso — Visualizar Detalhes do Evento

## Identificação

* **ID**: CU-08
* **Nome**: Visualizar Detalhes do Evento

## Descrição Geral

Permite que usuários visualizem informações detalhadas de um evento específico, incluindo dados principais, categorias, localização, datas, lotes disponíveis e opção de compra.

## Atores Envolvidos

* **Ator Principal**: Usuário (autenticado ou visitante)
* **Atores Secundários**:
  * Sistema de Eventos
  * Sistema de Cache
  * Sistema de Geolocalização

## Pré-condições

* Evento deve estar publicado
* Deve ter pelo menos um lote válido
* Sistema deve estar operacional

## Pós-condições

* Página do evento é exibida
* Dados são carregados do cache quando possível
* Métricas de visualização são registradas

## Fluxo Principal

1. Usuário clica em evento da listagem ou acessa URL direta
2. Sistema carrega dados do evento (nome, descrição, banner)
3. Exibe informações de localização (endereço, cidade, UF)
4. Mostra datas e horários (início/fim)
5. Lista categorias atribuídas
6. **Se evento ativo:**
   - Exibe lotes disponíveis com preços
   - Mostra quantidade restante
   - Exibe botão "Comprar Ingressos"
7. **Se evento encerrado:**
   - Exibe mensagem "Evento encerrado"
   - Mostra dados históricos
8. Sistema registra visualização para métricas

## Fluxos Alternativos

* **6a. Lotes esgotados:**
  - Exibe "Ingressos esgotados"
  - Oferece lista de espera (se configurado)
* **6b. Evento cancelado:**
  - Exibe aviso de cancelamento
  - Informa sobre reembolsos

## Exceções

| Código | Situação | Tratamento |
| --- | --- | --- |
| EXC-20 | Evento não encontrado | Redirecionar para página 404 |
| EXC-21 | Evento não publicado | Exibir erro de acesso |
| EXC-22 | Falha no carregamento | Tentar recarregar dados |

## Requisitos Relacionados

| Tipo | Código | Descrição |
| ---- | ------ | --------- |
| RF | RF18 | Página Pública do Evento |
| RNF | RNF15 | Cache |

---

# Caso de Uso — Cadastrar Produtor (Admin)

## Identificação

* **ID**: CU-09
* **Nome**: Cadastrar Produtor (Admin)

## Descrição Geral

Permite que um administrador cadastre um novo produtor no sistema, realizando onboarding com KYC básico, validação de dados bancários/PIX e habilitação de acesso ao painel de leitura.

## Atores Envolvidos

* **Ator Principal**: Administrador
* **Atores Secundários**:
  * Sistema de Validação (CNPJ/CPF)
  * Sistema de KYC
  * Sistema de Pagamentos (PIX)
  * Sistema de Notificações

## Pré-condições

* Administrador deve estar autenticado
* Deve ter permissões de administração
* Sistema de validação deve estar operacional

## Pós-condições

* Produtor é cadastrado no sistema
* Dados são validados e verificados
* Acesso ao painel é habilitado
* Notificações são enviadas

## Fluxo Principal

1. Administrador acessa painel administrativo
2. Navega para seção "Gerenciar Produtores"
3. Clica em "Cadastrar Novo Produtor"
4. Preenche dados básicos (nome, e-mail, telefone)
5. **Se pessoa jurídica:**
   - Insere CNPJ e razão social
   - Sistema valida CNPJ na Receita Federal
6. **Se pessoa física:**
   - Insere CPF e nome completo
   - Sistema valida CPF
7. Insere dados bancários (chave PIX, conta)
8. Anexa documentos (contrato, termos)
9. Sistema realiza validações automáticas
10. **Se validações OK:**
    - Cria conta do produtor
    - Envia credenciais por e-mail
    - Habilita acesso ao painel
11. **Se validações falham:**
    - Exibe erros específicos
    - Permite correção dos dados

## Fluxos Alternativos

* **5a. CNPJ inválido:**
  - Exibe erro específico
  - Sugere verificação manual
* **6a. CPF inválido:**
  - Exibe erro específico
  - Permite nova tentativa
* **9a. Validação bancária falha:**
  - Solicita dados bancários alternativos
  - Oferece validação manual

## Exceções

| Código | Situação | Tratamento |
| --- | --- | --- |
| EXC-23 | Falha na API de validação | Permitir cadastro manual com flag de pendência |
| EXC-24 | E-mail já cadastrado | Exibir erro e sugerir recuperação |
| EXC-25 | Falha no envio de credenciais | Tentar reenvio; notificar admin |

## Requisitos Relacionados

| Tipo | Código | Descrição |
| ---- | ------ | --------- |
| RF | RF12 | Onboarding de Produtor (Admin) |
| RF | RF13 | Verificação/KYC |
| RNF | RNF04 | Proteção de Dados |

---

# Caso de Uso — Acessar Painel do Produtor

## Identificação

* **ID**: CU-10
* **Nome**: Acessar Painel do Produtor

## Descrição Geral

Permite que um produtor autenticado acesse seu painel de controle para visualizar métricas de vendas, check-ins, repasses e cashback apenas dos eventos vinculados a ele, com opção de exportar dados em CSV.

## Atores Envolvidos

* **Ator Principal**: Produtor autenticado
* **Atores Secundários**:
  * Sistema de Relatórios
  * Sistema de Cache
  * Sistema de Exportação (CSV)
  * Sistema de Eventos Vinculados

## Pré-condições

* Produtor deve estar autenticado
* Deve ter eventos vinculados
* Sistema de relatórios deve estar operacional

## Pós-condições

* Painel é exibido com dados atualizados
* Métricas são carregadas do cache quando possível
* Dados são atualizados em tempo real

## Fluxo Principal

1. Produtor faz login no sistema
2. Acessa painel através do menu "Meu Painel"
3. Sistema carrega eventos vinculados ao produtor
4. **Se há eventos vinculados:**
   - Exibe dashboard com métricas principais
   - Mostra vendas por evento (quantidade, valor)
   - Exibe check-ins realizados
   - Mostra saldo de cashback acumulado
   - Lista repasses programados/recebidos
5. **Se não há eventos vinculados:**
   - Exibe mensagem "Nenhum evento vinculado"
   - Oferece contato com administrador
6. Produtor pode filtrar por período
7. **Para exportar dados:**
   - Seleciona período e eventos
   - Clica em "Exportar CSV"
   - Sistema gera arquivo e disponibiliza download

## Fluxos Alternativos

* **4a. Dados em cache:**
  - Carrega dados rapidamente do cache
  - Atualiza em background se necessário
* **7a. Exportação de grande volume:**
  - Processa em background
  - Envia e-mail quando pronto

## Exceções

| Código | Situação | Tratamento |
| --- | --- | --- |
| EXC-26 | Falha no carregamento de dados | Exibir dados em cache; tentar atualizar |
| EXC-27 | Erro na exportação | Tentar novamente; notificar suporte |
| EXC-28 | Cache desatualizado | Forçar atualização dos dados |

## Requisitos Relacionados

| Tipo | Código | Descrição |
| ---- | ------ | --------- |
| RF | RF14 | Painel do Produtor — somente leitura |
| RNF | RNF15 | Cache |

---

# Caso de Uso — Criar Evento (Admin)

## Identificação

* **ID**: CU-11
* **Nome**: Criar Evento (Admin)

## Descrição Geral

Permite que um administrador crie um novo evento no sistema com todas as informações necessárias, incluindo dados básicos, localização, categorias e status inicial como rascunho.

## Atores Envolvidos

* **Ator Principal**: Administrador
* **Atores Secundários**:
  * Sistema de Eventos
  * Sistema de Categorias
  * Sistema de Geolocalização
  * Sistema de Upload de Arquivos

## Pré-condições

* Administrador deve estar autenticado
* Deve ter permissões de administração
* Sistema deve estar operacional

## Pós-condições

* Evento é criado com status "rascunho"
* Dados são validados e armazenados
* Cache é invalidado para atualizações
* Log de auditoria é registrado

## Fluxo Principal

1. Administrador acessa painel administrativo
2. Navega para "Gerenciar Eventos"
3. Clica em "Criar Novo Evento"
4. Preenche dados básicos (nome, descrição)
5. Faz upload do banner/imagem do evento
6. Insere informações de localização (endereço, cidade, UF)
7. Define datas de início e fim do evento
8. Seleciona categoria(ies) obrigatória(s)
9. Define status inicial como "rascunho"
10. Sistema valida todos os dados
11. **Se validação OK:**
    - Salva evento no banco
    - Invalida cache relacionado
    - Registra log de auditoria
12. **Se validação falha:**
    - Exibe erros específicos
    - Permite correção dos dados

## Fluxos Alternativos

* **6a. Endereço não encontrado:**
  - Sugere endereços similares
  - Permite inserção manual
* **8a. Categoria não existe:**
  - Oferece criação de nova categoria
  - Redireciona para gestão de categorias

## Exceções

| Código | Situação | Tratamento |
| --- | --- | --- |
| EXC-29 | Falha no upload de imagem | Tentar novamente; permitir evento sem imagem |
| EXC-30 | Data inválida | Exibir erro específico; sugerir datas válidas |
| EXC-31 | Falha na validação de localização | Permitir criação com validação manual posterior |

## Requisitos Relacionados

| Tipo | Código | Descrição |
| ---- | ------ | --------- |
| RF | RF15 | Criação de Evento (Admin) |
| RF | RF20 | Gerenciar Categorias (Admin) |
| RNF | RNF15 | Cache |

---

# Caso de Uso — Publicar Evento (Admin)

## Identificação

* **ID**: CU-12
* **Nome**: Publicar Evento (Admin)

## Descrição Geral

Permite que um administrador publique um evento que estava em rascunho, desde que tenha pelo menos um lote válido e categoria atribuída, tornando-o visível para o público.

## Atores Envolvidos

* **Ator Principal**: Administrador
* **Atores Secundários**:
  * Sistema de Eventos
  * Sistema de Lotes
  * Sistema de Cache
  * Sistema de Notificações

## Pré-condições

* Evento deve estar em status "rascunho"
* Deve ter pelo menos um lote válido
* Deve ter categoria atribuída
* Administrador deve ter permissões

## Pós-condições

* Evento é publicado e visível publicamente
* Cache é atualizado
* Notificações são enviadas
* Log de auditoria é registrado

## Fluxo Principal

1. Administrador acessa lista de eventos em rascunho
2. Seleciona evento para publicar
3. Sistema verifica pré-condições:
   - Pelo menos 1 lote válido
   - Categoria atribuída
   - Dados obrigatórios preenchidos
4. **Se pré-condições atendidas:**
   - Altera status para "publicado"
   - Atualiza data de publicação
   - Invalida cache de eventos
   - Envia notificações para produtores vinculados
5. **Se pré-condições não atendidas:**
   - Exibe lista de pendências
   - Impede publicação até correção

## Fluxos Alternativos

* **3a. Lotes inválidos:**
  - Lista lotes com problemas
  - Oferece correção direta
* **3b. Sem categoria:**
  - Redireciona para seleção de categoria
  - Permite atribuição rápida

## Exceções

| Código | Situação | Tratamento |
| --- | --- | --- |
| EXC-32 | Falha na atualização do cache | Tentar novamente; notificar admin |
| EXC-33 | Erro nas notificações | Continuar publicação; tentar notificar depois |

## Requisitos Relacionados

| Tipo | Código | Descrição |
| ---- | ------ | --------- |
| RF | RF17 | Publicação (Admin) |
| RNF | RNF15 | Cache |

---

# Caso de Uso — Vincular Produtor a Evento (Admin)

## Identificação

* **ID**: CU-13
* **Nome**: Vincular Produtor a Evento (Admin)

## Descrição Geral

Permite que um administrador vincule um ou mais produtores a um evento específico, concedendo acesso de leitura ao painel do produtor para acompanhar vendas e métricas.

## Atores Envolvidos

* **Ator Principal**: Administrador
* **Atores Secundários**:
  * Sistema de Eventos
  * Sistema de Produtores
  * Sistema de Permissões
  * Sistema de Notificações

## Pré-condições

* Administrador deve estar autenticado
* Evento deve existir
* Produtor(es) devem estar cadastrados
* Sistema deve estar operacional

## Pós-condições

* Vinculação é criada no sistema
* Produtor recebe acesso ao evento
* Notificação é enviada ao produtor
* Log de auditoria é registrado

## Fluxo Principal

1. Administrador acessa detalhes do evento
2. Navega para seção "Produtores Vinculados"
3. Clica em "Vincular Produtor"
4. Busca produtor por nome/e-mail
5. Seleciona produtor da lista
6. **Se produtor não vinculado:**
   - Confirma vinculação
   - Sistema cria relação evento-produtor
   - Envia notificação ao produtor
   - Atualiza permissões de acesso
7. **Se produtor já vinculado:**
   - Exibe mensagem de erro
   - Oferece opção de desvincular

## Fluxos Alternativos

* **4a. Produtor não encontrado:**
  - Oferece cadastro de novo produtor
  - Redireciona para cadastro
* **6a. Múltiplos produtores:**
  - Permite seleção múltipla
  - Vincula todos de uma vez

## Exceções

| Código | Situação | Tratamento |
| --- | --- | --- |
| EXC-34 | Falha na criação da vinculação | Tentar novamente; notificar admin |
| EXC-35 | Erro nas notificações | Continuar vinculação; tentar notificar depois |

## Requisitos Relacionados

| Tipo | Código | Descrição |
| ---- | ------ | --------- |
| RF | RF19 | Vincular Produtor↔Evento |
| RNF | RNF04 | Proteção de Dados |

---

# Caso de Uso — Transferir Ingresso

## Identificação

* **ID**: CU-14
* **Nome**: Transferir Ingresso

## Descrição Geral

Permite que um usuário autenticado transfira um ingresso não utilizado para outro usuário através de e-mail/CPF, com aceite do destinatário, reemissão de QR Code e cobrança de taxa de transferência.

## Atores Envolvidos

* **Ator Principal**: Usuário autenticado (remetente)
* **Atores Secundários**:
  * Destinatário (usuário)
  * Sistema de Transferências
  * Sistema de Pagamentos
  * Sistema de QR Code
  * Sistema de Notificações

## Pré-condições

* Remetente deve estar autenticado
* Ingresso deve estar não utilizado
* Evento deve permitir transferências
* Deve estar dentro da janela de tempo permitida

## Pós-condições

* Solicitação de transferência é criada
* Destinatário é notificado
* QR original é invalidado após aceite
* Novo QR é emitido para destinatário
* Taxa é cobrada e transferência é concluída

## Fluxo Principal

1. Usuário acessa "Meus Ingressos"
2. Seleciona ingresso para transferir
3. Sistema verifica elegibilidade:
   - Ingresso não utilizado
   - Evento permite transferência
   - Dentro da janela de tempo
4. **Se elegível:**
   - Insere e-mail/CPF do destinatário
   - Sistema calcula taxa de transferência (10%)
   - Exibe resumo da transferência
5. Confirma transferência e escolhe método de pagamento
6. **Se pagamento aprovado:**
   - Cria solicitação pendente
   - Envia convite ao destinatário
   - Invalida QR original
7. **Destinatário aceita:**
   - Transfere ingresso para sua carteira
   - Gera novo QR Code assinado
   - Envia notificações de conclusão

## Fluxos Alternativos

* **3a. Ingresso não elegível:**
  - Exibe motivo específico
  - Impede transferência
* **6a. Destinatário recusa:**
  - Cancela transferência
  - Retorna ingresso ao remetente
  - Reembolsa taxa
* **6b. Transferência expira:**
  - Cancela automaticamente
  - Retorna ingresso ao remetente

## Exceções

| Código | Situação | Tratamento |
| --- | --- | --- |
| EXC-36 | Falha no pagamento da taxa | Cancelar transferência; notificar usuário |
| EXC-37 | Erro na geração do novo QR | Tentar novamente; notificar suporte |
| EXC-38 | Destinatário não encontrado | Sugerir criação de conta |

## Requisitos Relacionados

| Tipo | Código | Descrição |
| ---- | ------ | --------- |
| RF | RF40 | Iniciar Transferência (Remetente) |
| RF | RF41 | Aceite do Destinatário |
| RF | RF42 | Reemissão de Ingresso |
| RF | RF45 | Taxa de Transferência |
| RNF | RNF17 | Segurança de Transferência |

---

# Caso de Uso — Criar Lote (Admin)

## Identificação

* **ID**: CU-15
* **Nome**: Criar Lote (Admin)

## Descrição Geral

Permite que um administrador crie lotes de ingressos para um evento específico, definindo preço, quantidade, janela de venda e tipos de ingressos, com encerramento automático por tempo ou quantidade.

## Atores Envolvidos

* **Ator Principal**: Administrador
* **Atores Secundários**:
  * Sistema de Lotes
  * Sistema de Eventos
  * Sistema de Validação

## Pré-condições

* Administrador deve estar autenticado
* Evento deve existir
* Sistema deve estar operacional

## Pós-condições

* Lote é criado e vinculado ao evento
* Validações são aplicadas
* Cache é invalidado
* Log de auditoria é registrado

## Fluxo Principal

1. Administrador acessa detalhes do evento
2. Navega para seção "Lotes"
3. Clica em "Criar Novo Lote"
4. Preenche dados do lote:
   - Nome do lote
   - Preço unitário
   - Quantidade total
   - Data/hora início da venda
   - Data/hora fim da venda
5. Define tipos de ingressos (inteira, meia, VIP, cortesia)
6. Sistema valida dados:
   - Janela de venda dentro do período do evento
   - Preços válidos
   - Quantidades positivas
7. **Se validação OK:**
   - Salva lote no banco
   - Invalida cache relacionado
   - Registra log de auditoria

## Fluxos Alternativos

* **6a. Validação falha:**
  - Exibe erros específicos
  - Permite correção dos dados
* **6b. Conflito de datas:**
  - Sugere ajustes na janela de venda
  - Oferece datas alternativas

## Exceções

| Código | Situação | Tratamento |
| --- | --- | --- |
| EXC-39 | Falha na validação de datas | Exibir erro específico; sugerir correção |
| EXC-40 | Erro ao salvar lote | Tentar novamente; notificar admin |

## Requisitos Relacionados

| Tipo | Código | Descrição |
| ---- | ------ | --------- |
| RF | RF21 | Criação de Lotes (Admin) |
| RF | RF22 | Encerramento por Limite |
| RF | RF23 | Tipos de Ingressos |

---

# Caso de Uso — Aplicar Cupom de Influenciador

## Identificação

* **ID**: CU-16
* **Nome**: Aplicar Cupom de Influenciador

## Descrição Geral

Permite que um usuário aplique um cupom de influenciador durante o checkout, obtendo desconto percentual ou fixo, com validação de vigência, limites de uso e registro de atribuição ao influenciador.

## Atores Envolvidos

* **Ator Principal**: Usuário autenticado
* **Atores Secundários**:
  * Sistema de Cupons
  * Sistema de Influenciadores
  * Sistema de Checkout
  * Sistema de Validação

## Pré-condições

* Usuário deve estar autenticado
* Deve estar no processo de checkout
* Cupom deve estar ativo e válido

## Pós-condições

* Desconto é aplicado ao pedido
* Cupom é registrado como utilizado
* Atribuição ao influenciador é registrada
* Valor final é recalculado

## Fluxo Principal

1. Usuário está no checkout do pedido
2. Insere código do cupom no campo apropriado
3. Sistema valida cupom:
   - Código existe e está ativo
   - Dentro da vigência
   - Limite de uso não excedido
   - Aplicável ao evento/lote
4. **Se cupom válido:**
   - Calcula desconto (percentual ou fixo)
   - Aplica ao valor total
   - Registra uso do cupom
   - Registra atribuição ao influenciador
   - Exibe desconto aplicado
5. **Se cupom inválido:**
   - Exibe mensagem de erro específica
   - Permite nova tentativa

## Fluxos Alternativos

* **3a. Cupom expirado:**
  - Exibe "Cupom expirado"
  - Sugere cupons similares ativos
* **3b. Limite excedido:**
  - Exibe "Limite de uso excedido"
  - Informa quando foi usado pela última vez

## Exceções

| Código | Situação | Tratamento |
| --- | --- | --- |
| EXC-41 | Falha na validação do cupom | Tentar novamente; notificar suporte |
| EXC-42 | Erro no registro de atribuição | Continuar checkout; registrar depois |

## Requisitos Relacionados

| Tipo | Código | Descrição |
| ---- | ------ | --------- |
| RF | RF31 | Cupom de Influenciador |
| RB | RB12 | Cupom de Influenciador |

---

# Caso de Uso — Gerenciar Painel Administrativo

## Identificação

* **ID**: CU-17
* **Nome**: Gerenciar Painel Administrativo

## Descrição Geral

Permite que um administrador acesse o painel administrativo completo para gerenciar usuários, produtores, eventos, vendas, cupons, cashback, transferências e configurar parâmetros globais do sistema.

## Atores Envolvidos

* **Ator Principal**: Administrador
* **Atores Secundários**:
  * Sistema de Relatórios
  * Sistema de Auditoria
  * Sistema de Configurações
  * Sistema de Cache

## Pré-condições

* Administrador deve estar autenticado
* Deve ter permissões administrativas completas
* Sistema deve estar operacional

## Pós-condições

* Painel é exibido com dados atualizados
* Ações administrativas são executadas
* Logs de auditoria são registrados
* Configurações são aplicadas

## Fluxo Principal

1. Administrador faz login no sistema
2. Acessa painel administrativo
3. **Dashboard principal:**
   - Visualiza métricas gerais (usuários, eventos, vendas)
   - Acessa relatórios de cashback e transferências
   - Monitora status do sistema
4. **Gestão de usuários:**
   - Lista usuários cadastrados
   - Pode bloquear/desbloquear contas
   - Visualiza histórico de atividades
5. **Gestão de produtores:**
   - Lista produtores cadastrados
   - Gerencia vinculações com eventos
   - Monitora cashback acumulado
6. **Gestão de eventos:**
   - Lista todos os eventos
   - Gerencia publicação e lotes
   - Monitora vendas e check-ins
7. **Configurações globais:**
   - Ajusta taxas e políticas
   - Configura regras de cashback
   - Define políticas de transferência

## Fluxos Alternativos

* **3a. Dados em cache:**
  - Carrega rapidamente do cache
  - Atualiza em background
* **4a. Usuário suspeito:**
  - Oferece opções de bloqueio
  - Registra motivo da ação

## Exceções

| Código | Situação | Tratamento |
| --- | --- | --- |
| EXC-43 | Falha no carregamento de dados | Exibir dados em cache; tentar atualizar |
| EXC-44 | Erro nas configurações | Reverter para valores anteriores |

## Requisitos Relacionados

| Tipo | Código | Descrição |
| ---- | ------ | --------- |
| RF | RF48 | Painel Admin |
| RF | RF49 | Auditoria |
| RF | RF51 | Parâmetros Globais |
| RNF | RNF15 | Cache |

---

# Caso de Uso — Reenviar Ingresso

## Identificação

* **ID**: CU-18
* **Nome**: Reenviar Ingresso

## Descrição Geral

Permite que um usuário autenticado reenvie um ingresso por e-mail, útil quando o e-mail original não foi recebido ou foi perdido, mantendo a segurança do QR Code.

## Atores Envolvidos

* **Ator Principal**: Usuário autenticado
* **Atores Secundários**:
  * Sistema de Ingressos
  * Sistema de Notificações (E-mail)
  * Sistema de QR Code

## Pré-condições

* Usuário deve estar autenticado
* Deve possuir ingresso válido
* E-mail deve estar cadastrado

## Pós-condições

* Ingresso é reenviado por e-mail
* QR Code é mantido inalterado
* Log de reenvio é registrado

## Fluxo Principal

1. Usuário acessa "Meus Ingressos"
2. Localiza ingresso desejado
3. Clica em "Reenviar por E-mail"
4. Sistema verifica:
   - Ingresso pertence ao usuário
   - E-mail está cadastrado
   - Ingresso ainda é válido
5. **Se verificação OK:**
   - Gera e-mail com ingresso
   - Inclui QR Code original
   - Envia para e-mail cadastrado
   - Registra log de reenvio
6. Exibe confirmação de envio

## Fluxos Alternativos

* **4a. E-mail não cadastrado:**
  - Solicita cadastro de e-mail
  - Redireciona para perfil
* **4b. Ingresso expirado:**
  - Exibe mensagem de erro
  - Oferece contato com suporte

## Exceções

| Código | Situação | Tratamento |
| --- | --- | --- |
| EXC-45 | Falha no envio de e-mail | Tentar novamente; notificar usuário |
| EXC-46 | QR Code corrompido | Gerar novo QR; notificar usuário |

## Requisitos Relacionados

| Tipo | Código | Descrição |
| ---- | ------ | --------- |
| RF | RF34 | Reenvio |
| RF | RF35 | Notificações |

---

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
| 1.5 | Expansão significativa dos casos de uso cobrindo todos os requisitos funcionais principais (RF01-RF52) | Assistente IA | 16/01/2025 |
