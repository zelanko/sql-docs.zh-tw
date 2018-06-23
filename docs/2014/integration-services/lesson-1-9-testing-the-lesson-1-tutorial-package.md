---
title: 步驟 9：測試第 1 課的教學課程套件 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9aee7acf-797b-46f2-830d-80ab64a9f0b6
caps.latest.revision: 26
author: douglaslM
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 8d423a6001888f0ec894ed2e73b715fb3c30db12
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36023157"
---
# <a name="step-9-testing-the-lesson-1-tutorial-package"></a>步驟 9：測試第 1 課的教學課程封裝
  在這一課，您完成了下列工作：  
  
-   建立新的 [!INCLUDE[ssIS](../includes/ssis-md.md)] 專案。  
  
-   設定封裝要連接到來源和目的地資料時所需的連接管理員。  
  
-   加入資料流程來取得一般檔案來源的資料，對資料執行必要的查閱轉換，以及設定目的地的資料。  
  
 現在已完成封裝！ 測試封裝的時間到了。  
  
## <a name="checking-the-package-layout"></a>檢查封裝配置  
 在測試封裝之前，您應該確認第 1 課封裝中的控制流程和資料流程是否包含下圖所顯示的物件。  
  
 **控制流程**  
  
 ![套件中的控制流程](../../2014/tutorials/media/task9lesson1control.gif "套件中的控制流程")  
  
 **資料流程**  
  
 ![套件中的資料流程](../../2014/tutorials/media/task9lesson1data.gif "套件中的資料流程")  
  
### <a name="to-run-the-lesson-1-tutorial-package"></a>若要執行第 1 課的教學課程封裝  
  
1.  在 **[偵錯]** 功能表上，按一下 **[開始偵錯]**。  
  
     封裝隨即執行，讓 1097 個資料列順利加入 **AdventureWorksDW2012** 的 **FactCurrency**事實資料表中。  
  
2.  在封裝完成執行之後，在 **[偵錯]** 功能表上，按一下 **[停止偵錯]**。  
  
## <a name="next-lesson"></a>下一課  
 [第 2 課： 加入迴圈](../integration-services/lesson-2-adding-looping-with-ssis.md)  
  
## <a name="see-also"></a>另請參閱  
 [執行專案和套件](packages/run-integration-services-ssis-packages.md)  
  
  