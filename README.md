# EasyJur

### EasyJur para Claude, ChatGPT e agentes de IA

Wrapper da API oficial do EasyJur (gestão jurídica): processos (e partes, pedidos, financeiros, documentos, mensagens), pessoas, agenda, oportunidades, timesheet, financeiro (receitas/despesas), grupos e usuários. Leitura + criação de processos, pessoas, agenda e oportunidades. Autenticação por token de API do escritório.

- 📊 **41 ferramentas**
- ✏️ **Leitura e escrita**
- 💬 **Funciona com qualquer cliente MCP**: Claude Desktop, Cursor, VS Code, Cline, Continue
- 🔑 **Login via magic-link (sem senha)**

[English version](README.en.md) · [Documentação completa](docs/) · [Skill pra agentes](skills/)

---

## Instalar em 1 clique

### Claude (Web e Desktop)

A Anthropic unificou a instalação de MCPs em `claude.ai/customize/connectors`. **O mesmo link serve pra Claude Web e Claude Desktop** (basta estar logado):

[➕ Abrir no Claude e conectar](https://claude.ai/new?modal=add-custom-connector#settings/customize-connectors)

**Manual** (se o deeplink não abrir): [claude.ai/customize/connectors](https://claude.ai/customize/connectors?surface=cowork) → **+** → **Adicionar conector personalizado** → cole **Nome** `EasyJur` e **URL** `https://api.mcp.ai/p_easyjur`.

### Cursor

[➕ Instalar EasyJur no Cursor](cursor://anysphere.cursor-deeplink/mcp/install?name=easyjur&config=eyJ1cmwiOiJodHRwczovL2FwaS5tY3AuYWkvcF9lYXN5anVyIn0=)

### VS Code (Copilot Chat)

[➕ Instalar EasyJur no VS Code](vscode:mcp/install?name=easyjur&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fapi.mcp.ai%2Fp_easyjur%22%7D)

### ChatGPT, Manus, OpenClaw e mais 40+ clientes

Funciona em qualquer cliente MCP que suporte **MCP over HTTP**. A URL do servidor é sempre:

```
https://api.mcp.ai/p_easyjur
```

Detalhes por cliente: [INSTALL.md](INSTALL.md).

---

## Exemplos de uso

```
Busque o processo número X no EasyJur e mostre as últimas mensagens
Liste processos com movimentação nos últimos 7 dias
Crie um item de agenda vinculado ao processo Y para registrar a movimentação
```

---

## 41 ferramentas disponíveis

| Tool | Descrição |
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

Detalhe de cada tool: [docs/ferramentas.md](docs/ferramentas.md)

---

## Preços

Grátis.

---

## Privacidade & LGPD

- **Sub-processadores**: o LLM host que você escolher (Claude, ChatGPT, Cursor, agente próprio). Lista completa em [docs/privacidade-lgpd.md](docs/privacidade-lgpd.md).
- Os dados retornados pelas tools são enviados ao **LLM host que você escolher**, sub-processador fora do nosso controle. Recomendamos planos com opt-out de treinamento.

---

## Perguntas frequentes

**O servidor é open source?**
O servidor é proprietário (hosted). Este repositório é o wrapper público com manifestos, docs e skills — tudo MIT.

**Posso usar com agente próprio (não Claude/Cursor)?**
Sim — qualquer cliente que suporte MCP over HTTP. URL: `https://api.mcp.ai/p_easyjur`.


---

## Suporte

- 📧 [easyjur@mcp.ai](mailto:easyjur@mcp.ai)
- 🐛 [GitHub Issues](https://github.com/mcp-dir/easyjur-mcp/issues)
- 📄 [docs/](docs/)

---

## Licença

MIT — veja [LICENSE](LICENSE). O servidor MCP em `api.mcp.ai/p_easyjur` é proprietário (hosted); este repositório (manifestos, docs, skills) é MIT.
