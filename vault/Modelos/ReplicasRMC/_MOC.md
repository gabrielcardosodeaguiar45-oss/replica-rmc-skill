---
tipo: MOC
tags: [modelos, moc, replica, rmc, rcc, bancario]
area: bancario
status: em-construcao
---

# MOC — Réplicas RMC/RCC

Mapa da biblioteca de réplicas à contestação em ações de Reserva de Margem Consignável (RMC) e Reserva de Cartão Consignado (RCC). Acervo operacional do escritório, cobrindo **Alagoas, Amazonas, Bahia e Minas Gerais**, com teses modulares reutilizáveis e modelos por estado/banco/cenário.

> [!info] Fase de construção
> Documentação ainda em progresso. Atualmente (2026-04-22) contém: manual consolidado + 25 teses modulares + estrutura-padrão. **Modelos por estado pendentes** — entrarão em rodadas seguintes de leitura. Fichas de aprendizado vazias até o primeiro caso paradigma.

> [!warning] Leitura obrigatória antes de montar réplica
> 1. [[manual-consolidado|Manual consolidado]] — catálogo do que revisar por tipo de peça.
> 2. [[estrutura-padrao|Estrutura padrão da réplica]] — anatomia dos 9 blocos.
> 3. [[erros-herdados|Erros herdados]] — armadilhas que saem dos modelos-base.
> 4. [[regras-de-adaptacao|Regras de adaptação]] — 0 regras consolidadas (preenchido a partir da Fase 3).
> 5. [[teses-modulares/_index|Biblioteca de teses]] — 11 preliminares nossas + 14 impugnações de preliminares do banco.

## Árvore de decisão (alta abstração)

```
Recebeu contestação em ação RMC/RCC?
├── Identificar ESTADO (AL / AM / BA / MG)
├── Identificar BANCO (BMG, PAN, Mercantil, Bradesco, Olé, Cetelem, Santander, Agibank, ...)
├── Identificar CENÁRIO
│   ├── Banco apresentou contrato FÍSICO regular?
│   ├── Banco apresentou contrato DIGITAL?
│   ├── Banco NÃO apresentou contrato? → usar tese "sem contrato"
│   ├── Banco apresentou contrato de TERCEIRO? → usar tese "contrato de terceiro"
│   ├── Contrato em CAIXA ELETRÔNICO (Mercantil)? → tese específica
│   └── Contrato pós dez/2018 SEM TCE? → tese TCE
├── Identificar PERFIL DO CLIENTE
│   ├── Analfabeto sem rogado (AL/PAN)?
│   ├── Idoso com aceites em poucos segundos?
│   └── Contratação digital rápida?
└── Selecionar MODELO BASE + TESES MODULARES
```

## Blocos da documentação

| Bloco | Descrição | Status |
|---|---|---|
| [[manual-consolidado\|Manual]] | Síntese do `RMC - Manual.docx` | ✅ pronto |
| [[estrutura-padrao\|Estrutura padrão]] | Anatomia da réplica em 9 blocos | ✅ pronto |
| [[configuracoes-visuais\|Configurações visuais]] | Timbrado, Cambria, margens | ✅ pronto (reaproveita apelações) |
| [[erros-herdados\|Erros herdados]] | Armadilhas frequentes | ✅ inicial |
| [[checklist-protocolo\|Checklist de protocolo]] | Conferência final interna | ✅ inicial |
| [[regras-de-adaptacao\|Regras de adaptação]] | Regras do caso paradigma | ⏳ pendente (Fase 3) |
| [[teses-modulares/_index\|Biblioteca de teses]] | 25 teses catalogadas | ✅ pronto |
| [[modelos-por-estado/_index\|Modelos por estado]] | AL, AM, BA, MG, histórico | ✅ 32 fichas |
| [[skill-replica-rmc-amazonas\|Skill replica-rmc-amazonas]] | Ferramenta do fluxo | ✅ catalogada |

## Estados cobertos (resumo estratégico)

Extraído do manual:

**Alagoas.** Maior taxa de procedência em primeiro grau. Padrão: majoração de danos morais + arbitramento de danos temporais em apelação. Cuidar com compensação (Ata da Seção Cível 10/09/2021, conclusões 5 e 6).

**Amazonas.** Quase nenhuma procedência em primeiro grau. Em Maués, só costumam considerar a ausência de contrato. IRDR Tema 5 TJAM (0005217-75.2019.8.04.0000) fixa 7 requisitos para validade do contrato — tese nuclear em todo caso AM. Prescrição decenal reconhecida (vs. regra geral quinquenal).

