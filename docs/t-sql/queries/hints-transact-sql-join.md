---
title: "聯結提示 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 08/09/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Join Hint
- Join_Hint_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- HASH join hint
- REMOTE join hint
- LOOP join hint
- join hints
- MERGE join hint
- hints [SQL Server], join
ms.assetid: 09069f4a-f2e3-4717-80e1-c0110058efc4
caps.latest.revision: 30
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 230241b9626c8d2790fb55fa82c40bab24613dbc
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="hints-transact-sql---join"></a>聯結提示 (TRANSACT-SQL)-
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  聯結提示會指定查詢最佳化工具強制執行 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中兩個資料表之間的聯結策略。 如需聯結和聯結語法的一般資訊，請參閱[FROM &#40;TRANSACT-SQL &#41;](../../t-sql/queries/from-transact-sql.md).  
  
> [!IMPORTANT]  
>  因為[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]查詢最佳化工具通常會選取查詢的最佳執行計畫，我們建議的提示有，包括\<join_hint >，來只當做最後手段資深的開發人員和資料庫管理員。
  
 **適用於：**  
  
 [DELETE](../../t-sql/statements/delete-transact-sql.md)  
  
 [SELECT](../../t-sql/queries/select-transact-sql.md)  
  
 [UPDATE](../../t-sql/queries/update-transact-sql.md)  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
<join_hint> ::=   
     { LOOP | HASH | MERGE | REMOTE }  
```  
  
## <a name="arguments"></a>引數  
 LOOP | HASH | MERGE  
 指定查詢中的聯結應該使用迴圈、雜湊或合併。 使用 LOOP |HASH | MERGE JOIN 會在兩份資料表之間強制執行特定聯結。 您無法同時使用 RIGHT 或 FULL，將 LOOP 指定為聯結類型。  
  
 REMOTE  
 指定在右資料表上執行聯結作業。 當左資料表是本機資料表，右資料表是遠端資料表時，這非常有用。 只有在左資料表的資料列數比右資料表少時，才應該使用 REMOTE。  
  
 如果右資料表是本機資料表，則聯結會在本機執行。 如果兩份資料表都在遠端，但來自不同的資料來源，REMOTE 會以右資料表為基礎來執行聯結。 如果兩份資料表都是遠端資料表，且來自相同資料來源，就不需要 REMOTE。  
  
 當利用 COLLATE 子句將聯結述詞所比較的其中一個值轉換成不同的定序時，便不能使用 REMOTE。  
  
 REMOTE 只能用於 INNER JOIN 作業。  
  
## <a name="remarks"></a>備註  
 聯結提示是在查詢的 FROM 子句中指定。 聯結提示會強制執行兩份資料表之間的聯結策略。 如果指定了兩份資料表的聯結提示，查詢最佳化工具會根據 ON 關鍵字的位置，自動強制執行查詢中所有聯結的資料表之聯結順序。 當使用不含 ON 子句的 CROSS JOIN 時，您可以用括號來指示聯結順序。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-hash"></a>A. 使用 HASH  
 下列範例指定查詢中的 `JOIN` 作業由 `HASH` 聯結執行。 此範例會使用 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫。  
  
```  
SELECT p.Name, pr.ProductReviewID  
FROM Production.Product AS p  
LEFT OUTER HASH JOIN Production.ProductReview AS pr  
ON p.ProductID = pr.ProductID  
ORDER BY ProductReviewID DESC;  
```  
  
### <a name="b-using-loop"></a>B. 使用 LOOP  
 下列範例指定查詢中的 `JOIN` 作業由 `LOOP` 聯結執行。 此範例會使用 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫。  
  
```  
DELETE FROM Sales.SalesPersonQuotaHistory   
FROM Sales.SalesPersonQuotaHistory AS spqh  
    INNER LOOP JOIN Sales.SalesPerson AS sp  
    ON spqh.SalesPersonID = sp.SalesPersonID  
WHERE sp.SalesYTD > 2500000.00;  
GO  
```  
  
### <a name="c-using-merge"></a>C. 使用 MERGE  
 下列範例指定查詢中的 `JOIN` 作業由 `MERGE` 聯結執行。 此範例會使用 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫。  
  
```  
SELECT poh.PurchaseOrderID, poh.OrderDate, pod.ProductID, pod.DueDate, poh.VendorID   
FROM Purchasing.PurchaseOrderHeader AS poh  
INNER MERGE JOIN Purchasing.PurchaseOrderDetail AS pod   
    ON poh.PurchaseOrderID = pod.PurchaseOrderID;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [提示 &#40;TRANSACT-SQL &#41;](../../t-sql/queries/hints-transact-sql.md)  
  
  

