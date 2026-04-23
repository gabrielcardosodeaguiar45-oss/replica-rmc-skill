---
tipo: referencia
tags: [replica, rmc, rcc, erros, bancario]
atualizado-em: 2026-04-22
status: inicial
---

# Erros herdados — armadilhas dos modelos RMC/RCC

Armadilhas que costumam ser embutidas nos modelos-base ou que surgem ao reusar teses sem pensar. Lista inicial; será expandida a cada caso paradigma.

## Erros de substituição de dados

### Erro 1 — Nome do banco mãe do modelo

Muitos modelos mencionam "Banco PAN" ou "Banco BMG" ou "Banco Inbursa" no meio do texto, mesmo em seções genéricas. Regex mental para varrer: todo nome de banco deve corresponder ao banco réu do caso concreto.

### Erro 2 — Gênero do autor

Modelos alternam "autor" e "autora". Verificar qualificação inicial (RG/inicial) e padronizar para um único gênero em toda a peça. Palavras a conferir: autor/autora, consumidor/consumidora, beneficiário/beneficiária, Apelante, Requerente.

### Erro 3 — Comarca e vara

Cabeçalho tem sempre a comarca do processo paradigma do arquivo-fonte. Nunca esquecer de substituir. Checklist: "DA COMARCA DE {{COMARCA}}/{{UF}}".

### Erro 4 — Data-limite do prazo

Modelo tem data específica ("se finda em 17 de abril de 2026"). Recalcular do zero com base na intimação real.

### Erro 5 — Número do processo (CNJ)

Sempre vem do arquivo-fonte. Substituir.

## Erros de tese

### Erro 6 — Tese A vs B (inexistência × anulabilidade)

**Regra**: ação declaratória de inexistência de relação jurídica → pedido é **declaração de inexistência** (Tese A, plano da existência). Nunca "anulação" (Tese B, plano da validade, vício de consentimento, art. 178 CC, decadência quadrienal).

Modelos mais antigos misturam. Varrer por "anulação", "anulabilidade", "vício de consentimento art. 178" e substituir.

### Erro 7 — Copiar seção de contrato digital em contrato físico

Se o contrato é físico, não faz sentido trazer hash, selfie liveness, validador ITI, metadados PDFium. Verificar modalidade antes de reusar [[teses-modulares/nossas/contrato-digital-contratacao-rapida]].

### Erro 8 — Geolocalização distante quando é compatível

Regra de ouro da Fase 2 das apelações, herdada aqui: **ler o laudo do banco antes de alegar geolocalização incompatível**. Se o IP/lat-long bate com a residência do autor, não levantar essa sub-tese.

### Erro 9 — Hash ausente × hash incompatível

São duas variantes **excludentes**. Escolher uma conforme o laudo. Nunca alegar as duas juntas.

### Erro 10 — Pedido de perícia digital em Amazonas

Manual indica que AM quase nunca defere perícia digital. Em MG e AL, pedir. Em AM, evitar — ou pedir pro forma mas sem insistir.

### Erro 11 — Tutela de urgência na inicial

Se por algum motivo a inicial pediu tutela, a tese [[teses-modulares/impugnacao/tutela-urgencia|rebater tutela]] não pode ser usada como argumento de "contestação genérica do banco". Confirmar sempre que a inicial NÃO pediu tutela.

## Erros de estrutura

### Erro 12 — Ordem das preliminares

Rebater **na ordem da contestação**, não na ordem do CPC. Bancos fazem contestações bagunçadas — nossa resposta segue a bagunça deles para não parecer "não resposta".

### Erro 13 — Preliminares nossas antes das impugnações

Colocar **impugnações das preliminares do banco primeiro** (bloco 6), depois **preliminares nossas** (bloco 6 contínuo). Nunca misturar os dois no mesmo fluxo sem separação.

### Erro 14 — Sub-seção de mérito para caso que não precisa

Consultar [[estrutura-padrao#Seleção das seções]] — nem toda réplica tem todas as 15 seções de mérito. Escolher conforme cenário.

### Erro 15 — Pedidos genéricos

Pedidos devem refletir a estratégia específica do caso. Ex.: pedido de expedição de ofício ao MP por litigância predatória só quando a peça desenvolveu a teoria do ilícito lucrativo.

## Erros de fontes e jurisprudência

### Erro 16 — Citar TJ errado

Ata Seção Cível AL não se aplica a AM. IRDR Tema 5 TJAM não se aplica a AL. IRDR MG não se aplica em outros estados. Conferir jurisdição.

### Erro 17 — Marco 30/03/2021 sem separar pré/pós

Restituição em dobro só se aplica a descontos pós 30/03/2021 (EAREsp 676.608/RS). Para descontos anteriores, pedir restituição simples. Separar os períodos no pedido.

### Erro 18 — Súmula fora do contexto

Súmula 532 STJ (cartão sem solicitação) aplica-se ao cartão consignado — sim. Mas alguns modelos aplicam em ação de RMC onde o cartão foi "oferecido" e "aceito"; nesse caso, dimensionar com cuidado.

## Erros de layout

### Erro 19 — Fonte diferente de Cambria

Todo texto em Cambria (ver [[configuracoes-visuais]]). Colagem de trechos de outros arquivos frequentemente arrasta Segoe UI, Times New Roman, Sitka Text. Rodar o script `forcar_cambria_global.py` no final.

### Erro 20 — Imagens em réplica RMC/RCC

Regra: **não há imagens em réplica RMC/RCC com tese de vício de consentimento**. Se algum modelo trouxer imagem residual, remover.

### Erro 21 — Lista com traços

Padrão interno: listas com a), b), c), d) ou i, ii, iii, iv. Não usar traços como marcador em texto corrido.

