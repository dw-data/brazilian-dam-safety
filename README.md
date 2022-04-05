# In Brazil, 1 million live near dangerous dams 

This repository contains the source code and the detailed methodology for the [DW story about threatening dams in Brazil](#).

 ## Data sources 

 To estimate how many people live around dangerous dams in Brazil, two main data sources were used: 

 - [SNISB](https://www.ana.gov.br/exporta-planilha/snisb/relatorio_barragens.csv), the National Dam Safety Database, which contains detailed information about the state of the known dams in the country. Data was extracted on February 7, 2022. 

- The [Statistical Grid](https://censo2010.ibge.gov.br/noticias-censo.html?busca=1&id=3&idnoticia=3123&t=grade-estatistica-permite-obter-dados-censo-2010-diversos-recortes-espaciais&view=noticia) published by IBGE, the Brazilian Institute for Geography and Statistics, which contains detailed information about the distribution of the Brazilian population on the territory. Although it was published in 2016, the dataset is based on 2010 Census data, the most recent survey available.	The data consists of millions of squares, ranging in area from 300 square meters to 1 square kilometer, for which the total amount of people living inside it is known. 

Additionally, the article also relied on data compiled by the researchers Mariano Andrade da Silva and Eliane Lima e Silva on [this research paper](https://doi.org/10.1590/0103-11042020E217); on [SIGBM](https://app.anm.gov.br/SIGBM/Publico/ClassificacaoNacionalDaBarragem), a national dataset on tailing dams mantained by the National Mining Agency (ANM); and on [MUNIC 2020](https://www.ibge.gov.br/#), a survey conducted by the IBGE with city administrators in Brazil.

Most of the maps used in the analysis and in the data visualizations were obtained through [geobr](https://github.com/ipeaGIT/geobr), a geographical package mantained by the Institute of Applied Economic Research (IPEA).

The population estimates, used to calculate the ratio of people living near dangerous dams in each city, state and region of the country, were downloaded from [this data repository](https://basedosdados.org/dataset/br-ibge-populacao) mantained by Base dos Dados, a non-profit organization that cleans and offers easier access to Brazilian public datasets.

## Methodology 

 The first step in the data analysis was to define and identify what a "dangerous dam" is. To do so, we selected all the dams that had, simultaneously, a high risk and a high potential damage classification in the SNISB dataset. 

 A high risk classification indicates that this dam has design, maintenance, safety planning or structural problems that put them at a higher risk of accidents. 

 A high potential damage classification, in turn, means that an incident would have severe impacts not only in potential casualties, but also on environmental damage and economic losses. 

 After detecting the dams that followed this criteria, the Geopandas Python package was used to draw a 1000m radius around their location. 

Then, using Geopandas, the intersection between those radiuses and the polygons of IBGE's statistical grid was computed. All the polygons in the statistical grid that intersect one or more dangerous dams were selected. After removing duplicate entries (that is, grid squares that are intersecting the radius of more than one dam), the population that lives inside the squares were summed, reaching a total of 937,648. 

This leads to an important caveat: in practice, we are not counting the people living inside a 1km radius from the dam, but all the **people that live inside populated sections of the grid that touch this same radius**. 

According to the experts interviewed, this area is likely to heavily **underestimate** the amount of people that would be affected in the event of failure.  

Nevertheless, since it wasn't possible to take into account factors such as the local topography, which are important for measuring potential impacts, we decided to be cautious and err on the conservative side. 

## Repository structure

Since most of the data files used in this analysis are too large, they weren't published in the repository. The links for download are available on the "data sources" item of this documentation.

The `code` directory is divided in four different subdirectories. In the subdirectory `data-prep`, you can find the scripts that were used to clean, concatenate and convert the formats of the source datasets. The files produced there are read by the scripts in `analysis`, which outline the main findings of the story. In `viz`, you can find the scripts that generated basic data visualizations which were later added in Adobe Illustrator.

The `docs` directory contain PDF files with documents produced by the Brazilian Water Agency (ANA), which were also used as sources for this story. It also contains the full text of an article by Mariando Andrade da Silva and Eliane Lima e Silva, Brazilian researchers which offered an outline of the health risks posed by the dams in the country, and, most importantly for this piece, a summary of the 19 largest dam disasters that happened in Brazil from 1986 to 2019.





