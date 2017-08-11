---
title: "PDF 裝置資訊設定 |Microsoft 文件"
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
- device information settings [Reporting Services], PDF rendering
- PDF [Reporting Services]
ms.assetid: 9a4aabe5-dbdc-4884-b999-1200983fee47
caps.latest.revision: 41
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e02ae92cfb973c7287fde080628fcc26cb784276
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---
# <a name="pdf-device-information-settings"></a>PDF 裝置資訊設定
  下表列出以 PDF 格式轉譯報表的裝置資訊設定。  
  
|設定|Value|  
|-------------|-----------|  
|**資料行**|為報表所設定的資料行數目。 這個值會覆寫報表的原始設定。|  
|**ColumnSpacing**|為報表所設定的資料行間距。 這個值會覆寫報表的原始設定。|  
|**DpiX**|輸出裝置在 x 方向的解析度。|  
|**DpiY**|輸出裝置在 y 方向的解析度。|  
|**EndPage**|要轉譯之報表的最後一頁。 預設值為 **StartPage**的值。|  
|**HumanReadablePDF**|指出是否應該壓縮 PDF，這可提高來源的可讀性。 預設值為 **false**。|  
|**MarginBottom**|為報表所設定的下邊界值 (以英吋為單位)。 您必須包含後面接著 "in" 的整數或小數值 (例如，1in)。 這個值會覆寫報表的原始設定。|  
|**MarginLeft**|為報表所設定的左邊界值 (以英吋為單位)。 您必須包含後面接著 "in" 的整數或小數值 (例如，1in)。 這個值會覆寫報表的原始設定。|  
|**MarginRight**|為報表所設定的右邊界值 (以英吋為單位)。 您必須包含後面接著 "in" 的整數或小數值 (例如，1in)。 這個值會覆寫報表的原始設定。|  
|**MarginTop**|為報表所設定的上邊界值 (以英吋為單位)。 您必須包含後面接著 "in" 的整數或小數值 (例如，1in)。 這個值會覆寫報表的原始設定。|  
|**PageHeight**|為報表所設定的頁面高度 (以英吋為單位)。 您必須包含後面接著 "in" 的整數或小數值 (例如，11in)。 這個值會覆寫報表的原始設定。|  
|**PageWidth**|為報表所設定的頁面寬度 (以英吋為單位)。 您必須包含後面接著 "in" 的整數或小數值 (例如，8.5in)。 這個值會覆寫報表的原始設定。|  
|**StartPage**|要轉譯之報表的第一頁。 **0** 值表示轉譯所有頁面。 預設值是 **1**秒。|  
  
## <a name="see-also"></a>請參閱＜  
 [將裝置資訊設定傳遞至轉譯延伸模組](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [自訂轉譯延伸模組參數，在 RSReportServer.Config 中](../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [技術參考 &#40;SSRS &#41;](../reporting-services/technical-reference-ssrs.md)  
  
  
