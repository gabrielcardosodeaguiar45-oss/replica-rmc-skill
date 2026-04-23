---
tipo: biblioteca-frases
tags: [replica, rmc, rcc, frases-modelo, redacao]
atualizado-em: 2026-04-23
---

# Biblioteca de frases-modelo para rebates

Esqueletos de parágrafo com placeholders `{{VAR}}` para serem preenchidos com dados REAIS do `_analise.json`. Cada frase-modelo tem ID único referenciado em `_contrato_rebate.json:frases_modelo_aplicaveis`.

## Regras de uso

1. **Sempre injetar dados reais** (valor, data, página, nome). Frase-modelo sem injeção fica genérica e abre flanco para o adversário.
2. **Reescrever em torno da frase-modelo, não copiar.** A frase é ponto de partida, não produto final. Adaptar a estrutura, ordem das ideias e conectivos para o caso específico.
3. **Combinar com outros parágrafos do bloco.** Cada subseção do mérito tem ao menos 3 parágrafos densos. Frase-modelo cobre 1, demais são redação livre fundamentada no contrato.
4. **Sem travessão como aposto.** Trocar todos por vírgulas, parênteses ou frase separada.

## Frases por categoria

### F.PRELIM.LITISP.01 — Litispendência (rebate genérico)

```
Sustenta a Requerida, em sua peça defensiva, a configuração de litispendência com o(s) processo(s) {{CNJ_DUPLICATA_BANCO}}. A alegação não procede. O art. 337, §§ 1º e 2º, do Código de Processo Civil exige, para a configuração da litispendência, a tríplice identidade entre as ações: mesmas partes, mesma causa de pedir e mesmo pedido. O ônus de demonstrar essa identidade recai inteiramente sobre o arguente, e a Requerida limitou-se a citar números de processo sem juntar cópia das iniciais correspondentes ou demonstrar, item a item, a coincidência exigida pela norma. A simples afirmação de que existem outras ações em curso, sem prova robusta da tríplice identidade, é insuficiente para a configuração da preliminar e não pode ser acolhida.
```

Variáveis: `CNJ_DUPLICATA_BANCO` (lista CSV).

### F.PRELIM.PROCURACAO.01 — Procuração desatualizada ou genérica

```
Aduz a parte Requerida que a procuração outorgada pela autora seria genérica ou estaria desatualizada. A alegação revela leitura desatenta dos autos. A procuração juntada à petição inicial (página {{PAG_PROCURACAO}} dos autos) outorga poderes ad judicia et extra para o foro em geral, dentro dos limites do art. 105 do Código de Processo Civil, e contém menção expressa à matéria objeto da ação. Eventual exigência de poderes específicos somente se justifica quando a lei expressamente impõe (art. 105, parte final, do CPC), o que não se verifica nesta hipótese. A jurisprudência consolidada do STJ rechaça o formalismo excessivo em matéria de mandato judicial, especialmente em ações de consumo movidas por idoso hipossuficiente.
```

Variáveis: `PAG_PROCURACAO`.

### F.PRELIM.INEPCIA.01 — Inépcia da inicial (genérico)

```
A preliminar de inépcia veiculada pela Requerida não comporta acolhimento. A petição inicial atende integralmente aos requisitos do art. 319 do CPC: contém qualificação completa das partes, indicação dos fatos e fundamentos jurídicos do pedido, formulação clara do pedido com suas especificações, valor da causa, provas pretendidas e opção pela realização ou não de audiência de conciliação. A causa de pedir está delineada com precisão, qual seja, o vício de consentimento na contratação da modalidade de cartão de crédito consignado, com descontos consequentes na margem do benefício previdenciário da autora. Não há contradição lógica entre os pedidos, tampouco ausência dos requisitos legais. A pretensão da Requerida configura verdadeira tentativa de obstaculizar a prestação jurisdicional por meio de tecnicismo desprovido de amparo no caso concreto.
```

### F.PRELIM.COMPRRES.01 — Comprovante de residência em nome de terceiro

