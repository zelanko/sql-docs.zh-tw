---
title: 步驟 5：測試第 4 課教學課程套件 | Microsoft Docs
ms.custom: ''
ms.date: 01/07/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 5f18df92-0248-4858-836b-c8b02f0e0439
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f1c7ec3026050181ae31150c4b5e190a65d889d4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65721515"
---
# <a name="lesson-4-5-test-the-lesson-4-package"></a>課程 4-5：測試第 4 課套件

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



在執行階段，損毀的檔案 **Currency_BAD.txt** 無法在 [貨幣索引鍵查閱] 轉換中產生相符的項目。 因為您已將 [貨幣索引鍵查閱] 的錯誤輸出設定成將失敗的資料列重新導向到新的「失敗的資料列」目的地，所以該元件不會失敗，且套件會順利執行。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 會將所有失敗的錯誤資料列寫入至 **ErrorOutput.txt**。  
  
在此工作中，您會執行套件來測試已修訂的錯誤輸出設定。 在順利執行套件之後，您需檢視 **ErrorOutput.txt**檔案的內容。  
  
> [!NOTE]  
> 如果您不想要在 **ErrorOutput.txt** 檔案中累積錯誤資料列，請手動刪除套件執行之間的檔案內容。  
  
## <a name="check-the-package-layout"></a>檢查套件配置  
在測試套件之前，請確認第 4 課套件中的控制流程和資料流程是否與下圖類似： 
  
**控制流程**  
  
![套件中的控制流程](../integration-services/media/task4lesson2control.gif "套件中的控制流程")  
  
**資料流程**  
  
![套件中的資料流程](../integration-services/media/task5lesson5data.gif "套件中的資料流程")  
  
## <a name="run-the-lesson-4-tutorial-package"></a>執行第 4 課教學課程套件  
  
1.  在 [偵錯]  功能表上，選取 [開始偵錯]  。  
  
2.  在套件執行完成之後，於 [偵錯]  功能表上，選取 [停止偵錯]  。  
  
## <a name="view-the-contents-of-the-erroroutputtxt-file"></a>檢視 ErrorOutput.txt 檔案的內容  
  
在「記事本」或任何其他文字編輯器中，開啟 **ErrorOutput.txt** 檔案。 預設資料行順序為：AverageRate、CurrencyID、CurrencyDate、EndOfDateRate、ErrorCode、ErrorColumn、ErrorDescription。  
 
此檔案中的所有資料列都包含不相符的 CurrencyID 值 "BAD"、ErrorCode 值 -1071607778、ErrorColumn 值 0 和 ErrorDescription 值「查閱期間產生的資料列不符」。 ErrorColumn 的值為 0，因為錯誤不是資料行特定的錯誤，而是查閱作業失敗。
  
  
## <a name="next-lesson"></a>下一課
[第 5 課：加入套件部署模型的 SSIS 套件組態](../integration-services/lesson-5-add-ssis-package-configurations-for-the-package-deployment-model.md)  
