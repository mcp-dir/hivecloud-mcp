# Ferramentas

HiveCloud CT-e / MDF-e expõe 27 ferramentas.

### 1. `hivecloud_list_accounts`
**Input**: `account` (opcional)

Lista as contas HiveCloud conectadas a este install (cada usuário+ambiente = uma conta).

### 2. `hivecloud_list_empresas`
**Input**: `account` (opcional)

Lista as empresas emitentes do ambiente (id, nome, cnpj).

### 3. `hivecloud_list_ctes`
**Input**: `empresa_id` (opcional), `pageSize` (opcional), `pageNumber` (opcional), `data_inicial` (opcional), `data_final` (opcional), `account` (opcional), `empresa_ids` (opcional)

Lista os CT-e (Conhecimento de Transporte eletrônico) da empresa, paginado, com filtro por data de emissão.

### 4. `hivecloud_get_cte`
**Input**: `id`, `empresa_id` (opcional), `account` (opcional), `ids` (opcional), `empresa_ids` (opcional)

Detalha um CT-e específico pelo id.

### 5. `hivecloud_cte_dacte`
**Input**: `ids`, `empresa_id` (opcional), `account` (opcional)

Gera o PDF do DACTE de um ou mais CT-e autorizados e devolve a URL de download (temporária).

### 6. `hivecloud_cte_xml`
**Input**: `ids`, `empresa_id` (opcional), `account` (opcional)

Exporta o XML de um ou mais CT-e (zip) e devolve a URL de download (temporária).

### 7. `hivecloud_nfe_info`
**Input**: `chave`, `empresa_id` (opcional), `account` (opcional), `empresa_ids` (opcional)

Consulta os dados de uma NF-e pela chave de acesso (44 dígitos) via emissor: remetente e destinatário (já resolvidos no cadastro), valor da carga, pesos, volumes e produto predominante.

### 8. `hivecloud_cte_criar_de_nfe`
**Input**: `nfe_chaves`, `valor_frete`, `tomador` (opcional), `responsavel_frete` (opcional), `cfop_codigo` (opcional), `cfop_natureza` (opcional), `produto_predominante` (opcional), `observacao` (opcional), `template_cte_id` (opcional), `empresa_id` (opcional), `account` (opcional), `template_cte_ids` (opcional), `empresa_ids` (opcional)

Cria um RASCUNHO de CT-e a partir de uma ou mais chaves de NF-e (mesmo remetente e destinatário).

### 9. `hivecloud_list_dces`
**Input**: `empresa_id` (opcional), `pageSize` (opcional), `pageNumber` (opcional), `account` (opcional), `empresa_ids` (opcional)

Lista as DC-e (Declaração de Conteúdo eletrônica) da empresa, paginado.

### 10. `hivecloud_list_inutilizacoes`
**Input**: `empresa_id` (opcional), `pageSize` (opcional), `pageNumber` (opcional), `account` (opcional), `empresa_ids` (opcional)

Lista as inutilizações de numeração de CT-e da empresa, paginado.

### 11. `hivecloud_sefaz_status`
**Input**: `empresa_id` (opcional), `account` (opcional), `empresa_ids` (opcional)

Status do serviço da SEFAZ para a empresa (se o servidor da Fazenda está em operação).

### 12. `hivecloud_mdfe_empresas`
**Input**: `account` (opcional)

Lista as empresas emitentes do ambiente de MDF-e (o MDF-e tem ambiente e empresas PRÓPRIOS, distintos do CT-e).

### 13. `hivecloud_list_mdfes`
**Input**: `empresa_id` (opcional), `pageSize` (opcional), `pageNumber` (opcional), `data_inicial` (opcional), `data_final` (opcional), `account` (opcional), `empresa_ids` (opcional)

Lista os MDF-e (Manifesto Eletrônico de Documentos Fiscais) da empresa, paginado (número, série, dataEmissao, statusMdfe, UF de carregamento/descarregamento, CIOT).

