<p align="center">
  <img src="imagens/banner.png" alt="Desafios técnicos da Generation Brasil">
</p>

# Desafios Técnicos

Repositório de materiais e atividades dos desafios técnicos do Bootcamp da Generation Brasil. Cada desafio reúne seus próprios guias, conteúdos e arquivos de apoio; esta página serve como ponto de entrada e catálogo, preparado para receber novos desafios.

## Catálogo de desafios

| Desafio | Tema | Material | Conteúdo |
|---|---|---|---|
| 1 | Python, APIs e IA | [Abrir materiais do Desafio 1](.) | Preparação, conexão com Google Sheets e construção de uma base de dados fictícia |

> Novos desafios serão adicionados a esta tabela. Para manter a navegação organizada, cada desafio deve ficar em sua própria pasta e incluir um README com objetivo, materiais, instruções e arquivos de apoio.

## Desafio 1 · Python, APIs e IA

No primeiro desafio, cada participante escolhe um dos oito temas abaixo e trabalha com ele ao longo do bootcamp. O mesmo tema será utilizado nas atividades de Estatística, Excel, SQL/Data Vis e Big Data.

### Guias

| Material | Conteúdo |
|---|---|
| [Guia principal](Guia_Desafio1_Google_Colab.md) | Preparação e conteúdo da sessão |
| [Parte 2](Guia_Desafio1_Google_Colab_Parte2.md) | Prática: conexão com o Google Sheets e escrita de dados de teste |
| [Parte 3](Guia_Desafio1_Google_Colab_Parte3.md) | Continuação do trabalho autônomo e conclusão da base |

### Temas e planos de dados

Cada tema possui um plano de modelagem com esquema, tabelas, volumetria e regras de geração. Os nomes de coluna definidos nos planos devem ser usados sem alterações.

| # | Tema | Plano | Tabelas (dimensão · fato) | Linhas aproximadas |
|---:|---|---|---|---:|
| 1 | Estacionamento | [Plano](bases_dados/01-estacionamento/01-estacionamento.md) | `vagas` · `movimentacoes` | 52.200 |
| 2 | Posto de saúde (triagem) | [Plano](bases_dados/02-posto-de-saude/02-posto-de-saude.md) | `pacientes` · `atendimentos` | 52.500 |
| 3 | Streaming de filmes | [Plano](bases_dados/03-streaming-de-filmes/03-streaming-de-filmes.md) | `filmes` · `visualizacoes` | 65.300 |
| 4 | Atendimento ao cliente | [Plano](bases_dados/04-atendimento-ao-cliente/04-atendimento-ao-cliente.md) | `clientes` · `chamados` | 52.400 |
| 5 | Passagens aéreas | [Plano](bases_dados/05-passagens-aereas/05-passagens-aereas.md) | `voos` · `reservas` | 65.600 |
| 6 | Serviço meteorológico | [Plano](bases_dados/06-servico-meteorologico/06-servico-meteorologico.md) | `estacoes` · `leituras` | 72.050 |
| 7 | Telemetria esportiva | [Plano](bases_dados/07-telemetria-esportiva/07-telemetria-esportiva.md) | `pilotos` · `voltas` | 65.800 |
| 8 | Festival de música | [Plano](bases_dados/08-festival-de-musica/08-festival-de-musica.md) | `atracoes` · `ingressos_vendidos` | 65.100 |

Os planos foram conferidos com o script `gerar_bases.py`. Os dados são fictícios e reproduzíveis, gerados com semente fixa e exportados em CSV. Consulte cada plano para ver o esquema e os detalhes da geração.

### Organização dos dados

Os temas começam com duas tabelas relacionadas:

- **Dimensão/cadastro:** descreve a entidade central e possui uma chave primária única.
- **Fato/evento:** registra ocorrências e referencia a dimensão por uma chave estrangeira.

Essa estrutura serve de base para atividades posteriores, que podem acrescentar dimensões e explorar relacionamentos e modelos em estrela.

### Fluxo de trabalho

1. Escolha um tema e leia seu plano de dados.
2. Siga os guias para configurar a credencial e conectar o Python ao Google Sheets pelo Colab.
3. Escreva o cabeçalho e valide os dados de teste.
4. Gere ou carregue as tabelas completas e confira os resultados.

### Boas práticas

- Use somente dados fictícios; nunca inclua dados pessoais reais. Tenha cuidado especial com temas sensíveis, como saúde.
- Mantenha os nomes e tipos de coluna conforme o plano do tema.
- Proteja as credenciais: não publique arquivos JSON, chaves ou segredos.
- Use IA como apoio, verifique o conteúdo gerado e não apresente estatísticas inventadas como fatos reais.

## Como incluir um novo desafio

Ao adicionar uma atividade, inclua uma linha no catálogo com o número, o tema, o link para a pasta ou guia principal e uma descrição curta. Organize os materiais específicos na pasta do desafio e documente no README correspondente seus objetivos, etapas, dependências e cuidados relevantes. Assim, a página principal continua sendo um índice geral, sem misturar instruções particulares de atividades diferentes.
