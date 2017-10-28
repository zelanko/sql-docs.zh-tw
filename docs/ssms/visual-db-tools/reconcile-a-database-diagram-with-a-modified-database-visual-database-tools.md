---
title: "使用修改的資料庫協調資料庫圖表 | Microsoft Docs"
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
- updating diagram to match database
- reconciling database diagrams
- diagrams [SQL Server], reconciling changes
- updating database to match diagram
- database diagrams [SQL Server], reconciling changes
ms.assetid: eda8dea2-eedd-43a7-85aa-92bd97783b5f
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 38ef2e93566791eeb1963b02792942ec5450031d
ms.contentlocale: zh-tw
ms.lasthandoff: 08/18/2017

---
# <a name="reconcile-a-database-diagram-with-a-modified-database-visual-database-tools"></a>使用修改的資料庫協調資料庫圖表 (Visual Database Tools)
當您準備開始更新資料庫以便與圖表相符時，您可以儲存資料庫圖表。 但是，在您開啟圖表之後，如果其他使用者更新資料庫，他們所做的變更可能會影響您的圖表，反之亦然。  
  
儲存圖表會覆寫其他使用者的變更，讓資料庫符合您的圖表，以便使資料庫與圖表趨於一致。  
  
### <a name="to-update-a-database-to-match-your-diagram"></a>若要更新資料庫以便與圖表相符  
  
1.  儲存您的資料庫圖表。  
  
    如果您先前未儲存圖表，請在 [儲存新資料庫圖表] 對話方塊中輸入圖表名稱，再選擇 [確定]。  
  
2.  [儲存] 對話方塊會列出儲存圖表時會影響的資料表。 選擇 [是] 繼續進行。  
  
3.  [偵測到資料庫變更] 對話方塊會列出修改的物件，這些物件將會變更，以符合您的圖表。 選擇 [是] 儲存圖表，並接受變更的清單。  
  
    > [!NOTE]  
    > 如果您的圖表包含已經在資料庫中刪除的資料表和資料行，儲存圖表時只會在資料庫中重新建立這些物件的定義。 此程序不會還原刪除這些物件之前就存在於物件中的任何資料。  
  
### <a name="to-update-your-diagram-to-match-a-modified-database"></a>若要更新圖表以便與修改的資料庫相符  
  
1.  關閉圖表而不儲存變更。  
  
2.  在 [物件總管] 的圖表上按一下滑鼠右鍵。  
  
3.  從快速鍵功能表按一下 [重新整理]。  
  
4.  重新開啟圖表。  
  
## <a name="see-also"></a>另請參閱  
[使用資料庫圖表 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/work-with-database-diagrams-visual-database-tools.md)  
  

