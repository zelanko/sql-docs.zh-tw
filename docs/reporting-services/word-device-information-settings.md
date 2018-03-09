---
title: "Word 裝置資訊設定 | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: reporting-services
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Word [Reporting Services]
- device information settings [Reporting Services], Word
ms.assetid: 28146498-fae7-4b13-b47f-6ec05aa8e057
caps.latest.revision: "7"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: b6ca29c16e7b50183623530f8bceedd349c1f23f
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/09/2018
---
# <a name="word-device-information-settings"></a>Word 裝置資訊設定
  下表列出以 [!INCLUDE[ofprword](../includes/ofprword-md.md)] 格式轉譯的裝置資訊設定。  
  
|設定|ReplTest1|  
|-------------|-----------|  
|**AutoFit**|**False**： 在任何 Word 資料表上都會將 AutoFit 設定為 **false** 。<br /><br /> **True**。 在每個 Word 資料表上都會將 AutoFit 設定為 **true** 。<br /><br /> **Never**。 在任何 Word 資料表上未設定 AutoFit 值，而且會將行為轉換 Word 預設值。<br /><br /> **Default**。 在每個邏輯頁上，AutoFit 是設定在比實體繪製區域 (排除邊界的實體頁面寬度) 更狹窄的資料表上。|  
|**ExpandToggles**|指出可以切換的所有項目是否應該以其完全展開的狀態來轉譯。 預設值為 **false**。|  
|**FixedPageWidth**|指定寫入 DOC 檔案的「頁面寬度」是否將配合「報表主體」中最大頁面的寬度來增加。 預設值為 **false**。|  
|**OmitHyperlinks**|指定在設定 Hyperlink 動作的位置上，是否在所有的項目上省略該動作。 預設值為 **false**|  
|**OmitDrillthroughs**|指定在設定 Drillthrough 動作的位置上，是否在所有的項目上省略該動作。 預設值為 **false**|  
  
## <a name="see-also"></a>另請參閱  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [將裝置資訊設定傳遞至轉譯延伸模組](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [在 RSReportServer.Config 中自訂轉譯延伸模組參數](../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [技術參考 &#40;SSRS&#41;](../reporting-services/technical-reference-ssrs.md)  
  
  
