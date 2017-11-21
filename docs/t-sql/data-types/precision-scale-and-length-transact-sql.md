---
title: "有效位數、 小數位數和長度 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 7/22/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 31
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 557d7a5c45e9cc5a0839dfb4a1fdb0d08c2bf83f
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="precision-scale-and-length-transact-sql"></a>有效位數、 小數位數和長度 (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

位數 (Precision) 是指數字中總共的位數。 小數位數 (Scale) 則是指數字中小數點右方的位數。 例如 123.45 的位數是 5，小數位數是 2。
  
在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的預設最大有效位數**數值**和**十進位**資料型別為 38。 在舊版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，預設的最大值是 28。
  
數值資料類型的長度是用來儲存數字的位元組數目。 字元字串或 Unicode 資料類型的長度是字元的數目。 長度**二進位**， **varbinary**，和**映像**資料型別是位元組數。 例如， **int**資料類型可以保留 10 位數，儲存在 4 個位元組，而不接受小數點。 **Int**資料類型的精確度為 10，長度為 4 和小數位數為 0。
  
當兩個**char**， **varchar**，**二進位**，或**varbinary**運算式串連、 產生運算式的長度兩個來源運算式或 8,000 個字元，長度總和少者為準。
  
當兩個**nchar**或**nvarchar**運算式串連、 產生運算式的長度是 4000 個字元的兩個來源運算式長度的總和、 少者為準。
  
當利用 UNION、EXCEPT 或 INTERSECT 來比較長度不同之相同資料類型的運算式時，產生的長度是兩個運算式的最大長度。
  
有效位數和小數位數的數值資料類型，除了**十進位**固定的。 如果算術運算子有兩個相同類型的運算式，結果會有相同的資料類型，且會有定義給這個類型的有效位數和小數位數。 如果運算子有兩個含不同數值資料類型的運算式，資料類型優先順序的規則會定義這個結果的資料類型。 結果會有定義給它的資料類型的有效位數和小數位數。
  
下表定義的有效位數和小數位數為結果的計算方式是作業的結果類型**十進位**。 結果是**十進位**下列任一項為真時：
-   這兩個運算式都是**十進位**。  
-   一個運算式**十進位**，另一個較低的優先順序高於的資料型別**十進位**。  
  
運算元運算式表示成運算式 e1 (有效位數是 p1，小數位數是 s1) 和運算式 e2 (有效位數是 p2，小數位數是 s2)。 有效位數和小數位數不是任何運算式**十進位**的有效位數和小數位數的運算式資料類型的定義。
  
|作業|結果有效位數|結果小數位數 *|  
|---|---|---|
|e1 + e2|max(s1, s2) + max(p1-s1, p2-s2) + 1|max(s1, s2)|  
|e1 - e2|max(s1, s2) + max(p1-s1, p2-s2) + 1|max(s1, s2)|  
|e1 * e2|p1 + p2 + 1|s1 + s2|  
|e1 / e2|p1 - s1 + s2 + max(6, s1 + p2 + 1)|max(6, s1 + p2 + 1)|  
|e1 {聯集 &#124;除了 &#124;INTERSECT} e2|max(s1, s2) + max(p1-s1, p2-s2)|max(s1, s2)|  
|e1 % e2|min(p1-s1, p2 -s2) + max( s1,s2 )|max(s1, s2)|  
  
\*結果有效位數和小數位數有絕對最大值 38。 結果有效位數大於 38 時，可減少至 38，而且對應的標尺會降低再試一次，以防止截斷結果不可或缺的一部分。 在類似乘法或除法某些情況下，縮放比例將不會減少以保持十進制有效位數，雖然可以引發溢位錯誤。

加法與減法運算需要`max(p1 – s1, p2 – s2)`位置來儲存的十進位數字不可或缺的一部分。 如果沒有足夠的空間，也就是將它們儲存`max(p1 – s1, p2 – s2) < min(38, precision) – scale`，小數位數會減少到不可或缺的一部分，提供足夠的空間。 產生的小數位數是`MIN(precision, 38) - max(p1 – s1, p2 – s2)`，因此可能會捨入而無法放入產生的小數位數的小數部分。

乘法與除法運算需要`precision - scale`位置來儲存結果不可或缺的一部分。 可能會使用下列規則來減少小數位數：
1.  產生的小數位數降至`min(scale, 38 – (precision-scale))`不可或缺的部分是否小於 32、 因為它不能大於`38 – (precision-scale)`。 在此情況下可能會捨入結果。
1. 如果是小於 6，而且不可或缺的部分大於 32，不會變更小數位數。 在此情況下，溢位錯誤可能會引發它無法容納成十進位 （38，小數位數） 
1. 標尺將會設為 6 如果大於 6 的整數部分是否大於 32。 在此情況下，會降低不可或缺的一部分和小數位數，且結果類型是 decimal(38,6)。 結果可能會捨入為 6 的小數位數，或溢位錯誤會擲回不可或缺的一部分，無法納入 32 位數。

## <a name="examples"></a>範例
下列運算式會傳回結果`0.00000090000000000`而不需四捨五入，因為結果可以納入`decimal(38,17)`:
```sql
select cast(0.0000009000 as decimal(30,20)) * cast(1.0000000000 as decimal(30,20)) [decimal 38,17]
```
在此情況下精確度 61，且小數位數為 40。
不可或缺的一部分 (有效位數的小數位數 = 21) 並小於 32，因此這是乘法規則中的案例 (1)，小數位數的計算方式為`min(scale, 38 – (precision-scale)) = min(40, 38 – (61-40)) = 17`。 結果型別是`decimal(38,17)`。

下列運算式會傳回結果`0.000001`而無法放入`decimal(38,6)`:
```sql
select cast(0.0000009000 as decimal(30,10)) * cast(1.0000000000 as decimal(30,10)) [decimal(38, 6)]
```
在此情況下精確度 61，且小數位數是 20。
小數位數大於 6 和不可或缺的一部分 (`precision-scale = 41`) 大於 32。 乘法規則中的案例 (3)，而且結果型別是`decimal(38,6)`。

## <a name="see-also"></a>另請參閱
[運算式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
[資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
  
  

