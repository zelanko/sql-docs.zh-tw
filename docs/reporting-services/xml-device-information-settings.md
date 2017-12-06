---
title: "XML 裝置資訊設定 | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: reporting-services
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- XML [Reporting Services], rendering
- device information settings [Reporting Services], PDF rendering
ms.assetid: a32e83fe-c10e-4ebd-8975-5be7dcc422e7
caps.latest.revision: "43"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 5bb74b8da1b59adaab0f1b8f736f10c769ea2f8e
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="xml-device-information-settings"></a>XML 裝置資訊設定
  下表列出以 XML 格式轉譯的裝置資訊設定。  
  
|設定|值|詳細資料|  
|-------------|------------|-------------|  
|**XSLT**|要套用至 XML 檔案之 XSLT 的報表伺服器命名空間中的路徑，例如 **/Transforms/myxslt**。|xsl 檔案必須是報表伺服器上已發行的資源，而且您必須透過報表伺服器項目路徑存取它。 在報表中指定任何 XSLT 之後，會套用此設定的值。 如果套用 **XSLT** 設定，則會忽略 **OmitSchema** 設定。|  
|**MIMEType**|XML 檔案的多用途網際網路郵件延伸標準 (MIME) 類型。||  
|**UseFormattedValues**|**true**<br /><br /> **false**|指出當產生 XML 資料時，是否要轉譯文字方塊的格式值。<br /><br /> 值為 False 時，表示使用文字方塊的基礎值。|  
|**Indented**|**true**<br /><br /> **false**|指出是否要產生縮排的 XML。 預設值 **false** 會產生非縮排、壓縮的 XML。|  
|**OmitNamespace**|**true**<br /><br /> **false**|指出是否省略 XML 中的預設命名空間。<br /><br /> 如果為 true，則 XML 不會指定預設命名空間。<br /><br /> 如果為 false，則 XML 會以報表的 DataSchema 屬性值指定預設命名空間。 DataSchema 屬性預設為報表名稱。<br /><br /> 預設值為**false**。|  
|**OmitSchema**|**true**<br /><br /> **false**|指出是否省略 XML 中的結構描述位置。 位置是 SchemaLocation 屬性。<br /><br /> OmitSchema 的預設值取決於 OmitNamespace 的值：<br /><br /> 如果 OmitNamespace = False，則預設為 OmitSchema = **False** 。 使用者可以設定 OmitSchema = True 來覆寫預設值。<br /><br /> 如果 OmitNamespace = True，則無論為 OmitShema 明確設定的值為何，OmitSchema 都會當做 **True** 運作。|  
|**編碼方式**|.NET Framework 所支援之字元編碼方式的 Internet Assigned Numbers Authority (IANA) 名稱。|預設值為 **UTF-8**。 其他值的範例包括 ASCII、UTF-7 和 UTF-16。|  
|**FileExtension**|使用於產生的檔案之副檔名。||  
|**結構描述**|值 **true** 表示已轉譯 XML 結構描述。 預設值為 **false**。|指出是否轉譯 XML 結構描述定義 (XSD) 以及是否轉譯實際的 XML 資料。|  
  
## <a name="see-also"></a>另請參閱  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [將裝置資訊設定傳遞至轉譯延伸模組](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [在 RSReportServer.Config 中自訂轉譯延伸模組參數](../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [技術參考 &#40;SSRS&#41;](../reporting-services/technical-reference-ssrs.md)  
  
  
