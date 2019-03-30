Web Scraping - Despesas dos Municípios do Estado da Bahia, via site do
Tribunal de Contas dos Municípios do Estado da Bahia - TCM-Ba
================
George Santiago
17 de fevereiro de 2019

# O Projeto

O pacote `tcmbadespesas` é uma das ferramentas utilizadas no projeto de
“Transparência das Contas Públicas”, desenvolvido e executado pelo
Observatório Social do Brasil - Município de Santo Antônio de Jesus -
Estado da Bahia.

## Sobre a proposta e o objetivo do pacote

O objetivo do pacote `tcmbadespesas` é obter/capturar os dados de
Despesas dos Municípios da Bahia, custodiados e disponibilizados
publicamente no site do Tribunal de Contas dos Municípios do Estado da
Bahia (TCM-Ba - [link do
TCM-Ba](http://www.tcm.ba.gov.br/consulta-de-despesas/). Para tanto, foi
aplicado uma técnica denominada “Web Scraping” para ‘capturar’ os dados
no formato de arquivo eletrônico HTML e, após o seu tratamento e
modelagem, consolidar todos os dados num formato *legível por máquina*
que permita a sua utilização em ferramentas de análise de dados como
Excel, Power Bi, Qlik, Tableau, RStudio… dentre outras.

Todo o esforço empregado no desenvolvimento desta ferramenta tem como
motivação o propósito de tornar o conteúdo das Contas Públicas mais
acessíveis ao cidadão, ao capturar dados e, em seguida, aplicar técnicas
de visualização que permitam a qualquer pessoa obter respostas a partir
de perguntas simples como, por exemplo: Qual são os maiores fornecedores
do ente municipal (prefeitura, câmara e entidades da adm. indireta)?
Quanto o ente municipal (prefeitura, câmara e entidades da adm.
indireta) gasta com despesas de diárias? Quanto o ente municipal
(prefeitura. câmara e entidades da adm. indireta) gasta com despesas de
Locação de Imóvel? Quanto o ente municipal (prefeitura, câmara e
entidades da adm. indireta) gasta com despesas de Combustível? Quanto o
ente municipal (prefeitura, câmara e entidades da adm. indireta) gasta
com despesas de Merenda Escolar?… dentre outras perguntas.

Além disso, parte do esforço empregado no desenvolvimento desta
ferramenta é motivado pelo fato de que o TCM-Ba ainda não disponibiliza
os dados municipais custodiados no formato de Dados Abertos (apesar de
ter um excelente Portal de Transparência dos Dados Municipais). Na
oportunidade, cabe esclarecer que há uma diferença substancial (de
propósito e de finalidade jurídica) entre *Portal de Transparência* e
*Portal de Dados Abertos*. Enquanto o Portal de Transparência visa
disponibilizar o acesso de informações com foco em dados *legíveis por
Humanos*, o Portal de Dados Abertos visa disponibilizar dados *legíveis
por máquinas* (computadores) que facilitarão a produção de conteúdo e
conhecimento (relatórios, gráficos, grafos…) para Humanos. Ou seja,
embora Portal de Transparência e Portal de Dados Abertos tenham como
objetivo maximizar a Transparência dos dados Governamentais, são
ferramentas complementares e, por isso, não se confundem. Além disso,
numa perspectiva jurídica, cabe pontuar que o Portal de Transparência,
assim como o Portal de Dados Abertos, tem fundamento jurídico
específicos na Constituição Federal de 1988, na Lei de Responsabilidade
Fiscal (Lei n.° 101/2000) e na Lei de Acesso à Informação (Lei n.º
12.527/2011), logo, é dever/obrigação dos entes públicos implementarem
as duas funcionalidades para concretizar ao máximo o princípio da
publicidade.

Nesse contexto, entretanto, cabe informar que após interlocução do
Observatório Social do Brasil - Município de Santo Antônio de Jesus com
o TCM-Ba (por meio de ofício e eventos institucionais) foi sinalizado
que o desenvolvimento de um Portal de Dados Abertos, haja vista a sua
relevância para a Sociedade.

Com isso, o TCM-Ba, assim como outros Entes Governamentais e Tribunais
de Contas do Brasil, consolidam a sua postura de parceria e colaboração
com o exercício do Controle Social da Administração Pública. Nesse
contexto, assim que o site de Portal de Dados Abertos do TCM-Ba for
lançado, o desenvolvimento do presente pacote se tornará desnecessário.
Até lá, o seu desenvolvimento será extremamente necessário para
viabilizar maior transparência e acesso das despesas dos municípios do
Estado da Bahia.

## Propósito do Web Scraping para o OS-SAJ

Ao fim da execução do “Web Scraping”, é gerado um arquivo “.csv” com os
dados de despesas coletados e tratados dos municípios indicados.

No caso do Observatório Social de Santo Antônio de Jesus, esses dados
serão utilizados para alimentar o [Painel de Monitoramento das Despesas
dos Municípios do Estado da Bahia](https://goo.gl/rQhwsg). Contudo,
disponibilizaremos a base de dados por meio do link para que qualquer
interessado possa realizar suas próprias análises.

## Etapas e Estratégias do Web Scraping

Como citado no material disponibilizado pelo do
[Curso-R](https://www.curso-r.com/material/webscraping/), há 4 (quatro)
tipos de “macro ‘desafios’ de Web Scraping” que exigem estratégias e
técnicas distintas, a saber:

  - Uma busca e uma paginação;
  - Uma busca e muitas paginações;
  - Muitas buscas e uma paginação por busca;
  - Muitas buscas e muitas paginações por busca.

Os dois primeiros “macro desafios de Web Scraping” são os mais “fáceis”,
não exigindo maiores técnicas ou estratégias, especificamente no
controle das requisição das páginas HTML. Já os dois últimos, podem
representar grandes desafios no desenvolvimento do “Web Scraping”, em
especial no controle das requisição das páginas HTML, a depender, por
exemplo: *i)* do volume (quantidade) de requisições a serem realizadas;
*ii)* de como o Servidor requisitado se comporta com o crescente número
de requisições; *iii)* das estratégias de controle a serem adotadas para
não obter dados duplicados ou “esquecer” de raspar determinadas páginas;
*iv)* da infraestrutura que será utilizada para executar o Web Scraping…
dentre outros desafios enfrentados a depender do caso concreto.

