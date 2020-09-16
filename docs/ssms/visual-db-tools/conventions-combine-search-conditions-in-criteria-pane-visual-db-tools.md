---
description: 在條件窗格中合併搜尋條件的慣例 (Visual Database Tools)
title: 在準則窗格中合併搜尋條件的慣例
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- search conditions [SQL Server], combining
- precedence [SQL Server], Criteria pane
- search criteria [SQL Server], combining conditions
- multiple OR clauses
- combining search conditions
- OR operator
- AND, Criteria pane
- multiple AND clauses
ms.assetid: d4859be5-ff5b-48b2-a101-ad40c6dbcc68
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: ae92bc88f3b18dcd195d857c1ccc975d116880f3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88491711"
---
# <a name="conventions-for-combining-search-conditions-in-the-criteria-pane-visual-database-tools"></a>在條件窗格中合併搜尋條件的慣例 (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
您可以建立使用任意多個 AND 和 OR 運算子連結，包含任何搜尋條件的查詢。 查詢中如有使用 AND 與 OR 子句組合比較複雜，因此建議能夠先了解這類查詢在您執行時的解譯方式，以及這類查詢在 [[準則窗格]](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md) 及 [SQL 窗格](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md)中的表示方式。  
  
> [!NOTE]  
> 如需只包含 AND 或 OR 運算子之搜尋條件的詳細資料，請參閱[指定單一資料行的多重搜尋條件 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-multiple-search-conditions-for-one-column-visual-database-tools.md) 及[指定多重資料行的多重搜尋條件 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-multiple-search-conditions-for-multiple-columns-visual-database-tools.md)。  
  
您可以在下面找到的資訊：  
  
-   同時包含 AND 和 OR 運算子的查詢中運算子的優先順序。  
  
-   AND 和 OR 子句裡各種條件相互的邏輯關係。  
  
-   查詢和檢視設計工具在 [準則窗格] 中表示包含 AND 和 OR 的查詢的方式。  
  
為了協助您了解下列的討論，試想您正在使用包含資料行 `employee` 、 `hire_date`和 `job_lvl`的 `status`資料表。 範例假設您必須知道某個員工在公司的年資 (員工的雇用日期)、員工負責的工作類型 (工作階層) 以及員工的狀態 (例如已退休) 等資訊。  
  
## <a name="precedence-of-and-and-or"></a>AND 和 OR 的優先順序  
執行查詢時，查詢會先評估以 AND 連結的子句，然後再評估以 OR 連結的子句。  
  
> [!NOTE]  
> NOT 運算子的優先順序高於 AND 和 OR。  
  
例如，要尋找在公司擔任低階層工作，年資在五年以上的員工；或者擔任中階層工作，不論雇用日期為何的員工，可以依照以下範例建構一個 WHERE 子句：  
  
```  
WHERE   
   hire_date < '01/01/95' AND   
   job_lvl = 100 OR  
   job_lvl = 200  
```  
  
若要覆寫預設的 AND 先於 OR 的優先順序，可以在 SQL 窗格中利用括號括住特定的條件。 括號裡的條件一定會先評估。 例如，要尋找在公司擔任低階層或中階層工作且滿五年的員工，可以建構如下的 WHERE 子句：  
  
```  
WHERE   
   hire_date < '01/01/95' AND   
   (job_lvl = 100 OR job_lvl = 200)  
```  
  
> [!TIP]  
> 為了保持明確，AND 和 OR 合併使用時，建議您加上括號，不要依賴預設的優先順序。  
  
## <a name="how-and-works-with-multiple-or-clauses"></a>AND 和多個 OR 子句配合的方式  
了解 AND 和 OR 子句合併使用時的關聯方式，可幫助您建構及了解查詢和檢視設計工具中複雜的查詢。  
  
如果使用 AND 連結多個條件，以 AND 連結的第一組條件套用於第二組裡的所有條件。 換句話說，使用 AND 和其他條件連結的條件會分配至第二組裡的所有條件。 例如，以下圖說顯示的是連結至一組 OR 條件的 AND 條件：  
  
```  
A AND (B OR C)  
```  
  
以上式子在邏輯上等於下面的式子，顯示 AND 條件是如何分散至第二組條件的：  
  
```  
(A AND B) OR (A AND C)  
```  
  
此分散原則會影響使用查詢和檢視設計工具的方式。 例如，想像一下您要尋找已經在公司擔任低階層或中階層工作且滿五年的員工。 在 [SQL 窗格] 的陳述式中輸入以下的 WHERE 子句：  
  
```  
WHERE (hire_date < '01/01/95' ) AND   
   (job_lvl = 100 OR job_lvl = 200)  
```  
  
以 AND 連結的子句會套用至以 OR 連結的兩個子句。 明確表示這種情形的方法是在 OR 子句裡的每一個條件重複一次 AND 條件。 以下的陳述式比前面的陳述式更明確 (也更長)，但是在邏輯上相等：  
  
