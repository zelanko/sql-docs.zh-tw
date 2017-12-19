---
title: "建立外部聯結 (Visual Database Tools) | Microsoft Docs"
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
- outer joins
- joins [SQL Server], outer
ms.assetid: 18de47b1-f936-427d-b852-fe6d20334f71
caps.latest.revision: "3"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ccbda35c56aaa7aeb221ff3f0c7527b0389eebe8
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="create-outer-joins-visual-database-tools"></a>建立外部聯結 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] 在預設狀況下，[查詢和檢視表設計工具](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md)會在資料表之間建立內部聯結 (Inner Join)。 內部聯結將刪除不符合其他資料表之資料列的資料列。 然而，外部聯結則至少傳回 FROM 子句提到的一個資料表或檢視，只要這些資料列符合任何 WHERE 或 HAVING 搜尋條件。 若要在不具有符合聯結資料表中資料的結果集中包含資料列，就可以建立外部聯結。  
  
在建立外部聯結時，資料表在 SQL 陳述式中出現的順序 (如 SQL 窗格所反映) 非常重要。 您加入的第一個資料表會成為「左」資料表，第二個資料表會成為「右」資料表  (資料表出現在[圖表窗格](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md)的實際順序並不重要)。在指定左或右外部聯結時，是指這些資料表加入查詢時的順序，以及它們出現在 [SQL 窗格](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md)的 SQL 陳述式中的順序。  
  
### <a name="to-create-an-outer-join"></a>若要建立外部聯結  
  
1.  自動或手動建立聯結。 如需詳細資訊，請參閱[自動聯結資料表 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/join-tables-automatically-visual-database-tools.md) 或[手動聯結資料表 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/join-tables-manually-visual-database-tools.md)。  
  
2.  選取 [圖表] 窗格中的聯結線 (Join Line)，然後從 [查詢設計工具] 功能表選擇 [選取 <tablename> 中所有的資料列]，以選取包含您要併入其額外資料列之資料表的命令。  
  
    -   選擇第一個資料表以建立左外部聯結。  
  
    -   選擇第二個資料表以建立右外部聯結。  
  
    -   選擇兩個資料表以建立完整外部聯結 (Full Outer Join)。  
  
在指定外部聯結時，查詢和檢視設計師會修改聯結線以指出外部聯結。  
  
此外，查詢和檢視設計師會修改 [SQL] 窗格中的 SQL 陳述式，以反映聯結類型的變更，如下列陳述式所示：  
  
```  
SELECT employee.job_id, employee.emp_id,  
   employee.fname, employee.minit, jobs.job_desc  
FROM employee LEFT OUTER JOIN jobs ON   
    employee.job_id = jobs.job_id  
```  
  
因為外部聯結包含不符的資料列，因此可以用它來尋找違反外部索引鍵條件約束的資料列。 若要如此，可以建立外部聯結，然後加入搜尋條件，以尋找最右方的資料表中主索引鍵資料行為 null 的資料列。 例如，下列外部聯結會找出 `employee` 資料表中在 `jobs` 資料表沒有對應資料列的資料列：  
  
```  
SELECT employee.emp_id, employee.job_id  
FROM employee LEFT OUTER JOIN jobs   
   ON employee.job_id = jobs.job_id  
WHERE (jobs.job_id IS NULL)  
```  
  
## <a name="see-also"></a>另請參閱  
[使用聯結查詢 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md)  
[聯結對話方塊 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/join-dialog-box-visual-database-tools.md)  
  