Neste Web Scraping, esfrentamos um defasio de alta dificuldade técnica
*Muitas buscas e muitas paginações por busca*, pelo menos do ponto de
vista da arquitetura de execução do código.

A título de exemplo, ao analisar a quantidade de requisições das
despesas de 25 municípios do Estado da Bahia (de uma total de 417)
somente do ano de 2018, chegamos ao número aproximado de 280.000
requisições ao site do TCM-Ba\! Isso se deve ao “caminho” a ser
percorrido até chegar na página HTML com os dados detalhados da
respectiva despesa. Para sintetizar o desafio, foi preciso percorrer 02
(duas) macro etapas: 1) Acessar, via requisição POST, as páginas que
disponibilizavam as tabelas com os dados sumarizados das despesas do
respectivo Ente Municipal (aqui, o desafio foi acessar a primeira página
e pecorrer até a última, já que cada página somente disponibilizava 20
linhas de dados); 2) Acessar, via requisição GET, cada link
disponibilizado nas páginas acessadas (as quais continham as tabela
sumarizada) para chegar ao conteúdo detalhamento das despesas.

Por exemplo, ao acessar as despesas de da Prefeitura Municipal de Santo
Antônio de Jesus referente ao exercício 2018, vamos acessar uma página
com as 20 primeiras despesas sumarizadas e mais os respectivos links
para acesso detalhados das respectivas despesas. Num cálculo simples,
conclui-se que se o site do TCM-Ba disponibiliza 20 resultados por
páginas e identificando que a Prefeitura de Santo Antônio de Jesus tem
744 páginas referntes ao exercício de 2018, teremos que realizar cerca
de 14.800 requisições para obter os dados detalhados das despesas, de um
total de quase 280.000, ao considerar somente os 25 municípios
inicialmente selecionados pelo OS-SAJ. Para incrementar o nosso cálculo,
cabe informar que cada requisição de página de despesa detalhada ao site
do TCM-Ba demora entre 5 a 12 segundos em regra. Logo, numa perspectiva
otimista (ou seja, sem interrupções), ao realizar uma requisição por
vez, demoraríamos cerca de 25 dias para concluir a obtenção de todas as
280.000 páginas referentes às despesas executadas somente por 25
municípios\!\!\!

A parti deste contexto, percebe-se que o esforço computacional para
requisitar os 417 municípios desmotivaria a obtenção dos dados, já que o
tempo que se levaria para obtê-los reduziria o interessa Social
(considerando que o interesse social é movido por fatos
recentes/atuais), pois não conseguiríamos obter dados atualizados, ainda
que pensássemos que a atualização dos dados mensalmente.

Ciente dessas informações, conclui-se, portanto, que ao considerar o
tempo de execução de um web scraping para obter dados de 417 municípios,
referentes às despesas de 2018, tal possibilidade seria inviável sob a
perspectiva computacional e do interesse social.

Por outro lado, caso o TCM-Ba adote o Portal de Dados Abertos, obter
esse volume de informação demore somente alguns minutos, pois exigirá
apenas alguns clicks do usuários para obter os dados tratados e no
formato adequado para utilização em ferramentas de análise como o Excel,
Power Bi, Qlik, Tableau, RStudio… dentre outras.

