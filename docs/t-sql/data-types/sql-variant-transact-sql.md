---
title: sql_variant (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 9/12/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|data-types
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
ms.openlocfilehash: fc20b30cf079bb597108483e3b71d5c151535f2a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sqlvariant-transact-sql"></a>sql_variant (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

儲存各種 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援之資料類型值的資料類型。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
sql_variant  
```  
  
## <a name="remarks"></a>Remarks  
**sql_variant** 可用在資料行、參數、變數及使用者定義函式的傳回值中。 **sql_variant** 可讓這些資料庫物件支援其他資料類型的值。
  
**sql_variant** 類型的資料行可包含不同資料類型的資料列。 例如，定義為 **sql_variant** 的資料行可儲存 **int**、**binary**，及 **char** 值。
  
**sql_variant** 的最大長度是 8016 位元組。 其中包括基底類型資訊和基底類型值。 實際基底類型值的最大長度是 8,000 位元組。
  
**sql_variant** 資料類型必須先轉換成其基底資料型別值，之後才能參與加法和減法之類的作業。
  
您可以指派預設值給 **sql_variant**。 這項資料類型也可以用 NULL 作為基礎值，但 NULL 值並沒有相關的基底類型。 此外，**sql_variant** 的基底類型不可為另一個 **sql_variant**。
  
唯一、主要或外部索引鍵可以包括 **sql_variant** 類型的資料行，但組成特定資料列的索引鍵之資料值總長度，不應超出索引的最大長度。 這是 900 位元組。
  
一份資料表可以有任意數目的 **sql_variant** 資料行。
  
在 CONTAINSTABLE 和 FREETEXTTABLE 中，無法使用 **sql_variant**。
  
ODBC 不完全支援 **sql_variant**。 因此，當您使用 Microsoft OLE DB Provider for ODBC (MSDASQL) 時，會將 **sql_variant** 資料行的查詢當作二進位資料傳回。 例如，包含 'PS2091' 字元字串資料的 **sql_variant** 資料行會以 0x505332303931 傳回。
  
## <a name="comparing-sqlvariant-values"></a>比較 sql_variant 值  
**sql_variant** 資料類型屬於轉換的資料類型階層清單頂端。 為比較 **sql_variant**，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型階層順序會分組成資料類型家族。
  
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
  
下列規則適用於 **sql_variant** 比較：
-   當比較不同基底資料型別的 **sql_variant** 值，且基底資料型別是在不同的資料類型家族中時，資料類型家族在階層圖表中較高位置的值，會被視為兩個值中的較大者。  
-   當比較不同基底資料型別的 **sql_variant** 值，且基底資料型別是在相同的資料類型家族中，會先將基底資料型別在階層圖表中較低位置的值隱含轉換成其他資料類型，之後再進行比較。  
-   當比較 **char**、**varchar**、**nchar** 或 **nvarchar** 資料類型的 **sql_variant** 值時，將會先根據以下準則來比較其定序：LCID、LCID 版本、比較旗標和排序識別碼。 每一個準則都會以整數值的形式來比較，而且會根據所列的順序來比較。 如果所有的準則都相同，將會根據此定序來比較實際的字串值。  
  
## <a name="converting-sqlvariant-data"></a>轉換 sql_variant 資料  
處理 **sql_variant** 資料類型時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援將有其他資料類型的物件隱含轉換成 **sql_variant** 類型。 但 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支援從 **sql_variant** 資料隱含轉換成其他資料類型的物件。
  
## <a name="restrictions"></a>限制  
下表列出無法使用 **sql_variant** 來儲存的值類型：
  
|||  
|-|-|  
|**varchar(max)**|**varbinary(max)**|  
|**nvarchar(max)**|**xml**|  
|**text**|**ntext**|  
|**image**|**rowversion** (**timestamp**)|  
|**sql_variant**|**地理位置**|  
|**hierarchyid**|**幾何**|  
|使用者定義型別|**datetimeoffset**|  

## <a name="examples"></a>範例  

### <a name="a-using-a-sqlvariant-in-a-table"></a>A. 在資料表中使用 sql_variant  
 下列範例會使用 sql_variant 資料類型建立資料表。 接著範例會擷取有關 `colA` 值 `46279.1` 的 `SQL_VARIANT_PROPERTY` 資訊，如果 `tableA` 有 `colB` 和 `sql_variant` 類型的 `colA`，則 `colB` =`1689`。  
  
```sql    
CREATE   TABLE tableA(colA sql_variant, colB int)  
INSERT INTO tableA values ( cast (46279.1 as decimal(8,2)), 1689)  
SELECT   SQL_VARIANT_PROPERTY(colA,'BaseType') AS 'Base Type',  
         SQL_VARIANT_PROPERTY(colA,'Precision') AS 'Precision',  
         SQL_VARIANT_PROPERTY(colA,'Scale') AS 'Scale'  
FROM      tableA  
WHERE      colB = 1689  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)] 請注意，這三個值的每一個都是 **sql_variant**。  
  
```  
Base Type    Precision    Scale  
---------    ---------    -----  
decimal      8           2  
  
(1 row(s) affected)  
```  
  
### <a name="b-using-a-sqlvariant-as-a-variable"></a>B. 使用 sql_variant 作為變數   
 下列範例會使用 sql_variant 資料類型建立變數，然後擷取關於名為 @v1 之變數的 `SQL_VARIANT_PROPERTY` 資訊。  
  
```sql    
DECLARE @v1 sql_variant;  
SET @v1 = 'ABC';  
SELECT @v1;  
SELECT SQL_VARIANT_PROPERTY(@v1, 'BaseType');  
SELECT SQL_VARIANT_PROPERTY(@v1, 'MaxLength');  
```    


## <a name="see-also"></a>另請參閱
[CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[SQL_VARIANT_PROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/sql-variant-property-transact-sql.md)
  
  
