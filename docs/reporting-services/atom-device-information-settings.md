---
title: ATOM 裝置資訊設定 | Microsoft Docs
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: fe4a56a4-5552-423c-85c1-895e2e212fee
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b2d04fae8687e31df79d72aec2b41bfe67cc1cc3
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "65504115"
---
# <a name="atom-device-information-settings"></a>ATOM 裝置資訊設定
  Atom 轉譯延伸模組的裝置資訊設定支援提交 Atom 摘要名稱以及要使用的字元編碼。  
  
 下表列出用來轉譯至資料服務文件的裝置資訊設定。  
  
|設定|值|  
|-------------|-----------|  
|**DataFeed**|如果指定這個設定，則會轉譯對應到此設定中所提供之摘要名稱的 Atom 摘要。 如果不指定的話，則會轉譯報表的 Atom 服務文件。 資料摘要的唯一自動產生的識別碼。 這個值是在內部使用，您不應該變更它。|  
|**編碼方式**|.NET Framework 所支援之字元編碼方式的 Internet Assigned Numbers Authority (IANA) 名稱。 預設值為 **UTF-8**。 其他值的範例包括 ASCII、UTF-7 和 UTF-16。|  
  
## <a name="see-also"></a>另請參閱  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [將裝置資訊設定傳遞至轉譯延伸模組](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [在 RSReportServer.Config 中自訂轉譯延伸模組參數](../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [技術參考 &#40;SSRS&#41;](../reporting-services/technical-reference-ssrs.md)  
  
  
