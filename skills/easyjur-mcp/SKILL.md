---
name: easyjur-mcp
description: Skill da REST API do EasyJur na MCP.AI: 41 endpoints em /api/easyjur. Wrapper da API oficial do EasyJur (gestão jurídica): processos (e partes, pedidos, financeiros, documentos, mensagens), pessoas, agenda, oportunidades, timesheet, financeiro (receitas/despesas), grupos e usuários. Leitura + criação de processos, pessoas, agenda e oportunidades. Autenticação por token de API do escritório. Autentique com workspace API key (sk_live) gerada em app.mcp.ai/settings/api-keys. Use quando o usuário pedir algo coberto pelos endpoints.
---

# EasyJur — REST API skill

Você tem acesso à **EasyJur** REST API na MCP.AI.

> Wrapper da API oficial do EasyJur (gestão jurídica): processos (e partes, pedidos, financeiros, documentos, mensagens), pessoas, agenda, oportunidades, timesheet, financeiro (receitas/despesas), grupos e usuários. Leitura + criação de processos, pessoas, agenda e oportunidades. Autenticação por token de API do escritório.

## Base URL

```
https://api.mcp.ai/api/easyjur
```

Todo endpoint é um **POST** na Base URL + o path abaixo. Os parâmetros vão no corpo JSON.

## Autenticação

Inclua em toda request:

```
Authorization: Bearer sk_live_...
Content-Type: application/json
```

> Gere sua chave em **https://app.mcp.ai/settings/api-keys** (workspace API key `sk_live_…`, não expira, revogável). Uma única chave serve pra todos os seus MCPs.

## Formato de resposta

```json
{ "ok": true, "tool": "<tool_id>", "result": <payload> }
```

## Exemplo cURL

```bash
curl -X POST https://api.mcp.ai/api/easyjur/agenda/comentarios \
  -H "Authorization: Bearer sk_live_..." \
  -H "Content-Type: application/json" \
  -d '{"id_agenda":"..."}'
```

## Reportar problemas

Se um endpoint retornar erro, vazio ou dado inesperado, reporte (não desista calado): **POST /api/easyjur/report** com `{ "message": "...", "context"?: "...", "conversation"?: [...] }`. Isso notifica o time da MCP.AI.

## Endpoints (41)

#### `easyjur_agenda_comentarios`

Comentários de um item de agenda. _(POST /api/easyjur/agenda/comentarios)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `id_agenda` | string | Sim | Path: id_agenda |
| `query` | object | Não | Parâmetros de query adicionais conforme a API oficial do EasyJur. |

#### `easyjur_agenda_envolvidos`

Envolvidos em um item de agenda. _(POST /api/easyjur/agenda/envolvidos)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `agenda_id` | string | Sim | Path: agenda_id |
| `query` | object | Não | Parâmetros de query adicionais conforme a API oficial do EasyJur. |
| `agenda_ids` | string[] | Não | Bulk mode: multiple values for agenda_id |

#### `easyjur_agenda_etapas`

Etapas de workflow de um item de agenda. _(POST /api/easyjur/agenda/etapas)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `agenda_id` | string | Sim | Path: agenda_id |
| `query` | object | Não | Parâmetros de query adicionais conforme a API oficial do EasyJur. |
| `agenda_ids` | string[] | Não | Bulk mode: multiple values for agenda_id |

#### `easyjur_api_status`

Status da API EasyJur do escritório autenticado (identidade + limites). _(POST /api/easyjur/api/status)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `query` | object | Não | Parâmetros de query adicionais conforme a API oficial do EasyJur. |

#### `easyjur_create_agenda`

Cria item de agenda. Obrigatórios: tipo, id_advogado. Vincule a um processo (campo `processo`) para registrar uma movimentação/atualização. _(POST /api/easyjur/create/agenda)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `tipo` | string | Sim | Tipo do item de agenda. |
| `id_advogado` | string | Sim | ID do advogado. |
| `descricao` | string | Não |  |
| `data` | string | Não | Data (formato da API). |
| `data_fim` | string | Não |  |
| `hora_inicio` | string | Não |  |
| `hora_fim` | string | Não |  |
| `status` | string | Não |  |
| `processo` | string | Não | ID do processo vinculado. |
| `cliente` | string | Não |  |
| `local` | string | Não |  |
| `extra` | object | Não | Campos adicionais do body conforme a API oficial. |

#### `easyjur_create_oportunidade`

Cria oportunidade. Obrigatórios: nome, status, responsavel, cliente. _(POST /api/easyjur/create/oportunidade)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `nome` | string | Sim |  |
| `status` | string | Sim |  |
| `responsavel` | string | Sim | ID do responsável. |
| `cliente` | string | Sim | ID do cliente. |
| `valor_total` | string | Não |  |
| `data_atendimento` | string | Não |  |
| `extra` | object | Não | Campos adicionais do body conforme a API oficial. |

