# OSMBUS2PGR

## Ferramenta escrita em [Python](https://python.org) para importação de rede viária e rotas de ônibus de uma cidade a partir de dados do [OpenStreetMap](https://openstreetmap.org) para o banco de dados [PostgreSQL](https://www.postgresql.org/) com as extensões [PostGIS](https://postgis.net) e [pgRouting](https://pgrouting.org). 

### Extração de Sistema Viário
* Busca no [Nominatim](https://nominatim.openstreetmap.org/) a cidade informada pelo usuário
* Faz o download a partir do OpenStreetMap da rede viária em toda a extensão da cidade
* Segmenta todas as linhas de n vértices em n-1 linhas de 2 vértices (origem e destino do arco)
* Cria as extensões, tabelas e colunas necessárias no banco
* Preenche as colunas de custo e custo no sentido oposto da via
* Cria a topologia de rede utilizando a função [pgr_createTopology](https://docs.pgrouting.org/3.3/en/pgr_createTopology.html) do pgRouting

### Extração de Rotas
* Busca no Nominatim a cidade informada pelo usuário
* Faz o download de todas as [relations](https://wiki.openstreetmap.org/wiki/Relation:route) de rotas de ônibus na extensão da cidade (inclusive rotas intermunicipais)
* Cria tabelas rotas, rotas_vias e rotas_paradas no banco
* Faz o preenchimento das tabelas a partir do processamento dos dados obtidos do OpenStreetMap

Testado com:
- Python 3.9.2
- PostgreSQL 14
- PostGIS 3.2.2
- pgRouting 3.3.0

Dependências:
- [requests](https://pypi.org/project/requests/)
- [psycopg2](https://pypi.org/project/psycopg2/)
- [dotenv](https://pypi.org/project/dotenv/)