---
title: 包含或排除資料列 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- search criteria [SQL Server], excluding rows
- search criteria [SQL Server], WHERE clause
- included rows
- search conditions [SQL Server], HAVING clause
- search criteria [SQL Server], including rows
- row excluded in search [SQL Server]
- search criteria [SQL Server], HAVING clause
- search conditions [SQL Server], WHERE clause
- row included in search [SQL Server]
- excluding rows
ms.assetid: ba4e1202-31a2-444d-8365-c68a530ef223
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3785a777571ef7659b1ae21a693e6754659a80e5
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "63298584"
---
# <a name="include-or-exclude-rows-visual-database-tools"></a>包含或排除資料列 (Visual Database Tools)
  若要限制 SELECT 查詢傳回的資料列數目，您可以建立搜尋條件或篩選條件。 在 SQL 中，搜尋條件出現在陳述式中的 WHERE 子句，或如果您要建立彙總查詢，查詢條件則位於 HAVING 子句中。  
  
> [!NOTE]  
>  您也可以使用搜尋條件來指出受到 UPDATE、Insert Results、Insert Values、DELETE 或製成資料表查詢影響的資料列。  
  
 執行查詢時， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會檢查並將搜尋條件套用到您正在搜尋之資料表中的每個資料列。 如果符合搜尋條件，該資料列將包含在查詢中。 例如，要在特定區域中尋找所有員工的搜尋條件可以是：  
  
```  
region = 'UK'  
```  
  
 若要建立將資料列包含在結果的準則，您可以使用多重搜尋條件。 例如，下列搜尋準則含有兩個搜尋條件。 如果資料列同時符合這兩個條件，查詢才會將該資料列包含在結果集中。  
  
```  
region = 'UK' AND product_line = 'Housewares'  
```  
  
 您可以使用 AND 或 OR 來結合這些條件。 上面的範例即使用 AND。 相反的，下面的搜尋準則則是使用 OR。 結果集將包含符合其中一個或同時符合兩個搜尋條件的所有資料列：  
  
```  
region = 'UK' OR product_line = 'Housewares'  
```  
  
 您甚至可以在單一資料行中結合搜尋條件。 例如，以下準則即結合了區域資料行的兩個條件：  
  
```  
region = 'UK' OR region = 'US'  
```  
  
 如需結合搜尋條件的詳細資訊，請參閱下列主題：  
  
-   [在條件窗格中合併搜尋條件的慣例 &#40;Visual Database Tools&#41;](conventions-combine-search-conditions-in-criteria-pane-visual-db-tools.md)  
  
-   [指定單一資料行的多重搜尋條件 &#40;Visual Database Tools&#41;](visual-database-tools.md)  
  
-   [指定多重資料行的多重搜尋條件 &#40;Visual Database Tools&#41;](specify-multiple-search-conditions-for-multiple-columns-visual-database-tools.md)  
  
-   [在 AND 具有優先權時結合條件 &#40;Visual Database Tools&#41;](combine-conditions-when-and-has-precedence-visual-database-tools.md)  
  
-   [在 OR 具有優先權時結合條件 &#40;Visual Database Tools&#41;](combine-conditions-when-or-has-precedence-visual-database-tools.md)  
  
## <a name="examples"></a>範例  
 此處是使用不同運算子和資料列準則之查詢的一些範例：  
  
-   **常值** ，單一文字、數字、日期或邏輯值。 下例即使用常值搜尋所有資料列，尋找位於英國的員工：  
  
    ```  
    WHERE region = 'UK'  
    ```  
  
-   **資料行參考** ：將某一資料行中的值與另一個資料行中的值進行比較。 下例即搜尋 `products` 資料表中的所有資料列，其中生產成本的值低於貨運成本：  
  
    ```  
    WHERE prod_cost < ship_cost  
    ```  
  
-   **函數** ：函數的參考，資料庫後端可解析該函數以計算搜尋的值。 函數可以是資料庫伺服器所定義的函數，或傳回純量值的使用者定義函數。 下列範例即搜尋今天所發出的訂單 (GETDATE( ) 函數將傳回目前日期)：  
  
    ```  
    WHERE order_date = GETDATE()  
    ```  
  
-   **NULL** ，下列範例將在 `authors` 資料表中搜尋檔案中出現其名字的所有作者：  
  
    ```  
    WHERE au_fname IS NOT NULL  
    ```  
  
-   **計算** ：計算的結果可能是常值、資料行參考或其他運算式。 下列範例中即在 `products` 資料表中搜尋所有資料列，其中尋找零售價格是生產價格的兩倍：  
  
    ```  
    WHERE sales_price > (prod_cost * 2)  
    ```  
  
## <a name="see-also"></a>另請參閱  
 [設計查詢和觀看 how to 主題 &#40;Visual Database Tools&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)   
 [&#40;Visual Database Tools 指定搜尋準則&#41;](specify-search-criteria-visual-database-tools.md)   
 [使用參數查詢 &#40;Visual Database Tools&#41;](query-with-parameters-visual-database-tools.md)  
  
  
