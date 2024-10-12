
# Votos versus Vacinas (2015 - 2022)

Este projeto tem como objetivo explorar a relação entre a cobertura vacinal no Brasil e o contexto das eleições de 2018 e 2022, com foco no impacto da concordância com as ideias dos candidatos eleitos em cada município.

---

## 📊 Objetivo
O principal objetivo é entender se existe uma correlação significativa entre o posicionamento do candidato eleito em cada município e a variação na cobertura vacinal ao longo dos anos.
Em outras palavras, a ideia é entender se municípios brasileiros que elegeram candidatos que se manifestavam expressamente contra a vacinação da covid-19 durante a pandemia tiveram ou não variação na cobertura vacinal.

---

## 🗂️ Dados Utilizados

Os dados utilizados foram coletados das seguintes fontes:

- **Eleições 2018 e 2022**: Resultados das eleições presidenciais por município.
- **Cobertura Vacinal (2015 - 2022)**: Informações de cobertura vacinal, por município, fornecidas pelo [Tabnet DATASUS](http://www2.datasus.gov.br/DATASUS/index.php?area=02).

### Caminho para as bases de dados:
- Dados brutos eleições 2018 / Dados brutos eleições 2022: [TSE](https://sig.tse.jus.br)
  - Clique em Conjunto de dados no menu lateral esquerdo
  - Selecione a opção "Resultados"
  - Escolha a opção "Votação candidato""
  - Selecione o ano de interesse e clique em próximo
  - Aplique os filtros opcionais que desejar
  - Aplique as dimensões e métricas que desejar
  - Escolha o tipo de arquivo que deseja salvar (nesse projeto ".csv")

- Dados brutos de vacinas de 2015 a 2022: [Tabnet DATASUS](http://tabnet.datasus.gov.br/cgi/dhdat.exe?bd_pni/cpnibr.def)
  - Escolha Município na opção "Linha"
  - Escolha Ano na opção "Coluna"
  - Selecione as vacinas de interesse em medidas (nesse projeto foram selecionadas todas)
  - Selecione os períodos disponíves de interesse (nesse projeto os anos 2015 a 2022)
  - Clique em Mostra no final da página
  - Salve como arquivo .csv

O período escolhido (2015 a 2022) visou contemplar um período de tempo igual (4 anos) entre antes e depois das eleições de 2018.

---

## 🛠️ Bibliotecas Utilizadas

O código foi desenvolvido em Python utilizando um Jupyter Notebook, e as bibliotecas utilizadas foram:

```bash
pip install pandas numpy matplotlib seaborn fuzzywuzzy unidecode scipy statsmodels
```

As principais bibliotecas são:
- **pandas**: Manipulação e análise de dados.
- **numpy**: Cálculos matemáticos.
- **matplotlib** e **seaborn**: Visualização de dados.
- **fuzzywuzzy**: Para correspondência de textos.
- **unidecode**: Para padronização de strings.
- **scipy** e **statsmodels**: Para testes estatísticos.

---

## 📋 Estrutura do Projeto

O projeto segue as seguintes etapas no **Jupyter Notebook**:

1. **Tratamento dos Dados de Eleições 2018**
   - Importação e limpeza dos dados.
   - Filtragem para considerar apenas resultados da eleição presidencial (uma vez que na primeira extração foram importados dados também dos Governadores).
   - Agrupamento por estado e município.
   - Padronização dos nomes de municípios com `unidecode`.

2. **Tratamento dos Dados de Vacinação (2015-2022)**
   - Leitura e limpeza dos dados brutos de vacinação.
   - Conversão de colunas de anos para o tipo numérico.
   - Padronização dos nomes dos municípios.

3. **Unificação dos Dados**
   - Merge dos dados de vacinação e eleições utilizando o nome de municípios como chave composta.
   - Aplicação de algoritmos de fuzzy matching para resolver inconsistências de nomenclatura.

4. **Análise Estatística**
   - Aplicação de testes t e regressão linear simples.
   - Uso do teste de Diferença em Diferenças (DiD) para entender o impacto das eleições na cobertura vacinal.

---

## ⚙️ Como Rodar o Projeto

### Requisitos:
- **Python 3.x**
- **Jupyter Notebook**

### Passos:
1. **Clone o repositório**:
   ```bash
   git clone [https://github.com/jessicabom/analise_cobertura_vacinal_x_eleicoes_2015_2022]
   ```
2. **Instale as dependências**:
   ```bash
   pip install -r requirements.txt
   ```
3. **Execute o Jupyter Notebook**:
   ```bash
   jupyter notebook
   ```
4. Abra o arquivo `ETL.ipynb` no Jupyter e execute as células para reproduzir a análise.

---

## 🔍 Resultados

### Principais Descobertas:
1. **Diferença Significativa**: Os testes estatísticos evidenciaram uma diferença significativa na cobertura vacinal antes e depois das eleições de 2018. Contudo não se pode descartar a influência do próprio período pandêmico, em que as medidas de isolamento nos anos 2020 e 2021 por si só poderiam justificar as diminuições verificadas, sendo um fator muito relevante. Para associar mais diretamente às eleições, foram rodadas novas análises, considerando dessa vez a permanência do voto em 2022 no candidato manifestamente contra vacinação, o que pode indicar concordância com as ideias do mesmo. Nesse caso, utilizou-se os dados do primeiro turno das eleições 2022, uma vez no segundo turno existia a possibilidade de enviesamento de escolha de um candidato em detrimento do outro, cenário esse amenizado no primeiro turno pela possibilidade de escolha de mais candidatos.
2. **Municípios com Bolsonaro (2022)**: Municípios que elegeram Bolsonaro em 2022 apresentaram, em média, uma **cobertura vacinal 6,1 pontos percentuais menor** que outros municípios.
3. **Cobertura Vacinal > 100%**: Alguns municípios apresentam cobertura vacinal acima de 100% devido a discrepâncias nas estimativas populacionais ou deslocamento de pessoas para outros municípios.

---

## 📈 Visualizações

A análise gerou gráficos para ilustrar os resultados, como:

- Comparação da cobertura vacinal entre municípios que elegeram Bolsonaro e não elegeram Bolsonaro em 2018 e em 2022.
- Comparação da cobertura vacinal antes e depois das eleições.

---

## 🤝 Contribuições

Sinta-se à vontade para abrir uma **issue** para contribuir com melhorias no projeto.

---

## 📈 Visualização de Dashboard

Os dados tratados foram utilizados para montagem de um Dashboard que pode ser acessado no seguinte diretório:

[Dashboar Tableau Public](https://public.tableau.com/views/VacinasxDesinformao-anlisedacoberturavacinalnoBrasilde2015a2022/Painel1?:language=pt-BR&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)