## Estrutura do Código em Linguagem R do Web Scraping

Numa perspectiva de arquitetura das etapas e de organização dos arquivos
.R, as funções para execução do código foram divididas em 17 arquivos
.R, a saber:

`01_executar_web_scraping.R` - É o ‘orquestrador’ de toda a execução do
código. É este arquivo que contém a função que executará as funções numa
ordem lógica e predefinida para obter o resultado final, ou seja: Os
dados de despesas municipais disponíveis em um formato legível por
máquina.

`02_criar_diretorios.R` - Cria a estrutura de diretórios na pasta de
trabalho (Work Directory) definida pelo usuário.

`03_criar_ws_id.R` - Cria uma arquivo .rds com metadados do Web
Scraping. Além disso, serve para identificar a pasta de trabalho (Work
Directory) do Web Scraping.

`04_connect_sgbd.R` - Cria a conexão para o Sistema Gerenciador do Banco
de Dados e, também, por padrão, cria o arquivo do Banco de Dados do
SQLite.

`05_criar_tabelas_bd.R` - Cria as tabelas no Banco de Dados.

`06_criar_tb_dcalendario.R` - Cria a tabela ‘tabela\_dcalendario’ no BD
(uma tabela dimensão, numa perspectiva do conceito de Business
Intelligence - BI), para ser utilizada tanto na confecção das tabelas de
requisição, como para construir e manter a tabela a ser utilizada no BI
(Power BI a Microsoft) que utilizados no painel de análise.

`07_criar_tb_dmunicipios.R` - Cria a tabela ‘tabela\_tcm\_dmunicipios’
no BD (uma tabela dimensão, numa perspectiva do conceito de Business
Intelligence - BI), para ser utilizada tanto na confecção das tabelas de
requisição, como para construir e manter a tabela a ser utilizada no BI
(Power BI a Microsoft) que utilizados no painel de análise.

`08_criar_tb_dmunicipios_entidades.R` - Cria a tabela
‘tabela\_tcm\_dmunicipios\_entidades’ (uma tabela dimensão, numa
perspectiva do conceito de Business Intelligence - BI), para ser
utilizada tanto na confecção das tabelas de requisição, como para
construir e manter a tabela a ser utilizada no BI (Power BI a Microsoft)
que utilizados no painel de análise.

`09_criar_tb_entidades_alvos_paginas.R` - Cria a tabela
‘tabela\_entidades\_alvos\_paginas’ no BD para ser utilizada na
confecção das tabelas de requisição, com o propósito de registrar as
páginas já “raspadas” que contêm as despesas sumarizadas dos entes
municipais, bem como os links para as páginas com as despesas
detalhadas.

`10_executar_scraping_num_pags.R` - Realiza a execução do “Web Scraping”
responsável por obter as páginas com os dados sumarizados e os links das
páginas com os dados das despesas detalhadas.

`11_criar_tb_requisicoes_despesas.R` - Realiza o ‘parser’ (extração) dos
dados contidos nos arquivos HTML que armazenam as tabelas com os dados
sumarizados e os links para acessar as páginas com os dados detalhados
das despesas e, então, confeccionar a tabela central de requisições no
Banco de Dados.

`12_executar_scraping_html_despesas.R` - Executa o Web Scraping das
páginas HTML que contêm os dados detalhados das despesas municipais.

`13_executar_data_wrangling_html_despesas.R` - Realiza o ‘parser’
(extração) dos dados das despesas municipais que estão armazenados nos
arquivos HTML.

`14_executar_tidy_data.R` - Transmuta os dados do arquivo HTML (que já
estão armazenados no BD) para o formato ‘Tidy Data’, com vista a
possibilitar a importação dos dados para qualquer software de análise de
dados.

`15_backup_arquivos.R` - Realiza o Backup dos dados.

`16_exportar_dropbox.R` - Exporta os dados tratados para o DropBox com o
objetivo de alimentar a ferramenta de BI ou disponibilizar os dados à
Sociedade.

`17_utils.R` - Arquivo que contém diversas funções confeccionadas para
utilizar durante a execução do Web Scraping.

## Outros objetivos/propósitos técnicos do Web Scraping

1 - Empregar um comportamento de Web Scraping, em vez de Web Crawler.

2 - Tornar o Web Scraping autônomo e que não pare devido a exceções após
ser executado.

3 - Tornar o Web Scraping executável por aplições de automação/tarefas
como Cron do Linux.

4 - Tornar o Web Scraping agnóstico de Sistema de Banco de Dados
Relacional (pelo menos, aceite o SQLite e MySQL).

5 - Tornar o Web Scraping reprodutível em um ambiente RStuido implantado
via Docker

