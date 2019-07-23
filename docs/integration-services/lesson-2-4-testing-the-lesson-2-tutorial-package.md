---
title: 步驟 4：測試第 2 課教學課程套件 | Microsoft Docs
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 0e8c0a25-8f79-41df-8ed2-f82a74b129cd
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 907dd855186236e05eb103fd771a28ff0bc916ef
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086573"
---
# <a name="lesson-2-4-test-the-lesson-2-tutorial-package"></a>課程 2-4：測試第 2 課教學課程套件

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



在現已設定好「Foreach 迴圈」容器和「一般檔案」連線管理員的情況下，第 2 課套件可逐一查看「範例資料」資料夾中的 14 個一般檔案。 每當某個檔案名稱與指定的準則相符時，「Foreach 迴圈」容器就會以該檔案名稱填入使用者定義的變數。 此變數會接著更新「一般檔案」連線管理員的 ConnectionString 屬性，以連線至該一般檔案。 然後，「Foreach 迴圈」容器會對該一般檔案中的資料執行未修改過的資料流程工作。  
  
> [!NOTE]  
> 如果您已執行第 1 課的套件，就必須先從 AdventureWorksDW2012 的 dbo.NewFactCurrencyRate 資料表中刪除記錄，再執行這一課的套件。 第 2 課會嘗試插入已經在第 1 課中插入的記錄，這會造成錯誤。  
  
## <a name="check-the-package-layout"></a>檢查套件配置  
在測試套件之前，請確認第 2 課套件中的控制流程和資料流程包含下列圖中所示的物件。 第 2 課的資料流程與第 1 課相同。  
  
**控制流程**  
  
![套件中的控制流程](../integration-services/media/task4lesson2control.gif "套件中的控制流程")  
  
**資料流程**  
  
![套件中的資料流程](../integration-services/media/task9lesson1data.gif "套件中的資料流程")  
  
## <a name="test-the-lesson-2-tutorial-package"></a>測試第 2 課教學課程套件  
  
1.  在 [方案總管]  中，於 [Lesson 2.dtsx]  上按一下滑鼠右鍵，然後選取 [執行封裝]  。  
  
    隨即會執行套件。 您可以在 [輸出]  視窗中或透過選取 [進度]  索引標籤，來確認每個迴圈的狀態。例如，您會看到有 1,097 個資料列已從 Currency_VEB.txt 檔案新增到目的地資料表中。  
  
2.  在套件執行完成之後，於 [偵錯]  功能表上，選取 [停止偵錯]  。  
  
## <a name="go-to-next-lesson"></a>移至下一課  
[第 3 課：使用 SSIS 來新增記錄功能](../integration-services/lesson-3-add-logging-with-ssis.md)  
  
## <a name="see-also"></a>另請參閱  
[執行專案和套件](../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md)  
  
  
  

