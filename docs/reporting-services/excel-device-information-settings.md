---
title: Excel 裝置資訊設定 | Microsoft Docs
ms.date: 01/23/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- device information settings [Reporting Services], Excel rendering
- Excel [Reporting Services], rendering
ms.assetid: bb5f3566-f033-4470-be87-1f52fb7a4ab6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 7a83bcd79a50400888d5a973ad9a743db19b87b5
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "76761822"
---
# <a name="excel-device-information-settings"></a>Excel 裝置資訊設定
  下表列出以 [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] 格式轉譯的裝置資訊設定。  
  
|設定|值|  
|-------------|-----------|  
|**OmitDocumentMap**|指出是否為支援它的報表省略文件引導模式。 預設值為 **false**。|  
|**OmitFormulas**|指出是否從轉譯的報表省略公式。 預設值為 **false**。|  
|**SimplePageHeaders**|指出是否將報表的頁首轉譯為 Excel 頁首。 **false** 的值指出將頁首轉譯為工作表的第一列。 預設值為 **false**。|  
|**DynamicImageDpi**|動態影像的解析度，例如圖表、量測計和地圖。 預設值為 **96**。 (Power BI 報表伺服器 (2020 年 1 月) 及更新版本中提供)|  

  
## <a name="see-also"></a>另請參閱  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [將裝置資訊設定傳遞至轉譯延伸模組](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [在 RSReportServer.Config 中自訂轉譯延伸模組參數](../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [技術參考 &#40;SSRS&#41;](../reporting-services/technical-reference-ssrs.md)  
  
  
