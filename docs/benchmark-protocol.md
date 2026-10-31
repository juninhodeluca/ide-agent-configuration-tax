# Protocolo de benchmark — versão 0.1.0

**Proposta para execução futura. Nenhum experimento deste protocolo foi executado.**

Este documento operacionaliza o [paper](../paper.md). O protocolo pode ser adaptado antes do estudo; depois do pré-registro, mudanças devem aparecer como desvios, com justificativa. Os CSVs do repositório contêm somente cabeçalhos, sem resultados.

## 1. Perguntas e estimandos

Pergunta principal: para uma entrega com qualidade pré-definida, qual é a diferença de capacidade humana consumida ao usar um agente, incluindo implantação, operação e manutenção?

Pergunta de mecanismo: uma configuração governada com proveniência explícita reduz auditoria e recuperação o suficiente para compensar seu próprio custo?

| Contraste | Interpretação pretendida |
| --- | --- |
| A versus H | Efeito do pacote padrão com IA no domínio estudado |
| G versus H | Efeito do pacote com governança, incluindo seu custo |
| G versus A | Efeito do pacote de governança, não apenas do manifesto isolado |
| Ablação dentro de A ou G | Efeito de um mecanismo com demais condições controladas |

**H:** sem IA generativa; ferramentas convencionais, documentação e busca permitidas conforme regra igual para todos. **A:** agente com padrões documentados do produto. **G:** o mesmo agente com fontes e políticas explicitadas, snapshot efetivo e recibos disponíveis no limite de observação. Não usar mudança de modelo ou remoção de verificações para favorecer G.

Desfecho primário: atenção humana mais espera ponderada até entrega aceita, sob orçamento por tarefa. Reportar conjuntamente taxa de aceitação, tarefas interrompidas e qualidade. Implantação e manutenção compartilhadas serão alocadas em cenários de horizonte explícitos. Tempo de calendário e custo financeiro são desfechos separados.

## 2. Tarefas e critérios de aceitação

Usar três estratos:

1. Correção localizada, com comportamento errado bem especificado.
2. Mudança de contrato, envolvendo chamadores ou consumidores.
3. Trabalho entre componentes, exigindo navegação e entendimento do projeto.

Para cada tarefa, congelar enunciado, commit inicial, dados permitidos, critérios de aceitação, orçamento e material de avaliação. O conjunto de verificações de referência fica fora do material acessível ao agente e ao participante. Evitar tarefas que premiem apenas geração de código volumoso.

A avaliação deve combinar verificações de comportamento com revisão de adequação e regressões. Revisores não devem conhecer o braço experimental quando isso for viável. Se um artefato revelar a ferramenta usada, registrar perda de cegamento. O nível de exigência é igual para H, A e G.

Nunca remover da análise uma falha porque o agente não conseguiu terminar. Publicar taxa de aceitação por orçamento e tempo consumido em falhas. A comparação de tempo apenas entre sucessos é secundária e condicionada a um resultado pós-tratamento.

## 3. Participantes, desenho e amostra

Registrar experiência com linguagem, projeto, produto e agentes. Separar familiaridade com a IDE de familiaridade com o repositório. O convite não deve selecionar apenas entusiastas ou apenas usuários frustrados.

Piloto proposto: oito participantes, seis tarefas distintas por participante, duas por condição, com ordem balanceada. As 48 execuções propostas não são 48 participantes independentes e não constituem justificativa de poder estatístico.

Após o piloto, definir diferença mínima de interesse e calcular a amostra do estudo principal usando variabilidade e correlação dentro de participante e tarefa. Fixar a regra antes de observar os resultados confirmatórios. Se a amostra viável for pequena, declarar estudo exploratório e publicar incerteza.

Usar randomização da condição e da ordem, por blocos de experiência. Um quadrado latino ou desenho balanceado equivalente pode controlar ordem. Cada participante recebe tarefas distintas: repetir a mesma solução entre braços produz aprendizado. Variantes precisam ser calibradas no piloto, com versão e hipótese de equivalência registradas.

