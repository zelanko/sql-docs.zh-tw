---
title: 影像裝置資訊設定 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- images [Reporting Services], rendering
- device information settings [Reporting Services], IMAGE rendering
ms.assetid: edad9498-69f7-4726-8699-fa615f704dff
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: be32765c6d996bcc67580949176c2265a0741eed
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56039009"
---
# <a name="image-device-information-settings"></a>影像裝置資訊設定
  下表列出以 IMAGE 格式轉譯的裝置資訊設定。  
  
|設定|值|  
|-------------|-----------|  
|**資料行**|為報表所設定的資料行數目。 這個值會覆寫報表的原始設定。|  
|**ColumnSpacing**|為報表所設定的資料行間距。 這個值會覆寫報表的原始設定。|  
|`DpiX`|輸出影像的水平解析度。 預設值為 **96**。 適用於`BMP`， `GIF`， `PNG`，和`TIFF`輸出格式。|  
|`DpiY`|輸出影像的垂直解析度。 預設值為 **96**。 適用於`BMP`， `GIF`， `PNG`，和`TIFF`輸出格式。|  
|**EndPage**|要轉譯之報表的最後一頁。 預設值為 `StartPage` 的值。|  
|**MarginBottom**|為報表所設定的下邊界值 (以英吋為單位)。 您必須包含後面接著 "in" 的整數或小數值 (例如，`1in`)。 這個值會覆寫報表的原始設定。|  
|**MarginLeft**|為報表所設定的左邊界值 (以英吋為單位)。 您必須包含後面接著 "in" 的整數或小數值 (例如，`1in`)。 這個值會覆寫報表的原始設定。|  
|**MarginRight**|為報表所設定的右邊界值 (以英吋為單位)。 您必須包含後面接著 "in" 的整數或小數值 (例如，`1in`)。 這個值會覆寫報表的原始設定。|  
|**MarginTop**|為報表所設定的上邊界值 (以英吋為單位)。 您必須包含後面接著 "in" 的整數或小數值 (例如，`1in`)。 這個值會覆寫報表的原始設定。|  
|**OutputFormat**|[!INCLUDE[ndptecgdiexpanded](../includes/ndptecgdiexpanded-md.md)] ([!INCLUDE[ndptecgdi](../includes/ndptecgdi-md.md)]) 所支援的輸出格式之一：`BMP`、`EMF`、`GIF`、`JPEG`、`PNG` 或 `TIFF`。|  
|**PageHeight**|為報表所設定的頁面高度 (以英吋為單位)。 您必須包含後面接著 "in" 的整數或小數值 (例如，`11in`)。 這個值會覆寫報表的原始設定。|  
|**PageWidth**|為報表所設定的頁面寬度 (以英吋為單位)。 您必須包含後面接著 "in" 的整數或小數值 (例如，`8.5in`)。 這個值會覆寫報表的原始設定。|  
|**PrintDpiX**|輸出影像的水平解析度。 預設值是 `300`。 適用於增強型中繼檔 (`EMF`) 輸出格式。|  
|**PrintDpiY**|輸出影像的垂直解析度。 預設值是 `300`。 適用於增強型中繼檔 (`EMF`) 輸出格式。|  
|`StartPage`|要轉譯之報表的第一頁。 `0` 的值表示轉譯所有頁面。 預設值是 `1`。|  
  
## <a name="see-also"></a>另請參閱  
 [將裝置資訊設定傳遞至轉譯延伸模組](report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [在 RSReportServer.Config 中自訂轉譯延伸模組參數](customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [技術參考 &#40;SSRS&#41;](../../2014/reporting-services/technical-reference-ssrs.md)  
  
  
