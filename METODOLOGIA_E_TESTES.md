# Metodologia, testes e limitações

## 1. Fontes e tratamento

Foram comparados os dois arquivos disponibilizados no desafio DIO: a base de assinaturas (`base.xlsx`) e o dashboard didático finalizado (`dashboard_xbox_finalizado.xlsx`). A solução usa a base de 295 linhas de registros do ano de 2024.

**Tratamento:** mantidos ID, plano, início, renovação, valor do plano, periodicidade, adicionais, cupom e total. O campo de **nome** foi excluído da versão pública por não ser necessário para os indicadores. Campos `Yes`/`No` foram traduzidos para `Sim`/`Não`; os preços ausentes dos adicionais foram convertidos para zero, quando indicados por `-`. Periodicidades foram traduzidas para Português. A coluna `MÊS DE INÍCIO` é derivada da data e `CONFERÊNCIA` é derivada dos valores.

## 2. Reconciliação e evidências

| Verificação | Resultado |
|---|---:|
| Registros lidos | 295 |
| IDs distintos | 295 |
| Plano Core | 101 |
| Plano Standard | 96 |
| Plano Ultimate | 98 |
| Periodicidade Mensal | 139 |
| Periodicidade Trimestral | 85 |
| Periodicidade Anual | 71 |
| Renovação Sim | 148 |
| Renovação Não | 147 |
| Preço dos planos (soma) | 2.935,00 u.m. |
| EA Play (soma) | 2.940,00 u.m. |
| Minecraft (soma) | 3.880,00 u.m. |
| Cupons (soma) | 2.122,00 u.m. |
| Valor total calculado | **7.633,00 u.m.** |
| Divergências entre componentes e total | **0** |

**Reconciliação:** 2.935 + 2.940 + 3.880 − 2.122 = **7.633**.

**Filtro combinado validado:** Plano `Ultimate` + periodicidade `Mensal` retorna **45 assinaturas** e **2.421,00 u.m.**, equivalentes às somas recalculadas diretamente sobre a base fornecida. Teste final de células com erro de referência, divisão por zero, nome ou valor: **nenhum erro identificado** nas verificações realizadas.

## 3. Implementação

- Fórmulas na guia `PAINEL`: `SUMIFS`, `COUNTIFS`, `IFERROR` com critérios derivados dos filtros `C7` e `K7`.
- Agrupamento mensal pela data de início na coluna M de `DADOS`.
- Coluna N de `DADOS`: `=IF(ABS(E2+H2+J2-K2-L2)<0.001,"OK","REVER")` preenchida até a linha 296.
- Gráficos ligados a células calculadas na guia `ANALISE`.
- Validações de dados para os filtros e tabela estruturada na guia `DADOS`.

## 4. Limitações

- A fonte não especifica moeda; os valores são apresentados como `u.m.`.
- Os registros estão associados ao **início de assinaturas** em 2024; o projeto não demonstra recebimentos financeiros mensais efetivos.
- A periodicidade informada é categórica; os preços não são multiplicados por número de meses ou anos.
- As análises têm intervalos configurados para os **295 registros originais** (linhas 2:296). Para acrescentar registros, será necessário estender os intervalos das fórmulas e tabelas auxiliares.
- Macros e dependências externas não são utilizadas; filtros por seleção de células com lista suspensa, em vez de segmentações de tabelas dinâmicas.
- A exibição gráfica pode variar entre versões do Excel e outros softwares de planilha.

## 5. Privacidade e publicação

A versão disponibilizada no repositório não inclui a coluna de nomes presente no material de aula. Os dados devem ser tratados como **base didática fornecida no curso**, e não como demonstrativo de uma empresa.