```  
WHERE    (hire_date < '01/01/95' ) AND  
  (job_lvl = 100) OR   
  (hire_date < '01/01/95' ) AND   
  (job_lvl = 200)  
```  
  
不論有多少個個別的條件，將 AND 子句分散至連結的 OR 子句的原則都適用。 例如，想像您要尋找在公司任職已滿五年或已退休的高階層或中階層員工。 WHERE 子句看起來應該像是這樣：  
  
```  
WHERE   
   (job_lvl = 200 OR job_lvl = 300) AND  
   (hire_date < '01/01/95' ) OR (status = 'R')  
```  
  
分散了使用 AND 連結的條件以後，WHERE 子句看起來就像這樣：  
  
```  
WHERE   
   (job_lvl = 200 AND hire_date < '01/01/95' ) OR  
   (job_lvl = 200 AND status = 'R') OR  
   (job_lvl = 300 AND hire_date < '01/01/95' ) OR  
   (job_lvl = 300 AND status = 'R')  
```  
  
## <a name="how-multiple-and-and-or-clauses-are-represented-in-the-criteria-pane"></a>多個 AND 和 OR 子句在準則窗格中表示的方式  
查詢和檢視設計工具會在 [準則窗格](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)中表示您的搜尋條件。 然而，如果以 AND 和 OR 連結多個子句，[準則窗格] 中呈現的可能就不是您所預料的結果。 此外，若您在 [準則窗格] 或 [圖表窗格](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md)中修改查詢，您可能會發現您的 SQL 陳述式已經變更，與您所輸入的不同。  
  
一般而言，這些規則指示了 AND 和 OR 子句在 [準則窗格] 中顯示的方式：  
  
-   所有使用 AND 連結的條件都會顯示在 [篩選]**** 格線欄或同一個 [或...]**** 資料欄中。  
  
-   所有使用 OR 連結的條件都會顯示在不同的 [或...]**** 資料欄中。  
  
-   如果 AND 和 OR 子句合併的邏輯結果是 AND 分散至數個 OR 子句，[準則窗格] 會以需要的次數重複 AND 子句，以明確表示這一點。  
  
例如，您可以在 [SQL 窗格] 中建立如下的搜尋條件，利用 AND 連結的兩個子句優先於使用 OR 連結的第三個子句：  
  
```  
WHERE (hire_date < '01/01/95' ) AND   
  (job_lvl = 100) OR   
  (status = 'R')  
```  
  
查詢和檢視設計工具會在 [準則窗格] 中如下顯示此 WHERE 子句：  
  
![準則窗格中的 OR 子句優先順序](../../ssms/visual-db-tools/media/vs_criteriapane1.gif "準則窗格中的 OR 子句優先順序")  
  
但是，如果連結的 OR 子句優先於 AND 子句，將會為每一個 OR 子句重複 AND 子句。 這會使得 AND 子句分散至每一個 OR 子句。 例如，您可以在 [SQL 窗格] 中建立如下所示的 WHERE 子句：  
  
```  
WHERE (hire_date < '01/01/95' ) AND   
  ( (job_lvl = 100) OR   
  (status = 'R') )  
```  
  
查詢和檢視設計工具會在 [準則窗格] 中如下顯示此 WHERE 子句：  
  
![準則窗格中的多個 AND 和 OR 子句](../../ssms/visual-db-tools/media/vs_criteriapane2.gif "準則窗格中的多個 AND 和 OR 子句")  
  
如果連結的 OR 子句只牽涉到一個資料行，查詢和檢視設計工具可以將整個 OR 子句放入方格的單一資料格內，避免重複 AND 子句的必要。 例如，您可以在 [SQL 窗格] 中建立如下所示的 WHERE 子句：  
  
```  
WHERE (hire_date < '01/01/95' ) AND   
  ((status = 'R') OR (status = 'A'))  
```  
  
查詢和檢視設計工具會在 [準則窗格] 中如下顯示此 WHERE 子句：  
  
![準則窗格中定義的連結 OR 子句](../../ssms/visual-db-tools/media/vs_criteriapane3.gif "準則窗格中定義的連結 OR 子句")  
  
如果您變更查詢 (例如變更 [準則窗格] 中的其中一個值)，查詢和檢視設計工具會在 [SQL 窗格] 中重建 SQL 陳述式。 重建的 SQL 陳述式和 [準則窗格] 中顯示的內容類似，而不是和原始陳述式類似。 例如，[準則窗格] 中如果包含了分散式 AND 子句，[SQL 窗格] 中產生的陳述式將會以明確的分散式 AND 子句重建。 如需詳細資訊，請參閱此主題中的＜AND 和多個 OR 子句配合的方式＞。  
  
## <a name="see-also"></a>另請參閱  
[指定搜尋準則 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
  
