# Ferramentas

EasyJur expõe 41 ferramentas.

### 1. `easyjur_api_status`
**Input**: `query` (opcional)

Status da API EasyJur do escritório autenticado (identidade + limites).

### 2. `easyjur_list_tokens`
**Input**: `page` (opcional), `page_size` (opcional), `query` (opcional)

Lista os tokens de API da empresa.

### 3. `easyjur_get_token`
**Input**: `token_id`, `query` (opcional), `token_ids` (opcional)

Consulta um token de API por ID.

### 4. `easyjur_list_pessoas`
**Input**: `page` (opcional), `page_size` (opcional), `nome` (opcional), `cpf` (opcional), `cnpj` (opcional), `query` (opcional)

Lista pessoas (clientes, contrários, terceiros).

### 5. `easyjur_get_pessoa`
**Input**: `pessoa_id`, `query` (opcional), `pessoa_ids` (opcional)

Busca uma pessoa por ID. Bulk support: accepts pessoa_ids for batched execution.

### 6. `easyjur_list_pessoas_grupo`
**Input**: `grupo_id`, `page` (opcional), `page_size` (opcional), `query` (opcional), `grupo_ids` (opcional)

Lista pessoas de um grupo. Bulk support: accepts grupo_ids for batched execution.

### 7. `easyjur_create_pessoa`
**Input**: `nome`, `fisica_juridica`, `apelido` (opcional), `cpf` (opcional), `cnpj` (opcional), `email` (opcional), `celular` (opcional), `extra` (opcional)

Cria uma pessoa. Obrigatórios: nome, fisica_juridica.

### 8. `easyjur_list_processos`
**Input**: `page` (opcional), `page_size` (opcional), `numero` (opcional), `nome_parte` (opcional), `cpf` (opcional), `cnpj` (opcional), `advogado_nome` (opcional), `status` (opcional), `comarca` (opcional), `uf` (opcional), `data_inicio` (opcional), `data_fim` (opcional), `movimentacao` (opcional), `dias_movimentacao` (opcional), `query` (opcional)

Lista/busca processos. Filtros úteis: numero, nome_parte, cpf, cnpj, advogado_nome, status, comarca, uf, data_inicio, data_fim, movimentacao, dias_movimentacao. Demais filtros via `query`.

### 9. `easyjur_list_tribunais`
**Input**: `query` (opcional)

Lista tribunais/órgãos disponíveis.

### 10. `easyjur_list_processos_grupo`
**Input**: `grupo_id`, `page` (opcional), `page_size` (opcional), `query` (opcional), `grupo_ids` (opcional)

Lista processos de um grupo. Bulk support: accepts grupo_ids for batched execution.

### 11. `easyjur_get_processo`
**Input**: `processo_id`, `query` (opcional), `processo_ids` (opcional)

Busca um processo por ID (dados completos).

### 12. `easyjur_processo_pedidos`
**Input**: `processo_id`, `query` (opcional), `processo_ids` (opcional)

Pedidos de um processo. Bulk support: accepts processo_ids for batched execution.

### 13. `easyjur_processo_financeiros`
**Input**: `processo_id`, `query` (opcional), `processo_ids` (opcional)

Lançamentos financeiros de um processo.

### 14. `easyjur_processo_documentos`
**Input**: `processo_id`, `query` (opcional), `processo_ids` (opcional)

Documentos de um processo. Bulk support: accepts processo_ids for batched execution.

### 15. `easyjur_processo_partes`
**Input**: `processo_id`, `query` (opcional), `processo_ids` (opcional)

Partes de um processo. Bulk support: accepts processo_ids for batched execution.

### 16. `easyjur_processo_vinculados`
**Input**: `processo_id`, `query` (opcional), `processo_ids` (opcional)

Processos vinculados a um processo.

### 17. `easyjur_processo_mensagens`
**Input**: `processo_id`, `query` (opcional), `processo_ids` (opcional)

Mensagens/andamentos de um processo.

### 18. `easyjur_create_processo`
**Input**: `numero`, `id_advogado`, `outro_numero` (opcional), `titulo_acao` (opcional), `id_cliente` (opcional), `id_contrario` (opcional), `tipo_processo` (opcional), `extra` (opcional)

Cria um processo. Obrigatórios: numero, id_advogado. (A API oficial não tem update — para registrar movimentação use easyjur_create_agenda vinculada ao processo.)

### 19. `easyjur_list_agenda`
**Input**: `page` (opcional), `page_size` (opcional), `query` (opcional)

Lista itens de agenda (prazos, compromissos, tarefas).

### 20. `easyjur_get_agenda`
**Input**: `agenda_id`, `query` (opcional), `agenda_ids` (opcional)