### 14. `hivecloud_get_mdfe`
**Input**: `id`, `empresa_id` (opcional), `account` (opcional), `ids` (opcional), `empresa_ids` (opcional)

Detalha um MDF-e pelo id: placa do veículo (dadosVeiculo), condutores (nome/CPF), CIOT, documentos vinculados (chaves de CT-e/NF-e), UFs, valor e peso da carga, status e protocolos.

### 15. `hivecloud_mdfe_damdfe`
**Input**: `ids`, `empresa_id` (opcional), `account` (opcional)

Gera o PDF do DAMDFE de um ou mais MDF-e e devolve a URL de download (temporária).

### 16. `hivecloud_mdfe_xml`
**Input**: `ids`, `empresa_id` (opcional), `account` (opcional)

Exporta o XML de um ou mais MDF-e (zip) e devolve a URL de download (temporária).

### 17. `hivecloud_relatorio_viagens`
**Input**: `empresa_ids` (opcional), `data_inicial` (opcional), `data_final` (opcional), `placa` (opcional), `motorista` (opcional), `incluir_cancelados` (opcional), `incluir_faturamento` (opcional), `account` (opcional)

Relatório consolidado de viagens (MDF-e) por período: contagem por mês, ranking por placa e por motorista, com filtros por placa e/ou motorista (CPF ou nome) e faturamento opcional (soma do valorTotalFrete dos CT-e vi…

### 18. `hivecloud_list_veiculos`
**Input**: `empresa_id` (opcional), `pageSize` (opcional), `pageNumber` (opcional), `account` (opcional), `empresa_ids` (opcional)

Lista os veículos cadastrados (placa, motorista, reboque, tara), usados no MDF-e, paginado.

### 19. `hivecloud_list_motoristas`
**Input**: `empresa_id` (opcional), `pageSize` (opcional), `pageNumber` (opcional), `account` (opcional), `empresa_ids` (opcional)

Lista os motoristas/condutores cadastrados (nome, cpf, cnh), usados no MDF-e, paginado.

### 20. `hivecloud_cte_emitir`
**Input**: `ids`, `empresa_id` (opcional), `account` (opcional)

ATO FISCAL REAL: transmite um ou mais CT-e à SEFAZ (por id).

### 21. `hivecloud_cte_cancelar`
**Input**: `ids`, `empresa_id` (opcional), `account` (opcional)

ATO FISCAL REAL: cancela um ou mais CT-e autorizados (por id) junto à SEFAZ.

### 22. `hivecloud_cte_excluir`
**Input**: `ids`, `empresa_id` (opcional), `account` (opcional)

Exclui um ou mais CT-e (rascunhos/rejeitados, por id).

### 23. `hivecloud_cte_averbar`
**Input**: `ids`, `empresa_id` (opcional), `account` (opcional)

Averba (registra o seguro de carga) um ou mais CT-e (por id).

### 24. `hivecloud_cte_carta_correcao`
**Input**: `cte_id`, `correcoes`, `empresa_id` (opcional), `account` (opcional), `cte_ids` (opcional), `empresa_ids` (opcional)

ATO FISCAL REAL: emite uma carta de correção (CC-e) para um CT-e autorizado.

### 25. `hivecloud_mdfe_emitir`
**Input**: `ids`, `empresa_id` (opcional), `account` (opcional)

ATO FISCAL REAL: transmite um ou mais MDF-e à SEFAZ (por id).

### 26. `hivecloud_mdfe_encerrar`
**Input**: `ids`, `empresa_id` (opcional), `account` (opcional)

ATO FISCAL REAL: encerra um ou mais MDF-e (por id) após o fim da viagem.

### 27. `hivecloud_mdfe_cancelar`
**Input**: `ids`, `empresa_id` (opcional), `account` (opcional)

ATO FISCAL REAL: cancela um ou mais MDF-e (por id) junto à SEFAZ.

## Prompts de exemplo

```
Liste os CT-e emitidos este mês da empresa
Qual o status do serviço da SEFAZ agora?
Quantas viagens a placa ANX6H66 fez no trimestre?
```
