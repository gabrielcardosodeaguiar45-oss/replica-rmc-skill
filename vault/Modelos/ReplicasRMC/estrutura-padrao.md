---
tipo: referencia
tags: [replica, rmc, rcc, estrutura, bancario]
atualizado-em: 2026-04-22
---

# Estrutura padrão da réplica — RMC/RCC

Deduzida a partir de todos os modelos do acervo (Alagoas, Amazonas, Bahia, MG, SC). Uma réplica do escritório segue **sempre** os 9 blocos abaixo, nesta ordem.

## Os 9 blocos

### Bloco 1 — Endereçamento

Cabeçalho ao juízo, identificação do processo.

```
EXCELENTÍSSIMO(A) SENHOR(A) DOUTOR(A) JUIZ(A) DE DIREITO DA {{VARA}} DA COMARCA DE {{COMARCA}}/{{UF}}

Processo nº {{CNJ}}
```

### Bloco 2 — Título-manchete (opcional mas frequente)

Frase em caixa-alta sintetizando a tese nuclear (2-3 linhas). Serve de "título interno" do bloco argumentativo principal. Exemplos reais do acervo:

1. `CONTRATAÇÃO IRREGULAR – INSTRUMENTO SUPOSTAMENTE FIRMADO POR PESSOA ANALFABETA, SEM ASSINATURA À ROGO, SOMENTE SUBSCRITO POR DUAS TESTEMUNHAS.`
2. `A INSTITUIÇÃO BANCÁRIA NÃO TROUXE AOS AUTOS O CONTRATO OBJETO DA PRESENTE LIDE`
3. `CONTRATO SUPOSTAMENTE CELEBRADO POR PESSOA IDOSA COM ACEITES REALIZADOS EM POUCOS SEGUNDOS – RAPIDEZ ANORMAL – AUSÊNCIA DE INFORMAÇÃO CLARA AO CONSUMIDOR`
4. `CONTRATAÇÃO FEITA SUPOSTAMENTE EM CAIXA ELETRÔNICO – EXISTÊNCIA DE IRREGULARIDADES – JUNTADA SOMENTE DE TELAS SISTÊMICAS – DOCUMENTOS UNILATERAIS.`
5. `CONTRATO DESACOMPANHADO DE TERMO DE CONSENTIMENTO ESCLARECIDO – DESCUMPRIMENTO DO ART. 21-A DA IN INSS/PRES Nº 28/2008`

Usar quando houver uma tese central forte. Omitir quando o caso é "réplica padrão" sem particularidade protagonista.

### Bloco 3 — Preâmbulo

Parágrafo de qualificação + verbo núcleo.

```
{{NOME_AUTOR}}, já devidamente qualificad{{O_A}} nos autos do processo em epígrafe, que
move contra {{BANCO_REU}} também já devidamente qualificado, vem, à presença
de Vossa Excelência, por meio de seu{{S}} procurador{{ES}} signatário{{S}},
apresentar, com fulcro no art. 350 do Código de Processo Civil, MANIFESTAÇÃO
À CONTESTAÇÃO, pelas razões de fato e de direito a seguir expostas:
```

### Bloco 4 — Síntese da contestação

Resumo em um parágrafo do que o banco levantou. Formato recorrente (reciclável):

```
SÍNTESE DA CONTESTAÇÃO

Excelência, a Requerida apresentou defesa em forma de contestação: preliminarmente
{{LISTA_PRELIMINARES_BANCO}}. Em prejudicial do mérito {{LISTA_PREJUDICIAIS}}. No mérito
arguiu que a parte autora contratou o serviço em questão, a impossibilidade de
inversão do ônus probatório e a inaplicabilidade do Código de Defesa do Consumidor,
a ausência de requisitos de indenizar, a impossibilidade de declarar inexigíveis
os débitos, a desnecessidade de interposição de ação judicial para o cancelamento
do cartão, a ausência de violação ao dever de informação, a não configuração de
venda casada, a impossibilidade do pedido de liberação de margem e de repetição
do indébito.

Contudo, em que pese a instituição financeira ré tente demonstrar a suposta
contratação do cartão de crédito, restará comprovado a ofensa do direito da
parte autora, conforme verifica-se a seguir:
```

### Bloco 5 — Tempestividade

Curta. Invariável no esqueleto.

