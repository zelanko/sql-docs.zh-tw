---
title: "BINARY_CHECKSUM (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- BINARY_CHECKSUM
- BINARY_CHECKSUM_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- BINARY_CHECKSUM function
- binary [SQL Server], checksum values
ms.assetid: 07fece4d-58e3-446e-a3b5-92fe24d2d1fb
caps.latest.revision: 21
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b84847f3efe7224c6fa0ad945b03f3afbc1381b9
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="binarychecksum--transact-sql"></a>BINARY_CHECKSUM (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

傳回針對一份資料表的某個資料列或一份運算式清單，來計算的二進位總和檢查碼值。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
BINARY_CHECKSUM ( * | expression [ ,...n ] )   
```  
  
## <a name="arguments"></a>引數  
*\**  
指定針對資料表的所有資料行來計算。 BINARY_CHECKSUM 忽略其計算中無法比較之資料類型的資料行。 無法比較之資料類型包括**文字**， **ntext**，**映像**，**游標**， **xml**，和無法比較之 common language runtime (CLR) 使用者定義類型。
  
*expression*  
是[運算式](../../t-sql/language-elements/expressions-transact-sql.md)任何型別。 BINARY_CHECKSUM 忽略其計算中無法比較之資料類型的運算式。
  
## <a name="remarks"></a>備註  
只要後續未修改資料列，對資料表任何資料列執行計算的 BINARY_CHECKSUM(*)，會傳回相同值。 BINARY_CHECKSUM 會滿足雜湊函式的屬性： 如果兩個 list 的對應元素有相同的類型，且利用等於 （=） 運算子的比較時相等，套用在任何兩份運算式清單的 BINARY_CHECKSUM 會傳回相同的值。 對這項定義而言，指定類型的 Null 值會被視為比較結果相等。 如果變更了運算式清單中的其中一個值，清單的總和檢查碼通常也會改變。 不過，總和檢查碼也有可能不會變更。 基於這個理由，我們不建議使用 BINARY_CHECKSUM 來偵測是否已變更值，除非您的應用程式可以容忍偶爾遺失變更。 請考慮改用 HashBytes。 當指定 MD5 雜湊演算法時，HashBytes 傳回兩個不同的輸入相同的結果的機率是比的 BINARY_CHECKSUM 更低。
  
BINARY_CHECKSUM 可套用至運算式清單，並傳回指定清單的相同值。 如果兩份清單的相對應元素有相同類型和位元組表示法，則套用在任何兩份運算式清單上的 BINARY_CHECKSUM 會傳回相同的值。 對這項定義而言，指定類型的 Null 值會被視為具有相同位元組表示法。
  
BINARY_CHECKSUM 和 CHECKSUM 是相似的函數：它們可用來計算運算式清單的總和檢查碼值，而運算式的順序會影響結果值。 用於 BINARY_CHECKSUM(*) 的資料行順序，是資料表或檢視定義所指定之資料行的順序。 其中包括計算資料行。
  
CHECKSUM 和 BINARY_CHECKSUM 傳回字串資料類型的不同值，其中地區設定會造成不同表示法的字串比較之後相等。 字串資料類型為**char**， **varchar**， **nchar**， **nvarchar**，或**sql_variant** (如果基底類型**sql_variant**是字串資料類型)。 例如，"McCavity" 和 "Mccavity" 字串的 BINARY_CHECKSUM 值不同。 反之，在不區分大小寫的伺服器上，CHECKSUM 對那些字串會傳回相同的總和檢查碼值。 CHECKSUM 值不應該與 BINARY_CHECKSUM 值做比較。
 
BINARY_CHECKSUM 支援最多 8000 個字元的**varbinary （max)**和最多 255 個字元的型別**nvarchar （max)**。
  
## <a name="examples"></a>範例  
下列範例會利用 `BINARY_CHECKSUM` 來偵測資料表中資料列的變更。
  
```sql
USE AdventureWorks2012;  
GO  
CREATE TABLE myTable (column1 int, column2 varchar(256));  
GO  
INSERT INTO myTable VALUES (1, 'test');  
GO  
SELECT BINARY_CHECKSUM(*) from myTable;  
GO  
UPDATE myTable set column2 = 'TEST';  
GO  
SELECT BINARY_CHECKSUM(*) from myTable;  
GO  
```  
  
## <a name="see-also"></a>另請參閱
[彙總函式 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)  
[總和檢查碼 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/checksum-transact-sql.md)  
[CHECKSUM_AGG &#40;TRANSACT-SQL &#41;](../../t-sql/functions/checksum-agg-transact-sql.md)
  
  

