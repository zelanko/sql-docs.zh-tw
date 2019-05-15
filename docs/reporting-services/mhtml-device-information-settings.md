---
title: MHTML 裝置資訊設定 | Microsoft Docs
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- device information settings [Reporting Services], MHTML rendering
- MHTML [Reporting Services]
ms.assetid: 60b85dd8-b4fb-4ad9-be6a-e7c89ac076fe
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 996a7f53b5969c9c1d8c39edcd23b62d45a7ff15
ms.sourcegitcommit: e4794943ea6d2580174d42275185e58166984f8c
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 05/09/2019
ms.locfileid: "65502732"
---
# <a name="mhtml-device-information-settings"></a>MHTML 裝置資訊設定
  下表列出以 Web 封存 (MHTML) 格式轉譯報表的裝置資訊設定。  
  
|設定|ReplTest1|  
|-------------|-----------|  
|**JavaScript**|指出在轉譯的報表中是否支援 JavaScript。|  
|**OutlookCompat**|指出是否要使用額外中繼資料轉譯，讓報表在 Outlook 中有較佳的外觀。 預設值為 **true**。|  
|**MHTML 片段**|指出是否建立 MHTML 片段來取代完整的 MHTML 文件。 MHTML 片段會在 TABLE 元素中包含報表內容，並省略 HTML 和 BODY 元素。 預設值為 **false**。|  
|**DataVisualizationFitSizing**|指示資料在 Tablix 內的視覺效果調整行為。 其中包括圖表、量測計和地圖。<br /><br /> 可能的值為 **[近似]** 和 **[精確]**。<br /><br /> 預設值為 **[近似]**。 如果從 **rsreportserver.config** 檔案中移除此設定，則預設行為是 **[精確]**。<br /><br /> 啟用 **[精確]** 可能會影響效能，因為判斷精確大小的處理所花的時間可能會比較長。|  
  
## <a name="see-also"></a>另請參閱  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [將裝置資訊設定傳遞至轉譯延伸模組](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [在 RSReportServer.Config 中自訂轉譯延伸模組參數](../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [技術參考 &#40;SSRS&#41;](../reporting-services/technical-reference-ssrs.md)  
  
  
