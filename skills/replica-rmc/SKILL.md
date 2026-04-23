---
name: replica-rmc
description: Gera réplica à contestação em ações de RMC/RCC (Reserva de Margem Consignável / Cartão Consignado) de forma autônoma. Use quando o usuário pedir réplica de RMC, réplica de RCC, réplica de cartão consignado, réplica bancária sobre margem consignável, ou quando jogar pasta de processo RMC/RCC para análise. Não usar para apelações (existe skill separada).
---

# Skill — replica-rmc

Orquestra a produção autônoma de **réplica à contestação** em ações de RMC/RCC, cobrindo AM/AL/BA/MG. Escopo restrito — réplica. Apelação, inicial ou cumprimento não entram aqui.

## Quando sou invocada

1. Usuário diz "faz a réplica RMC", "gera réplica RCC", "réplica do consignado", "joga a réplica desse processo".
2. Usuário envia pasta/PDF de processo RMC ou RCC e pede peça.
3. Slash command `/replica-rmc <pasta-do-processo>` é disparado.

## Entrada obrigatória

Caminho para **pasta de processo** contendo pelo menos:

1. PDF consolidado do processo (eproc/PJE), OU
2. Pasta já fatiada com inicial + contestação + anexos (`fatiar-processo` prévia).

Se apenas o PDF consolidado estiver presente, a skill roda `fatiar-processo` automaticamente antes de prosseguir.

## Fluxo autônomo — NÃO pedir confirmação ao usuário

```
/replica-rmc <pasta>
      │
      ├─ (0) fatiar-processo se necessário (PDF consolidado → pasta fatiada)
      │
      ├─ (1) Subagent `analisador-processo-rmc`
      │        Extrai JSON do caso (autor, processo, banco, contratos, anexos,
      │        TEDs, faturas, laudo digital, RCC gêmeo, etc.)
      │
      ├─ (2) Subagent `consultor-vault-rmc`
      │        Lê vault Obsidian (Modelos/ReplicasRMC), aplica árvore de
      │        decisão, seleciona modelo-base + teses + precedentes,
      │        roda as 16 regras-de-adaptacao, devolve plano editorial
      │
      ├─ (3) Subagent `redator-replica-rmc`
      │        Gera .docx Cambria seguindo estrutura-padrao
      │        (9 blocos + sub-seções de mérito selecionadas)
      │
      ├─ (4) Subagent `revisor-replica-rmc`
      │        Roda checklist-protocolo (7 blocos), erros-herdados (29
      │        armadilhas) e scripts de validação. Emite relatório
      │        APTO ou AJUSTES NECESSÁRIOS.
      │
      ├─ (5) Se AJUSTES → volta a (3) com feedback; máx 2 iterações
      │
      └─ (6) Entrega:
              - .docx da réplica (pronto para revisão humana)
              - Relatório de conferência (.docx paralelo)
              - Ficha de aprendizado pré-preenchida em
                vault/Aprendizado/ReplicasRMC/YYYY-MM-DD-cliente-processo.md
```

## Orquestração — instruções precisas

### Etapa 0 — Normalização da entrada

1. Verificar se a pasta contém PDFs já fatiados (arquivos separados tipo `01-inicial.pdf`, `02-contestacao.pdf`) ou um PDF consolidado.
2. Se consolidado: invocar a skill `fatiar-processo` primeiro.
3. Confirmar existência mínima: inicial + contestação. Se faltar qualquer, interromper e reportar.

### Etapa 1 — Análise

Invocar o subagent `analisador-processo-rmc` com prompt:

> "Analise esta pasta de processo RMC/RCC: {{PASTA}}. Extraia dados estruturados conforme template em references/schema_caso.json. Devolva apenas JSON válido. Sem comentários, sem markdown."

Esperar JSON de volta. Salvar em `{{PASTA}}/_analise.json`.

### Etapa 2 — Consulta ao vault

Invocar o subagent `consultor-vault-rmc` com prompt:

> "Dado o JSON de caso em {{PASTA}}/_analise.json, navegue o vault Obsidian (`$OBSIDIAN_VAULT_RMC/Modelos/ReplicasRMC/`) e monte o plano editorial completo. Aplique as 16 regras de adaptação. Devolva apenas JSON com o plano, sem comentários."

Esperar JSON de plano editorial. Salvar em `{{PASTA}}/_plano.json`.

### Etapa 3 — Redação

Invocar o subagent `redator-replica-rmc` com prompt:

> "Gere a réplica .docx com base em {{PASTA}}/_analise.json e {{PASTA}}/_plano.json. Salve em {{PASTA}}/Réplica - {{CNJ-resumido}} - {{NOME_AUTOR}}.docx. Layout Cambria conforme configuracoes-visuais do vault. NÃO use traços como marcadores em listas (usar a), b), c), d) ou i, ii, iii)."

### Etapa 4 — Revisão

Invocar o subagent `revisor-replica-rmc` com prompt:

> "Valide a réplica em {{PASTA}}/Réplica*.docx. Rode checklist-protocolo, erros-herdados (29) e scripts scripts/check_*.py. Gere relatório em {{PASTA}}/Relatorio_Conferencia_{{CNJ-resumido}}.docx. Classifique APTO ou AJUSTES NECESSÁRIOS. Se AJUSTES, liste exatamente o que refazer."

### Etapa 5 — Iteração

Se o revisor retornou AJUSTES, invocar novamente o redator com o relatório do revisor como feedback. Máximo **2 iterações**. Após 2, parar e entregar mesmo assim com alerta claro no final da resposta.

### Etapa 6 — Ficha de aprendizado

