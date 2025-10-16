# Glossário – Projeto Ingressou

## Sumário
- [Introdução](#introdução)
- [Objetivos](#objetivos)
- [Metodologia](#metodologia)
- [Léxicos do tipo Sujeito](#léxicos-do-tipo-sujeito)
- [Léxicos do tipo Objeto](#léxicos-do-tipo-objeto)
- [Léxicos do tipo Verbo](#léxicos-do-tipo-verbo)
- [Léxicos do tipo Estado](#léxicos-do-tipo-estado)
- [Conclusão](#conclusão)
- [Bibliografia](#bibliografia)
- [Histórico de Versão](#histórico-de-versão)

---

## Introdução

O glossário, também chamado de **léxico**, é um artefato essencial na engenharia de requisitos. Ele tem como objetivo identificar e padronizar os termos técnicos, conceitos de negócio, siglas e expressões usadas ao longo do projeto **Ingressou** — uma plataforma moderna para compra e gestão de ingressos de eventos.  

Sua função principal é evitar ambiguidades e garantir que todos os membros da equipe compartilhem o mesmo entendimento sobre os conceitos envolvidos, desde usuários até desenvolvedores.

---

## Objetivos

- Padronizar o vocabulário técnico do projeto Ingressou;  
- Evitar interpretações diferentes sobre os mesmos termos;  
- Garantir consistência entre a equipe de desenvolvimento e stakeholders;  
- Criar uma base de referência para a documentação técnica e de requisitos.  

---

## Metodologia

A elaboração do glossário foi baseada na técnica **eLEL (Elaborated Lexicon Extended Language)**, conforme apresentada por Mohand et al. (2015).  

Os termos foram classificados em quatro categorias:
1. **Sujeito** – entidades que realizam ações;  
2. **Objeto** – elementos sobre os quais as ações são realizadas;  
3. **Verbo** – ações executadas pelos sujeitos;  
4. **Estado** – condições ou situações de objetos ou sujeitos.  

Cada termo é descrito por meio de cinco elementos:
- **Noção**  
- **Comportamento**  
- **Atributos**  
- **Métodos**  
- **Relações semânticas** (sinônimos e antônimos)  

---

## Léxicos do tipo Sujeito

<details>
<summary><b>📘 Tabela – Léxicos do tipo Sujeito</b></summary>

| Léxico | Noção | Comportamento | Atributos | Métodos | Sinônimos | Antônimos |
|---------|--------|----------------|-------------|-------------|-------------|-------------|
| Usuário | Pessoa que acessa e interage com a plataforma Ingressou | Realiza login, busca eventos, compra ingressos | Nome, e-mail, senha, histórico de compras | Cadastrar, autenticar, comprar | Cliente, participante | Visitante |
| Administrador | Responsável pela gestão da plataforma | Gerencia usuários, eventos e relatórios | Nome, cargo, permissões | Moderar, excluir, aprovar | Gestor, moderador | Usuário comum |
| Produtor | Responsável por cadastrar e administrar eventos | Cria eventos, define lotes e preços | Nome, CNPJ, eventos publicados | Publicar, editar, encerrar vendas | Organizador, promotor | Consumidor |
| Convidado | Visitante não autenticado | Visualiza páginas públicas e busca eventos | IP, histórico temporário | Navegar, pesquisar | Visitante | Membro registrado |
| Desenvolvedor | Responsável por manutenção e novas features | Corrige bugs e implementa melhorias | Nome, cargo, repositórios | Atualizar, corrigir, testar | Programador | Usuário final |

</details>

---

## Léxicos do tipo Objeto

<details>
<summary><b>🎟️ Tabela – Léxicos do tipo Objeto</b></summary>

| Léxico | Noção | Comportamento | Atributos | Métodos | Sinônimos | Antônimos |
|---------|--------|----------------|-------------|-------------|-------------|-------------|
| Evento | Representa uma atração cadastrada (show, peça, festa) | Pode ser criado, publicado e encerrado | Nome, data, local, preço, descrição | Criar, editar, publicar | Atração, espetáculo | Evento encerrado |
| Ingresso | Documento digital que dá acesso a um evento | Pode ser comprado, validado e transferido | Código QR, tipo, status | Comprar, validar, transferir | Ticket, bilhete | Cancelamento |
| Lote | Conjunto de ingressos com preço e data definidos | Determina disponibilidade e valor | Nome, quantidade, preço, validade | Criar, atualizar, encerrar | Faixa de venda | Lote esgotado |
| Carteira Digital | Repositório virtual de ingressos do usuário | Armazena e exibe ingressos comprados | ID do usuário, lista de ingressos | Acessar, exibir, excluir | Wallet, portfólio | Papel impresso |
| Relatório | Documento com métricas de vendas e acessos | Pode ser gerado e exportado | Tipo, data, métricas | Gerar, exportar | Documento, estatística | Dado bruto |

</details>

---

## Léxicos do tipo Verbo

<details>
<summary><b>⚙️ Tabela – Léxicos do tipo Verbo</b></summary>

| Léxico | Noção | Comportamento | Atributos | Métodos | Sinônimos | Antônimos |
|---------|--------|----------------|-------------|-------------|-------------|-------------|
| Cadastrar | Inserir novos dados ou eventos | O usuário fornece dados e confirma criação | Nome, e-mail, dados do evento | Validar, salvar | Registrar | Excluir |
| Comprar | Adquirir ingressos disponíveis | Escolher lote e pagar | Evento, forma de pagamento | Pagar, confirmar | Adquirir | Cancelar |
| Validar | Confirmar autenticidade do ingresso | Verifica código QR e status | ID, status | Escanear, autenticar | Conferir | Rejeitar |
| Pesquisar | Buscar eventos, produtores ou usuários | Inserir termos e aplicar filtros | Termo, categoria | Consultar, listar | Procurar | Ignorar |
| Publicar | Tornar evento visível ao público | Ativar evento após configuração | Evento, data de publicação | Ativar, divulgar | Lançar | Ocultar |

</details>

---

## Léxicos do tipo Estado

<details>
<summary><b>🔄 Tabela – Léxicos do tipo Estado</b></summary>

| Léxico | Noção | Comportamento | Atributos | Métodos | Sinônimos | Antônimos |
|---------|--------|----------------|-------------|-------------|-------------|-------------|
| Ativo | Estado de evento ou conta disponível | Indica que o item está habilitado | Status, data de ativação | Habilitar, exibir | Disponível | Inativo |
| Esgotado | Lote sem ingressos disponíveis | Impede novas compras | Quantidade, data | Encerrar, atualizar | Finalizado | Disponível |
| Cancelado | Evento ou compra anulada | Remove acesso e reembolsa | Motivo, data | Cancelar, reembolsar | Anulado | Confirmado |
| Pendente | Aguardando confirmação de ação | Espera pagamento ou aprovação | Status, data de criação | Aprovar, rejeitar | Em análise | Concluído |
| Concluído | Evento ou ação finalizada com sucesso | Permite acesso ao histórico | Data, resultado | Arquivar, exibir | Finalizado | Em andamento |

</details>

---

## Conclusão

A criação deste glossário do **projeto Ingressou** contribui para o alinhamento semântico entre todos os envolvidos no desenvolvimento.  
Ele serve como referência para analistas, desenvolvedores e stakeholders, assegurando que os termos técnicos e de negócio mantenham um significado único e padronizado ao longo de todo o ciclo de vida do projeto.

---

## Bibliografia

<a name="ref1"></a>  
MOHAND, Ounsa R. et al. **Elaborate Lexicon Extended Language with a Lot of Conceptual Information.** *International Journal of Computer Science, Engineering and Applications (IJCSEA)*, v. 5, n. 6, p. 1–18, dez. 2015.

<a name="ref2"></a>  
VAZQUEZ, Carlos Eduardo; SIMÕES, Guilherme Siqueira. **Engenharia de Requisitos: Software Orientado ao Negócio.** Rio de Janeiro: Brasport, 2016.

---

## Histórico de Versão

| Versão | Alteração | Responsável | Data |
|--------|------------|--------------|------|
| 1.0 | Criação do documento do glossário | Gabriel Lima | 16/10/2025 |
| 1.1 | Adição das tabelas de Sujeito e Objeto | Gabriel Lima | 16/10/2025 |
| 1.2 | Inclusão das tabelas de Verbo e Estado | Gabriel Lima | 16/10/2025 |
| 1.3 | Revisão final e adaptação ao padrão MkDocs | Gabriel Lima | 16/10/2025 |
