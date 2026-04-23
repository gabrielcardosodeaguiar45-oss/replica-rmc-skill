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
      ├─ (0) fatiar-processo se necessário (PDF consolidado vira pasta fatiada)
      │
      ├─ (1) analisador-processo-rmc
      │        Extrai _analise.json (autor, processo, banco, contratos, anexos,
      │        TEDs, faturas, laudo digital, RCC gêmeo, observações_caso,
      │        bloqueadores). Trecho literal OBRIGATÓRIO em cada tese do banco.
      │
      ├─ (1.5) Checagem de bloqueadores
      │        Se houver bloqueador ALTA, pipeline para. Apresenta ao usuário
      │        antes de redigir. Sem confirmação não segue.
      │
      ├─ (2) consultor-vault-rmc
      │        Aplica 16 regras de adaptação. Gera DOIS arquivos:
      │        . _plano.json (modelo-base + teses + precedentes + alertas)
      │        . _contrato_rebate.json (cobertura 100%: cada tese do banco
      │          com seção dedicada, fundamentos, criticidade, min_paragrafos)
      │
      ├─ (3) redator-replica-rmc
      │        Gera .docx Cambria seguindo estrutura espelhada à contestação
      │        (preliminares antes do mérito) com densidade dos parágrafos do
      │        modelo do escritório. Zero travessão como aposto. Frases-modelo
      │        injetadas com dados reais do caso. Autovalidação 11 itens
      │        antes de devolver.
      │
      ├─ (4) revisor-replica-rmc
      │        Checklist + 29 erros + scripts. Cobertura métrica explícita.
      │        Severidade graduada (CRÍTICO / MÉDIO / COSMÉTICO).
      │        Word Comments embutidos no .docx, sem relatório paralelo.
      │
      ├─ (5) Se AJUSTES NECESSÁRIOS, volta a (3) com feedback; máx 2 iterações.
      │
      └─ (6) Entrega:
              . .docx da réplica com Word Comments do revisor
              . Ficha de aprendizado pré-preenchida em
                vault/Aprendizado/ReplicasRMC/YYYY-MM-DD-cliente-processo.md
```

## Orquestração — instruções precisas

### Etapa 0 — Normalização da entrada

1. Verificar se a pasta contém PDFs já fatiados (arquivos separados tipo `01-inicial.pdf`, `02-contestacao.pdf`) ou um PDF consolidado.
2. Se consolidado: invocar a skill `fatiar-processo` primeiro.
3. Confirmar existência mínima: inicial + contestação. Se faltar qualquer, interromper e reportar.

### Etapa 1 — Análise

Invocar o subagent `analisador-processo-rmc` com prompt:

> "Analise esta pasta de processo RMC/RCC: {{PASTA}}. Extraia dados estruturados conforme template em references/schema_caso.json. Trecho literal OBRIGATÓRIO em cada preliminar e tese do banco. Sinalize bloqueadores em campo próprio. Devolva apenas JSON válido."

Salvar em `{{PASTA}}/_analise.json`.

### Etapa 1.5 — Checagem de bloqueadores

Ler `_analise.json:bloqueadores`. Se houver entrada com `criticidade = ALTA`:

1. NÃO avançar para etapa 2.
2. Apresentar ao usuário a lista de bloqueadores com `acao_recomendada` de cada um.
3. Aguardar instrução explícita do usuário (resolver, ignorar com risco, abortar).

### Etapa 2 — Consulta ao vault e contrato de rebate

Invocar o subagent `consultor-vault-rmc` com prompt:

> "Dado {{PASTA}}/_analise.json, leia o vault em `$OBSIDIAN_VAULT_RMC/Modelos/ReplicasRMC/`. Aplique as 16 regras de adaptação. Gere DOIS arquivos: _plano.json (plano editorial) e _contrato_rebate.json (cobertura 100% das teses do banco com seção, fundamentos, criticidade e min_paragrafos)."

Salvar em `{{PASTA}}/_plano.json` e `{{PASTA}}/_contrato_rebate.json`.

### Etapa 3 — Redação

Invocar o subagent `redator-replica-rmc` com prompt:

> "Gere a réplica .docx baseada em _analise.json + _plano.json + _contrato_rebate.json em {{PASTA}}. Salve em {{PASTA}}/Réplica - {{CNJ-resumido}} - {{NOME_AUTOR}}.docx. Estrutura espelhada à contestação (preliminares antes do mérito). Densidade dos parágrafos do modelo do escritório. ZERO travessão (—) ou hífen (-) como aposto. Listas em a), b), c) ou i, ii, iii. Autovalidação obrigatória dos 11 itens antes de devolver."

### Etapa 4 — Revisão

Invocar o subagent `revisor-replica-rmc` com prompt:

> "Valide {{PASTA}}/Réplica*.docx. Cobertura 100% do _contrato_rebate.json. Severidade graduada nos achados. Word Comments embutidos no .docx (não gerar relatório paralelo). Resumo no chat com cobertura métrica e classificação APTO / APTO COM RESSALVAS / AJUSTES NECESSÁRIOS."

### Etapa 5 — Iteração

Se classificação AJUSTES NECESSÁRIOS, salvar `_ajustes_v<N>.md` e re-invocar o redator com esse arquivo como feedback. Máximo **2 iterações**. Após 2, entregar com classificação AJUSTES RESIDUAIS e alerta no final da resposta.

### Etapa 6 — Ficha de aprendizado

Criar ficha em `$OBSIDIAN_VAULT_RMC/Aprendizado/ReplicasRMC/YYYY-MM-DD-<slug-cliente>-<slug-comarca>.md` usando o template `_template.md` do vault, pré-preenchida com os metadados do caso e os padrões detectados pelo revisor.

## Entrega ao usuário — formato fixo

No final, responder ao usuário com mensagem curta neste formato exato:

```
Réplica gerada.

