---
tipo: referencia
tags: [replica, rmc, rcc, layout, visual]
atualizado-em: 2026-04-26
---

# Configurações visuais — RMC/RCC

Padrão visual **idêntico** ao das [[../Apelacoes/configuracoes-visuais|apelações]]. A peça é gerada **a partir do `.docx` modelo do escritório**, nunca do zero, para preservar timbrado, estilos nomeados e configurações de seção.

## Fonte e estilos nomeados (NÃO Cambria solto)

A peça final usa os **estilos nomeados do modelo** (mesmos das Apelações). Cambria solto em corpo é erro herdado da fase 1 do projeto e foi descontinuado em 2026-04-26 após validação no caso PAN/Maués.

| Estilo do modelo | Uso |
|---|---|
| `Normal` | Endereçamento ao Juízo e identificador "Processo nº ..." da folha de rosto |
| `1. Parágrafo` | Texto corrido do mérito, das preliminares, da síntese, dos pedidos. Sitka Text, justificado, recuo de primeira linha 1cm, entrelinhamento 1,2 |
| `2. Título` | EMENTA + cabeçalhos romanos (I — SÍNTESE DA CONTESTAÇÃO, II — TEMPESTIVIDADE, III — DAS PRELIMINARES, etc.). Segoe UI bold preto #000000, caixa alta |
| `3. Subtítulo` | Subseções principais do mérito (DA IRREGULARIDADE DA CONTRATAÇÃO DIGITAL, DA PRÁTICA ABUSIVA, DOS DANOS MORAIS, etc.). Segoe UI Semibold dourado #B3824C, 11pt |
| `3.1 Subtítulo intermediário` | Sub-subseções dentro do mérito (Da margem livre, Da onerosidade). Segoe UI Semibold dourado |
| `3.1 Subtítulo secundário` | Reservado para divisões internas raras. Franklin Gothic Book bold |
| `4. Citação` | Ementas e trechos de jurisprudência citados. Sitka Text 11pt itálico, recuo aprox. 4cm |
| `5. Lista alfabética` | Listas tipo a), b), c) |

## Itálico tipográfico

Aplicar `run.italic = True` em todos os termos de:

. **Latim jurídico:** *actio nata*, *dies a quo*, *dies ad quem*, *ipsis litteris*, *ipso facto*, *ipso jure*, *in re ipsa*, *data venia*, *maxima venia*, *mutatis mutandis*, *ad nutum*, *ad valorem*, *ad cautelam*, *ad rem*, *ad fim*, *lato sensu*, *stricto sensu*, *in casu*, *in totum*, *in fine*, *ex officio*, *ex tunc*, *ex nunc*, *erga omnes*, *inter partes*, *fumus boni iuris*, *periculum in mora*, *habeas corpus*, *quantum debeatur*, *quantum satis*, *modus operandi*, *amicus curiae*, *obiter dictum*, *ratio decidendi*, *stare decisis*, *status quo*, *status quo ante*, *exempli gratia*, *id est*, *verbi gratia*.
. **Inglês jurídico-técnico:** *duty to mitigate*, *liveness*, *FaceTec*, *deepfake*, *biometric template*.
. **Citações literais entre aspas** com mais de uma frase (trechos da contestação ou de doutrina).

Itálico é tipográfico, não retórico. Não confundir com ênfase de texto comum.

## Folha de rosto (ordem obrigatória)

Toda réplica abre com:

1. **Endereçamento ao Juízo** (estilo `Normal`, bold).
2. **Processo nº** (estilo `Normal`, bold, à direita).
3. **EMENTA do caso** (estilo `2. Título`, bold, justificado, **recuo à esquerda de 4 cm**). CAIXA ALTA, palavras-chave separadas por ponto, cobrindo: tipo de peça, ação, modalidade contratual, pilar técnico do laudo digital, pedidos centrais. Mínimo 5 termos. Exemplo:
    > RÉPLICA À CONTESTAÇÃO. AÇÃO DECLARATÓRIA DE INEXISTÊNCIA DE NEGÓCIO JURÍDICO. CARTÃO DE CRÉDITO CONSIGNADO (RCC). CONTRATAÇÃO DIGITAL. VÍCIO DE CONSENTIMENTO NA MODALIDADE. GEOLOCALIZAÇÃO INCONSISTENTE. AUSÊNCIA DE HASH SHA-256. ONEROSIDADE EXCESSIVA. PEDIDO DE COMPENSAÇÃO DO TED.
4. **Qualificação do autor** (estilo `1. Parágrafo`). O **nome do autor** vai em **negrito** (`run.bold = True` no run que contém o nome).

A ementa não substitui a síntese (cabeçalho "SÍNTESE DA CONTESTAÇÃO"); apenas antecede.

## Numeração e capitalização

**Cabeçalhos principais** (estilo `2. Título`):

. **NUNCA escrever numerais romanos no texto** ("I — SÍNTESE", "II — TEMPESTIVIDADE"). A numeração 1., 2., 3., 4., 5. vem automaticamente do estilo. Texto correto: "SÍNTESE DA CONTESTAÇÃO", "TEMPESTIVIDADE", "DAS PRELIMINARES ARGUIDAS PELA REQUERIDA", "DOS FUNDAMENTOS JURÍDICOS DOS PEDIDOS", "DOS PEDIDOS".
. Mantém CAIXA ALTA.

