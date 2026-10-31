# A conta da configuração de agentes em IDEs

**Prompt Bill of Materials, proveniência, integridade do prompt, context/token overhead e produtividade em VS Code, Copilot e Codex.**

Um assistente pode economizar tempo ao implementar uma tarefa e devolver essa economia na forma de configuração, supervisão e manutenção. Este projeto transforma essa preocupação em definições verificáveis, um modelo de break-even e um protocolo de benchmark.

**Estado:** paper técnico de posição e proposta metodológica, versão 0.1.0, 31 de outubro de 2026. Não revisado por pares. **Não há resultados de benchmark próprios nesta versão.**

## Comece pelo paper

- [Paper completo em português, com abstract em inglês](paper.md).
- [Protocolo de benchmark](docs/benchmark-protocol.md): desenho experimental, ablações, controle de versões e análise.
- [Perfil proposto de Prompt Bill of Materials para IDEs](docs/pbom-profile.md) e [exemplo sintético em JSON](examples/pbom.example.json).
- [Evidências e legendas das dez capturas recuperadas](evidence/README.md), incluindo as nove imagens de opções do VS Code.
- [Fontes primárias e limites de cada referência](references.md).
- [Dicionário e planilhas CSV vazias para coleta](benchmark/data-dictionary.md).
- [Etapas concluídas e trabalho empírico futuro](ROADMAP.md).

## O que esta versão estabelece

As capturas mostram opções que afetam descoberta de instruções, contexto implícito, saídas de ferramentas, seleção de modelo e prompts específicos por família de modelo. Algumas se aplicam apenas ao agente Local; outras mencionam Agent Host. Uma opção visível não implica que ela tenha afetado uma requisição.

A documentação oficial reconhece diferentes mecanismos de customização e composição de contexto. Ela fundamenta o mapa técnico; as capturas documentam um ambiente particular. Os vínculos estão no [registro de fontes](references.md).

O paper propõe um PBoM por requisição: quais componentes foram considerados, incluídos, excluídos ou transformados; de onde vieram; por que foram ativados; qual autoridade foi realmente atribuída; e o que continua opaco. A proposta reconhece o projeto anterior [EqoAI/pbom-spec](https://github.com/EqoAI/pbom-spec) e **não reivindica a criação do termo nem compatibilidade com seu formato**.

## O que ainda é hipótese

Não demonstramos que opções sejam acrescentadas diariamente, que uma configuração tenha reescrito o texto digitado, que tenha ocorrido prompt injection, que Desktop e Web devam compartilhar o mesmo armazenamento, nem que a produtividade líquida de todos os usuários tenha caído.

Os relatos de quase seis bilhões de tokens individuais e de quatro bilhões em quatro meses para uma equipe de 80 pessoas são motivação qualitativa. Não são telemetria auditada, amostras comparáveis ou medidas de produtividade. Os números do break-even são sintéticos.

## Pergunta central

Quanto do ganho do agente permanece depois de pagar o custo de configurá-lo, compreender seu contexto efetivo, verificar o resultado, corrigir erros e acompanhar mudanças?

Para tarefas comparáveis e qualidade equivalente:

```text
ganho líquido = tempo humano de referência
              − trabalho humano com o agente
              − espera que realmente ocupa capacidade
              − configuração e auditoria
              − implantação e manutenção amortizadas
```

Tokens, custo financeiro, tempo de calendário e atenção humana são contabilizados separadamente. Mais tokens não significam mais trabalho aceito; menos tokens também não garantem melhor resultado.

## Como contribuir

Uma contribuição útil informa versões, agente/harness, modelo, configuração efetiva, tarefa, critério de aceitação, tempos e limites de observabilidade. Use os [modelos de coleta](benchmark/data-dictionary.md). Não envie segredos, conteúdo privado de projetos ou transcrições integrais sem autorização.

Esta publicação não abre issues nos repositórios da OpenAI, Microsoft ou VS Code. A discussão externa fica para uma etapa posterior.

## Autoria e uso

Juninho De Luca. Redação e pesquisa assistidas por IA, a partir de argumentos e capturas fornecidos pelo autor. A responsabilidade editorial é humana. Esta versão não representa a OpenAI, Microsoft, GitHub, Hugging Face ou METR.

Para citar, use o [CITATION.cff](CITATION.cff) e indique a versão ou o commit consultado. Nenhuma licença de reutilização foi escolhida nesta versão; marcas, documentação citada e interfaces de terceiros permanecem sob os direitos dos respectivos titulares.
