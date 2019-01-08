---
title: 在結果窗格中加入新的資料列 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- View Designer, Results pane
- inserting rows
- Query Designer [SQL Server], Results pane
- Results pane
- adding rows
- row additions [SQL Server], Results pane
ms.assetid: 59891c84-3f54-4ab9-8b86-72c59627b480
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cda813db916faf4819f85d3d09213679fba2eeec
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52801590"
---
# <a name="add-new-rows-in-the-results-pane-visual-database-tools"></a>在結果窗格中加入新的資料列 (Visual Database Tools)
  您可以利用輸入或是從其他諸如「記事本」或 Excel 程式貼上的方式，加入新的資料。 要貼上資料列必須要有與貼入的資料表完全相同的資料行數目和類型。 多重資料列可一併貼上至 [結果] 窗格。  
  
 如需如何輸入資料的資訊，請參閱 [更新結果的規則 &#40;Visual Database Tools&#41;](visual-database-tools.md)。  
  
### <a name="to-add-a-new-data-row"></a>若要加入新資料列  
  
1.  導覽至 [結果] 窗格下方，有空白資料列可加入新的資料列之處。  
  
     所有資料行的初始值皆為 *NULL*。  
  
    > [!TIP]  
    >  若要直接移至第一個空白資料列，請使用位於 [結果] 窗格底部的導覽列。  
  
2.  若要把剪貼簿中的資料列貼上，按一下新資料列左邊的按鈕，加以選取。  
  
    > [!NOTE]  
    >  如果所貼上的一或多個資料列無法為資料庫認可，您將會收到通知哪些資料列不被認可的訊息。  
  
3.  輸入新資料列的資料。 若要貼上，請從 [編輯] 功能表選擇 [貼上]。  
  
4.  離開該資料列，讓資料庫對其進行認可。  
  
 儲存資料列時如果發生錯誤，查詢和檢視設計工具會顯示訊息，然後讓您返回先前所編輯的資料列。 您可以：  
  
-   進一步編輯資料列來解決錯誤。  
  
-   按一下 ESC 鍵來取消編輯。 如果是在變更過的資料格中按 ESC 鍵，那麼該資料格中的變更會取消。 如果在沒有變更的資料格中按 ESC 鍵，整個資料列的變更都會取消。  
  
## <a name="see-also"></a>另請參閱  
 [在 [結果] 窗格中的資料搭配使用&#40;Visual Database Tools&#41;](results-pane-visual-database-tools.md)   
 [使用查詢執行基本作業 &#40;Visual Database Tools&#41;](perform-basic-operations-with-queries-visual-database-tools.md)  
  
  
