<h1 align="center">Desafio 01 - Python, APIs e IA</h1>

<p align="center">
  Projeto de geração de bases de dados fictícias com Python, Google Colab e Google Sheets API.
</p>

---

## Sobre o projeto

O Desafio 01 faz parte de uma trilha de formação em análise de dados. Cada participante escolhe um dos oito temas disponíveis e constrói uma base de dados fictícia que será reutilizada nos desafios seguintes: Estatística, Excel, SQL/Visualização de Dados e Big Data.

O projeto apresenta o uso de APIs, autenticação por *service account*, geração de dados com Python e integração com o Google Sheets. O esquema de cada tema - nomes e ordem das colunas, tabelas e relacionamentos - deve ser seguido sem alterações, garantindo compatibilidade entre as etapas do bootcamp.

## Objetivos de aprendizagem

- Compreender o que é uma API e como Python se comunica com o Google Sheets.
- Configurar uma credencial de serviço e autenticar uma aplicação.
- Gerar dados fictícios com Faker, Python, pandas e NumPy.
- Aplicar um esquema de dados definido previamente.
- Enviar dados para o Google Sheets em lotes.
- Validar cabeçalhos, relacionamentos e quantidade de registros.
- Utilizar IA como apoio, identificando e verificando o conteúdo gerado.

## Temas disponíveis

Escolha um tema e mantenha-o durante toda a trilha. Cada tema possui uma tabela de dimensão/cadastro e uma tabela de fato/evento.

| # | Tema | Tabela dimensão | Tabela fato | Volume de referência |
|---:|---|---|---|---:|
| 1 | Estacionamento | `vagas` | `movimentacoes` | 52.200 |
| 2 | Posto de saúde (triagem) | `pacientes` | `atendimentos` | 52.500 |
| 3 | Streaming de filmes | `filmes` | `visualizacoes` | 65.300 |
| 4 | Atendimento ao cliente | `clientes` | `chamados` | 52.400 |
| 5 | Passagens aéreas | `voos` | `reservas` | 65.600 |
| 6 | Serviço meteorológico | `estacoes` | `leituras` | 72.050 |
| 7 | Telemetria esportiva | `pilotos` | `voltas` | 65.800 |
| 8 | Festival de música | `atracoes` | `ingressos_vendidos` | 65.100 |

Os volumes da tabela são referências das bases geradas pelo projeto. A exigência mínima da atividade é de **20.000 linhas somadas entre todas as tabelas** do tema.

