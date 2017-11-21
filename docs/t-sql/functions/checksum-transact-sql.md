---
title: "總和檢查碼 (TRANSACT-SQL) |Microsoft 文件"
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
- CHECKSUM_TSQL
- CHECKSUM
dev_langs:
- TSQL
helpviewer_keywords:
- hash indexes
- CHECKSUM function
- checksum values
ms.assetid: e26d3339-845c-49c2-9d89-243376874c13
caps.latest.revision: 44
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0379260c517f546bf00c5e757f6a3069f574f102
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="checksum-transact-sql"></a>CHECKSUM (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

傳回針對一份資料表的某個資料列或一份運算式清單，來計算的總和檢查碼值。 CHECKSUM 用來建立雜湊索引。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
CHECKSUM ( * | expression [ ,...n ] )  
```  
  
## <a name="arguments"></a>引數  
\*  
指定針對資料表的所有資料行來計算。 如果有任何資料行是不可比較的資料類型，CHECKSUM 會傳回錯誤。 不可比較的資料類型為**文字**， **ntext**，**映像**，XML 和**游標**，以及**sql_variant**與任何一個先前的類型作為其基底類型。
  
*expression*  
是[運算式](../../t-sql/language-elements/expressions-transact-sql.md)不可比較的資料類型以外之任何類型。
  
## <a name="return-types"></a>傳回型別
 **int**  
  
## <a name="remarks"></a>備註  
CHECKSUM 會針對它的引數清單，來計算稱為總和檢查碼的雜湊值。 雜湊值用來建立雜湊索引。 如果 CHECKSUM 的引數是資料行，且在計算的 CHECKSUM 值上建立索引，結果就是雜湊索引。 這可用來進行資料行的相等搜尋。
  
CHECKSUM 會滿足雜湊函數的屬性：如果兩份清單的對應元素有相同的類型，且利用等於 (=) 運算子來比較時相等，套用在任何兩份運算式清單上的 CHECKSUM 會傳回相同的值。 對這項定義而言，指定類型的 Null 值會被視為比較結果相等。 如果變更了運算式清單中的其中一個值，清單的總和檢查碼通常也會改變。 不過，總和檢查碼也有可能不會變更。 因此，我們不建議使用 CHECKSUM 來偵測是否已變更值，除非應用程式可以容忍偶爾遺失變更。 請考慮使用[HashBytes](../../t-sql/functions/hashbytes-transact-sql.md)改為。 當指定 MD5 雜湊演算法時，HashBytes 為兩個不同的輸入傳回相同結果的可能性比 CHECKSUM 要低很多。
  
運算式的順序會影響 CHECKSUM 的結果值。 搭配 CHECKSUM(*) 一起使用的資料行順序，是資料表或檢視定義所指定之資料行的順序。 計算資料行也包括在內。
  
CHECKSUM 值取決於定序。 以不同的定序儲存相同的值，將會傳回不同的 CHECKSUM 值。
  
## <a name="examples"></a>範例  
下列範例會示範如何利用 `CHECKSUM` 建立雜湊索引。 雜湊索引的建立方式，是將計算總和檢查碼資料行加入要建立索引的資料表，然後再建立總和檢查碼資料行的索引。
  
```sql
-- Create a checksum index.  
SET ARITHABORT ON;  
USE AdventureWorks2012;   
GO  
ALTER TABLE Production.Product  
ADD cs_Pname AS CHECKSUM(Name);  
GO  
CREATE INDEX Pname_index ON Production.Product (cs_Pname);  
GO  
```  
  
總和檢查碼索引可用來作為雜湊索引，當建立索引的資料行是長的字元資料行時，尤其能夠改進建立索引的速度。 總和檢查碼索引也可用來進行相等搜尋。
  
```sql
/*Use the index in a SELECT query. Add a second search   
condition to catch stray cases where checksums match,   
but the values are not the same.*/  
SELECT *   
FROM Production.Product  
WHERE CHECKSUM(N'Bearing Ball') = cs_Pname  
AND Name = N'Bearing Ball';  
GO  
```  
  
建立計算資料行的索引，會使總和檢查碼資料行具體化，`ProductName` 值的任何變更都會傳播到總和檢查碼資料行。 另外，您也可以在建立索引的資料行上，直接建立索引。 不過，如果索引鍵值很長，可能不會執行正規索引及總和檢查碼索引。
  
## <a name="see-also"></a>另請參閱
[CHECKSUM_AGG &#40;TRANSACT-SQL &#41;](../../t-sql/functions/checksum-agg-transact-sql.md)  
[HASHBYTES &#40;TRANSACT-SQL &#41;](../../t-sql/functions/hashbytes-transact-sql.md)  
[BINARY_CHECKSUM &#40;TRANSACT-SQL &#41;](../../t-sql/functions/binary-checksum-transact-sql.md)
  
  

