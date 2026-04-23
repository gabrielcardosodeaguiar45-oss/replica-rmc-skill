---
tipo: referencia
tags: [replica, rmc, rcc, layout, visual]
atualizado-em: 2026-04-22
---

# Configurações visuais — RMC/RCC

Padrão visual **idêntico** ao das [[../Apelacoes/configuracoes-visuais|apelações]]. Este arquivo documenta as particularidades da réplica.

## Fonte

**Cambria** em todo o documento. Tamanho-base 12pt para corpo, 14pt para títulos, 10-11pt para citações e rodapé.

Se a fonte se perder por colagem de trechos, rodar:

```
python ~/.claude/skills/replica-rmc/scripts/forcar_cambria.py
```

Script varre estilos + runs + tabelas + cabeçalhos/rodapés e força Cambria em tudo.

## Margens e estilo de página

Seguir o mesmo padrão do timbrado do escritório. Não é necessário folha de rosto (confirmação do usuário em 2026-04-22).

## Sem imagens

Réplicas de RMC/RCC com tese de vício de consentimento **não** levam imagens dos autos. Sem prints de CCB, trilha, geolocalização, HISCON. Apenas texto e, eventualmente, tabela comparativa de requisitos (Tema 5/Ata Seção) e compras da fatura.

## Tabelas

Não há tabelas-padrão. As duas que surgem naturalmente:

1. **Requisitos × Provas nos autos** — tabela comparativa do IRDR Tema 5 TJAM ou da Ata da Seção Cível TJAL. 2 colunas (Requisitos impostos | Provas constantes nos autos). Linhas com "Não há" nas provas faltantes.
2. **Compras do cartão por competência** (raro) — se tiver que listar compras reais vs. automáticas.

## Subscritores

| Estado | Subscritor padrão | OAB |
|---|---|---|
| Amazonas | Eduardo Fernando Rebonatto (histórico) ou Patrick (atual) | AM A2118 (Eduardo) / a confirmar (Patrick) |
| Alagoas | (a confirmar — há subscritores específicos na pasta) | — |
| Bahia | (a confirmar) | — |
| Minas Gerais | (a confirmar) | — |
| Santa Catarina (histórico) | Patronos do escritório matriz Joaçaba | — |

## Ver também

- [[../Apelacoes/configuracoes-visuais|Configurações visuais — Apelações]]
- [[../../Escritorio/dados-escritorio|Dados do escritório]]
- [[erros-herdados#Erros de layout]]
