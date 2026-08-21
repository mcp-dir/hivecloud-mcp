---
name: hivecloud-mcp
description: Skill da REST API do HiveCloud CT-e / MDF-e na MCP.AI: 27 endpoints em /api/hivecloud. Emissor de documentos fiscais de transporte da Bsoft by nstech (HiveCloud). Consulta de CT-e (Conhecimento de Transporte), MDF-e (Manifesto de Documentos Fiscais), DC-e, inutilizações, status da SEFAZ, além de veículos e motoristas. Conecte com o usuário e a senha do seu emissor e o ambiente. Somente leitura nesta versão. Autentique com workspace API key (sk_live) gerada em app.mcp.ai/settings/api-keys. Use quando o usuário pedir algo coberto pelos endpoints.
---

# HiveCloud CT-e / MDF-e — REST API skill

Você tem acesso à **HiveCloud CT-e / MDF-e** REST API na MCP.AI.

> Emissor de documentos fiscais de transporte da Bsoft by nstech (HiveCloud). Consulta de CT-e (Conhecimento de Transporte), MDF-e (Manifesto de Documentos Fiscais), DC-e, inutilizações, status da SEFAZ, além de veículos e motoristas. Conecte com o usuário e a senha do seu emissor e o ambiente. Somente leitura nesta versão.

## Base URL

```
https://api.mcp.ai/api/hivecloud
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
curl -X POST https://api.mcp.ai/api/hivecloud/cte/averbar \
  -H "Authorization: Bearer sk_live_..." \
  -H "Content-Type: application/json" \
  -d '{"ids":"..."}'
```

## Reportar problemas

Se um endpoint retornar erro, vazio ou dado inesperado, reporte (não desista calado): **POST /api/hivecloud/report** com `{ "message": "...", "context"?: "...", "conversation"?: [...] }`. Isso notifica o time da MCP.AI.

## Endpoints (27)

#### `hivecloud_cte_averbar`

Averba (registra o seguro de carga) um ou mais CT-e (por id). _(POST /api/hivecloud/cte/averbar)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `ids` | string[] | Sim | Lista de ids dos documentos (o campo `id` retornado nas listagens). |
| `empresa_id` | string | Não | empresaId (empresa emitente). 1 de N, veja hivecloud_list_empresas. Omitido = empresa padrão da conexão / primeira disponível. |
| `account` | string | Não | Quando há múltiplas contas HiveCloud conectadas: id/label da conexão. Veja hivecloud_list_accounts. |

#### `hivecloud_cte_cancelar`

ATO FISCAL REAL: cancela um ou mais CT-e autorizados (por id) junto à SEFAZ. _(POST /api/hivecloud/cte/cancelar)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `ids` | string[] | Sim | Lista de ids dos documentos (o campo `id` retornado nas listagens). |
| `empresa_id` | string | Não | empresaId (empresa emitente). 1 de N, veja hivecloud_list_empresas. Omitido = empresa padrão da conexão / primeira disponível. |
| `account` | string | Não | Quando há múltiplas contas HiveCloud conectadas: id/label da conexão. Veja hivecloud_list_accounts. |

#### `hivecloud_cte_carta_correcao`

ATO FISCAL REAL: emite uma carta de correção (CC-e) para um CT-e autorizado. _(POST /api/hivecloud/cte/carta/correcao)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `cte_id` | string | Sim | id do CT-e a corrigir. |
| `correcoes` | object | Sim | Objeto com os campos a corrigir (só os alterados). |
| `empresa_id` | string | Não | empresaId (empresa emitente). 1 de N, veja hivecloud_list_empresas. Omitido = empresa padrão da conexão / primeira disponível. |
| `account` | string | Não | Quando há múltiplas contas HiveCloud conectadas: id/label da conexão. Veja hivecloud_list_accounts. |
| `cte_ids` | string[] | Não | Bulk mode: multiple values for cte_id |
| `empresa_ids` | string[] | Não | Bulk mode: multiple values for empresa_id |

#### `hivecloud_cte_criar_de_nfe`

