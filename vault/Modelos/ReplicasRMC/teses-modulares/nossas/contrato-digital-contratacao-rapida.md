---
tipo: tese-modular
categoria: nossa
tags: [replica, rmc, rcc, preliminar-nossa, contrato-digital, hash, selfie, geolocalizacao]
arquivo-fonte: "00. Teses gerais de réplica/Preliminares nossas/Contrato digital + Contratação digital rápida.docx"
banco-associado: BMG, Itaú, C6, diversos
estado-origem: BA
processo-paradigma: 5065817-37.2022.8.24.0930
modo: tese + réplica-completa
---

# Contrato digital + contratação digital rápida

**Tese-mãe** do acervo — 147 parágrafos cobrindo todos os ângulos técnicos do contrato digital fraudulento. Também funciona como **modelo de réplica completa** quando a réplica é estruturada em torno desse eixo.

## Quando usar

Contratação digital (por app, site ou whatsapp) em que o banco apresenta **trilha de auditoria / CCB digital** como prova. Características gravantes:

1. Cliente **idoso**, vulnerável, baixa escolaridade.
2. Aceites realizados em **poucos segundos** (fluxo automatizado, não humano).
3. Ausência de selfie liveness em padrão iBeta 2.
4. Assinatura eletrônica fora do ICP-Brasil.
5. Código hash ausente ou incompatível com o documento juntado.
6. Geolocalização incompatível com residência da parte (ex.: IP Manaus × residência Maués).
7. Correspondente bancário em estado diverso (ex.: Santana de Parnaíba/SP × Maués/AM).
8. Metadata do PDF indica criação posterior à data da "contratação".

## O que levanta

Nulidade do contrato por ausência de consentimento válido e vícios técnicos na formalização digital. Subsidiariamente, pedido de perícia digital.

## Sub-teses (blocos usados juntos ou separados)

1. **Parâmetros de validade do contrato RMC** — IRDR Tema 5 TJAM + IN INSS 28, art. 21 (8 requisitos mínimos).
2. **Contratação em segundos** — arts. 104 I e II CC (requisitos do ato jurídico); hipervulnerabilidade do idoso (CDC 4º I; Estatuto do Idoso art. 3º).
3. **Assinatura eletrônica inválida** — Lei 14.063/2020, art. 4º (simples × avançada × qualificada). ICP-Brasil.
4. **Selfie liveness** — Nota Técnica INSS; IEEE Std 2790/2020; ISO/IEC 30107-3; ISO/IEC 29.794-5; iBeta 2; validação em bases governamentais (TSE, DENATRAN).
5. **Validador ITI** — documento com assinatura válida passa no validador oficial do Instituto Nacional de Tecnologia da Informação (governo.br). O contrato do banco não passa.
6. **Hash ausente** — REsp 2.159.442/PR, Rel. Nancy Andrighi, 3ª Turma, j. 24/09/2024 — fundamento conceitual. Sem hash, não há integridade; documento pode ter sido alterado.
7. **Hash incompatível** — variante: banco apresenta código hash no corpo do documento, mas a análise (PowerShell `Get-FileHash`) mostra hash diferente. Prova de adulteração.
8. **Propriedades do documento** — metadados PDFium: contrato criado 2 anos depois da alegada data da contratação (ex.: contrato "assinado" 30/08/2023, criado 06/08/2025 12:49:23).
9. **IP / geolocalização** — IP aponta para cidade diversa da residência. Distância em km (ex.: Maués×Manaus 259 km).
10. **Correspondente em estado diverso** — empresa terceirizada em SP×cliente AM = inverossímil.
11. **Ausência de dados necessários** — contrato digital sem assinatura eletrônica qualificada nem geolocalização = nulo (CC art. 422 + jurisprudência TJAL).
12. **Imprescindibilidade de perícia digital** — pedido final.

## Base legal e jurisprudencial

Legal: art. 350 CPC (prazo); arts. 104, 166 IV, 422 CC; CDC arts. 4º I, 6º III, 14, 39 IV, 42 par.; Estatuto do Idoso art. 3º; Lei 14.063/2020 art. 4º; IN INSS 28 arts. 15, 21; normas técnicas IEEE 2790/2020, ISO/IEC 30107-3, ISO/IEC 29.794-5, iBeta 2.

Jurisprudência:
1. **STJ REsp 2.159.442/PR** (Nancy Andrighi, 3ª T, 24/09/2024) — função hash, efeito avalanche, cadeia de custódia.
2. **STJ AgRg no RHC 143.169/RJ** (5ª T, DJe 02/03/2023) — hash em cadeia de custódia de prova digital penal.
3. **TJAL Apelação 0745371-43.2022.8.02.0001** (Márcio Roberto Tenório, 4ª CC, 15/05/2024) — nulidade por ausência de selfie, protocolo, geolocalização, ID usuário.
4. **TJAL Apelação 0740736-48.2024.8.02.0001** (Márcio Tenório, 4ª CC, 05/02/2025) — contrato eletrônico exige geolocalização, ID sessão, IP/terminal.

## Pega jurídica

1. **LER O LAUDO DO BANCO ANTES DE APLICAR.** Se a geolocalização bate com a residência, a sub-tese 9 cai e pode ser contraproducente insistir. Remover essa parte e focar em precisão insuficiente.
2. **Verificar hash com PowerShell** (`Get-FileHash -Algorithm SHA256`) antes de alegar incompatibilidade. Mostrar o hash calculado e o hash declarado.
3. **Validador ITI** — é no site `validar.iti.gov.br` ou similar. Tirar prints. Imagem 1 do contrato válido, Imagem 2 do inválido.
4. **Pedir perícia digital apenas em MG e AL** (AM quase nunca defere).
5. **Idoso**: idade cliente > 60 anos reforça muito. Se cliente tem 40 anos, suavizar o tom de hipervulnerabilidade.
6. **Não confundir** "ausência de hash" (sub-tese 6) com "hash incompatível" (sub-tese 7). São duas variantes a escolher, nunca as duas juntas.

## Arquivos-irmãos / dupla função

Este arquivo é **tese + modelo de réplica completa**. Quando usado como modelo completo, segue integralmente os 9 blocos de [[../../estrutura-padrao]].

## Ver também

- [[sem-tce]]
- [[contrato-de-terceiro-ma-fe]]
- [[../../manual-consolidado#Questões de mérito]]
- [[../../../../Teses/apelacao-improcedencia-contrato-digital]]