6 - Exportar o resultado do Scraping para um repositório público (ex:
DropBox) para que qualquer pessoa possa baixar os dados.

7 - Desenvolver um ChatBot no Telegram para sinalizar ao mantenedor do
Web Scraping quando ele inicia e termina, ou quando ocorre um erro que
interrompe a execução. (em
desenvolvimento)

## Base de dados obtidas pelo Web Scraping (Despesas Municipais - TCM/BA)

É possível ter acesso à [base de dados das despesas municipais,
referentes a cerca de 25 municípios, por meio deste
link](https://www.dropbox.com/s/ykxn1twikwpwwie/tabela_despesas_municipais_tidy_data_BR.csv.gz?dl=1).
Os dados estão armazenados em um único arquino no formato CSV
(compactados com GZip) e armazenados no DropBox.

# Comunidade e Colaboração

O Observatório Social do Brasil, aqui representado pelo Observatório
Social do Município de Santo Antônio de Jesus - Ba, gostaria de
agradecer ao apoio da Comunidade R para o desenvolvimento do presente
pacote, em especial à comunidade
[TidyVerse](https://www.tidyverse.org/), ao
[Curso-R](https://www.curso-r.com/) pela colaboração ativa e material
disponibilizado, à comunidade R Brasil (no Telegram), e todos aqueles de
disponibilizam ebook sobre a linguagem R [link](https://bookdown.org/),
posts e desenvolvem pacotes e soluções de infraestrutura para a
linguagem R. Sem o esforço, colaboração, cooperativismo e abnegação de
todos, esse trabalho não seria possível.

Ademais, quaisquer sugestões, reclamações ou críticas podem ser
realizadas no área `issues` do GitHub.

# Preparando e Executando o pacote `tcmbadespesas`

## Infraestrutura

Caso o usuário deseje executar o “Web Scraping” do seu computador
pessoal, precisará apensas seguir a sugestão de nomenclattura dos
arguimentos abaixo:

Na hipótese do usuário preferir contratar um servidor numa
infraestrutura de nuvem (ex: DigitalOcean, Microsoft Azure, Amazon Web
Service), indicamos, a seguir, algumas dicas e condigurações para
implementação do RStudio via Docker.

Nesta sugestão de configuração via VPS na DigitalOcean usando Docker,
realizamos a instalação do Cointainer do Projeto Rocker
[link](https://hub.docker.com/r/rocker/tidyverse) (que agrupa:
Compilador R; pacote TidyVerse; e Rstudio). Para obter mais detalhes
sobre a configuração de implementação do “droplet” (nomenclatura de
‘servidor’ na DigitalOcean), indicamos como fonte de consulta o post:
[‘Run on a remote
server’](https://www.andrewheiss.com/blog/2017/04/27/super-basic-practical-guide-to-docker-and-rstudio/)
.

As demais configurações sobre o ‘Volume’ (conceito do Docker que
significa a pasta - diretório - compartilhado entre o ‘container’ Docker
e o Host ‘servidor’) e as configurações de permissão para criação,
leitura e escrita do diretório ‘os\_saj\_web\_scraping’ (nome do
diretório de trabalho escolhido pelo OS-SAJ), foram obtidos por meio de
consulta no Google. OBS: A configuração de escrita no diretório
‘os\_saj\_web\_scraping’, que será utilizado como diretório de
trabalho do ‘Web Scraping’, foi necessário, pois caso não seja
realizado, o RStudio retorna um erro que informa a impossibilidade de
escrever/gravar/modificar os arquivos no diretório selecionado para ser
o ‘Volume’.

—————— Pré-Configuração do Container Docker do Rstudio na Digital Ocean
——————

-----

—————— Configuração do Container Docker do Rstudio no Shell do Linux
——————

Após implementar o VPS do RStudio via Docker na DigitalOcean com as
diretrizes indicadas acima, será necessário instalar o pacote
`tcmbadespesas`por meio do comando:
`devtools::install_github("georgevbsantiago/tcmbadespesas")`. Concluída
a instalção, basta executar o Web Scraping com o exemplo de código
demonstado acima.

# BUGS e Melhorias

Sabemos que o código disponibilizado na versão 1.0 pode ser melhorado e
otimizado a sua performance. Contudo, até onde testamos, os resultados
obtidos mostraram-se consistentes ao objetivo final que é alimentar o
‘Painel de Monitoramento das Despesas dos Municípios do Estado da
Bahia’, que tem o acesso disponibilizado a qualquer pessoa por meio do
site do Observatório Social de Santo Antônio de Jesus.

Entretanto, registramos os seguintes tópicos para relatar: Prioridades,
Bugs, Melhorias, Implementações, Ajuste na Infraestrutura… do código:
