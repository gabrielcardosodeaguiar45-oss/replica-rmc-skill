---
tipo: MOC
tags: [aprendizado, moc, replica, rmc, rcc]
---

# MOC — Aprendizado (Réplicas RMC/RCC)

Registro cumulativo do aprendizado ao gerar réplicas de RMC/RCC. Cada caso novo vira uma ficha datada. A cada 3-5 casos, consolido os padrões recorrentes em [[../../Modelos/ReplicasRMC/regras-de-adaptacao]].

## Princípios

1. **Cada caso gera uma ficha** — nomeada `YYYY-MM-DD-cliente-processo.md`.
2. **Três blocos por ficha**: decisões não óbvias + correções do advogado sênior + padrões novos.
3. **Não edito aprendizado antigo** — só acrescento. Correções apagadas desaparecem do histórico, o que é ruim.
4. **Consolido periodicamente** no `regras-de-adaptacao.md` sem apagar as fichas — a regra aponta para a ficha de origem.

## Usar template

- [[_template|Template de ficha de aprendizado]] — copiar antes de iniciar cada caso.

## Fichas

```dataview
TABLE cliente, processo, cenario, resultado, file.mtime AS "Atualizado"
FROM "Aprendizado/ReplicasRMC"
WHERE tipo = "aprendizado-replica-rmc"
SORT file.ctime DESC
```

## Regras canônicas consolidadas

- [[../../Modelos/ReplicasRMC/regras-de-adaptacao|Regras de adaptação (em construção)]].

## Ver também

- [[../../Modelos/ReplicasRMC/_MOC]]
- [[../../Modelos/ReplicasRMC/erros-herdados]]
- [[../Apelacoes/_MOC|MOC Aprendizado — Apelações (referência de estrutura)]]
- [[../../Home]]
