---
title: 有效位數、小數位數和長度 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/22/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- data types [SQL Server], length
- data types [SQL Server], scale
- precision [SQL Server], data types
- lengths [SQL Server], data types
- number of digits
- scale [SQL Server]
- scale [SQL Server], data types
- data types [SQL Server], precision
ms.assetid: fbc9ad2c-0d3b-4e98-8fdd-4d912328e40a
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 6ecb198e9c2bcc7e23d1b4b66e8109ecf7c8fb5a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85786576"
---
# <a name="precision-scale-and-length-transact-sql"></a>有效位數、小數位數和長度 (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

位數 (Precision) 是指數字中總共的位數。 小數位數 (Scale) 則是指數字中小數點右方的位數。 例如 123.45 的位數是 5，小數位數是 2。
  
在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，**numeric** 和 **decimal** 資料類型的預設最大有效位數為 38。 在舊版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，預設的最大值是 28。
  
數值資料類型的長度是用來儲存數字的位元組數目。 若為 varchar 和 cha，則其字元字串的長度即是位元組的數目。 若為 nvarchar 和 nchar，則其字元字串的長度即是位元組配對的數目。 **binary**、**varbinary** 及 **image** 資料類型的長度為位元組的數目。 例如，**int** 資料類型可以保留 10 位數，儲存在 4 個位元組中且不接受小數點。 **int** 資料類型的有效位數是 10，長度是 4，小數位數是 0。
  
當串連兩個 **char**、**varchar**、**binary** 或 **varbinary** 運算式時，所產生運算式長度是兩個來源運算式長度的總和，最多為 8,000 個位元組。
  
當串連兩個 **nchar** 或 **nvarchar** 運算式時，所產生運算式長度是兩個來源運算式長度的總和，最多為 4,000 個位元組配對。
  
使用 UNION、EXCEPT 或 INTERSECT 來比較資料類型相同但長度不同的兩個運算式時，所產生長度是兩個運算式中較長的長度。
  
**decimal** 兩旁數值資料類型的有效位數和小數位數是固定的。 當算術運算子有兩個相同類型的運算式時，結果會有相同的資料類型，並具有定義給這個類型的有效位數和小數位數。 如果運算子有兩個含不同數值資料類型的運算式，資料類型優先順序的規則會定義這個結果的資料類型。 結果會有定義給它的資料類型的有效位數和小數位數。
  
下表定義在運算結果是 **decimal** 類型時，如何計算結果的有效位數和小數位數。 若符合下列其中一項條件，結果為 **decimal**：
-   兩個運算式都是 **decimal**。  
-   一個運算式為 **decimal**，另一個運算式為優先順序低於 **decimal** 的資料類型。  
  
運算元運算式表示成運算式 e1 (有效位數是 p1，小數位數是 s1) 和運算式 e2 (有效位數是 p2，小數位數是 s2)。 任何不是 **decimal** 之運算式的有效位數和小數位數，都是定義給運算式資料類型的有效位數和小數位數。 函式 max(a,b) 的意思是：取 "a" 或 "b" 當中較大的值。 同樣地，min(a,b) 表示取 "a" 或 "b" 當中較小的值。
  
|作業|結果有效位數|結果小數位數 *|  
|---|---|---|
|e1 + e2|max(s1, s2) + max(p1-s1, p2-s2) + 1|max(s1, s2)|  
|e1 - e2|max(s1, s2) + max(p1-s1, p2-s2) + 1|max(s1, s2)|  
|e1 * e2|p1 + p2 + 1|s1 + s2|  
|e1 / e2|p1 - s1 + s2 + max(6, s1 + p2 + 1)|max(6, s1 + p2 + 1)|  
|e1 { UNION &#124; EXCEPT &#124; INTERSECT } e2|max(s1, s2) + max(p1-s1, p2-s2)|max(s1, s2)|  
|e1 % e2|min(p1-s1, p2 -s2) + max( s1,s2 )|max(s1, s2)|  
  
\* 結果有效位數及小數位數的絕對最大值為 38。 當結果有效位數大於 38 時，會縮小至 38，並會縮減對應的小數位數，以防止截斷結果的整數部分。 在乘法或除法等某些案例中，為保持十進位有效位數，將不會縮減小數位數因數 (雖然可能會引發溢位錯誤)。

在加法跟減法運算中，我們需要 `max(p1 - s1, p2 - s2)` 位置來儲存十進位數字的整數部分。 若沒有足夠的空間來儲存它們 (即 `max(p1 - s1, p2 - s2) < min(38, precision) - scale`) 時，便會縮減小數位數，為整數部分提供足夠的空間。 其結果的小數位數便是 `MIN(precision, 38) - max(p1 - s1, p2 - s2)`，因此小數部分可能會四捨五入以調整至符合結果的小數位數。

在乘法及除法運算中，我們需要 `precision - scale` 位置來儲存結果的整數部分。 可能會使用下列規則來縮小小數位數：
1.  若整數部分小於 32，則結果的小數位數會縮減至 `min(scale, 38 - (precision-scale))`，因為它不可大於 `38 - (precision-scale)`。 在此案例中，結果可能會四捨五入。
1. 若小數位數小於 6 且整數部分大於 32，則小數位數便不會變更。 在此案例中，若無法調整為符合 decimal(38, scale)，便可能會引發溢位錯誤 
1. 若小數位數大於 6 且整數部分大於 32，則小數位數便會設為 6。 在此案例中，整數部分及小數位數都會縮小，且其結果的類型為 decimal(38, 6)。 結果可能會四捨五入至 6 個小數位數，或是擲回溢位錯誤 (若整數部分無法調整至 32 位數)。

## <a name="examples"></a>範例
下列運算式會傳回結果 `0.00000090000000000` 且不四捨五入，因為結果可調整至符合 `decimal(38,17)`：
```sql
select cast(0.0000009000 as decimal(30,20)) * cast(1.0000000000 as decimal(30,20)) [decimal 38,17]
```
在此案例中，位數 (precision) 為 61，小數位數 (scale) 為 40。
整數部分 (precision-scale = 21) 小於 32，因此這個案例屬於乘法規則中的案例 (1)，小數位數會計算為 `min(scale, 38 - (precision-scale)) = min(40, 38 - (61-40)) = 17`。 結果類型為 `decimal(38,17)`。

下列運算式會傳回結果 `0.000001` 以符合 `decimal(38,6)`：
```sql
select cast(0.0000009000 as decimal(30,10)) * cast(1.0000000000 as decimal(30,10)) [decimal(38, 6)]
```
在此案例中，位數為 61，小數位數為 20。
小數位數大於 6 且整數位數 (`precision-scale = 41`) 大於 32。 這個案例屬於乘法規則中的案例 (3)，其結果類型為 `decimal(38,6)`。

## <a name="see-also"></a>另請參閱
[運算式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
[資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
  
