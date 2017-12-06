---
title: "PPTX 裝置資訊設定 | Microsoft Docs"
ms.custom: 
ms.date: 09/11/2015
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: reporting-services
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-native
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- render
- powerpoint
- pptx
- export
ms.assetid: 4dc2045f-8025-41a3-8f9d-5635fb24cf4a
caps.latest.revision: "6"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 03664a60aaa111295491985de103882091bb43aa
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="pptx-device-information-settings"></a>PPTX 裝置資訊設定
  下表列出以 PPTX 格式轉譯 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 報表的裝置資訊設定。  
  
|設定|Value|  
|-------------|-----------|  
|**資料行**|為報表所設定的資料行數目。 這個值會覆寫報表的原始設定。|  
|**ColumnSpacing**|為報表所設定的資料行間距。 這個值會覆寫報表的原始設定。|  
|**DpiX**|輸出影像的水平解析度。 預設值為 **96**。 適用於 **BMP**、 **GIF**、 **PNG**和 **TIFF** 輸出格式。|  
|**DpiY**|輸出影像的垂直解析度。 預設值為 **96**。 適用於 **BMP**、 **GIF**、 **PNG**和 **TIFF** 輸出格式。|  
|**EndPage**|要轉譯之報表的最後一頁。 預設值為 **StartPage**的值。|  
|**MarginBottom**|為報表所設定的下邊界值 (以英吋為單位)。 您必須包含後面接著 "in" 的整數或小數值 (例如 **1in**)。 這個值會覆寫報表的原始設定。|  
|**MarginLeft**|為報表所設定的左邊界值 (以英吋為單位)。 您必須包含後面接著 "in" 的整數或小數值 (例如 **1in**)。 這個值會覆寫報表的原始設定。|  
|**MarginRight**|為報表所設定的右邊界值 (以英吋為單位)。 您必須包含後面接著 "in" 的整數或小數值 (例如 **1in**)。 這個值會覆寫報表的原始設定。|  
|**MarginTop**|為報表所設定的上邊界值 (以英吋為單位)。 您必須包含後面接著 "in" 的整數或小數值 (例如 **1in**)。 這個值會覆寫報表的原始設定。|  
|**PageHeight**|為報表所設定的頁面高度 (以英吋為單位)。 您必須包含後面接著 "in" 的整數或小數值 (例如 **11in**)。 這個值會覆寫報表的原始設定。|  
|**PageWidth**|為報表所設定的頁面寬度 (以英吋為單位)。 您必須包含後面接著 "in" 的整數或小數值 (例如 **8.5in**)。 這個值會覆寫報表的原始設定。|  
|**StartPage**|要轉譯之報表的第一頁。 **0** 值表示轉譯所有頁面。 預設值是 **1**秒。|  
|**UseReportPageSize**|如果 UseReportPageSize =**false** ，則預設投影片大小為 PowerPoint 預設值 13.333” x 7.5” (16:9 外觀比例)。 如果 UseReportPageSize =true，則預設投影片大小為報表的定義頁面大小。<br /><br /> 預設值為 **false**<br /><br /> 請注意，PageWidth 和 PageHeight 設定會覆寫預設的寬度和高度。|  
  
## <a name="see-also"></a>另請參閱  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [將裝置資訊設定傳遞至轉譯延伸模組](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [在 RSReportServer.Config 中自訂轉譯延伸模組參數](../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [技術參考 &#40;SSRS&#41;](../reporting-services/technical-reference-ssrs.md)  
  
  
