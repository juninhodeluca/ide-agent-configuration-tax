# Perfil de composição PBoM para IDEs — rascunho 0.1

**Proposta deste repositório, sem implementação de captura.** O [exemplo JSON](../examples/pbom.example.json) é sintético. Não é saída de um produto, um padrão aprovado ou um documento compatível com a especificação EqoAI.

## Antecedentes e escopo

O [projeto EqoAI/pbom-spec](https://github.com/EqoAI/pbom-spec) usa o termo Prompt Bill of Materials para registros de interações de LLM. Reconhecemos esse antecedente. A contribuição aqui é descrever necessidades da resolução de contexto de agentes em IDEs: gatilhos, fontes candidatas, exclusões, papéis observados, transformações e lacunas.

O perfil não deve substituir SBOMs de software, controles de execução ou verificação do resultado. Um manifesto descreve uma composição; não obriga o modelo a obedecer a ela.

Namespace experimental: `urn:ide-agent-pbom:0.1-draft`. Uma futura integração com EqoAI exigirá definir mapeamento de campos, semântica de extensões, canonicalização e validação. O exemplo atual não deve ser passado como se já satisfizesse esse contrato.

## Dois níveis de registro

**Descritor de ambiente:** cliente, extensões pertinentes, harness, modelo solicitado, políticas, snapshots de configuração e fontes disponíveis. Atualiza quando houver mudança material.

**Recibo de requisição:** referências ao descritor, componentes realmente considerados para aquela chamada, inclusão ou exclusão, transformações, uso e observabilidade. Deve existir um recibo por chamada, inclusive para subagentes e compactação quando observáveis.

Um catálogo de tudo que está instalado não substitui o segundo nível. Do mesmo modo, um recibo do lado cliente não prova que o servidor recebeu exatamente a mesma composição.

## Estados e relações

Cada componente tem `id`, `kind`, `state`, `origin`, `activation`, `transport_role`, `fingerprint`, `token_measurement` e `visibility`.

Estados de composição:

- `included`: incluído no limite observado, identificado no recibo.
- `excluded`: candidato conhecido que não entrou; informar motivo.
- `unknown`: o registrador não pode determinar sua presença ou conteúdo.

Disponibilidade, instalação, habilitação e elegibilidade pertencem ao descritor e à ativação; não devem ser confundidas com envio. Cumprimento de instrução pertence a evidência de comportamento posterior e deve ser registrado separadamente.

As relações formam um grafo: `discovered_from`, `selected_by`, `transformed_from`, `included_in` e `decided_by`. Um componente derivado deve apontar para seu original, sem substituir silenciosamente sua identidade.

## Origem e autoridade

`origin` informa tipo de fonte, escopo, publicador, versão ou commit, e referência sanitizada. Caminhos absolutos, contas e endereços privados não são necessários em um recibo público.

`declared_authority` registra uma alegação do conteúdo quando relevante. `transport_role` registra o papel realmente observado na requisição. `policy_decisions` identifica a regra que resolveu aplicação e precedência. Esses três campos não devem ser tratados como equivalentes.

Não inventar um ranking universal para VS Code, Copilot e Codex. Versão e harness precisam acompanhar a política. Se o papel de transporte não é observável, usar `null` e uma razão explícita.

## Transformações

Cada transformação informa entradas e saídas, operador e versão, motivo, momento e método de fingerprint. Exemplos: resumo de histórico, compressão de saída, resolução de referência e truncamento.

Uma transformação de resultado de ferramenta não deve ser registrada como alteração da mensagem do usuário. Uma seleção de referência não deve ser descrita como envio integral do diretório. O recibo deve preservar essa granularidade.

Hash diferente detecta diferença de bytes quando há observação confiável de ambos. Não prova erro nem perda de significado. A avaliação de integridade semântica pertence a invariantes verificáveis e ao benchmark.

## Tokens, cobertura e lacunas

`token_measurement` contém valor ou `null`, tokenizer/contador e origem: provedor, cliente, estimativa local ou desconhecida. Métricas por componente podem não somar exatamente ao total serializado; registrar método de atribuição e resíduo.

`usage` pode conter entrada, parcela cacheada, saída e parcela de raciocínio, respeitando a semântica do fornecedor. Não preencher lacunas com zero. Campos de cache e raciocínio que sejam subconjuntos não devem ser adicionados novamente ao total.

`visibility` e `coverage` declaram o limite capturado: visualização do cliente, saída serializada, recepção pelo provedor ou resposta de contabilização. Partes proprietárias podem ter somente um identificador de versão ou nenhuma informação. `partial` não significa completo e `opaque` não significa ausente.

## Integridade do registro

Uma implementação futura deverá definir canonicalização, ordenação, codificação, normalização, algoritmo e proteção contra reescrita ou truncamento de histórico. Esta versão não define uma canonicalização normativa e não fornece assinatura.

Uma cadeia de hashes sem âncora externa confiável não garante que toda a cadeia não tenha sido reescrita. Assinatura, identidade e retenção precisam de um modelo de confiança explícito. Mesmo uma atestação correta não demonstra segurança do conteúdo ou obediência do modelo.

O exemplo inclui fingerprints SHA-256 somente de textos sintéticos públicos, cujos bytes são especificados nos campos de exemplo. Não usa hashes inventados de documentos reais nem representa dados ocultos como observados.

## Privacidade e custo operacional

Minimizar coleta e retenção. Evitar segredos, conteúdo de terceiros e caminhos pessoais. Um hash de uma frase previsível pode permitir testes de adivinhação; hashing não anonimiza o conteúdo. Quando necessário, usar compromissos ou HMACs com gestão apropriada de chaves e deixar claro o custo para verificação externa.

Produzir o recibo no host e oferecê-lo sob demanda. Não anexá-lo integralmente a cada prompt por padrão. Medir tempo de coleta, armazenamento, renderização e interpretação. O resultado útil é um diagnóstico mais rápido e correto com custo total aceitável.

## Critérios para uma futura implementação

1. Demonstrar ligação entre um recibo e uma chamada, inclusive retries e subagentes.
2. Distinguir fonte candidata de fonte enviada e registrar exclusões explicáveis.
3. Mostrar transformação antes/depois de um artefato sintético, com fingerprints reproduzíveis.
4. Representar componente opaco e medição desconhecida sem números fictícios.
5. Resolver uma pergunta diagnóstica e medir seu custo frente ao fluxo existente.
6. Documentar modelo de confiança, política de redação e limites de cobertura.

Esses critérios são trabalho futuro, não funcionalidades já presentes neste repositório.