Arquivo: {{PATH_DOCX}}
Ficha: {{PATH_FICHA}}

Classificação: {{APTO | APTO COM RESSALVAS | AJUSTES APLICADOS | AJUSTES RESIDUAIS}}
Cobertura de teses do banco: {{N}}/{{N}} (100%)
Pontos de atenção: {{LISTA_CURTA}}
```

O `.docx` da réplica já vem com Word Comments do revisor embutidos no parágrafo problemático (apenas CRÍTICOS e MÉDIOS, sem poluir com COSMÉTICOS).

Nada mais. Sem resumo do que foi feito, sem recap, o usuário abre o `.docx`, revisa e protocola. NÃO usar travessão como aposto na resposta.

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

1. `extract_processo.py` para extração estruturada de PDF processual.
2. `check_ip_rfc1918.py` para validação de IP contra blocos privados.
3. `check_ted_conta_inss.py` para cruzamento conta INSS × conta TED.
4. `detect_2via_massiva.py` para detectar postagem concentrada em faturas.
5. `check_cartao_gemeo.py` para cruzar número do cartão × HISCON.
6. `check_bmg_pre_09_2023.py` para flag de BMG pré-setembro/2023.
7. `check_refin_maquiador_bmg.py` para detectar "crédito de refin" sem queda de saldo.
8. `check_ancora_contestacao.py` para validar âncora de cada afirmação da réplica.
9. `gerar_tabela_onerosidade.py` para os 6 valores adaptativos da tabela do mérito.
10. `gerar_docx.py` para montagem final .docx Cambria.
11. `forcar_cambria.py` para forçar Cambria em .docx existente.
12. `aplicar_layout_modelo.py` para aplicar timbre + estilos + alinhamentos do modelo do vault.

## O que esta skill NÃO faz

1. Não redige inicial, apelação ou cumprimento.
2. Não negocia acordo.
3. Não analisa HISCON isoladamente (usar skill `analise-cadeias-hiscon`).
4. Não fatia PDF sozinha (usa skill `fatiar-processo`).

## Retomada em nova sessão

Se a skill for interrompida no meio (ex: contexto acaba), retomar pelo JSON salvo:

1. Se existir `_analise.json` e não `_plano.json`: começar da etapa 1.5 (checagem de bloqueadores) e seguir para etapa 2.
2. Se existir `_plano.json` mas não `_contrato_rebate.json`: começar da etapa 2 com prompt parcial pedindo só o contrato.
3. Se existir os três JSONs e não `.docx`: começar da etapa 3.
4. Se existir `.docx` sem revisão: começar da etapa 4.

## Referências cruzadas

1. Skill `fatiar-processo` — pré-requisito se PDF consolidado.
2. Skill `conferencia-processual` — usada internamente pelo revisor.
3. Skill `analise-cadeias-hiscon` — NÃO é chamada aqui; usar em triagem antes da inicial.
