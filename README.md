
<div align="center">
   <img height="30" width="40" src="https://github.com/hipolitorodrigues/assets-for-github/blob/985021e61af3982fd9f28be446b106b958f24696/images/01/img-readme-ico.svg">
   <a href="./README.md">
      <img height="30" width="120" src="https://github.com/hipolitorodrigues/assets-for-github/blob/985021e61af3982fd9f28be446b106b958f24696/images/01/img-readme-en.svg">
   </a>
   <a href="./README.pt-BR.md">
      <img height="30" width="60" src="https://github.com/hipolitorodrigues/assets-for-github/blob/985021e61af3982fd9f28be446b106b958f24696/images/01/img-readme-pt-br.svg">
   </a>
</div>

# Progressive Guide to DAX Fundamentals

This guide is aimed at those who already have experience with other programming or query languages but are beginners in DAX. The goal is to progressively become familiar with the syntax and core concepts of the language used in Power BI, Excel, and Analysis Services.

## 1. Introduction to DAX

### 1.1 What is DAX?
- **DAX (Data Analysis Expressions)** is a functional language used for data modeling and calculations in Power BI, Excel, and SQL Server Analysis Services (SSAS).
- It enables the creation of **calculated columns, measures, and tables**.

### 1.2 Basic Syntax
- DAX expressions use functions, operators, and values similar to Excel formulas.
- Example of a simple measure:

```DAX
Total Sales = SUM(Sales[Amount])
```

## 2. Data Types in DAX

### 2.1 Common Data Types
- **Whole Number (Integer)**
- **Decimal Number (Floating Point)**
- **Boolean (TRUE/FALSE)**
- **String (Text)**
- **Date/Time**

### 2.2 Implicit vs Explicit Data Types
- DAX automatically converts data types when necessary.
- Explicit conversions can be done using functions like `CONVERT`.

```DAX
Converted Value = CONVERT('Table'[Column], STRING)
```

## 3. Basic Functions

### 3.1 Aggregation Functions
- `SUM`, `AVERAGE`, `MIN`, `MAX`, `COUNT`

```DAX
Total Quantity = SUM(Sales[Quantity])
Average Price = AVERAGE(Sales[Price])
```

### 3.2 Logical Functions
- `IF`, `SWITCH`, `AND`, `OR`, `NOT`

```DAX
Discount Applied = IF(Sales[Amount] > 1000, "Yes", "No")
```

### 3.3 Text Functions
- `LEFT`, `RIGHT`, `MID`, `LEN`, `CONCATENATE`, `SEARCH`

```DAX
Full Name = Sales[First Name] & " " & Sales[Last Name]
```

## 4. Working with Dates

### 4.1 Date Functions
- `TODAY`, `NOW`, `YEAR`, `MONTH`, `DAY`

```DAX
Current Year = YEAR(TODAY())
```

### 4.2 Time Intelligence Functions
- `TOTALYTD`, `TOTALQTD`, `SAMEPERIODLASTYEAR`, `DATESYTD`

```DAX
Sales YTD = TOTALYTD(SUM(Sales[Amount]), Sales[Date])
```

## 5. Row Context vs Filter Context

### 5.1 Understanding Contexts
- **Row Context**: Evaluates expressions **row by row** in a table.
- **Filter Context**: Filters applied by slicers, rows, or filters in a report.

### 5.2 CALCULATE Function
- Modifies the filter context to apply different conditions.

```DAX
Sales 2023 = CALCULATE(SUM(Sales[Amount]), YEAR(Sales[Date]) = 2023)
```

## 6. Iterator Functions

### 6.1 Using Iterators
- Functions that operate **row by row**: `SUMX`, `AVERAGEX`, `MAXX`, `MINX`

```DAX
Total Revenue = SUMX(Sales, Sales[Quantity] * Sales[Price])
```

## 7. Advanced Filtering and Relationships

### 7.1 RELATED and RELATEDTABLE
- Used to reference data from related tables.

```DAX
Category Name = RELATED(Category[Category Name])
```

### 7.2 USERELATIONSHIP
- Allows activating an inactive relationship.

```DAX
Alternate Sales = CALCULATE(SUM(Sales[Amount]), USERELATIONSHIP(Sales[Date], Calendar[Date]))
```

## 8. Performance Optimization

### 8.1 Best Practices
- Use **measures** instead of **calculated columns** where possible.
- Avoid unnecessary **iterator functions**.
- Minimize **cardinality** in relationships to improve performance.

## 9. Common Use Cases

### 9.1 Running Totals
```DAX
Running Total = CALCULATE(SUM(Sales[Amount]), FILTER(ALL(Sales[Date]), Sales[Date] <= MAX(Sales[Date])))
```

### 9.2 Dynamic Rankings
```DAX
Sales Rank = RANKX(ALL(Sales), SUM(Sales[Amount]), , DESC, DENSE)
```

### 9.3 Year-over-Year Growth
```DAX
YoY Growth = ([Total Sales] - [Sales LY]) / [Sales LY]
```

---
This guide provides a structured introduction to the fundamental concepts of DAX. As you progress, explore more advanced topics like **calculation groups**, **variables**, and **optimizing DAX queries** for performance. 🚀
