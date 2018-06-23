---
title: 工作 3： 針對清理資料供應商知識庫 |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 647c924a-9b91-4294-8d96-e81416e4e90e
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: ca1a98045bd9f0ee9dfc52eafb274d5698195d68
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36030410"
---
# <a name="task-3-cleansing-data-against-the-suppliers-knowledge-base"></a>工作 3：針對供應商知識庫清理資料
  在這項工作中，您會執行電腦輔助的清理程序。 DQS 會根據為了針對選取的知識庫分析及清理資料所指定的臨界值，使用進階演算法與信賴等級。 請參閱[清理資料使用 DQS （內部） 知識](http://msdn.microsoft.com/library/hh213061.aspx)如需詳細資訊。  
  
1.  按一下**啟動**啟動電腦輔助的清理程序。  
  
     ![清理 頁面的清理程序](../../2014/tutorials/media/et-cleansingdataagainstthesupplierkb-01.jpg "清理 頁面的清理程序")  
  
2.  將清理程序完成時，檢閱**統計資料**中**Profiler**  索引標籤。來源統計資料 會提供已處理的記錄數、發現正確的記錄數、DQS 更正的記錄數、套用 DQS 建議之變更的記錄數，以及無效的記錄數。 在右邊的清單方塊中，您可以看到清理程序中每一個相關定義域的更正值、建議值及完整性 (資料存在的程度) 和精確度 (資料可用於預定用途的程度) 等值。  
  
     ![清理結果](../../2014/tutorials/media/et-cleansingdataagainstthesupplierkb-02.jpg "清理結果")  
  
3.  按一下**下一步**切換至**管理和檢視結果**頁面。  
  
## <a name="next-step"></a>下一個步驟  
 [工作 4： 管理和檢視結果](../../2014/tutorials/task-4-manaing-and-viewing-results.md)  
  
  