# HiveCloud CT-e / MDF-e

### HiveCloud CT-e / MDF-e para Claude, ChatGPT e agentes de IA

Emissor de documentos fiscais de transporte da Bsoft by nstech (HiveCloud). Consulta de CT-e (Conhecimento de Transporte), MDF-e (Manifesto de Documentos Fiscais), DC-e, inutilizações, status da SEFAZ, além de veículos e motoristas. Conecte com o usuário e a senha do seu emissor e o ambiente. Somente leitura nesta versão.

- 📊 **27 ferramentas**
- ✏️ **Leitura e escrita**
- 💬 **Funciona com qualquer cliente MCP**: Claude Desktop, Cursor, VS Code, Cline, Continue
- 🔑 **Login via magic-link (sem senha)**

[English version](README.en.md) · [Documentação completa](docs/) · [Skill pra agentes](skills/)

---

## Instalar em 1 clique

### Claude (Web e Desktop)

A Anthropic unificou a instalação de MCPs em `claude.ai/customize/connectors`. **O mesmo link serve pra Claude Web e Claude Desktop** (basta estar logado):

[➕ Abrir no Claude e conectar](https://claude.ai/new?modal=add-custom-connector#settings/customize-connectors)

**Manual** (se o deeplink não abrir): [claude.ai/customize/connectors](https://claude.ai/customize/connectors?surface=cowork) → **+** → **Adicionar conector personalizado** → cole **Nome** `HiveCloud CT-e / MDF-e` e **URL** `https://api.mcp.ai/p_hivecloud`.

### Cursor

[➕ Instalar HiveCloud CT-e / MDF-e no Cursor](cursor://anysphere.cursor-deeplink/mcp/install?name=hivecloud&config=eyJ1cmwiOiJodHRwczovL2FwaS5tY3AuYWkvcF9oaXZlY2xvdWQifQ==)

### VS Code (Copilot Chat)

[➕ Instalar HiveCloud CT-e / MDF-e no VS Code](vscode:mcp/install?name=hivecloud&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fapi.mcp.ai%2Fp_hivecloud%22%7D)

### ChatGPT, Manus, OpenClaw e mais 40+ clientes

Funciona em qualquer cliente MCP que suporte **MCP over HTTP**. A URL do servidor é sempre:

```
https://api.mcp.ai/p_hivecloud
```

Detalhes por cliente: [INSTALL.md](INSTALL.md).

---

## Exemplos de uso

```
Liste os CT-e emitidos este mês da empresa
Qual o status do serviço da SEFAZ agora?
Quantas viagens a placa ANX6H66 fez no trimestre?
```

---

## 27 ferramentas disponíveis

| Tool | Descrição |
|---|---|
| `hivecloud_list_accounts` | Lista as contas HiveCloud conectadas a este install (cada usuário+ambiente = uma conta). |
| `hivecloud_list_empresas` | Lista as empresas emitentes do ambiente (id, nome, cnpj). |
| `hivecloud_list_ctes` | Lista os CT-e (Conhecimento de Transporte eletrônico) da empresa, paginado, com filtro por data de emissão. |
| `hivecloud_get_cte` | Detalha um CT-e específico pelo id. |
| `hivecloud_cte_dacte` | Gera o PDF do DACTE de um ou mais CT-e autorizados e devolve a URL de download (temporária). |
| `hivecloud_cte_xml` | Exporta o XML de um ou mais CT-e (zip) e devolve a URL de download (temporária). |
| `hivecloud_nfe_info` | Consulta os dados de uma NF-e pela chave de acesso (44 dígitos) via emissor: remetente e destinatário (já resolvidos no cadastro), valor da carga, pesos, volumes e produto predominante. |
| `hivecloud_cte_criar_de_nfe` | Cria um RASCUNHO de CT-e a partir de uma ou mais chaves de NF-e (mesmo remetente e destinatário). |
| `hivecloud_list_dces` | Lista as DC-e (Declaração de Conteúdo eletrônica) da empresa, paginado. |
| `hivecloud_list_inutilizacoes` | Lista as inutilizações de numeração de CT-e da empresa, paginado. |
| `hivecloud_sefaz_status` | Status do serviço da SEFAZ para a empresa (se o servidor da Fazenda está em operação). |
| `hivecloud_mdfe_empresas` | Lista as empresas emitentes do ambiente de MDF-e (o MDF-e tem ambiente e empresas PRÓPRIOS, distintos do CT-e). |
| `hivecloud_list_mdfes` | Lista os MDF-e (Manifesto Eletrônico de Documentos Fiscais) da empresa, paginado (número, série, dataEmissao, statusMdfe, UF de carregamento/descarregamento, CIOT). |
| `hivecloud_get_mdfe` | Detalha um MDF-e pelo id: placa do veículo (dadosVeiculo), condutores (nome/CPF), CIOT, documentos vinculados (chaves de CT-e/NF-e), UFs, valor e peso da carga, status e protocolos. |
| `hivecloud_mdfe_damdfe` | Gera o PDF do DAMDFE de um ou mais MDF-e e devolve a URL de download (temporária). |
| `hivecloud_mdfe_xml` | Exporta o XML de um ou mais MDF-e (zip) e devolve a URL de download (temporária). |
| `hivecloud_relatorio_viagens` | Relatório consolidado de viagens (MDF-e) por período: contagem por mês, ranking por placa e por motorista, com filtros por placa e/ou motorista (CPF ou nome) e faturamento opcional (soma do valorTotalFrete dos CT-e vi… |
| `hivecloud_list_veiculos` | Lista os veículos cadastrados (placa, motorista, reboque, tara), usados no MDF-e, paginado. |
| `hivecloud_list_motoristas` | Lista os motoristas/condutores cadastrados (nome, cpf, cnh), usados no MDF-e, paginado. |
| `hivecloud_cte_emitir` | ATO FISCAL REAL: transmite um ou mais CT-e à SEFAZ (por id). |
| `hivecloud_cte_cancelar` | ATO FISCAL REAL: cancela um ou mais CT-e autorizados (por id) junto à SEFAZ. |
| `hivecloud_cte_excluir` | Exclui um ou mais CT-e (rascunhos/rejeitados, por id). |
| `hivecloud_cte_averbar` | Averba (registra o seguro de carga) um ou mais CT-e (por id). |
| `hivecloud_cte_carta_correcao` | ATO FISCAL REAL: emite uma carta de correção (CC-e) para um CT-e autorizado. |
| `hivecloud_mdfe_emitir` | ATO FISCAL REAL: transmite um ou mais MDF-e à SEFAZ (por id). |
| `hivecloud_mdfe_encerrar` | ATO FISCAL REAL: encerra um ou mais MDF-e (por id) após o fim da viagem. |
| `hivecloud_mdfe_cancelar` | ATO FISCAL REAL: cancela um ou mais MDF-e (por id) junto à SEFAZ. |

Detalhe de cada tool: [docs/ferramentas.md](docs/ferramentas.md)

---

## Preços

Planos a partir do tier grátis. Veja [docs/precos.md](docs/precos.md).

---

## Privacidade & LGPD

- **Sub-processadores**: HiveCloud (Bsoft / nstech), o LLM host que você escolher (Claude, ChatGPT, Cursor, agente próprio). Lista completa em [docs/privacidade-lgpd.md](docs/privacidade-lgpd.md).
- Os dados retornados pelas tools são enviados ao **LLM host que você escolher**, sub-processador fora do nosso controle. Recomendamos planos com opt-out de treinamento.

---

## Perguntas frequentes

**O servidor é open source?**
O servidor é proprietário (hosted). Este repositório é o wrapper público com manifestos, docs e skills — tudo MIT.

**Posso usar com agente próprio (não Claude/Cursor)?**
Sim — qualquer cliente que suporte MCP over HTTP. URL: `https://api.mcp.ai/p_hivecloud`.


---

## Suporte

- 📧 [hivecloud@mcp.ai](mailto:hivecloud@mcp.ai)
- 🐛 [GitHub Issues](https://github.com/mcp-dir/hivecloud-mcp/issues)
- 📄 [docs/](docs/)

---

## Licença

MIT — veja [LICENSE](LICENSE). O servidor MCP em `api.mcp.ai/p_hivecloud` é proprietário (hosted); este repositório (manifestos, docs, skills) é MIT.
