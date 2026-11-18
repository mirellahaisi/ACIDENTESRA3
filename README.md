# Projeto de análise de acidentes em rodovias federais

Projeto acadêmico sobre os acidentes registrados pela Polícia Rodoviária Federal (PRF) em 2025, desenvolvido em três etapas:

- **RA1 — preparação:** leitura e exploração da base, diagnóstico de qualidade, limpeza e transformação dos dados com PySpark.
- **RA2 — streaming:** simulação de chegada de registros, agregação por janelas diárias e validação dos resultados contra processamento em lote.
- **RA3 — análise:** respostas às cinco perguntas do projeto por meio de pandas e NumPy, visualizações com Matplotlib e classificação supervisionada com scikit-learn.

Como a base contém várias linhas por acidente (pessoas, veículos, causas e tipos), as análises consideram a unidade adequada a cada pergunta, como acidentes distintos (`id`) ou condutores identificados.

## Arquivos

- `Projeto_Acidentes_2025_RA1_RA2_RA3_AJUSTES_FINAIS_EXECUTADO.ipynb` — notebook com explicações, código e resultados de uma execução completa.
- `requirements_ra3.txt` — dependências Python.
- `acidentes2025_todas_causas_tipos.csv` — arquivo de dados esperado pelo notebook; não é versionado neste repositório por seu tamanho. Baixe a extração de acidentes de 2025 agrupada por pessoa (todas as causas e tipos) no [portal de dados abertos da PRF](https://www.gov.br/prf/pt-br/acesso-a-informacao/dados-abertos/dados-abertos-da-prf).

O notebook também referencia o [dicionário oficial de acidentes da PRF](https://www.gov.br/prf/pt-br/acesso-a-informacao/dados-abertos/dicionario-acidentes).

## Requisitos

- Python compatível com as versões listadas em `requirements_ra3.txt`.
- Java 17 ou superior para o PySpark 4.0. Recomenda-se Java 17 LTS; configure `JAVA_HOME` antes de iniciar Jupyter ou VS Code.
- Jupyter Notebook, JupyterLab ou VS Code com suporte a notebooks.

Confira a instalação do Java com `java -version`. Instalar PySpark com `pip` não instala o JDK.

## Instalação e execução

1. Clone o repositório e entre na pasta:

   ```bash
   git clone https://github.com/mirellahaisi/ACIDENTESRA3.git
   cd ACIDENTESRA3
   ```

2. Crie e ative um ambiente virtual e instale as dependências:

   ```bash
   python -m venv .venv
   source .venv/bin/activate
   python -m pip install -r requirements_ra3.txt
   ```

   No Windows, ative o ambiente com `.venv\Scripts\activate`.

3. Baixe o CSV no portal da PRF e escolha uma das opções:
   - Coloque `acidentes2025_todas_causas_tipos.csv` no diretório de trabalho do notebook; ou
   - Configure o caminho do seu próprio arquivo em uma célula antes da leitura:

     ```python
     import os
     os.environ["CAMINHO_DADOS"] = "/caminho/para/acidentes2025_todas_causas_tipos.csv"
     ```

     No Windows, use o caminho local do arquivo, por exemplo `r"C:\dados\acidentes2025_todas_causas_tipos.csv"`.

   O notebook procura primeiro `CAMINHO_DADOS`, depois o arquivo no diretório de trabalho e, por fim, `/content` (Colab). Nenhum caminho de computador pessoal está definido no projeto.

4. Abra o notebook, selecione o kernel do ambiente virtual e execute as células em ordem, do início ao fim. A célula inicial instala/valida as bibliotecas; se instalar ou atualizar pacotes, reinicie o kernel e execute novamente. As etapas RA2 e RA3 dependem de objetos criados durante a preparação do RA1.

## Execução e resultados

O notebook incluído tem as células de código executadas e seus resultados preservados. Para reproduzir os cálculos ou gerar novamente as figuras e a simulação de streaming, forneça o CSV e execute todas as células em ordem. A execução original registra 584.010 linhas e 72.529 acidentes distintos, de 1º de janeiro a 31 de dezembro de 2025; resultados podem variar se a extração ou as versões das bibliotecas forem diferentes.

As figuras do RA3 são salvas em `figuras_ra3/`. Os arquivos de entrada e checkpoint da simulação RA2 são criados em `ra2_streaming_acidentes/`. Esses itens são saídas locais e não precisam ser adicionados ao Git.
