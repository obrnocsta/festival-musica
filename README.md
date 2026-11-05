# Projeto de Análise de Dados

Repositório dos desafios do bootcamp de **Análise de Dados da Generation Brasil**.

No Desafio 1, cada participante escolhe um dos oito temas abaixo e utiliza a mesma base nos desafios de Estatística, Excel, SQL/Data Viz e Big Data.

## Guias

| Desafio | Material |
|---|---|
| 1 · Python, API e IA | [Guia do Desafio 01](Guia_Desafio1_Google_Colab.md) |

## Temas disponíveis

| # | Tema | Tabelas | Registros |
|---:|---|---|---:|
| 1 | Estacionamento | `vagas` · `movimentacoes` | 52.200 |
| 2 | Posto de saúde | `pacientes` · `atendimentos` | 52.500 |
| 3 | Streaming de filmes | `filmes` · `visualizacoes` | 65.300 |
| 4 | Atendimento ao cliente | `clientes` · `chamados` | 52.400 |
| 5 | Passagens aéreas | `voos` · `reservas` | 65.600 |
| 6 | Serviço meteorológico | `estacoes` · `leituras` | 72.050 |
| 7 | Telemetria esportiva | `pilotos` · `voltas` | 65.800 |
| 8 | Festival de música | `atracoes` · `ingressos_vendidos` | 65.100 |

Os planos de modelagem estão disponíveis na pasta [`bases_dados`](bases_dados/).

## Estrutura das bases

Cada tema possui duas tabelas:

- **Dimensão ou cadastro:** contém as entidades principais e uma chave primária.
- **Fato ou evento:** registra ocorrências ao longo do tempo e referencia a tabela de dimensão por chave estrangeira.

Os nomes das colunas são fixos e devem ser mantidos em todos os desafios.

## Geração dos dados

As bases são geradas pelo script `gerar_bases.py`, utilizando:

- Python;
- `pandas`;
- `numpy`;
- `Faker` com localidade `pt_BR`.

A geração usa a semente `42`, garantindo resultados reproduzíveis, e produz arquivos CSV em UTF-8, organizados por tema.

Cada tema possui pelo menos 20.000 linhas somadas, conforme a exigência do projeto.

## Ética e privacidade

Todos os dados são fictícios. Nomes, identificadores e demais informações são gerados artificialmente e não representam pessoas ou situações reais.

No tema de saúde, essa regra é especialmente importante por envolver informações sensíveis.

O uso de inteligência artificial deve seguir os princípios de uso responsável definidos no projeto.