```
Sustenta a Requerida que o comprovante de residência juntado estaria em nome de terceiro. A alegação merece pronto repúdio. O art. 73, § 3º, do CPC, com redação dada pelo CDC, autoriza o ajuizamento da ação no foro do domicílio do consumidor, e a comprovação de residência por documento em nome de familiar com quem coabita constitui prova válida e amplamente admitida pela jurisprudência. {{NOME_TERCEIRO}}, titular do comprovante apresentado, é {{RELACAO_PARENTESCO_OU_COABITANTE}} da autora, fato comprovado por declaração nos autos. A exigência de comprovante exclusivamente nominal contraria a realidade socioeconômica da autora, idosa, hipossuficiente, beneficiária de aposentadoria por {{TIPO_BENEFICIO}} cujo valor mensal não comporta a manutenção de contas em seu nome.
```

Variáveis: `NOME_TERCEIRO`, `RELACAO_PARENTESCO_OU_COABITANTE`, `TIPO_BENEFICIO`.

### F.MERITO.MODALIDADE.01 — Manutenção da modalidade até liquidação

```
Pretende ainda a Requerida a manutenção da modalidade contratada e dos descontos em folha até a liquidação integral do débito. O pedido, contudo, é juridicamente impossível. Reconhecida a nulidade do contrato por vício de consentimento, os efeitos da declaração retroagem à data da contratação, na forma do art. 182 do Código Civil. Manter os descontos significaria perpetuar os efeitos de negócio jurídico nulo, em contradição com a própria pretensão declaratória deduzida na inicial. A nulidade desfaz o vínculo contratual desde a origem e impõe a restituição das partes ao estado anterior, com cessação imediata dos descontos e devolução dos valores indevidamente retidos.
```

### F.MERITO.PRESCRICAO.01 — Prescrição (rebate)

```
Não procede a tese prescricional invocada pela Requerida. O prazo aplicável às pretensões de repetição de indébito decorrentes de relação de consumo é decenal, na forma do art. 205 do Código Civil, conforme entendimento consolidado pela Segunda Seção do STJ no julgamento dos EAREsp 1.280.825/RJ, com marco inicial em 30/03/2021 para os contratos cuja cobrança indevida persistia naquela data. A averbação do contrato impugnado data de {{DATA_AVERBACAO_CONTRATO}}, e os descontos perduram até a presente data, o que afasta integralmente a prescrição. Mesmo na hipótese aventada de aplicação do prazo trienal do art. 206, § 3º, IV, do CC, o termo inicial seria a data do conhecimento inequívoco do vício pela autora, igualmente fora da janela prescricional.
```

Variáveis: `DATA_AVERBACAO_CONTRATO`.

### F.MERITO.COMPENSACAO.01 — Pedido de compensação dos TEDs (anuência)

```
A autora não nega o recebimento dos valores transferidos pela Requerida, no total de R$ {{VALOR_TOTAL_TED_POR_EXTENSO}} ({{VALOR_TOTAL_TED_NUMERICO_POR_EXTENSO_EXTENSO}}), distribuídos em {{NUMERO_TEDS}} transferência(s) realizada(s) em {{DATAS_TEDS_FORMATADAS}}. Reconhece-se expressamente o crédito e desde já ANUI-SE com a compensação dos referidos valores no montante a ser restituído pela Requerida em sede de cumprimento de sentença. A anuência ao recebimento, contudo, não convalida o vício de consentimento quanto à modalidade contratada: a autora pretendia empréstimo consignado tradicional, não cartão de crédito consignado com saldo rotativo perpétuo. O depósito do principal foi efetivamente percebido, mas a forma contratual imposta pelo banco, com seus encargos abusivos e ausência de previsibilidade de quitação, é o vício a ser declarado.
```

Variáveis: `VALOR_TOTAL_TED_POR_EXTENSO`, `NUMERO_TEDS`, `DATAS_TEDS_FORMATADAS`.

### F.MERITO.HASH_DIGITAL.01 — Hash do laudo cobre só contrato posterior

