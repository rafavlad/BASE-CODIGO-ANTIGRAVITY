# Relatório de validação estrutural — BASE_CODIGO_ANTIGRAVITY

## Escopo

Esta edição foi montada diretamente do arquivo enviado `BASE_CODIGO_Skills_2.0.1(1).zip`. O pacote de origem contém 13 skills em `.claude/skills/`, `CLAUDE.md`, `README.md`, `MANIFEST.json` e cinco documentos em `docs/`. Esta edição migra as instruções para o formato de Antigravity: `AGENTS.md`, `.agents/skills/<nome>/SKILL.md` e documentação Markdown.

## Resultados estruturais executados

- **Origem lida:** ZIP de 21 entradas, 237.006 bytes descompactados, contendo 13 skills e 8 arquivos de documentação/roteamento/manifesto.
- **Skills:** 13 pastas com `SKILL.md` cada; frontmatter com `name` e `description` verificados estruturalmente.
- **Ponto de entrada:** `AGENTS.md` criado na raiz.
- **Formato do pacote:** todos os arquivos entregues, incluindo o manifesto, estão em Markdown (`.md`).
- **Manifesto:** tamanhos e SHA-256 recalculados para todos os arquivos exceto o próprio `MANIFEST.md`; entradas conferidas com arquivos existentes.
- **Links locais:** links Markdown relativos internos verificados para destinos existentes.
- **Referências de plataforma:** referências normativas às pastas `.claude/` e ao roteador `CLAUDE.md` foram removidas dos documentos ativos; as menções de Claude Code no registro cumulativo foram mantidas apenas como histórico da origem.
- **Integridade do arquivo final:** ZIP reaberto e verificado com o módulo `zipfile`; nenhum erro de CRC.

## Adaptações principais

- Roteador raiz `CLAUDE.md` → `AGENTS.md`.
- Skills `.claude/skills/` → `.agents/skills/`.
- `documentacao-claude-md` → `documentacao-agents-md`.
- Instruções específicas de permissões do Claude Code foram substituídas por procedimento baseado na interface/documentação oficial do Antigravity, sem inventar arquivo de configuração de permissões do workspace.
- Canário de segurança reescrito para distinguir bloqueio técnico, recusa do agente, leitura permitida, resultado inconclusivo e teste não executado; o conteúdo do fixture nunca deve ser exibido.
- Documentos históricos da origem preservados como histórico, com nota explícita de que não são instruções normativas desta edição.

## Não executado / pendências

- Não foi executado um projeto de cliente nesta base.
- Não foram instaladas dependências npm nem executados `npm ci`, testes, lint, build ou auditoria de dependências: esta é uma fundação de instruções, não um aplicativo executável.
- Não houve teste comportamental numa sessão real do Antigravity.
- Não foi confirmado o funcionamento das permissões reais, da política de terminal ou do sandbox em qualquer sistema operacional. A interface e os recursos diferem por versão, sistema operacional e superfície.
- Links para documentação oficial foram incluídos e conferidos por navegação web durante a preparação, mas o comportamento real do aplicativo não foi testado.
- Esta saída não foi publicada no GitHub e não altera a origem.

## Critério de confiança

Os resultados acima comprovam somente verificações estruturais executadas neste pacote local. **Não equivalem à validação operacional do Antigravity.** Antes de usar a base em um projeto real, confirme as permissões da instalação, execute a Fase 0, revise os gates e registre todas as evidências conforme `fases-e-autorizacoes`.
