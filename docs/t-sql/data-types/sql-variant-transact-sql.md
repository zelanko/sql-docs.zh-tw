---
title: "sql_variant (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 9/12/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sql_variant
- sql_variant_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sql_variant comparisons
- storing data [SQL Server], sql_variant
- sql_variant data type
- storage [SQL Server], sql_variant
ms.assetid: 01229779-8bc1-4c7d-890a-8246d4899250
caps.latest.revision: 43
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 6e754198cf82a7ba0752fe8f20c3780a8ac551d7
ms.openlocfilehash: 014cf6a2859bc60b4366418363681b1cd53dc5c6
ms.contentlocale: zh-tw
ms.lasthandoff: 09/14/2017

---
# <a name="sqlvariant-transact-sql"></a>sql_variant (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

儲存各種 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援之資料類型值的資料類型。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
sql_variant  
```  
  
## <a name="remarks"></a>備註  
**sql_variant**可用於資料行、 參數、 變數和使用者定義函數的傳回值。 **sql_variant**使這些資料庫物件，以支援其他資料類型的值。
  
類型的資料行**sql_variant**可能包含不同資料類型的資料列。 例如，資料行定義為**sql_variant**可以儲存**int**，**二進位**，和**char**值。
  
**sql_variant**可以有最大長度是 8016 位元組。 其中包括基底類型資訊和基底類型值。 實際基底類型值的最大長度是 8,000 位元組。
  
A **sql_variant**資料類型必須先轉換成其基底資料型別值之後，才能參與加法和減法之類的作業。
  
**sql_variant**可以指派預設值。 這項資料類型也可以用 NULL 作為基礎值，但 NULL 值並沒有相關的基底類型。 此外， **sql_variant**不能有另一個**sql_variant**作為其基底類型。
  
唯一、 主要或外部索引鍵可能包含類型的資料行**sql_variant**，但組成特定的資料列的索引鍵的資料值的總長度不可以是多個索引的最大長度。 這是 900 位元組。
  
資料表可以有任意數目的**sql_variant**資料行。
  
**sql_variant**不能在 CONTAINSTABLE 和 FREETEXTTABLE。
  
ODBC 不完全支援**sql_variant**。 因此，查詢的**sql_variant**當您使用 Microsoft OLE DB Provider for ODBC (MSDASQL) 時，將會傳回二進位資料的資料行。 例如， **sql_variant**行會以 0x505332303931 傳回包含 'PS2091' 的字元字串資料的資料行。
  
## <a name="comparing-sqlvariant-values"></a>比較 sql_variant 值  
**Sql_variant**資料類型屬於轉換的資料類型階層清單頂端。 如**sql_variant**比較，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料類型階層順序會分組為資料類型家族。
  
|資料類型階層|資料類型家族|  
|---|---|
|**sql_variant**|sql_variant |  
|**datetime2**|日期和時間|  
|**datetimeoffset**|日期和時間|  
|**datetime**|日期和時間|  
|**smalldatetime**|日期和時間|  
|**date**|日期和時間|  
|**time**|日期和時間|  
|**float**|近似數值|  
|**real**|近似數值|  
|**decimal**|精確數值|  
|**money**|精確數值|  
|**smallmoney**|精確數值|  
|**bigint**|精確數值|  
|**int**|精確數值|  
|**smallint**|精確數值|  
|**tinyint**|精確數值|  
|**bit**|精確數值|  
|**nvarchar**|Unicode|  
|**nchar**|Unicode|  
|**varchar**|Unicode|  
|**char**|Unicode|  
|**varbinary**|二進位|  
|**binary**|二進位|  
|**uniqueidentifier**|Uniqueidentifier |  
  
下列規則適用於**sql_variant**比較：
-   當**sql_variant**比較不同基底資料型別的值位在不同資料類型家族的基底資料類型，其資料類型家族在階層圖中較高的值會被視為兩個值的較大者。  
-   當**sql_variant**比較不同基底資料類型的值和基底資料類型是在相同的資料類型家族中，基底資料型別階層架構圖表中較低的值會隱含地轉換成其他資料類型和然後進行比較。  
-   當**sql_variant**值**char**， **varchar**， **nchar**，或**nvarchar**資料型別相較之下，其定序會先比較根據下列準則： LCID、 LCID 版本、 比較旗標和排序識別碼。 每一個準則都會以整數值的形式來比較，而且會根據所列的順序來比較。 如果所有的準則都相同，將會根據此定序來比較實際的字串值。  
  
## <a name="converting-sqlvariant-data"></a>轉換 sql_variant 資料  
當處理**sql_variant**資料型別，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]支援的物件與其他資料類型的隱含轉換**sql_variant**型別。 不過，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不支援的隱含地轉換**sql_variant**資料具有另一個資料類型的物件。
  
## <a name="restrictions"></a>限制  
下表列出的類型無法使用儲存的值**sql_variant**:
  
|||  
|-|-|  
|**varchar(max)**|**varbinary(max)**|  
|**nvarchar(max)**|**xml**|  
|**text**|**ntext**|  
|**image**|**rowversion** (**時間戳記**)|  
|**sql_variant**|**地理位置**|  
|**hierarchyid**|**幾何**|  
|使用者定義型別|**datetimeoffset**|  

## <a name="examples"></a>範例  

### <a name="a-using-a-sqlvariant-in-a-table"></a>A. 使用資料表中的 sql_variant  
 下列範例中，建立具有 sql_variant 資料類型的資料表。 然後此範例會擷取`SQL_VARIANT_PROPERTY`資訊`colA`值`46279.1`其中`colB`  = `1689`、 假設`tableA`具有`colA`型別的`sql_variant`和`colB`.  
  
```sql    
CREATE   TABLE tableA(colA sql_variant, colB int)  
INSERT INTO tableA values ( cast (46279.1 as decimal(8,2)), 1689)  
SELECT   SQL_VARIANT_PROPERTY(colA,'BaseType') AS 'Base Type',  
         SQL_VARIANT_PROPERTY(colA,'Precision') AS 'Precision',  
         SQL_VARIANT_PROPERTY(colA,'Scale') AS 'Scale'  
FROM      tableA  
WHERE      colB = 1689  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]請注意，每個這三個值是**sql_variant**。  
  
```  
Base Type    Precision    Scale  
---------    ---------    -----  
decimal      8           2  
  
(1 row(s) affected)  
```  
  
### <a name="b-using-a-sqlvariant-as-a-variable"></a>B. 使用 sql_variant 做為變數   
 下列範例中，使用 sql_variant 資料類型，建立變數，然後擷取`SQL_VARIANT_PROPERTY`名為變數的相關資訊@v1。  
  
```sql    
DECLARE @v1 sql_variant;  
SET @v1 = 'ABC';  
SELECT @v1;  
SELECT SQL_VARIANT_PROPERTY(@v1, 'BaseType');  
SELECT SQL_VARIANT_PROPERTY(@v1, 'MaxLength');  
```    


## <a name="see-also"></a>另請參閱
[CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[SQL_VARIANT_PROPERTY &#40;TRANSACT-SQL &#41;](../../t-sql/functions/sql-variant-property-transact-sql.md)
  
  

