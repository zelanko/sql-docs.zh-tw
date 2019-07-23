---
title: 指定多重資料行的多重搜尋條件 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- search criteria [SQL Server], multiple conditions
- multiple search conditions
- search conditions [SQL Server], multiple
- OR operator
- AND, Criteria pane
ms.assetid: 06617729-0d0b-4da2-9890-b7e2f5cdbc7b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 1110e4ae1ca4268af611cbb039af2b148694b552
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265496"
---
# <a name="specify-multiple-search-conditions-for-multiple-columns-visual-database-tools"></a>指定多重資料行的多重搜尋條件 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
藉由包含幾個資料行做為搜尋條件的一部分，可以擴展或縮小查詢的範圍。 例如，您可能要：  
  
-   搜尋在公司工作超過五年或維持特定工作的員工。  
  
-   搜尋由特定發行者所發行有關烹飪的書籍。  
  
若要建立搜尋兩個 (或多個) 資料行中值的查詢，可以指定 OR 條件。 若要建立必須符合兩個 (或多個) 資料行中所有條件的查詢，可以指定 AND 條件。  
  
## <a name="specifying-an-or-condition"></a>指定 OR 條件  
若要建立使用 OR 連結的多重條件，請將個別條件放在 [準則] 窗格中的不同資料行。  
  
#### <a name="to-specify-an-or-condition-for-two-different-columns"></a>若要指定兩個不同資料行的 OR 條件  
  
1.  在[準則窗格](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)中，新增想要搜尋的資料行。  
  
2.  在想要搜尋的第一個資料行的 [篩選條件]  資料行中，指定第一個條件。  
  
3.  在要搜尋的第二個資料行之 [或...]  資料行中，指定第二個條件，請將 [篩選條件]  資料行保留空白。  
  
    [查詢和檢視表設計工具] 會建立包含 OR 條件的 WHERE 子句，如下所示：  
  
    ```  
    SELECT job_lvl, hire_date  
    FROM employee  
    WHERE (job_lvl >= 200) OR   
      (hire_date < '01/01/1998')  
    ```  
  
4.  對想要加入的每個額外條件重複步驟 2 和 3。 為每個新增的條件使用不同的 [或...]  資料行。  
  
## <a name="specifying-an-and-condition"></a>指定 AND 條件  
若要搜尋使用 AND 連結條件的不同資料行，請將所有條件放入方格的 [篩選條件]  資料行。  
  
#### <a name="to-specify-an-and-condition-for-two-different-columns"></a>若要指定兩個不同資料行的 AND 條件  
  
1.  在 [準則窗格](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)中，新增想要搜尋的資料行。  
  
2.  在想要搜尋的第一個資料行的 [篩選條件]  資料行中，指定第一個條件。  
  
3.  在第二個資料行的 [篩選條件]  資料行中，指定第二個條件。  
  
    查詢與檢視設計工具會建立 WHERE 子句，其中包含 AND 條件，如下所示：  
  
    ```  
    SELECT pub_id, title  
    FROM titles  
    WHERE (pub_id = '0877') AND (title LIKE '%Cook%')  
    ```  
  
4.  對想要加入的每個額外條件重複步驟 2 和 3。  
  
## <a name="see-also"></a>另請參閱  
[在 AND 具有優先權時結合條件 (Visual Database Tools)](../../ssms/visual-db-tools/combine-conditions-when-and-has-precedence-visual-database-tools.md)  
[在 OR 具有優先權時結合條件 (Visual Database Tools)](../../ssms/visual-db-tools/combine-conditions-when-or-has-precedence-visual-database-tools.md)  
[在條件窗格中合併搜尋條件的慣例 (Visual Database Tools)](../../ssms/visual-db-tools/conventions-combine-search-conditions-in-criteria-pane-visual-db-tools.md)  
[指定搜尋條件 (Visual Database Tools)](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
  
