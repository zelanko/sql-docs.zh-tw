---
title: 步驟 3：測試第 6 課套件 | Microsoft Docs
ms.custom: ''
ms.date: 01/11/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: c184c92d-948f-4037-a502-5fabd909c84c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a0c50372c199d80dc0e6d3d7e3326918011f8a28
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "71283070"
---
# <a name="lesson-6-3-test-the-lesson-6-package"></a>第 6-3 課：測試第 6 課套件

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


在執行階段，您的套件會從 **VarFolderName** 參數取得 **Directory** 屬性值。  
  
若要確認套件會更新 **Directory** 屬性，請執行套件。 因為您已將三個範例資料檔案複製到新目錄，所以資料流程會執行三次。
  
## <a name="check-the-package-layout"></a>檢查套件配置  
在測試套件之前，請確認第 6 課套件中的控制流程和資料流程類似下圖所示物件：   
  
**控制流程**  
  
![控制流程](../integration-services/media/task4lesson2control.gif "控制流程")  
  
**資料流程**  
  
![資料流程](../integration-services/media/task5lesson5data.gif "資料流程")  
  
## <a name="test-the-lesson-6-package"></a>測試第 6 課套件  
  
1.  在 [偵錯]  功能表上，選取 [開始偵錯]  。  
  
2.  在套件執行完成之後，於 [偵錯]  功能表上，選取 [停止偵錯]  。  
  
## <a name="go-to-next-task"></a>移至下一個工作
[步驟 4：部署第 6 課套件](../integration-services/lesson-6-4-deploying-the-lesson-6-package.md)  
  
  
  
