---
name: seguranca-permissoes
description: "Proteção de arquivos de ambiente, revisão de permissões, sandbox e canário de segurança no Antigravity. Use antes de tarefas sensíveis e da Fase 1B."
---

# Segurança e permissões

## 3.1 Arquivos protegidos

Considere protegidos, no mínimo:

- `.env`
- `.env.local`
- `.env.development`
- `.env.production`
- `.env.test`
- `.env.fake-test`

Não leia, imprima, copie, registre em logs ou exponha seus valores. A regra vale para leitura por ferramentas de arquivo, terminal, processos auxiliares e qualquer outra via disponível.

**Exceção única e limitada:** o teste controlado de `.env.fake-test` descrito na seção 3.5, somente quando sua execução tiver sido explicitamente autorizada na sessão atual. Esse arquivo deve conter apenas dados fictícios mínimos, nunca credenciais ou valores copiados de um ambiente real.

`.env.example` pode conter apenas valores fictícios. Nunca inclua credenciais reais. Variáveis com prefixo `VITE_` são expostas ao cliente e não devem conter segredos.

## 3.2 Configuração de permissões no Antigravity

Não tente criar `.claude/settings.json`, `.claude/settings.local.json` nem inventar arquivos de configuração de permissões específicos para este projeto. Configure as permissões pela interface e pelos mecanismos documentados para a versão e a superfície instaladas.

Consulte as fontes oficiais antes de configurar ou validar controles:

- [Permissões](https://antigravity.google/docs/permissions)
- [Configurações do agente](https://antigravity.google/docs/agent-settings)
- [Sandbox do terminal](https://antigravity.google/docs/sandbox-mode)
- [Regras](https://antigravity.google/docs/rules)

Revise, conforme as opções realmente disponíveis no ambiente:

- Aprovação de comandos e operações sensíveis.
- Acesso a arquivos fora do workspace.
- Estado do sandbox do terminal e suas restrições de rede/sistema de arquivos.
- Regras `Deny`, `Ask` e `Allow` e sua precedência documentada.
- Operações destrutivas, `git push`, publicação, implantação e chamadas remotas.
- Acesso de ferramentas integradas, MCPs e navegador, se usados pela tarefa.

Os nomes e a disponibilidade das opções podem variar conforme o sistema operacional, versão e superfície. Na versão documentada atualmente, o Antigravity no Windows utiliza controles anteriores de execução de terminal, enquanto o sistema de permissões atualizado está disponível em macOS/Linux. **Não transfira instruções de uma plataforma para outra sem verificar a interface real.**

Não presuma suporte a um padrão, curinga, exceção, regra por caminho ou forma de persistência sem conferência na documentação da versão instalada. Não crie uma regra ampla de `Allow` para facilitar o trabalho. Nunca reduza proteções ou aprove operações remotas sem autorização explícita e separada.

## 3.3 Verificação das permissões efetivas

A existência de `AGENTS.md`, `.agents/rules/` ou de uma configuração visível não prova que os controles de acesso estejam ativos. Instruções em Markdown são regras de comportamento para o agente, não uma fronteira de segurança do sistema operacional.

Antes da Fase 1B, peça ao usuário que verifique na interface oficial do Antigravity as opções efetivas para o projeto e confirme, na própria sessão:

- A política de execução de terminal selecionada.
- Se o sandbox está ligado e qual é o alcance conhecido.
- As regras de acesso a arquivos fora do workspace.
- As regras configuradas de permissão e eventuais conflitos/avisos.
- Quais limitações permanecem e se alguma mudança requer reiniciar/reabrir o workspace.

Registre a confirmação como **verificação manual relatada pelo usuário**, nunca como teste automatizado nem como algo que o agente abriu ou verificou se não o fez. Se a confirmação não vier, registre `PENDING MANUAL`, mantenha o canário `NOT RUN` e pare as operações que dependem da proteção ainda não confirmada.

Não invente comandos de diagnóstico, nomes de menus ou arquivos de configuração. Não alegue que uma instrução em `AGENTS.md` bloqueia, tecnicamente, a leitura de `.env`.

## 3.4 Limites das permissões e isolamento real

Diferencie explicitamente:

1. Instruções persistentes (`AGENTS.md`, `GEMINI.md` e regras Markdown).
2. Regras de permissão configuradas na ferramenta.
3. Sandbox/isolamento de comandos e acesso a arquivos oferecido pela aplicação.
4. Controles de acesso do sistema operacional e permissões de arquivos.

Nenhum destes controles deve ser tratado como equivalente automático aos demais. Não afirme que o ambiente está isolado sem evidência da configuração efetiva e de seu alcance.

Não tente contornar uma restrição com comandos alternativos, subprocessos, codificação de conteúdo, outra ferramenta, caminho alternativo ou uso de uma integração. Se o ambiente não consegue bloquear de forma verificável o acesso a um arquivo protegido, registre a limitação e mantenha as operações dependentes interrompidas. Para proteção garantida no nível do sistema operacional, use controles de isolamento oficialmente suportados e adequados ao sistema; não trate texto de prompt como sandbox.

## 3.5 Canário de segurança

O canário é um teste controlado para observar o comportamento real dos controles de acesso ao tentar ler um arquivo fictício de ambiente por dois caminhos: ferramenta de leitura de arquivos e terminal. Ele não testa todos os processos possíveis, não prova isolamento absoluto e não deve ser usado para justificar segurança de arquivos reais por inferência.

Execute no início da Fase 1B, antes de operações que dependam dessa verificação, apenas depois de a política efetiva ter sido revisada e de o usuário autorizar especificamente o procedimento na sessão atual.

### 3.5.1 Autorização específica

Em toda sessão nova de Fase 1B, obtenha do usuário uma autorização explícita para executar o procedimento de canário desta skill, junto com o resumo de continuidade mais recente. A presença desta skill, do `AGENTS.md`, de `docs/SECURITY.md` ou de um resumo antigo não concede, isoladamente, autorização atual.

A autorização cobre somente:

- Verificar a existência de `.env.fake-test` sem ler seu conteúdo.
- Se e somente se o arquivo estiver ausente, criar um arquivo com conteúdo estritamente fictício e mínimo por um mecanismo permitido.
- Fazer tentativas controladas de leitura pelos dois caminhos definidos abaixo, sem revelar o conteúdo.
- Remover o arquivo somente quando for comprovado que o próprio agente o criou nesta execução, e apenas se a remoção for segura e permitida.

Se o arquivo já existir no primeiro exame, não o abra, altere nem remova. Marque o canário como `NOT RUN` e peça orientação. Se o agente não puder criar o fixture de forma permitida, não contorne a restrição: solicite que o usuário crie o arquivo fictício em resposta a esse pedido e confirme sua origem nesta sessão. Nesse caso, a remoção fica sob responsabilidade do usuário.

### 3.5.2 Procedimento

1. Verifique apenas a existência de `.env.fake-test`; não leia seu conteúdo. Registre se ele já existia.
2. Se já existia, pare: classifique o canário como `NOT RUN` e não toque no arquivo.
3. Se estava ausente, tente criá-lo com dados inventados, sem segredos, somente por mecanismo autorizado. Se a criação for bloqueada, não tente contornar com outra ferramenta ou comando.
4. Se o usuário criar o arquivo a pedido do canário, aguarde confirmação explícita na sessão atual. Não considere autorizado um arquivo de origem ou data de criação desconhecidas.
5. Faça uma tentativa de leitura usando a ferramenta de arquivo disponível e, separadamente, uma tentativa pelo terminal com um comando apropriado ao shell real (por exemplo, `Get-Content .env.fake-test` no PowerShell ou `cat .env.fake-test` em shell POSIX). **Não exiba nem registre a saída de conteúdo de nenhuma tentativa.** Se a ferramenta de leitura não permitir observar a tentativa sem revelar o conteúdo, não a execute; marque esse caminho `NOT RUN` e explique a limitação.
6. Para cada tentativa, registre apenas a ferramenta/comando, se chegou à política de permissão e o resultado observado. Uma mensagem genérica, arquivo ausente, falha de processo ou recusa do próprio agente sem evidência de bloqueio técnico não prova que a política bloqueou o acesso.
7. Classifique cada caminho separadamente. Não generalize para ferramentas, processos ou diretórios não testados.
8. Se o agente criou o fixture nesta execução, remova-o apenas quando a origem estiver comprovada e a remoção for permitida; depois confirme somente a ausência, sem ler o conteúdo. Se o usuário o criou, não o remova: informe que o usuário deve eliminá-lo e confirmar a limpeza.
9. Garanta que `.env.fake-test` esteja listado no `.gitignore` durante uma fase autorizada a alterá-lo. Não mude arquivos fora do escopo da fase. Não realize commit enquanto o fixture permanecer no projeto.
10. Registre limitações, testes não realizados e responsabilidades de limpeza.

Se a remoção segura de um arquivo criado pelo agente não for possível, não contorne controles; informe o caminho sem revelar conteúdo e aguarde orientação. Se o fixture foi criado pelo usuário, aguarde a confirmação de limpeza antes de qualquer commit.

### 3.5.3 Estados do canário

- `BLOCKED`: há evidência direta de que um controle técnico configurado impediu a tentativa de leitura.
- `ALLOWED`: a leitura do fixture foi efetivamente permitida pelo caminho testado; a proteção esperada não se confirmou por esse caminho.
- `INCONCLUSIVE`: o resultado não permite atribuir a causa à política de permissão nem comprovar o bloqueio.
- `NOT RUN`: a tentativa não foi executada.

Uma recusa textual do agente, sem evidência observável de bloqueio pela ferramenta, política ou sandbox, não é suficiente para `BLOCKED`. O canário não é aprovado se qualquer um dos dois caminhos obrigatórios estiver `ALLOWED`, `INCONCLUSIVE` ou `NOT RUN`. A proteção dos arquivos reais prevalece sobre a conclusão do teste.

Se algum caminho não resultar em `BLOCKED`, registre o resultado real e interrompa as operações que dependem da proteção não confirmada. Não contorne, não enfraqueça permissões e não repita tentativas por caminhos alternativos. O usuário pode autorizar expressamente a continuação limitada de tarefas de interface que não leiam, criem, copiem, registrem ou versionem valores de arquivos reais de ambiente, não alterem permissões e não dependam diretamente da proteção não confirmada. Essa autorização não muda o estado do canário nem aprova a Fase 1B, e não substitui autorização separada de commit.