Cria um RASCUNHO de CT-e a partir de uma ou mais chaves de NF-e (mesmo remetente e destinatário). _(POST /api/hivecloud/cte/criar/de/nfe)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `nfe_chaves` | string[] | Sim | Chaves de acesso das NF-e (44 dígitos). Todas do mesmo remetente→destinatário. |
| `valor_frete` | number | Sim | Valor do frete (R$) do CT-e. |
| `tomador` | string | Não | Quem paga o frete (tomador). Default: destinatario. (remetente, destinatario) |
| `responsavel_frete` | string | Não | Responsável pelo frete. Default: o do CT-e template. (REMETENTE, DESTINATARIO, EXPEDIDOR, RECEBEDOR, TERCEIROS) |
| `cfop_codigo` | string | Não | CFOP do serviço (ex. 6353). Default: o do último CT-e autorizado. |
| `cfop_natureza` | string | Não | Natureza da operação do CFOP (até 60 caracteres). |
| `produto_predominante` | string | Não | Produto predominante da carga. Default: o da NF-e. |
| `observacao` | string | Não | Observação geral do CT-e (campo de notas). |
| `template_cte_id` | string | Não | id de um CT-e pra usar como base de imposto/CFOP/local de emissão. Default: o último AUTORIZADO. |
| `empresa_id` | string | Não | empresaId (empresa emitente). 1 de N, veja hivecloud_list_empresas. Omitido = empresa padrão da conexão / primeira disponível. |
| `account` | string | Não | Quando há múltiplas contas HiveCloud conectadas: id/label da conexão. Veja hivecloud_list_accounts. |
| `template_cte_ids` | string[] | Não | Bulk mode: multiple values for template_cte_id |
| `empresa_ids` | string[] | Não | Bulk mode: multiple values for empresa_id |

#### `hivecloud_cte_dacte`

Gera o PDF do DACTE de um ou mais CT-e autorizados e devolve a URL de download (temporária). _(POST /api/hivecloud/cte/dacte)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `ids` | string[] | Sim | Lista de ids dos documentos (o campo `id` retornado nas listagens). |
| `empresa_id` | string | Não | empresaId (empresa emitente). 1 de N, veja hivecloud_list_empresas. Omitido = empresa padrão da conexão / primeira disponível. |
| `account` | string | Não | Quando há múltiplas contas HiveCloud conectadas: id/label da conexão. Veja hivecloud_list_accounts. |

#### `hivecloud_cte_emitir`

ATO FISCAL REAL: transmite um ou mais CT-e à SEFAZ (por id). _(POST /api/hivecloud/cte/emitir)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `ids` | string[] | Sim | Lista de ids dos documentos (o campo `id` retornado nas listagens). |
| `empresa_id` | string | Não | empresaId (empresa emitente). 1 de N, veja hivecloud_list_empresas. Omitido = empresa padrão da conexão / primeira disponível. |
| `account` | string | Não | Quando há múltiplas contas HiveCloud conectadas: id/label da conexão. Veja hivecloud_list_accounts. |

#### `hivecloud_cte_excluir`

Exclui um ou mais CT-e (rascunhos/rejeitados, por id). _(POST /api/hivecloud/cte/excluir)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `ids` | string[] | Sim | Lista de ids dos documentos (o campo `id` retornado nas listagens). |
| `empresa_id` | string | Não | empresaId (empresa emitente). 1 de N, veja hivecloud_list_empresas. Omitido = empresa padrão da conexão / primeira disponível. |
| `account` | string | Não | Quando há múltiplas contas HiveCloud conectadas: id/label da conexão. Veja hivecloud_list_accounts. |

#### `hivecloud_cte_xml`

Exporta o XML de um ou mais CT-e (zip) e devolve a URL de download (temporária). _(POST /api/hivecloud/cte/xml)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `ids` | string[] | Sim | Lista de ids dos documentos (o campo `id` retornado nas listagens). |
| `empresa_id` | string | Não | empresaId (empresa emitente). 1 de N, veja hivecloud_list_empresas. Omitido = empresa padrão da conexão / primeira disponível. |
| `account` | string | Não | Quando há múltiplas contas HiveCloud conectadas: id/label da conexão. Veja hivecloud_list_accounts. |

#### `hivecloud_get_cte`

Detalha um CT-e específico pelo id. _(POST /api/hivecloud/get/cte)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `id` | string | Sim | id do CT-e (retornado por hivecloud_list_ctes). |
| `empresa_id` | string | Não | empresaId (empresa emitente). 1 de N, veja hivecloud_list_empresas. Omitido = empresa padrão da conexão / primeira disponível. |
| `account` | string | Não | Quando há múltiplas contas HiveCloud conectadas: id/label da conexão. Veja hivecloud_list_accounts. |
| `ids` | string[] | Não | Bulk mode: multiple values for id |
| `empresa_ids` | string[] | Não | Bulk mode: multiple values for empresa_id |

