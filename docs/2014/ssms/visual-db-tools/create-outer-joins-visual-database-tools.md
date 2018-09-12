---
title: 建立外部聯結 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- outer joins
- joins [SQL Server], outer
ms.assetid: 18de47b1-f936-427d-b852-fe6d20334f71
caps.latest.revision: 12
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f827436a29b0f1a821ea3e707d498f13e41dd2e6
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/06/2018
ms.locfileid: "43818314"
---
# <a name="create-outer-joins-visual-database-tools"></a>建立外部聯結 (Visual Database Tools)
  在預設狀況下， [查詢和檢視表設計工具](visual-database-tools.md) 會在資料表之間建立內部聯結 (Inner Join)。 內部聯結將刪除不符合其他資料表之資料列的資料列。 然而，外部聯結則至少傳回 FROM 子句提到的一個資料表或檢視，只要這些資料列符合任何 WHERE 或 HAVING 搜尋條件。 若要在不具有符合聯結資料表中資料的結果集中包含資料列，就可以建立外部聯結。  
  
 在建立外部聯結時，資料表在 SQL 陳述式中出現的順序 (如 SQL 窗格所反映) 非常重要。 您加入的第一個資料表會成為「左」資料表，第二個資料表會成為「右」資料表  (資料表出現在[圖表窗格](diagram-pane-visual-database-tools.md)的實際順序並不重要)。在指定左或右外部聯結時，是指這些資料表加入查詢時的順序，以及它們出現在 [SQL 窗格](sql-pane-visual-database-tools.md)的 SQL 陳述式中的順序。  
  
### <a name="to-create-an-outer-join"></a>若要建立外部聯結  
  
1.  自動或手動建立聯結。 如需詳細資訊，請參閱[自動聯結資料表 &#40;Visual Database Tools&#41;](join-tables-automatically-visual-database-tools.md) 或[手動聯結資料表 &#40;Visual Database Tools&#41;](join-tables-manually-visual-database-tools.md)。  
  
2.  在 圖表 窗格中，然後再從選取的聯結線**查詢設計工具** 功能表中，選擇**選取所有資料列\<tablename >**，其額外選取包含資料表的命令您想要包含的資料列。  
  
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
 [使用聯結查詢&#40;Visual Database Tools&#41;](query-with-joins-visual-database-tools.md)   
 [聯結對話方塊 &#40;Visual Database Tools&#41;](join-dialog-box-visual-database-tools.md)  
  
  