Criar ficha em `$OBSIDIAN_VAULT_RMC/Aprendizado/ReplicasRMC/YYYY-MM-DD-<slug-cliente>-<slug-comarca>.md` usando o template `_template.md` do vault, pré-preenchida com os metadados do caso e os padrões detectados pelo revisor.

## Entrega ao usuário — formato fixo

No final, responder ao usuário com mensagem curta neste formato exato:

```
Réplica gerada.

Arquivo: {{PATH_DOCX}}
Relatório: {{PATH_RELATORIO}}
Ficha: {{PATH_FICHA}}

Classificação: {{APTO|AJUSTES APLICADOS|AJUSTES RESIDUAIS}}
Pontos de atenção: {{LISTA_CURTA}}
```

Nada mais. Sem resumo do que foi feito, sem recap — o usuário abre o `.docx`, revisa e protocola.

## Configuração

A skill espera duas variáveis de ambiente (ou caminhos hardcoded equivalentes no
seu fork):

| Variável                | Default                         | Para quê                                        |
|-------------------------|---------------------------------|-------------------------------------------------|
| `OBSIDIAN_VAULT_RMC`    | `~/Obsidian/`                   | raiz do vault Obsidian com `Modelos/ReplicasRMC/` e `Aprendizado/ReplicasRMC/` |
| `CLAUDE_HOME`           | `~/.claude/`                    | onde estão `skills/replica-rmc/scripts/*.py`    |

Antes de usar, popule `$OBSIDIAN_VAULT_RMC/Modelos/ReplicasRMC/` com os arquivos descritos
em "Arquivos de referência no vault" abaixo. O repositório fornece a estrutura de skill +
subagents + scripts; o conteúdo do vault é específico do seu escritório (modelos `.docx`,
teses modulares, regras de adaptação) e fica fora deste repo.

## Regras inegociáveis (do vault `Modelos/ReplicasRMC/`)

1. **Cidade do fecho** = comarca real do processo, NUNCA "Manaus/AM" automático. Erro 22.
2. **Cambria obrigatório**. Erro 19.
3. **Sem imagens**. Erro 20.
4. **Listas com a), b), c) ou i, ii, iii — NUNCA traços**. Erro 21.
5. **"Declaração de inexistência"**, NUNCA "anulação". Erro 6.
6. **IP**: checar RFC 1918 antes de chamar de privado. Regra 16.
7. **TED**: cruzar com conta INSS. Regra 4.
8. **2ª via massiva**: inserir Bloco A. Regra 2.
9. **BMG pré-09/2023**: inserir Bloco C (confissão do próprio banco). Regra 7.
10. **RMC + RCC gêmeos**: sempre verificar HISCON. Regra 1.
11. **Maués**: cautela de tom (alerta Juiz Anderson). Regra 13.

## Arquivos de referência no vault

O subagent `consultor-vault-rmc` deve ler (não duplicar aqui):

1. `Modelos/ReplicasRMC/_MOC.md` — árvore de decisão.
2. `Modelos/ReplicasRMC/manual-consolidado.md` — panorama geral.
3. `Modelos/ReplicasRMC/estrutura-padrao.md` — 9 blocos + 15 sub-seções.
4. `Modelos/ReplicasRMC/configuracoes-visuais.md` — Cambria, margens.
5. `Modelos/ReplicasRMC/erros-herdados.md` — 29 armadilhas.
6. `Modelos/ReplicasRMC/checklist-protocolo.md` — 7 blocos de validação.
7. `Modelos/ReplicasRMC/regras-de-adaptacao.md` — 16 regras + blocos A/B/C.
8. `Modelos/ReplicasRMC/modelos-por-estado/<uf>/_index.md` — matriz de escolha.
9. `Modelos/ReplicasRMC/teses-modulares/{nossas,impugnacao}/*.md` — teses.
10. `Aprendizado/ReplicasRMC/*.md` — aprendizado cumulativo (paradigmas).

## Scripts auxiliares

Ver `scripts/` desta skill. Todos Python 3, dependências: `pymupdf`, `python-docx`.

1. `extract_processo.py` — extração estruturada de PDF processual.
2. `check_ip_rfc1918.py` — validação de IP contra blocos privados.
3. `check_ted_conta_inss.py` — cruzamento conta INSS × conta TED.
4. `detect_2via_massiva.py` — detecta postagem concentrada em faturas.
5. `check_cartao_gemeo.py` — cruza número do cartão × HISCON.
6. `check_bmg_pre_09_2023.py` — flag para BMG pré-setembro/2023.
7. `check_refin_maquiador_bmg.py` — detecta "crédito de refin" sem queda de saldo.
8. `gerar_docx.py` — montagem final .docx Cambria.
9. `forcar_cambria.py` — força Cambria em .docx existente.

## O que esta skill NÃO faz

1. Não redige inicial, apelação ou cumprimento.
2. Não negocia acordo.
3. Não analisa HISCON isoladamente (usar skill `analise-cadeias-hiscon`).
4. Não fatia PDF sozinha (usa skill `fatiar-processo`).

## Retomada em nova sessão

Se a skill for interrompida no meio (ex: contexto acaba), retomar pelo JSON salvo:

1. Se existir `_analise.json` e não `_plano.json`: começar da etapa 2.
2. Se existir `_plano.json` e não `.docx`: começar da etapa 3.
3. Se existir `.docx` sem relatório: começar da etapa 4.

## Referências cruzadas

1. Skill `fatiar-processo` — pré-requisito se PDF consolidado.
2. Skill `conferencia-processual` — usada internamente pelo revisor.
3. Skill `analise-cadeias-hiscon` — NÃO é chamada aqui; usar em triagem antes da inicial.
