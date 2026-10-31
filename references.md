# Fontes primárias e alcance das afirmações

Corte documental e consulta: **31 de outubro de 2026**. URLs de documentação podem mudar. Este registro não é uma revisão sistemática e não fornece snapshots integrais de materiais de terceiros. Referências a produtos descrevem o escopo documentado, sem demonstrar execução no ambiente das capturas.

## Documentação oficial dos produtos e do protocolo

| ID | Fonte | Uso e limite |
| --- | --- | --- |
| D01 | Microsoft. [Understand agent customization](https://code.visualstudio.com/docs/agents/concepts/customization) | Taxonomia de customizações e distinção entre orientação e execução pelo runtime. Não mede custo humano. |
| D02 | Microsoft. [AI settings reference](https://code.visualstudio.com/docs/agents/reference/ai-settings) | Identificação de mecanismos e escopos. Padrões da documentação não substituem os estados visíveis nas imagens. |
| D03 | Microsoft. [Understand context in AI agents](https://code.visualstudio.com/docs/agents/concepts/context) | Composição do contexto e compactação. Não quantifica perda de informação no caso motivador. |
| D04 | Microsoft. [Debug chat interactions](https://code.visualstudio.com/docs/agents/agent-troubleshooting/chat-debug-view) | Instrumento existente para inspecionar interações onde suportado. Não é promessa de captura de todos os componentes de servidor. |
| D05 | Microsoft. [User and workspace settings](https://code.visualstudio.com/docs/configure/settings) | Configuração e escopos da IDE. Não define, por si só, a autoridade das mensagens do modelo. |
| D06 | Microsoft. [Settings Sync](https://code.visualstudio.com/docs/configure/settings-sync) | Referência para investigar sincronização dentro do escopo do produto. Não comprova o episódio Desktop/Web do Codex. |
| D07 | OpenAI. [Custom instructions with AGENTS.md](https://learn.chatgpt.com/docs/agent-configuration/agents-md) | Descoberta global e por diretório, overrides e limite de tamanho. Não autoriza inferir um papel de transporte a partir do título de um arquivo. |
| D08 | OpenAI. [Config basics](https://learn.chatgpt.com/docs/config-file/config-basic) | Camadas de configuração, confiança e restrições de políticas. Não deve ser confundida com uma hierarquia universal de instruções. |
| D09 | OpenAI. [Agent approvals & security](https://learn.chatgpt.com/docs/agent-approvals-security) | Controles de execução e risco de instruções não confiáveis. Não diagnostica um ataque nas capturas. |
| D10 | OpenAI. [Observability and usage](https://developers.openai.com/api/docs/guides/agents-api/observability) | Semântica das categorias de uso e limites de contabilização da API descrita. Não representa automaticamente cobrança de assinaturas de IDE. |
| D11 | Model Context Protocol. [Architecture, edição 2025-06-18](https://modelcontextprotocol.io/specification/2025-06-18/architecture/index) | Responsabilidades do host e separação entre clientes e servidores. Usamos uma edição identificada, sem apresentá-la como a versão mais recente do protocolo. |
| D12 | Hugging Face. [Pickle Scanning](https://huggingface.co/docs/hub/security-pickle) | Risco da desserialização de pickle e limites de proveniência. Sustenta a analogia limitada; não demonstra exploração de um agente em IDE. |

Os endereços antigos `developers.openai.com/codex/guides/agents-md/` e a navegação de configuração redirecionaram para páginas em `learn.chatgpt.com`. As referências acima usam os destinos consultados. Para D02, também foi consultada a versão Markdown disponibilizada pelo próprio site.

## Antecedentes do PBoM

| ID | Fonte | Uso e limite |
| --- | --- | --- |
| P01 | NTIA. [The Minimum Elements for a Software Bill of Materials](https://www.ntia.gov/report/2021/minimum-elements-software-bill-materials-sbom), 12/07/2021 | Base da analogia de componentes e relações. O relatório não padroniza um PBoM para IDEs. |
| P02 | EqoAI. [pbom-spec — README](https://github.com/EqoAI/pbom-spec/blob/main/README.md) | Antecedente explícito do termo e de registros de interações com fingerprints. O perfil deste repositório é independente e não declara compatibilidade. |

P02 foi consultado pelo conteúdo do README no ramo padrão. O SHA de blob Git retornado foi `b7799098d1cec9722d68e01c85510ae83ef219d9`; ele identifica os bytes recuperados, **não é um SHA de commit**. O texto do projeto descreve limites de assinatura, autoria e âncora externa. Não usamos sua autodescrição de “standard” como evidência de padronização institucional ou adoção ampla.

Não reivindicamos ter criado a expressão Prompt Bill of Materials. Também não realizamos levantamento exaustivo de todas as iniciativas relacionadas a AI-BOM, ML-BOM ou proveniência de prompts.

## Estudos primários de produtividade

| ID | Fonte | Uso e limite |
| --- | --- | --- |
| E01 | Peng, S.; Kalliamvakou, E.; Cihon, P.; Demirer, M. [The Impact of AI on Developer Productivity: Evidence from GitHub Copilot](https://arxiv.org/abs/2302.06590), 2023. DOI: [10.48550/arXiv.2302.06590](https://doi.org/10.48550/arXiv.2302.06590) | Experimento com tarefa de servidor HTTP em JavaScript. Não estima o custo isolado de configuração de agentes atuais. |
| E02 | Becker, J.; Rush, N.; Barnes, B.; Rein, D. [Measuring the Impact of Early-2025 AI on Experienced Open-Source Developer Productivity](https://metr.org/blog/2025-07-10-early-2025-ai-experienced-os-dev-study/), METR, 10/07/2025 | Experimento com desenvolvedores experientes em seus próprios projetos. Resultado histórico e contextual, não efeito universal em 2026. |
| E03 | Becker, J.; Rush, N.; Cunningham, T.; Rein, D.; Mahamud, K. [We are Changing our Developer Productivity Experiment Design](https://metr.org/blog/2026-02-24-uplift-update/), METR, 24/02/2026 | Atualização com ressalvas sobre seleção e medição. Impede tratar estimativas anteriores como retrato corrente sem qualificação. |

O paper apresenta os resultados de E01 e E02 como relatados pelos autores e os contextualiza com E03. Não combina percentuais de desenhos diferentes nem atribui os resultados ao mecanismo de configuração aqui proposto.

## Material fornecido pelo autor

| ID | Material | Alcance |
| --- | --- | --- |
| O01 | Nove capturas de configurações, catalogadas como S01–S09 | Estados visíveis e texto parcial de interface, sem versão exata ou prova de uso por requisição |
| O02 | Captura de personalização S10 | Texto de promessa de sincronização e instruções visíveis na Web, sem par Desktop instrumentado |
| R01 | Trechos relevantes da conversa “Corrija este e-mail” | Motivação e relatos do autor; respostas anteriores de assistente não são tomadas como confirmação factual |

O [catálogo](evidence/README.md) e o [manifesto de arquivos](evidence/manifest.json) preservam a ligação entre rótulos, nomes originais e fingerprints. Não publicamos a conversa inteira, que inclui assuntos alheios ao paper.

## Mapa resumido de sustentação

- Famílias de configuração e diferenças de escopo: O01, D01, D02, D07 e D08.
- Contexto, compactação e observabilidade disponível: D03, D04 e D10.
- Proveniência, controle de execução e analogia de confiança: D09, D11 e D12; a síntese de integridade é proposta do paper.
- Antecedente e perfil PBoM: P01 e P02; os campos específicos para IDEs são proposta independente.
- Cautela sobre produtividade: E01–E03; o modelo econômico e os cenários são construção analítica e sintética deste trabalho.
- Crescimento diário, reescrita da mensagem, defeito de sincronização e perda causal no caso: **não estabelecidos por estas fontes**.
