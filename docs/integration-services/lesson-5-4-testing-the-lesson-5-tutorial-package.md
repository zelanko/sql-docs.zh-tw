---
description: 第 5-4 課：測試第 5 課套件
title: 步驟 4：測試第 5 課套件 | Microsoft Docs
ms.custom: ''
ms.date: 01/08/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 5215b77d-c2ec-4b25-a3de-ca49ea197d74
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 57bad9d0d13f85ae52858005e3fb6acc6f9532f0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500798"
---
# <a name="lesson-5-4-test-the-lesson-5-package"></a>第 5-4 課：測試第 5 課套件

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]



在執行階段，您的套件會從設定變數取得 **Directory** 屬性的值，而不是從建立套件時所指定的目錄名稱取得。 變數的值來自 **SSISTutorial.dtsConfig** XML 檔。  
  
若要確認套件在執行階段使用新值來更新 **Directory** 屬性，請執行套件。 因為新目錄中只有三個範例資料檔案，所以資料流程只會執行三次。  
  
## <a name="checking-the-package-layout"></a>檢查封裝配置  
在測試套件之前，請確認第 5 課套件中的控制流程和資料流程類似下圖所示的物件：  
  
**控制流程**  
  
![套件中的控制流程](../integration-services/media/task4lesson2control.gif "套件中的控制流程")  
  
**資料流程**  
  
![套件中的資料流程](../integration-services/media/task9lesson1data.gif "套件中的資料流程")  
  
## <a name="test-the-lesson-5-package"></a>測試第 5 課套件  
  
1.  在 [偵錯] 功能表上，選取 [開始偵錯]。  
  
2.  在套件執行完成之後，於 [偵錯]**** 功能表上，選取 [停止偵錯]****。  
  
## <a name="next-lesson"></a>下一課  
[第 6 課：在 SSIS 中搭配專案部署模型使用參數](../integration-services/lesson-6-using-parameters-with-the-project-deployment-model-in-ssis.md)  
  
  
  
