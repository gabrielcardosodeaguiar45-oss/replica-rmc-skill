---
tipo: tese-modular
categoria: nossas
nome: onerosidade-excessiva-rcc
obrigatoria-no-merito: true
requer-tabela: true
calculavel: true
tags: [tese, nossa, rcc, rmc, merito, obrigatoria, onerosidade, tabela]
---

# Tese — Onerosidade excessiva do cartão RMC/RCC (com tabela)

> **Obrigatória em toda réplica RCC/RMC**. Padrão histórico do escritório: "explica qual foi a estimativa de prejuízo da parte". Junto com "margem-livre-consignado-tradicional", são as duas teses nucleares do mérito.

## Quando entra

**Sempre**, em toda réplica RMC/RCC. Não há cenário em que não se aplique — o cartão consignado é estruturalmente oneroso (dívida rotativa perpétua).

## Onde entra na peça

Heading 2, dentro de "DOS FUNDAMENTOS JURÍDICOS DOS PEDIDOS", logo **antes** de "DA PRÁTICA ABUSIVA — SÚMULA 532" e **antes** de "DOS DANOS MORAIS". A posição importa: a onerosidade abre caminho para o cálculo dos danos.

Título sugerido: **DA ONEROSIDADE EXCESSIVA DO CARTÃO RCC** (ou RMC conforme o caso).

## Estrutura do bloco

### Parágrafo 1 — intro (1 só)

> Ponto central e quantitativo: o contrato de RCC impugnado configura dívida manifestamente onerosa para o consumidor. A simples comparação entre o valor efetivamente emprestado e o valor que a parte autora já pagou comprova a desproporção:

### Tabela — 6 colunas × 2 linhas

| Valor do empréstimo | Início dos descontos | Valor médio das parcelas | Nº de parcelas pagas | Valor pago até o momento | Valor supostamente refinanciado |
|---|---|---|---|---|---|
| R$ X,YZ | MM/AAAA | R$ X,YZ | N | R$ X,YZ | R$ X,YZ ou — |

Fórmulas:
1. **Valor do empréstimo** = soma dos TEDs (`_analise.json:teds[*].valor`) ou, na ausência, `contrato_principal.limite`.
2. **Início dos descontos** = mês seguinte a `contrato_principal.data_averbacao`.
3. **Valor médio das parcelas** = `contrato_principal.parcela_media`.
4. **Nº de parcelas pagas** = meses decorridos de "início dos descontos" até a data da réplica (inclusivo).
5. **Valor pago até o momento** = nº parcelas × parcela média.
6. **Valor supostamente refinanciado** = `_analise.json:faturas.valor_refin_maquiador` se detectado; senão "—" (traço).

### Parágrafo 2 — números frios (1)

> Em números frios, Excelência, o Banco emprestou R$ X,YZ (por extenso) à parte autora, e esta já pagou, em N (por extenso) parcelas mensais consecutivas, o valor aproximado de R$ Y,ZW (por extenso) — ou seja, cerca de R$ ΔVALOR (por extenso) a mais que o valor originário do empréstimo, equivalente a aproximadamente P% de excedente. Frise-se: o cálculo considera o valor médio das parcelas; o valor exato a ser restituído deverá ser apurado em cumprimento de sentença.

### Parágrafo 3 — conclusão de onerosidade estrutural (1)

> O mais grave, Excelência, é que, diferentemente do empréstimo consignado tradicional — que se extingue com o pagamento das parcelas pactuadas —, o cartão de crédito consignado NUNCA SE ENCERRA automaticamente. O saldo devedor é reciclado indefinidamente, mantendo a parte autora presa a descontos perpétuos enquanto viver beneficiária do INSS, salvo intervenção judicial. Configurada está, portanto, a onerosidade excessiva superveniente e, mais precisamente, a onerosidade estrutural da modalidade contratada — fruto direto do vício de informação e consentimento narrado nos tópicos anteriores.

## Automação da tabela

O script `scripts/gerar_tabela_onerosidade.py` (a criar) calcula os 6 valores a partir do `_analise.json` e devolve um dicionário. O redator só insere.

## Precedentes úteis

1. STJ, Tema 929 / EAREsp 600.663 — dobro integral.
2. STJ, Súmula 532 — prática abusiva de envio de cartão não solicitado.
3. TJAL, Ata Seção Cível — cláusula 12 (descontos de grandes montas como dano moral in re ipsa).
4. REsp 2.159.442/PR, Min. Nancy Andrighi — hash e vícios digitais (usado em complemento).

## Ver também

1. [[margem-livre-consignado-tradicional]] — tese irmã (entram juntas).
2. [[../../regras-de-adaptacao]] — regra 18.