#### `easyjur_create_pessoa`

Cria uma pessoa. Obrigatórios: nome, fisica_juridica. _(POST /api/easyjur/create/pessoa)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `nome` | string | Sim |  |
| `fisica_juridica` | string | Sim | Tipo de pessoa (ex.: "F" física, "J" jurídica). |
| `apelido` | string | Não |  |
| `cpf` | string | Não |  |
| `cnpj` | string | Não |  |
| `email` | string | Não |  |
| `celular` | string | Não |  |
| `extra` | object | Não | Campos adicionais do body conforme a API oficial. |

#### `easyjur_create_processo`

Cria um processo. Obrigatórios: numero, id_advogado. (A API oficial não tem update — para registrar movimentação use easyjur_create_agenda vinculada ao processo.) _(POST /api/easyjur/create/processo)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `numero` | string | Sim | Número do processo. |
| `id_advogado` | string | Sim | ID do advogado responsável. |
| `outro_numero` | string | Não |  |
| `titulo_acao` | string | Não |  |
| `id_cliente` | string | Não |  |
| `id_contrario` | string | Não |  |
| `tipo_processo` | string | Não |  |
| `extra` | object | Não | Campos adicionais do body conforme a API oficial. |

#### `easyjur_get_agenda`

Busca um item de agenda por ID. _(POST /api/easyjur/get/agenda)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `agenda_id` | string | Sim | Path: agenda_id |
| `query` | object | Não | Parâmetros de query adicionais conforme a API oficial do EasyJur. |
| `agenda_ids` | string[] | Não | Bulk mode: multiple values for agenda_id |

#### `easyjur_get_despesa`

Busca uma despesa por ID. _(POST /api/easyjur/get/despesa)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `despesa_id` | string | Sim | Path: despesa_id |
| `query` | object | Não | Parâmetros de query adicionais conforme a API oficial do EasyJur. |
| `despesa_ids` | string[] | Não | Bulk mode: multiple values for despesa_id |

#### `easyjur_get_grupo`

Busca um grupo por ID. _(POST /api/easyjur/get/grupo)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `grupo_id` | string | Sim | Path: grupo_id |
| `query` | object | Não | Parâmetros de query adicionais conforme a API oficial do EasyJur. |
| `grupo_ids` | string[] | Não | Bulk mode: multiple values for grupo_id |

#### `easyjur_get_oportunidade`

Busca uma oportunidade por ID. _(POST /api/easyjur/get/oportunidade)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `oportunidade_id` | string | Sim | Path: oportunidade_id |
| `query` | object | Não | Parâmetros de query adicionais conforme a API oficial do EasyJur. |
| `oportunidade_ids` | string[] | Não | Bulk mode: multiple values for oportunidade_id |

#### `easyjur_get_pessoa`

Busca uma pessoa por ID. _(POST /api/easyjur/get/pessoa)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `pessoa_id` | string | Sim | Path: pessoa_id |
| `query` | object | Não | Parâmetros de query adicionais conforme a API oficial do EasyJur. |
| `pessoa_ids` | string[] | Não | Bulk mode: multiple values for pessoa_id |

#### `easyjur_get_processo`

Busca um processo por ID (dados completos). _(POST /api/easyjur/get/processo)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `processo_id` | string | Sim | Path: processo_id |
| `query` | object | Não | Parâmetros de query adicionais conforme a API oficial do EasyJur. |
| `processo_ids` | string[] | Não | Bulk mode: multiple values for processo_id |

#### `easyjur_get_receita`

Busca uma receita por ID. _(POST /api/easyjur/get/receita)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `receita_id` | string | Sim | Path: receita_id |
| `query` | object | Não | Parâmetros de query adicionais conforme a API oficial do EasyJur. |
| `receita_ids` | string[] | Não | Bulk mode: multiple values for receita_id |

#### `easyjur_get_timesheet`

Detalha um lançamento de timesheet. _(POST /api/easyjur/get/timesheet)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `id` | string | Sim | Path: id |
| `query` | object | Não | Parâmetros de query adicionais conforme a API oficial do EasyJur. |
| `ids` | string[] | Não | Bulk mode: multiple values for id |

#### `easyjur_get_token`

Consulta um token de API por ID. _(POST /api/easyjur/get/token)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `token_id` | string | Sim | Path: token_id |
| `query` | object | Não | Parâmetros de query adicionais conforme a API oficial do EasyJur. |
| `token_ids` | string[] | Não | Bulk mode: multiple values for token_id |

#### `easyjur_get_user`

