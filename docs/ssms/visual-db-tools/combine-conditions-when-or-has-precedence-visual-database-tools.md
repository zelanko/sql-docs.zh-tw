---
title: "在 OR 具有優先權時結合條件 (Visual Database Tools) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssms-visual-db
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- search conditions [SQL Server], combining
- precedence [SQL Server], Criteria pane
- search criteria [SQL Server], combining conditions
- combining search conditions
- OR operator
ms.assetid: b30f5ac9-25e7-4163-80ed-44e4bccb455d
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5f8852df6a617323c69741eebd7c9c1475f4f054
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="combine-conditions-when-or-has-precedence-visual-database-tools"></a>在 OR 具有優先權時結合條件 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] 若要使用 OR 來連結條件，並使其優先權超越使用 AND 連結的條件，則必須在每個 OR 條件中重複 AND 條件。  
  
例如，假設您想要尋找已經在公司工作超過五年，而且在低階工作或已退休的員工。 這一查詢需要三個條件，其中一個條件連結至兩個具有 AND 的其他條件：  
  
-   雇用日期在五年之前的員工，以及  
  
-   工作層級為 100 或其狀態為 "R" (已退休) 的員工。  
  
下列程序說明如何在 [準則] 窗格中建立這種查詢。  
  
### <a name="to-combine-conditions-when-or-has-precedence"></a>若要在 OR 具有優先權時結合條件  
  
1.  在 [準則窗格](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)中，新增想要搜尋的資料行。 若要搜尋使用由 AND 所連結的兩個或多個條件之相同資料行，就必須針對想要搜尋的每個值，將資料行名稱加入方格中。  
  
2.  在 [篩選條件] 方格資料行中輸入第一個條件，在另一個 [或...] 資料行中輸入第二個 (及後續其他的) 條件，即可建立使用 OR 連結的條件。 例如，若要使用 OR 連結搜尋 `job_lvl` 和 `status` 資料行的條件，請在 `job_lvl` 的 [篩選條件] 資料行輸入 `= 100`，在 `status` 的 [或...] 資料行輸入 `= 'R'`。  
  
    輸入上述方格中的值，會在 [SQL] 窗格的陳述式中產生下列 WHERE 子句：  
  
    ```  
    WHERE (job_lvl = 100) OR (status = 'R')  
    ```  
  
3.  藉由輸入每個 OR 條件的 AND 條件，即可建立此條件。 將每個項目放入相同的方格資料行中，做為它所對應的 OR 條件。 例如，若要新增搜尋 `hire_date` 資料行並套用至這兩個 OR 條件的 AND 條件，請在 [準則] 資料行和 [或...] 資料行中輸入 `< '1/1/91'`。  
  
    輸入上述方格中的值，會在 [SQL] 窗格的陳述式中產生下列 WHERE 子句：  
  
    ```  
    WHERE (job_lvl = 100) AND   
      (hire_date < '01/01/91' ) OR  
      (status = 'R') AND   
      (hire_date < '01/01/91' )  
    ```  
  
    > [!TIP]  
    > 您可以藉由新增 AND 條件，然後使用 [編輯] 功能表的 [剪下] 和 [貼上] 命令來重複此條件，即可在其他 OR 條件中重複此條件。  
  
查詢和檢視表設計師所建立的 WHERE 子句相當於下列 WHERE 子句，其中使用括號來指定 OR 的優先權高於 AND：  
  
```  
WHERE (job_lvl = 100 OR status = 'R') AND  
   (hire_date < '01/01/91')  
```  
  
> [!NOTE]  
> 如果您使用緊接在 [SQL 窗格](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md)之上的格式輸入搜尋條件，然後變更 [圖表] 或 [準則] 窗格中的查詢，則查詢和檢視表設計工具會重新建立 SQL 陳述式，以便讓格式與明確散發給兩個 OR 條件的 AND 條件相符。  
  
## <a name="see-also"></a>另請參閱  
[在條件窗格中合併搜尋條件的慣例 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/conventions-combine-search-conditions-in-criteria-pane-visual-db-tools.md)  
[指定搜尋準則 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
  
