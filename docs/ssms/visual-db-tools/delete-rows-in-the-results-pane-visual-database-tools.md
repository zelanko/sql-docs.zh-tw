---
title: "刪除結果窗格中的資料列 (Visual Database Tools) | Microsoft Docs"
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
- View Designer, Results pane
- removing rows
- row removal [SQL Server], Visual Database Tools Results pane
- row deletions [SQL Server], Visual Database Tools Results pane
- Query Designer [SQL Server], Results pane
- deleting rows
- Results pane
ms.assetid: a1147905-fe4a-4fac-b576-a17622477e66
caps.latest.revision: 3
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: cef300f5851e64620787d1dec2ca0b2d6fe114f9
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="delete-rows-in-the-results-pane-visual-database-tools"></a>刪除結果窗格中的資料列 (Visual Database Tools)
若要刪除資料庫中的資料錄，請刪除 [結果] 窗格中的資料列。 若要刪除所有的資料列，請使用刪除查詢。 如需詳細資訊，請參閱[建立製成資料表查詢 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/create-delete-queries-visual-database-tools.md)。 如果只是要從 [結果] 窗格移除資料列，請變更查詢的準則。 如需詳細資訊，請參閱[指定搜尋準則 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)。  
  
### <a name="to-delete-a-row-or-rows"></a>若要刪除資料列  
  
1.  在 [結果] 窗格中，選取要刪除的資料列左邊的方塊。  
  
2.  按下 DELETE 鍵。  
  
3.  在詢問確認的訊息方塊中，按一下 [是]。  
  
> [!CAUTION]  
> 用這種方式刪除的資料列，會永久自資料庫移除，無法重新叫用。  
  
> [!NOTE]  
> 如果選取的資料列中有任何一個無法從資料庫刪除，所有的資料列將都不會刪除，而且您會接收到通知哪個資料列無法刪除的訊息。  
  
## <a name="see-also"></a>另請參閱  
[建立製成資料表查詢 &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/create-delete-queries-visual-database-tools.md)  
[指定搜尋準則 &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
  