```
DA TEMPESTIVIDADE

A presente Manifestação à Contestação é tempestiva, haja vista que o prazo para
apresentação é de 15 (quinze) dias, conforme artigo 350 do CPC/2015 e, da análise
dos autos, verifica-se que o prazo se finda em {{DATA_FIM_PRAZO_POR_EXTENSO}}.
```

### Bloco 6 — Preliminares

Rebater na **ordem que o banco levantou** (o manual é explícito: bancos normalmente não seguem a ordem do CPC, e temos que seguir a ordem da contestação para não dar "cara de não-resposta"). Módulos aplicáveis vêm da biblioteca [[teses-modulares/impugnacao/_index|impugnação de preliminares do banco]] (14 teses).

Preliminares **nossas** (levantadas por nós) vêm **depois** das impugnações das do banco, em bloco separado com o subtítulo "PRELIMINARMENTE - ...". Módulos de [[teses-modulares/nossas/_index|preliminares nossas]] (11 teses).

### Bloco 7 — Fundamentos jurídicos / mérito

Subtítulo canônico:

```
DOS FUNDAMENTOS JURÍDICOS DOS PEDIDOS
```

Depois, sub-seções conforme a estratégia do caso. **Ordem-padrão que eu deduzi** do modelo-mãe de Amazonas (mais robusto):

1. **DOS PARÂMETROS PARA A VALIDADE DOS CONTRATOS DE CARTÃO RMC** — invoca IRDR/Ata da Seção e faz tabela comparativa `Requisitos impostos × Provas constantes nos autos`.
2. **Art. 21 e 21-A da IN INSS/PRES nº 28/2008** — lista os 8 requisitos obrigatórios + obrigatoriedade do TCE a partir de dez/2018.
3. **DA IRREGULARIDADE DA CONTRATAÇÃO DIGITAL** (quando aplicável) — 5 sub-subseções:
   a. Do contrato digital (Lei 14.063/2020 — 3 tipos de assinatura).
   b. Exigências para selfie liveness (IEEE Std 2790/2020, ISO/IEC 30107-3, ISO/IEC 29.794-5, iBeta 2).
   c. Da assinatura inválida (validador ITI).
   d. Do código HASH (REsp 2.159.442/PR Nancy Andrighi) — duas variantes: ausente ou incompatível.
   e. Das propriedades do documento (metadados PDFium, data de criação posterior).
   f. Da trilha de auditoria (IP, geolocalização, empresa terceirizada em cidade diversa).
   g. Da ausência de geolocalização e assinatura digital válida.
   h. Da imprescindibilidade de perícia digital.
4. **DO VÍCIO DE INFORMAÇÃO E CONSENTIMENTO** — parte autora achava que era empréstimo consignado usual.
5. **DAS FATURAS DO CARTÃO - SEM USO DO CARTÃO** — se não há compras, nunca foi usado; banco não comprovou envio.
6. **QUANTO AOS COMPROVANTES DE TED** — TEDs sem autorização = superendividamento.
7. **DA PRÁTICA ABUSIVA – NULIDADE CONTRATUAL** — arts. 51 IV, 39 III, 14 CDC. Súmula 532 STJ.
8. **TEORIA DO ILÍCITO LUCRATIVO** — CRIME CONTRA AS RELAÇÕES DE CONSUMO (Daniel Levy; TJMG Roberto Vasconcellos).
9. **QUANTO À ALEGAÇÃO DE MERO ABORRECIMENTO** — rebater dano moral, citar valor do benefício.
10. **DA RESTITUIÇÃO DOS VALORES** — em dobro a partir de 30/03/2021 (EAREsp 676.608/RS).
11. **DA INVERSÃO DO ÔNUS DA PROVA** — Súmula 297 STJ, art. 6º VIII CDC.
12. **DO DESCONTO DO VALOR MÍNIMO NO BENEFÍCIO** — técnica para maximizar lucro; paga só juros; dívida nunca amortiza.
13. **DA DÍVIDA ETERNA IMPOSTA** — reforço do vício de informação.
14. **DOS HONORÁRIOS ADVOCATÍCIOS** — 20% (ou tabela OAB mínimo R$ 4.000,00, art. 85 §§ 8º e 8º-A CPC).
15. **DO JULGAMENTO ANTECIPADO DO FEITO** — matéria de direito + preclusão.

