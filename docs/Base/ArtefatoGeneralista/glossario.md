## Glossário

## Sumário

- [Introdução](#Introdução)
- [Objetivos](#Objetivos)
- [Metodologia](#Metodologia)
- [Léxicos do tipo Sujeito](#Léxicos-do-tipo-Sujeito)
- [Léxicos do tipo Objeto](#Léxicos-do-tipo-Objeto)
- [Léxicos do tipo Verbo](#Léxicos-do-tipo-Verbo)
- [Léxicos do tipo Estado](#Léxicos-do-tipo-Estado)
- [Conclusão](#Conclusão)
- [Bibliografia](#Bibliografia)
- [Histórico de versão](#Histórico-de-versão)

## Introdução

Segundo o livro “Engenharia de Requisitos: Software orientado a negócio” [2](#ref2), o glossário, também chamado de léxico, tem como principal função identificar, registrar e padronizar os termos técnicos, conceitos do negócio, sinônimos e siglas utilizados ao longo do desenvolvimento de um projeto. Com isso, é uma ferramenta de gestão do conhecimento que contribui para a clareza na comunicação entre os envolvidos ao evitar  ambiguidade e interpretações divergentes sobre os mesmos termos.

Ele é importante porque é comum que determinadas palavras assumam diferentes significados dependendo do contexto ou da área de atuação. Como foi evidenciado no capítulo 7 do livro  [1](#ref1), em projetos de software, essa multiplicidade de sentidos pode comprometer a compreensão dos requisitos. Dessa forma, o glossário assume um papel recurso prático para consulta.

## Objetivos

O principal objetivo deste glossário é padronizar e tornar claro o vocabulário utilizado no projeto **Galáxia Conectada**. Portanto, busca prevenir ambiguidades,e garantir consistência na documentação.


## Metodologia

A metodologia adotada para a construção deste glossário baseou-se na abordagem apresentada no artigo "Elaborate Lexicon Extended Language with a Lot of Conceptual Information" (IJCSEA, 2015) [1](#ref1), que propõe uma estrutura detalhada chamada eLEL (Elaborated Lexicon Extended Language). De acordo com essa abordagem, os termos são classificados em quatro tipos — **sujeito, objeto, verbo e estado** — e são descritos por meio de cinco elementos principais: noção, comportamento, atributos e métodos.

 A tabela 1 foi elaborada com base nos tipos definidos.

<center>
Tabela 1: Os tipos de léxicos

| Tipo    | Definição                                                                 | Exemplo                       |
|---------|---------------------------------------------------------------------------|-------------------------------|
| Sujeito | Entidade ativa que executa ações e interage com outros elementos.         | Usuário, Sistema              |
| Objeto  | Entidade passiva manipulada por um sujeito.                               | Artigo, Comentário, Jogo      |
| Verbo   | Ação realizada por um sujeito sobre um objeto ou funcionalidade do sistema.| Cadastrar, Visualizar, Compartilhar |
| Estado  | Condição em que um objeto ou sujeito pode se encontrar.                   | Logado, Em edição, Publicado  |

<b> Autora: </b> <a href="https://github.com/SkywalkerSupreme">Larissa Stéfane</a>.

</center>

Ainda com base em "Elaborate Lexicon Extended Language with a Lot of Conceptual Information" (IJCSEA, 2015) [1](#ref1), a tabela 2 mostra como os elementos devem ser descritos.

<center>
Tabela 2: Os tipos 5 elementos principais.

| Tipo    | Noção                                                                                              | Comportamento                                                                                     | Atributos                                                                                          | Métodos                                                                                         |
|---------|----------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------|
| Sujeito | Entidade ativa do sistema, como uma pessoa ou componente que executa ações.                        | O que o sujeito faz? Quais objetos ele manipula?                                                  | Características como nome, tipo, código etc.                                                       | Operações que o sujeito pode realizar, especialmente sobre seus atributos ou objetos relacionados. |
| Objeto  | Entidade passiva manipulada por um sujeito.                                                        | Quais ações o objeto recebe? Quais outros objetos se relacionam com ele?                          | Nome, tipo, descrição, código e outros dados que o caracterizam.                                   | Ações para acessar, alterar ou excluir o objeto.                                                |
| Verbo   | Ação executada por um sujeito, impactando objetos ou o sistema.                                    | Quem executa a ação? Em qual objeto? Qual o objetivo ou finalidade?                               | Sujeitos ou objetos afetados pela ação.                                                            | Procedimentos necessários para realizar a ação.                                                  |
| Estado  | Situação em que um elemento do sistema se encontra em determinado momento.                         | Como esse estado é alcançado? Que ações o provocam?                                               | Informações que definem o estado (ex: nome do estado, descrição).                                 | Ações ou condições que geram ou modificam o estado.                                              |

<b> Autora: </b> <a href="https://github.com/SkywalkerSupreme">Larissa Stéfane</a>.

</center>

Com base nisso, os léxicos serão apresentados em tabela no seguinte estilo:

<center>
Tabela 3: Estrutura das tabelas

| Léxico      | Noção                                                      | Comportamento                                              | Atributos                              | Métodos                                 | Sinônimos       | Antônimos        |
|-------------|-------------------------------------------------------------|-------------------------------------------------------------|-----------------------------------------|------------------------------------------|------------------|-------------------|
| Exemplo 1   | Descreve o que o termo representa no contexto do projeto.   | Explica como o termo age ou reage no sistema.              | Lista de características associadas.   | Ações ou operações realizadas.           | Termo similar    | Termo oposto      |

<b> Autora: </b> <a href="https://github.com/SkywalkerSupreme">Larissa Stéfane</a>.

</center>

**Observação:** Para deixar mais completos foram adicionados os sinônimos e os antônimos.

## Léxicos do tipo Sujeito


<details>
  <summary size="20"><b> Léxicos do tipo Sujeito </b></summary> 
 
<center>
 
Tabela 4: Léxicos do tipo Sujeito

| Léxico           | Noção                                                                 | Comportamento                                                            | Atributos                                   | Métodos                                                         | Sinônimos         | Antônimos         |
|------------------|------------------------------------------------------------------------|---------------------------------------------------------------------------|----------------------------------------------|------------------------------------------------------------------|--------------------|--------------------|
| Usuário          | Pessoa que acessa e interage com a plataforma                         | Realiza login, consome conteúdo, participa de fóruns e jogos             | Nome, e-mail, tipo de usuário, preferências  | Cadastrar, acessar, comentar, jogar, avaliar                     | Participante       | Visitante anônimo  |
| Administrador    | Responsável pela gestão e moderação da plataforma                     | Modera fóruns, gerencia usuários e conteúdo                              | Nome, cargo, permissões                      | Aprovar conteúdo, excluir comentários, gerenciar acessos         | Moderador          | Usuário comum      |
| Convidado        | Pessoa que acessa a plataforma sem cadastro                           | Visualiza conteúdos públicos, não interage ativamente                    | Endereço IP, localização                     | Navegar, assistir, pesquisar                                     | Visitante          | Membro registrado  |
| Aluno            | Usuário com trilha de aprendizado ativa                               | Estuda conteúdos, realiza testes e interage com jogos                    | Nome, progresso, nível de conhecimento       | Aprender, jogar, participar de atividades                        | Estudante          | Professor          |
| Professor        | Usuário que compartilha conteúdo e responde dúvidas                   | Publica artigos, propõe atividades, responde perguntas                   | Nome, área de atuação, histórico de postagens| Ensinar, comentar, publicar, responder dúvidas                   | Educador           | Aluno              |
| Curador          | Usuário com permissão para revisar e organizar conteúdos              | Analisa artigos, atualiza seções da plataforma                           | Nome, seções gerenciadas                    | Editar, classificar, reordenar                                   | Editor             | Leitor             |
| Desenvolvedor    | Profissional responsável pelo código e manutenção da plataforma       | Corrige bugs, implementa novas funcionalidades                           | Nome, linguagem usada, histórico de commits  | Atualizar sistema, corrigir erros                                | Programador        | Usuário final      |
| Pesquisador      | Usuário voltado à análise de dados ou produção científica             | Consulta dados, contribui com estudos e relatórios                       | Nome, instituição, temas de interesse        | Pesquisar, publicar, citar                                      | Cientista          | Leigo              |
| Astrônomo        | Especialista em astronomia que contribui com conteúdo técnico         | Publica eventos astronômicos, artigos científicos                        | Nome, especialização, observatórios associados| Informar eventos, responder questões                             | Especialista       | Iniciante          |
| Mediador         | Usuário que facilita interações nos fóruns e eventos ao vivo          | Modera discussões, estimula engajamento                                  | Nome, eventos associados, reputação          | Interagir, moderar, incentivar participação                      | Facilitador        | Provocador         |
| Colaborador      | Pessoa que contribui com conteúdos ou sugestões pontuais              | Envia materiais, sugere melhorias ou participa de testes beta            | Nome, tipo de contribuição, histórico        | Sugerir, contribuir, revisar                                     | Voluntário         | Omissor            |
| Responsável legal| Pessoa que gerencia a conta de um usuário menor de idade              | Controla permissões e monitora atividades                                | Nome, relação com o usuário, e-mail          | Autorizar acesso, acompanhar atividades                          | Tutor              | Desresponsabilizado|


<b> Autora: </b> <a href="https://github.com/SkywalkerSupreme">Larissa Stéfane</a>.

</center>

</details>

## Léxicos do tipo Objeto

<details>
  <summary size="20"><b> Léxicos do tipo Objeto </b></summary> 
 
<center>
 
Tabela 5: Léxicos do tipo Objeto

| Léxico               | Noção                                                                 | Comportamento                                                     | Atributos                                         | Métodos                                                     | Sinônimos              | Antônimos             |
|----------------------|------------------------------------------------------------------------|--------------------------------------------------------------------|----------------------------------------------------|--------------------------------------------------------------|-------------------------|------------------------|
| Artigo               | Texto publicado com conteúdo educativo sobre astronomia               | Pode ser lido, comentado, avaliado e compartilhado                | Título, autor, data, conteúdo, tags                | Ler, comentar, compartilhar, avaliar                         | Publicação, conteúdo    | Comentário             |
| Jogo educativo       | Atividade lúdica com fins pedagógicos                                 | Pode ser jogado, pontuado e reiniciado                            | Nome, tipo, pontuação, nível de dificuldade        | Jogar, repetir, pontuar                                     | Desafio, quiz           | Teoria, leitura        |
| Fórum                | Espaço de discussão entre usuários                                    | Recebe tópicos, respostas e moderação                             | Título, categoria, autor, número de respostas      | Criar tópico, responder, moderar                             | Comunidade, discussão   | Página estática        |
| Evento astronômico   | Ocorrência científica programada (eclipses, chuvas de meteoros etc.)  | Pode ser divulgado, agendado e comentado                          | Nome, data, local, tipo de evento                  | Divulgar, agendar, notificar                                | Fenômeno                | Rotina, inatividade    |
| Trilhas de aprendizado| Sequência estruturada de conteúdos                                    | Podem ser iniciadas, pausadas ou concluídas                       | Nome, etapas, progresso, status                     | Iniciar, continuar, finalizar                                | Caminho, curso          | Sessão única           |
| Perfil de usuário     | Página com dados e atividades de um usuário                         | Pode ser editado, visualizado e excluído                          | Nome, imagem, bio, nível, conquistas               | Editar, atualizar, excluir                                  | Conta, cadastro         | Visitante              |
| Comentário            | Resposta curta a conteúdos ou interações                            | Pode ser postado, curtido ou removido                             | Autor, conteúdo, data                              | Comentar, apagar, curtir                                    | Observação, feedback    | Publicação principal   |
| Notificação           | Alerta informativo para o usuário                                   | Pode ser visualizada, lida ou arquivada                           | Mensagem, tipo, data                               | Enviar, arquivar, alertar                                   | Alerta, aviso           | Silêncio, ausência     |
| Tutorial              | Guia passo a passo sobre determinado tema                           | Pode ser iniciado, pausado e seguido                              | Título, passos, categoria                           | Acessar, seguir, concluir                                   | Manual, instrução       | Dúvida, confusão        |
| Recompensa            | Prêmio virtual oferecido por desempenho                             | Pode ser acumulada, trocada ou exibida                            | Nome, valor, tipo, condição de obtenção            | Ganhar, trocar, exibir                                      | Troféu, medalha         | Penalidade, perda      |
| Avaliação             | Pontuação ou feedback dado a conteúdos                              | Pode ser enviada, modificada ou excluída                          | Nota, comentário, autor                            | Avaliar, revisar, excluir                                  | Feedback, nota          | Ignorar, omitir        |
| Estatística           | Dados gerados pelas interações dos usuários                         | Pode ser analisada, exportada e atualizada                        | Tipo de dado, valor, período                        | Visualizar, exportar, atualizar                             | Métrica, relatório      | Intuição, achismo      |
| Dica astronômica      | Informação curta sobre curiosidades ou boas práticas                | Pode ser exibida aleatoriamente                                   | Texto, fonte, categoria                             | Exibir, salvar, compartilhar                                | Curiosidade, sugestão   | Erro, fake news        |
| Relatório             | Documento com resumo analítico das atividades                       | Pode ser gerado, baixado e impresso                               | Título, autor, período, dados                      | Gerar, exportar, imprimir                                  | Documento, resumo       | Fragmento, rascunho    |
| Pesquisa              | Recurso para busca de conteúdo dentro da plataforma                 | Pode ser realizada por palavra-chave ou categoria                 | Palavras-chave, filtros, data                      | Pesquisar, filtrar, refinar                                 | Busca, consulta         | Navegação cega         |
| Feedback              | Opinião enviada sobre funcionalidades da plataforma                 | Pode ser enviada e respondida                                     | Usuário, comentário, data                          | Enviar, responder                                           | Opinião, sugestão       | Indiferença, descaso   |
| Agenda                | Interface para controle de eventos e trilhas                        | Pode ser personalizada e sincronizada                             | Datas, horários, lembretes                         | Agendar, editar, notificar                                  | Calendário              | Improviso              |
| Enquete               | Instrumento para consulta rápida de opinião                         | Pode ser respondida, encerrada e analisada                        | Pergunta, opções, resultados                       | Responder, encerrar, visualizar resultados                  | Votação, pesquisa       | Ordem direta           |
| Banner                | Imagem de destaque usada na divulgação de conteúdo                  | Pode ser clicado, fechado ou compartilhado                        | Imagem, link, texto                                | Exibir, redirecionar, fechar                                | Anúncio, destaque       | Texto simples          |
| Mapa celeste          | Visualização do céu em tempo real                                   | Pode ser explorado, ampliado e rotacionado                        | Constelações, coordenadas, hora                    | Navegar, interagir, filtrar                                 | Carta celeste           | Lista textual          |
| Glossário             | Conjunto de definições de termos usados na plataforma               | Pode ser consultado e expandido                                   | Termo, definição, categoria                         | Consultar, atualizar                                       | Léxico, vocabulário     | Gíria, ambiguidade     |
| Biblioteca virtual    | Coleção de recursos digitais como e-books e PDFs                   | Pode ser acessada, organizada e baixada                           | Títulos, autores, formatos                          | Ler, baixar, organizar                                     | Acervo, repositório     | Vazio, desorganização  |
| Nível de usuário      | Indica progresso e engajamento do participante                      | Pode ser aumentado conforme as ações                              | Nome, pontuação, badges                            | Subir, exibir, comparar                                    | Ranking, patamar        | Estagnação             |
| Conquista             | Reconhecimento simbólico por ações realizadas                      | Pode ser desbloqueada e compartilhada                             | Nome, categoria, ícone                             | Desbloquear, exibir, compartilhar                          | Medalha, troféu         | Falha, punição         |

<b> Autora: </b> <a href="https://github.com/SkywalkerSupreme">Larissa Stéfane</a>.

</center>

</details>


## Léxicos do tipo Verbo

<details>
  <summary size="20"><b> Léxicos do tipo Verbo </b></summary> 
 
<center>
 
Tabela 6: Léxicos do tipo Verbo

| Léxico         | Noção                                                                 | Comportamento                                                                 | Atributos                       | Métodos                                                   | Sinônimos         | Antônimos         |
|----------------|------------------------------------------------------------------------|--------------------------------------------------------------------------------|----------------------------------|------------------------------------------------------------|--------------------|--------------------|
| Acessar        | Entrar em uma área da plataforma com login                             | O usuário fornece dados para autenticação                                      | Usuário, senha, permissão        | Inserir login e senha, clicar em "Entrar"                   | Entrar             | Sair               |
| Cadastrar      | Inserir novos dados ou registros na plataforma                         | O usuário fornece dados para criar uma conta ou conteúdo                      | Nome, e-mail, senha, tipo         | Preencher formulário e confirmar criação                    | Registrar          | Excluir            |
| Editar         | Modificar informações ou conteúdos existentes                          | O usuário altera textos ou dados previamente inseridos                        | Campos editáveis                 | Abrir item, modificar campos e salvar                       | Modificar          | Congelar           |
| Excluir        | Remover definitivamente dados ou conteúdos                             | O usuário seleciona e confirma a remoção de um item                           | ID, nome                         | Selecionar item, clicar em "Excluir" e confirmar            | Remover            | Restaurar          |
| Pesquisar      | Procurar informações específicas na plataforma                         | O usuário digita palavras-chave e recebe resultados relacionados              | Termo de busca, filtros           | Digitar no campo de busca e aplicar filtros                 | Consultar          | Ignorar            |
| Navegar        | Percorrer menus, páginas e conteúdos                                   | O usuário interage com a interface para acessar diferentes seções             | Menus, links, abas                | Clicar em menus e navegar por páginas                       | Explorar           | Abandonar          |
| Comentar       | Registrar uma opinião ou pergunta sobre um conteúdo                   | O usuário escreve e publica um comentário                                     | Texto, autor, data                | Escrever mensagem e clicar em "Publicar"                    | Opinar             | Silenciar          |
| Curtir         | Demonstrar aprovação ou interesse por um conteúdo                     | O usuário clica em um botão para indicar que gostou de algo                   | Nome do item, número de curtidas  | Clicar no ícone de "curtir"                                 | Apreciar           | Descurtir          |
| Compartilhar   | Enviar conteúdo a outras pessoas ou plataformas                       | O usuário gera um link ou envia o conteúdo diretamente                        | Link, redes sociais               | Clicar em "Compartilhar" e escolher destino                 | Divulgar           | Reter              |
| Assistir       | Consumir conteúdos em vídeo ou animação                               | O usuário clica para visualizar um conteúdo audiovisual                       | Vídeo, tempo, título              | Clicar em "Play", pausar, ajustar volume                    | Ver                | Ignorar            |
| Jogar          | Participar de jogos interativos e educativos                          | O usuário inicia e interage com elementos do jogo                             | Nome do jogo, pontuação           | Iniciar jogo, realizar ações, completar desafios            | Participar         | Desistir           |
| Aprender       | Adquirir conhecimento por meio de trilhas ou conteúdos                | O usuário segue trilhas, lê materiais e realiza atividades                    | Conteúdo, progresso, tema         | Ler, assistir, responder e revisar                          | Estudar            | Esquecer           |
| Avaliar        | Atribuir nota ou opinião sobre um conteúdo                            | O usuário escolhe uma pontuação ou comenta sobre sua experiência              | Nota, estrelas, feedback          | Selecionar nota e/ou deixar comentário                      | Classificar        | Omitir             |
| Agendar        | Marcar eventos no calendário pessoal                                  | O usuário seleciona data e hora para acompanhar um evento                     | Evento, data, horário             | Escolher evento, clicar em "Agendar"                       | Marcar             | Cancelar           |
| Participar     | Engajar-se em fóruns, eventos ou jogos                                | O usuário contribui com mensagens ou ações em tempo real                      | Fórum, evento, usuário            | Confirmar presença, interagir com outros participantes      | Colaborar          | Ausentar-se        |
| Notificar      | Informar o usuário sobre algo novo ou importante                      | O sistema exibe alertas sobre atualizações, mensagens ou eventos              | Título, conteúdo, prioridade      | Apresentar mensagem, emitir alerta sonoro ou visual         | Alertar            | Omitir             |
| Filtrar        | Selecionar dados com base em critérios específicos                    | O usuário restringe resultados de busca ou listagens                          | Parâmetros, categorias            | Selecionar filtros e aplicar visualização                   | Selecionar         | Ampliar            |
| Salvar         | Armazenar conteúdo ou informações para uso posterior                  | O usuário registra dados criados ou editados                                  | Conteúdo, local de armazenamento  | Clicar em "Salvar" após criação ou edição                   | Gravar             | Descartar          |

<b> Autora: </b> <a href="https://github.com/SkywalkerSupreme">Larissa Stéfane</a>.

</center>

</details>

## Léxicos do tipo Estado

<details>
  <summary size="20"><b> Léxicos do tipo Estado </b></summary> 
 
<center>
Tabela 7:  Léxicos do tipo Estado

| Léxico                  | Noção                                                                 | Comportamento                                                | Atributos                               | Métodos                                                  | Sinônimos           | Antônimos          |
|-------------------------|-----------------------------------------------------------------------|---------------------------------------------------------------|------------------------------------------|-----------------------------------------------------------|----------------------|---------------------|
| Conectado               | Estado em que o usuário está ativo e logado                          | Permite interações em tempo real                              | Tempo de conexão, status de sessão       | Iniciar sessão, interagir                                 | Online               | Desconectado        |
| Em progresso            | Situação de uma trilha ou atividade que foi iniciada, mas não finalizada | Indica continuidade ou pausa de ações                         | Nome da trilha, etapa atual              | Continuar, pausar, revisar                                | Em andamento         | Concluído           |
| Concluído               | Estado de término de uma ação ou atividade                           | Permite acesso ao resultado ou revisão                        | Nome da atividade, data de conclusão     | Revisar, compartilhar, gerar relatório                    | Finalizado           | Incompleto          |
| Notificado              | Situação de um usuário que recebeu uma notificação                   | Indica que uma nova informação foi entregue                   | Tipo de notificação, data                | Ler, arquivar                                            | Informado            | Ignorado            |
| Aguardando resposta     | Estado de uma pergunta, tópico ou feedback que ainda não teve retorno| Mostra pendência e necessidade de interação                   | Tempo de espera, autor original          | Responder, encaminhar                                    | Pendente             | Respondido          |
| Lido                    | Situação de um conteúdo já acessado pelo usuário                     | Indica que a informação foi consumida                         | Nome do conteúdo, data de leitura        | Marcar como lido, arquivar                                | Visualizado          | Não lido            |
| Sincronizado            | Estado em que dados locais e online estão atualizados                | Garante consistência e integridade da informação              | Fonte, data da última atualização        | Atualizar, confirmar sincronização                        | Atualizado           | Desatualizado       |
| Em destaque             | Situação de conteúdo priorizado na plataforma                        | Ganha mais visibilidade e engajamento                         | Título, tipo de destaque, validade       | Destacar, remover destaque                                | Evidenciado          | Oculto              |

<b> Autora: </b> <a href="https://github.com/SkywalkerSupreme">Larissa Stéfane</a>.

</center>

</details>

## Conclusão

A elaboração do glossário léxico para o projeto possibilitou um alinhamento da compreensão dos termos e das suas funções. 

## Bibliografia

<a name="ref1"></a>  
[1] MOHAND, Ounsa R. et al. **Elaborate Lexicon Extended Language with a Lot of Conceptual Information**. International Journal of Computer Science, Engineering and Applications (IJCSEA), v. 5, n. 6, p. 1–18, dez. 2015. Acessado em: 9 abr. 2025.

<a name="ref2"></a>  
[2] VAZQUEZ, Carlos Eduardo; SIMÕES, Guilherme Siqueira. **Engenharia de Requisitos: Software Orientado ao Negócio**. Rio de Janeiro: Brasport, 2016. Acessado em: 9 abr. 2025.
 
## Histórico de versão

| Versão | Alteração | Responsável | Data |
| - | - | - | - |
| 1.0 | Elaboração do documento| Larissa Stéfane | 09/04/2024 |
| 1.1 | Adicionar tabelas do tipo Sujetio e Objeto| Larissa Stéfane | 09/04/2024 |
| 1.2 | Adicionar tabelas de verbo e estado | Larissa Stéfane | 10/04/2024 |
| 1.3 | Colapsar tabelas | Larissa Stéfane | 11/04/2024 |