```
A Requerida juntou aos autos relatório de formalização eletrônica com hash SHA-256 {{HASH_RESUMIDO}} e identificador de sessão {{ID_SESSAO_RESUMIDO}}, alegando comprovação da assinatura eletrônica avançada do contrato. Análise atenta da documentação revela, contudo, que o referido hash e o identificador de sessão vinculam-se exclusivamente ao contrato {{CONTRATO_COBERTO_PELO_HASH}}, datado de {{DATA_CONTRATO_COBERTO}}, e não ao contrato originário de {{DATA_CONTRATO_ORIGINARIO}} que constitui o cerne desta demanda. O contrato originário, supostamente firmado em {{DATA_CONTRATO_ORIGINARIO}}, não conta com qualquer evidência criptográfica de assinatura eletrônica, biometria ou geolocalização, o que é incompatível com a tese defensiva e fragiliza por completo a documentação juntada. O STJ, no julgamento do REsp 2.159.442/PR (Min. Nancy Andrighi, 24/09/2024), reafirmou que a ausência de hash é vício insanável da formalização eletrônica e impede a presunção de autenticidade.
```

Variáveis: `HASH_RESUMIDO`, `ID_SESSAO_RESUMIDO`, `CONTRATO_COBERTO_PELO_HASH`, `DATA_CONTRATO_COBERTO`, `DATA_CONTRATO_ORIGINARIO`.

### F.MERITO.DANOS.01 — Dano moral in re ipsa para idoso hipossuficiente

```
A configuração do dano moral é inequívoca. A autora, com {{IDADE_AUTOR}} anos de idade, hipossuficiente, dependente exclusivamente de aposentadoria por {{TIPO_BENEFICIO}} no valor mensal líquido de R$ {{RENDA_MENSAL}}, foi submetida a descontos contínuos em sua única fonte de subsistência sem ter contratado conscientemente a modalidade que lhe foi imposta. A jurisprudência do TJAM, no precedente {{PRECEDENTE_TJAM}}, fixou o quantum compensatório de R$ {{VALOR_DANO_MORAL_POR_EXTENSO}} para hipóteses análogas, considerando a natureza alimentar do benefício, a vulnerabilidade etária e a má-fé bancária na imposição da modalidade. A presente demanda preenche todos os elementos para a fixação do quantum no mesmo patamar, sem necessidade de comprovação específica do abalo moral, configurando-se a hipótese de dano in re ipsa.
```

Variáveis: `IDADE_AUTOR`, `TIPO_BENEFICIO`, `RENDA_MENSAL`, `PRECEDENTE_TJAM`, `VALOR_DANO_MORAL_POR_EXTENSO`.

### F.MERITO.INVERSAO_ONUS.01 — Inversão do ônus da prova

```
Por fim, requer a parte autora a inversão do ônus da prova, com fulcro no art. 6º, VIII, do CDC, para que a Requerida comprove os fatos constitutivos do direito que invoca: a regularidade da contratação, a ciência inequívoca da autora quanto à modalidade de cartão de crédito consignado, a existência de informações claras e adequadas sobre os encargos e a ausência de vício no consentimento. A hipossuficiência técnica e econômica da autora é evidente: idosa de {{IDADE_AUTOR}} anos, com escolaridade {{ESCOLARIDADE_AUTOR}}, beneficiária do INSS, sem condições materiais de produzir contraprova das alegações da instituição financeira. A inversão é medida que se impõe e que decorre tanto do CDC quanto da distribuição dinâmica do ônus prevista no art. 373, § 1º, do CPC.
```

Variáveis: `IDADE_AUTOR`, `ESCOLARIDADE_AUTOR`.

## Como o redator escolhe e adapta

1. Lê `_contrato_rebate.json:frases_modelo_aplicaveis` para cada tese.
2. Carrega esta biblioteca, localiza a(s) frase(s) por ID.
3. Substitui placeholders `{{VAR}}` pelos valores reais do `_analise.json`.
4. Adapta a redação ao caso (não copia mecanicamente, escreve em torno da frase).
5. Adiciona parágrafos complementares para atingir `min_paragrafos`.
6. Garante densidade do modelo do escritório (6 a 12 linhas no mérito).
7. Varre o resultado para travessões usados como aposto e substitui.

## Crescimento da biblioteca

A cada caso novo onde uma tese do banco não tem frase-modelo correspondente, criar nova entrada aqui. Manter ID padronizado: `F.<categoria>.<tese-id>.NN`. Categorias: `PRELIM` (preliminar), `MERITO` (mérito), `LAYOUT` (parágrafos estruturais), `FECHO` (fechamento).
