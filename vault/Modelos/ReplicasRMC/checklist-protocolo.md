---
tipo: checklist
tags: [replica, rmc, rcc, protocolo]
uso: interno-claude
atualizado-em: 2026-04-22
---

# Checklist de protocolo — uso interno

Conferência final antes de entregar o `.docx` da réplica. **Uso interno** — rodar mentalmente antes de cada entrega.

## Bloco 1 — identificação

1. [ ] Cabeçalho: vara + comarca + UF corretos.
2. [ ] CNJ correto (confere com inicial e contestação).
3. [ ] Nome completo do autor bate com RG e procuração.
4. [ ] Gênero (qualificado/qualificada) consistente em toda a peça.
5. [ ] Razão social do banco réu correta (confere com contestação + CNPJ).
6. [ ] **Cidade do fecho** = comarca real do processo (item separado; Fase 3 confirmou que o modelo herda "Manaus/AM" mesmo em Caapiranga, Boa Vista do Ramos ou Maués).
7. [ ] **Dados cadastrais do autor conferidos em todos os documentos do banco** (sexo, data de nascimento, endereço, renda): se houver divergência, inserir parágrafo autônomo na réplica (Regra 15 de regras-de-adaptacao).

## Bloco 2 — tempestividade

1. [ ] Data do fim do prazo calculada com base na intimação real (15 dias úteis a partir da ciência da contestação).
2. [ ] Data por extenso correta.

## Bloco 3 — conteúdo

1. [ ] Cada preliminar do banco foi rebatida (nenhuma esquecida).
2. [ ] Ordem das impugnações segue a ordem da contestação (não a ordem do CPC).
3. [ ] Preliminares nossas incluídas (se aplicáveis ao caso).
4. [ ] Teses de mérito coerentes com o cenário (contrato físico vs digital vs sem contrato etc.).
5. [ ] Jurisprudência invocada é da jurisdição correta (IRDR Tema 5 para AM, Ata Seção para AL, IRDR MG para MG, etc.).
6. [ ] Marco 30/03/2021 respeitado na restituição em dobro.
7. [ ] Pedidos adaptados ao caso (não genéricos).
8. [ ] **RCC gêmeo conferido no HISCON:** se existir contrato gêmeo do mesmo banco, mencionar em parágrafo contextual ou aditar inicial (Regra 1 de regras-de-adaptacao).
9. [ ] **Conta destino do TED × conta INSS do autor:** se divergente, parágrafo específico invocando IN 28/2008 art. 15 (Regra 4).
10. [ ] **Faturas em 2ª via massiva:** se carimbo de postagem concentra em data próxima do protocolo da contestação, inserir parágrafo invocando IRDR Tema 5 requisito "b" + art. 52 V CDC (Regra 2).
11. [ ] **Contrato BMG pré-09/2023:** usar confissão do próprio banco sobre cronologia da videochamada (Regra 7).
12. [ ] **Correspondente bancário:** se cidade do correspondente é geograficamente incompatível com residência do autor (estados distintos), inserir parágrafo (Regra 14).
13. [ ] **IP/geolocalização:** se laudo menciona IP "privado", conferir faixa do RFC 1918 antes de alegar privado; se o IP for público, descrever como IPv4/IPv6 dinâmico (Regra 16).
14. [ ] **Número do cartão das faturas × contrato em lide** (Santander especialmente): conferir se o banco juntou faturas do cartão correto ou do gêmeo (Regra 10).
15. [ ] **Saque simultâneo à averbação:** se houver, inserir parágrafo sobre venda casada automática (Regra 11).

## Bloco 4 — erros comuns

1. [ ] Banco-mãe do modelo não aparece residualmente.
2. [ ] Placeholders `{{...}}` todos substituídos.
3. [ ] Sem "anulação" onde deveria ser "declaração de inexistência".
4. [ ] Sem sub-seção de contrato digital em caso físico (e vice-versa).
5. [ ] Sem menção a hash/selfie/geolocalização se contrato é físico.
6. [ ] Sem tutela de urgência mencionada como pedida (se não foi).

## Bloco 5 — layout

1. [ ] Fonte Cambria em todo o documento (rodar script de força se necessário).
2. [ ] Sem imagens residuais.
3. [ ] Listas com a), b), c), d) ou i, ii, iii, iv (sem traços).
4. [ ] Timbrado e margens padrão do escritório.
5. [ ] Assinatura do subscritor + OAB correta.
6. [ ] **Se comarca for Maués:** revisar tom — densificar técnica, eliminar apelos retóricos, revisar digitação em CAIXA-ALTA (Regra 13 — alerta Juiz Anderson).

## Bloco 6 — fechamento

1. [ ] Pedido final claro.
2. [ ] "Nestes termos, pede deferimento." no fim.
3. [ ] Cidade, UF, data por extenso.
4. [ ] Nome + OAB do subscritor.

## Bloco 7 — arquivo

1. [ ] Nome do arquivo: `Réplica - {{CNJ-resumido}} - {{NOME_AUTOR}}.docx`.
2. [ ] Versão final salva (não rascunho).
3. [ ] Backup em `_backups/` do histórico.

## Se algum item falhar

1. Voltar, corrigir, salvar nova versão.
2. Re-rodar checklist.
3. Só entregar quando todos os itens estiverem ✅.

## Ver também

- [[_MOC]]
- [[estrutura-padrao]]
- [[erros-herdados]]
- [[configuracoes-visuais]]