#### `hivecloud_get_mdfe`

Detalha um MDF-e pelo id: placa do veículo (dadosVeiculo), condutores (nome/CPF), CIOT, documentos vinculados (chaves de CT-e/NF-e), UFs, valor e peso da carga, status e protocolos. _(POST /api/hivecloud/get/mdfe)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `id` | string | Sim | id do MDF-e (retornado por hivecloud_list_mdfes). |
| `empresa_id` | string | Não | empresaId (empresa emitente). 1 de N, veja hivecloud_list_empresas. Omitido = empresa padrão da conexão / primeira disponível. |
| `account` | string | Não | Quando há múltiplas contas HiveCloud conectadas: id/label da conexão. Veja hivecloud_list_accounts. |
| `ids` | string[] | Não | Bulk mode: multiple values for id |
| `empresa_ids` | string[] | Não | Bulk mode: multiple values for empresa_id |

#### `hivecloud_list_accounts`

Lista as contas HiveCloud conectadas a este install (cada usuário+ambiente = uma conta). _(POST /api/hivecloud/list/accounts)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas HiveCloud conectadas: id/label da conexão. Veja hivecloud_list_accounts. |

#### `hivecloud_list_ctes`

Lista os CT-e (Conhecimento de Transporte eletrônico) da empresa, paginado, com filtro por data de emissão. _(POST /api/hivecloud/list/ctes)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `empresa_id` | string | Não | empresaId (empresa emitente). 1 de N, veja hivecloud_list_empresas. Omitido = empresa padrão da conexão / primeira disponível. |
| `pageSize` | integer | Não | Itens por página (default 20). |
| `pageNumber` | integer | Não | Página, 0-INDEXED (0 = primeira página). Default 0. |
| `data_inicial` | string | Não | Data de emissão inicial (YYYY-MM-DD). |
| `data_final` | string | Não | Data de emissão final (YYYY-MM-DD). |
| `account` | string | Não | Quando há múltiplas contas HiveCloud conectadas: id/label da conexão. Veja hivecloud_list_accounts. |
| `empresa_ids` | string[] | Não | Bulk mode: multiple values for empresa_id |

#### `hivecloud_list_dces`

Lista as DC-e (Declaração de Conteúdo eletrônica) da empresa, paginado. _(POST /api/hivecloud/list/dces)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `empresa_id` | string | Não | empresaId (empresa emitente). 1 de N, veja hivecloud_list_empresas. Omitido = empresa padrão da conexão / primeira disponível. |
| `pageSize` | integer | Não | Itens por página (default 20). |
| `pageNumber` | integer | Não | Página, 0-INDEXED (0 = primeira página). Default 0. |
| `account` | string | Não | Quando há múltiplas contas HiveCloud conectadas: id/label da conexão. Veja hivecloud_list_accounts. |
| `empresa_ids` | string[] | Não | Bulk mode: multiple values for empresa_id |

#### `hivecloud_list_empresas`

Lista as empresas emitentes do ambiente (id, nome, cnpj). _(POST /api/hivecloud/list/empresas)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas HiveCloud conectadas: id/label da conexão. Veja hivecloud_list_accounts. |

#### `hivecloud_list_inutilizacoes`

Lista as inutilizações de numeração de CT-e da empresa, paginado. _(POST /api/hivecloud/list/inutilizacoes)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `empresa_id` | string | Não | empresaId (empresa emitente). 1 de N, veja hivecloud_list_empresas. Omitido = empresa padrão da conexão / primeira disponível. |
| `pageSize` | integer | Não | Itens por página (default 20). |
| `pageNumber` | integer | Não | Página, 0-INDEXED (0 = primeira página). Default 0. |
| `account` | string | Não | Quando há múltiplas contas HiveCloud conectadas: id/label da conexão. Veja hivecloud_list_accounts. |
| `empresa_ids` | string[] | Não | Bulk mode: multiple values for empresa_id |

#### `hivecloud_list_mdfes`