Busca um item de agenda por ID.

### 21. `easyjur_agenda_etapas`
**Input**: `agenda_id`, `query` (opcional), `agenda_ids` (opcional)

Etapas de workflow de um item de agenda.

### 22. `easyjur_agenda_comentarios`
**Input**: `id_agenda`, `query` (opcional)

Comentários de um item de agenda.

### 23. `easyjur_agenda_envolvidos`
**Input**: `agenda_id`, `query` (opcional), `agenda_ids` (opcional)

Envolvidos em um item de agenda.

### 24. `easyjur_list_agenda_grupo`
**Input**: `grupo_id`, `page` (opcional), `page_size` (opcional), `query` (opcional), `grupo_ids` (opcional)

Lista agenda de um grupo. Bulk support: accepts grupo_ids for batched execution.

### 25. `easyjur_create_agenda`
**Input**: `tipo`, `id_advogado`, `descricao` (opcional), `data` (opcional), `data_fim` (opcional), `hora_inicio` (opcional), `hora_fim` (opcional), `status` (opcional), `processo` (opcional), `cliente` (opcional), `local` (opcional), `extra` (opcional)

Cria item de agenda. Obrigatórios: tipo, id_advogado. Vincule a um processo (campo `processo`) para registrar uma movimentação/atualização.

### 26. `easyjur_list_timesheet`
**Input**: `page` (opcional), `page_size` (opcional), `query` (opcional)

Lista lançamentos de timesheet.

### 27. `easyjur_get_timesheet`
**Input**: `id`, `query` (opcional), `ids` (opcional)

Detalha um lançamento de timesheet.

### 28. `easyjur_list_oportunidades`
**Input**: `page` (opcional), `page_size` (opcional), `query` (opcional)

Lista oportunidades (CRM/pré-venda).

### 29. `easyjur_get_oportunidade`
**Input**: `oportunidade_id`, `query` (opcional), `oportunidade_ids` (opcional)

Busca uma oportunidade por ID.

### 30. `easyjur_list_oportunidades_grupo`
**Input**: `grupo_id`, `page` (opcional), `page_size` (opcional), `query` (opcional), `grupo_ids` (opcional)

Lista oportunidades de um grupo.

### 31. `easyjur_create_oportunidade`
**Input**: `nome`, `status`, `responsavel`, `cliente`, `valor_total` (opcional), `data_atendimento` (opcional), `extra` (opcional)

Cria oportunidade. Obrigatórios: nome, status, responsavel, cliente.

### 32. `easyjur_list_receitas`
**Input**: `page` (opcional), `page_size` (opcional), `query` (opcional)

Lista receitas.

### 33. `easyjur_get_receita`
**Input**: `receita_id`, `query` (opcional), `receita_ids` (opcional)

Busca uma receita por ID. Bulk support: accepts receita_ids for batched execution.

### 34. `easyjur_list_receitas_grupo`
**Input**: `grupo_id`, `page` (opcional), `page_size` (opcional), `query` (opcional), `grupo_ids` (opcional)

Lista receitas de um grupo. Bulk support: accepts grupo_ids for batched execution.

### 35. `easyjur_list_despesas`
**Input**: `page` (opcional), `page_size` (opcional), `query` (opcional)

Lista despesas.

### 36. `easyjur_get_despesa`
**Input**: `despesa_id`, `query` (opcional), `despesa_ids` (opcional)

Busca uma despesa por ID. Bulk support: accepts despesa_ids for batched execution.

### 37. `easyjur_list_despesas_grupo`
**Input**: `grupo_id`, `page` (opcional), `page_size` (opcional), `query` (opcional), `grupo_ids` (opcional)

Lista despesas de um grupo. Bulk support: accepts grupo_ids for batched execution.

### 38. `easyjur_list_grupos`
**Input**: `page` (opcional), `page_size` (opcional), `query` (opcional)

Lista grupos (pastas/áreas).

### 39. `easyjur_get_grupo`
**Input**: `grupo_id`, `query` (opcional), `grupo_ids` (opcional)

Busca um grupo por ID. Bulk support: accepts grupo_ids for batched execution.

### 40. `easyjur_list_users`
**Input**: `page` (opcional), `page_size` (opcional), `query` (opcional)

Lista usuários do escritório.

### 41. `easyjur_get_user`
**Input**: `user_id`, `query` (opcional), `user_ids` (opcional)

Busca um usuário por ID. Bulk support: accepts user_ids for batched execution.

## Prompts de exemplo

```
Busque o processo número X no EasyJur e mostre as últimas mensagens
Liste processos com movimentação nos últimos 7 dias
Crie um item de agenda vinculado ao processo Y para registrar a movimentação
```
