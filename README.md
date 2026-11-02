# Nuclear Akinator - IoT e Redes - Sprint 1

## Equipe

- Caio Cantini Couto - RM 563452
- Guilherme Pinto Eustáquio - RM 566784
- Matheus Tavares - RM 566844

Conferir o cadastro oficial do grupo antes do envio.

## Proposta

Controle físico de respostas para o jogo educativo Nuclear Akinator em exposições e salas de aula. O visitante usa três botões (Sim, Não, Não sei), e a tela apresenta perguntas, palpite, confirmação e explicação científica. A proposta é conceitual, como permite o enunciado; não há firmware ou hardware implementado neste pacote.

## Tecnologias e componentes previstos

ESP32; três botões; LED de estado; fonte USB e caixa; Wi-Fi 2,4 GHz; MQTT 5/TLS com QoS 1; broker Mosquitto; gateway; serviço de partidas; catálogo Java; Oracle; monitor ou tablet com interface web. Botões capturam a interação. Não se propõe medir radiação.

## Caminho dos dados

![Fluxograma](diagramas/Fluxograma_IoT.png)

1. ESP32 recebe a pergunta ativa do gateway e habilita os botões.
2. Botão captura a escolha; firmware aplica debounce e publica JSON no broker.
3. Gateway valida sessão, pergunta, terminal e evento; duplicatas recebem o mesmo aceite.
4. Serviço de partidas registra Resposta, atualiza candidatos e apresenta palpite.
5. Visitante confirma ou corrige o objeto; a explicação vem do catálogo desse objeto confirmado.
6. LED acusa aceite somente depois da persistência. Em queda de rede, o controle pausa.

Tópico previsto: `nuclear-akinator/terminais/T01/respostas`, sem retain.

```json
{"eventoId":"T01-00042","partidaId":1,"perguntaId":3,"valor":"I","terminalId":"T01"}
```

Cache persistente de eventos, autenticação dos terminais e serviço de jogo são componentes futuros. Não fazem parte do banco acadêmico de cinco entidades. O Java existente implementa catálogo de objetos em H2, não o fluxo IoT. .NET poderá assumir Partida/Resposta, sujeito a alinhamento do grupo.

## IoB e IA generativa

Analisar perguntas com respostas Não sei e abandono de partidas para melhorar a interação. Não interpretar esses dados isolados como prova de aprendizagem. IA generativa é opcional para apoiar rascunhos revisados; a explicação exibida permanece previamente validada.

## Arquivos

- `Proposta_IoT_Redes.pdf`: documento completo.
- `diagramas/`: fluxograma em PDF vetorial e PNG.
- `ROTEIRO_VIDEO.md`: narração e plano visual de aproximadamente cinco minutos.
- `LINKS_ENTREGA.txt`: preencher com YouTube não listado e GitHub público dos materiais.
- `Proposta_Editavel.md`: texto para revisão pelo grupo.

## Entrega

Publicar estes materiais no GitHub escolhido pelo grupo e gravar o vídeo. Preencher os dois links reais, remover as indicações de pendência e gerar novamente o ZIP. A consulta ao repositório Java não publica estes arquivos nem cria um repositório para esta disciplina. O ZIP fornecido é uma base de preparação e permanece pendente desses links.

## Referências

- FIAP: `2TDS Agosto - Marinha 2026 - 1º Semestre V2 (1).pdf`, fornecido pela equipe. IoT: páginas 29-32; BD: páginas 37-40.
- Equipe: `Nuclear_Akinator_Projeto.pdf` e `Nuclear_Akinator_Sprint_1_Com_Personagem.pdf`.
- Java analisado: https://github.com/caioccouto/Nuclear-Akinator/tree/fa3fa1457519b55665c33088cf68fb1a11001069
- Oracle CREATE TABLE: https://docs.oracle.com/en/database/oracle/oracle-database/19/sqlrf/CREATE-TABLE.html
- Oracle CREATE SEQUENCE: https://docs.oracle.com/en/database/oracle/oracle-database/19/sqlrf/CREATE-SEQUENCE.html
- Oracle Data Modeler / Barker: https://docs.oracle.com/en/database/oracle/sql-developer-data-modeler/19.2/dmdug/data-modeler-concepts-usage.html
- MQTT 5.0 / OASIS: https://docs.oasis-open.org/mqtt/mqtt/v5.0/mqtt-v5.0.html

Consulta: 02/11/2026. O texto científico de demonstração provém dos documentos da equipe e deverá passar por revisão com fontes específicas antes de uso público.
