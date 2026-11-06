## Guias e Conteúdos dos desafios

Os materiais de cada atividade serão reunidos nesta tabela para facilitar a navegação pelo repositório.

| Desafio | Material | Conteúdo |
|---------|----------|----------|
| 1 · Python, API e IA | [Guia do Desafio 01](https://github.com/rafaelq80/desafios_tecnicos_ad/blob/01_Bases/Guia_Desafio1_Google_Colab.md) | Preparação e conteúdo da sessão |

---

## Sobre este material

No Desafio 1 (Python), cada participante escolhe um dos 8 temas abaixo e segue com ele durante o bootcamp inteiro. O mesmo tema alimentará os Desafios 2 (Estatística), 3 (Excel), 4 (SQL/Data Vis) e 5 (Big Data).

Cada arquivo desta pasta é o **plano de modelagem** da base mockada daquele tema: nomes de coluna definidos, tipos de tabela, cardinalidade, volumetria e regras de geração. Os nomes de coluna são fixos de propósito: Python, Excel e SQL precisam bater exatamente com esse esquema, sem erro de digitação entre desafios.

Os planos foram **validados contra o script `gerar_bases.py`**, que gera os arquivos CSV de cada tema. Onde o plano original e o script divergiam, uma das duas pontas foi ajustada: o script foi corrigido quando gerava dados incoerentes (datas impossíveis, corridas sem sequência, geografia incompatível, entre outros) e o plano foi ajustado quando a diferença era só de volumetria ou de descrição. As divergências relevantes estão sinalizadas no arquivo de cada tema.

---

## Os temas

| # | Tema | Plano | Tabelas (dimensão · fato) | Linhas |
|:-:|:--|:--|:--|--:|
| 1 | Estacionamento | [01-estacionamento.md](https://github.com/rafaelq80/desafios_tecnicos_ad/blob/01_Bases/bases_dados/01-estacionamento/01-estacionamento.md) | `vagas` · `movimentacoes` | 52.200 |
| 2 | Posto de saúde (triagem) | [02-posto-de-saude.md]([bases_dados/02-posto-de-saude/02-posto-de-saude.md](https://github.com/rafaelq80/desafios_tecnicos_ad/blob/01_Bases/bases_dados/02-posto-de-saude/02-posto-de-saude.md)) | `pacientes` · `atendimentos` | 52.500 |
| 3 | Streaming de filmes | [03-streaming-de-filmes.md]([bases_dados/03-streaming-de-filmes/03-streaming-de-filmes.md](https://github.com/rafaelq80/desafios_tecnicos_ad/blob/01_Bases/bases_dados/03-streaming-de-filmes/03-streaming-de-filmes.md)) | `filmes` · `visualizacoes` | 65.300 |
| 4 | Atendimento ao cliente | [04-atendimento-ao-cliente.md](https://github.com/rafaelq80/desafios_tecnicos_ad/blob/01_Bases/bases_dados/04-atendimento-ao-cliente/04-atendimento-ao-cliente.md) | `clientes` · `chamados` | 52.400 |
| 5 | Passagens aéreas | [05-passagens-aereas.md](https://github.com/rafaelq80/desafios_tecnicos_ad/blob/01_Bases/bases_dados/05-passagens-aereas/05-passagens-aereas.md) | `voos` · `reservas` | 65.600 |
| 6 | Serviço meteorológico | [06-servico-meteorologico.md](https://github.com/rafaelq80/desafios_tecnicos_ad/blob/01_Bases/bases_dados/06-servico-meteorologico/06-servico-meteorologico.md) | `estacoes` · `leituras` | 72.050 |
| 7 | Telemetria esportiva | [07-telemetria-esportiva.md](https://github.com/rafaelq80/desafios_tecnicos_ad/blob/01_Bases/bases_dados/07-telemetria-esportiva/07-telemetria-esportiva.md) | `pilotos` · `voltas` | 65.800 |
| 8 | Festival de música | [08-festival-de-musica.md](https://github.com/rafaelq80/desafios_tecnicos_ad/blob/01_Bases/bases_dados/08-festival-de-musica/08-festival-de-musica.md) | `atracoes` · `ingressos_vendidos` | 65.100 |

---

## Convenção comum a todos os temas

**Estrutura das tabelas**

- **Mínimo de 2 tabelas de tipos diferentes**: uma tabela de **dimensão/cadastro** (a entidade central, com chave primária única) e uma tabela de **fato/evento** (os registros ao longo do tempo, em maior volume, que referencia a dimensão por chave estrangeira).
- Essa separação é proposital: prepara o terreno para o Desafio 4, em que o aluno **adiciona novas tabelas de dimensão** para transformar o modelo de 2 tabelas em um esquema estrela com mais joins.
- Colunas de tipo e categoria ficam como **texto puro**, de propósito. A normalização delas em catálogos é tarefa do Desafio 4.

**Volumetria**

- Regra do projeto: **mínimo de 20.000 linhas somadas** por tema.
- O script gera **pelo menos 10.000 linhas por tabela** (dimensão e fato), então todos os temas ficam bem acima do mínimo, com entre 52 mil e 72 mil linhas.
- A tabela de fato carrega a maior parte do volume. A dimensão também passa de 10 mil linhas, o que faz com que cada entidade apareça em média de 4 a 6 vezes na tabela de fato.

**Geração**

- Script: `gerar_bases.py`, com Python, `pandas`, `numpy` e `Faker` (localidade `pt_BR`).
- Semente fixa (`SEED = 42`), portanto a geração é reproduzível. Saída em CSV (UTF-8), uma pasta por tema.
- O uso de IA para gerar ou ajustar dados deve seguir a regra de "IA de forma responsável" do Desafio 4, sem inventar estatística que pareça dado real de mercado.

**Ética e privacidade**

- **Nenhum dado pessoal real.** Todo nome de pessoa ou identificador é gerado (Faker ou sorteio), nunca de pessoa real.
- No tema 2 (saúde), a regra é reforçada por tratar de dado sensível por natureza, mesmo fictício.
