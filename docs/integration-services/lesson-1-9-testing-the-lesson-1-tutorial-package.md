---
title: 步驟 9：測試第 1 課教學課程套件 | Microsoft Docs
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 9aee7acf-797b-46f2-830d-80ab64a9f0b6
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 74099a8611c9c81b54619e1fc071b63a5d22777a
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/16/2019
ms.locfileid: "65722904"
---
# <a name="lesson-1-9-test-the-lesson-1-package"></a>課程 1-9：測試第 1 課套件

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



在本教學課程中，您已完成下列工作：  
  
-   建立新的 [!INCLUDE[ssIS](../includes/ssis-md.md)] 專案。  
  
-   為套件設定連線管理員以連線至來源和目的地資料。  
  
-   加入資料流程來取得一般檔案來源的資料，對資料執行必要的查閱轉換，以及設定目的地的資料。  
  
您的套件現在已完成且做好測試準備！
  
## <a name="check-the-package-components"></a>檢查套件元件
  
在測試套件之前，請確認第 1 課套件中的控制流程和資料流程包含下列圖中所示的物件。  
  
**控制流程** 
  
![套件中的控制流程](../integration-services/media/task9lesson1control.gif "套件中的控制流程")  
  
**資料流程**  
  
![套件中的資料流程](../integration-services/media/task9lesson1data.gif "套件中的資料流程")  
  
## <a name="run-the-lesson-1-package"></a>執行第 1 課套件  
  
1.  在 [偵錯] 功能表上，選取 [開始偵錯]。  
  
    套件隨即會執行，使得 1,097 個資料列順利新增至 **AdventureWorksDW2012** 的 **NewFactCurrencyRate** 事實資料表中。 若要確認此結果，請選取 [資料流程] 索引標籤。
  
2.  在套件執行完成之後，於 [偵錯] 功能表上，選取 [停止偵錯]。  
  
## <a name="go-to-next-lesson"></a>移至下一課
[第 2 課：使用 SSIS 來新增迴圈](../integration-services/lesson-2-adding-looping-with-ssis.md)  
  
## <a name="see-also"></a>另請參閱  
[執行專案和套件](packages/run-integration-services-ssis-packages.md) 
  
  
  
