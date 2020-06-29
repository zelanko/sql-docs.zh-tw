---
title: 步驟 4：測試第 5 課的教學課程封裝 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 5215b77d-c2ec-4b25-a3de-ca49ea197d74
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f7fcaa0ecab3561e49fc8080251d2523034f5149
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2020
ms.locfileid: "85440375"
---
# <a name="step-4-testing-the-lesson-5-tutorial-package"></a>步驟 4：測試第 5 課的教學課程封裝
  在執行階段，您的封裝將從執行階段更新的變數中取得 `Directory` 屬性的值，而不是使用您建立封裝時指定的原始目錄名稱。 變數的值會由 SSISTutorial.dtsConfig 檔案擴展。  
  
 若要確認封裝在執行階段使用新值來更新 Directory 屬性，只要執行封裝即可。 因為只有 3 個範例資料檔會複製到新目錄，所以資料流程只會執行 3 次，而不是反覆執行原始資料夾的 14 個檔案。  
  
## <a name="checking-the-package-layout"></a>檢查封裝配置  
 在測試封裝之前，您應該確認第 5 課封裝中的控制流程和資料流程是否包含下圖所顯示的物件。 其控制流程應該與第 4 課的控制流程相同。 資料流程應該與第 4 課的資料流程完全相同。  
  
 **控制流程**  
  
 ![套件中的控制流程](../../2014/tutorials/media/task4lesson2control.gif "套件中的控制流程")  
  
 **資料流程**  
  
 ![套件中的資料流程](../../2014/tutorials/media/task9lesson1data.gif "套件中的資料流程")  
  
### <a name="to-test-the-lesson-5-tutorial-package"></a>若要測試第 5 課的教學課程封裝  
  
1.  在 [**調試**] 功能表上，按一下 [**開始調試**]。  
  
2.  在封裝完成執行之後，請在 [**調試**程式] 功能表上，按一下 [**停止調試**程式]。  
  
## <a name="next-lesson"></a>下一課  
 [第 6 課：搭配專案部署模型使用參數](../integration-services/lesson-6-using-parameters-with-the-project-deployment-model-in-ssis.md)  
  
  
