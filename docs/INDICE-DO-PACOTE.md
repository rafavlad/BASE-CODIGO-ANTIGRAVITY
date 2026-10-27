# Índice de skills da fundação de desenvolvimento web — Antigravity

A fonte normativa deste pacote é `AGENTS.md` e `.agents/skills/`. Use os links relativos abaixo; não mantenha cópias divergentes das mesmas skills em outras pastas.

## Como funciona

- `AGENTS.md` contém as regras permanentemente ativas e a matriz de carregamento por fase. É o roteador desta fundação, **não um arquivo pronto para copiar sem adaptação a projetos de clientes**.
- Cada skill fica em `.agents/skills/<nome>/SKILL.md` e possui frontmatter YAML `name` e `description`. O Antigravity descobre skills a partir de `.agents/skills/`; leia explicitamente o conteúdo completo das skills obrigatórias antes de agir.
- Os números de subseções dentro dos arquivos são identificadores internos de referência. Não exigem um documento mestre externo.
- `docs/MAPA-DE-LEITURA.md` é um ponto de entrada para navegação; não carrega arquivos automaticamente nem concede acesso técnico.
- `docs/MENSAGENS-DE-SESSAO.md` contém mensagens de preparação/retomada e lembretes de autorização. Não substitui `AGENTS.md` nem as skills normativas.
- `docs/REGISTRO-ALTERACOES.md` é o único histórico técnico cumulativo. Acrescente novas entradas ao final sem apagar as antigas e não inclua segredos, logs extensos, diffs completos ou snapshots.
- `docs/RELATORIO-DE-VALIDACAO.md` registra verificações estruturais e limitações. Uma validação documental não prova que as fases funcionam numa sessão real.
- `MANIFEST.md` lista tamanhos e hashes SHA-256 dos arquivos distribuídos, excluindo a si próprio.

## Skills e quando carregá-las

| Skill | Responsabilidade | Quando carregar |
|---|---|---|
| [principios-globais](../.agents/skills/principios-globais/SKILL.md) | Prioridades, escopo, integridade, continuidade e referências específicas por tarefa. | Início de toda tarefa. |
| [fases-e-autorizacoes](../.agents/skills/fases-e-autorizacoes/SKILL.md) | Fases, autorizações humanas, estados, portões de saída, relatórios e diagnóstico inicial. | Toda fase. |
| [seguranca-permissoes](../.agents/skills/seguranca-permissoes/SKILL.md) | Arquivos de ambiente, permissões do Antigravity, limites de isolamento e canário. | Toda fase; especialmente antes de permissões e da Fase 1B. |
| [arquitetura-stack](../.agents/skills/arquitetura-stack/SKILL.md) | Estrutura, tecnologias, TypeScript, testes, lint, scripts npm e `.gitignore`. | Fases 0, 1A e 1B; alterações estruturais. |
| [auditoria-dependencias](../.agents/skills/auditoria-dependencias/SKILL.md) | Auditoria npm, classificação, CLI, timeouts, agregação e testes. | Fases 0, 1A e 1B; manutenção da auditoria. |
| [ci-dependabot](../.agents/skills/ci-dependabot/SKILL.md) | GitHub Actions, CI, segurança e Dependabot. | Planejamento na Fase 0; configuração na Fase 1A/1B. |
| [interface-cliente-referencias](../.agents/skills/interface-cliente-referencias/SKILL.md) | Separação núcleo/cliente, componentes, páginas, formulários e análise segura de referências. | Planejamento na Fase 0; separação na Fase 1A; interface na Fase 1B. |
| [qualidade-acessibilidade](../.agents/skills/qualidade-acessibilidade/SKILL.md) | Testes, regressão, acessibilidade, responsividade, diff e verificação final. | Planejamento na Fase 0; Fases 1A/1B e conclusão de fases. |
| [modulos-opcionais](../.agents/skills/modulos-opcionais/SKILL.md) | Limites de backend, banco, autenticação, uploads, agendamento e integrações. | Fase 2 para documentar módulos futuros; implementação somente com autorização própria. |
| [git-integridade](../.agents/skills/git-integridade/SKILL.md) | Integridade do repositório, identidade Git, commits e proibições de ações remotas. | Toda fase; antes de ações Git com efeitos colaterais. |
| [documentacao-agents-md](../.agents/skills/documentacao-agents-md/SKILL.md) | Documentação obrigatória, `AGENTS.md` por cliente e registro cumulativo. | Fases 1A, 1B e 2; sempre que criar/revisar documentação. |
| [continuidade-sessoes](../.agents/skills/continuidade-sessoes/SKILL.md) | Resumos externos, retomada segura e sessões interrompidas. | Toda troca, pausa, encerramento ou retomada. |
| [aceitacao-final](../.agents/skills/aceitacao-final/SKILL.md) | Checklist e critérios de aceitação por fase. | Fases 0, 1A, 1B e 2. |

## Matriz resumida de carregamento

As cinco skills globais obrigatórias são `principios-globais`, `fases-e-autorizacoes`, `seguranca-permissoes`, `git-integridade` e `continuidade-sessoes`. Além delas, leia as skills temáticas abaixo.

| Fase | Skills temáticas adicionais | Limite da fase |
|---|---|---|
| **0 — inspeção** | `arquitetura-stack`, `auditoria-dependencias`, `ci-dependabot`, `interface-cliente-referencias`, `qualidade-acessibilidade`, `aceitacao-final` | Somente leitura/planejamento; não criar nem alterar arquivos do projeto. |
| **1A — fundação técnica** | `arquitetura-stack`, `auditoria-dependencias`, `ci-dependabot`, `interface-cliente-referencias`, `qualidade-acessibilidade`, `documentacao-agents-md`, `aceitacao-final` | Definir separação núcleo/cliente sem antecipar a implementação da interface. |
| **1B — interface** | `arquitetura-stack`, `auditoria-dependencias`, `interface-cliente-referencias`, `ci-dependabot`, `qualidade-acessibilidade`, `documentacao-agents-md`, `aceitacao-final` | Confirmar manualmente as opções efetivas do Antigravity e executar o canário antes de operações dependentes. |
| **2 — documentação** | `documentacao-agents-md`, `modulos-opcionais`, `aceitacao-final` | Documentar `docs/MODULES.md`; não implementar módulos sem autorização específica. |
| **Módulo opcional** | `modulos-opcionais` e skills técnicas correspondentes | Exige escopo e autorização próprios. |

## Uso em projetos de clientes

`AGENTS.md` desta base é o roteador da fundação. Em cada projeto de cliente, crie um `AGENTS.md` específico com comandos, stack, estrutura, decisões e regras permanentes do projeto real, seguindo `documentacao-agents-md`. Copie apenas as skills relevantes, sem duplicá-las em caminhos alternativos, e mantenha personalizações do cliente fora da base genérica.

## Limites do formato

O Antigravity descobre as skills padronizadas em `.agents/skills/`, mas isso não transforma instruções Markdown em barreira de segurança. Controles reais dependem de permissões, sandbox, ferramentas e sistema operacional. Verifique os detalhes nas configurações/documentação da versão instalada.
