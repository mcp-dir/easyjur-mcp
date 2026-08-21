# EasyJur

### EasyJur for Claude, ChatGPT and AI agents

Wrapper for the official EasyJur API (legal practice management): cases (with parties, claims, financials, documents, messages), people, calendar, opportunities, timesheet, finance (income/expenses), groups and users. Read + create for cases, people, calendar and opportunities. Authenticated by the firm's API token.

- 📊 **41 tools**
- ✏️ **Read and write**
- 💬 **Works with any MCP client**: Claude Desktop, Cursor, VS Code, Cline, Continue
- 🔑 **Magic-link login (no password)**

[Portuguese version](README.md) · [Full docs (PT-BR)](docs/)

---

## One-click install

### Claude (Web and Desktop)

[➕ Open in Claude and connect](https://claude.ai/new?modal=add-custom-connector#settings/customize-connectors)

Manual: [claude.ai/customize/connectors](https://claude.ai/customize/connectors?surface=cowork) → **+** → **Add custom connector** → name `EasyJur`, URL `https://api.mcp.ai/p_easyjur`.

### Cursor

[➕ Install in Cursor](cursor://anysphere.cursor-deeplink/mcp/install?name=easyjur&config=eyJ1cmwiOiJodHRwczovL2FwaS5tY3AuYWkvcF9lYXN5anVyIn0=)

### VS Code (Copilot Chat)

[➕ Install in VS Code](vscode:mcp/install?name=easyjur&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fapi.mcp.ai%2Fp_easyjur%22%7D)

### Any other MCP-over-HTTP client

```
https://api.mcp.ai/p_easyjur
```

---

## 41 tools

| Tool | Description |
|---|---|
| `easyjur_api_status` | Status da API EasyJur do escritório autenticado (identidade + limites). |
| `easyjur_list_tokens` | Lista os tokens de API da empresa. |
| `easyjur_get_token` | Consulta um token de API por ID. |
| `easyjur_list_pessoas` | Lista pessoas (clientes, contrários, terceiros). |
| `easyjur_get_pessoa` | Busca uma pessoa por ID. Bulk support: accepts pessoa_ids for batched execution. |
| `easyjur_list_pessoas_grupo` | Lista pessoas de um grupo. Bulk support: accepts grupo_ids for batched execution. |
| `easyjur_create_pessoa` | Cria uma pessoa. Obrigatórios: nome, fisica_juridica. |
| `easyjur_list_processos` | Lista/busca processos. Filtros úteis: numero, nome_parte, cpf, cnpj, advogado_nome, status, comarca, uf, data_inicio, data_fim, movimentacao, dias_movimentacao. Demais filtros via `query`. |
| `easyjur_list_tribunais` | Lista tribunais/órgãos disponíveis. |
| `easyjur_list_processos_grupo` | Lista processos de um grupo. Bulk support: accepts grupo_ids for batched execution. |
| `easyjur_get_processo` | Busca um processo por ID (dados completos). |
| `easyjur_processo_pedidos` | Pedidos de um processo. Bulk support: accepts processo_ids for batched execution. |
| `easyjur_processo_financeiros` | Lançamentos financeiros de um processo. |
| `easyjur_processo_documentos` | Documentos de um processo. Bulk support: accepts processo_ids for batched execution. |
| `easyjur_processo_partes` | Partes de um processo. Bulk support: accepts processo_ids for batched execution. |
| `easyjur_processo_vinculados` | Processos vinculados a um processo. |
| `easyjur_processo_mensagens` | Mensagens/andamentos de um processo. |
| `easyjur_create_processo` | Cria um processo. Obrigatórios: numero, id_advogado. (A API oficial não tem update — para registrar movimentação use easyjur_create_agenda vinculada ao processo.) |
| `easyjur_list_agenda` | Lista itens de agenda (prazos, compromissos, tarefas). |
| `easyjur_get_agenda` | Busca um item de agenda por ID. |
| `easyjur_agenda_etapas` | Etapas de workflow de um item de agenda. |
| `easyjur_agenda_comentarios` | Comentários de um item de agenda. |
| `easyjur_agenda_envolvidos` | Envolvidos em um item de agenda. |
| `easyjur_list_agenda_grupo` | Lista agenda de um grupo. Bulk support: accepts grupo_ids for batched execution. |
| `easyjur_create_agenda` | Cria item de agenda. Obrigatórios: tipo, id_advogado. Vincule a um processo (campo `processo`) para registrar uma movimentação/atualização. |
| `easyjur_list_timesheet` | Lista lançamentos de timesheet. |
| `easyjur_get_timesheet` | Detalha um lançamento de timesheet. |
| `easyjur_list_oportunidades` | Lista oportunidades (CRM/pré-venda). |
| `easyjur_get_oportunidade` | Busca uma oportunidade por ID. |
| `easyjur_list_oportunidades_grupo` | Lista oportunidades de um grupo. |
| `easyjur_create_oportunidade` | Cria oportunidade. Obrigatórios: nome, status, responsavel, cliente. |
| `easyjur_list_receitas` | Lista receitas. |
| `easyjur_get_receita` | Busca uma receita por ID. Bulk support: accepts receita_ids for batched execution. |
| `easyjur_list_receitas_grupo` | Lista receitas de um grupo. Bulk support: accepts grupo_ids for batched execution. |
| `easyjur_list_despesas` | Lista despesas. |
| `easyjur_get_despesa` | Busca uma despesa por ID. Bulk support: accepts despesa_ids for batched execution. |
| `easyjur_list_despesas_grupo` | Lista despesas de um grupo. Bulk support: accepts grupo_ids for batched execution. |
| `easyjur_list_grupos` | Lista grupos (pastas/áreas). |
| `easyjur_get_grupo` | Busca um grupo por ID. Bulk support: accepts grupo_ids for batched execution. |
| `easyjur_list_users` | Lista usuários do escritório. |
| `easyjur_get_user` | Busca um usuário por ID. Bulk support: accepts user_ids for batched execution. |

---

## Pricing

Free.

---

## License

MIT — see [LICENSE](LICENSE). The MCP server at `api.mcp.ai/p_easyjur` is proprietary (hosted); this repo (manifests, docs, skills) is MIT.
