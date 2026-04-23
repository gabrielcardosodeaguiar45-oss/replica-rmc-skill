# replica-rmc — skill autônoma do Claude Code

Aparato para gerar **réplica à contestação** em ações de RMC/RCC (Reserva de Margem Consignável / Cartão Consignado) brasileiras, com cobertura para AM/AL/BA/MG. Recebe a pasta de um processo, encadeia 4 subagentes especializados e entrega `.docx` pronto para revisão humana, relatório de conferência paralelo e ficha de aprendizado.

Originalmente desenvolvido para o escritório **Azevedo Lima & Rebonatto**. Publicado aqui com a metodologia completa: além da skill, vai junto o **vault Obsidian** (modelos, teses modulares, regras de adaptação, checklist e erros herdados) usado no dia-a-dia. Quem clonar pode adotar tal qual ou usar como ponto de partida para um vault próprio.

> **Privacidade.** Nomes de clientes, terceiros e CPFs foram anonimizados (placeholders "Caso N" / "Terceiro A/B/C"). Bancos e escritórios da parte adversária permanecem identificados — são informações públicas profissionais.

## Conteúdo

```
replica-rmc-skill/
├── skills/
│   ├── replica-rmc/         ← skill principal
│   │   ├── SKILL.md
│   │   ├── README.md
│   │   ├── references/      (schemas JSON)
│   │   └── scripts/         (11 scripts Python)
│   └── fatiar-processo/     ← skill auxiliar (eproc + PJe TJAM + PJe TJBA)
│       ├── SKILL.md
│       └── scripts/fatiar.py
├── agents/                  ← 4 subagentes do Claude Code
│   ├── analisador-processo-rmc.md
│   ├── consultor-vault-rmc.md
│   ├── redator-replica-rmc.md
│   └── revisor-replica-rmc.md
├── vault/                   ← acervo Obsidian (Modelos + Aprendizado/templates)
│   └── Modelos/ReplicasRMC/
│       ├── _MOC.md
│       ├── manual-consolidado.md
│       ├── estrutura-padrao.md
│       ├── configuracoes-visuais.md
│       ├── erros-herdados.md
│       ├── checklist-protocolo.md
│       ├── regras-de-adaptacao.md
│       ├── modelos-por-estado/{am,al,ba,mg,sergipe}/
│       └── teses-modulares/{nossas,impugnacao}/
├── NOTICE.md                ← aviso de anonimização e direitos
├── INSTALL.md               ← passo a passo de instalação
├── LICENSE                  ← MIT
└── README.md                ← este arquivo
```

## Como funciona

```
/replica-rmc <pasta-do-processo>
      │
      ├─ (0) fatiar-processo (se PDF consolidado)
      │
      ├─ (1) analisador-processo-rmc   → _analise.json
      ├─ (2) consultor-vault-rmc       → _plano.json
      ├─ (3) redator-replica-rmc       → Replica - <CNJ> - <NOME>.docx
      ├─ (4) revisor-replica-rmc       → Relatorio_Conferencia_<CNJ>.docx
      ├─ (5) iteração (max 2) se AJUSTES
      └─ (6) ficha de aprendizado em Aprendizado/ReplicasRMC/
```

Cada subagente roda em contexto isolado. Os artefatos intermediários (`_analise.json`, `_plano.json`) ficam na própria pasta do processo, permitindo retomada se o fluxo for interrompido.

## Pré-requisitos

1. [Claude Code](https://claude.com/claude-code) instalado.
2. Python 3.10+ com `pymupdf` e `python-docx`.
3. Vault Obsidian: o conteúdo de `vault/` deste repositório serve como base — copie para o seu vault local ou aponte `OBSIDIAN_VAULT_RMC` direto para a pasta `vault/` clonada.

Veja [INSTALL.md](INSTALL.md) para o passo a passo.

## Skill auxiliar — `fatiar-processo`

Dividir PDF consolidado de processo eletrônico em PDFs por evento/movimentação/documento. Suporta:

| Sistema             | Marcação detectada                                           |
|---------------------|--------------------------------------------------------------|
| eproc/TRF4          | "PÁGINA DE SEPARAÇÃO" + "Evento N"                           |
| PJe TJAM (Amazonas) | tríade "Data: …" + "Movimentação:" + "Por:"                  |
| PJe TJBA (Bahia)    | "Num. NNNNNNN - Pág. 1" + "Assinado eletronicamente por:"    |

```bash
python skills/fatiar-processo/scripts/fatiar.py "<arquivo.pdf>" --saida "<pasta>"
```

Detecção automática; `--sistema eproc|pje_tjam|pje_tjba` força um modo específico.

## Regras inegociáveis (do vault)

1. Cidade do fecho = comarca real do processo. Nunca "Manaus/AM" automático.
2. Cambria 12pt obrigatório. Sem imagens no corpo.
3. Listas em `a) b) c)` ou `i ii iii` — nunca traços.
4. "Declaração de inexistência", nunca "anulação".
5. IP: validar contra RFC 1918 antes de chamar de "privado".
6. TED: cruzar conta-destino com conta INSS do autor.
7. RMC + RCC gêmeos: sempre verificar HISCON.

A lista completa (16 regras + 29 erros herdados + 7 blocos de checklist) vive no vault Obsidian e é consultada pelos subagentes em tempo de execução.

## O que esta skill NÃO faz

1. Não redige inicial, apelação ou cumprimento de sentença.
2. Não negocia acordo.
3. Não analisa HISCON isoladamente.
4. Não fatia PDF sozinha (delega para `fatiar-processo`).

## Licença

MIT — veja [LICENSE](LICENSE).

## Histórico

Criada em 2026-04-22 após consolidação de três casos paradigma em três fases de análise no vault. Publicada em 2026-04-23.