**Bahia.** Há decisões favoráveis em primeiro grau. Cuidar com prazo do PJE e com arbitramento de restituição simples (devia ser em dobro, pós 30/03/2021).

**Minas Gerais.** Pouquíssimas procedências por causa da decadência (aplicam 4 anos da assinatura). Apelação padrão: afastamento da decadência + julgamento do mérito em 2º grau por causa madura. Recurso especial sobre decadência já está pronto no acervo.

## Biblioteca modular — visão

11 teses nossas (preliminares que nós levantamos):

1. [[teses-modulares/nossas/agibank-contrato-irregular|Agibank — contrato irregular (profissão/dados)]]
2. [[teses-modulares/nossas/analfabeto-sem-rogado|Analfabeto sem assinatura a rogo]]
3. [[teses-modulares/nossas/contrato-de-terceiro-ma-fe|Contrato de terceiro — má-fé]]
4. [[teses-modulares/nossas/contrato-digital-contratacao-rapida|Contrato digital + contratação rápida]] (tese mãe, 147 parágrafos)
5. [[teses-modulares/nossas/contrato-caixa-eletronico|Contrato em caixa eletrônico]] (Mercantil)
6. [[teses-modulares/nossas/contrato-pan-sem-informacoes|Contrato PAN sem informações mínimas]]
7. [[teses-modulares/nossas/documentos-intempestivos-procuracao|Documentos intempestivos]]
8. [[teses-modulares/nossas/faturas-mesma-data|Faturas emitidas na mesma data]] (Santander)
9. [[teses-modulares/nossas/sem-contrato|Sem contrato / contrato errado]] (tese mãe para BMG reaverbação 2017)
10. [[teses-modulares/nossas/sem-faturas|Sem faturas]]
11. [[teses-modulares/nossas/sem-tce|Sem TCE — a partir de dez/2018]]

14 teses de impugnação (rebater preliminares que o banco levanta):

1. [[teses-modulares/impugnacao/abuso-direito-peticao|Abuso do direito de petição]]
2. [[teses-modulares/impugnacao/amazonas-distancia-adv-cliente|Amazonas — distância ADV × cliente]]
3. [[teses-modulares/impugnacao/amazonas-observancia-irdr|Amazonas — observância do IRDR Tema 5]]
4. [[teses-modulares/impugnacao/amazonas-suspensao-irdr-rr|Amazonas — suspensão por IRDR RR]]
5. [[teses-modulares/impugnacao/decorrencia-logica-valores|Decorrência lógica + valores incontroversos]]
6. [[teses-modulares/impugnacao/ausencia-extratos|Ausência de extratos bancários]]
7. [[teses-modulares/impugnacao/conexao|Conexão]]
8. [[teses-modulares/impugnacao/desnecessidade-aij|Desnecessidade de AIJ]]
9. [[teses-modulares/impugnacao/longo-transcurso-tempo|Longo transcurso do tempo]]
10. [[teses-modulares/impugnacao/pagamento-adicional-faturas|Pagamento adicional voluntário de faturas]]
11. [[teses-modulares/impugnacao/pedido-dilacao-banco|Pedido de dilação do banco]]
12. [[teses-modulares/impugnacao/procuracao-desatualizada|Procuração desatualizada]]
13. [[teses-modulares/impugnacao/procuracao-generica|Procuração genérica]]
14. [[teses-modulares/impugnacao/tutela-urgencia|Tutela de urgência]]

## Convenções

Placeholders em CAIXA-ALTA entre chaves duplas: `{{NOME_AUTOR}}`, `{{CNJ}}`, `{{BANCO_REU}}`, `{{DATA_PROTOCOLO}}`, `{{MOV_CONTRATO}}`, `{{MOV_FATURAS}}`, `{{MOV_CONTESTACAO}}`.

Subscritores: conforme responsável pelo processo (Eduardo — OAB/AM A2118, Patrick — OAB/AM nº a confirmar).

Fonte: Cambria (mesmo padrão visual das apelações).

## Ver também

- [[../Apelacoes/_MOC|MOC das Apelações bancárias]]
- [[../../Teses/rmc-irdr-tema5-tjam|Tese IRDR Tema 5 TJAM (7 requisitos)]]
- [[../../Procedimentos/_index|Procedimentos operacionais]]
- [[../../Home]]
