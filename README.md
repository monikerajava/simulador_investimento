# simulador-fii-excel

Planilha em Excel que simula investimentos em fundos imobiliários (FIIs): do aporte mensal ao patrimônio acumulado e aos dividendos, com projeção em cenários e divisão do aporte por perfil de investidor.

> Todos os valores (salário, aporte, taxas e percentuais) são **exemplos didáticos**, não recomendação de investimento.

## Perguntas que a ferramenta responde (aba `APP`)
| Pergunta | Onde |
|---|---|
| Quanto investir por mês? | `C12` (entrada) |
| Por quantos anos? | `C13` (entrada) |
| Qual a taxa de rendimento mensal? | `C14` (entrada) |
| Quanto de patrimônio vai acumular? | `C15` |
| Quanto vai receber de dividendos por mês? | `C16` |

Também: cenários de 2, 5, 10, 20 e 30 anos (linhas 21–25), simulação com 30% do salário (linhas 28–30) e divisão do aporte por perfil (linhas 33–43, com gráfico de pizza).

## Como VF e PROCV entram
- **VF (FV):** `=FV(taxa_mensal, qtd_anos*12, -aporte)` — taxa por período (mensal), nº de períodos (anos × 12) e pagamento (aporte, negativo para o resultado sair positivo). Os cenários usam `$B21*12` com referência absoluta/mista para arrastar sem erro.
- **Dividendos:** `=patrimonio*rendimento_carteira`.
- **PROCV (VLOOKUP) com chave composta:** na aba `Apoio`, a coluna A é `=PERFIL&"-"&TIPO` (ex.: `Moderado-TIJOLO`). Na `APP`: `=VLOOKUP(perfil&"-"&B37, tabela_perfis, 4, FALSE)` traz o percentual do perfil escolhido para cada tipo de FII.

## Intervalos nomeados
`salario` (C6) · `rendimento_carteira` (C7) · `perc_sugestao` (C8) · `sugestao_investimento` (C9) · `aporte` (C12) · `qtd_anos` (C13) · `taxa_mensal` (C14) · `patrimonio` (C15) · `dividendo_mensal` (C16) · `perfil` (C33) · `tabela_perfis` (Apoio!A4:D21)

## Percentuais por perfil (exemplo do autor; cada perfil soma 100%)
| Tipo | Conservador | Moderado | Agressivo |
|---|---|---|---|
| Papel | 35% | 30% | 40% |
| Tijolo | 45% | 35% | 10% |
| Híbridos | 10% | 10% | 10% |
| FOFs | 10% | 5% | 5% |
| Desenvolvimento | 0% | 10% | 25% |
| Hotelarias | 0% | 10% | 10% |

A aba `Apoio` confere a soma de cada perfil (coluna "STATUS").

