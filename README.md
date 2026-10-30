# Base de Dados Municipais do Brasil — IBGE

Projeto de coleta, integração e consolidação de dados municipais brasileiros a partir de APIs oficiais do Instituto Brasileiro de Geografia e Estatística (IBGE).

## Objetivo

Construir uma base de dados unificada contendo informações dos municípios brasileiros, reunindo indicadores de diferentes áreas em uma única estrutura tabular.

A base utiliza o código oficial do IBGE como identificador municipal, permitindo relacionar informações territoriais, demográficas, econômicas, educacionais, de saúde e infraestrutura.

## Fontes de dados

Os dados são obtidos por meio de APIs oficiais do IBGE:

- **API de Localidades:** identificação dos municípios, códigos IBGE, unidades da federação, estados e regiões.
- **API de Indicadores do Portal Cidades e Estados (Cidades@):** obtenção dos indicadores estatísticos municipais.

Links das fontes:

- [API de Localidades](https://servicodados.ibge.gov.br/api/v1/localidades/municipios)
- [IBGE — Cidades e Estados](https://www.ibge.gov.br/cidades-e-estados.html)

## Abrangência

A base contempla os **5.570 municípios brasileiros**, identificados por seus respectivos códigos oficiais de 7 dígitos do IBGE.

## Indicadores disponíveis

A base reúne indicadores de diferentes áreas, incluindo:

- Demografia;
- Território;
- Economia;
- Educação;
- Saúde;
- Infraestrutura;
- Aspectos geográficos e regionais.

### Relação de variáveis

Abaixo estão relacionadas as colunas presentes na base de dados:

**Colunas disponíveis:** `codigo_ibge estabelecimentos_saude_sus estabelecimentos_saude_sus_ano mortalidade_infantil mortalidade_infantil_ano matriculas_ensino_fundamental matriculas_ensino_fundamental_ano matriculas_ensino_medio matriculas_ensino_medio_ano docentes_ensino_fundamental docentes_ensino_fundamental_ano docentes_ensino_medio docentes_ensino_medio_ano estabelecimentos_ensino_fundamental estabelecimentos_ensino_fundamental_ano estabelecimentos_ensino_medio estabelecimentos_ensino_medio_ano pib_per_capita pib_per_capita_ano arborizacao_vias_publicas arborizacao_vias_publicas_ano esgotamento_sanitario_adequado esgotamento_sanitario_adequado_ano urbanizacao_vias_publicas urbanizacao_vias_publicas_ano populacao_renda_per_capita_maior_meio_salario populacao_renda_per_capita_maior_meio_salario_ano taxa_escolarizacao_6_14 taxa_escolarizacao_6_14_ano populacao_exposta_risco populacao_exposta_risco_ano populacao_censo populacao_censo_ano populacao_estimada populacao_estimada_ano internacoes_diarreia_sus_100mil internacoes_diarreia_sus_100mil_ano receitas_brutas_realizadas receitas_brutas_realizadas_ano despesas_brutas_empenhadas despesas_brutas_empenhadas_ano transferencias_correntes transferencias_correntes_ano populacao_ocupada populacao_ocupada_ano area_km2 area_km2_ano hierarquia_urbana hierarquia_urbana_ano regiao_influencia regiao_influencia_ano bioma bioma_ano sistema_costeiro_marinho sistema_costeiro_marinho_ano regiao_intermediaria regiao_intermediaria_ano regiao_imediata regiao_imediata_ano mesorregiao mesorregiao_ano microrregiao microrregiao_ano area_urbanizada_km2 area_urbanizada_km2_ano densidade_demografica densidade_demografica_ano pessoal_ocupado pessoal_ocupado_ano rendimento_medio_sal_min rendimento_medio_sal_min_ano`

## Metodologia

O processamento compreende as seguintes etapas:

1. Obtenção da relação de municípios e seus códigos oficiais por meio da API de Localidades.
2. Consulta aos indicadores municipais disponibilizados pela API do Cidades@.
3. Seleção do ano mais recente disponível para cada indicador.
4. Transformação e organização dos dados em estrutura tabular.
5. Padronização dos códigos municipais para compatibilizar as diferentes fontes.
6. Integração das informações em uma única base, utilizando o código IBGE como chave.
7. Verificação da correspondência entre municípios e indicadores e análise da completude dos dados.
8. Exportação do resultado em formato CSV.

## Referência temporal

Os indicadores não possuem necessariamente o mesmo ano de referência. Cada variável utiliza o período mais recente disponibilizado pelo IBGE no momento da consulta.

Quando disponível, o ano de referência é armazenado em uma coluna específica associada ao respectivo indicador.

## Validação

Foram realizadas conferências manuais de valores selecionados no portal oficial IBGE — Cidades e Estados, comparando os resultados apresentados no portal com aqueles obtidos pelo processo automatizado.

Os valores verificados foram compatíveis com os dados retornados pelas APIs.

Essa conferência constitui uma validação adicional do procedimento de coleta e integração, não representando uma auditoria individual de todos os municípios e indicadores.

## Como utilizar

O projeto disponibiliza o notebook `indicadores_municipais_ibge.ipynb`, que contém todo o código necessário para realizar a coleta, o processamento e a exportação dos dados.

Para executar:

1. Baixe o arquivo `indicadores_municipais_ibge.ipynb`.
2. Abra-o em um ambiente Jupyter Notebook ou JupyterLab.
3. Certifique-se de que as bibliotecas necessárias estejam instaladas (`requests`, `pandas` e `numpy`, quando utilizadas).
4. Execute as células sequencialmente.
5. Ao final, será gerado o arquivo `municipios_ibge.csv`.

### Observação sobre o Google Colab

Durante os testes, foi identificada uma limitação de conectividade do Google Colab com o domínio `servicodados.ibge.gov.br`, ocasionando erros de timeout nas consultas à API.

A mesma rotina foi executada com sucesso em ambiente Jupyter Notebook local.

Por esse motivo, recomenda-se a execução local do notebook. A disponibilidade de acesso à API depende da conectividade com os servidores do IBGE.

## Resultado

O processamento gera um arquivo `municipios_ibge.csv`, contendo uma linha por município e as colunas correspondentes aos indicadores disponíveis.

O arquivo utiliza codificação UTF-8 com BOM (`utf-8-sig`), visando facilitar sua utilização em ferramentas como Microsoft Excel e LibreOffice Calc.

## Atualização e expansão

Como os dados são obtidos diretamente das APIs do IBGE, o notebook pode ser executado novamente para incorporar atualizações e novos valores disponibilizados pelo instituto.

A estrutura também permite a inclusão futura de outras bases oficiais, como séries históricas do Produto Interno Bruto dos Municípios.

## Licença

Este projeto utiliza a licença MIT para seu código, permitindo sua utilização, modificação e redistribuição, inclusive para fins comerciais, conforme os termos da licença.

Os dados utilizados são provenientes de fontes oficiais do IBGE, devendo ser observadas as condições de uso e atribuição aplicáveis a essas fontes.
