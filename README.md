# GET<i>Var</i> 🧬👨🏻‍💻

O **GET<i>Var</i>** (MVP with Docker) é uma ferramenta desenvolvida para **análise e anotação de variantes genéticas**. Com um workflow eficiente, a ferramenta integra dados de variantes genômicas para identificar e interpretar anotações de variantes de forma rápida e precisa em bancos de dados públicos.

## Funcionalidades

- **Análise de Variantes**: Processamento e visualização dados de variantes genéticas.
- **Anotação Funcional**: Integração de variantes com consulta em bancos de dados genéticos.
- **Automatização**: Workflow padronizado para maior eficiência.

## Workflow da Aplicação

1. **Entrada de Dados**:

   - Apenas arquivos **VCF** são válidos como entrada.

2. **Identificação de Variantes**:

   - A aplicação faz anotações com os seguintes campos:
     - **ID**: Identificador único da variante no banco de dados de referência.
     - **CHROM**: Cromossomo onde a variante está localizada.
     - **REF**: Alelo de referência no genoma.
     - **ALT**: Alelo alternativo identificado.
     - **Population Allele Frequency**: Frequência da variante em populações conhecidas.
     - **Var Class**: Classe da variante, como SNV (Single Nucleotide Variant) ou INDEL.
     - **Most Severe Consequence**: Consequência mais grave da variante em relação à função do gene.
     - **Clinical Significance**: Relevância clínica da variante com base em dados de referência.
     - **Synonyms**: Nomes alternativos ou identificadores da variante.
     - **Ambiguity**: Nível de ambiguidade na identificação da variante.
     - **Minor Allele**: Alelo menos frequente encontrado na população.
     - **Mappings**: Informações adicionais de diferentes bancos e referências genômicas.

   - Os bancos consultados incluem **dbSNP**, **Ensembl** e **ClinVar**.

3. **Anotação Funcional**:

   - Integração com bancos de dados como dbSNP, ClinVar e Ensembl para fornecer informações funcionais e clínicas sobre as variantes.

## Tecnologias Utilizadas

- **Linguagem**: Python
- **Framework**: Snakemake, Bootstrap e Flask
- **Bancos de Dados**: Integrações com dbSNP, ClinVar e Ensembl
- **Docker**: Para contêinerização e execução do projeto.
- **Pandas**: Biblioteca Python para análise de dados.
- **NumPy**: Suporte para operações numéricas e manipulação de arrays.
- **Requests**: Para chamadas HTTP às APIs REST (dbSNP, ClinVar, Ensembl).

## Estrutura do Projeto

- **`main.py`**: Arquivo principal para executar a aplicação.
- **`api_getters.py`**: Contém funções para integrar e buscar dados externos.
- **`views.py`**: Gerencia as rotas e interações do usuário.
- **`utils.py`**: Arquivo com funções auxiliares para processamento de dados.
- **`Snakefile`**: Define os workflows automatizados usando Snakemake para gerenciar pipelines de análise.
- **`templates/`**: Arquivos HTML para visualização de resultados.
- **`static/`**: Arquivos de imagens e vídeos usados pela aplicação.
  - **`images/`**: Contém ícones, logos e outras imagens.
  - **`videos/`**: Contém vídeos ilustrativos ou de demonstração.
- **`requirements.txt`**: Lista de dependências necessárias para o projeto.
- **`.gitignore`**: Arquivo para ignorar arquivos e diretórios desnecessários no controle de versão.
- **`LICENSE`**: Arquivo contendo a licença do projeto.

## Requisitos de Instalação

Certifique-se de ter as seguintes ferramentas instaladas:

- Python >= 3.8
- Gerenciador de pacotes `pip`
- Docker (opcional, para execução com contêineres).
- Virtualenv (para criar ambientes isolados de Python, opcional).
- Acesso às chaves de API para os bancos de dados utilizados (dbSNP, ClinVar, Ensembl).

## Instalação

1. Clone o repositório:

   ```bash
   git clone https://github.com/madsondeluna/getvar_mvp.git
   cd getvar_mvp
   ```

2. Crie um ambiente virtual (opcional, mas é recomendado):

   ```bash
   python3 -m venv venv
   source venv/bin/activate
   ```

