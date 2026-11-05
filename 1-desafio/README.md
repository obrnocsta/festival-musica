# 🎶 Desafio 01 — Festival de Música

Projeto do bootcamp de **Análise de Dados** da **Generation Brasil**. O desafio consiste em criar uma base de dados fictícia sobre um **festival de música**, gerá-la com Python no Google Colab e enviá-la automaticamente para uma planilha do Google Sheets, que funciona como uma "API" simples de dados.

## 📌 Sobre o projeto

O notebook `Desafio1_API_Python.ipynb` faz todo o caminho: conecta ao Google Sheets, cria a estrutura da tabela, gera dados fictícios, carrega bases maiores a partir de arquivos CSV, envia tudo em lotes e confere se o que foi gravado bate com o que foi gerado.

## 🗂️ Tabelas

| Tabela | Tipo | Linhas | Descrição |
|---|---|---:|---|
| `atracoes` | Dimensão | 10.100 | Atrações (artistas) do festival |
| `ingressos_vendidos` | Fato | 55.000 | Ingressos vendidos para as atrações |

**Total: 65.100 linhas** (o desafio exige no mínimo 20.000).

### Colunas da tabela `atracoes`

| Coluna | Descrição |
|---|---|
| `atracao_id` | Identificador único da atração |
| `nome_artista_ficticio` | Nome fictício do artista ou banda |
| `genero_musical` | Gênero (rock, pop, eletrônica, funk, sertanejo, rap, forró, reggae, mpb) |
| `edicao_festival` | Edição do festival em que a atração se apresenta |
| `dia_apresentacao` | Dia da apresentação (texto) |
| `palco` | Palco (principal, secundário, eletrônico, acústico) |
| `horario_inicio` | Horário de início (texto) |

## 🔄 Como funciona

1. **Instala e importa** as bibliotecas (`gspread`, `faker`, `pandas`).
2. **Autentica** no Google Sheets usando uma conta de serviço, com as credenciais guardadas nos *Secrets* do Colab (nada sensível vai para o código).
3. **Renomeia a aba** da planilha para o nome da tabela (`atracoes`) e escreve o **cabeçalho**.
4. **Gera 10 registros de teste** com `Faker` (`pt_BR`) e listas de valores fictícios, usando seed fixa (`42`) para os resultados serem reproduzíveis.
5. **Lê os dados de volta** da planilha para conferir cabeçalho e quantidade de linhas.
6. **Carrega os CSVs** (`atracoes.csv` e `ingressos_vendidos.csv`) em DataFrames do pandas.
7. **Envia cada tabela para uma aba**, em lotes de 5.000 linhas, com pausa entre os envios para respeitar o limite de escritas por minuto da API do Google.
8. **Valida** o resultado com `assert`: volume mínimo de linhas, cabeçalhos iguais e contagem de registros igual em cada aba.

## 🛠️ Tecnologias

- **Python**
- **Google Colab**
- **gspread**: integração com o Google Sheets
- **Faker**: geração de dados fictícios
- **pandas**: leitura e tratamento das tabelas
- **Google Sheets**: armazenamento da base

## ▶️ Como executar

1. Abra o notebook `Desafio1_API_Python.ipynb` no [Google Colab](https://colab.research.google.com/).
2. Crie uma conta de serviço no Google Cloud e ative as APIs do Google Sheets e do Google Drive.
3. Compartilhe a planilha com o e-mail da conta de serviço (com permissão de editor).
4. No Colab, abra **Secrets** (ícone de chave) e cadastre:
   - `GCP_SA_JSON`: o conteúdo do JSON da conta de serviço
   - `ID_SEGREDO`: o ID da sua planilha
5. Execute as células em ordem e, quando solicitado, selecione os arquivos CSV.

> ⚠️ Nunca publique o JSON da conta de serviço nem o ID da planilha no GitHub.

## 💡 Aprendizados

- Autenticação com conta de serviço e uso de *Secrets* para proteger credenciais
- Leitura e escrita no Google Sheets via Python
- Geração de dados fictícios e reproduzíveis com `Faker` e seeds
- Envio de grandes volumes em lotes, respeitando limites de API
- Validação de dados com `assert` para garantir a integridade da carga

## 👤 Autor

**Thúlio Ferreira Jacauna**

- GitHub: [Thuliofj](https://github.com/Thuliofj)
- LinkedIn: [thulioferreirajacauna](https://www.linkedin.com/in/thulioferreirajacauna)
- X: [@ThulioFJ](https://x.com/ThulioFJ)

---

📚 Projeto desenvolvido durante o bootcamp de Análise de Dados da Generation Brasil.
