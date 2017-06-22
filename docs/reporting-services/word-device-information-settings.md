---
title: "Word 裝置資訊設定 |Microsoft 文件"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Word [Reporting Services]
- device information settings [Reporting Services], Word
ms.assetid: 28146498-fae7-4b13-b47f-6ec05aa8e057
caps.latest.revision: 7
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 491940329df26ba67f447aacb6a32f5d6578c4a5
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="word-device-information-settings"></a>Word 裝置資訊設定
  下表列出以 [!INCLUDE[ofprword](../includes/ofprword-md.md)] 格式轉譯的裝置資訊設定。  
  
|設定|Value|  
|-------------|-----------|  
|**AutoFit**|**False**： 在任何 Word 資料表上都會將 AutoFit 設定為 **false** 。<br /><br /> **True**。 在每個 Word 資料表上都會將 AutoFit 設定為 **true** 。<br /><br /> **Never**。 在任何 Word 資料表上未設定 AutoFit 值，而且會將行為轉換 Word 預設值。<br /><br /> **Default**。 在每個邏輯頁上，AutoFit 是設定在比實體繪製區域 (排除邊界的實體頁面寬度) 更狹窄的資料表上。|  
|**ExpandToggles**|指出可以切換的所有項目是否應該以其完全展開的狀態來轉譯。 預設值是 **false**秒。|  
|**FixedPageWidth**|指定寫入 DOC 檔案的「頁面寬度」是否將配合「報表主體」中最大頁面的寬度來增加。 預設值是 **false**秒。|  
|**OmitHyperlinks**|指定在設定 Hyperlink 動作的位置上，是否在所有的項目上省略該動作。 預設值為 **false**|  
|**OmitDrillthroughs**|指定在設定 Drillthrough 動作的位置上，是否在所有的項目上省略該動作。 預設值為 **false**|  
  
## <a name="see-also"></a>另請參閱  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [將裝置資訊設定傳遞至轉譯延伸模組](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [在 RSReportServer.Config 中自訂轉譯延伸模組參數](../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [技術參考 &#40;SSRS&#41;](../reporting-services/technical-reference-ssrs.md)  
  
  
