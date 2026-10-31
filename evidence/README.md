# Capturas, observações e limites

Dez arquivos recuperados da conversa fornecida pelo autor: nove imagens de opções do VS Code e uma captura adicional da personalização Web relacionada ao Codex. Esta é uma amostra selecionada, não um inventário completo da IDE.

As cópias abaixo mantêm os bytes dos anexos recebidos. Não houve recriação por IA, edição, novo recorte ou redação sobre as imagens. Os nomes originais, dimensões, tamanhos e SHA-256 estão em [manifest.json](manifest.json). Os nomes contêm a data 2026-10-31; isso não autentica relógio, fuso ou sequência de execução. O hash permite conferir identidade dos arquivos publicados, não a veracidade ou completude da captura original.

As versões da IDE/extensões, o sistema operacional da captura e o harness ativo em uma requisição não foram recuperados. Selos Experimental, Preview e Advanced descrevem a interface recebida. Não são uma classificação independente deste trabalho.

## S01 — inclusão de instruções

![S01: Include Applying Instructions e Include Referenced Instructions marcados](screenshots/s01-instruction-inclusion.png)

Ambas as opções aparecem marcadas. As descrições mencionam o agente Local. A primeira fala em correspondência de `applyTo`; a segunda, em instruções referenciadas. Não é possível identificar arquivos concretos enviados ao modelo ou presumir que outro harness aplicou as mesmas opções.

## S02 — skills, contexto implícito e AGENTS.md aninhado

![S02: Skill Adherence, contexto implícito, editor ativo e Nested Agents Md](screenshots/s02-skills-and-implicit-context.png)

Use Skill Adherence Prompt está marcado e menciona Local. Implicit Context: Enabled exibe `panel: always` e `terminal: always`. Include Active Editor está marcado e sua nota menciona Agent Host, como Copilot. Use Nested Agents Md Files está marcado, mas descreve listagem de instruções e carregamento sob demanda, quando há ferramenta de leitura disponível.

Esses textos não sustentam a conclusão de que todos os arquivos aninhados foram integralmente anexados a todas as requisições, nem que todos esses mecanismos estavam ativos no mesmo runtime.

## S03 — compressão de saída

![S03: Compress Output marcado com selo Preview](screenshots/s03-compress-output.png)

A opção está marcada. A descrição fala em pós-processar saída de ferramenta para reduzir tokens antes de enviá-la ao modelo, com exemplos de comandos. É evidência de um controle de transformação de resultados; não prova reescrita do texto digitado ou perda efetiva de informação.

## S04 — compactação do terminal desativada

![S04: Terminal Output Compaction desmarcado](screenshots/s04-terminal-compaction-disabled.png)

Caixa desmarcada, com selo Experimental. Sua descrição trata de compactar saída de comandos e preservar informação importante. A imagem não permite atribuir a esse mecanismo qualquer compactação ocorrida na sessão.

## S05 — capacidade de modelos, opção avançada

![S05: Model Capability Overrides e nota de uso para avaliação](screenshots/s05-model-capability-overrides.png)

Mostra um recurso avançado com configuração por identificador de modelo, referências a `family` e `thinkingHistory`, e link para `settings.json`. A descrição informa que o recurso se destina a avaliação, não à configuração regular de usuário final. Não há valor de override visível. Sua exposição contribui para a superfície apresentada, mas não prova necessidade de uso ou efeito sobre uma chamada.

## S06 — omissão de anexos desativada

![S06: Omit File Attachment Contents desmarcado](screenshots/s06-omit-attachments-disabled.png)

Omit File Attachment Contents está desmarcado, com selos Experimental e Advanced. Não há evidência de que conteúdo de anexos tenha sido omitido por essa opção no caso estudado.

## S07 — prompts alternativos e context editing desativados

![S07: prompts alternativos desmarcados e Context Editing em off](screenshots/s07-alternate-prompts-disabled.png)

As opções de prompt alternativo para Gemini Model F e GPT estão desmarcadas. Anthropic Context Editing: Mode está em `off`. A descrição apresenta modos de edição e alerta sobre efeitos de cache, mas esses modos não aparecem ativados. Não inferimos comportamento de modelos específicos nem tratamos seu texto como uma especificação atual de todos os provedores.

## S08 — modelo do Ask Agent, prompts por família e code search

![S08: campo de modelo preenchido, prompts Claude desmarcados e Code Search marcado](screenshots/s08-model-and-code-search.png)

O campo Ask Agent: Model contém `gpt-6-luna`. A área Additional Tools mostra um botão de inclusão, sem entradas legíveis na captura. As opções de prompt Claude Opus 5 e Claude Sonnet 5 estão desmarcadas. Codesearch: Agent: Enabled está marcado.

O identificador no campo é uma observação literal, não confirmação de disponibilidade geral, escolha de modelo em outra sessão ou modelo efetivamente resolvido pelo servidor.

## S09 — três opções Gemini desativadas

![S09: Reduced Tool Use Prompt, Get Changed Files Tool e Flash Prompt Additions desmarcados](screenshots/s09-gemini-options-disabled.png)

Gemini35 Flash Reduced Tool Use Prompt, Gemini3 Get Changed Files Tool e Gemini Flash Prompt Additions aparecem desmarcados. Parte das descrições está cortada à direita. Não reconstruímos o trecho ausente nem atribuímos efeito a recursos inativos.

## S10 — personalização Web e alegação de sincronização

![S10: instruções personalizadas para Codex com texto de sincronização desktop e web](screenshots/s10-web-personalization.png)

A tela mostra “Instruções para o Codex sincronizadas entre o desktop e a web” e uma área de instruções com o título GLOBAL AGENT — OPERATING SYSTEM. Trata-se de uma captura adicional, distinta das nove imagens de opções do VS Code.

O autor relatou que o Desktop exibia outro conteúdo. Sem par instrumentado do Desktop, identificação do objeto de armazenamento e teste controlado, o material sustenta uma expectativa de sincronização e um relato de divergência, não um bug reproduzido.

## Argumentos do diálogo preservados no paper

O autor questiona a carga de acompanhar opções, a inclusão de instruções sem compreensão de sua origem, transformações de contexto e o saldo de produtividade. O humor sobre uma função de “Full Model Setter” e a referência retórica a passar o dia configurando ilustram essa preocupação.

Os volumes de tokens e o caso de uso coletivo relatado na palestra permanecem relatos sem auditoria. Não se identificam o palestrante, a equipe ou a instituição. A analogia com modelos em Hugging Face é tratada com limites técnicos no paper.

As interpretações anteriores de assistente foram reavaliadas contra as capturas e as fontes primárias. Não foram promovidas a observações independentes.