Busca um usuário por ID. _(POST /api/easyjur/get/user)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `user_id` | string | Sim | Path: user_id |
| `query` | object | Não | Parâmetros de query adicionais conforme a API oficial do EasyJur. |
| `user_ids` | string[] | Não | Bulk mode: multiple values for user_id |

#### `easyjur_list_agenda`

Lista itens de agenda (prazos, compromissos, tarefas). _(POST /api/easyjur/list/agenda)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `page` | integer | Não |  |
| `page_size` | integer | Não |  |
| `query` | object | Não | Parâmetros de query adicionais conforme a API oficial do EasyJur. |

#### `easyjur_list_agenda_grupo`

Lista agenda de um grupo. _(POST /api/easyjur/list/agenda/grupo)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `grupo_id` | string | Sim | Path: grupo_id |
| `page` | integer | Não |  |
| `page_size` | integer | Não |  |
| `query` | object | Não | Parâmetros de query adicionais conforme a API oficial do EasyJur. |
| `grupo_ids` | string[] | Não | Bulk mode: multiple values for grupo_id |

#### `easyjur_list_despesas`

Lista despesas. _(POST /api/easyjur/list/despesas)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `page` | integer | Não |  |
| `page_size` | integer | Não |  |
| `query` | object | Não | Parâmetros de query adicionais conforme a API oficial do EasyJur. |

#### `easyjur_list_despesas_grupo`

Lista despesas de um grupo. _(POST /api/easyjur/list/despesas/grupo)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `grupo_id` | string | Sim | Path: grupo_id |
| `page` | integer | Não |  |
| `page_size` | integer | Não |  |
| `query` | object | Não | Parâmetros de query adicionais conforme a API oficial do EasyJur. |
| `grupo_ids` | string[] | Não | Bulk mode: multiple values for grupo_id |

#### `easyjur_list_grupos`

Lista grupos (pastas/áreas). _(POST /api/easyjur/list/grupos)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `page` | integer | Não |  |
| `page_size` | integer | Não |  |
| `query` | object | Não | Parâmetros de query adicionais conforme a API oficial do EasyJur. |

#### `easyjur_list_oportunidades`

Lista oportunidades (CRM/pré-venda). _(POST /api/easyjur/list/oportunidades)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `page` | integer | Não |  |
| `page_size` | integer | Não |  |
| `query` | object | Não | Parâmetros de query adicionais conforme a API oficial do EasyJur. |

#### `easyjur_list_oportunidades_grupo`

Lista oportunidades de um grupo. _(POST /api/easyjur/list/oportunidades/grupo)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `grupo_id` | string | Sim | Path: grupo_id |
| `page` | integer | Não |  |
| `page_size` | integer | Não |  |
| `query` | object | Não | Parâmetros de query adicionais conforme a API oficial do EasyJur. |
| `grupo_ids` | string[] | Não | Bulk mode: multiple values for grupo_id |

#### `easyjur_list_pessoas`

Lista pessoas (clientes, contrários, terceiros). _(POST /api/easyjur/list/pessoas)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `page` | integer | Não |  |
| `page_size` | integer | Não |  |
| `nome` | string | Não |  |
| `cpf` | string | Não |  |
| `cnpj` | string | Não |  |
| `query` | object | Não | Parâmetros de query adicionais conforme a API oficial do EasyJur. |

#### `easyjur_list_pessoas_grupo`

Lista pessoas de um grupo. _(POST /api/easyjur/list/pessoas/grupo)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `grupo_id` | string | Sim | Path: grupo_id |
| `page` | integer | Não |  |
| `page_size` | integer | Não |  |
| `query` | object | Não | Parâmetros de query adicionais conforme a API oficial do EasyJur. |
| `grupo_ids` | string[] | Não | Bulk mode: multiple values for grupo_id |

#### `easyjur_list_processos`

Lista/busca processos. Filtros úteis: numero, nome_parte, cpf, cnpj, advogado_nome, status, comarca, uf, data_inicio, data_fim, movimentacao, dias_movimentacao. Demais filtros via `query`. _(POST /api/easyjur/list/processos)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `page` | integer | Não |  |
| `page_size` | integer | Não |  |
| `numero` | string | Não |  |
| `nome_parte` | string | Não |  |
| `cpf` | string | Não |  |
| `cnpj` | string | Não |  |
| `advogado_nome` | string | Não |  |
| `status` | string | Não |  |
| `comarca` | string | Não |  |
| `uf` | string | Não |  |
| `data_inicio` | string | Não |  |
| `data_fim` | string | Não |  |
| `movimentacao` | string | Não |  |
| `dias_movimentacao` | string | Não |  |
| `query` | object | Não | Parâmetros de query adicionais conforme a API oficial do EasyJur. |

