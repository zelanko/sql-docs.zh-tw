---
title: 步驟 5：測試第 4 課的教學課程封裝
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: tutorial
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 5f18df92-0248-4858-836b-c8b02f0e0439
caps.latest.revision: 23
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7d123192e2115c909af8afaec1237360fcb9e7a7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="lesson-4-5---testing-the-lesson-4-tutorial-package"></a>第 4-5 課 - 測試課程 4 的教學課程封裝
在執行階段，損毀的檔案 Currency_BAD.txt 將無法在 [貨幣索引鍵查閱] 轉換中產生相符者。 因為 [貨幣索引鍵查閱] 的錯誤輸出現在已設定為將失敗的資料列重新導向至新的失敗資料列目的地，所以該元件不會失敗，且封裝會順利執行。 所有失敗的錯誤資料列會寫入至 ErrorOutput.txt。  
  
在這項工作中，您將執行封裝來測試修改過的錯誤輸出組態。 在封裝順利執行後，即會看到 ErrorOutput.txt 檔的內容。  
  
> [!NOTE]  
> 如果您不想要在 ErrorOutput.txt 檔案中累計錯誤資料列，應該手動刪除封裝執行之間的檔案內容。  
  
## <a name="checking-the-package-layout"></a>檢查封裝配置  
在測試封裝之前，您應該確認第 4 課封裝中的控制流程和資料流程是否包含下圖所顯示的物件。 其控制流程應該與第 2 - 4 課的控制流程相同。  
  
**控制流程**  
  
![套件中的控制流程](../integration-services/media/task4lesson2control.gif "套件中的控制流程")  
  
**資料流程**  
  
![套件中的資料流程](../integration-services/media/task5lesson5data.gif "套件中的資料流程")  
  
### <a name="to-run-the-lesson-4-tutorial-package"></a>若要執行第 4 課的教學課程封裝  
  
1.  在 **[偵錯]** 功能表上，按一下 **[開始偵錯]**。  
  
2.  在封裝完成執行之後，在 **[偵錯]** 功能表上，按一下 **[停止偵錯]**。  
  
### <a name="to-verify-the-contents-of-the-erroroutputtxt-file"></a>若要驗證 ErrorOutput.txt 檔的內容  
  
-   在記事本或任何其他文字編輯器中開啟 ErrorOutput.txt 檔。 預設資料行順序為：AverageRate、CurrencyID、CurrencyDate、EndOfDateRate、ErrorCode、ErrorColumn、ErrorDescription。  
  
    請注意，檔案中的所有資料列都包含不相符的 CurrencyID 值 BAD、ErrorCode 值 -1071607778、ErrorColumn 值 0 和 ErrorDescription 值「查閱期間產生的資料列不符」。 ErrorColumn 的值是設為 0，因為該錯誤不是特定資料行的錯誤。 它是失敗的查閱作業。 執行個體時提供 SQL Server 登入。  
  
  
  
