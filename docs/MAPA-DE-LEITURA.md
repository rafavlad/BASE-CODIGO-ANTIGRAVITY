# Mapa de leitura da BASE_CODIGO_ANTIGRAVITY

Este mapa é a entrada de navegação para o pacote local. Os links são relativos e funcionam quando o repositório completo está disponível no workspace. Um link não significa que o assistente já leu o arquivo nem que tem acesso de escrita ao GitHub.

## Ordem de leitura

1. Leia [`AGENTS.md`](../AGENTS.md) e [`INDICE-DO-PACOTE.md`](INDICE-DO-PACOTE.md) para entender as regras globais e a matriz de carregamento.
2. Leia integralmente as cinco skills globais obrigatórias: princípios globais, fases e autorizações, segurança/permissões, integridade Git e continuidade de sessões.
3. Leia as skills temáticas exigidas pela fase, conforme o índice.
4. Leia [`MENSAGENS-DE-SESSAO.md`](MENSAGENS-DE-SESSAO.md) para selecionar um modelo de início/retomada; adapte-o ao estado atual e à autorização real.
5. Leia [`REGISTRO-ALTERACOES.md`](REGISTRO-ALTERACOES.md) antes de adicionar uma entrada e [`RELATORIO-DE-VALIDACAO.md`](RELATORIO-DE-VALIDACAO.md) para entender as verificações desta edição.

## Skills normativas

- [Princípios globais](../.agents/skills/principios-globais/SKILL.md) — prioridades, escopo e regras não negociáveis.
- [Fases e autorizações](../.agents/skills/fases-e-autorizacoes/SKILL.md) — fases, estados, portões e relatórios.
- [Segurança e permissões](../.agents/skills/seguranca-permissoes/SKILL.md) — arquivos de ambiente, acesso, sandbox e canário.
- [Integridade Git](../.agents/skills/git-integridade/SKILL.md) — estado do repositório, commits e ações remotas.
- [Continuidade de sessões](../.agents/skills/continuidade-sessoes/SKILL.md) — retomada segura.
- [Aceitação final](../.agents/skills/aceitacao-final/SKILL.md) — critérios de aprovação.
- [Arquitetura e stack](../.agents/skills/arquitetura-stack/SKILL.md) — estrutura, tecnologias e scripts.
- [Auditoria de dependências](../.agents/skills/auditoria-dependencias/SKILL.md) — auditoria npm e contratos da CLI.
- [CI e Dependabot](../.agents/skills/ci-dependabot/SKILL.md) — automação e cadeia de fornecimento.
- [Interface e referências de clientes](../.agents/skills/interface-cliente-referencias/SKILL.md) — UI, separação núcleo/cliente e materiais externos.
- [Qualidade e acessibilidade](../.agents/skills/qualidade-acessibilidade/SKILL.md) — testes, regressão e acessibilidade.
- [Módulos opcionais](../.agents/skills/modulos-opcionais/SKILL.md) — documentação de recursos que exigem autorização própria.
- [Documentação de projeto](../.agents/skills/documentacao-agents-md/SKILL.md) — `AGENTS.md` do cliente e documentos obrigatórios.

## Referências oficiais do Antigravity

As regras de produto mudam com versões e variam entre sistemas operacionais e IDE/CLI. Confirme os detalhes nas páginas oficiais: [Agent Skills](https://antigravity.google/docs/skills), [Rules](https://antigravity.google/docs/rules), [Agent Settings](https://antigravity.google/docs/agent-settings), [Permissions](https://antigravity.google/docs/permissions) e [Terminal Sandbox](https://antigravity.google/docs/sandbox-mode).

## Avisos

- A Fase 0 é somente leitura e não deve gravar alterações no projeto.
- O resultado `APPROVED` requer evidência para todos os portões aplicáveis; intenção ou documento existente não é evidência suficiente.
- A confirmação manual de configuração e o canário de segurança são verificações distintas.
- Não leia segredos ou valores reais de arquivos de ambiente.
- Não faça `git push`, publicação ou deploy sem autorização explícita separada.