Os planos de modelagem e os arquivos de cada tema estão no repositório de referência: [desafios_tecnicos_ad](https://github.com/rafaelq80/desafios_tecnicos_ad).

## Estrutura e regras dos dados

- Cada tema possui, no mínimo, uma tabela de dimensão (cadastro) e uma tabela de fato (eventos).
- A tabela de dimensão identifica as entidades por uma chave primária; a tabela de fato referencia essas entidades por chave estrangeira.
- Gere ou carregue primeiro as tabelas de referência e depois as tabelas dependentes. Toda chave estrangeira deve apontar para um ID existente.
- Cada tabela deve ocupar uma aba própria no Google Sheets, com o mesmo nome definido no plano do tema.
- Os nomes e a ordem das colunas devem ser exatamente os da ficha do tema.
- Colunas de tipo e categoria permanecem como texto, conforme a convenção do projeto.
- Todo dado deve ser fictício. Não utilize dados pessoais reais nem informações que possam ser associadas a pessoas conhecidas.

## Tecnologias e serviços

| Tecnologia | Finalidade |
|---|---|
| Python | Linguagem utilizada para gerar e tratar os dados |
| Google Colab | Ambiente de execução do notebook |
| Google Sheets | Destino das tabelas geradas |
| Google Sheets API | Interface de acesso programático às planilhas |
| Google Drive API | Acesso e gerenciamento de arquivos no Drive |
| `gspread` | Comunicação entre Python e Google Sheets |
| `Faker` | Geração de dados fictícios |
| `pandas` | Organização e manipulação das tabelas |
| `numpy` | Geração eficiente de valores e amostras |

## Fluxo de execução

A atividade está organizada em três momentos. A sessão tem duração total prevista de 60 minutos; a construção da base completa é realizada de forma autônoma, em aproximadamente 150 a 180 minutos.

### 1. Preparação - antes da sessão

1. Acesse o [Google Cloud Console](https://console.cloud.google.com/) e crie um projeto.
2. Em **APIs e serviços → Biblioteca**, ative:
   - Google Sheets API;
   - Google Drive API.
3. Em **IAM e administrador → Contas de serviço**, crie uma service account, por exemplo `desafio1-python`.
4. Abra a conta de serviço, acesse **Chaves → Adicionar chave → Criar nova chave**, selecione JSON e faça o download.
5. Abra o JSON e copie o valor de `client_email`. Esse endereço será usado para compartilhar a planilha.

> **Segurança:** o arquivo JSON contém uma chave privada e deve ser tratado como uma senha. Não o publique, não o envie por chat e não o adicione ao repositório. Se houver suspeita de exposição, revogue a chave no Google Cloud Console.

### 2. Prática - durante a sessão

**Passo 1 - Criar e compartilhar a planilha**

1. Acesse [sheets.new](https://sheets.new) e crie uma planilha com o nome correspondente ao tema:
   - `Desafio_01_Estacionamento`
   - `Desafio_01_Posto_Saude`
   - `Desafio_01_Streaming_Filmes`
   - `Desafio_01_Atendimento_Cliente`
   - `Desafio_01_Passagens_Aereas`
   - `Desafio_01_Meteorologia`
   - `Desafio_01_Telemetria_Esportiva`
   - `Desafio_01_Festival_Musica`
2. Compartilhe a planilha com o `client_email` da service account, concedendo a função **Editor**.
3. Copie o ID da planilha: é o trecho da URL entre `/d/` e `/edit`.

**Passo 2 - Criar o notebook e configurar o acesso**

Acesse [Google Colab](https://colab.research.google.com), crie um notebook chamado `Desafio1_API_Python` e salve o conteúdo integral do JSON nos Secrets do Colab com o nome `GCP_SA_JSON`.

Execute as células a seguir, em ordem.

**Célula 1 - Instalação**

```python
!pip install -q gspread faker
```

**Célula 2 - Importação e autenticação**

```python
import json
import random
import gspread
from google.colab import userdata
from faker import Faker

info = json.loads(userdata.get("GCP_SA_JSON"))
gc = gspread.service_account_from_dict(info)

print("Conectado como:", info["client_email"])
```

Na primeira execução, autorize o notebook a acessar o Secret `GCP_SA_JSON`. Execute novamente a célula e confirme a exibição do e-mail da service account.

**Célula 3 - Abrir a planilha**

Substitua o ID e o nome da aba pelos valores do seu tema.

| Tema | Nome da aba de dimensão | Nome da aba de fato |
|---|---|---|
| Estacionamento | `vagas` | `movimentacoes` |
| Posto de saúde | `pacientes` | `atendimentos` |
| Streaming de filmes | `filmes` | `visualizacoes` |
| Atendimento ao cliente | `clientes` | `chamados` |
| Passagens aéreas | `voos` | `reservas` |
| Serviço meteorológico | `estacoes` | `leituras` |
| Telemetria esportiva | `pilotos` | `voltas` |
| Festival de música | `atracoes` | `ingressos_vendidos` |

```python
SHEET_ID = "COLE_AQUI_O_ID_DA_PLANILHA"
NOME_TABELA = "nome_da_tabela"

sh = gc.open_by_key(SHEET_ID)
ws = sh.sheet1
ws.update_title(NOME_TABELA)

print(sh.title, "|", ws.title, "|", sh.url)
```

**Célula 4 - Definir o esquema da dimensão**

Substitua os exemplos pelos nomes exatos e na ordem indicada na ficha do tema.

```python
COLUNAS = ["coluna_1", "coluna_2", "coluna_3"]

ws.update(range_name="A1", values=[COLUNAS])
print("Cabeçalho confere:", ws.row_values(1) == COLUNAS)
```

**Célula 5 - Gerar e enviar 10 linhas de teste**

Adapte os campos e os tipos de dados à tabela escolhida.

```python
fake = Faker("pt_BR")
Faker.seed(42)
random.seed(42)

def gerar_linha(i):
    return {
        "coluna_1": i,
        "coluna_2": random.choice(["A", "B", "C"]),
        "coluna_3": fake.date_this_year().isoformat(),
    }

linhas = [gerar_linha(i) for i in range(1, 11)]
valores = [[linha[c] for c in COLUNAS] for linha in linhas]

ws.append_rows(valores, value_input_option="RAW")
print(len(valores), "linhas enviadas")
```

**Célula 6 - Ler e conferir os dados**

```python
valores_lidos = ws.get_all_values()

print("Linhas (cabeçalho + dados):", len(valores_lidos))
print("Cabeçalho confere:", valores_lidos[0] == COLUNAS)
print(valores_lidos[:3])
```

Ao final da sessão, abra a planilha no navegador e confirme que o cabeçalho está na primeira linha e que existem 10 registros abaixo dele. A meta da sessão é ter a conexão funcionando e os dados de teste gravados; a base completa será feita depois.

### 3. Construção da base completa - depois da sessão

Até a data combinada com o instrutor, gere ou carregue todas as tabelas do tema, atingindo pelo menos 20.000 linhas somadas.

**Célula 7 - Funções de conversão e envio**

```python
import time
import pandas as pd
import gspread

def df_para_valores(df):
    df = df.copy()

    for coluna in df.columns:
        if pd.api.types.is_datetime64_any_dtype(df[coluna]):
            df[coluna] = df[coluna].dt.strftime("%Y-%m-%d %H:%M:%S")
        elif df[coluna].dtype == object:
            df[coluna] = df[coluna].map(
                lambda v: v.isoformat() if hasattr(v, "isoformat") else v
            )

    return df.astype(object).where(df.notna(), "").values.tolist()


def enviar(sh, df, nome_aba, lote=5000, pausa=2):
    try:
        ws = sh.worksheet(nome_aba)
        ws.clear()
    except gspread.WorksheetNotFound:
        ws = sh.add_worksheet(
            title=nome_aba,
            rows=len(df) + 1,
            cols=len(df.columns)
        )

    ws.resize(rows=len(df) + 1, cols=len(df.columns))
    ws.update(range_name="A1", values=[list(df.columns)])

    valores = df_para_valores(df)

    for i in range(0, len(valores), lote):
        ws.append_rows(
            valores[i:i + lote],
            value_input_option="RAW"
        )
        print(f"{nome_aba}: {min(i + lote, len(valores))} / {len(valores)}")
        time.sleep(pausa)

    linhas_lidas = len(ws.col_values(1)) - 1
    if linhas_lidas != len(df):
        raise RuntimeError(
            f"Aba {nome_aba}: enviei {len(df)}, li {linhas_lidas}."
        )

    print(f"OK - {nome_aba}: {len(df)} linhas")
    return ws


def remover_aba_padrao(sh):
    abas = sh.worksheets()
    nomes_padrao = ("Página1", "Sheet1", "Planilha1")

    for aba in abas:
        if (
            aba.title in nomes_padrao
            and len(abas) > 1
            and not aba.get_all_values()
        ):
            sh.del_worksheet(aba)
```

Escolha **uma** das opções abaixo para montar o dicionário `BASES`. Cada chave deve ser o nome exato da tabela e cada valor deve ser um DataFrame.

**Opção A - Carregar arquivos CSV fornecidos pelo instrutor**

```python
from google.colab import files

files.upload()  # Selecione os CSVs do tema.

BASES = {
    "nome_tabela_1": pd.read_csv("nome_tabela_1.csv"),
    "nome_tabela_2": pd.read_csv("nome_tabela_2.csv"),
}

total = sum(len(df) for df in BASES.values())
print({nome: len(df) for nome, df in BASES.items()}, "| total:", total)
```

Use os nomes de arquivo correspondentes ao tema:

| Tema | CSV da dimensão | CSV do fato |
|---|---|---|
| Estacionamento | `vagas.csv` | `movimentacoes.csv` |
| Posto de saúde | `pacientes.csv` | `atendimentos.csv` |
| Streaming de filmes | `filmes.csv` | `visualizacoes.csv` |
| Atendimento ao cliente | `clientes.csv` | `chamados.csv` |
| Passagens aéreas | `voos.csv` | `reservas.csv` |
| Serviço meteorológico | `estacoes.csv` | `leituras.csv` |
| Telemetria esportiva | `pilotos.csv` | `voltas.csv` |
| Festival de música | `atracoes.csv` | `ingressos_vendidos.csv` |

**Opção B - Gerar as tabelas com Faker e NumPy**

O exemplo abaixo demonstra a estrutura para duas tabelas relacionadas. Adapte as colunas, os tipos e as regras de geração à ficha do tema.

```python
import numpy as np
from faker import Faker
import pandas as pd

rng = np.random.default_rng(42)
fake = Faker("pt_BR")
Faker.seed(42)

# Tabela de dimensão/referência
N1 = 10_000
tabela_1 = pd.DataFrame({
    "coluna_1": np.arange(1, N1 + 1),
    "coluna_2": rng.choice(["A", "B", "C"], size=N1),
    # Inclua aqui todas as colunas da ficha.
})

# Tabela de fato: a chave estrangeira referencia IDs existentes.
N2 = 20_000
tabela_2 = pd.DataFrame({
    "coluna_1": np.arange(1, N2 + 1),
    "coluna_2": rng.integers(1, N1 + 1, size=N2),
    # Inclua aqui todas as colunas da ficha.
})

BASES = {
    "nome_tabela_1": tabela_1,
    "nome_tabela_2": tabela_2,
}

COLUNAS_FICHA = {
    "nome_tabela_1": ["coluna_1", "coluna_2"],
    "nome_tabela_2": ["coluna_1", "coluna_2"],
}

for nome, df in BASES.items():
    assert list(df.columns) == COLUNAS_FICHA[nome], f"Colunas erradas em {nome}"

total = sum(len(df) for df in BASES.values())
print({nome: len(df) for nome, df in BASES.items()}, "| total:", total)
```

Para campos fictícios, o Faker oferece, por exemplo, `fake.name()` e `fake.city()`. Revise os resultados para garantir que não correspondam a pessoas conhecidas. No tema Posto de Saúde, prefira identificadores fictícios (por exemplo, `PAC-0001`) em vez de nomes.

**Célula 9 - Enviar todas as tabelas**

```python
for nome, df in BASES.items():
    enviar(sh, df, nome)

remover_aba_padrao(sh)
```

O envio ocorre em lotes de 5.000 linhas, com pausa de 2 segundos entre os lotes. A função limpa o conteúdo da aba antes de gravar os dados, evitando duplicação quando a célula é executada novamente.

**Célula 10 - Validar a base**

```python
total = sum(len(df) for df in BASES.values())
print("Total de linhas:", f"{total:,}".replace(",", "."))

assert total >= 20_000, "Abaixo do mínimo de 20.000 linhas."

for nome, df in BASES.items():
    ws = sh.worksheet(nome)

    assert ws.row_values(1) == list(df.columns), (
        f"Cabeçalho diferente em {nome}"
    )
    assert len(ws.col_values(1)) - 1 == len(df), (
        f"Contagem diferente em {nome}"
    )

print("A planilha confere com a base gerada.")
```

Depois da validação no código, abra a planilha e confira manualmente:
- Uma aba por tabela, com o nome correto.
- Cabeçalho na primeira linha, idêntico ao da ficha.
- Quantidade de registros esperada em cada aba.
- Chaves estrangeiras apontando para IDs existentes.
- Ausência de dados pessoais reais ou identificáveis.

## Uso responsável de IA e privacidade

A IA pode apoiar a criação de nomes claramente fictícios, categorias e textos de exemplo. Ela não deve ser tratada como fonte de estatísticas reais sem verificação.

- Prefira Faker e NumPy para gerar grandes volumes de dados repetitivos.
- Use IA generativa apenas para casos pontuais e revise o resultado.
- Não solicite nem utilize dados pessoais de pessoas reais, mesmo como exemplo.
- Registre quando um trecho ou conjunto de dados recebeu apoio de IA.
- Não apresente dados simulados como fatos ou estatísticas reais.
- No tema de saúde, redobre o cuidado: todos os registros e identificadores devem ser fictícios.

## Solução de problemas

| Sintoma ou erro | Causa provável | Verificação ou correção |
|---|---|---|
| Planilha não atualiza, sem mensagem de erro | Planilha não compartilhada com a credencial | Compartilhe com o `client_email` como Editor |
| Escrita ocorre em outra planilha ou aba | ID ou aba incorretos | Confira `print(sh.title, ws.title, sh.url)` e abra o link |
| Células não produzem o resultado esperado | Execução fora de ordem ou célula não executada | Execute o notebook de cima para baixo |
| `APIError 403 PERMISSION_DENIED` | Falta de permissão | Revise o compartilhamento com a service account |
| `Google Sheets API has not been used...` | API não ativada | Ative a Google Sheets API no projeto |
| `SpreadsheetNotFound` | ID incorreto ou falta de acesso | Confira o ID e as permissões |
| `KeyError` | Nome de coluna diferente do esquema | Corrija o dicionário retornado pela função de geração |
| `APIError 429 Quota exceeded` | Limite de requisições atingido | Aguarde, reduza o lote ou aumente a pausa |
| Código Python não executa no Apps Script | Ambiente incompatível | Execute Python no Google Colab; Apps Script utiliza JavaScript |

**Regra de diagnóstico:** executar sem erro não garante que os dados chegaram à planilha. Sempre leia os valores de volta e compare cabeçalhos e contagens com a base enviada.

## Conceitos e referências rápidas

| Termo | Significado |
|---|---|
| API | Interface que permite a comunicação entre sistemas por meio de solicitações e respostas definidas |
| Autenticação | Processo de comprovar a identidade de quem solicita acesso |
| Service account | Identidade de aplicação usada para acessar serviços do Google |
| Google Sheets API | Interface para ler e escrever dados em planilhas Google |
| Google Drive API | Interface para gerenciar arquivos no Google Drive |
| Apps Script | Ambiente de automação do Google baseado em JavaScript |
| Dado mockado | Dado fictício criado para testes, treinamento ou simulação |
| Esquema de dados | Definição de tabelas, colunas e respectivos tipos |
| Chave primária (PK) | Identificador único de um registro |
| Chave estrangeira (FK) | Campo que referencia um registro de outra tabela |
| IA responsável | Uso de IA com verificação, transparência e respeito à privacidade |

### HTTP Status Codes

| Código | Nome | Significado geral |
|---:|---|---|
| 200 | OK | Requisição concluída com sucesso |
| 201 | Created | Recurso criado |
| 204 | No Content | Requisição concluída sem conteúdo de resposta |
| 400 | Bad Request | Requisição inválida ou malformada |
| 401 | Unauthorized | Autenticação ausente ou inválida |
| 403 | Forbidden | Identidade autenticada sem permissão para o recurso |
| 404 | Not Found | Recurso não encontrado |
| 500 | Internal Server Error | Erro interno do servidor |
| 502 | Bad Gateway | Resposta inválida recebida por um servidor intermediário |
| 503 | Service Unavailable | Serviço temporariamente indisponível |
| 504 | Gateway Timeout | Tempo de espera por resposta excedido |

## Critérios de conclusão

- [ ] Tema escolhido e mantido ao longo da trilha.
- [ ] Google Sheets API e Google Drive API ativadas.
- [ ] Service account criada e credencial armazenada nos Secrets do Colab.
- [ ] Planilha compartilhada com a service account como Editor.
- [ ] Conexão testada e 10 registros de teste gravados.
- [ ] Todas as tabelas do tema geradas ou carregadas.
- [ ] Pelo menos 20.000 linhas somadas entre as tabelas.
- [ ] Cabeçalhos e nomes das abas conferidos com a ficha.
- [ ] Chaves estrangeiras e contagens validadas.
- [ ] Dados fictícios e uso de IA registrados de forma transparente.
- [ ] Planilha final conferida no navegador e apresentada ao instrutor.

---

<p align="center">
  <sub>Desafio 01 · Python, APIs e IA · Projeto de formação em Análise de Dados</sub>
</p>
