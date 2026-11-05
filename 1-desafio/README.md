# Desafio 01 — Festival de Música

Projeto do bootcamp de **Análise de Dados da Generation Brasil**. O objetivo é criar uma base fictícia de um festival de música usando Python, Google Colab e Google Sheets.

## Estrutura da base

| Tabela | Tipo | Registros |
|---|---|---:|
| `atracoes` | Dimensão | 10.100 |
| `ingressos_vendidos` | Fato | 55.000 |
| **Total** |  | **65.100** |

A base atende ao requisito mínimo de 20.000 registros.

### Tabela `atracoes`

| Coluna | Descrição |
|---|---|
| `atracao_id` | Identificador da atração |
| `nome_artista_ficticio` | Nome fictício do artista ou banda |
| `genero_musical` | Gênero musical |
| `edicao_festival` | Edição do festival |
| `dia_apresentacao` | Data da apresentação |
| `palco` | Palco da apresentação |
| `horario_inicio` | Horário de início |

## Funcionamento

O notebook `Desafio1_API_Python.ipynb`:

1. conecta o Python ao Google Sheets;
2. autentica usando uma conta de serviço;
3. cria os cabeçalhos das tabelas;
4. gera dados fictícios com `Faker`;
5. carrega os arquivos `atracoes.csv` e `ingressos_vendidos.csv`;
6. envia os dados em lotes de 5.000 registros;
7. valida cabeçalhos, contagens e volume total.

## Tecnologias

- Python
- Google Colab
- Google Sheets
- `gspread`
- `Faker`
- `pandas`

## Como executar

1. Abra o notebook no [Google Colab](https://colab.research.google.com/).
2. Configure uma conta de serviço no Google Cloud.
3. Ative as APIs do Google Sheets e Google Drive.
4. Compartilhe a planilha com a conta de serviço como **Editor**.
5. Cadastre as credenciais nos **Secrets** do Colab:
   - `GCP_SA_JSON`
   - `ID_SEGREDO`
6. Execute as células na ordem.
7. Quando solicitado, envie os arquivos CSV.

> Nunca publique o JSON da conta de serviço ou o ID da planilha em repositórios públicos.

## Aprendizados

- Autenticação com conta de serviço;
- Uso de Secrets para proteger credenciais;
- Geração de dados fictícios com `Faker`;
- Integração entre Python e Google Sheets;
- Envio de grandes volumes em lotes;
- Validação de dados com `assert`.

## Autor

**Bruno Costa da Silva**

- [LinkedIn](https://www.linkedin.com/in/obrnocsta)

Projeto desenvolvido durante o bootcamp de Análise de Dados da **Generation Brasil**.
