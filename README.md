# AI900-busca-cognitiva

# Explorar um Índice (UI) do Azure AI Search

## Descrição
Este projeto visa explorar o Azure AI Search para criar uma solução de mineração de conhecimento usando dados de avaliações de clientes da Fourth Coffee, uma rede nacional de cafés. O objetivo é facilitar a pesquisa de insights sobre as experiências do cliente ao criar um índice de pesquisa no Azure AI Search, enriquecendo os dados com habilidades de IA.

## Funcionalidades
- **Criação de Recursos do Azure:** Configuração dos serviços necessários para o Azure AI Search.
- **Extração e Enriquecimento de Dados:** Utilização de habilidades de IA para extrair e enriquecer dados a partir de avaliações de clientes.
- **Indexação e Consulta:** Uso do indexador do Azure para criar índices e realizar consultas eficientes.
- **Armazenamento de Conhecimento:** Salvamento de resultados enriquecidos para análise aprofundada.

---

## Pré-requisitos
- Conta no **Azure** com permissões para criar recursos.
- **Assinatura ativa** no Azure.
- Familiaridade com o **Portal do Azure**.

---

## Arquitetura

A solução utiliza os seguintes recursos do Azure:
1. **Azure AI Search:** Gerencia a indexação e a consulta dos dados.
2. **Serviços de IA do Azure:** Fornece as habilidades de IA para enriquecer os dados.
3. **Conta de Armazenamento do Azure:** Armazena documentos brutos e dados enriquecidos.

---

## Configuração do Ambiente

1. **Criar um Recurso do Azure AI Search:**
    - Vá para o Portal do Azure.
    - Clique em "+ Criar um recurso" e procure por **Azure AI Search**.
    - Configure com as seguintes opções:
      - **Tipo de Preço:** Básico
      - **Local:** Mesma região dos demais recursos
    - Selecione **Examinar + criar** e, em seguida, **Criar**.

2. **Criar um Recurso de Serviços de IA do Azure:**
    - Volte ao Portal do Azure e procure por **Serviços de IA do Azure**.
    - Selecione **Criar** e configure com:
      - **Tipo de Preço:** Standard S0
      - **Região:** Mesma região do AI Search
    - Selecione **Examinar + criar** e, em seguida, **Criar**.

3. **Criar uma Conta de Armazenamento:**
    - No Portal do Azure, clique em **+ Criar um recurso** e procure por **Conta de Armazenamento**.
    - Configure com:
      - **Redundância:** LRS (armazenamento com redundância local)
      - **Acesso anônimo ao Blob:** Habilitado
    - Selecione **Criar**.

---

## Carregamento de Dados

1. Faça o download do arquivo [coffee-reviews.zip](https://aka.ms/mslearn-coffee-reviews) e extraia os arquivos.
2. No **Portal do Azure**, acesse a **Conta de Armazenamento** criada.
3. Selecione **Contêineres** e crie um contêiner chamado **coffee-reviews** com acesso **Público**.
4. Faça o **upload** dos arquivos extraídos para o contêiner.

---

## Indexação e Enriquecimento

1. **Conectar ao Armazenamento e Indexar:**
    - No recurso **Azure AI Search**, selecione **Import data**.
    - Selecione **Azure Blob Storage** como fonte de dados.
    - Conecte ao contêiner **coffee-reviews**.
    - Selecione **Content and metadata** como dados a serem extraídos.

2. **Habilitar Habilidades de IA:**
    - Selecione **Enable OCR** e **merge all text into merged_content**.
    - Ative habilidades como:
      - **Extract location names**
      - **Extract key phrases**
      - **Detect sentiment**
      - **Generate tags from images**
      - **Generate captions from images**
    - Armazene os dados enriquecidos no **knowledge-store**.

3. **Configurar o Índice e Indexador:**
    - Defina o nome do índice como **coffee-index**.
    - Defina o nome do indexador como **coffee-indexer**.
    - Mantenha o **Base-64 Encode Keys** ativado.
    - Clique em **Submit** para criar o índice e iniciar o indexador.

---

## Consultando o Índice

Utilize o **Search Explorer** no Azure AI Search para consultar o índice.

- Para visualizar todos os documentos:
    ```json
    {
        "search": "*",
        "count": true
    }
    ```
- Para filtrar por local (ex: Chicago):
    ```json
    {
        "search": "locations:'Chicago'",
        "count": true
    }
    ```
- Para filtrar por sentimento (ex: Negativo):
    ```json
    {
        "search": "sentiment:'negative'",
        "count": true
    }
    ```

---

## Análise de Resultados

Os resultados das consultas são exibidos em formato JSON e incluem:
- **@odata.count:** Número total de documentos encontrados.
- **@search.score:** Relevância do resultado com base na consulta.
- **Campos enriquecidos:** Como `locations`, `keyphrases`, `sentiment`, etc.

---

## Armazenamento de Conhecimento

1. Navegue até a **Conta de Armazenamento** no Portal do Azure.
2. Acesse o **knowledge-store** criado durante a indexação.
3. Explore os arquivos JSON e imagens salvas com os dados enriquecidos.

---

## Limpeza e Exclusão de Recursos

Após concluir o exercício, exclua os recursos para evitar cobranças desnecessárias:
- Navegue até o **Portal do Azure**.
- Selecione o **Grupo de Recursos** criado.
- Clique em **Excluir Grupo de Recursos**.

---

## Tecnologias Utilizadas

- **Azure AI Search**
- **Serviços de IA do Azure**
- **Azure Blob Storage**
- **Habilidades de IA para enriquecimento de dados**
