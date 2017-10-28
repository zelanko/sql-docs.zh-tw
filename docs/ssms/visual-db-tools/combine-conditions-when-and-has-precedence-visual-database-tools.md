---
title: "在 AND 具有優先權時結合條件 (Visual Database Tools) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- search conditions [SQL Server], combining
- precedence [SQL Server], Criteria pane
- search criteria [SQL Server], combining conditions
- combining search conditions
- AND, Criteria pane
ms.assetid: 450eb2eb-6ea3-405b-8dd2-1ff926c016e7
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 8c8d08365ac129d8b43e49d166ffccd866396c37
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="combine-conditions-when-and-has-precedence-visual-database-tools"></a>在 AND 具有優先權時結合條件 (Visual Database Tools)
若要使用 AND 結合條件，請將資料行加入至查詢兩次，每一個條件一次。 若要使用 OR 結合條件，請將第一個條件放入 [篩選條件] 資料行，其他條件則放入 [或...] 資料行。  
  
例如，假設要尋找公司中已經擔任低階工作超過五年的員工，或不論其雇用日期負責中階工作的員工。 此一查詢需要三個條件，其中兩個以 AND 連結：  
  
-   雇用日期早於五年前且工作層級為 100 的員工。  
  
    -或-  
  
-   工作層級為 200 的員工。  
  
### <a name="to-combine-conditions-when-and-has-precedence"></a>若要在 AND 具有優先權時結合條件  
  
1.  在 [準則窗格](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)中，新增想要搜尋的資料行。 若要搜尋使用由 AND 所連結的兩個或多個條件之相同資料行，就必須針對想要搜尋的每個值，將資料行名稱加入方格中。  
  
2.  在 [篩選條件] 資料行，輸入想要使用 AND 連結的所有條件。 例如，若要以 AND 連結搜尋 `hire_date` 和 `job_lvl` 資料行的條件，請在 [篩選條件] 資料行分別輸入值 `< '1/1/91'` 和 `= 100`。  
  
    這些方格項目會在 [SQL 窗格](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md)的陳述式中產生下列 WHERE 子句：  
  
    ```  
    WHERE (hire_date < '01/01/91') AND  
      (job_lvl = 100)  
    ```  
  
3.  在 [或...] 方格資料行中，輸入想要使用 OR 連結的條件。 例如，若要新增搜尋 `job_lvl` 資料行中其他值的條件，請在 [或...] 資料行中輸入其他值，例如 `= 200`。  
  
    在 [或...] 資料行中新增一個值，就會在 SQL 窗格中將另一個條件新增至陳述式中的 WHERE 子句：  
  
    ```  
    WHERE (hire_date < '01/01/91' ) AND  
      (job_lvl = 100) OR   
      (job_lvl = 200)  
    ```  
  
## <a name="see-also"></a>另請參閱  
[在 OR 具有優先權時結合條件 (Visual Database Tools)](../../ssms/visual-db-tools/combine-conditions-when-or-has-precedence-visual-database-tools.md)  
[在條件窗格中合併搜尋條件的慣例 (Visual Database Tools)](../../ssms/visual-db-tools/conventions-combine-search-conditions-in-criteria-pane-visual-db-tools.md)  
[輸入搜尋值的規則 (Visual Database Tools)](../../ssms/visual-db-tools/rules-for-entering-search-values-visual-database-tools.md)  
[指定搜尋條件 (Visual Database Tools)](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
  

