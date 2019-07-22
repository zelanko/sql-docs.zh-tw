---
title: 步驟 3：測試第 3 課教學課程套件 | Microsoft Docs
ms.custom: ''
ms.date: 01/04/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 1096a476-93cf-4474-86f5-27d6357eb380
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 7f0bf7d9a38f25af008be3bf77ce8dc31070f5bd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68055935"
---
# <a name="lesson-3-3-test-the-lesson-3-tutorial-package"></a>課程 3-3：測試第 3 課教學課程套件

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



在此工作中，您會執行 **Lesson 3.dtsx**套件。 當套件執行時，[記錄事件]  視窗會列出 SSIS 寫入至記錄提供者所提供記錄檔的記錄項目。 在套件執行完成之後，您可以檢視記錄檔的內容。  
  
## <a name="check-the-package-layout"></a>檢查套件配置  
在測試套件之前，請確認第 3 課套件中的控制流程和資料流程是否類似於下列圖中所示的物件。 控制流程應該與第 2 課相同，資料流程則應該與第 1 課和第 2 課相同。  
  
**控制流程**  
  
![套件中的控制流程](../integration-services/media/task4lesson2control.gif "套件中的控制流程")  
  
**資料流程**  
  
![套件中的資料流程](../integration-services/media/task9lesson1data.gif "套件中的資料流程")  
  
## <a name="run-the-lesson-3-tutorial-package"></a>執行第 3 課教學課程套件  
  
1.  在 SSIS 功能表上，選取 [記錄事件]  。  
  
2.  在 [偵錯]  功能表上，選取 [開始偵錯]  。  
  
3.  在套件執行完成之後，於 [偵錯]  功能表上，選取 [停止偵錯]  。  
  
## <a name="examine-the-generated-log-file"></a>檢查產生的記錄檔  
  
-   使用記事本或任何其他文字編輯器來開啟 TutorialLog.log 檔。  
  
-   本教學課程不包含針對 **PipelineExecutionPlan** 和 **PipelineExecutionTrees** 事件產生之資訊的完整說明。  在記錄檔中，您可以看到第一行列出在 [設定 SSIS 記錄]  對話方塊的 [詳細資料]  索引標籤中指定的資訊欄位。 此外，您也會看到 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 針對 Foreach 迴圈的每一次反覆運算，記錄了您選取的兩個事件 **PipelineExecutionPlan** 和 **PipelineExecutionTrees**。  
  
## <a name="next-lesson"></a>下一課  
[第 4 課：使用 SSIS 來新增錯誤流程重新導向](../integration-services/lesson-4-add-error-flow-redirection-with-ssis.md)  
  
  
  
