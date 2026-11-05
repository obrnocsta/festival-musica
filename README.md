# Desafios Técnicos

Repositório de materiais, guias e bases de apoio para os desafios técnicos do Bootcamp da Generation Brasil.

## Objetivo

Este projeto reúne os materiais do Desafio 1 e a estrutura base para a modelagem de dados fictícios em diferentes temas, com foco em:

- Python
- API do Google Sheets
- uso responsável de IA
- geração de dados simulados
- organização de bases de dados em tabelas de dimensão e fato

## Desafio 1 · Python, API e IA

O material principal está organizado em três partes:

- `Guia_Desafio1_Google_Colab.md` — preparação e conteúdo da sessão
- `Guia_Desafio1_Google_Colab_Parte2.md` — prática na sessão
- `Guia_Desafio1_Google_Colab_Parte3.md` — continuidade do trabalho autônomo

O objetivo da atividade é:

1. criar a credencial de acesso à Google Sheets API;
2. autenticar o Python no Google Colab;
3. escolher um tema entre oito opções;
4. criar a planilha e escrever dados de teste;
5. modelar a base de dados em tabelas de dimensão e fato;
6. gerar ou carregar os dados completos;
7. validar a carga na planilha;
8. registrar o uso de IA e entregar a solução com ética e consistência.

## Temas disponíveis

Os desafios usam um conjunto padronizado de temas, sempre com o mesmo modelo de dados para os próximos módulos do bootcamp:

- Estacionamento
- Posto de saúde
- Streaming de filmes
- Atendimento ao cliente
- Passagens aéreas
- Serviço meteorológico
- Telemetria esportiva
- Festival de música

Cada tema possui:

- esquema de colunas fixo;
- tabela de dimensão/cadastro;
- tabela de fato/evento;
- volumetria mínima proposta;
- regras de geração e validação.

## Estrutura do repositório

A estrutura base do projeto é organizada para facilitar a navegação e a execução dos desafios:

- `README.md` — documentação geral do repositório
- `Guia_Desafio1_Google_Colab.md` — guia inicial do desafio
- `Guia_Desafio1_Google_Colab_Parte2.md` — prática em planilha e Colab
- `Guia_Desafio1_Google_Colab_Parte3.md` — etapa final do guia
- `bases_dados/` — planos e dados dos temas
- `imagens/` — ilustrações e instruções visuais
- `icones/` — ícones dos temas

## Como funciona a modelagem

Todos os temas seguem a mesma lógica de organização:

- Dimensão/cadastro: representa a entidade central e possui chave primária única.
- Fato/evento: registra ocorrências ao longo do tempo e geralmente concentra a maior parte do volume.

Essa separação prepara o terreno para desafios mais avançados, como modelagem em estrela e joins entre tabelas.

## Regras importantes

- Nenhum dado pessoal real deve ser utilizado.
- Dados devem ser fictícios, mesmo em contextos sensíveis, como saúde.
- Nomes de colunas devem seguir exatamente o esquema definido.
- O uso de IA deve apoiar a geração, mas nunca substituir a verificação humana.
- Estatísticas e números não podem ser apresentados como fatos reais sem fonte confiável.

## Fluxo sugerido

1. Escolha um tema.
2. Leia o plano de esquema do tema.
3. Configure a credencial de acesso ao Google Sheets.
4. Crie a planilha e compartilhe com a conta de serviço.
5. Use o Colab para autenticar e testar a conexão.
6. Escreva o cabeçalho e gere dados de teste.
7. Valide a carga na planilha.
8. Gere ou carregue a base completa.
9. Registre o uso de IA e entregue o material final.

## Observação

Este repositório foi pensado como base didática para praticar modelagem de dados, API e automatização com Python, mantendo uma abordagem segura, organizada e coerente com as exigências do desafio.

---

Se quiser, posso também criar a estrutura completa de pastas e os arquivos iniciais dos temas (`bases_dados/...`) no repositório, conforme o padrão dos guias anexados.
