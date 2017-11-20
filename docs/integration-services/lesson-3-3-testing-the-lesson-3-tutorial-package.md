---
title: "步驟 3： 測試第 3 課的教學課程封裝 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 1096a476-93cf-4474-86f5-27d6357eb380
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: d6477267c95ffd200f70b2c93191dfaf0883a4af
ms.contentlocale: zh-tw
ms.lasthandoff: 09/26/2017

---
# <a name="lesson-3-3---testing-the-lesson-3-tutorial-package"></a>課程 3-3-測試第 3 課的教學課程封裝
在這項工作中，您將執行 Lesson 3.dtsx 封裝。 當封裝執行時，[記錄事件] 視窗會列出寫入記錄檔的記錄項目。 在封裝完成執行之後，您要確認記錄提供者所產生之記錄檔的內容。  
  
## <a name="checking-the-package-layout"></a>檢查封裝配置  
在測試封裝之前，您應該確認第 3 課封裝中的控制流程和資料流程是否包含下圖所顯示的物件。 其控制流程應該與第 2 課的控制流程相同。 資料流程應該與第 1 和第 2 課的資料流程相同。  
  
**控制流程**  
  
![控制流程封裝中](../integration-services/media/task4lesson2control.gif "控制流程封裝中")  
  
**資料流程**  
  
![封裝中的資料流程](../integration-services/media/task9lesson1data.gif "中封裝的資料流程")  
  
### <a name="to-run-the-lesson-4-tutorial-package"></a>若要執行第 4 課的教學課程封裝  
  
1.  在 [SSIS] 功能表上，按一下 [記錄事件]。  
  
2.  在 **[偵錯]** 功能表上，按一下 **[開始偵錯]**。  
  
3.  在封裝完成執行之後，在 **[偵錯]** 功能表上，按一下 **[停止偵錯]**。  
  
### <a name="to-examine-the-generated-log-file"></a>若要檢查產生的記錄檔  
  
-   使用記事本或任何其他文字編輯器來開啟 TutorialLog.log 檔。  
  
-   雖然對 **PipelineExecutionPlan** 和 **PipelineExecutionTrees** 事件產生的資訊之語意並不在本教學課程的範圍之內，但您可以看到第一行列出在 **[設定 SSIS 記錄]** 對話方塊的 **[詳細資料]** 索引標籤中指定的資訊欄位。 而且，您還可以確認，在 Foreach 迴圈的每一個反覆運算中，已記錄您選取的兩個事件 PipelineExecutionPlan 和 PipelineExecutionTrees。  
  
## <a name="next-lesson"></a>下一課  
[第 4 課：使用 SSIS 加入錯誤流程重新導向](../integration-services/lesson-4-add-error-flow-redirection-with-ssis.md)  
  
  
  

