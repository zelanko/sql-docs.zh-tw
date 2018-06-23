---
title: Excel 裝置資訊設定 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- device information settings [Reporting Services], Excel rendering
- Excel [Reporting Services], rendering
ms.assetid: bb5f3566-f033-4470-be87-1f52fb7a4ab6
caps.latest.revision: 40
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 518033807ca52001a09a01136225f3a7594af7d2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36135571"
---
# <a name="excel-device-information-settings"></a>Excel 裝置資訊設定
  下表列出以 [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] 格式轉譯的裝置資訊設定。  
  
|設定|ReplTest1|  
|-------------|-----------|  
|**OmitDocumentMap**|指出是否為支援它的報表省略文件引導模式。 預設值是 `false`。|  
|**OmitFormulas**|指出是否從轉譯的報表省略公式。 預設值是 `false`。|  
|`SimplePageHeade`rs|指出是否將報表的頁首轉譯為 Excel 頁首。 值為`false`表示頁首會轉譯工作表的第一個資料列。 預設值是 `false`。|  
  
## <a name="see-also"></a>另請參閱  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [將裝置資訊設定傳遞至轉譯延伸模組](report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [在 RSReportServer.Config 中自訂轉譯延伸模組參數](customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [技術參考 &#40;SSRS&#41;](../../2014/reporting-services/technical-reference-ssrs.md)  
  
  