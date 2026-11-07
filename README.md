<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=c0392b&height=220&section=header&text=CIPHER&fontColor=ffffff&fontSize=72&fontAlignY=38&desc=Seguranca%20da%20Informacao&descSize=22&descAlignY=60" width="100%" />

<img src="./assets/portrait.png" width="200" alt="Cipher" />

# 🔐 Cipher · Seguranca da Informacao

**Audita, endurece e responde. Encontra a falha antes do atacante e corrige com defesa em camadas — sem quebrar o que funciona.**

![Skills](https://img.shields.io/badge/skills-5-c0392b?style=for-the-badge)
![CLIs](https://img.shields.io/badge/CLIs-8-2980b9?style=for-the-badge)
![Idioma](https://img.shields.io/badge/pt--BR-nativo-1abc9c?style=for-the-badge)

</div>

---

## Por que usar este agente

- **Auditoria com confirmacao.** Nenhum achado vai para correcao sem ser reproduzido — evita gastar esforco em falso positivo de severidade inflada.
- **Camadas, nao remendo.** Cabecalhos, limites de taxa, autorizacao por recurso e gestao de segredo trabalhando juntos.
- **Higiene de segredo.** Varredura no historico do repositorio, rotacao e permissao de arquivo — nao apenas o estado atual.
- **Autorizacao testada de verdade.** Duas contas reais, tentativa de acesso cruzado, evidencia do resultado.
- **Resposta a incidente ensaiada.** Contencao, erradicacao, recuperacao e licao registrada.

---

## Skills

| Skill | Titulo | O que resolve |
|---|---|---|
| [`auditoria-de-aplicacao`](skills/auditoria-de-aplicacao/SKILL.md) | Auditoria de aplicacao | Revisar codigo e comportamento em busca das falhas mais exploradas, confirmando cada achado antes de classificar. |
| [`endurecimento-de-infraestrutura`](skills/endurecimento-de-infraestrutura/SKILL.md) | Endurecimento de infraestrutura | Reduzir superficie de ataque: exposicao minima, acesso por chave, cabecalhos de seguranca e isolamento de servicos. |
| [`gestao-de-segredos`](skills/gestao-de-segredos/SKILL.md) | Gestao de segredos | Manter credenciais fora do codigo, com cofre, rotacao, varredura de historico e permissoes corretas. |
| [`autenticacao-e-sessao`](skills/autenticacao-e-sessao/SKILL.md) | Autenticacao e sessao | Implementar autenticacao com token de curta duracao, renovacao rotativa, segundo fator e invalidacao confiavel. |
| [`resposta-a-incidente`](skills/resposta-a-incidente/SKILL.md) | Resposta a incidente | Conter, erradicar, recuperar e aprender — com registro do que aconteceu e do que mudou para nao repetir. |

Cada skill e um arquivo markdown autocontido (`skills/<slug>/SKILL.md`): pode ser instalada
isolada, sem o resto do repositorio.

---

## Instalacao rapida

```bash
git clone https://github.com/WallysonDuarte/agente-cipher.git
cd agente-cipher

# Claude Code — skills nativas
cp -r skills/* ~/.claude/skills/

# Qualquer outra CLI — arquivo unico de instrucao
cat AGENT.md skills/*/SKILL.md > AGENTS.md
```

| CLI | Instalacao (Windows / PowerShell) | Onde colocar as skills | Rodar |
|---|---|---|---|
| **Claude Code** | `irm https://claude.ai/install.ps1 \| iex` | `~/.claude/skills/` | `claude -p "<pedido>"` |
| **Codex** | `irm https://chatgpt.com/codex/install.ps1 \| iex` | `AGENTS.md na raiz do projeto` | `codex exec --skip-git-repo-check "<pedido>"` |
| **Grok** | `irm https://x.ai/cli/install.ps1 \| iex` | `passado no prompt` | `grok -p "<pedido>"` |
| **Antigravity** | `irm https://antigravity.google/cli/install.ps1 \| iex` | `passado no prompt` | `agy -p "<pedido>"` |
| **Hermes** | `iex (irm https://hermes-agent.nousresearch.com/install.ps1)` | `passado no prompt` | `hermes` |
| **OpenClaw** | `& ([scriptblock]::Create((iwr -useb https://openclaw.ai/install.ps1))) -NoOnboard` | `~/.openclaw/skills/` | `openclaw agent --local -m "<pedido>"` |
| **OpenCode** | `irm https://opencode.ai/install \| iex` | `AGENTS.md na raiz do projeto` | `opencode` |
| **Kimi Code** | `irm https://code.kimi.com/kimi-code/install.ps1 \| iex` | `passado no prompt` | `kimi -p "<pedido>"` |

Passo a passo por CLI, incluindo macOS/Linux: **[install/README.md](install/README.md)**

---

## Estrutura

```
agente-cipher/
├── AGENT.md                 definicao canonica do agente
├── .agent/agent.json        metadados legiveis por maquina
├── skills/
│   └── auditoria-de-aplicacao/SKILL.md
│   └── endurecimento-de-infraestrutura/SKILL.md
│   └── gestao-de-segredos/SKILL.md
│   └── autenticacao-e-sessao/SKILL.md
│   └── resposta-a-incidente/SKILL.md
├── install/README.md        instalacao nas 8 CLIs
└── assets/portrait.png
```

---

## Ecossistema

Este agente faz parte de um time de 9 agentes especializados:

[![Master](https://img.shields.io/badge/Master-00ff41?style=flat-square)](https://github.com/WallysonDuarte/agente-master) [![Nova](https://img.shields.io/badge/Nova-9b59b6?style=flat-square)](https://github.com/WallysonDuarte/agente-nova) [![Atlas](https://img.shields.io/badge/Atlas-1abc9c?style=flat-square)](https://github.com/WallysonDuarte/agente-atlas) [![Pixel](https://img.shields.io/badge/Pixel-e91e63?style=flat-square)](https://github.com/WallysonDuarte/agente-pixel) [![Forge](https://img.shields.io/badge/Forge-e67e22?style=flat-square)](https://github.com/WallysonDuarte/agente-forge) [![Cipher](https://img.shields.io/badge/Cipher-c0392b?style=flat-square)](https://github.com/WallysonDuarte/agente-cipher) [![Luna](https://img.shields.io/badge/Luna-f39c12?style=flat-square)](https://github.com/WallysonDuarte/agente-luna) [![Lira](https://img.shields.io/badge/Lira-f0932b?style=flat-square)](https://github.com/WallysonDuarte/agente-lira) [![Rank](https://img.shields.io/badge/Rank-2980b9?style=flat-square)](https://github.com/WallysonDuarte/agente-rank)

[![Hub](https://img.shields.io/badge/ver%20o%20time%20completo-c0392b?style=for-the-badge)](https://github.com/WallysonDuarte/softwarehub-agentes)

---

<div align="center">

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


</div>

<img src="https://capsule-render.vercel.app/api?type=waving&color=c0392b&height=100&section=footer" width="100%" />
