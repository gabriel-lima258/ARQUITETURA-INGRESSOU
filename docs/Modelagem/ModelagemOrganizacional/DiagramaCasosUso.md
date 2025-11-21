# Diagrama de Casos de Uso — Ingressou

> **Versão:** 2.0  
> **Data:** 21 de Novembro de 2025  
> **Autor:** Gabriel Lima  
> **Projeto:** Ingressou — Plataforma Web de Venda e Gestão de Ingressos  

---

## Sumário

- [Introdução](#introdução)
- [Objetivos](#objetivos)
- [Metodologia](#metodologia)
- [Atores do Sistema](#atores-do-sistema)
- [Checklist de Casos de Uso](#checklist-de-casos-de-uso)
- [Grupo A — Conta e Autenticação](#grupo-a--conta-e-autenticação)
- [Grupo B — Eventos, Lotes e Produtos](#grupo-b--eventos-lotes-e-produtos)
- [Grupo C — Catálogo e Descoberta](#grupo-c--catálogo-e-descoberta)
- [Grupo D — Pedidos, Pagamentos e Cupons](#grupo-d--pedidos-pagamentos-e-cupons)
- [Grupo E — Tickets, Transferência e Check-in](#grupo-e--tickets-transferência-e-check-in)
- [Grupo F — Cashback e Relatórios](#grupo-f--cashback-e-relatórios)
- [Grupo G — Administração](#grupo-g--administração)
- [Conclusão](#conclusão)
- [Bibliografia](#bibliografia)
- [Histórico de versão](#histórico-de-versão)

---

## Introdução

O Diagrama de Casos de Uso é um dos diagramas comportamentais da UML (Unified Modeling Language), fundamental para capturar os requisitos funcionais de um sistema sob a perspectiva do usuário. Conforme descrito por [Diagrama de caso de uso UML: O que é, como fazer e exemplos](https://www.lucidchart.com/pages/pt/diagrama-de-caso-de-uso-uml) e [O que é UML e Diagramas de Caso de Uso: Introdução Prática à UML](https://www.devmedia.com.br/o-que-e-uml-e-diagramas-de-caso-de-uso-introducao-pratica-a-uml/23408), ele identifica quem interage com o sistema (Atores) e o que esses atores podem fazer (Casos de Uso) ao definir o escopo e as funcionalidades principais da aplicação de forma visual e intuitiva.

Este documento apresenta **27 casos de uso** organizados em **7 grupos funcionais**, cobrindo todo o ciclo de vida da plataforma Ingressou, desde autenticação até gestão administrativa, incluindo funcionalidades de eventos, pedidos, pagamentos, transferências, check-in e cashback.

---

## Objetivos

Os principais objetivos deste artefato são:

- Representar de forma estruturada todos os casos de uso do sistema **Ingressou (MVP)**.
- Mapear as interações entre os atores e o sistema para cada funcionalidade.
- Facilitar a comunicação entre desenvolvedores, analistas e stakeholders.
- Servir como **documentação base** para o desenvolvimento e testes do sistema.
- Garantir rastreabilidade completa aos requisitos funcionais (RF01-RF65) e regras de negócio.

---

## Metodologia

1. O documento foi elaborado com base na **versão 1.6 dos Requisitos Elicitados do Ingressou (Novembro de 2025)**, que incorpora todos os requisitos funcionais, não funcionais e regras de negócio do MVP.
2. Os casos de uso foram identificados através de **análise criteriosa dos requisitos funcionais** (RF01 a RF65), mapeando:
   - Cadastro e autenticação de usuários com RBAC
   - Onboarding e vinculação de produtores a eventos
   - Criação e gestão de eventos com categorização e localização
   - Busca e filtros nacionais (cidade/UF/categoria/data)
   - Gestão de lotes com encerramento por tempo ou quantidade
   - Compra de ingressos e produtos com pagamentos PIX/Cartão e aplicação de cupons
   - Transferência de ingressos com aceite e reemissão de QR Code
   - Validação de check-in (online/offline) com detecção de fraude
   - Sistema de notificações assíncronas
   - Cashback e relatórios para produtores
   - Gestão administrativa completa
3. A modelagem seguiu as normas da **UML 2.0**, priorizando:
   - **Clareza**: cada caso de uso tem objetivo bem definido
   - **Completude**: fluxos principais, alternativos e exceções detalhados
   - **Rastreabilidade**: todos os casos de uso são justificados por requisitos específicos

---

## Atores do Sistema

| Ator | Descrição | Papel no Sistema |
|------|-----------|------------------|
| **Visitante** | Usuário não autenticado que navega pelos eventos | Pode visualizar eventos, buscar e filtrar, mas não pode comprar |
| **Cliente** | Usuário autenticado que compra ingressos e produtos | Realiza compras, gerencia perfil, transfere ingressos |
| **Produtor** | Usuário com perfil de produtor, cria e gerencia eventos | Cria eventos, gerencia lotes e produtos, visualiza relatórios e cashback |
| **Operador de Check-in** | Usuário que valida tickets na entrada do evento | Valida ingressos via QR Code (online/offline) |
| **Administrador** | Usuário de backoffice, gerencia usuários, eventos, cupons, etc. | Gerencia todo o sistema, cadastra produtores, vincula eventos, configura parâmetros |
| **Gateway de Pagamento** | Sistema externo (PIX, cartão) que processa pagamentos | Processa transações financeiras e envia webhooks de confirmação |
| **Sistema de Notificação** | Serviço de envio de e-mail/push (interno/externo) | Envia notificações assíncronas para usuários |

---

## Checklist de Casos de Uso

| ID | Nome do Caso de Uso | Grupo | Status | Link |
|----|---------------------|-------|--------|------|
| UC01 | [Registrar usuário](#uc01--registrar-usuário) | A | ☐ | [Ir para UC01](#uc01--registrar-usuário) |
| UC02 | [Autenticar usuário (login/logout)](#uc02--autenticar-usuário-loginlogout) | A | ☐ | [Ir para UC02](#uc02--autenticar-usuário-loginlogout) |
| UC03 | [Gerenciar perfil do usuário](#uc03--gerenciar-perfil-do-usuário) | A | ☐ | [Ir para UC03](#uc03--gerenciar-perfil-do-usuário) |
| UC04 | [Cadastrar produtor (Admin)](#uc04--cadastrar-produtor-admin) | A | ☐ | [Ir para UC04](#uc04--cadastrar-produtor-admin) |
| UC05 | [Criar evento](#uc05--criar-evento) | B | ☐ | [Ir para UC05](#uc05--criar-evento) |
| UC06 | [Configurar localização, categorias e imagem do evento](#uc06--configurar-localização-categorias-e-imagem-do-evento) | B | ☐ | [Ir para UC06](#uc06--configurar-localização-categorias-e-imagem-do-evento) |
| UC07 | [Gerenciar lotes de ingressos do evento](#uc07--gerenciar-lotes-de-ingressos-do-evento) | B | ☐ | [Ir para UC07](#uc07--gerenciar-lotes-de-ingressos-do-evento) |
| UC08 | [Gerenciar produtos extras do evento](#uc08--gerenciar-produtos-extras-do-evento) | B | ☐ | [Ir para UC08](#uc08--gerenciar-produtos-extras-do-evento) |
| UC09 | [Publicar / despublicar evento](#uc09--publicar--despublicar-evento) | B | ☐ | [Ir para UC09](#uc09--publicar--despublicar-evento) |
| UC10 | [Listar e filtrar eventos](#uc10--listar-e-filtrar-eventos) | C | ☐ | [Ir para UC10](#uc10--listar-e-filtrar-eventos) |
| UC11 | [Visualizar detalhes do evento, lotes e produtos](#uc11--visualizar-detalhes-do-evento-lotes-e-produtos) | C | ☐ | [Ir para UC11](#uc11--visualizar-detalhes-do-evento-lotes-e-produtos) |
| UC12 | [Criar pedido com ingressos e produtos](#uc12--criar-pedido-com-ingressos-e-produtos) | D | ☐ | [Ir para UC12](#uc12--criar-pedido-com-ingressos-e-produtos) |
| UC13 | [Aplicar cupom de desconto](#uc13--aplicar-cupom-de-desconto) | D | ☐ | [Ir para UC13](#uc13--aplicar-cupom-de-desconto) |
| UC14 | [Realizar pagamento (PIX ou cartão)](#uc14--realizar-pagamento-pix-ou-cartão) | D | ☐ | [Ir para UC14](#uc14--realizar-pagamento-pix-ou-cartão) |
| UC15 | [Processar confirmação de pagamento (webhook)](#uc15--processar-confirmação-de-pagamento-webhook) | D | ☐ | [Ir para UC15](#uc15--processar-confirmação-de-pagamento-webhook) |
| UC16 | [Cancelar pedido / lidar com expiração](#uc16--cancelar-pedido--lidar-com-expiração) | D | ☐ | [Ir para UC16](#uc16--cancelar-pedido--lidar-com-expiração) |
| UC17 | [Emitir tickets após pagamento aprovado](#uc17--emitir-tickets-após-pagamento-aprovado) | E | ☐ | [Ir para UC17](#uc17--emitir-tickets-após-pagamento-aprovado) |
| UC18 | [Listar tickets do usuário](#uc18--listar-tickets-do-usuário) | E | ☐ | [Ir para UC18](#uc18--listar-tickets-do-usuário) |
| UC19 | [Transferir ticket para outro usuário](#uc19--transferir-ticket-para-outro-usuário) | E | ☐ | [Ir para UC19](#uc19--transferir-ticket-para-outro-usuário) |
| UC20 | [Aceitar ou recusar transferência de ticket](#uc20--aceitar-ou-recusar-transferência-de-ticket) | E | ☐ | [Ir para UC20](#uc20--aceitar-ou-recusar-transferência-de-ticket) |
| UC21 | [Realizar check-in de ticket (validação QRCode)](#uc21--realizar-check-in-de-ticket-validação-qrcode) | E | ☐ | [Ir para UC21](#uc21--realizar-check-in-de-ticket-validação-qrcode) |
| UC22 | [Gerar cashback para produtor em vendas](#uc22--gerar-cashback-para-produtor-em-vendas) | F | ☐ | [Ir para UC22](#uc22--gerar-cashback-para-produtor-em-vendas) |
| UC23 | [Consultar extrato de cashback do produtor](#uc23--consultar-extrato-de-cashback-do-produtor) | F | ☐ | [Ir para UC23](#uc23--consultar-extrato-de-cashback-do-produtor) |
| UC24 | [Solicitar saque de cashback](#uc24--solicitar-saque-de-cashback) | F | ☐ | [Ir para UC24](#uc24--solicitar-saque-de-cashback) |
| UC25 | [Gerenciar cupons](#uc25--gerenciar-cupons) | G | ☐ | [Ir para UC25](#uc25--gerenciar-cupons) |
| UC26 | [Gerenciar usuários e papéis](#uc26--gerenciar-usuários-e-papéis) | G | ☐ | [Ir para UC26](#uc26--gerenciar-usuários-e-papéis) |
| UC27 | [Gerar relatórios de vendas por evento/lote/produto](#uc27--gerar-relatórios-de-vendas-por-eventoloteproduto) | G | ☐ | [Ir para UC27](#uc27--gerar-relatórios-de-vendas-por-eventoloteproduto) |

**Legenda:**
- ☐ = Não implementado/Revisado
- ☑ = Implementado/Revisado
- ⚠ = Em andamento/Revisão pendente

---

## Grupo A — Conta e Autenticação

### UC01 — Registrar usuário

#### Identificação

* **ID**: UC01
* **Nome**: Registrar usuário
* **Grupo**: A — Conta e Autenticação

#### Descrição Geral

Permite que um novo usuário se cadastre na plataforma Ingressou através de e-mail/senha ou login social (Google/Apple), com verificação por OTP/e-mail para garantir a autenticidade da conta.

#### Atores Envolvidos

* **Ator Principal**: Visitante (usuário não cadastrado)
* **Atores Secundários**:
  * Sistema de Autenticação
  * Provedores de Login Social (Google/Apple)
  * Sistema de Notificações (E-mail)
  * Sistema de Verificação OTP

#### Pré-condições

* O usuário deve ter acesso à internet
* Deve possuir um e-mail válido ou conta social (Google/Apple)
* Não deve possuir conta já cadastrada com o mesmo e-mail

#### Pós-condições

* Conta de usuário é criada no sistema
* E-mail de verificação é enviado (se cadastro por e-mail)
* Usuário recebe acesso limitado até verificação completa
* Dados são armazenados de forma segura conforme LGPD

#### Fluxo Principal

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

#### Fluxos Alternativos

* **3a. E-mail já cadastrado:**
  - Sistema exibe mensagem: "E-mail já possui conta cadastrada"
  - Oferece opção de recuperação de senha
* **3b. Dados inválidos:**
  - Sistema exibe erros específicos para cada campo
  - Permite correção sem perder dados preenchidos
* **4a. Falha na autorização social:**
  - Usuário é redirecionado de volta com erro
  - Oferece opção de cadastro por e-mail como alternativa

#### Exceções

| Código | Situação | Tratamento |
| --- | --- | --- |
| EXC-01 | Falha no envio de e-mail | Tentar reenvio; notificar usuário sobre possível atraso |
| EXC-02 | OTP expirado | Permitir solicitação de novo código |
| EXC-03 | CPF inválido | Exibir mensagem específica e solicitar correção |

#### Requisitos Relacionados

| Tipo | Código | Descrição |
| ---- | ------ | --------- |
| RF | RF01 | Cadastro de Usuário |
| RF | RF02 | Login |
| RNF | RNF04 | Proteção de Dados |
| RNF | RNF13 | LGPD |

---

### UC02 — Autenticar usuário (login/logout)

#### Identificação

* **ID**: UC02
* **Nome**: Autenticar usuário (login/logout)
* **Grupo**: A — Conta e Autenticação

#### Descrição Geral

Permite que um usuário autentique-se na plataforma através de e-mail/senha ou login social (Google/Apple), com controle de rate-limit para prevenir ataques de força bruta. Também permite logout seguro.

#### Atores Envolvidos

* **Ator Principal**: Visitante/Cliente (usuário cadastrado)
* **Atores Secundários**:
  * Sistema de Autenticação
  * Provedores de Login Social
  * Sistema de Rate Limiting
  * Sistema de Sessão JWT

#### Pré-condições

* Usuário deve possuir conta cadastrada e verificada
* Deve ter acesso à internet
* Conta não deve estar bloqueada por tentativas excessivas

#### Pós-condições

* Sessão JWT é criada (1h) com refresh token (7d)
* Usuário é autenticado e redirecionado
* Log de acesso é registrado para auditoria
* Rate-limit é aplicado para prevenir abuso

#### Fluxo Principal (Login)

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

#### Fluxo Principal (Logout)

1. Usuário autenticado acessa menu de perfil
2. Clica em "Sair" ou "Logout"
3. Sistema invalida JWT e refresh token
4. Limpa dados de sessão no cliente
5. Redireciona para página inicial

#### Fluxos Alternativos

* **3a. Credenciais inválidas:**
  - Sistema incrementa contador de tentativas
  - Exibe mensagem genérica de erro
  - Após 5 tentativas, bloqueia temporariamente
* **3b. Conta bloqueada:**
  - Exibe tempo restante para desbloqueio
  - Oferece opção de recuperação de senha

#### Exceções

| Código | Situação | Tratamento |
| --- | --- | --- |
| EXC-04 | Rate-limit excedido | Bloquear por 15 minutos; notificar usuário |
| EXC-05 | Falha na geração de JWT | Tentar novamente; logar erro crítico |
| EXC-06 | Refresh token inválido | Solicitar novo login |

#### Requisitos Relacionados

| Tipo | Código | Descrição |
| ---- | ------ | --------- |
| RF | RF02 | Login |
| RF | RF03 | Sessão JWT |
| RNF | RNF05 | Sessões/JWT |

---

### UC03 — Gerenciar perfil do usuário

#### Identificação

* **ID**: UC03
* **Nome**: Gerenciar perfil do usuário
* **Grupo**: A — Conta e Autenticação

#### Descrição Geral

Permite que um usuário autenticado visualize e edite seus dados pessoais, exceto CPF, e gerencie provedores sociais vinculados à sua conta.

#### Atores Envolvidos

* **Ator Principal**: Cliente (usuário autenticado)
* **Atores Secundários**:
  * Sistema de Perfil
  * Provedores de Login Social
  * Sistema de Validação de Dados

#### Pré-condições

* Usuário deve estar autenticado
* Deve ter sessão válida
* Dados devem estar atualizados

#### Pós-condições

* Dados do perfil são atualizados
* Alterações são registradas em auditoria
* Provedores sociais são vinculados/desvinculados conforme solicitado

#### Fluxo Principal

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

#### Fluxos Alternativos

* **5a. Falha na confirmação de e-mail:**
  - Mantém e-mail original
  - Notifica sobre falha na alteração
* **6a. Tentativa de desvincular último provedor:**
  - Impede ação se não houver senha cadastrada
  - Solicita criação de senha primeiro

#### Exceções

| Código | Situação | Tratamento |
| --- | --- | --- |
| EXC-07 | Dados inválidos | Exibir erros específicos por campo |
| EXC-08 | E-mail já em uso | Solicitar outro e-mail |
| EXC-09 | Falha na vinculação social | Tentar novamente; exibir erro específico |

#### Requisitos Relacionados

| Tipo | Código | Descrição |
| ---- | ------ | --------- |
| RF | RF05 | Perfil |
| RNF | RNF04 | Proteção de Dados |
| RNF | RNF13 | LGPD |

---

### UC04 — Cadastrar produtor (Admin)

#### Identificação

* **ID**: UC04
* **Nome**: Cadastrar produtor (Admin)
* **Grupo**: A — Conta e Autenticação

#### Descrição Geral

Permite que o administrador cadastre um novo produtor no sistema, realizando onboarding com KYC básico, validação de dados bancários/PIX e habilitação de acesso ao painel de leitura.

#### Atores Envolvidos

* **Ator Principal**: Administrador
* **Atores Secundários**:
  * Sistema de Validação (CNPJ/CPF)
  * Sistema de KYC
  * Sistema de Pagamentos (PIX)
  * Sistema de Notificações

#### Pré-condições

* Administrador deve estar autenticado
* Deve ter permissões de administração
* Sistema de validação deve estar operacional

#### Pós-condições

* Produtor é cadastrado no sistema
* Dados são validados e verificados
* Acesso ao painel é habilitado
* Notificações são enviadas

#### Fluxo Principal

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
8. Configura percentual padrão de cashback (defaultCashbackPercent)
9. Anexa documentos (contrato, termos)
10. Sistema realiza validações automáticas
11. **Se validações OK:**
    - Cria conta do produtor
    - Envia credenciais por e-mail
    - Habilita acesso ao painel
12. **Se validações falham:**
    - Exibe erros específicos
    - Permite correção dos dados

#### Fluxos Alternativos

* **4a. CNPJ inválido:**
  - Exibe erro específico
  - Sugere verificação manual
* **6a. Validação bancária falha:**
  - Solicita dados bancários alternativos
  - Oferece validação manual

#### Exceções

| Código | Situação | Tratamento |
| --- | --- | --- |
| EXC-10 | Falha na API de validação | Permitir cadastro manual com flag de pendência |
| EXC-11 | Chave PIX inválida | Exibir erro específico; solicitar correção |

#### Requisitos Relacionados

| Tipo | Código | Descrição |
| ---- | ------ | --------- |
| RF | RF12 | Onboarding de Produtor (Admin) |
| RF | RF13 | Verificação/KYC |
| RNF | RNF04 | Proteção de Dados |

---

## Grupo B — Eventos, Lotes e Produtos

### UC05 — Criar evento

#### Identificação

* **ID**: UC05
* **Nome**: Criar evento
* **Grupo**: B — Eventos, Lotes e Produtos

#### Descrição Geral

Permitir que o administrador cadastre um novo evento na plataforma. O evento é criado com status inicial DRAFT e pode ser editado antes da publicação. O administrador vincula o evento a um ou mais produtores.

#### Atores Envolvidos

* **Ator Principal**: Administrador
* **Atores Secundários**:
  * Sistema de Eventos
  * Sistema de Categorias
  * Sistema de Geolocalização
  * Sistema de Upload de Arquivos

#### Pré-condições

* Administrador deve estar autenticado
* Deve ter permissões de administração
* Sistema deve estar operacional

#### Pós-condições de Sucesso

* Evento é criado com status inicial (DRAFT)
* Evento pode ser vinculado a produtores posteriormente
* Nenhum lote ou produto extra é obrigatório neste momento

#### Fluxo Principal

1. Administrador acessa painel administrativo
2. Navega para "Gerenciar Eventos"
3. Clica em "Criar Novo Evento"
4. Preenche dados básicos (nome, descrição)
5. Faz upload do banner/imagem do evento
6. Insere informações de localização (endereço, cidade, UF) ou seleciona Location existente
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

#### Fluxos Alternativos

* **5A. Categorias inválidas:**
  - Sistema rejeita categorias inexistentes e exibe mensagem de erro
* **6A. Dados obrigatórios ausentes:**
  - Sistema notifica campos obrigatórios faltantes e impede o salvamento

#### Exceções

| Código | Situação | Tratamento |
| --- | --- | --- |
| EXC-12 | Falha no upload de imagem | Tentar novamente; permitir evento sem imagem |
| EXC-13 | Data inválida | Exibir erro específico; sugerir datas válidas |
| EXC-14 | Falha na validação de localização | Permitir criação com validação manual posterior |

#### Requisitos Relacionados

| Tipo | Código | Descrição |
| ---- | ------ | --------- |
| RF | RF15 | Criação de Evento (Admin) |
| RF | RF20 | Gerenciar Categorias (Admin) |
| RB | RB13 | Criação de Evento (Admin) |

---

### UC06 — Configurar localização, categorias e imagem do evento

#### Identificação

* **ID**: UC06
* **Nome**: Configurar localização, categorias e imagem do evento
* **Grupo**: B — Eventos, Lotes e Produtos

#### Descrição Geral

Permite que o administrador configure detalhes adicionais do evento, incluindo localização completa (com foto, complemento, CEP e coordenadas), categorias obrigatórias e imagem/banner do evento. O administrador também pode criar novas localizações e categorias.

#### Atores Envolvidos

* **Ator Principal**: Administrador
* **Atores Secundários**:
  * Sistema de Geolocalização
  * Sistema de Upload de Arquivos
  * Sistema de Categorias

#### Pré-condições

* Evento existe e está em status DRAFT ou PUBLISHED
* Administrador deve ter permissões de administração

#### Pós-condições

* Localização é configurada ou atualizada (ou criada se nova)
* Categorias são atribuídas ao evento (ou criadas se novas)
* Imagem/banner é carregado e associado ao evento

#### Fluxo Principal

1. Administrador acessa tela de edição do evento
2. Navega para seção "Configurações"
3. **Configurar localização:**
   - Seleciona Location existente ou cria nova
   - Preenche endereço, cidade, UF, país
   - (Opcional) adiciona complemento, CEP, coordenadas (latitude/longitude)
   - (Opcional) faz upload de foto da localização
4. **Configurar categorias:**
   - Seleciona uma ou mais categorias obrigatórias (ou cria nova categoria)
   - Sistema valida categorias existentes
5. **Configurar imagem:**
   - Faz upload de banner/imagem do evento
   - Sistema valida formato e tamanho
6. Administrador salva alterações
7. Sistema atualiza Event e Location (se criada)
8. Sistema invalida cache relacionado

#### Fluxos Alternativos

* **3a. Endereço não encontrado:**
  - Sugere endereços similares
  - Permite inserção manual
* **4a. Categoria não existe:**
  - Solicita ao administrador criação de nova categoria
  - Pode continuar sem categoria temporariamente

#### Exceções

| Código | Situação | Tratamento |
| --- | --- | --- |
| EXC-15 | Falha no upload de imagem | Tentar novamente; permitir evento sem imagem |
| EXC-16 | Formato de imagem inválido | Exibir erro específico; solicitar formato válido |
| EXC-17 | Falha na validação de coordenadas | Permitir evento sem coordenadas |

#### Requisitos Relacionados

| Tipo | Código | Descrição |
| ---- | ------ | --------- |
| RF | RF15 | Criação de Evento (Admin) |
| RF | RF20 | Gerenciar Categorias (Admin) |
| RF | RF65 | Gestão de Localização |
| RB | RB16 | Taxonomia Oficial de Categorias |
| RB | RB17 | Localização Obrigatória |

---

### UC07 — Gerenciar lotes de ingressos do evento

#### Identificação

* **ID**: UC07
* **Nome**: Gerenciar lotes de ingressos do evento
* **Grupo**: B — Eventos, Lotes e Produtos

#### Descrição Geral

Permitir que o administrador crie/edite lotes de ingressos (TicketLot) de um evento, definindo preço, quantidade, janela de venda e tipos de ingressos.

#### Atores Envolvidos

* **Ator Principal**: Administrador
* **Atores Secundários**:
  * Sistema de Lotes
  * Sistema de Eventos
  * Sistema de Validação

#### Pré-condições

* Evento existe e está em estado DRAFT ou PUBLISHED
* Administrador deve ter permissões de administração

#### Pós-condições

* Um ou mais lotes são criados/atualizados para o evento
* Estoque de cada lote é definido por totalQuantity

#### Fluxo Principal

1. Administrador acessa tela de edição do evento
2. Seleciona seção "Lotes"
3. Sistema lista lotes existentes (se houver)
4. Administrador cria um novo lote informando:
   - Nome (ex.: "Lote 1 – Inteira", "VIP")
   - Preço
   - Quantidade total (totalQuantity)
   - Período de venda (startsAt, endsAt, opcional)
5. Administrador salva o lote
6. Sistema cria TicketLot associado ao Event com soldQuantity = 0 e status ACTIVE

#### Fluxos Alternativos

* **4A. Administrador altera lote existente:**
  - Sistema valida se não haverá inconsistência (ex.: reduzir totalQuantity abaixo do soldQuantity)
* **4B. Administrador desativa lote:**
  - Sistema marca status = CANCELLED para parar de vender aquele lote

#### Regras de Negócio Importantes

* soldQuantity jamais pode ser maior que totalQuantity
* Ao confirmar pagamento, o sistema incrementa soldQuantity
* Lote encerra automaticamente quando esgotar quantidade ou atingir fim da janela de venda (o que vier primeiro)

#### Exceções

| Código | Situação | Tratamento |
| --- | --- | --- |
| EXC-18 | Falha na validação de datas | Exibir erro específico; sugerir correção |
| EXC-19 | Erro ao salvar lote | Tentar novamente; notificar produtor |
| EXC-20 | Tentativa de reduzir quantidade abaixo do vendido | Bloquear alteração; exibir quantidade mínima permitida |

#### Requisitos Relacionados

| Tipo | Código | Descrição |
| ---- | ------ | --------- |
| RF | RF21 | Criação de Lotes (Admin) |
| RF | RF22 | Encerramento por Limite |
| RF | RF23 | Tipos de Ingressos |
| RB | RB11 | Lote por Tempo/Quantidade |

---

### UC08 — Gerenciar produtos extras do evento

#### Identificação

* **ID**: UC08
* **Nome**: Gerenciar produtos extras do evento
* **Grupo**: B — Eventos, Lotes e Produtos

#### Descrição Geral

Permite que o administrador crie, edite e gerencie produtos e serviços extras (merchandising, serviços adicionais) que podem ser vendidos junto com ingressos no evento.

#### Atores Envolvidos

* **Ator Principal**: Administrador
* **Atores Secundários**:
  * Sistema de Produtos
  * Sistema de Eventos
  * Sistema de Validação

#### Pré-condições

* Evento existe
* Administrador deve ter permissões de administração

#### Pós-condições

* Produtos/serviços são criados/atualizados para o evento
* Estoque de produtos é controlado (totalQuantity, soldQuantity)

#### Fluxo Principal

1. Administrador acessa tela de edição do evento
2. Seleciona seção "Produtos Extras"
3. Sistema lista produtos existentes (se houver)
4. Administrador cria um novo produto informando:
   - Nome, descrição
   - Tipo (SERVICE, MERCH, etc.)
   - Preço
   - Quantidade total (totalQuantity)
   - Status ativo/inativo
5. Administrador salva o produto
6. Sistema cria Product associado ao Event com soldQuantity = 0 e active = true

#### Fluxos Alternativos

* **4A. Administrador altera produto existente:**
  - Sistema valida se não haverá inconsistência (ex.: reduzir totalQuantity abaixo do soldQuantity)
* **4B. Administrador desativa produto:**
  - Sistema marca active = false para parar de vender aquele produto

#### Exceções

| Código | Situação | Tratamento |
| --- | --- | --- |
| EXC-21 | Tentativa de reduzir quantidade abaixo do vendido | Bloquear alteração; exibir quantidade mínima permitida |
| EXC-22 | Erro ao salvar produto | Tentar novamente; notificar produtor |

#### Requisitos Relacionados

| Tipo | Código | Descrição |
| ---- | ------ | --------- |
| RF | RF53 | Criação de Produtos (Admin) |
| RF | RF54 | Gestão de Produtos |
| RF | RF56 | Estoque de Produtos |
| RB | RB18 | Produtos em Eventos |

---

### UC09 — Publicar / despublicar evento

#### Identificação

* **ID**: UC09
* **Nome**: Publicar / despublicar evento
* **Grupo**: B — Eventos, Lotes e Produtos

#### Descrição Geral

Permite que o administrador publique um evento que estava em rascunho, desde que tenha pelo menos um lote válido e categoria atribuída, tornando-o visível para o público. Também permite despublicar um evento publicado.

#### Atores Envolvidos

* **Ator Principal**: Administrador
* **Atores Secundários**:
  * Sistema de Eventos
  * Sistema de Lotes
  * Sistema de Cache
  * Sistema de Notificações

#### Pré-condições

* Evento deve estar em status DRAFT (para publicar) ou PUBLISHED (para despublicar)
* Para publicar: deve ter pelo menos um lote válido e categoria atribuída
* Administrador deve ter permissões de administração

#### Pós-condições

* Evento é publicado e visível publicamente (ou despublicado)
* Cache é atualizado
* Notificações são enviadas (se publicado)
* Log de auditoria é registrado

#### Fluxo Principal (Publicar)

1. Administrador acessa lista de eventos em rascunho
2. Seleciona evento para publicar
3. Sistema verifica pré-condições:
   - Pelo menos 1 lote válido
   - Categoria atribuída
   - Dados obrigatórios preenchidos
4. **Se pré-condições atendidas:**
   - Altera status para PUBLISHED
   - Atualiza data de publicação
   - Invalida cache de eventos
   - Envia notificações para produtores vinculados
5. **Se pré-condições não atendidas:**
   - Exibe lista de pendências
   - Impede publicação até correção

#### Fluxo Principal (Despublicar)

1. Administrador acessa evento publicado
2. Clica em "Despublicar"
3. Sistema confirma ação
4. Altera status para DRAFT
5. Invalida cache de eventos
6. Evento deixa de aparecer no catálogo público

#### Fluxos Alternativos

* **3a. Lotes inválidos:**
  - Lista lotes com problemas
  - Oferece correção direta
* **3b. Sem categoria:**
  - Redireciona para seleção de categoria
  - Permite atribuição rápida

#### Exceções

| Código | Situação | Tratamento |
| --- | --- | --- |
| EXC-23 | Falha na atualização do cache | Tentar novamente; notificar admin |
| EXC-24 | Erro nas notificações | Continuar publicação; tentar notificar depois |

#### Requisitos Relacionados

| Tipo | Código | Descrição |
| ---- | ------ | --------- |
| RF | RF17 | Publicação (Admin) |
| RNF | RNF15 | Cache |

---

## Grupo C — Catálogo e Descoberta

### UC10 — Listar e filtrar eventos

#### Identificação

* **ID**: UC10
* **Nome**: Listar e filtrar eventos
* **Grupo**: C — Catálogo e Descoberta

#### Descrição Geral

Permite que usuários (autenticados ou não) descubram eventos através de busca por nome do evento e filtros por localização (cidade/UF) e categoria, com URLs amigáveis para compartilhamento.

#### Atores Envolvidos

* **Ator Principal**: Visitante / Cliente (usuário autenticado ou visitante)
* **Atores Secundários**:
  * Sistema de Busca
  * Sistema de Cache (Redis)
  * Sistema de Geolocalização
  * Sistema de URLs Amigáveis

#### Pré-condições

* Deve haver eventos publicados no sistema
* Sistema de busca deve estar operacional
* Cache deve estar sincronizado

#### Pós-condições

* Lista de eventos filtrados é exibida
* Parâmetros de busca são preservados na URL
* Cache é atualizado para próximas consultas
* Métricas de busca são registradas

#### Fluxo Principal

1. Usuário acessa página inicial ou catálogo de eventos
2. **Busca por nome do evento:**
   - Digita nome do evento no campo de busca
   - Sistema busca eventos pelo nome
3. **Filtros por localização:**
   - Seleciona UF e cidade (autocompletar)
   - Sistema filtra eventos da região
4. **Filtros por categoria:**
   - Escolhe categoria(ies) desejada(s)
   - Sistema aplica filtro categórico
5. Exibe lista paginada de eventos
6. URL é atualizada com parâmetros para compartilhamento

#### Fluxos Alternativos

* **2a. Busca sem resultados:**
  - Exibe mensagem "Nenhum evento encontrado"
  - Sugere filtros alternativos ou termos similares
* **3a. Localização não encontrada:**
  - Sugere cidades próximas
  - Oferece busca por UF apenas
* **4a. Múltiplas categorias:**
  - Permite seleção múltipla
  - Aplica filtro OR entre categorias
* **2b. Busca combinada:**
  - Usuário pode combinar busca por nome com filtros de localização e categoria
  - Sistema aplica todos os filtros simultaneamente

#### Exceções

| Código | Situação | Tratamento |
| --- | --- | --- |
| EXC-25 | Sistema de busca indisponível | Exibir eventos em ordem cronológica |
| EXC-26 | Cache expirado | Buscar diretamente no banco |
| EXC-27 | Parâmetros inválidos na URL | Usar valores padrão |

#### Requisitos Relacionados

| Tipo | Código | Descrição |
| ---- | ------ | --------- |
| RF | RF06 | Busca Global |
| RF | RF07 | Filtro por Localização |
| RF | RF08 | Filtro por Categoria |
| RF | RF11 | URLs Amigáveis |
| RNF | RNF15 | Cache |
| RNF | RNF16 | Busca e Filtros |

---

### UC11 — Visualizar detalhes do evento, lotes e produtos

#### Identificação

* **ID**: UC11
* **Nome**: Visualizar detalhes do evento, lotes e produtos
* **Grupo**: C — Catálogo e Descoberta

#### Descrição Geral

Permite que usuários visualizem informações detalhadas de um evento específico, incluindo dados principais, categorias, localização, datas, lotes disponíveis, produtos extras e opção de compra.

#### Atores Envolvidos

* **Ator Principal**: Visitante / Cliente (usuário autenticado ou visitante)
* **Atores Secundários**:
  * Sistema de Eventos
  * Sistema de Cache
  * Sistema de Geolocalização

#### Pré-condições

* Evento deve estar publicado
* Deve ter pelo menos um lote válido
* Sistema deve estar operacional

#### Pós-condições

* Página do evento é exibida
* Dados são carregados do cache quando possível
* Métricas de visualização são registradas

#### Fluxo Principal

1. Usuário clica em evento da listagem ou acessa URL direta
2. Sistema carrega dados do evento (nome, descrição, banner)
3. Exibe informações de localização (endereço, cidade, UF)
4. Mostra datas e horários (início/fim)
5. Lista categorias atribuídas
6. **Se evento ativo:**
   - Exibe lotes disponíveis com preços
   - Mostra quantidade restante
   - Exibe produtos extras disponíveis (se houver)
   - Exibe botão "Comprar Ingressos"
7. **Se evento encerrado:**
   - Exibe mensagem "Evento encerrado"
   - Mostra dados históricos
8. Sistema registra visualização para métricas

#### Fluxos Alternativos

* **6a. Lotes esgotados:**
  - Exibe "Ingressos esgotados"
  - Oferece lista de espera (se configurado)
* **6b. Evento cancelado:**
  - Exibe aviso de cancelamento
  - Informa sobre reembolsos

#### Exceções

| Código | Situação | Tratamento |
| --- | --- | --- |
| EXC-28 | Evento não encontrado | Redirecionar para página 404 |
| EXC-29 | Evento não publicado | Exibir erro de acesso |
| EXC-30 | Falha no carregamento | Tentar recarregar dados |

#### Requisitos Relacionados

| Tipo | Código | Descrição |
| ---- | ------ | --------- |
| RF | RF18 | Página Pública do Evento |
| RNF | RNF15 | Cache |

---

## Grupo D — Pedidos, Pagamentos e Cupons

### UC12 — Criar pedido com ingressos e produtos

#### Identificação

* **ID**: UC12
* **Nome**: Criar pedido com ingressos e produtos
* **Grupo**: D — Pedidos, Pagamentos e Cupons

#### Descrição Geral

Permitir que o usuário monte um carrinho com ingressos (por lote) e produtos extras do evento, gerando um Order.

#### Atores Envolvidos

* **Ator Principal**: Cliente
* **Atores Secundários**:
  * Sistema de Eventos
  * Sistema de Lotes
  * Sistema de Produtos

#### Pré-condições

* Usuário está autenticado
* Evento está PUBLISHED
* Lotes e produtos desejados estão active = true

#### Pós-condições de Sucesso

* Pedido (Order) é criado com status PENDING
* Os itens são registrados em OrderItem, referenciando Event, TicketLot e Product conforme o caso

#### Fluxo Principal

1. Cliente acessa página de detalhes do evento
2. Sistema exibe lotes de ingressos e produtos extras
3. Cliente seleciona:
   - Quantidade de ingressos por lote (TicketLot)
   - Quantidade de produtos extras (Product)
4. Cliente prossegue para checkout
5. Sistema calcula:
   - subtotal = soma dos (unitPrice * quantity) de todos os OrderItem
6. Cliente confirma intenção de compra
7. Sistema cria um Order com:
   - status PENDING
   - subtotal preenchido
   - discountAmount = 0
   - totalAmount = subtotal
8. Sistema cria OrderItem para cada combinação de (evento, lote, produto) com:
   - itemType = TICKET ou PRODUCT
   - quantity, unitPrice e totalPrice

#### Fluxos Alternativos

* **3A. Lote ou produto inativo:**
  - Sistema não permite selecionar item e exibe mensagem "produto/lote indisponível"
* **7A. Usuário abandona antes de confirmar:**
  - Pedido não é criado

#### Exceções

| Código | Situação | Tratamento |
| --- | --- | --- |
| EXC-31 | Estoque insuficiente | Exibir mensagem; atualizar disponibilidade |
| EXC-32 | Limite por CPF excedido | Exibir mensagem "Limite de ingressos por CPF excedido" |
| EXC-33 | Falha ao criar pedido | Tentar novamente; notificar usuário |

#### Requisitos Relacionados

| Tipo | Código | Descrição |
| ---- | ------ | --------- |
| RF | RF26 | Checkout |
| RF | RF24 | Limite por CPF |
| RF | RF55 | Tipos de Item no Pedido |
| RB | RB03 | Limite por CPF |
| RB | RB19 | Status de Pedido |

---

### UC13 — Aplicar cupom de desconto

#### Identificação

* **ID**: UC13
* **Nome**: Aplicar cupom de desconto
* **Grupo**: D — Pedidos, Pagamentos e Cupons

#### Descrição Geral

Permitir aplicação de cupom em um pedido pendente, validando vigência, limites de uso e aplicando desconto percentual ou fixo.

#### Atores Envolvidos

* **Ator Principal**: Cliente
* **Atores Secundários**:
  * Sistema de Cupons
  * Sistema de Influenciadores
  * Sistema de Checkout

#### Pré-condições

* Pedido existe com status PENDING
* Cupom existe e está active = true

#### Pós-condições

* Se válido, pedido é atualizado com discountAmount e totalAmount reajustados e coupon associado
* usageCount do cupom pode ser incrementado conforme regra

#### Fluxo Principal

1. No checkout, cliente informa um código de cupom
2. Sistema busca Coupon pelo código
3. Sistema valida:
   - active = true
   - validFrom <= agora <= validUntil
   - usageCount < maxUses
   - Aplicável ao evento (se vinculado)
4. Sistema calcula o desconto:
   - Se discountType == PERCENT, discountAmount = subtotal * discountPercent
   - Se discountType == FIXED, discountAmount = discountValue
5. Sistema recalcula totalAmount = subtotal - discountAmount
6. Sistema associa o Coupon ao Order e exibe valores atualizados

#### Fluxos Alternativos / Exceções

* **3A. Cupom expirado ou inativo:**
  - Sistema rejeita cupom, exibe motivo e não altera o pedido
* **3B. Limite de uso atingido (usageCount >= maxUses):**
  - Cupom é rejeitado

#### Exceções

| Código | Situação | Tratamento |
| --- | --- | --- |
| EXC-34 | Falha na validação do cupom | Tentar novamente; notificar suporte |
| EXC-35 | Erro no registro de atribuição | Continuar checkout; registrar depois |

#### Requisitos Relacionados

| Tipo | Código | Descrição |
| ---- | ------ | --------- |
| RF | RF31 | Cupom de Influenciador |
| RB | RB12 | Cupom de Influenciador |

---

### UC14 — Realizar pagamento (PIX ou cartão)

#### Identificação

* **ID**: UC14
* **Nome**: Realizar pagamento (PIX ou cartão)
* **Grupo**: D — Pedidos, Pagamentos e Cupons

#### Descrição Geral

Permitir que o cliente pague um pedido pendente via PIX ou cartão (crédito/débito).

#### Atores Envolvidos

* **Ator Principal**: Cliente
* **Atores Secundários**: Gateway de Pagamento

#### Pré-condições

* Pedido em status PENDING
* totalAmount > 0

#### Pós-condições de Sucesso

* É criado/atualizado um Payment associado ao Order
* Redirecionamento ou exibição de informações de pagamento (QR PIX ou status de cartão)

#### Fluxo Principal (Geral)

1. Cliente seleciona forma de pagamento: PIX ou cartão
2. Sistema cria ou atualiza Payment com:
   - method (PIX, CREDIT_CARD ou DEBIT_CARD)
   - amount = order.totalAmount
   - status = PENDING
3. **Se PIX:**
   - Sistema solicita ao gateway a criação de uma cobrança PIX
   - Gateway retorna pixQrCode e pixExpiresAt
   - Sistema preenche esses campos no Payment e exibe o QRCode para o cliente
4. **Se cartão:**
   - Cliente informa dados de cartão (ou tokeniza no frontend)
   - Sistema envia dados/token para o gateway
   - Gateway responde com autorização (authorizationCode, cardBrand, etc.), podendo ser aprovada ou recusada
   - Sistema atualiza status do Payment conforme resposta

#### Fluxos Alternativos

* **4A. Pagamento por cartão recusado:**
  - Payment.status = REFUSED
  - Order.status permanece PENDING
* **3A. PIX expirado sem pagamento:**
  - Após pixExpiresAt, sistema pode expirar Payment e Order

#### Exceções

| Código | Situação | Tratamento |
| --- | --- | --- |
| EXC-36 | Falha na API de pagamento | Exibir erro amigável; logar falha e enviar alerta |
| EXC-37 | Gateway indisponível | Tentar novamente; oferecer método alternativo |

#### Requisitos Relacionados

| Tipo | Código | Descrição |
| ---- | ------ | --------- |
| RF | RF27 | PIX |
| RF | RF28 | Cartão de Crédito |
| RF | RF28.1 | Cartão de Débito |
| RB | RB04 | Reserva PIX |
| RB | RB20 | Status de Pagamento |

---

### UC15 — Processar confirmação de pagamento (webhook)

#### Identificação

* **ID**: UC15
* **Nome**: Processar confirmação de pagamento (webhook)
* **Grupo**: D — Pedidos, Pagamentos e Cupons

#### Descrição Geral

Processar confirmação de pagamento recebida via webhook do gateway, atualizando status do pedido e emitindo tickets quando aprovado.

#### Atores Envolvidos

* **Ator Principal**: Gateway de Pagamento
* **Atores Secundários**:
  * Sistema de Pagamentos
  * Sistema de Tickets
  * Sistema de Notificações

#### Pré-condições

* Payment existe com status PENDING ou PROCESSING
* Webhook recebido do gateway é válido e assinado

#### Pós-condições

* Payment.status é atualizado conforme resposta do gateway
* Se aprovado, Order.status = PAID e tickets são emitidos
* Notificações são enviadas

#### Fluxo Principal

1. Gateway envia webhook de confirmação de pagamento
2. Sistema valida assinatura e autenticidade do webhook
3. Sistema busca Payment pelo gatewayTransactionId
4. **Se pagamento aprovado:**
   - Atualiza Payment.status = APPROVED
   - Atualiza Order.status = PAID
   - Dispara processo de emissão de tickets (UC17)
   - Envia notificações de confirmação
5. **Se pagamento recusado:**
   - Atualiza Payment.status = REFUSED
   - Order.status permanece PENDING
   - Notifica cliente sobre recusa

#### Fluxos Alternativos

* **4a. Pagamento PIX confirmado:**
  - Sistema processa confirmação e segue fluxo de aprovação
* **4b. Pagamento expirado:**
  - Atualiza Payment.status = EXPIRED
  - Atualiza Order.status = EXPIRED
  - Libera estoque de ingressos e produtos

#### Exceções

| Código | Situação | Tratamento |
| --- | --- | --- |
| EXC-38 | Webhook inválido ou não assinado | Rejeitar webhook; logar tentativa |
| EXC-39 | Payment não encontrado | Logar erro; notificar suporte |
| EXC-40 | Falha na emissão de tickets | Tentar novamente; notificar suporte |

#### Requisitos Relacionados

| Tipo | Código | Descrição |
| ---- | ------ | --------- |
| RF | RF27 | PIX |
| RF | RF29 | Confirmação |
| RF | RF32 | Emissão |
| RB | RB04 | Reserva PIX |
| RB | RB20 | Status de Pagamento |

---

### UC16 — Cancelar pedido / lidar com expiração

#### Identificação

* **ID**: UC16
* **Nome**: Cancelar pedido / lidar com expiração
* **Grupo**: D — Pedidos, Pagamentos e Cupons

#### Descrição Geral

Permitir que o cliente cancele um pedido pendente ou que o sistema expire automaticamente pedidos com pagamento não confirmado dentro do prazo.

#### Atores Envolvidos

* **Ator Principal**: Cliente / Sistema
* **Atores Secundários**:
  * Sistema de Pedidos
  * Sistema de Estoque

#### Pré-condições

* Pedido existe com status PENDING ou AWAITING_PAYMENT
* Para cancelamento manual: cliente deve ser dono do pedido

#### Pós-condições

* Pedido é cancelado ou expirado
* Estoque de ingressos e produtos é liberado
* Se houver pagamento, é processado reembolso (se aplicável)

#### Fluxo Principal (Cancelamento Manual)

1. Cliente acessa "Meus Pedidos"
2. Seleciona pedido pendente
3. Clica em "Cancelar Pedido"
4. Sistema confirma ação
5. Atualiza Order.status = CANCELLED
6. Libera estoque de ingressos e produtos
7. Se houver Payment pendente, cancela pagamento
8. Notifica cliente sobre cancelamento

#### Fluxo Principal (Expiração Automática)

1. Sistema verifica pedidos com status PENDING ou AWAITING_PAYMENT
2. Para cada pedido:
   - Verifica se expiresAt < agora
   - Se PIX: verifica se pixExpiresAt < agora
3. **Se expirado:**
   - Atualiza Order.status = EXPIRED
   - Atualiza Payment.status = EXPIRED (se houver)
   - Libera estoque de ingressos e produtos
   - Notifica cliente sobre expiração

#### Fluxos Alternativos

* **5a. Pedido já pago:**
  - Sistema impede cancelamento manual
  - Oferece opção de solicitar reembolso (se dentro do prazo)

#### Exceções

| Código | Situação | Tratamento |
| --- | --- | --- |
| EXC-41 | Falha ao liberar estoque | Tentar novamente; notificar suporte |
| EXC-42 | Falha no cancelamento de pagamento | Processar manualmente; notificar suporte |

#### Requisitos Relacionados

| Tipo | Código | Descrição |
| ---- | ------ | --------- |
| RF | RF30 | Falha/Cancelamento |
| RB | RB04 | Reserva PIX |
| RB | RB19 | Status de Pedido |

---

## Grupo E — Tickets, Transferência e Check-in

### UC17 — Emitir tickets após pagamento aprovado

#### Identificação

* **ID**: UC17
* **Nome**: Emitir tickets após pagamento aprovado
* **Grupo**: E — Tickets, Transferência e Check-in

#### Descrição Geral

Gerar tickets (Ticket) para os itens de ingressos de um pedido pago, criando QR Codes assinados e atribuindo-os ao usuário.

#### Atores Envolvidos

* **Ator Principal**: Sistema (acionado pelo webhook ou job interno)
* **Atores Secundários**: Cliente (notificado)

#### Pré-condições

* Payment.status = APPROVED
* Order.status ainda não foi marcado como PAID
* Estoque de lotes está disponível

#### Pós-condições

* Order.status = PAID
* Para cada OrderItem com itemType = TICKET, são criados Tickets
* Tickets apontam para Order, Event, TicketLot (se houver) e User dono
* Notificação é enviada ao usuário

#### Fluxo Principal

1. Sistema recebe confirmação de pagamento aprovado (via webhook do gateway ou job)
2. Sistema carrega Order e OrderItems
3. Para cada OrderItem com itemType = TICKET:
   - Valida se ainda há estoque suficiente no TicketLot (se houver lote)
   - Atualiza soldQuantity do TicketLot (ou do Event, se sem lote)
   - Para quantity daquele item, cria N registros Ticket com:
     - qrCode (assinado digitalmente)
     - price (pode ser unitPrice)
     - status = ACTIVE
     - owner = User do pedido
     - ticketType (FULL, HALF, VIP, COURTESY)
4. Sistema marca Order.status = PAID e confirmedAt = agora
5. Sistema envia Notification ao usuário informando que os ingressos foram emitidos

#### Fluxos Alternativos

* **3A. Estoque insuficiente no TicketLot:**
  - Sistema pode:
    - não emitir os tickets daquele item,
    - registrar erro e acionar suporte/estorno
  - Na modelagem ideal, o controle de estoque é checado ANTES de aprovar o pagamento (UC12/14), mas é bom ter esse safety

#### Exceções

| Código | Situação | Tratamento |
| --- | --- | --- |
| EXC-43 | Falha na geração do QR Code | Tentar um fallback ou gerar em um processo em batch posterior |
| EXC-44 | Falha no envio de notificação | Continuar processo; tentar reenviar depois |

#### Requisitos Relacionados

| Tipo | Código | Descrição |
| ---- | ------ | --------- |
| RF | RF29 | Confirmação |
| RF | RF32 | Emissão |
| RF | RF35 | Notificações |
| RB | RB21 | Status de Ticket |

---

### UC18 — Listar tickets do usuário

#### Identificação

* **ID**: UC18
* **Nome**: Listar tickets do usuário
* **Grupo**: E — Tickets, Transferência e Check-in

#### Descrição Geral

Permite que o usuário visualize todos os seus tickets (ingressos) adquiridos, com informações do evento, status, QR Code e opções de transferência.

#### Atores Envolvidos

* **Ator Principal**: Cliente
* **Atores Secundários**: Sistema de Tickets

#### Pré-condições

* Usuário deve estar autenticado
* Deve possuir pelo menos um ticket

#### Pós-condições

* Lista de tickets é exibida
* Usuário pode visualizar detalhes, QR Code e opções de ação

#### Fluxo Principal

1. Cliente acessa "Meus Ingressos" ou "Carteira"
2. Sistema busca todos os Tickets onde ownerId = userId
3. Sistema agrupa tickets por evento (opcional)
4. Para cada ticket, exibe:
   - Nome do evento
   - Data e horário
   - Tipo de ingresso (inteira, meia, VIP)
   - Status (ACTIVE, TRANSFERRED, VALIDATED, CANCELLED, EXPIRED)
   - QR Code (se ainda não validado)
   - Opções: Transferir, Reenviar, Visualizar
5. Cliente pode filtrar por:
   - Status
   - Evento
   - Data

#### Fluxos Alternativos

* **4a. Ticket já validado:**
  - Exibe mensagem "Ingresso já utilizado"
  - Não exibe QR Code
  - Mostra data/hora do check-in

#### Exceções

| Código | Situação | Tratamento |
| --- | --- | --- |
| EXC-45 | Falha ao carregar tickets | Tentar novamente; exibir mensagem de erro |

#### Requisitos Relacionados

| Tipo | Código | Descrição |
| ---- | ------ | --------- |
| RF | RF34 | Reenvio |
| RF | RF40 | Iniciar Transferência (Remetente) |

---

### UC19 — Transferir ticket para outro usuário

#### Identificação

* **ID**: UC19
* **Nome**: Transferir ticket para outro usuário
* **Grupo**: E — Tickets, Transferência e Check-in

#### Descrição Geral

Permitir que o usuário inicie a transferência de um ticket para outra pessoa, criando uma solicitação pendente com token de aceite.

#### Atores Envolvidos

* **Ator Principal**: Cliente (dono atual do ticket)
* **Atores Secundários**:
  * Destinatário (usuário)
  * Sistema de Transferências
  * Sistema de Pagamentos (taxa)
  * Sistema de Notificações

#### Pré-condições

* Usuário está autenticado
* Usuário é o dono do Ticket
* Ticket está em status que permita transferência (ACTIVE) e transferable = true
* Caso de regra de negócio: transferência só é permitida até certa data do evento (opcional)

#### Pós-condições

* É criado um TicketTransfer com status PENDING
* Ticket fica associado a essa transferência ativa
* Um token de aceite é gerado e enviado ao destinatário (e-mail, por exemplo)

#### Fluxo Principal

1. Usuário acessa lista de tickets
2. Seleciona um ticket e aciona "Transferir"
3. Sistema verifica regras:
   - status do ticket
   - se já existe TicketTransfer ativa
   - se ainda está dentro do prazo de transferência
4. Usuário informa dados do destinatário:
   - e-mail
   - CPF (opcional, se você exigir)
5. Sistema calcula taxa de transferência (se configurada)
6. Sistema exibe resumo da transferência com taxa
7. Usuário confirma e escolhe método de pagamento da taxa
8. **Se pagamento da taxa aprovado:**
   - Sistema cria TicketTransfer com:
     - ticket
     - fromUser = usuário atual
     - recipientEmail / recipientCpf
     - status = PENDING
     - acceptToken (token único)
     - expiresAt (prazo para aceitar)
   - Sistema envia um e-mail ao destinatário com link contendo acceptToken
   - (Opcional) Sistema cria Notification para o remetente indicando que a transferência foi iniciada

#### Fluxos Alternativos

* **3A. Ticket já transferido antes (se você limitar a 1 vez):**
  - Sistema bloqueia, mostra mensagem "Ticket já foi transferido anteriormente"
* **3B. Ticket já usado ou cancelado:**
  - Sistema bloqueia transferência
* **8a. Taxa não configurada ou gratuita:**
  - Sistema cria transferência sem exigir pagamento

#### Exceções

| Código | Situação | Tratamento |
| --- | --- | --- |
| EXC-46 | Falha no pagamento da taxa | Cancelar transferência; notificar usuário |
| EXC-47 | Falha no envio de e-mail | Tentar reenvio; notificar usuário |

#### Requisitos Relacionados

| Tipo | Código | Descrição |
| ---- | ------ | --------- |
| RF | RF40 | Iniciar Transferência (Remetente) |
| RF | RF45 | Taxa de Transferência |
| RF | RF47 | Notificações |
| RB | RB15 | Política de Transferência |

---

### UC20 — Aceitar ou recusar transferência de ticket

#### Identificação

* **ID**: UC20
* **Nome**: Aceitar ou recusar transferência de ticket
* **Grupo**: E — Tickets, Transferência e Check-in

#### Descrição Geral

Permitir que o destinatário aceite a transferência e passe a ser o novo dono do ticket, ou recuse a transferência.

#### Atores Envolvidos

* **Ator Principal**: Destinatário (pode ou não estar cadastrado ainda)
* **Atores Secundários**:
  * Sistema de Transferências
  * Sistema de QR Code
  * Sistema de Notificações

#### Pré-condições

* TicketTransfer.status = PENDING
* Token de aceite (acceptToken) válido e não expirado

#### Pós-condições (Aceite)

* Ticket.owner passa a ser o usuário destinatário
* TicketTransfer.status = COMPLETED
* QR Code original é invalidado e novo QR é emitido
* Notificações são enviadas para remetente e destinatário

#### Fluxo Principal (Aceitar)

1. Destinatário acessa o link de aceite (contendo acceptToken)
2. Sistema valida:
   - se existe TicketTransfer com aquele token,
   - se status = PENDING,
   - se expiresAt >= agora
3. Se o destinatário não tiver conta:
   - sistema pode redirecionar para fluxo de cadastro e depois voltar
4. Destinatário confirma que deseja aceitar o ticket
5. Sistema:
   - Atualiza Ticket.owner = destinatário
   - Invalida QR Code original
   - Gera novo QR Code assinado
   - Atualiza TicketTransfer.status = COMPLETED
6. Sistema cria Notification:
   - para o remetente (confirmando transferência),
   - para o destinatário (confirmando recebimento)

#### Fluxo Principal (Recusar)

1. Destinatário acessa o link de aceite
2. Sistema valida token
3. Destinatário clica em "Recusar"
4. Sistema marca TicketTransfer.status = REFUSED
5. Ticket mantém o dono original
6. Sistema notifica remetente sobre recusa
7. Sistema processa reembolso da taxa (se aplicável)

#### Fluxos Alternativos

* **2A. Token inválido ou expirado:**
  - Sistema seta TicketTransfer.status = EXPIRED e informa usuário
* **5a. Falha na geração do novo QR:**
  - Tentar novamente; notificar suporte

#### Exceções

| Código | Situação | Tratamento |
| --- | --- | --- |
| EXC-48 | Ticket já foi transferido | Informar destinatário; cancelar transferência |
| EXC-49 | Falha na invalidação do QR original | Processar manualmente; notificar suporte |

#### Requisitos Relacionados

| Tipo | Código | Descrição |
| ---- | ------ | --------- |
| RF | RF41 | Aceite do Destinatário |
| RF | RF42 | Reemissão de Ingresso |
| RF | RF43 | Recusa/Expiração |
| RB | RB15 | Política de Transferência |

---

### UC21 — Realizar check-in de ticket (validação QRCode)

#### Identificação

* **ID**: UC21
* **Nome**: Realizar check-in de ticket (validação QRCode)
* **Grupo**: E — Tickets, Transferência e Check-in

#### Descrição Geral

Validar a entrada do participante via leitura do QRCode do ticket, registrando check-in com informações detalhadas e detecção de fraude.

#### Atores Envolvidos

* **Ator Principal**: Operador de Check-in
* **Atores Secundários**:
  * Cliente (portador do ticket)
  * Sistema de Validação
  * Sistema de Check-in

#### Pré-condições

* Operador está autenticado com papel de check-in
* Evento está em andamento
* Aplicativo de check-in consegue ler o QRCode e enviar ticketCode à API

#### Pós-condições de Sucesso

* Ticket.status é atualizado para VALIDATED
* Um registro CheckIn é criado com status VALID
* Informações detalhadas são registradas (deviceId, IP, location, deviceInfo)

#### Fluxo Principal

1. Operador aponta o leitor de QR para o ticket do participante
2. Aplicativo envia ticketCode (do QR) para endpoint de check-in
3. Sistema busca Ticket pelo ticketCode (ou qrCode)
4. Sistema valida:
   - se ticket existe
   - se pertence ao evento correto
   - se está em status válido para entrada (ACTIVE)
5. Sistema verifica detecção de fraude:
   - mesmo IP, dispositivo diferente
   - múltiplas tentativas recentes
6. **Se válido e sem fraude:**
   - Atualiza Ticket.status = VALIDATED
   - Atualiza Ticket.validatedAt = agora
   - Cria registro CheckIn com:
     - ticket
     - operator (User)
     - status = VALID
     - validatedAt = agora
     - deviceId, ipAddress, location, deviceInfo
     - isOffline (se aplicável)
7. Sistema retorna resposta de sucesso para o app de check-in
8. App exibe tela verde / OK

#### Fluxos Alternativos / Exceções

* **3A. Ticket não encontrado:**
  - Cria CheckIn com status = INVALID
  - App exibe erro e recusa a entrada
* **4A. Ticket já usado:**
  - Cria novo CheckIn com status = ALREADY_USED
  - App sinaliza tentativa de reutilização
* **5A. Detecção de fraude:**
  - Cria CheckIn com status = FRAUD_ATTEMPT
  - App sinaliza tentativa suspeita
  - Sistema pode bloquear ticket temporariamente
* **4B. Ticket expirado ou cancelado:**
  - CheckIn.status = EXPIRED ou INVALID
  - Entrada não permitida

#### Exceções

| Código | Situação | Tratamento |
| --- | --- | --- |
| EXC-50 | Falha na validação do QR Code | Tentar novamente; exibir erro |
| EXC-51 | Falha no registro de check-in | Tentar novamente; notificar operador |

#### Requisitos Relacionados

| Tipo | Código | Descrição |
| ---- | ------ | --------- |
| RF | RF36 | Validação |
| RF | RF37 | Registro Detalhado |
| RF | RF38 | Modo Offline |
| RF | RF57 | Detecção de Fraude |
| RB | RB10 | Check-in Único |

---

## Grupo F — Cashback e Relatórios

### UC22 — Gerar cashback para produtor em vendas

#### Identificação

* **ID**: UC22
* **Nome**: Gerar cashback para produtor em vendas
* **Grupo**: F — Cashback e Relatórios

#### Descrição Geral

Creditar cashback ao produtor com base nas vendas de seus eventos, registrando transações rastreáveis.

#### Atores Envolvidos

* **Ator Principal**: Sistema (após pagamento aprovado)
* **Atores Secundários**:
  * Produtor (notificado)
  * Sistema de Cashback

#### Pré-condições

* Order.status = PAID
* Payment.status = APPROVED
* Eventos dos OrderItems têm producer associado
* Existe configuração de cashback (Event.producerCashbackPercent ou Producer.defaultCashbackPercent)

#### Pós-condições

* Producer.cashbackBalance é incrementado
* Uma ou mais ProducerCashbackTransaction são criadas

#### Fluxo Principal

1. Após confirmar o pagamento do pedido (UC17), sistema identifica os OrderItem
2. Para cada OrderItem:
   - Carrega o Event e seu EventProducer
   - Determina o percentual de cashback:
     - Usa Event.producerCashbackPercent se não nulo,
     - Senão, usa Producer.defaultCashbackPercent
   - Calcula cashbackAmount = orderItem.totalPrice * cashbackPercent
3. Para cada produtor afetado:
   - Soma os cashbackAmount dos itens dos eventos dele
   - Atualiza producer.cashbackBalance += totalCashbackProducer
   - Cria ProducerCashbackTransaction para cada item ou consolidada por pedido:
     - producer, event, order
     - type = CREDIT
     - amount = cashbackAmount
     - balanceAfter = cashbackBalance atualizado
4. (Opcional) Envia Notification para produtor informando novo crédito de cashback

#### Fluxos Alternativos

* **2A. Evento sem configuração de cashback:**
  - Sistema pode:
    - Não gerar cashback para aquele item, ou
    - Cair no defaultCashbackPercent do produtor

#### Exceções

| Código | Situação | Tratamento |
| --- | --- | --- |
| EXC-52 | Falha ao atualizar saldo | Tentar novamente; registrar erro |
| EXC-53 | Falha ao criar transação | Tentar novamente; notificar suporte |

#### Requisitos Relacionados

| Tipo | Código | Descrição |
| ---- | ------ | --------- |
| RF | RF62 | Transações de Cashback |
| RB | RB02 | Cashback do Produtor |

---

### UC23 — Consultar extrato de cashback do produtor

#### Identificação

* **ID**: UC23
* **Nome**: Consultar extrato de cashback do produtor
* **Grupo**: F — Cashback e Relatórios

#### Descrição Geral

Permite que o produtor visualize o histórico de movimentações de cashback (créditos, débitos, ajustes) e o saldo atual.

#### Atores Envolvidos

* **Ator Principal**: Produtor
* **Atores Secundários**:
  * Sistema de Cashback
  * Sistema de Relatórios

#### Pré-condições

* Usuário autenticado
* Usuário possui perfil de produtor (EventProducer associado ao User)

#### Pós-condições

* Nenhuma alteração de estado obrigatório
* Produtor visualiza saldo atual e lista paginada de transações

#### Fluxo Principal

1. Produtor acessa área "Financeiro / Cashback"
2. Sistema obtém EventProducer vinculado ao usuário
3. Sistema recupera o cashbackBalance atual
4. Sistema lista ProducerCashbackTransaction do produtor, ordenadas por data (mais recentes primeiro), com:
   - data (createdAt)
   - tipo (CREDIT, DEBIT, ADJUSTMENT)
   - valor (amount)
   - descrição
   - event e order relacionados (se existirem)
5. Sistema exibe o saldo e o extrato na interface

#### Fluxos Alternativos

* **2A. Usuário não possui perfil de produtor:**
  - Sistema bloqueia acesso e exibe mensagem de permissão negada
* **4a. Filtrar por período:**
  - Produtor seleciona período (data inicial/final)
  - Sistema filtra transações do período
* **4b. Filtrar por tipo:**
  - Produtor seleciona tipo (CREDIT, DEBIT, ADJUSTMENT)
  - Sistema filtra transações do tipo selecionado

#### Exceções

| Código | Situação | Tratamento |
| --- | --- | --- |
| EXC-54 | Falha ao carregar extrato | Tentar novamente; exibir mensagem de erro |
| EXC-55 | Nenhuma transação encontrada | Exibir mensagem "Nenhuma movimentação registrada" |

#### Requisitos Relacionados

| Tipo | Código | Descrição |
| ---- | ------ | --------- |
| RF | RF63 | Extrato de Cashback |
| RB | RB02 | Cashback do Produtor |

---

### UC24 — Solicitar saque de cashback

#### Identificação

* **ID**: UC24
* **Nome**: Solicitar saque de cashback
* **Grupo**: F — Cashback e Relatórios

#### Descrição Geral

Permite que o produtor solicite saque do saldo de cashback acumulado, processando débito e transferência via PIX ou sistema bancário.

#### Atores Envolvidos

* **Ator Principal**: Produtor
* **Atores Secundários**:
  * Administrador (aprovação manual, se necessário)
  * Sistema de Pagamento Externo (PIX bancário)
  * Sistema de Notificações

#### Pré-condições

* Usuário autenticado com perfil de produtor
* cashbackBalance ≥ valor mínimo de saque (se houver)
* Produtor possui dados financeiros preenchidos (ex.: pixKey ou dados bancários)

#### Pós-condições de Sucesso

* Um débito de cashback é registrado via ProducerCashbackTransaction (type = DEBIT)
* cashbackBalance é reduzido
* Solicitação de saque é processada (imediata ou pendente de aprovação)

#### Fluxo Principal (Saque Imediato via PIX)

1. Produtor acessa área "Saque de cashback"
2. Sistema exibe saldo disponível e, se houver, valor mínimo para saque
3. Produtor informa valor de saque (ou clica em "Sacar tudo")
4. Sistema valida:
   - valor > 0
   - valor ≤ cashbackBalance
   - valor ≥ valor mínimo (se configurado)
5. Sistema confirma com o produtor os dados de recebimento (ex.: pixKey)
6. Sistema dispara operação de pagamento (ex.: pedido de PIX para API bancária)
7. **Se operação externa retornar sucesso:**
   - Sistema cria ProducerCashbackTransaction:
     - type = DEBIT
     - amount = valor de saque
     - description = "Saque de cashback via PIX"
     - balanceAfter = cashbackBalance - amount
   - Atualiza cashbackBalance do produtor
   - Sistema exibe mensagem de sucesso e registra Notification para o produtor

#### Fluxo Principal (Solicitação Pendente)

1. Produtor acessa área "Saque de cashback"
2. Sistema exibe saldo disponível
3. Produtor informa valor de saque
4. Sistema valida valor
5. Sistema cria solicitação de saque com status PENDING
6. Administrador recebe notificação para aprovar saque
7. **Se aprovado:**
   - Sistema processa pagamento
   - Cria transação DEBIT
   - Atualiza saldo
8. **Se recusado:**
   - Sistema notifica produtor sobre recusa

#### Fluxos Alternativos

* **4A. Valor solicitado maior que o saldo:**
  - Sistema rejeita com erro "saldo insuficiente"
* **6A. Falha na API de pagamento:**
  - Sistema não altera saldo nem cria transação de débito
  - Exibe mensagem de erro e, opcionalmente, registra incidente para suporte
* **4b. Valor abaixo do mínimo:**
  - Sistema exibe mensagem informando valor mínimo necessário

#### Exceções

| Código | Situação | Tratamento |
| --- | --- | --- |
| EXC-56 | Dados financeiros não configurados | Solicitar configuração de chave PIX ou dados bancários |
| EXC-57 | Falha na API de pagamento externa | Tentar novamente; notificar suporte |
| EXC-58 | Saldo insuficiente | Exibir saldo disponível; impedir saque |

#### Requisitos Relacionados

| Tipo | Código | Descrição |
| ---- | ------ | --------- |
| RF | RF64 | Configuração de Percentual |
| RB | RB02 | Cashback do Produtor |

---

## Grupo G — Administração

### UC25 — Gerenciar cupons

#### Identificação

* **ID**: UC25
* **Nome**: Gerenciar cupons
* **Grupo**: G — Administração

#### Descrição Geral

Criar, editar, ativar/desativar cupons de desconto que podem ser usados em pedidos, com validação de código único e regras de aplicação.

#### Atores Envolvidos

* **Ator Principal**: Administrador
* **Atores Secundários**: Produtor (se permitir cupons por evento/produtor)

#### Pré-condições

* Usuário autenticado com papel de administrador (ou produtor, se limitado ao próprio evento)
* Sistema de cupons deve estar operacional

#### Pós-condições

* Novos cupons são criados ou cupons existentes são atualizados
* Cupons podem ser ativados/desativados
* Cupons ficam disponíveis para uso nos pedidos

#### Fluxo Principal (Admin Global)

1. Administrador acessa módulo "Cupons"
2. Sistema lista cupons existentes com filtros (código, status, período de validade)
3. Admin clica em "Criar cupom"
4. Preenche dados:
   - code (código único)
   - discountType (PERCENT ou FIXED)
   - discountPercent ou discountValue
   - validFrom, validUntil
   - maxUses
   - active = true/false
   - (opcional) associação a evento específico ou a um produtor
   - (opcional) influencerId para rastreamento
5. Sistema valida:
   - código único
   - valores coerentes (não ter ambos percent e value ao mesmo tempo, etc.)
   - datas válidas
6. Sistema salva o cupom
7. Cupom passa a estar disponível para uso nos pedidos, conforme regras de aplicação

#### Fluxo Principal (Editar Cupom)

1. Admin escolhe um cupom da lista
2. Clica em "Editar"
3. Altera propriedades desejadas
4. Sistema valida alterações
5. Sistema salva alterações
6. Sistema impede alterações destrutivas em cupons já amplamente usados (regra de negócio opcional)

#### Fluxos Alternativos

* **3A. Editar cupom existente:**
  - Admin escolhe um cupom da lista, altera propriedades e salva
  - Sistema impede alterações destrutivas em cupons já amplamente usados
* **5A. Validação falha:**
  - Sistema exibe erros e não salva o registro
* **4a. Desativar cupom:**
  - Admin marca active = false
  - Cupom deixa de estar disponível para novos pedidos
* **4b. Vincular cupom a evento:**
  - Admin seleciona evento(s) específico(s)
  - Sistema cria associação via CouponEvent

#### Exceções

| Código | Situação | Tratamento |
| --- | --- | --- |
| EXC-59 | Código já existe | Exibir erro; solicitar código alternativo |
| EXC-60 | Datas inválidas | Exibir erro específico; sugerir datas válidas |
| EXC-61 | Falha ao salvar cupom | Tentar novamente; notificar admin |

#### Requisitos Relacionados

| Tipo | Código | Descrição |
| ---- | ------ | --------- |
| RF | RF31 | Cupom de Influenciador |
| RB | RB12 | Cupom de Influenciador |

---

### UC26 — Gerenciar usuários e papéis

#### Identificação

* **ID**: UC26
* **Nome**: Gerenciar usuários e papéis
* **Grupo**: G — Administração

#### Descrição Geral

Permitir que o administrador gerencie contas de usuários, incluindo ativar/desativar e atribuir papéis (roles) conforme RBAC.

#### Atores Envolvidos

* **Ator Principal**: Administrador
* **Atores Secundários**:
  * Sistema de RBAC
  * Sistema de Usuários

#### Pré-condições

* Usuário autenticado com papel de administrador
* Sistema de RBAC deve estar operacional

#### Pós-condições

* Papéis de usuários podem ser alterados (por exemplo, tornar um usuário um produtor ou operador)
* Contas podem ser desativadas (sem excluir histórico)
* Associações User-Role são atualizadas

#### Fluxo Principal

1. Admin acessa área "Usuários"
2. Sistema exibe lista paginada de User com filtros (nome, e-mail, status, papel)
3. Admin seleciona um usuário para edição
4. Admin pode:
   - alterar status (ativo/inativo)
   - alterar papéis (Role), adicionando/removendo roles
   - visualizar informações básicas do usuário
5. Admin salva alterações
6. Sistema atualiza User e suas associações com Role (via UserRole)

#### Fluxo Principal (Converter em Produtor)

1. Admin seleciona usuário comum
2. Adiciona ROLE_PRODUCER ao usuário
3. (Opcional) Admin inicia fluxo de criação de EventProducer com dados fiscais (CPF/CNPJ, chave PIX etc.)
4. Sistema cria Producer vinculado ao User
5. Sistema habilita acesso ao painel do produtor

#### Fluxos Alternativos

* **4A. Converter usuário comum em produtor:**
  - Admin adiciona ROLE_PRODUCER ao usuário
  - (Opcional) Admin inicia fluxo de criação de EventProducer com dados fiscais
* **5A. Falha de validação (por exemplo, tentativa de remover último admin do sistema):**
  - Sistema bloqueia ação e exibe mensagem
* **4a. Desativar usuário:**
  - Admin marca status = inativo
  - Usuário não pode mais fazer login
  - Histórico é preservado

#### Exceções

| Código | Situação | Tratamento |
| --- | --- | --- |
| EXC-62 | Tentativa de remover último admin | Bloquear ação; exibir mensagem de segurança |
| EXC-63 | Falha ao atualizar papéis | Tentar novamente; notificar admin |
| EXC-64 | Usuário não encontrado | Exibir erro; atualizar lista |

#### Requisitos Relacionados

| Tipo | Código | Descrição |
| ---- | ------ | --------- |
| RF | RF48 | Painel Admin |
| RF | RF12 | Onboarding de Produtor (Admin) |
| RB | RB14 | RBAC por Papel |

---

### UC27 — Gerar relatórios de vendas por evento/lote/produto

#### Identificação

* **ID**: UC27
* **Nome**: Gerar relatórios de vendas por evento/lote/produto
* **Grupo**: G — Administração

#### Descrição Geral

Disponibilizar relatórios consolidados de vendas, incluindo ingressos e produtos extras, com filtros por evento, lote, produto e período.

#### Atores Envolvidos

* **Ator Principal**: Produtor, Administrador
* **Atores Secundários**:
  * Sistema de Relatórios
  * Sistema de Cache
  * Sistema de Exportação (CSV/Excel)

#### Pré-condições

* Usuário autenticado
* Produtor só enxerga seus próprios eventos
* Admin pode enxergar todos

#### Pós-condições

* Nenhuma mudança de estado necessária
* Relatórios são gerados e apresentados (ou exportados)
* Dados são carregados do cache quando possível

#### Fluxo Principal (Visão do Produtor)

1. Produtor acessa área "Relatórios / Vendas"
2. Seleciona um evento (ou todos os seus eventos)
3. (Opcional) informa filtros:
   - período (data inicial/final)
   - tipo (somente ingressos, somente produtos, ambos)
4. Sistema consulta:
   - Order com status PAID para aquele evento(s)
   - OrderItem relacionados
   - TicketLot e Product de referência
5. Sistema calcula agregados, por exemplo:
   - total bruto vendido por evento
   - total por lote de ingresso (TicketLot)
   - total por produto (Product)
   - quantidade de ingressos vendidos por tipo (inteira, meia, VIP)
   - uso de cupons (quantidade e valor de desconto)
6. Sistema exibe:
   - tabelas resumidas
   - gráficos (se implementado)
   - possibilidade de exportar CSV/Excel (opcional)

#### Fluxo Principal (Visão do Admin)

1. Admin acessa módulo de relatórios
2. Pode filtrar por:
   - produtor
   - evento
   - período
3. Resto do fluxo igual ao do produtor, mas com escopo global

#### Fluxo Principal (Exportar CSV)

1. Produtor/Admin gera relatório
2. Clica em "Exportar CSV"
3. Sistema gera arquivo CSV com dados do relatório
4. Sistema disponibiliza download do arquivo
5. (Opcional) Sistema envia arquivo por e-mail

#### Fluxos Alternativos

* **4A. Nenhum dado encontrado para os filtros:**
  - Sistema exibe mensagem "Nenhum resultado para o período selecionado"
* **3a. Filtrar por lote específico:**
  - Produtor seleciona lote específico
  - Sistema exibe vendas apenas daquele lote
* **3b. Filtrar por produto específico:**
  - Produtor seleciona produto específico
  - Sistema exibe vendas apenas daquele produto

#### Exceções

| Código | Situação | Tratamento |
| --- | --- | --- |
| EXC-65 | Falha ao gerar relatório | Tentar novamente; exibir mensagem de erro |
| EXC-66 | Falha na exportação CSV | Tentar novamente; notificar suporte |
| EXC-67 | Cache desatualizado | Forçar atualização dos dados |

#### Requisitos Relacionados

| Tipo | Código | Descrição |
| ---- | ------ | --------- |
| RF | RF14 | Painel do Produtor — somente leitura |
| RF | RF48 | Painel Admin |
| RNF | RNF15 | Cache |

---

## Conclusão

Este documento apresenta **27 casos de uso** organizados em **7 grupos funcionais**, cobrindo todo o ciclo de vida da plataforma Ingressou, desde autenticação até gestão administrativa. Os casos de uso foram elaborados com base na versão 1.6 dos Requisitos Elicitados, garantindo rastreabilidade completa aos requisitos funcionais (RF01-RF65) e regras de negócio.

### Principais Características

1. **Cobertura Completa**: Os 27 casos de uso cobrem todas as funcionalidades do MVP, incluindo:
   - Autenticação e gestão de perfis (Grupo A)
   - Criação e gestão de eventos, lotes e produtos (Grupo B)
   - Descoberta e visualização de eventos (Grupo C)
   - Processo completo de compra, pagamento e cupons (Grupo D)
   - Emissão, transferência e check-in de tickets (Grupo E)
   - Cashback e relatórios para produtores (Grupo F)
   - Gestão administrativa completa (Grupo G)

2. **Detalhamento Completo**: Cada caso de uso inclui:
   - Identificação clara (ID, nome, grupo)
   - Descrição geral e objetivo
   - Atores envolvidos (principal e secundários)
   - Pré-condições e pós-condições
   - Fluxo principal detalhado
   - Fluxos alternativos
   - Exceções e tratamentos
   - Rastreabilidade aos requisitos

3. **Rastreabilidade**: Todos os casos de uso são justificados por requisitos específicos, facilitando a manutenção e evolução do sistema.

4. **Base para Implementação**: Esta documentação servirá como base sólida para o desenvolvimento, testes e validação do sistema.

### Próximos Passos

Com esta modelagem concluída, o próximo passo é a implementação do sistema seguindo esta estrutura, garantindo que todos os casos de uso sejam suportados pela arquitetura e pela lógica de negócios.

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
| 1.0 | Expansão significativa dos casos de uso cobrindo todos os requisitos funcionais principais (RF01-RF52) | Gabriel Lima | 27/10/2025 |
| 2.0 | **Reestruturação completa**: (1) Organização em 7 grupos funcionais (A-G); (2) Expansão para 27 casos de uso (UC01-UC27) cobrindo todos os requisitos da versão 1.6; (3) Detalhamento completo de cada caso de uso com fluxos principais, alternativos e exceções; (4) Adição de casos de uso para produtos extras (UC08), gestão de localização (UC06), cashback (UC22-UC24), relatórios (UC27) e administração (UC25-UC26); (5) Atualização de atores do sistema; (6) Rastreabilidade completa aos requisitos RF01-RF65 | Gabriel Lima | 21/11/2025 |
