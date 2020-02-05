---
title: OPTION 子句 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- OPTION clause
- OPTION_TSQL
- OPTION
- OPTION_clause_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- clauses [SQL Server], OPTION
- OPTION clause
ms.assetid: f47e2f3f-9302-4711-9d66-16b1a2a7ffe3
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a1266097e82f5db84f5a91951adc784d6d9580ef
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "67901847"
---
# <a name="option-clause-transact-sql"></a>OPTION 子句 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  指定所指出的查詢提示應該用於整個查詢。 雖然可以有多個查詢提示，不過每個查詢提示只能指定一次。 只有一個 OPTION 子句可以利用陳述式加以指定。  
  
 這個子句可以在 SELECT、DELETE、UPDATE 和 MERGE 陳述式中指定。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
[ OPTION ( <query_hint> [ ,...n ] ) ]   
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
OPTION ( <query_option> [ ,...n ] )  
  
<query_option> ::=  
    LABEL = label_name |  
    <query_hint>  
  
<query_hint> ::=  
    HASH JOIN   
    | LOOP JOIN   
    | MERGE JOIN  
    | FORCE ORDER  
    | { FORCE | DISABLE } EXTERNALPUSHDOWN  
```  
  
## <a name="arguments"></a>引數  
 *query_hint*  
 關鍵字，它們會指出要使用哪一個最佳化工具提示來自訂 Database Engine 處理陳述式的方式。 如需詳細資訊，請參閱[查詢提示 &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md)。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-an-option-clause-with-a-group-by-clause"></a>A. 搭配 GROUP BY 子句使用 OPTION 子句  
 下列範例會顯示如何搭配 `OPTION` 子句來使用 `GROUP BY` 子句。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductID, OrderQty, SUM(LineTotal) AS Total  
FROM Sales.SalesOrderDetail  
WHERE UnitPrice < $5.00  
GROUP BY ProductID, OrderQty  
ORDER BY ProductID, OrderQty  
OPTION (HASH GROUP, FAST 10);  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-select-statement-with-a-label-in-the-option-clause"></a>B. OPTION 子句中含有標籤的 SELECT 陳述式  
 下列範例示範一個 OPTION 子句中含有標籤的簡單 [!INCLUDE[ssDW](../../includes/ssdw-md.md)] SELECT 陳述式。  
  
```  
-- Uses AdventureWorks  
  
SELECT * FROM FactResellerSales  
  OPTION ( LABEL = 'q17' );  
```  
  
### <a name="c-select-statement-with-a-query-hint-in-the-option-clause"></a>C. OPTION 子句中含有查詢提示的 SELECT 陳述式  
 下列範例示範一個在 OPTION 子句中使用 HASH JOIN 查詢提示的 SELECT 陳述式。  
  
```  
-- Uses AdventureWorks  
  
SELECT COUNT (*) FROM dbo.DimCustomer a  
INNER JOIN dbo.FactInternetSales b   
ON (a.CustomerKey = b.CustomerKey)  
OPTION (HASH JOIN);  
```  
  
### <a name="d-select-statement-with-a-label-and-multiple-query-hints-in-the-option-clause"></a>D. OPTION 子句中含有一個標籤和多個查詢提示的 SELECT 陳述式  
 下列範例是一個包含一個標籤和多個查詢提示的 [!INCLUDE[ssDW](../../includes/ssdw-md.md)] SELECT 陳述式。 在計算節點上執行此查詢時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會根據 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所決定的最佳策略，套用雜湊聯結或合併聯結。  
  
```  
-- Uses AdventureWorks  
  
SELECT COUNT (*) FROM dbo.DimCustomer a  
INNER JOIN dbo.FactInternetSales b   
ON (a.CustomerKey = b.CustomerKey)  
OPTION ( Label = 'CustJoin', HASH JOIN, MERGE JOIN);  
```  
  
### <a name="e-using-a-query-hint-when-querying-a-view"></a>E. 在查詢檢視表時使用查詢提示  
 下列範例會建立一個名為 CustomerView 的檢視表，然後在參考檢視表和資料表的查詢中使用 HASH JOIN 查詢提示。  
  
```  
-- Uses AdventureWorks  
  