## Erros consolidados na Fase 3 (trinca Caso 1 / Caso 2 / Caso 3 — 22/04/2026)

### Erro 22 — "Manaus/AM" no fecho quando a comarca real é outra

**Origem:** Caso 1 (Caapiranga). Modelo-paradigma AM herda "Manaus/AM" no fecho. Precisa ser substituído caso a caso.

**Regra:** separar **comarca do cabeçalho** (item 3 do Bloco 1 do checklist) da **cidade do fecho** (Bloco 6). Ambas precisam bater com a comarca real — Caapiranga/AM no Caso 1, Boa Vista do Ramos/AM na Caso 2, Maués/AM no Caso 3.

**Nota importante (advogado sênior):** assinar em cidade diferente dentro do mesmo estado não invalida a peça, mas "Manaus/AM" em caso de Caapiranga denuncia uso mecânico de modelo. Trocar sempre.

### Erro 23 — Alegar "IP privado" sem conferir faixa do RFC 1918

**Origem:** Caso 2 (IP 172.15.225.64 alegado como privado — faixa **não é** RFC 1918; privadas são 10.0.0.0/8, 172.16-31.0.0/12, 192.168.0.0/16).

**Regra:** nunca classificar IP como "privado" sem conferir a faixa. Se for público (operadora móvel, banda larga residencial), descrever como IPv4/IPv6 dinâmico não identificável sem requisição ao provedor. Risco se mantido errado: o banco derruba a tese apontando a classificação errada.

### Erro 24 — Ignorar RCC gêmeo do mesmo banco

**Origem:** Caso 1 + Caso 2 + Caso 3 (3 em 3 casos). Cliente RMC tem também um RCC ativo do mesmo banco, mas a inicial só ataca um.

**Regra:** toda triagem tem que rodar HISCON/HISCRE completo **antes** da inicial para identificar contratos gêmeos. Se já protocolado, considerar aditamento da inicial ou ação autônoma para o gêmeo. Ver [[regras-de-adaptacao#Regra 1]].

### Erro 25 — Banco junta faturas do contrato-gêmeo como se fossem prova do contrato em lide

**Origem:** Caso 1 (Santander juntou faturas do cartão RCC ***5469, mas o contrato em discussão era o RMC, com número distinto).

**Regra:** conferir terminação do cartão nas faturas × HISCON do contrato em lide. Se divergente, na réplica apontar que o banco **sequer juntou prova do contrato em discussão** — juntou faturas de contrato alheio. Reforço direto da tese `sem-contrato`.

### Erro 26 — Alegar "sem videochamada" em contrato BMG sem conferir data de averbação

**Origem:** Caso 3. BMG confessou que videochamada só existe a partir de 09/2023. Antes disso, não havia.

**Regra:** para contratos BMG pré-09/2023, invocar a **confissão do próprio banco** (parágrafo da contestação). Para contratos pós-09/2023, NÃO é cabível alegar ausência de videochamada como regra — conferir se o fluxo foi efetivamente cumprido (selfie, liveness, ID de sessão).

### Erro 27 — Comprovante de residência de terceiro sem declaração de coabitação

**Origem:** Caso 2 e Caso 3. Interior do Amazonas: autor hipossuficiente usa comprovante de parente/vizinho.

**Regra:** o comprovante em nome de outra pessoa **precisa** vir acompanhado de declaração de coabitação assinada pelo titular da conta. Se a inicial foi protocolada sem, anexar na réplica como documento suplementar. Alternativa: rebater a preliminar com art. 73 CPC + hipossuficiência. Ver [[regras-de-adaptacao#Regra 5]].

### Erro 28 — TED em conta de outro banco não cruzada com conta INSS

**Origem:** Caso 2 e Caso 3. Banco junta TED mas a conta destino não é a conta do benefício.

**Regra:** cruzar sempre: conta INSS declarada pelo autor × conta destino do TED juntado pelo banco. Se divergente, parágrafo específico na réplica invocando IN 28/2008 art. 15 I (**norma citada pelo próprio banco**). Ver [[regras-de-adaptacao#Regra 4]].

### Erro 29 — Tom retórico em Maués (Juiz Anderson)

**Origem:** Caso 3. Trechos retóricos ("é possível imaginar o impacto?") e erros de digitação em caixa-alta ("DIGINIDADE" em vez de "DIGNIDADE") destoam do padrão técnico exigido na comarca.

**Regra:** densificar argumento técnico, revisar com atenção palavras em CAIXA-ALTA (as que mais escapam), evitar perguntas retóricas ao juízo. Ver [[regras-de-adaptacao#Regra 13]].

## Ver também

- [[_MOC]]
- [[estrutura-padrao]]
- [[manual-consolidado]]
- [[configuracoes-visuais]]
- [[../Apelacoes/erros-herdados]]
