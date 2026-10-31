# Coleta de benchmark: arquivos vazios e dicionário

**Não há execuções registradas.** [runs-template.csv](runs-template.csv) e [requests-template.csv](requests-template.csv) possuem apenas cabeçalhos. Não usar o exemplo PBoM ou os números sintéticos do paper como dados experimentais.

## Convenções comuns

Usar UTF-8 e CSV com vírgula e regras usuais de aspas. Números decimais usam ponto. Durações são em segundos; horários de eventos ou requisições, em UTC ISO 8601. Campos não observados ficam vazios, com razão em `protocol_deviation` ou cobertura. Zero exige observação de zero. Para H, tokens não aplicáveis ficam vazios.

Identificadores de participante devem ser pseudônimos sem tabela de identificação publicada. Identificadores de tarefa e versão devem remeter a artefatos sanitizados congelados no estudo.

## runs-template.csv — uma linha por tarefa e condição

| Campo ou grupo | Definição |
| --- | --- |
| `run_id` | Identificador único da tentativa experimental, mesmo se interrompida |
| `participant_id` | Pseudônimo do participante |
| `task_id`, `task_variant` | Tarefa e variante congeladas |
| `arm` | H, A ou G conforme protocolo |
| `harness`, `harness_version` | Runtime e versão, ou desconhecido explícito |
| `client_version`, `extension_version` | Versões do ambiente pertinentes ao experimento |
| `model_id`, `model_revision` | Modelo pedido/resolvido conforme documentação da coleta |
| `repo_commit`, `config_snapshot_id` | Estado inicial e snapshot efetivo |
| `sequence`, `cache_condition` | Ordem e condição observada ou desconhecida de cache |
| `status` | `completed`, `failed`, `timeout` ou `withdrawn` |
| `accepted` | `true`/`false` conforme avaliação; vazio se não avaliado |
| `wall_s` | Tempo de calendário da tentativa, sem somar sobreposição entre tarefas |
| `execution_active_s` | Atenção em implementação e interação de tarefa |
| `configuration_active_s` | Atenção em configurar a tentativa |
| `audit_active_s` | Atenção em identificar composição, origem e resolução |
| `verification_active_s` | Atenção em avaliar correção e critérios de aceitação |
| `rework_active_s` | Atenção em corrigir resultado inadequado |
| `exclusive_wait_s` | Espera sem atenção ativa já contada nessa tentativa |
| `wait_opportunity_weight` | α, de zero a um, com método e sensibilidade publicados |
| `setup_allocated_s` | Parcela de F atribuída ao horizonte escolhido |
| `maintenance_allocated_s` | Parcela de manutenção compartilhada, sem repetir C ou A |
| `input_tokens`, `cached_input_tokens` | Entrada total e seu subconjunto cacheado, se essa for a semântica da fonte |
| `output_tokens`, `reasoning_tokens` | Saída total e seu subconjunto de raciocínio, quando aplicável |
| `usage_observability` | `provider`, `client`, `estimated`, `partial`, `unknown` ou `not_applicable`, detalhado no relatório |
| `ai_incremental_cost`, `currency` | Custo incremental conhecido e moeda; vazio se não observável |
| `quality_score` | Escore sob rubrica pré-definida, acompanhado de aceitação binária |
| `protocol_deviation` | Desvio, cobertura ausente ou observação material |

As cinco categorias de atenção são exclusivas. Não incluir atenção ativa dentro de espera. Não adicionar F ou M novamente ao total se suas parcelas já tiverem sido somadas por execução. Publicar a regra de amortização e o número de tarefas do horizonte.

O total de tokens por execução deve agregar chamadas distintas do ledger. Não adicionar um agregado de sessão às mesmas requisições individuais. Quando parte das chamadas estiver invisível, marcar o total como parcial em vez de tratá-lo como completo.

## requests-template.csv — uma linha por chamada ao modelo

| Campo | Definição |
| --- | --- |
| `request_id`, `run_id` | Identidade da chamada e vínculo à execução |
| `agent_id` | Agente raiz ou subagente; não contém identidade pessoal |
| `parent_request_id` | Chamada que originou a subtarefa, quando a relação for conhecida |
| `timestamp_utc` | Início observado da chamada |
| `request_kind` | `task`, `retry`, `compaction`, `subagent` ou outra categoria documentada |
| `model_id`, `model_revision` | Identificação observada, distinguindo alias de revisão fixa |
| `input_tokens`, `cached_input_tokens`, `output_tokens`, `reasoning_tokens` | Contagens conforme semântica da fonte |
| `usage_source` | Provedor, cliente, estimativa local ou desconhecida |
| `capture_boundary` | Ponto da cadeia em que a informação foi observada |
| `pbom_record_id` | Recibo correspondente, se existente |
| `latency_s` | Latência observada dessa chamada |
| `cost_amount`, `currency` | Custo incremental atribuível conhecido, ou vazio |
| `coverage_note` | Lacunas, aproximações e indisponibilidades |

`parent_request_id` não autoriza inferir causalidade detalhada ou acesso ao conteúdo de outra chamada. A correlação deve vir do instrumento real, não de proximidade de horários.

## Dados complementares do estudo futuro

O estudo deve manter um ledger de implantação/manutenção compartilhada e uma linha do tempo de transições de atenção. Seus formatos precisam ser congelados no pré-registro antes da coleta. Esta versão entrega somente os dois templates centrais e não implementa um coletor.