#### `easyjur_list_processos_grupo`

Lista processos de um grupo. _(POST /api/easyjur/list/processos/grupo)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `grupo_id` | string | Sim | Path: grupo_id |
| `page` | integer | Não |  |
| `page_size` | integer | Não |  |
| `query` | object | Não | Parâmetros de query adicionais conforme a API oficial do EasyJur. |
| `grupo_ids` | string[] | Não | Bulk mode: multiple values for grupo_id |

#### `easyjur_list_receitas`

Lista receitas. _(POST /api/easyjur/list/receitas)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `page` | integer | Não |  |
| `page_size` | integer | Não |  |
| `query` | object | Não | Parâmetros de query adicionais conforme a API oficial do EasyJur. |

#### `easyjur_list_receitas_grupo`

Lista receitas de um grupo. _(POST /api/easyjur/list/receitas/grupo)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `grupo_id` | string | Sim | Path: grupo_id |
| `page` | integer | Não |  |
| `page_size` | integer | Não |  |
| `query` | object | Não | Parâmetros de query adicionais conforme a API oficial do EasyJur. |
| `grupo_ids` | string[] | Não | Bulk mode: multiple values for grupo_id |

#### `easyjur_list_timesheet`

Lista lançamentos de timesheet. _(POST /api/easyjur/list/timesheet)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `page` | integer | Não |  |
| `page_size` | integer | Não |  |
| `query` | object | Não | Parâmetros de query adicionais conforme a API oficial do EasyJur. |

#### `easyjur_list_tokens`

Lista os tokens de API da empresa. _(POST /api/easyjur/list/tokens)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `page` | integer | Não |  |
| `page_size` | integer | Não |  |
| `query` | object | Não | Parâmetros de query adicionais conforme a API oficial do EasyJur. |

#### `easyjur_list_tribunais`

Lista tribunais/órgãos disponíveis. _(POST /api/easyjur/list/tribunais)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `query` | object | Não | Parâmetros de query adicionais conforme a API oficial do EasyJur. |

#### `easyjur_list_users`

Lista usuários do escritório. _(POST /api/easyjur/list/users)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `page` | integer | Não |  |
| `page_size` | integer | Não |  |
| `query` | object | Não | Parâmetros de query adicionais conforme a API oficial do EasyJur. |

#### `easyjur_processo_documentos`

Documentos de um processo. _(POST /api/easyjur/processo/documentos)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `processo_id` | string | Sim | Path: processo_id |
| `query` | object | Não | Parâmetros de query adicionais conforme a API oficial do EasyJur. |
| `processo_ids` | string[] | Não | Bulk mode: multiple values for processo_id |

#### `easyjur_processo_financeiros`

Lançamentos financeiros de um processo. _(POST /api/easyjur/processo/financeiros)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `processo_id` | string | Sim | Path: processo_id |
| `query` | object | Não | Parâmetros de query adicionais conforme a API oficial do EasyJur. |
| `processo_ids` | string[] | Não | Bulk mode: multiple values for processo_id |

#### `easyjur_processo_mensagens`

Mensagens/andamentos de um processo. _(POST /api/easyjur/processo/mensagens)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `processo_id` | string | Sim | Path: processo_id |
| `query` | object | Não | Parâmetros de query adicionais conforme a API oficial do EasyJur. |
| `processo_ids` | string[] | Não | Bulk mode: multiple values for processo_id |

#### `easyjur_processo_partes`

Partes de um processo. _(POST /api/easyjur/processo/partes)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `processo_id` | string | Sim | Path: processo_id |
| `query` | object | Não | Parâmetros de query adicionais conforme a API oficial do EasyJur. |
| `processo_ids` | string[] | Não | Bulk mode: multiple values for processo_id |

#### `easyjur_processo_pedidos`

Pedidos de um processo. _(POST /api/easyjur/processo/pedidos)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `processo_id` | string | Sim | Path: processo_id |
| `query` | object | Não | Parâmetros de query adicionais conforme a API oficial do EasyJur. |
| `processo_ids` | string[] | Não | Bulk mode: multiple values for processo_id |

#### `easyjur_processo_vinculados`

Processos vinculados a um processo. _(POST /api/easyjur/processo/vinculados)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `processo_id` | string | Sim | Path: processo_id |
| `query` | object | Não | Parâmetros de query adicionais conforme a API oficial do EasyJur. |
| `processo_ids` | string[] | Não | Bulk mode: multiple values for processo_id |

---

Este MCP também funciona via **conexão MCP** (Claude / Cursor) em `https://api.mcp.ai/p_easyjur` — veja o [README](../../README.md). A skill acima é pra consumir a **REST API** direto (agente próprio / código).
