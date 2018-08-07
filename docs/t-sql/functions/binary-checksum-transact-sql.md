---
title: BINARY_CHECKSUM  (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 64761bdee416467fa5cf0f73db93becb31901572
ms.sourcegitcommit: e02c28b0b59531bb2e4f361d7f4950b21904fb74
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/02/2018
ms.locfileid: "39452152"
---
# <a name="binarychecksum--transact-sql"></a>BINARY_CHECKSUM  (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

傳回針對一份資料表的某個資料列或一份運算式清單，來計算的二進位總和檢查碼值。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
BINARY_CHECKSUM ( * | expression [ ,...n ] )   
```  
  
## <a name="arguments"></a>引數  
*\**  
指定計算涵蓋所有資料表資料行。 BINARY_CHECKSUM 忽略其計算中無法比較之資料類型的資料行。 無法比較的資料類型包含  
* **cursor**  
* **image**  
* **ntext**  
* **text**  
* **xml**  

和無法比較的 Common Language Runtime (CLR) 使用者定義類型。
  
*expression*  
任意類型的[運算式](../../t-sql/language-elements/expressions-transact-sql.md)。 BINARY_CHECKSUM 忽略其計算中無法比較之資料類型的運算式。

## <a name="return-types"></a>傳回類型  
 **int**
  
## <a name="remarks"></a>Remarks  
只要後續未修改資料列，對資料表任何資料列執行計算的 BINARY_CHECKSUM(*)，會傳回相同值。 BINARY_CHECKSUM 會滿足雜湊函式的屬性：如果兩份清單的對應項目有相同的類型，且使用 equals (=) 運算子來比較時相等，則套用在任兩份運算式清單上的 BINARY_CHECKSUM 會傳回相同的值。 在此定義中，假設所指定類型的 Null 值比較為相等值。 如果運算式清單中至少有一個值變更，則運算式總和檢查碼也會變更。 不過，不保證一定會如此。 因此，若要偵測值是否已變更，建議只有在您的應用程式可以容忍偶而遺失的變更時才使用 BINARY_CHECKSUM。 否則，請考慮改用 HashBytes。 使用指定的 MD5 雜湊演算法時，HashBytes 為兩個不同的輸入傳回相同結果的可能性比 BINARY_CHECKSUM 要低很多。
  
BINARY_CHECKSUM 可以對運算式清單進行操作，並傳回所指定清單的相同值。 如果兩份清單的相對應元素有相同類型和位元組表示法，則套用在任何兩份運算式清單上的 BINARY_CHECKSUM 會傳回相同的值。 對這項定義而言，指定類型的 Null 值會被視為具有相同位元組表示法。
  
BINARY_CHECKSUM 和 CHECKSUM 是相似的函數：它們可用來計算運算式清單的總和檢查碼值，而運算式的順序會影響結果值。 用於 BINARY_CHECKSUM(*) 的資料行順序，是資料表或檢視定義所指定之資料行的順序。 計算資料行也包括在內。
  
BINARY_CHECKSUM 和 CHECKSUM 所傳回的字串資料類型值不同，其中地區設定會造成不同表示法的字串比較為相等。 字串資料類型為  

* **char**  
* **nchar**  
* **nvarchar**  
* **varchar**  

中的多個  

* **sql_variant** (如果 **sql_variant** 的基底類型是字串資料類型)。  
  
例如，"McCavity" 和 "Mccavity" 字串的 BINARY_CHECKSUM 值不同。 反之，在不區分大小寫的伺服器中，CHECKSUM 對那些字串會傳回相同的總和檢查碼值。 您應該避免比較 CHECKSUM 值與 BINARY_CHECKSUM 值。
 
BINARY_CHECKSUM 針對 **varbinary(max)** 類型支援最多 8,000 個字元，針對 **nvarchar(max)** 類型則支援最多 255 個字元。
  
## <a name="examples"></a>範例  
此範例使用 `BINARY_CHECKSUM` 來偵測資料表資料列中的變更。
  
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
[彙總函式 &#40;Transact-SQL&#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)  
[CHECKSUM &#40;Transact-SQL&#41;](../../t-sql/functions/checksum-transact-sql.md)  
[CHECKSUM_AGG &#40;Transact-SQL&#41;](../../t-sql/functions/checksum-agg-transact-sql.md)
  
  
