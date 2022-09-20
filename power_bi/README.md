# Power BI
> https://powerbi.microsoft.com

## Download Oracle Client from Power BI dependence
https://docs.microsoft.com/zh-tw/power-bi/connect-data/desktop-connect-oracle-database

#### 32-bit:
https://www.oracle.com/database/technologies/dotnet-utilsoft-downloads.html

#### 64-bit
https://www.oracle.com/database/technologies/odac-downloads.html



## Comparing Power BI Report Server and the Power BI service
> https://docs.microsoft.com/en-us/power-bi/report-server/compare-report-server-service

## Embed
> https://docs.microsoft.com/zh-tw/power-bi/report-server/quickstart-embed

URL帶入參數: rs:embed=true
```
https://myserver/reports/powerbi/Sales?rs:embed=true

// with password
https://username:Password@myserver/reports/powerbi/Sales?rs:embed=true

<iframe width="800" height="600" src="https://myserver/reports/powerbi/Sales?rs:embed=true" frameborder="0" allowFullScreen="true"></iframe>
```

#### Tags
```
<iframe>

<object data="https://myserver/reports/powerbi/Sales?rs:embed=true"></object>

<embed src="http://win-hauseq7hanj:82/Reports/powerbi/bb?rs:embed=true" />

```


## Download for using Microsoft Cloud service
** Power BI Desktop **
> https://powerbi.microsoft.com/zh-tw/desktop/

## Downloads for Power BI Report Server
1, POWER BI Report Server

2, POWER BI Desktop for report Server
> https://www.microsoft.com/en-us/download/details.aspx?id=56722

3, SQL server 2019，developer version
> https://www.microsoft.com/zh-tw/sql-server/sql-server-downloads

4, SSMS - DB management Tool (option)
> https://docs.microsoft.com/zh-tw/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-ver15


## Switch Import-data to directQuery
> https://xxlbi.com/blog/switching-from-imported-data-to-directquery-or-live-connection-in-power-bi/

## Go to detail when click a bar in chart
> https://docs.microsoft.com/en-us/power-bi/create-reports/desktop-see-data-see-records

## DAX
> https://medium.com/mastertalks-tw/%E4%BD%BF%E7%94%A8-power-bi-%E4%B8%80%E5%AE%9A%E8%A6%81%E6%87%82%E5%BE%97-dax-%E5%87%BD%E6%95%B8-%E7%9C%8B%E5%AE%8C%E9%80%99%E7%AF%87%E7%AB%8B%E5%8D%B3%E4%B8%8A%E6%89%8B-1206283eed6f


## Like VLOOKUP in power bi
### 1, RELATED
> https://community.powerbi.com/t5/Community-Blog/Good-Ol-VLOOKUP-The-Ultimate-Guide-to-Lookups-in-Power-BI/ba-p/35912

### 2, LOOKUPVALUE
> https://docs.microsoft.com/en-us/dax/lookupvalue-function-dax

> https://exceltown.com/en/tutorials/power-bi/powerbi-com-and-power-bi-desktop/dax-query-language-for-power-bi-and-power-pivot/lookupvalue-assigning-of-values-from-other-table-dax-power-pivot-power-bi/

```
LOOKUPVALUE(
    <result_columnName>,
    <search_columnName>,
    <search_value>
    [, <search2_columnName>, <search2_value>]…
    [, <alternateResult>]
)
```

```
[Region] = LOOKUPVALUE(Employee[Region], Employee[Email], USERNAME(), BLANK())

Product = LOOKUPVALUE('Product'[Product], Sales[ProductKey], 'Product'[ProductKey])

Product = RELATED('Product'[Product])
```


## 3, ROLLING 12 MONTH
> DEFAULT VALUE ALSO USING CALCULATE

```
VALUE_1 =
CALCULATE (
    SUMX (
        TableName,
        TableName[Column Name]
    )
)

ROLLING_12_MONTH =
CALCULATE(
    [VALUE_1],
    FILTER (
        ALL(Dates),
        AND (
            Dates[Date] <= MAX( Dates[Date] ),
            DATEADD (
                Dates[Date],
                1,
                YEAR
            )  > MAX ( Dates[Date] )
        )
    )
)
```

## 4, CONVERT IMPORT MODE TO DIRECT QUERY
> https://datacaffee.com/convert-import-mode-to-direct-query-in-power-bi/


## 5, Dynamic Top N
```
THE_TOP_VALUES =
VAR SELECTED_TOP = SELECTEDVALUE('TOP_VALUES'[TOP_VALUE])
RETURN
SWITCH(TRUE(),
    SELECTED_TOP = 0, [MEANSURE_VALUE],
    RANKX (
            ALLSELECTED(  'TABLES'[COLUMN_NAME] ),
            [MEANSURE_VALUE]
                )
                  <= SELECTED_TOP,
        [MEANSURE_VALUE]
)
```

