---
title: SQL_VARIANT_PROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/25/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SQL_VARIANT_PROPERTY_TSQL
- SQL_VARIANT_PROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- SQL_VARIANT_PROPERTY function
- sql_variant data type
ms.assetid: 50e5c1d9-4e95-4ed0-9c92-435c872a399e
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2de6604c494a73666f4ae481cdef2d18a50fa5ea
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/06/2020
ms.locfileid: "85996628"
---
# <a name="sql_variant_property-transact-sql"></a>SQL_VARIANT_PROPERTY (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  傳回基底資料型別和 **sql_variant** 值的其他相關資訊。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
SQL_VARIANT_PROPERTY ( expression , property )  
```  
  
## <a name="arguments"></a>引數  
 *expression*  
 為 **sql_variant** 類型的運算式。  
  
 *property*  
 包含要為其提供資訊的 **sql_variant** 屬性名稱。 *property* 為 **varchar(** 128 **)** ，可以是下列值中的任何一個：  
  
|值|描述|傳回的 sql_variant 的基底類型|  
|-----------|-----------------|----------------------------------------|  
|**BaseType**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型，例如：<br /><br /> **bigint**<br /><br /> **binary**<br /><br /> **bit**<br /><br /> **char**<br /><br /> **date**<br /><br /> **datetime**<br /><br /> **datetime2**<br /><br /> **datetimeoffset**<br /><br /> **decimal**<br /><br /> **float**<br /><br /> **int**<br /><br /> **money**<br /><br /> **nchar**<br /><br /> **numeric**<br /><br /> **nvarchar**<br /><br /> **real**<br /><br /> **smalldatetime**<br /><br /> **smallint**<br /><br /> **smallmoney**<br /><br /> **time**<br /><br /> **tinyint**<br /><br /> **uniqueidentifier**<br /><br /> **varbinary**<br /><br /> **varchar**|**sysname**<br /><br /> NULL = 輸入無效。|  
|**有效位數**|數值基底資料型別的位數：<br /><br /> **date** = 10<br /><br /> **datetime** = 23<br /><br /> **datetime2** = 27<br /><br /> 當 s = 0 時，**datetime2** (s) = 19，否則 s + 20<br /><br /> **datetimeoffset** = 34<br /><br /> 當 s = 0 時，**datetimeoffset** (s) = 26，否則 s + 27<br /><br /> **smalldatetime** = 16<br /><br /> **time** = 16<br /><br /> 當 s = 0 時，**time** (s) = 8，否則 s + 9<br /><br /> **float** = 53<br /><br /> **real** = 24<br /><br /> **decimal** 和 **numeric** = 18<br /><br /> **decimal** (p,s) 和 **numeric** (p,s) = p<br /><br /> **money** = 19<br /><br /> **smallmoney** = 10<br /><br /> **bigint** = 19<br /><br /> **int** = 10<br /><br /> **smallint** = 5<br /><br /> **tinyint** = 3<br /><br /> **bit** = 1<br /><br /> 其他所有類型 = 0|**int**<br /><br /> NULL = 輸入無效。|  
|**調整**|數值基底資料型別小數點右側的位數：<br /><br /> **decimal** 和 **numeric** = 0<br /><br /> **decimal** (p,s) 和 **numeric** (p,s) = s<br /><br /> **money** 和 **smallmoney** = 4<br /><br /> **datetime** = 3<br /><br /> **datetime2** = 7<br /><br /> **datetime2** (s) = s (0 - 7)<br /><br /> **datetimeoffset** = 7<br /><br /> **datetimeoffset** (s) = s (0 - 7)<br /><br /> **time** = 7<br /><br /> **time** (s) = s (0 - 7)<br /><br /> 其他所有類型 = 0|**int**<br /><br /> NULL = 輸入無效。|  
|**TotalBytes**|存放值的中繼資料和資料所需要的位元組數。 在檢查 **sql_variant** 資料行中資料的最大值一端時，這項資訊非常有用。 如果值大於 900，建立索引會失敗。|**int**<br /><br /> NULL = 輸入無效。|  
|**定序**|代表特定 **sql_variant** 值的定序。|**sysname**<br /><br /> NULL = 輸入無效。|  
|**MaxLength**|最大資料類型長度 (以位元組為單位)。 例如，**nvarchar(** 50 **)** 的 **MaxLength** 為 100，**int** 的 **MaxLength** 為 4。|**int**<br /><br /> NULL = 輸入無效。|  
  
## <a name="return-types"></a>傳回型別  
 **sql_variant**  
  
## <a name="examples"></a>範例  
### <a name="a-using-a-sql_variant-in-a-table"></a>A. 在資料表中使用 sql_variant  
 下列範例會擷取有關 `colA` 值 `46279.1` 的 `SQL_VARIANT_PROPERTY` 資訊，其中 `colB` =`1689` (若 `tableA` 有類型為 `sql_variant` 的 `colA` 及 `colB`)。  
  
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
  
### <a name="b-using-a-sql_variant-as-a-variable"></a>B. 使用 sql_variant 作為變數   
 下列範例會擷取名為 @v1 之變數的相關 `SQL_VARIANT_PROPERTY` 資訊。  
  
```sql    
DECLARE @v1 sql_variant;  
SET @v1 = 'ABC';  
SELECT @v1;  
SELECT SQL_VARIANT_PROPERTY(@v1, 'BaseType');  
SELECT SQL_VARIANT_PROPERTY(@v1, 'MaxLength');  
```  
  
## <a name="see-also"></a>另請參閱  
 [sql_variant &#40;Transact-SQL&#41;](../../t-sql/data-types/sql-variant-transact-sql.md)  
  
  