**Subtítulos** (estilo `3. Subtítulo` e `3.1 Subtítulo intermediário`):

. Capitalização "primeira letra maiúscula apenas", com siglas conhecidas preservadas em caixa alta.
. Exemplos corretos: "Da irregularidade da contratação digital", "Dos parâmetros de validade do contrato RCC — IRDR Tema 5 TJAM", "Da prática abusiva e da nulidade contratual", "Da alegada prescrição trienal".
. Siglas a preservar: RCC, RMC, CCB, IRDR, TJAM, TJAL, TJBA, TJMG, STJ, STF, INSS, OAB, AM, AL, BA, MG, SC, CDC, CPC, CC, TED, BMG, PAN, ICP, FIDC, AGIBANK, FACTA, TCE, IP, CPF, CNPJ, CNJ, B41, B31, B52, BPC.
. **Border bottom (linha horizontal abaixo do parágrafo)** aplicado via XML `w:pBdr w:bottom`. Cor sugerida: `B3824C` (dourado do escritório).

## Alinhamento dos títulos e subtítulos

Os estilos do modelo (`2. Título`, `3. Subtítulo`, `3.1 Subtítulo intermediário`) **já vêm com alinhamento à esquerda**. Cabeçalhos e subtítulos da réplica **não devem ter alignment override** no parágrafo. Quando o redator copia parágrafos de modelo antigo (Cambria centralizado) para o novo modelo, é preciso limpar o `<w:jc>` do `<w:pPr>` antes de aplicar o estilo.

Verificação no `.docx` final: nenhum `2. Título`, `3. Subtítulo` ou `3.1 Subtítulo intermediário` pode estar centralizado. Cabe ao revisor flagar como AJUSTE caso encontre.

## Preliminares — agrupar sob um único cabeçalho

Todas as preliminares ficam dentro de **UM cabeçalho `2. Título`** chamado "DAS PRELIMINARES ARGUIDAS PELA REQUERIDA". Cada preliminar individual vira **subtítulo `3.1 Subtítulo intermediário`**. NÃO criar `2. Título` separado para cada preliminar.

Estrutura correta:

```
2. Título: SÍNTESE DA CONTESTAÇÃO
2. Título: TEMPESTIVIDADE
2. Título: DAS PRELIMINARES ARGUIDAS PELA REQUERIDA
   3.1 Subtítulo intermediário: Da alegada prescrição trienal
   3.1 Subtítulo intermediário: Da alegada ausência de interesse processual
   3.1 Subtítulo intermediário: Da revogação da gratuidade de justiça
2. Título: DOS FUNDAMENTOS JURÍDICOS DOS PEDIDOS
   3. Subtítulo: Dos parâmetros de validade do contrato RCC
   3. Subtítulo: Da irregularidade da contratação digital
   ...
2. Título: DOS PEDIDOS
```

## Margens, timbrado e cabeçalho/rodapé

Vêm do `.docx` modelo do escritório. Não recriar do zero. Trocar apenas:

. Endereçamento, processo, comarca, vara, parte autora.
. Procuradores no fecho (modelos guardam Eduardo / Tiago / Patrick — nunca copiar cego, sempre puxar de `_analise.json:advogado_autor`).

Header (1 imagem de timbrado) e footer (1 imagem de assinatura visual do escritório) ficam intactos.

## Sem imagens no corpo

Réplicas de RMC/RCC com tese de vício de consentimento **não** levam imagens dos autos. Sem prints de CCB, trilha, geolocalização, HISCON dentro do corpo. As únicas exceções são:

. Marcador vermelho "[INSERIR AQUI: print do extrato HISCON ...]" para o advogado colar manualmente antes do protocolo, na seção "DA MARGEM LIVRE".

## Tabelas

Não há tabelas-padrão. As duas que surgem naturalmente:

1. **Requisitos × Provas nos autos** — tabela comparativa do IRDR Tema 5 TJAM ou da Ata da Seção Cível TJAL. 2 colunas.
2. **Onerosidade do cartão** — 6 colunas (Valor do empréstimo / Início dos descontos / Parcela média / Parcelas pagas / Valor pago total / Excesso pago).

## Subscritores

| Estado | Subscritor padrão | OAB |
|---|---|---|
| Amazonas (histórico) | Eduardo Fernando Rebonatto | OAB/AM A2118 |
| Amazonas (atual) | Patrick Willian da Silva | OAB/AM A2638 (suplementar) ou OAB/SC 53969N (origem) |
| Alagoas | (a confirmar) | — |
| Bahia | (a confirmar) | — |
| Minas Gerais | (a confirmar) | — |
| Santa Catarina (matriz) | Eduardo Rebonatto + Tiago de Azevedo Lima | OAB/SC 36592 e 36672 |

A OAB do procurador na peça é a do estado onde a peça é protocolada. Para AM, usar a inscrição AM (suplementar de Patrick = OAB/AM A2638). Para BA, MG, AL — confirmar inscrição local antes de subscrever.

## Ver também

- [[../Apelacoes/configuracoes-visuais|Configurações visuais — Apelações]]
- [[../../Escritorio/dados-escritorio|Dados do escritório]]
- [[erros-herdados#Erros de layout]]
- [[regras-de-adaptacao|Regras de adaptação]]
