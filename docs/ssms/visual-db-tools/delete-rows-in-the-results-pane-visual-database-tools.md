---
title: 刪除結果窗格中的資料列
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- View Designer, Results pane
- removing rows
- row removal [SQL Server], Visual Database Tools Results pane
- row deletions [SQL Server], Visual Database Tools Results pane
- Query Designer [SQL Server], Results pane
- deleting rows
- Results pane
ms.assetid: a1147905-fe4a-4fac-b576-a17622477e66
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 71e70000e6a4b1c6208e19f5d233f44fb31b965b
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/06/2020
ms.locfileid: "86008331"
---
# <a name="delete-rows-in-the-results-pane-visual-database-tools"></a>刪除結果窗格中的資料列 (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
若要刪除資料庫中的資料錄，請刪除 [結果] 窗格中的資料列。 若要刪除所有的資料列，請使用刪除查詢。 如需詳細資訊，請參閱 [建立製成資料表查詢 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/create-delete-queries-visual-database-tools.md)。 如果只是要從 [結果] 窗格移除資料列，請變更查詢的準則。 如需詳細資訊，請參閱 [指定搜尋準則 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)。  
  
### <a name="to-delete-a-row-or-rows"></a>若要刪除資料列  
  
1.  在 [結果] 窗格中，選取要刪除的資料列左邊的方塊。  
  
2.  按下 DELETE 鍵。  
  
3.  在詢問確認的訊息方塊中，按一下 [是]  。  
  
> [!CAUTION]  
> 用這種方式刪除的資料列，會永久自資料庫移除，無法重新叫用。  
  
> [!NOTE]  
> 如果選取的資料列中有任何一個無法從資料庫刪除，所有的資料列將都不會刪除，而且您會接收到通知哪個資料列無法刪除的訊息。  
  
## <a name="see-also"></a>另請參閱  
[建立製成資料表查詢 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/create-delete-queries-visual-database-tools.md)  
[指定搜尋準則 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
  