Lista os MDF-e (Manifesto Eletrônico de Documentos Fiscais) da empresa, paginado (número, série, dataEmissao, statusMdfe, UF de carregamento/descarregamento, CIOT). _(POST /api/hivecloud/list/mdfes)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `empresa_id` | string | Não | empresaId (empresa emitente). 1 de N, veja hivecloud_list_empresas. Omitido = empresa padrão da conexão / primeira disponível. |
| `pageSize` | integer | Não | Itens por página (default 20). |
| `pageNumber` | integer | Não | Página, 0-INDEXED (0 = primeira página). Default 0. |
| `data_inicial` | string | Não | Data de emissão inicial (YYYY-MM-DD). |
| `data_final` | string | Não | Data de emissão final (YYYY-MM-DD). |
| `account` | string | Não | Quando há múltiplas contas HiveCloud conectadas: id/label da conexão. Veja hivecloud_list_accounts. |
| `empresa_ids` | string[] | Não | Bulk mode: multiple values for empresa_id |

#### `hivecloud_list_motoristas`

Lista os motoristas/condutores cadastrados (nome, cpf, cnh), usados no MDF-e, paginado. _(POST /api/hivecloud/list/motoristas)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `empresa_id` | string | Não | empresaId (empresa emitente). 1 de N, veja hivecloud_list_empresas. Omitido = empresa padrão da conexão / primeira disponível. |
| `pageSize` | integer | Não | Itens por página (default 20). |
| `pageNumber` | integer | Não | Página, 0-INDEXED (0 = primeira página). Default 0. |
| `account` | string | Não | Quando há múltiplas contas HiveCloud conectadas: id/label da conexão. Veja hivecloud_list_accounts. |
| `empresa_ids` | string[] | Não | Bulk mode: multiple values for empresa_id |

#### `hivecloud_list_veiculos`

Lista os veículos cadastrados (placa, motorista, reboque, tara), usados no MDF-e, paginado. _(POST /api/hivecloud/list/veiculos)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `empresa_id` | string | Não | empresaId (empresa emitente). 1 de N, veja hivecloud_list_empresas. Omitido = empresa padrão da conexão / primeira disponível. |
| `pageSize` | integer | Não | Itens por página (default 20). |
| `pageNumber` | integer | Não | Página, 0-INDEXED (0 = primeira página). Default 0. |
| `account` | string | Não | Quando há múltiplas contas HiveCloud conectadas: id/label da conexão. Veja hivecloud_list_accounts. |
| `empresa_ids` | string[] | Não | Bulk mode: multiple values for empresa_id |

#### `hivecloud_mdfe_cancelar`

ATO FISCAL REAL: cancela um ou mais MDF-e (por id) junto à SEFAZ. _(POST /api/hivecloud/mdfe/cancelar)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `ids` | string[] | Sim | Lista de ids dos documentos (o campo `id` retornado nas listagens). |
| `empresa_id` | string | Não | empresaId (empresa emitente). 1 de N, veja hivecloud_list_empresas. Omitido = empresa padrão da conexão / primeira disponível. |
| `account` | string | Não | Quando há múltiplas contas HiveCloud conectadas: id/label da conexão. Veja hivecloud_list_accounts. |

#### `hivecloud_mdfe_damdfe`

Gera o PDF do DAMDFE de um ou mais MDF-e e devolve a URL de download (temporária). _(POST /api/hivecloud/mdfe/damdfe)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `ids` | string[] | Sim | Lista de ids dos documentos (o campo `id` retornado nas listagens). |
| `empresa_id` | string | Não | empresaId (empresa emitente). 1 de N, veja hivecloud_list_empresas. Omitido = empresa padrão da conexão / primeira disponível. |
| `account` | string | Não | Quando há múltiplas contas HiveCloud conectadas: id/label da conexão. Veja hivecloud_list_accounts. |

#### `hivecloud_mdfe_emitir`

ATO FISCAL REAL: transmite um ou mais MDF-e à SEFAZ (por id). _(POST /api/hivecloud/mdfe/emitir)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `ids` | string[] | Sim | Lista de ids dos documentos (o campo `id` retornado nas listagens). |
| `empresa_id` | string | Não | empresaId (empresa emitente). 1 de N, veja hivecloud_list_empresas. Omitido = empresa padrão da conexão / primeira disponível. |
| `account` | string | Não | Quando há múltiplas contas HiveCloud conectadas: id/label da conexão. Veja hivecloud_list_accounts. |

#### `hivecloud_mdfe_empresas`

