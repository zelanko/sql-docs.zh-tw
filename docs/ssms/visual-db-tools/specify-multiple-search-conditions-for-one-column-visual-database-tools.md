---
title: "指定單一資料行的多重搜尋條件 | Microsoft Docs"
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
- search criteria [SQL Server], multiple conditions
- multiple search conditions
- search conditions [SQL Server], multiple
- OR operator
- AND, Criteria pane
ms.assetid: 2c006e36-56b1-4992-89b4-c6c0b19808f3
caps.latest.revision: 3
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: a7b140acf1b00f31df0d8c948cdeca8ff6703726
ms.contentlocale: zh-tw
ms.lasthandoff: 08/18/2017

---
# <a name="specify-multiple-search-conditions-for-one-column-visual-database-tools"></a>指定單一資料行的多重搜尋條件 (Visual Database Tools)
在一些執行個體中，可能要套用許多搜尋條件至相同的資料行。 例如，您可能要：  
  
-   搜尋 `employee` 資料表中幾個不同的名稱，或在不同薪資範圍的員工。 這種搜尋需要 OR 條件。  
  
-   搜尋以文字 "The" 為開頭並包含文字 "Cook" 的書名。 這種搜尋需要 AND 條件。  
  
> [!NOTE]  
> 此主題的資訊適用於查詢的 WHERE 和 HAVING 子句中的搜尋條件。 本範例集中在建立 WHERE 子句，但上述原則仍可套用至兩種搜尋條件。  
  
若要搜尋同一資料行的其他值，可以指定 OR 條件。 若要搜尋符合幾個條件的值，可以指定 AND 條件。  
  
## <a name="specifying-an-or-condition"></a>指定 OR 條件  
使用 OR 條件可讓您指定搜尋資料行中的幾個其他值。 這一選項會擴展搜尋的範圍，並可傳回比搜尋單一值還多的資料列。  
  
> [!TIP]  
> 您可以經常改用 IN 運算子來搜尋同一資料行中的多重值。  
  
#### <a name="to-specify-an-or-condition"></a>若要指定 OR 條件  
  
1.  在[準則窗格](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)中，新增要搜尋的資料行。  
  
2.  在剛新增的資料行的 [篩選條件] 資料行中，指定第一個條件。  
  
3.  在相同資料行的 [**或...**] 資料行中，指定第二個條件。  
  
[查詢和檢視表設計工具] 會建立包含 OR 條件的 WHERE 子句，如下所示：  
  
```  
SELECT fname, lname  
FROM employees  
WHERE (salary < 30000) OR (salary > 100000)  
```  
  
## <a name="specifying-an-and-condition"></a>指定 AND 條件  
使用 AND 條件可讓指定資料行中的值必須符合包含在結果集中資料列兩個 (或更多) 的條件。 這一選項會縮小搜尋的範圍，通常傳回的資料列比搜尋單一值還少。  
  
> [!TIP]  
> 如果您在搜尋某範圍的值，可改用 BETWEEN 運算子以 AND 連結兩個條件。  
  
#### <a name="to-specify-an-and-condition"></a>若要指定 AND 條件  
  
1.  在 [準則] 窗格中，加入要搜尋的資料行。  
  
2.  在剛新增的資料行的 [篩選條件] 資料行中，指定第一個條件。  
  
3.  再將相同的資料行加入 [準則] 窗格，將它放在方格的空資料列中。  
  
4.  在資料行的第二個執行個體的 [篩選條件] 欄位中，指定第二個條件。  
  
查詢設計工具會建立 WHERE 子句，其中包含 AND 條件，如下所示：  
  
```  
SELECT title_id, title  
FROM titles  
WHERE (title LIKE '%Cook%') AND   
  (title LIKE '%Recipe%')  
```  
  
## <a name="see-also"></a>另請參閱  
[在條件窗格中合併搜尋條件的慣例 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/conventions-combine-search-conditions-in-criteria-pane-visual-db-tools.md)  
[指定搜尋準則 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
  

