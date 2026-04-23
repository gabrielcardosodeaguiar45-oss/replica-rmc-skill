# Instalação

## 1. Pré-requisitos

```bash
# Python 3.10+
python --version

# Dependências Python
pip install pymupdf python-docx
```

[Claude Code](https://claude.com/claude-code) instalado e funcional.

## 2. Copiar skills e subagentes para `~/.claude/`

A estrutura esperada pelo Claude Code é:

```
~/.claude/
├── skills/
│   ├── replica-rmc/
│   └── fatiar-processo/
└── agents/
    ├── analisador-processo-rmc.md
    ├── consultor-vault-rmc.md
    ├── redator-replica-rmc.md
    └── revisor-replica-rmc.md
```

### macOS / Linux

```bash
# A partir do clone deste repositório:
mkdir -p ~/.claude/skills ~/.claude/agents

cp -r skills/replica-rmc       ~/.claude/skills/
cp -r skills/fatiar-processo   ~/.claude/skills/
cp -r agents/*.md              ~/.claude/agents/
```

### Windows (PowerShell)

```powershell
$claude = "$env:USERPROFILE\.claude"
New-Item -ItemType Directory -Force "$claude\skills","$claude\agents" | Out-Null

Copy-Item -Recurse -Force ".\skills\replica-rmc"     "$claude\skills\"
Copy-Item -Recurse -Force ".\skills\fatiar-processo" "$claude\skills\"
Copy-Item -Recurse -Force ".\agents\*.md"            "$claude\agents\"
```

## 3. Variáveis de ambiente

| Variável             | Default          | Para quê                                                          |
|----------------------|------------------|-------------------------------------------------------------------|
| `OBSIDIAN_VAULT_RMC` | `~/Obsidian/`    | raiz do vault Obsidian que contém `Modelos/ReplicasRMC/` e `Aprendizado/ReplicasRMC/` |
| `CLAUDE_HOME`        | `~/.claude/`     | onde estão `skills/replica-rmc/scripts/*.py`                      |

Se você usa os defaults, não precisa configurar nada. Caso contrário:

```bash
# bash/zsh
export OBSIDIAN_VAULT_RMC="$HOME/MeuVault"
export CLAUDE_HOME="$HOME/.claude"
```

```powershell
# PowerShell
[System.Environment]::SetEnvironmentVariable('OBSIDIAN_VAULT_RMC', "$env:USERPROFILE\Documents\Obsidian Vault", 'User')
```

## 4. Popular o vault Obsidian

Este repositório **já vem com um vault de partida** em `vault/Modelos/ReplicasRMC/` (anonimizado — ver [NOTICE.md](NOTICE.md)). Você tem três opções:

### Opção A — Adotar o vault como está

Aponte a variável `OBSIDIAN_VAULT_RMC` para a pasta `vault/` deste repositório:

```bash
export OBSIDIAN_VAULT_RMC="$(pwd)/vault"
```

Funciona imediatamente, mas atualizações no acervo viram conflitos quando você der `git pull`.

### Opção B — Copiar para o seu vault Obsidian

```bash
# macOS / Linux
cp -r vault/Modelos/ReplicasRMC      "$OBSIDIAN_VAULT_RMC/Modelos/"
mkdir -p "$OBSIDIAN_VAULT_RMC/Aprendizado/ReplicasRMC"
cp vault/Aprendizado/ReplicasRMC/_template.md \
   vault/Aprendizado/ReplicasRMC/_MOC.md \
   "$OBSIDIAN_VAULT_RMC/Aprendizado/ReplicasRMC/"
```

```powershell
# Windows PowerShell
Copy-Item -Recurse -Force ".\vault\Modelos\ReplicasRMC" "$env:OBSIDIAN_VAULT_RMC\Modelos\"
New-Item -ItemType Directory -Force "$env:OBSIDIAN_VAULT_RMC\Aprendizado\ReplicasRMC" | Out-Null
Copy-Item ".\vault\Aprendizado\ReplicasRMC\*.md" "$env:OBSIDIAN_VAULT_RMC\Aprendizado\ReplicasRMC\"
```

Depois adapte os arquivos ao seu escritório (cidade do fecho, subscritores, comarca-padrão).

### Opção C — Construir do zero

Use os arquivos de `vault/` apenas como referência arquitetural. A árvore esperada pelos subagentes:

```
Modelos/ReplicasRMC/
├── _MOC.md                              ← árvore de decisão
├── manual-consolidado.md                ← panorama geral
├── estrutura-padrao.md                  ← 9 blocos + 15 sub-seções
├── configuracoes-visuais.md             ← Cambria, margens, recuos
├── erros-herdados.md                    ← 29 armadilhas
├── checklist-protocolo.md               ← 7 blocos de validação
├── regras-de-adaptacao.md               ← 16 regras + Blocos A/B/C
├── modelos-por-estado/
│   ├── am/_index.md
│   ├── al/_index.md
│   ├── ba/_index.md
│   ├── mg/_index.md
│   └── sergipe/_index.md
└── teses-modulares/
    ├── nossas/*.md       (teses que sempre levantamos)
    └── impugnacao/*.md   (rebates às teses do banco)

Aprendizado/ReplicasRMC/
├── _MOC.md
├── _template.md
└── YYYY-MM-DD-<slug>-<comarca>.md  (uma por caso processado)
```

A skill vai alimentando `Aprendizado/ReplicasRMC/` automaticamente conforme você processa novos casos.

## 5. Sanity check

Abra um novo terminal e rode:

```bash
claude /replica-rmc /caminho/para/uma/pasta/de/processo
```

Se a skill carregar e começar a chamar o `analisador-processo-rmc`, está tudo certo. Se reclamar de "schema_caso.json não encontrado", confira o passo 2 (cópia para `~/.claude/skills/`).

## 6. Troubleshooting

1. **`pymupdf` não instala**: tente `pip install --upgrade pip` antes; em alguns Linux velhos pode precisar de `python3-dev` e `build-essential`.
2. **Subagente não é encontrado**: confirme que o `.md` está em `~/.claude/agents/` e que o frontmatter `name:` bate com o nome no slash command.
3. **Vault em local não-default**: configure `OBSIDIAN_VAULT_RMC` no shell ou em `~/.claude/settings.json` como variável global.
4. **Salvaguarda anti-inflate em `fatiar-processo`** dispara: o PDF tem fontes/XObjects compartilhados problemáticos. Investigue o PDF original — não desative a salvaguarda sem entender o porquê.
