---
title: 建立刪除查詢 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- row removal [SQL Server], Delete query
- Delete query
- queries [SQL Server], types
- removing rows
- removing data
- data deletions [SQL Server]
- deleting rows
- deleting data
ms.assetid: 0db3af43-1ec4-48c8-b769-2bb9c76d3434
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f1103e1715c01cfc868c59af17ee0f95fa7cedff
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62661682"
---
# <a name="create-delete-queries-visual-database-tools"></a>建立刪除查詢 (Visual Database Tools)
  您可以使用刪除查詢 (Delete Query) 刪除資料表中的所有資料列。  
  
> [!NOTE]  
>  從資料表中刪除所有資料列可清除資料表中的資料，但不會刪除資料表本身。 若要將資料表從資料庫中刪除，請在物件總管的資料表上按一下滑鼠右鍵，並且按一下 [刪除]  。  
  
 建立刪除查詢時，[準則] 窗格將會變更，以反映可以用來刪除資料列的選項。 由於您不會在刪除查詢中顯示資料，因此 [輸出]、[排序依據] 和 [排序次序] 等資料行都會移除。 此外，在表示資料表或資料表值物件的矩形中，資料行名稱旁邊的核取方塊也會移除，因為您無法個別指定要刪除的資料行。  
  
 如果 [查詢和檢視設計師] 無法刪除一個或多個資料列，它便不會刪除任何資料列，您會收到訊息說明哪些資料列包含無法從資料庫刪除的資訊。  
  
> [!CAUTION]  
>  您無法恢復執行刪除查詢的動作。 為求安全起見，在執行刪除查詢之前，請先備份資料。  
  
### <a name="to-create-a-delete-query"></a>若要建立刪除查詢  
  
1.  將要刪除資料列的來源資料表加入至 [圖表] 窗格中。  
  
2.  從 [查詢設計工具]  功能表中，指向 [變更類型]  ，然後按一下 [刪除]  。 **注意**：在啟動刪除查詢時，如果 [圖表] 窗格中顯示一個以上的資料表，查詢和檢視設計師就會顯示[刪除資料表對話方塊](visual-database-tools.md)，提示您輸入要刪除資料列的資料表名稱。  
  
 執行刪除查詢時， [結果窗格](results-pane-visual-database-tools.md)不會報告任何結果。 但是畫面會出現訊息，指出已經刪除的資料列數目。  
  
## <a name="see-also"></a>另請參閱  
 [支援的查詢類型 &#40;Visual Database Tools&#41;](supported-query-types-visual-database-tools.md)   
 [設計查詢和檢視使用說明主題 &#40;Visual Database Tools&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
  
