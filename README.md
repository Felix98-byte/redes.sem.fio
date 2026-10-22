# Blocos básicos do Node-RED

Exercício prático: um flow com seis linhas independentes (cada uma vai de um `inject` até um `debug`), na aba **Blocos básicos**. Usa só nós nativos do Node-RED.

Arquivo do flow: [`blocos-basicos-do-node-red.json`](blocos-basicos-do-node-red.json)

## Como importar

1. Abra o Node-RED em <http://localhost:1880>.
2. Menu (☰) → **Import** → **select a file to import** → escolha o `.json` → **Import**.
3. Clique em **Deploy**, abra a aba **debug** e clique no botão de cada `inject`.

## Atividades e saídas esperadas

| # | Nó | Entrada (inject) | Saída esperada (debug) |
|---|----|------------------|------------------------|
| 1 | function | número `7` | `{"original":7,"dobro":14,"par":false}` |
| 2 | change | `{"nome":"Ana","idade":20}` | mensagem completa com `topic: "cadastro"` e `payload: {"nome":"Ana","status":"ativo"}` |
| 3 | switch | `temperatura` 32 e 22 | 32 → saída 1 (ALERTA); 22 → saída 2 (normal) |
| 4 | template | `{"nome":"Ana","nota":9.5}` | `Aluno(a) Ana tirou nota 9.5.` |
| 5 | split + function + join | `["ana","bruno","carla"]` | `["ANA","BRUNO","CARLA"]` |
| 6 | delay | string `agora` | a mesma mensagem, 2 s depois do clique |

## Como cada atividade foi feita

1. **function**: devolve `{original, dobro, par}` a partir de `msg.payload`.
2. **change**: três regras, sem JavaScript: *set* `msg.topic`, *set* `msg.payload.status`, *delete* `msg.payload.idade`.
3. **switch**: testa `msg.payload.temperatura`; regra 1 `>= 30`, regra 2 `otherwise`; para na primeira regra que casar.
4. **template**: mustache `Aluno(a) {{payload.nome}} tirou nota {{payload.nota}}.`, com saída em string.
5. **split → function → join**: o join em modo *automatic* usa `msg.parts` para remontar a lista na ordem original.
6. **delay**: *Delay each message* por 2 segundos; o payload não é alterado.