CREATE VIEW CustomerView  
AS  
SELECT CustomerKey, FirstName, LastName FROM ssawPDW..DimCustomer;  
  
SELECT COUNT (*) FROM dbo.CustomerView a  
INNER JOIN dbo.FactInternetSales b  
ON (a.CustomerKey = b.CustomerKey)  
OPTION (HASH JOIN);  
  
DROP VIEW CustomerView;  
  
```  
  
### <a name="f-query-with-a-subselect-and-a-query-hint"></a>F. 含有子選擇和查詢提示的查詢  
 下列範例示範一個同時包含子選擇和查詢提示的查詢。 查詢提示會在全域套用。 不允許將查詢提示附加至子選擇陳述式。  
  
```  
-- Uses AdventureWorks  
  
CREATE VIEW CustomerView AS  
SELECT CustomerKey, FirstName, LastName FROM ssawPDW..DimCustomer;  
  
SELECT * FROM (  
SELECT COUNT (*) AS a FROM dbo.CustomerView a  
INNER JOIN dbo.FactInternetSales b  
ON ( a.CustomerKey = b.CustomerKey )) AS t  
OPTION (HASH JOIN);  
```  
  
### <a name="g-force-the-join-order-to-match-the-order-in-the-query"></a>G. 強制聯結順序與查詢中的順序相符  
 下列範例會使用 FORCE ORDER 提示，以強制查詢計劃使用查詢所指定的聯結順序。 這可改善某些查詢的效能；但並非所有查詢。  
  
```  
-- Uses AdventureWorks  
  
-- Obtain partition numbers, boundary values, boundary value types, and rows per boundary  
-- for the partitions in the ProspectiveBuyer table of the ssawPDW database.  
SELECT sp.partition_number, prv.value AS boundary_value, lower(sty.name) AS boundary_value_type, sp.rows   
FROM sys.tables st JOIN sys.indexes si ON st.object_id = si.object_id AND si.index_id <2  
JOIN sys.partitions sp ON sp.object_id = st.object_id AND sp.index_id = si.index_id  
JOIN sys.partition_schemes ps ON ps.data_space_id = si.data_space_id   
JOIN sys.partition_range_values prv ON prv.function_id = ps.function_id   
JOIN sys.partition_parameters pp ON pp.function_id = ps.function_id   
JOIN sys.types sty ON sty.user_type_id = pp.user_type_id AND prv.boundary_id = sp.partition_number   
WHERE st.object_id = (SELECT object_id FROM sys.objects WHERE name = 'FactResellerSales')   
ORDER BY sp.partition_number  
OPTION ( FORCE ORDER )  
;  
```  
  
### <a name="h-using-externalpushdown"></a>H. 使用 EXTERNALPUSHDOWN  
 下列範例會強制將 WHERE 子句下推至外部 Hadoop 資料表上的 MapReduce 作業。  
  
```  
SELECT ID FROM External_Table_AS A   
WHERE ID < 1000000  
OPTION (FORCE EXTERNALPUSHDOWN);  
```  
  
 下列範例會防止將 WHERE 子句下推至外部 Hadoop 資料表上的 MapReduce 作業。 所有資料列都會傳回給套用 WHERE 子句的 PDW。  
  
```  
SELECT ID FROM External_Table_AS A   
WHERE ID < 10  
OPTION (DISABLE EXTERNALPUSHDOWN);  
```  
  
## <a name="see-also"></a>另請參閱  
 [提示 &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)   
 [MERGE &#40;Transact-SQL&#41;](../../t-sql/statements/merge-transact-sql.md)   
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)  
  
  

