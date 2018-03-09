---
title: "步驟 4：測試第 5 課的教學課程封裝 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: tutorial
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 5215b77d-c2ec-4b25-a3de-ca49ea197d74
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 600fa07aaffe0612cd87bcf33436c01481658782
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="lesson-5-4---testing-the-lesson-5-tutorial-package"></a>課程 5-4 - 測試第 5 課的教學課程封裝
在執行階段，您的封裝將從執行階段更新的變數中取得 **Directory** 屬性的值，而不是使用您建立封裝時指定的原始目錄名稱。 變數的值會由 SSISTutorial.dtsConfig 檔案擴展。  
  
若要確認封裝在執行階段使用新值來更新 Directory 屬性，只要執行封裝即可。 因為只有 3 個範例資料檔會複製到新目錄，所以資料流程只會執行 3 次，而不是反覆執行原始資料夾的 14 個檔案。  
  
## <a name="checking-the-package-layout"></a>檢查封裝配置  
在測試封裝之前，您應該確認第 5 課封裝中的控制流程和資料流程是否包含下圖所顯示的物件。 其控制流程應該與第 4 課的控制流程相同。 資料流程應該與第 4 課的資料流程完全相同。  
  
**控制流程**  
  
![套件中的控制流程](../integration-services/media/task4lesson2control.gif "套件中的控制流程")  
  
**資料流程**  
  
![套件中的資料流程](../integration-services/media/task9lesson1data.gif "套件中的資料流程")  
  
### <a name="to-test-the-lesson-5-tutorial-package"></a>若要測試第 5 課的教學課程封裝  
  
1.  在 **[偵錯]** 功能表上，按一下 **[開始偵錯]**。  
  
2.  在封裝完成執行之後，在 **[偵錯]** 功能表上，按一下 **[停止偵錯]**。  
  
## <a name="next-lesson"></a>下一課  
[第 6 課：在 SSIS 中搭配專案部署模型使用參數](../integration-services/lesson-6-using-parameters-with-the-project-deployment-model-in-ssis.md)  
  
  
  