**Seleção das seções**: nem toda réplica usa todas. A seleção depende do cenário:

| Cenário | Seções obrigatórias |
|---|---|
| Sem contrato | 1, 2, 4, 10, 11, 14, 15 |
| Contrato físico regular | 1, 2, 4, 5, 6, 7, 8, 10, 11, 14, 15 |
| Contrato digital | 1, 2, 3 (todas sub), 4, 5, 6, 7, 8, 9, 10, 11, 14, 15 |
| Analfabeto | 1, 2 + bloco-específico analfabeto + 4, 9, 10, 14, 15 |
| Caixa eletrônico | 1, 2 + bloco-específico caixa eletrônico + 4, 9, 10, 14, 15 |
| Sem TCE (pós dez/2018) | 1, 2 + bloco-específico TCE + 4, 10, 11, 14, 15 |

### Bloco 8 — Dos pedidos

Estrutura recorrente:

```
DOS PEDIDOS

Quanto à preliminar e prejudicial de mérito alegadas pela instituição ré, requer-se
que sejam rechaçadas, haja vista que conforme comprovado pela parte requerente,
não merecem prosperar;

No mérito, diante de todos os argumentos fáticos e de direito até aqui aduzidos,
em razão do vício de informação e da conduta fraudulenta cometida pela instituição
ré, impugna-se totalmente a peça contestatória, bem como todos os documentos
acostados, requerendo a total procedência dos pedidos constantes na peça de
ingresso.

Nestes termos, pede deferimento.
```

Adaptações pontuais conforme cenário (ex.: pedido de perícia digital em contrato digital, pedido de expedição de ofício ao Ministério Público por litigância predatória).

### Bloco 9 — Fechamento

Cidade, data por extenso, assinatura + OAB.

```
{{COMARCA}}/{{UF}}, {{DATA_POR_EXTENSO}}.

{{NOME_SUBSCRITOR}}
OAB/{{UF_OAB}} {{NUMERO_OAB}}
```

Subscritores recorrentes:

1. **Eduardo Fernando Rebonatto** — OAB/AM A2118 (Amazonas; advogado antigo; ainda há ações em nome dele).
2. **Patrick** — (OAB/AM, número a confirmar; advogado atual em Amazonas).
3. **Subscritor histórico** — (OAB a confirmar; modelos antigos da pasta histórica).

## Placeholders canônicos

Usar sempre em CAIXA-ALTA entre chaves duplas.

| Placeholder | O que é | Onde extrair |
|---|---|---|
| `{{CNJ}}` | Número do processo | Capa do PDF |
| `{{VARA}}` | Vara / Unidade | Capa do PDF |
| `{{COMARCA}}` | Comarca | Capa do PDF |
| `{{UF}}` | Estado | Capa do PDF |
| `{{NOME_AUTOR}}` | Nome completo do autor | Inicial, RG, procuração |
| `{{NOME_AUTOR_GENERO}}` | "qualificado" ou "qualificada" | Idem |
| `{{BANCO_REU}}` | Razão social do banco | Contestação |
| `{{DATA_FIM_PRAZO}}` | Data limite da réplica | 15 dias úteis a partir da intimação |
| `{{DATA_PROTOCOLO}}` | Data do protocolo por extenso | A definir |
| `{{MOV_CONTESTACAO}}` | Movimentação da contestação | Autos |
| `{{MOV_CONTRATO}}` | Movimentação da CCB | Autos |
| `{{MOV_FATURAS}}` | Movimentação das faturas | Autos |
| `{{NUMERO_CCB}}` | Número da CCB | Contrato |
| `{{DATA_CCB}}` | Data do contrato | CCB |
| `{{VALOR_BENEFICIO}}` | Valor líquido do benefício | Extrato INSS |
| `{{VALOR_DESCONTO_MENSAL}}` | Valor da parcela RMC descontada | Extrato INSS |
| `{{NOME_SUBSCRITOR}}` | Advogado responsável | Conforme caso |
| `{{NUMERO_OAB}}` | OAB do subscritor | — |
| `{{UF_OAB}}` | UF da OAB | — |

## Ver também

- [[_MOC]]
- [[manual-consolidado]]
- [[erros-herdados]]
- [[checklist-protocolo]]
- [[teses-modulares/_index]]
