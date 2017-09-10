---
title: "SQL_VARIANT_PROPERTY (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 42
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8cc3088c7025333c5cea3766cc65f56efdd45134
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="sqlvariantproperty-transact-sql"></a>SQL_VARIANT_PROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  傳回基底資料類型和其他資訊有關**sql_variant**值。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
SQL_VARIANT_PROPERTY ( expression , property )  
```  
  
## <a name="arguments"></a>引數  
 *expression*  
 這是類型的運算式**sql_variant**。  
  
 *屬性*  
 包含名稱的**sql_variant**資訊所提供的屬性。 *屬性*是**varchar (**128**)**，而且可以是下列值之一。  
  
|值|Description|傳回的 sql_variant 的基底類型|  
|-----------|-----------------|----------------------------------------|  
|**基本類型**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型，例如：<br /><br /> **bigint**<br /><br /> **binary**<br /><br /> **char**<br /><br /> **date**<br /><br /> **datetime**<br /><br /> **datetime2**<br /><br /> **datetimeoffset**<br /><br /> **decimal**<br /><br /> **float**<br /><br /> **int**<br /><br /> **money**<br /><br /> **nchar**<br /><br /> **numeric**<br /><br /> **nvarchar**<br /><br /> **real**<br /><br /> **smalldatetime**<br /><br /> **smallint**<br /><br /> **smallmoney**<br /><br /> **time**<br /><br /> **tinyint**<br /><br /> **uniqueidentifier**<br /><br /> **varbinary**<br /><br /> **varchar**|**sysname**<br /><br /> NULL = 輸入無效。|  
|**有效位數**|數值基底資料型別的位數：<br /><br /> **datetime** = 23<br /><br /> **smalldatetime** = 16<br /><br /> **float** = 53<br /><br /> **實際**= 24<br /><br /> **十進位**（p，s） 和**數值**（p，s） = p<br /><br /> **money** = 19<br /><br /> **smallmoney** = 10<br /><br /> **bigint** = 19<br /><br /> **int** = 10<br /><br /> **smallint** = 5<br /><br /> **tinyint** = 3<br /><br /> **位元**= 1<br /><br /> 其他所有類型 = 0|**int**<br /><br /> NULL = 輸入無效。|  
|**小數位數**|數值基底資料型別小數點右側的位數：<br /><br /> **十進位**（p，s） 和**數值**（p，s） = s<br /><br /> **money**和**smallmoney** = 4<br /><br /> **datetime** = 3<br /><br /> 其他所有類型 = 0|**int**<br /><br /> NULL = 輸入無效。|  
|**TotalBytes**|存放值的中繼資料和資料所需要的位元組數。 這項資訊會用於檢查中的資料最大值一端**sql_variant**資料行。 如果值大於 900，建立索引會失敗。|**int**<br /><br /> NULL = 輸入無效。|  
|**定序**|代表特定的定序**sql_variant**值。|**sysname**<br /><br /> NULL = 輸入無效。|  
|**MaxLength**|最大資料類型長度 (以位元組為單位)。 例如， **MaxLength**的**nvarchar (**50**)**是 100， **MaxLength**的**int**為 4。|**int**<br /><br /> NULL = 輸入無效。|  
  
## <a name="return-types"></a>傳回類型  
 **sql_variant**  
  
## <a name="examples"></a>範例  
 下列範例會擷取`SQL_VARIANT_PROPERTY`資訊`colA`值`46279.1`其中`colB`  = `1689`、 假設`tableA`具有`colA`型別的`sql_variant`和`colB`.  
  
```  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 下列範例會擷取`SQL_VARIANT_PROPERTY`名為變數的相關資訊@v1。  
  
```  
DECLARE @v1 sql_variant;  
SET @v1 = 'ABC';  
SELECT @v1;  
SELECT SQL_VARIANT_PROPERTY(@v1, 'BaseType');  
SELECT SQL_VARIANT_PROPERTY(@v1, 'MaxLength');  
```  
  
## <a name="see-also"></a>另請參閱  
 [sql_variant &#40;Transact-SQL&#41;](../../t-sql/data-types/sql-variant-transact-sql.md)  
  
  


