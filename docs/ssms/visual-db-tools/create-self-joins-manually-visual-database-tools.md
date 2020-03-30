---
title: 手動建立自我聯結
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- self-joins
- manual joins [SQL Server]
- joins [SQL Server], self
ms.assetid: 910ed516-cb84-481b-95d0-cba3e89afdba
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.openlocfilehash: 57ceb0963f303a1674642b65ef6c2089fd86ef70
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "75254246"
---
# <a name="create-self-joins-manually-visual-database-tools"></a>手動建立自我聯結 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
即使資料表沒有資料庫中的自反關聯性，也可以將資料表聯結至它本身。 例如，可以使用自我聯結 (Self-Join) 來找出住在同一城市的作者。  
  
如同任何聯結一樣，自我聯結至少需要兩個資料表。 其差異在於並未將第二個資料表加入查詢中，而是加入同一資料表的第二個執行個體。 如此就可以比較資料表第一個執行個體的資料行，與第二個執行個體中的同一資料行，以便讓您比較資料行中的各值。 [查詢和檢視表設計工具](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) 會指派別名給資料表的第二個執行個體。  
  
例如，若要建立自我聯結以找出住在 Berkeley 的所有作者對，您可以比較資料表第一個執行個體中的 `city` 資料行與第二個執行個體中的 `city` 資料行。 產生的查詢可能如下所示：  
  
```  
SELECT   
         authors.au_fname,   
         authors.au_lname,   
         authors1.au_fname AS Expr2,   
         authors1.au_lname AS Expr3  
      FROM   
         authors   
            INNER JOIN  
            authors authors1   
               ON authors.city   
                = authors1.city  
      WHERE  
         authors.city = 'Berkeley'  
```  
  
建立自我聯結通常需要多重聯結條件。 若要暸解其原因，請考量先前查詢的結果：  
  
```  
Cheryl Carson       Cheryl Carson  
   Abraham Bennet      Abraham Bennet  
   Cheryl Carson       Abraham Bennet  
   Abraham Bennet      Cheryl Carson  
```  
  
第一個資料列毫無用處，其中指出 Cheryl Carson 與 Cheryl Carson 住在同一城市。 第二個資料列也毫無用處。 若要消除這些無用的資料，可以加入另一個條件，使其只保留作者姓名不同的結果資料列。 產生的查詢可能如下所示：  
  
```  
SELECT   
         authors.au_fname,   
         authors.au_lname,   
         authors1.au_fname AS Expr2,   
         authors1.au_lname AS Expr3  
      FROM   
         authors   
            INNER JOIN  
            authors authors1   
               ON authors.city   
                = authors1.city  
               AND authors.au_id  
                <> authors1.au_id  
      WHERE  
         authors.city = 'Berkeley'  
```  
  
結果集則改善為：  
  
```  
Cheryl Carson       Abraham Bennet  
   Abraham Bennet      Cheryl Carson  
```  
  
但這兩個資料列互為冗餘。 第一個資料列說明 Carson 與 Bennet 住在同一城市，第二個資料列則說明 Bennet 與 Carson 住在同一城市。 若要消除這種冗餘，可以將第二個聯結條件由 "not equals"變更為 " less than"。 產生的查詢可能如下所示：  
  
```  
SELECT   
         authors.au_fname,   
         authors.au_lname,   
         authors1.au_fname AS Expr2,   
         authors1.au_lname AS Expr3  
      FROM   
         authors   
            INNER JOIN  
            authors authors1   
               ON authors.city   
                = authors1.city  
               AND authors.au_id  
                < authors1.au_id  
      WHERE  
         authors.city = 'Berkeley'  
```  
  
結果集則如下所示：  
  
```  
Cheryl Carson       Abraham Bennet  
```  
  
### <a name="to-create-a-self-join-manually"></a>手動建立自我聯結  
  
1.  將要使用的資料表或資料表值物件新增至 [圖表窗格](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md) 中。  
  
2.  再加入同一資料表，使 [圖表] 窗格顯示兩次相同的資料表或資料表值物件。  
  
    查詢和檢視設計師藉由在資料表名稱加入連續編號，來指派第二個執行個體的別名。 此外，[查詢和檢視設計師] 會在 [圖表] 窗格的兩個資料表或資料表值物件之間建立聯結線。  
  
3.  在聯結線上按一下滑鼠右鍵，然後在捷徑功能表中選擇 [屬性]  。  
  
4.  在 [屬性] 視窗中，按一下 [聯結條件及類型]  ，再按一下屬性右邊的省略符號 ([...]  )。  
  
5.  在[聯結對話方塊](../../ssms/visual-db-tools/join-dialog-box-visual-database-tools.md)中，在必要時變更主索引鍵之間的比較運算子。 例如，您可以會將運算子變更為小於 (<)。  
  
6.  將資料表或資料表值物件的第一個執行個體的主聯結 (Primary Join) 資料行名稱，拖放至第二個執行個體的對應資料行，即可建立其他聯結條件 (例如，authors.zip = authors1.zip)。  
  
7.  指定查詢的其他選項，例如輸出資料行、搜尋條件和排序順序。  
  
## <a name="see-also"></a>另請參閱  
[自動建立自我聯結 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/create-self-joins-automatically-visual-database-tools.md)  
[使用聯結查詢 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md)  
  