## 6. Convert import mode to direct query mode
1. Create empty file and setup tables in direct query mode. This file named 'A'.
2. Copy the import mode file and named 'B'.
3. Change extend name of A and B to '.zip'.
4. Remove DataMashup and DataModel files in B. And then copy DataMashup and DataModel from A to B.
5. rename extend name of B to '.pbix'
6. Open B.pbix and rebuild meansures and loss somethings.

## 7. Rank top
```
meansure =
VAR RankResult = RANKX(ALL(table_name), [value], , desc)
return
IF(RankResult < 10, table_name[column_name], "other")
```

## 8. Using Drill Through Buttons to Replace Right-Click Navigation
> https://blog.pragmaticworks.com/using-drill-through-buttons-to-replace-right-click-navigation-in-power-bi

```
StringForDemoButton = If(SELECTEDVALUE(DimKey[CorporateGroup], 0) == 0, “See Demo Details”, “See customer loss details for ” & SELECTEDVALUE(Dimkey[CorporateGroup]))

Button text is function and set value as StringForDemoButton

Button Action:

Type: Drill through (Preview or not)

Destination: Customer Losses (your column)

Enabled tooltip Go to Customer Losses……
```

## 9. dynamic table value
> https://www.nathanprats.com/4-different-ways-to-dynamically-change-tables-rows-in-power-bi/

```
UNION group date:

Tool -SlicerTable =
	VAR ProductCategory =
		CROSSJOIN(
			ROW(“Type”, “ProductCategoy)”,
			VALUES ( DimProductCategory[EnglishProducts'])
		)
	VAR ProductsSubCategory =
		CROSSJOIN(
			ROW(“Type”, “ProductSubCategoy)”,
			VALUES ( DimProductSubCategory[EnglishProductSubcategoryName])
		)
	VAR SalesTerritoryGroup =
		CROSSJOIN(
			ROW(“Type”, “SalesTerritoryGroup)”,
			VALUES ( DimSalesTerritory[SalesTerritoryGroup])
		)
	VAR ProductsSubCategory =
		CROSSJOIN(
			ROW(“Type”, “SalesTerritoryRegion)”,
			VALUES ( DimSalesTerritory[SalesTerritoryRegion])
		)
	VAR ProductsSubCategory =
		CROSSJOIN(
			ROW(“Type”, “SalesTerritoryCountry)”,
			VALUES ( DimSalesTerritory[SalesTerritoryCountry])
		)

RETURN
	UNION (
		ProductCategory,
		ProductSubCategory,
		SalesTerritoryGroup,
		SalesTerritoryRegion,
		SalesTerritoryCountry
	)


Measure:
SumSalesAmount (Dynamic Slicer) =

IF (
	HASCONEVALUE ( ’Tool - SlicerTable’[Type] ),
	SWITCH (
		VALUES ( ’Tool - SlicerTable’[Type]),

		“ProductCategory”, CALCULATE (
			[SumSalesAmount],
			TREATAS ( VALUES ( ’Tool - SlicerTable’[Values] ), DimProductCategory[EnglishProductCategoryName] )
		),
		“ProductSubCategory”, CALCULATE (
			[SumSalesAmount],
			TREATAS ( VALUES ( ’Tool - SlicerTable’[Values] ), DimProductCategory[EnglishProductSubcategoryName] )
		),
		“SalesTerritoryGroup”, CALCULATE (
			[SumSalesAmount],
			TREATAS ( VALUES ( ’Tool - SlicerTable’[Values] ), DimSalesTerritory[SalesTerritoryGroup] )
		),
		“SalesTerritoryRegion”, CALCULATE (
			[SumSaleAmount],
			TREATAS ( VALUES ( ’Tool - SlicerTable’[Values] ), DimSalesTerritory[SalesTerritoryRegion] )
		),
		“SalesTerritoryCountry”, CALCULATE (
			[SumSalesAmount],
			TREATAS ( VALUES ( ’Tool -SlicerTable’[Values] ), DimSalesTerritory[SalesTerritoryCountry] )
		)
	)
)


```

## 10. rank category by count
```
RANK =
VAR _TMP_TABLE = SUMMARIZE(ALL(TABLE_A), TABLE_A[COLUMN_1], "_NEW_COUNT", COUNT(TABLE_A[COLUMN_1]))
RETURN MAXX(FILTER(_TMP_TABLE, [COLUMN_1] = SELECTEDALUE(TABLE_A[COLUMN_1])), RANKX(_TMP_TABLE, [_NEW_COUNT]))

```
```
RANK =
VAR _CURRENT_COUNT = [count_b]
RETURN CALCULATE(
    RANKX(
        VALUES(TABLE_A[COLUMN_1]),
        CALCULATE(
            COUNT(TABLE_A[COLUMN_1])
        ),
        _CURRENT_COUNT,
        DESC
    ),
    ALLSELECTED(TABLE_A)
)

```

## countrow Row Number
```
Row_Number =
CALCULATE (
    COUNTROWS(Profit_Table),
    FILTER ( ALLSELECTED ( Profit_Table ), Profit_Table[Position] <= MAX ( Profit_Table[Position]) )
)
```
