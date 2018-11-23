---
title: 步驟 4：測試第 2 課的教學課程封裝 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 0e8c0a25-8f79-41df-8ed2-f82a74b129cd
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5f612768d1e4cd6bff6be8204b38c0a99e1eb285
ms.sourcegitcommit: 7e828cd92749899f4e1e45ef858ceb9a88ba4b6a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/14/2018
ms.locfileid: "51629511"
---
# <a name="lesson-2-4---testing-the-lesson-2-tutorial-package"></a>課程 2-4 - 測試第 2 課的教學課程封裝
利用現在已設定的 Foreach 迴圈容器和一般檔案連接管理員，第 2 課的封裝可反覆進行範例資料夾之 14 個一般檔案的集合。 每次一找到符合指定檔案名稱準則的檔案名稱時，Foreach 迴圈容器就會以該檔案名稱擴展使用者自訂變數。 然後，這個變數會更新一般檔案連接管理員的 ConnectionString 屬性，並建立與新的一般檔案之連接。 在連接到資料夾的下一個檔案之前，Foreach 迴圈容器會對新的一般檔案中的資料執行未修改過的資料流程工作。  
  
請利用下列程序來測試您已加入封裝中的新迴圈功能。  
  
> [!NOTE]  
> 如果您執行了第 1 課的套件，就必須先從 AdventureWorksDW2012 的 dbo.NewFactCurrencyRate 中刪除記錄，再執行這一課的套件，否則套件會失敗並出現錯誤，指出主索引鍵違規條件約束。 如果您是透過選取 [偵錯]/[開始偵錯] (或按下 F5) 來執行封裝，也會收到相同的錯誤，因為第 1 課和第 2 課都將執行。 第 2 課會嘗試插入已經在第 1 課中插入的記錄。  
  
## <a name="checking-the-package-layout"></a>檢查封裝配置  
在測試封裝之前，您應該確認第 2 課封裝中的控制流程和資料流程是否包含下圖所顯示的物件。 資料流程應該與第 1 課的資料流程相同。  
  
**控制流程**  
  
![套件中的控制流程](../integration-services/media/task4lesson2control.gif "套件中的控制流程")  
  
**資料流程**  
  
![套件中的資料流程](../integration-services/media/task9lesson1data.gif "套件中的資料流程")  
  
### <a name="to-test-the-lesson-2-tutorial-package"></a>若要測試第 2 課的教學課程封裝  
  
1.  在 **[方案總管]** 中，以滑鼠右鍵按一下 **[Lesson 2.dtsx]** ，然後按一下 **[執行封裝]**。  
  
    此時會執行封裝。 您可以在 [輸出] 視窗中確認每一個迴圈的狀態，或按一下 **[進度]** 索引標籤來確認。例如，您會看到有 1097 行已從 Currency_VEB.txt 檔案加入目的地資料表中。  
  
2.  在封裝完成執行之後，在 **[偵錯]** 功能表上，按一下 **[停止偵錯]**。  
  
## <a name="next-lesson"></a>下一課  
[第 5 課：加入套件部署模型的 SSIS 套件組態](../integration-services/lesson-5-add-ssis-package-configurations-for-the-package-deployment-model.md)  
  
## <a name="see-also"></a>另請參閱  
[執行專案和封裝](~/integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md)  
  
  
  

