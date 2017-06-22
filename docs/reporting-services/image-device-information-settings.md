---
title: "影像裝置資訊設定 |Microsoft 文件"
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
- images [Reporting Services], rendering
- device information settings [Reporting Services], IMAGE rendering
ms.assetid: edad9498-69f7-4726-8699-fa615f704dff
caps.latest.revision: 39
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 528ff1aac617e36ac8b3faeed0bad0981479f651
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="image-device-information-settings"></a>影像裝置資訊設定
  下表列出以 IMAGE 格式轉譯的裝置資訊設定。  
  
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
|**OutputFormat**|[!INCLUDE[ndptecgdiexpanded](../includes/ndptecgdiexpanded-md.md)] ([!INCLUDE[ndptecgdi](../includes/ndptecgdi-md.md)]) 過去支援的輸出格式之一： **BMP**、 **EMF**、 **GIF**、 **JPEG**、 **PNG**或 **TIFF**。|  
|**PageHeight**|為報表所設定的頁面高度 (以英吋為單位)。 您必須包含後面接著 "in" 的整數或小數值 (例如 **11in**)。 這個值會覆寫報表的原始設定。|  
|**PageWidth**|為報表所設定的頁面寬度 (以英吋為單位)。 您必須包含後面接著 "in" 的整數或小數值 (例如 **8.5in**)。 這個值會覆寫報表的原始設定。|  
|**PrintDpiX**|輸出影像的水平解析度。 預設值為 **300**。 適用於增強型中繼檔 (**EMF**) 輸出格式。|  
|**PrintDpiY**|輸出影像的垂直解析度。 預設值為 **300**。 適用於增強型中繼檔 (**EMF**) 輸出格式。|  
|**StartPage**|要轉譯之報表的第一頁。 **0** 值表示轉譯所有頁面。 預設值是 **1**秒。|  
  
## <a name="see-also"></a>另請參閱  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [將裝置資訊設定傳遞至轉譯延伸模組](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [在 RSReportServer.Config 中自訂轉譯延伸模組參數](../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [技術參考 &#40;SSRS&#41;](../reporting-services/technical-reference-ssrs.md)  
  
  
