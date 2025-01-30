<div align="center">
   <img height="30" width="40" src="https://github.com/hipolitorodrigues/assets-for-github/blob/985021e61af3982fd9f28be446b106b958f24696/images/01/img-readme-ico.svg">
   <a href="./README.md">
      <img height="30" width="120" src="https://github.com/hipolitorodrigues/assets-for-github/blob/985021e61af3982fd9f28be446b106b958f24696/images/01/img-readme-en.svg">
   </a>
   <a href="./README.pt-BR.md">
      <img height="30" width="60" src="https://github.com/hipolitorodrigues/assets-for-github/blob/985021e61af3982fd9f28be446b106b958f24696/images/01/img-readme-pt-br.svg">
   </a>
</div>

# Guia Progressivo de Fundamentos do DAX

Este guia é destinado a aqueles que já possuem experiência com outras linguagens de programação ou consulta, mas são iniciantes em DAX. O objetivo é se familiarizar progressivamente com a sintaxe e os conceitos fundamentais da linguagem usada no Power BI, Excel e Analysis Services.

## 1. Introdução ao DAX

### 1.1 O que é DAX?
- **DAX (Data Analysis Expressions)** é uma linguagem funcional utilizada para modelagem de dados e cálculos no Power BI, Excel e SQL Server Analysis Services (SSAS).
- Permite a criação de **colunas calculadas, medidas e tabelas**.

### 1.2 Sintaxe Básica
- Expressões DAX utilizam funções, operadores e valores semelhantes às fórmulas do Excel.
- Exemplo de uma medida simples:

```DAX
Total Vendas = SUM(Vendas[Valor])
```

## 2. Tipos de Dados no DAX

### 2.1 Tipos de Dados Comuns
- **Número Inteiro**
- **Número Decimal (Ponto Flutuante)**
- **Booleano (VERDADEIRO/FALSO)**
- **Texto (String)**
- **Data/Hora**

### 2.2 Tipos Implícitos vs Explícitos
- O DAX converte automaticamente os tipos de dados quando necessário.
- Conversões explícitas podem ser feitas usando funções como `CONVERT`.

```DAX
Valor Convertido = CONVERT('Tabela'[Coluna], STRING)
```

## 3. Funções Básicas

### 3.1 Funções de Agregação
- `SUM`, `AVERAGE`, `MIN`, `MAX`, `COUNT`

```DAX
Quantidade Total = SUM(Vendas[Quantidade])
Preço Médio = AVERAGE(Vendas[Preço])
```

### 3.2 Funções Lógicas
- `IF`, `SWITCH`, `AND`, `OR`, `NOT`

```DAX
Desconto Aplicado = IF(Vendas[Valor] > 1000, "Sim", "Não")
```

### 3.3 Funções de Texto
- `LEFT`, `RIGHT`, `MID`, `LEN`, `CONCATENATE`, `SEARCH`

```DAX
Nome Completo = Vendas[Primeiro Nome] & " " & Vendas[Sobrenome]
```

## 4. Trabalhando com Datas

### 4.1 Funções de Data
- `TODAY`, `NOW`, `YEAR`, `MONTH`, `DAY`

```DAX
Ano Atual = YEAR(TODAY())
```

### 4.2 Funções de Inteligência de Tempo
- `TOTALYTD`, `TOTALQTD`, `SAMEPERIODLASTYEAR`, `DATESYTD`

```DAX
Vendas YTD = TOTALYTD(SUM(Vendas[Valor]), Vendas[Data])
```

## 5. Contexto de Linha vs Contexto de Filtro

### 5.1 Entendendo os Contextos
- **Contexto de Linha**: Avalia expressões **linha por linha** em uma tabela.
- **Contexto de Filtro**: Filtros aplicados por segmentações, linhas ou filtros em um relatório.

### 5.2 Função CALCULATE
- Modifica o contexto de filtro para aplicar diferentes condições.

```DAX
Vendas 2023 = CALCULATE(SUM(Vendas[Valor]), YEAR(Vendas[Data]) = 2023)
```

## 6. Funções Iteradoras

### 6.1 Utilizando Iteradores
- Funções que operam **linha por linha**: `SUMX`, `AVERAGEX`, `MAXX`, `MINX`

```DAX
Receita Total = SUMX(Vendas, Vendas[Quantidade] * Vendas[Preço])
```

## 7. Filtragem Avançada e Relacionamentos

### 7.1 RELATED e RELATEDTABLE
- Utilizadas para referenciar dados de tabelas relacionadas.

```DAX
Nome da Categoria = RELATED(Categoria[Nome da Categoria])
```

### 7.2 USERELATIONSHIP
- Permite ativar um relacionamento inativo.

```DAX
Vendas Alternativas = CALCULATE(SUM(Vendas[Valor]), USERELATIONSHIP(Vendas[Data], Calendario[Data]))
```

## 8. Otimização de Desempenho

### 8.1 Melhores Práticas
- Utilize **medidas** em vez de **colunas calculadas** sempre que possível.
- Evite funções **iteradoras** desnecessárias.
- Minimize a **cardinalidade** nos relacionamentos para melhorar o desempenho.

## 9. Casos de Uso Comuns

### 9.1 Acumulados
```DAX
Acumulado = CALCULATE(SUM(Vendas[Valor]), FILTER(ALL(Vendas[Data]), Vendas[Data] <= MAX(Vendas[Data])))
```

### 9.2 Rankings Dinâmicos
```DAX
Ranking Vendas = RANKX(ALL(Vendas), SUM(Vendas[Valor]), , DESC, DENSE)
```

### 9.3 Crescimento Ano a Ano
```DAX
Crescimento YoY = ([Total Vendas] - [Vendas LY]) / [Vendas LY]
```

---
Este guia oferece uma introdução estruturada aos conceitos fundamentais do DAX. À medida que avança, explore tópicos mais avançados como **grupos de cálculo**, **variáveis** e **otimização de consultas DAX** para melhor desempenho. 🚀
