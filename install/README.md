# Instalar o agente Cipher

Este agente e um conjunto de arquivos markdown: uma definicao (`AGENT.md`) e varias skills
(`skills/<slug>/SKILL.md`). Funciona em qualquer CLI de agente — o que muda e onde os
arquivos sao colocados.

## 1. Clonar

```bash
git clone https://github.com/WallysonDuarte/agente-cipher.git
cd agente-cipher
```

## 2. Instalar a CLI e carregar o agente

### Claude Code

```powershell
# Windows
irm https://claude.ai/install.ps1 | iex
```

```bash
# macOS / Linux
curl -fsSL https://claude.ai/install.sh | bash
```

- **Definicao do agente:** `~/.claude/CLAUDE.md (ou .claude/agents/<nome>.md no projeto)`
- **Skills:** `~/.claude/skills/`
- **Executar:** `claude -p "<pedido>"`
- Le `skills/<slug>/SKILL.md` nativamente e ativa a skill pela `description`.

### Codex

```powershell
# Windows
irm https://chatgpt.com/codex/install.ps1 | iex
```

```bash
# macOS / Linux
npm i -g @openai/codex
```

- **Definicao do agente:** `AGENTS.md (concatene AGENT.md + as skills que for usar)`
- **Skills:** `AGENTS.md na raiz do projeto`
- **Executar:** `codex exec --skip-git-repo-check "<pedido>"`
- Nao tem carregamento automatico de skills: cole o conteudo em `AGENTS.md`.

### Grok

```powershell
# Windows
irm https://x.ai/cli/install.ps1 | iex
```

```bash
# macOS / Linux
ver instrucoes oficiais da CLI
```

- **Definicao do agente:** `AGENT.md via prompt inicial`
- **Skills:** `passado no prompt`
- **Executar:** `grok -p "<pedido>"`
- Use modo one-shot com o AGENT.md no inicio do prompt.

### Antigravity

```powershell
# Windows
irm https://antigravity.google/cli/install.ps1 | iex
```

```bash
# macOS / Linux
ver instrucoes oficiais da CLI
```

- **Definicao do agente:** `AGENT.md via prompt inicial`
- **Skills:** `passado no prompt`
- **Executar:** `agy -p "<pedido>"`
- Binario `agy`. Nao le arquivos de instrucao automaticamente.

### Hermes

```powershell
# Windows
iex (irm https://hermes-agent.nousresearch.com/install.ps1)
```

```bash
# macOS / Linux
ver instrucoes oficiais da CLI
```

- **Definicao do agente:** `AGENT.md via prompt inicial`
- **Skills:** `passado no prompt`
- **Executar:** `hermes`
- Requer API key de um provider (ex.: OpenRouter) antes do primeiro uso.

### OpenClaw

```powershell
# Windows
& ([scriptblock]::Create((iwr -useb https://openclaw.ai/install.ps1))) -NoOnboard
```

```bash
# macOS / Linux
curl -fsSL https://openclaw.ai/install.sh | bash
```

- **Definicao do agente:** `AGENT.md como instrucao do agente`
- **Skills:** `~/.openclaw/skills/`
- **Executar:** `openclaw agent --local -m "<pedido>"`
- Suporta slash commands e selecao de modelo.

### OpenCode

```powershell
# Windows
irm https://opencode.ai/install | iex
```

```bash
# macOS / Linux
curl -fsSL https://opencode.ai/install | bash
```

- **Definicao do agente:** `AGENTS.md`
- **Skills:** `AGENTS.md na raiz do projeto`
- **Executar:** `opencode`
- Le `AGENTS.md` do projeto; cole o AGENT.md ali.

### Kimi Code

```powershell
# Windows
irm https://code.kimi.com/kimi-code/install.ps1 | iex
```

```bash
# macOS / Linux
ver instrucoes oficiais da CLI
```

- **Definicao do agente:** `AGENT.md via prompt inicial`
- **Skills:** `passado no prompt`
- **Executar:** `kimi -p "<pedido>"`
- Modo one-shot com `-p`.

## 3. Receita rapida (qualquer CLI sem suporte nativo a skills)

```bash
# Monta um unico arquivo de instrucao com o agente + todas as skills
cat AGENT.md skills/*/SKILL.md > AGENTS.md
```

Depois aponte a CLI para `AGENTS.md` (ou cole o conteudo como instrucao de sistema).

## 4. Usar apenas uma skill

Cada `SKILL.md` e autocontido: pode ser usado isolado, sem o resto do repositorio.

```bash
cat skills/auditoria-de-aplicacao/SKILL.md
```

## Apoie este trabalho

Os 9 agentes sao mantidos de forma independente e publicados abertamente.
Se este material te poupou tempo, voce pode retribuir com um cafe:

<a href="https://buy.stripe.com/bJefZi3wJ4JH18WeuEgA800">
<img src="https://img.shields.io/badge/Apoie--me-R$%2010-c0392b?style=for-the-badge&logo=stripe&logoColor=white" alt="Apoie-me com R$ 10" />
</a>

## Links

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/dududev/)
[![Do Zero ao Junior](https://img.shields.io/badge/Do%20Zero%20ao%20Junior-1abc9c?style=for-the-badge)](https://dozeroaojunior.com.br/)
[![Curitiba Software](https://img.shields.io/badge/Curitiba%20Software-2980b9?style=for-the-badge)](https://curitibasoftware.com.br/)
[![SoftwareHub](https://img.shields.io/badge/SoftwareHub-00ff41?style=for-the-badge)](https://softwarehub.com.br/)
