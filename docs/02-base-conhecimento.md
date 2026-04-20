# Base de Conhecimento

## Dados Utilizados

O agente utiliza um conjunto simples de dados financeiros para análise de gastos:

| Arquivo          | Formato | Utilização no Agente                                             |
| ---------------- | ------- | ---------------------------------------------------------------- |
| `transacoes.csv` | CSV     | Armazenar e analisar histórico de receitas e despesas do usuário |


> [!TIP]
> **Quer um dataset mais robusto?** Você pode utilizar datasets públicos do [Hugging Face](https://huggingface.co/datasets) relacionados a finanças, desde que sejam adequados ao contexto do desafio.

---

## Adaptações nos Dados

> Você modificou ou expandiu os dados mockados? Descreva aqui.
> 
Os dados foram estruturados e padronizados para facilitar o processamento automático pelo agente:

- Padronização de datas no formato YYYY-MM-DD
- Classificação de transações em categorias fixas:
    alimentação
    transporte
    moradia
    saúde
    lazer
    receita
- Separação clara entre entrada (receitas) e saida (despesas)
- Valores numéricos normalizados (formato decimal)

Essas adaptações permitem:

- Cálculo de totais por categoria
- Identificação de padrões de consumo
- Geração de insights simples

---

## Estratégia de Integração

### Como os dados são carregados?
> Descreva como seu agente acessa a base de conhecimento.
> 
O arquivo transacoes.csv é carregado no início da execução do agente e armazenado em memória (ex: estrutura de lista ou dataframe).
> 
### Como os dados são usados no prompt?
> Os dados vão no system prompt? São consultados dinamicamente?
> 
Os dados não são totalmente enviados ao modelo para evitar sobrecarga.

Em vez disso:
- O sistema processa os dados previamente
- Gera resumos (totais, categorias, alertas)
- Apenas essas informações resumidas são incluídas no prompt do modelo

---

## Exemplo de Contexto Montado

> Mostre um exemplo de como os dados são formatados para o agente.

```
Resumo Financeiro do Usuário:

Total de entradas: R$ 5.000
Total de despesas: R$ 2.488,90

Gastos por categoria:
- Moradia: R$ 1.380
- Alimentação: R$ 570
- Transporte: R$ 295
- Saúde: R$ 188
- Lazer: R$ 55,90

Principais insights:
- Maior gasto: Moradia
- Alimentação está acima da média esperada
- Possível oportunidade de economia em lazer e delivery

Últimas transações:
- 25/10: Combustível - R$ 250
- 20/10: Academia - R$ 99
- 15/10: Conta de Luz - R$ 180
```
