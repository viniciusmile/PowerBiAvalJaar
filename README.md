Aqui está uma sugestão de README profissional e bem estruturado para o seu repositório GitHub, destacando os pontos que você mencionou: o esforço analítico, a complexidade das medidas DAX e a replicação do front-end.

Basta copiar e colar o texto abaixo no seu arquivo `README.md`.

-----

# 🚀 Projeto Power BI: Avaliação Analista de BI Junior (Jaar Consult)

Este repositório documenta o desenvolvimento de um projeto de Business Intelligence em Power BI, realizado como parte do processo seletivo para a vaga de Analista de BI Junior na Jaar Consult.

O projeto demonstra habilidades em modelagem de dados, criação de medidas DAX complexas e design de dashboards, transformando dados brutos em insights acionáveis.

## 🎯 Objetivo do Desafio

O desafio consistiu em analisar um conjunto de dados de vendas (extraído do banco de dados `AdventureWorks`), desenvolver um modelo de dados performático e criar um relatório completo que atendesse a diversos requisitos analíticos.

Um dos principais destaques deste projeto foi a **replicação "de olho" de um layout de dashboard** (página `Front`) a partir de uma imagem estática, exigindo atenção minuciosa aos detalhes de UI/UX, alinhamento, cores e formatação.

## 📊 Principais Análises e Funcionalidades

O relatório é composto por diversas páginas, cada uma focada em um aspecto diferente da análise de performance de vendas:

  * **Visão Geral (Front-end):** Um dashboard consolidado com KPIs principais (Vendas Brutas, Lucro, Margem), análise de performance de vendas (vs. Meta e vs. Ano Anterior) e visões geográficas e de categoria.
  * **Análise de Vendas e Custo:** Gráfico de linhas detalhado comparando a evolução das Vendas Brutas e do Custo Total ao longo do tempo.
  * **Performance Geográfica e Promocional:** Análise de Vendas Brutas por País e Retorno por Tipo de Promoção.
  * **Análise de Margem:** Visão de rentabilidade por Continente e País utilizando *treemaps*.
  * **Time Intelligence:** Relatório tabular detalhado com cálculos de inteligência de tempo, incluindo:
      * Vendas Brutas LY (Last Year)
      * Vendas Brutas YTD (Year-to-Date)
      * Variação % vs. LY
  * **Análise de Share (%):** Tabelas demonstrando a participação percentual (share) das vendas sob diferentes contextos, validando as medidas DAX criadas.

## ⚙️ Destaques Técnicos: Medidas DAX

A complexidade deste projeto reside na criação de medidas DAX robustas para responder a perguntas de negócio específicas. As principais medidas desenvolvidas incluem:

### 1\. Medidas de Time Intelligence

Medidas essenciais para comparar a performance atual com períodos anteriores, como:

```dax
Vendas Brutas LY = 
CALCULATE(
    [Vendas Brutas],
    SAMEPERIODLASTYEAR('dCalendario'[Data])
)
```

```dax
Vendas Brutas YTD = 
TOTALYTD(
    [Vendas Brutas],
    'dCalendario'[Data]
)
```

### 2\. Medidas de Share (Participação Percentual)

Foram criadas três medidas de *share* com lógicas de contexto distintas para demonstrar profundo entendimento das funções `CALCULATE`, `ALL`, `ALLEXCEPT` e `VALUES`.

  * **[% Share vendas brutas Categoria Produtos]:**

      * **Objetivo:** Calcular o % de vendas da categoria em relação ao total, **ignorando filtros externos** aplicados à categoria, mas mantendo o contexto da linha.
      * **Fórmula DAX:**

    <!-- end list -->

    ```dax
    % Share vendas brutas Categoria Produtos = 
    DIVIDE(
        [Vendas Brutas],
        CALCULATE(
            [Vendas Brutas],
            ALL('dCategoriaProdutos'),
            VALUES('dCategoriaProdutos'[Categoria]) 
        )
    )
    ```

  * **[% Share vendas brutas Genérico]:**

      * **Objetivo:** Calcular o % de vendas da linha em relação ao **total geral**, independente de qualquer filtro aplicado no relatório (ano, mês, categoria, etc.).
      * **Fórmula DAX:**

    <!-- end list -->

    ```dax
    % Share vendas brutas Genérico = 
    DIVIDE(
        [Vendas Brutas],
        CALCULATE(
            [Vendas Brutas],
            ALL('fVendas') // Remove todo o contexto de filtro da tabela fato
        )
    )
    ```

  * **[% Share vendas brutas Agrupável]:**

      * **Objetivo:** Calcular o % de share por Continente e Categoria, totalizando 100% no nível selecionado.
      * **Fórmula DAX:**

    <!-- end list -->

    ```dax
    % Share vendas brutas Agrupável = 
    DIVIDE(
        [Vendas Brutas],
        CALCULATE(
            [Vendas Brutas],
            ALLEXCEPT(
                'dLocalidades',
                'dLocalidades'[Continente] // Mantém apenas o filtro de continente
            )
        )
    )
    ```

## 🎨 Desafio de Front-end

A página `Front` do relatório não foi construída de forma livre. Ela é uma **replicação fiel, baseada em uma única imagem de referência**. Este exercício demonstra competências em:

  * **Design de Dashboard:** Escolha e formatação correta de visuais (KPIs, gráficos de barra, *treemaps*, slicers).
  * **Atenção ao Detalhe (Pixel-Perfect):** Cuidado com alinhamento, espaçamento, tamanhos de fonte e paleta de cores.
  * **UX (User Experience):** Disposição lógica dos elementos para facilitar a leitura e a interação do usuário.

## 🗂️ Estrutura do Repositório

Este repositório utiliza o formato de projeto Power BI (`.pbip`), que salva o relatório e o modelo de dados em pastas separadas, facilitando o versionamento com o Git.

  * `Avaliação PBI JR - VINICIUS MOREIRA.Report/`: Contém os arquivos JSON que definem o layout do relatório, visuais e configurações.
  * `Avaliação PBI JR - VINICIUS MOREIRA.SemanticModel/`: Contém os arquivos que definem o modelo de dados, relacionamentos e as medidas DAX.
  * `Avaliação PBI JR - VINICIUS MOREIRA.pbip`: O arquivo principal do projeto a ser aberto no Power BI Desktop.

## 🚀 Como Visualizar

1.  Clone este repositório.
2.  Certifique-se de ter a versão mais recente do [Power BI Desktop](https://powerbi.microsoft.com/pt-br/desktop/) instalada (com suporte a arquivos `.pbip`).
3.  Abra o arquivo `Avaliação PBI JR - VINICIUS MOREIRA.pbip`.
4.  Explore as diferentes páginas do relatório.

-----

**Autor:** Vinicius Moreira