Registrar recusas de participação, abandono e tarefas que candidatos não aceitam realizar sem IA. A atualização metodológica da [METR em 2026](https://metr.org/blog/2026-02-24-uplift-update/) torna especialmente relevante examinar seleção e trabalho concorrente. Não inferir ausência de ganho entre quem recusou o experimento a partir de quem aceitou.

## 4. Fixação do ambiente

Antes de cada bloco, registrar:

- Cliente/IDE, canal, versão e sistema operacional.
- Extensões pertinentes, versões e identificadores.
- Harness e versão; local, remoto ou hospedado.
- Modelo solicitado, modelo resolvido quando observável, revisão e esforço de raciocínio.
- Commit inicial do projeto, diretório de trabalho e perfil.
- Fontes de instrução aplicáveis, políticas e snapshots de configuração.
- Ferramentas disponíveis, aprovações e restrições de execução.
- Estado de memória, indexação, cache e histórico conhecido.

Restaurar o mesmo commit inicial em cópias isoladas por execução. Começar sessões novas e remover memórias específicas da tarefa quando o produto permitir, sem alterar política de segurança. Não prometer isolamento que o cliente não oferece: registrar o estado residual.

Manter modelo e ferramentas constantes nas comparações de mecanismo. Se não houver o mesmo modelo em dois produtos, rotular a comparação como efeito do pacote, sem atribuir causalidade isolada à IDE ou ao harness.

Registrar tráfego concorrente, latência e indisponibilidade quando observáveis. Separar blocos de cache quente e frio ou tratá-los como estratos; uma conversa nova não garante cache frio no provedor. Não afirmar que uma condição de cache foi controlada sem evidência.

## 5. Linha do tempo e classificação do trabalho

No estudo controlado inicial, cada participante trabalha em uma tarefa por vez. Registrar transições de categoria com horário UTC e um relógio monotônico para duração, quando disponível.

| Categoria | Inclui | Exclui |
| --- | --- | --- |
| Execução | Implementação, formulação de pedidos e interpretação necessária ao avanço da tarefa | Ajustes persistentes de configuração |
| Configuração | Seleção e alteração de opções específicas para aquela tarefa | Implantação compartilhada já registrada em F |
| Auditoria | Identificar fontes, escopos, resolução e transformações | Revisar correção do código produzido |
| Verificação | Avaliar atendimento da tarefa e qualidade do resultado | Corrigir um problema já identificado |
| Retrabalho | Reparar entrega ou tentativa inadequada | Aprendizado inicial compartilhado |
| Espera exclusiva | Intervalo sem ação ativa nessa tarefa enquanto ela está bloqueada | Atenção já registrada em outra categoria |

Nenhum segundo de atenção humana deve pertencer a duas categorias. Manutenção compartilhada deve ficar em um ledger de horizonte, alocada uma única vez. Se uma investigação já está em auditoria da tarefa, não registrá-la novamente como manutenção.

Publicar o peso de oportunidade da espera, α, e sua justificativa. Sempre mostrar sensibilidade em α = 0, α = 0,25 e α = 1, sem afirmar que qualquer valor corresponde universalmente ao uso real. Em etapa ecológica com tarefas simultâneas, não somar tempos de calendário sobrepostos como se fossem atenção exclusiva.

## 6. Requisições, tokens e PBoM

Associar cada chamada a `run_id`, `request_id` e `agent_id`, incluindo chamadas de compactação, retries e subagentes. Um retry é outra linha; evitar somar o uso agregado de uma sessão ao mesmo uso já contabilizado em suas chamadas.

Para cada métrica, declarar se ela veio do provedor, cliente, tokenizer local ou estimativa. Separar consumo acumulado de componentes únicos. As categorias de contexto devem usar uma regra de atribuição publicada e reconhecer o resíduo de serialização/tokenização.

Não somar `cached_input_tokens` novamente a `input_tokens`, nem `reasoning_tokens` a `output_tokens`, quando forem subconjuntos no contrato do provedor. Não derivar custo de assinatura por uma tabela de preços de API. Se não existir captura de uso, deixar vazio e marcar desconhecido.

A [Chat Debug view do VS Code](https://code.visualstudio.com/docs/agents/agent-troubleshooting/chat-debug-view) pode servir de instrumento onde suportada. Registrar exatamente qual limite foi observado: visualização do cliente, serialização de saída, recebimento pelo provedor ou contabilização retornada. Esses limites não são equivalentes.

O PBoM proposto é um registro de observabilidade do host. Se for necessário instrumentar um proxy ou extensão, documentar sua versão e medir seu próprio custo. Não interceptar contas, tráfego ou projetos de terceiros sem autorização. Não solicitar divulgação de prompts privados do provedor como condição para participar; declarar a opacidade.

## 7. Ablações e tarefas diagnósticas

Executar após o estudo principal, como fase pré-registrada ou exploratória identificada:

- Contexto implícito ligado/desligado, com tarefa e editor controlados.
- Inclusão automática de instruções pertinente, com arquivos candidatos conhecidos.
- Compressão de saída ligada/desligada, preservando saídas brutas como referência autorizada.
- Recibos de composição disponíveis/indisponíveis para uma pergunta diagnóstica.

Se dois fatores forem estudados juntos, usar um desenho fatorial explícito e considerar sua interação. Não escolher combinações depois de ver qual favorece a hipótese.

Exemplos de tarefas diagnósticas: identificar qual regra acionou uma verificação; descobrir por que um arquivo foi incluído; explicar qual configuração venceu; localizar o que mudou entre dois snapshots. Medir tempo, acerto e número de superfícies consultadas.

Para compressão, preparar saídas com invariantes benignos relevantes ao trabalho: um código de erro, um arquivo modificado ou uma divergência de contrato. Medir preservação desses sinais e efeito na aceitação. Não presumir que menos bytes implica equivalência semântica.

Casos de conflito de instruções usam fixtures locais e inofensivas. Não usar segredos reais, exfiltração, redes externas ou alteração de sistemas compartilhados. A intenção é medir atribuição de autoridade e recuperação, não demonstrar exploração operacional.

## 8. Estudo longitudinal de drift

Proposta: acompanhar snapshots semanais durante oito a doze semanas, com versões e janelas de atualização registradas. A duração deve ser fixada antes da coleta; a proposta não afirma que mudanças ocorrerão toda semana.

Separar duas coortes quando viável: ambiente fixado e ambiente com atualizações planejadas. Para cada mudança, classificar conteúdo, resolução, política ou comportamento. Distinguir mudança deliberada, renomeação, valor padrão, migração e divergência inesperada.

A regra de contagem de opções deve fixar produtos, extensões, harnesses, maturidade e critérios de relevância. Publicar opções únicas, opções ativas e fontes efetivamente carregadas separadamente. Remoções e fusões contam tanto quanto adições.

Medir tempo de reaprendizado, diagnóstico e restauração após mudanças. Sem randomização de atualização, análise de diferenças tem limitações causais. Conectividade, novos modelos, tarefas e experiência acumulada são confundidores.

## 9. Plano de análise e divulgação

Pré-registrar desfecho primário, critérios de qualidade, orçamento, tamanho da amostra, exclusões, outliers, falhas, perdas e correções por comparações múltiplas, se aplicáveis. Publicar estimativas absolutas e relativas com intervalos de confiança. Considerar agrupamento por participante e tarefa.

Mostrar resultados por experiência, estrato de tarefa e fase de uso, sem transformar análises pequenas de subgrupos em conclusões firmes. Reportar implantação inicial, operação estabilizada e manutenção separadamente antes de amortizar.

Calcular break-even com a equação geral do paper e indicar o horizonte. Uma margem negativa no período observado não prova que ela permanecerá negativa; aprendizado ou atualização podem mudar o regime. Uma margem positiva de implementação não prova que o investimento total foi amortizado.

Publicar materiais sanitizados, dicionário, versões, desvios e instrumentos. Guardar registros privados em ambiente autorizado com prazo de retenção. Não publicar conteúdo bruto apenas para tornar a reprodução mais conveniente.

## 10. Condições de interpretação

O estudo sustentará afirmações apenas para população, tarefas, versões e horizonte observados. Não poderá, sozinho, provar uma tendência universal de perda de produtividade ou de aumento diário da configuração. Um resultado favorável a PBoM será um efeito medido do mecanismo aplicado, com seus custos, não prova de que todo produto precise do mesmo formato.