3. Instale as dependências:

   ```bash
   pip install -r requirements.txt
   ```

4. Instale o Snakemake:

   ```bash
   pip install snakemake
   ```

## Configuração do Arquivo `.env`

O arquivo `.env` é utilizado para configurar variáveis de ambiente necessárias para o funcionamento da aplicação. Crie um arquivo `.env` na raiz do projeto com o seguinte conteúdo de exemplo:

```
FLASK_ENV=production
SNAKEMAKE_THREADS=4
DBSNP_API_KEY=your_dbsnp_api_key
CLINVAR_API_KEY=your_clinvar_api_key
ENSEMBL_API_KEY=your_ensembl_api_key
```

- **`FLASK_ENV`**: Define o ambiente de execução (ex.: `development`, `production`).
- **`SNAKEMAKE_THREADS`**: Quantidade de threads utilizadas pelo Snakemake.
- **`DBSNP_API_KEY`**, **`CLINVAR_API_KEY`**, **`ENSEMBL_API_KEY`**: Chaves de acesso para integração com os respectivos bancos de dados.

## Execução com Docker

O projeto inclui um `Dockerfile` configurado para facilitar a execução. Siga as etapas abaixo:

### 1. Construir a Imagem

```bash
docker build -t getvar_mvp .
```

### 2. Executar o Container

```bash
docker run -d -p 5000:5000 --env-file .env --name getvar_mvp_container getvar_mvp
```

### Detalhes do Comando:
- **`-d`**: Executa o container em modo "detached" (em segundo plano).
- **`-p 5000:5000`**: Mapeia a porta 5000 do container para a porta 5000 do host.
- **`--env-file .env`**: Passa variáveis de ambiente definidas no arquivo `.env`.
- **`--name getvar_mvp_container`**: Nomeia o container como `getvar_mvp_container`.

### 3. Verificar Logs

```bash
docker logs getvar_mvp_container
```

### 4. Testar a Aplicação

Acesse a aplicação no navegador em:

```
http://localhost:5000
```

### 5. Gerenciar o Container

#### Parar o Container:

```bash
docker stop getvar_mvp_container
```

#### Reiniciar o Container:

```bash
docker start getvar_mvp_container
```

#### Remover o Container:

```bash
docker rm getvar_mvp_container
```

## Contribuição

Contribuições são bem-vindas! Siga as etapas abaixo para contribuir com o projeto:

1. **Fork do Repositório**:
   Crie um fork do repositório em sua conta do GitHub.

2. **Clone o Repositório**:
   ```bash
   git clone https://github.com/sua-conta/getvar_mvp.git
   cd getvar_mvp
   ```

3. **Crie uma Nova Branch**:
   ```bash
   git checkout -b minha-contribuicao
   ```

4. **Implemente as Alterações**:
   Realize as modificações desejadas no código.

5. **Faça o Commit das Alterações**:
   ```bash
   git add .
   git commit -m "Descrição das alterações"
   ```

6. **Envie as Alterações para o seu Fork**:
   ```bash
   git push origin minha-contribuicao
   ```

7. **Abra um Pull Request**:
   Acesse o repositório original no GitHub e abra um Pull Request com suas alterações.

## Exemplo de Uso

Submeta um arquivo **VCF** através da interface web. O sistema processará os dados, realizará as anotações e disponibilizará um relatório final em formato tabular que pode ser filtrado através das respectivas anotações. 

## Informações Adicionais de Uso

As APIs REST do dbSNP, ClinVar e Ensembl possuem um limite de até 30 requisições por solicitação. Por isso, a aplicação pode apresentar instabilidade ou lentidão em alguns momentos. Além disso, os servidores dessas plataformas ocasionalmente podem ficar instáveis ou não responder adequadamente às requisições. Nesses casos, o manual das APIs recomenda a resubmissão dos dados para completar o processo de anotação.

## Licença

Este projeto está licenciado sob a [Licença MIT](https://opensource.org/licenses/MIT). Consulte o arquivo LICENSE para mais informações.

## Contato

Madson Aragão\
[madsondeluna@gmail.com](mailto:madsondeluna@gmail.com)\
[LinkedIn](https://www.linkedin.com/in/madsonaragao)

🌟 <i>Created by Madson Aragão in somewhere, where bytes and biomolecules collide.</i>