Lista as empresas emitentes do ambiente de MDF-e (o MDF-e tem ambiente e empresas PRÓPRIOS, distintos do CT-e). _(POST /api/hivecloud/mdfe/empresas)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas HiveCloud conectadas: id/label da conexão. Veja hivecloud_list_accounts. |

#### `hivecloud_mdfe_encerrar`

ATO FISCAL REAL: encerra um ou mais MDF-e (por id) após o fim da viagem. _(POST /api/hivecloud/mdfe/encerrar)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `ids` | string[] | Sim | Lista de ids dos documentos (o campo `id` retornado nas listagens). |
| `empresa_id` | string | Não | empresaId (empresa emitente). 1 de N, veja hivecloud_list_empresas. Omitido = empresa padrão da conexão / primeira disponível. |
| `account` | string | Não | Quando há múltiplas contas HiveCloud conectadas: id/label da conexão. Veja hivecloud_list_accounts. |

#### `hivecloud_mdfe_xml`

Exporta o XML de um ou mais MDF-e (zip) e devolve a URL de download (temporária). _(POST /api/hivecloud/mdfe/xml)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `ids` | string[] | Sim | Lista de ids dos documentos (o campo `id` retornado nas listagens). |
| `empresa_id` | string | Não | empresaId (empresa emitente). 1 de N, veja hivecloud_list_empresas. Omitido = empresa padrão da conexão / primeira disponível. |
| `account` | string | Não | Quando há múltiplas contas HiveCloud conectadas: id/label da conexão. Veja hivecloud_list_accounts. |

#### `hivecloud_nfe_info`

Consulta os dados de uma NF-e pela chave de acesso (44 dígitos) via emissor: remetente e destinatário (já resolvidos no cadastro), valor da carga, pesos, volumes e produto predominante. _(POST /api/hivecloud/nfe/info)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `chave` | string | Sim | Chave de acesso da NF-e (44 dígitos). |
| `empresa_id` | string | Não | empresaId (empresa emitente). 1 de N, veja hivecloud_list_empresas. Omitido = empresa padrão da conexão / primeira disponível. |
| `account` | string | Não | Quando há múltiplas contas HiveCloud conectadas: id/label da conexão. Veja hivecloud_list_accounts. |
| `empresa_ids` | string[] | Não | Bulk mode: multiple values for empresa_id |

#### `hivecloud_relatorio_viagens`

Relatório consolidado de viagens (MDF-e) por período: contagem por mês, ranking por placa e por motorista, com filtros por placa e/ou motorista (CPF ou nome) e faturamento opcional (soma do valorTotal _(POST /api/hivecloud/relatorio/viagens)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `empresa_ids` | string[] | Não | Empresas MDF-e a consolidar (UUID, nome ou CNPJ). Omitido = TODAS as empresas do ambiente MDF-e. |
| `data_inicial` | string | Não | Data de emissão inicial (YYYY-MM-DD). |
| `data_final` | string | Não | Data de emissão final (YYYY-MM-DD). |
| `placa` | string | Não | Filtra pela placa do veículo de tração (aceita com ou sem hífen, ex. ANX6H66). |
| `motorista` | string | Não | Filtra por condutor: CPF (com ou sem pontuação) ou nome. |
| `incluir_cancelados` | boolean | Não | Default false: MDF-e cancelados ficam fora da contagem. |
| `incluir_faturamento` | boolean | Não | Soma o valorTotalFrete dos CT-e vinculados (ranking de faturamento por caminhão). Um pouco mais lento. |
| `account` | string | Não | Quando há múltiplas contas HiveCloud conectadas: id/label da conexão. Veja hivecloud_list_accounts. |

#### `hivecloud_sefaz_status`

Status do serviço da SEFAZ para a empresa (se o servidor da Fazenda está em operação). _(POST /api/hivecloud/sefaz/status)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `empresa_id` | string | Não | empresaId (empresa emitente). 1 de N, veja hivecloud_list_empresas. Omitido = empresa padrão da conexão / primeira disponível. |
| `account` | string | Não | Quando há múltiplas contas HiveCloud conectadas: id/label da conexão. Veja hivecloud_list_accounts. |
| `empresa_ids` | string[] | Não | Bulk mode: multiple values for empresa_id |

---

Este MCP também funciona via **conexão MCP** (Claude / Cursor) em `https://api.mcp.ai/p_hivecloud` — veja o [README](../../README.md). A skill acima é pra consumir a **REST API** direto (agente próprio / código).
