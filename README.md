# BASE_CODIGO_ANTIGRAVITY

Base reutilizável de engenharia para iniciar e validar projetos web de clientes com **Google Antigravity**. Esta edição deriva do pacote `BASE_CODIGO Skills 2.0.1` e adapta o roteador, caminhos, documentação e os controles específicos da ferramenta.

> **Importante:** a base descreve um processo e um conjunto de regras; não é, por si só, um aplicativo web pronto. A existência de instruções não prova que a ferramenta, o sandbox, a configuração, os testes ou os scripts estejam funcionando.

## Estrutura

```text
BASE_CODIGO_ANTIGRAVITY/
├── AGENTS.md
├── README.md
├── MANIFEST.md
├── .agents/
│   └── skills/
│       ├── aceitacao-final/SKILL.md
│       ├── arquitetura-stack/SKILL.md
│       ├── auditoria-dependencias/SKILL.md
│       ├── ci-dependabot/SKILL.md
│       ├── continuidade-sessoes/SKILL.md
│       ├── documentacao-agents-md/SKILL.md
│       ├── fases-e-autorizacoes/SKILL.md
│       ├── git-integridade/SKILL.md
│       ├── interface-cliente-referencias/SKILL.md
│       ├── modulos-opcionais/SKILL.md
│       ├── principios-globais/SKILL.md
│       ├── qualidade-acessibilidade/SKILL.md
│       └── seguranca-permissoes/SKILL.md
└── docs/
    ├── INDICE-DO-PACOTE.md
    ├── MAPA-DE-LEITURA.md
    ├── MENSAGENS-DE-SESSAO.md
    ├── REGISTRO-ALTERACOES.md
    └── RELATORIO-DE-VALIDACAO.md
```

## Como usar

1. Abra a pasta raiz desta base como workspace no Antigravity.
2. Leia `AGENTS.md` e `docs/INDICE-DO-PACOTE.md`.
3. Leia integralmente as cinco skills globais obrigatórias e as skills temáticas da fase autorizada, conforme `AGENTS.md`. As skills em `.agents/skills/<nome>/SKILL.md` seguem o formato padrão de Agent Skills.
4. Comece pela Fase 0, somente leitura. Não instale dependências, altere arquivos, inicialize Git nem avance de fase antes da autorização apropriada.
5. Consulte `docs/MENSAGENS-DE-SESSAO.md` para preparar/retomar sessões; as mensagens são atalhos e não substituem as instruções normativas.

## Segurança no Antigravity

- Revise as permissões na interface oficial da versão instalada. O comportamento difere conforme a versão, sistema operacional e superfície (IDE/CLI).
- Não presuma que `AGENTS.md` ou uma skill bloqueiam tecnicamente a leitura ou gravação de arquivos. Markdown orienta o agente; controles técnicos pertencem às permissões, ao sandbox e ao sistema operacional.
- Não leia valores de `.env`, `.env.local` nem outros arquivos de ambiente protegidos. O único teste de acesso previsto é o canário fictício `.env.fake-test`, com autorização explícita de sessão e seguindo `seguranca-permissoes`.
- Não autorize `git push`, publicação, deploy, exclusões ou comandos destrutivos por implicação. Exija autorização separada.
- Consulte [Permissões](https://antigravity.google/docs/permissions), [Configurações do agente](https://antigravity.google/docs/agent-settings), [Sandbox do terminal](https://antigravity.google/docs/sandbox-mode), [Regras](https://antigravity.google/docs/rules) e [Agent Skills](https://antigravity.google/docs/skills) para validar os detalhes da versão em uso.

## Regra de separação entre base e cliente

Esta base é um roteador/coleção normativa, não um `AGENTS.md` de cliente pronto. Cada projeto de cliente precisa de instruções próprias, baseadas na stack, nos comandos, nos módulos e nas decisões efetivamente presentes naquele projeto. Não copie regras irrelevantes nem inclua caminhos pessoais ou materiais privados na base genérica. Preserve a separação entre núcleo reutilizável e personalizações autorizadas em `src/client/`.

## Manutenção e validação

- Use `docs/REGISTRO-ALTERACOES.md` como histórico técnico cumulativo. Acrescente novas entradas ao final e nunca apague o histórico anterior.
- Use `MANIFEST.md` para confirmar os tamanhos e hashes SHA-256 dos arquivos distribuídos. O próprio manifesto é excluído do cálculo para evitar autorreferência.
- Leia `docs/RELATORIO-DE-VALIDACAO.md` para conhecer o que foi verificado e o que permanece pendente. A validação estrutural desta edição não substitui o teste numa instalação real do Antigravity.
- Esta pasta é independente e não altera o repositório original da base para Claude Code.
