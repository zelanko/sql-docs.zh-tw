---
title: CSV 裝置資訊設定 | Microsoft Docs
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- CSV [Reporting Services]
- device information settings [Reporting Services], CSV rendering
ms.assetid: f96f83a6-50bc-48ce-9fcd-fd9e1952d40a
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 9423f82e025146773c5d04a276cf15c76c6b1101
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 05/14/2019
ms.locfileid: "65571602"
---
# <a name="csv-device-information-settings"></a>CSV 裝置資訊設定
  CSV 轉譯延伸模組的裝置資訊設定，允許變更分隔符號與限定詞，以及指定分行符號處理。 您也可以提交檔案的延伸模組，以及在輸出中編碼和包括標頭資料列。 因為分隔符號有可能是特殊的字元，所以如果設定是以 XML 來撰寫，您應該在 CDATA 區段中編碼它們。  
  
 下表列出以 Text 格式轉譯的裝置資訊設定。  
  
|設定|ReplTest1|  
|-------------|-----------|  
|**編碼方式**|.NET Framework 所支援之字元編碼方式的 Internet Assigned Numbers Authority (IANA) 名稱。 預設值為 **UTF-8**。 其他值的範例包括 ASCII、UTF-7 和 UTF-16。|  
|**ExcelMode**|指定 Excel 的目標輸出。 預設值為 **true**。|  
|**FieldDelimiter**|要放置於結果中的分隔符號字串。 預設值是逗號 (,)。 當以 URL 傳遞時，您應該在 URL 中編碼此裝置資訊的值。 例如，做為分隔符號的定位字元應該是 "%09"。<br /><br /> 您可以將預設欄位分隔符號變更為所需的任何字元，包括 TAB，方法是在組態檔中變更裝置資訊設定。 例如，若要使用 TAB，請將 FieldDelimiter 設定更新為 \<FieldDelimiter xml:space="preserve">[TAB]\</FieldDelimiter><br /><br /> 在範例 [TAB] 中是實際的定位字元，這表示空白會出現在組態檔中。 "xml:space" 屬性會告知剖析器以保留空白字元。|  
|**FileExtension**|在結果上放置副檔名。 預設值是 **.CSV**。 如果同時指定 **FileExtension** 和 **Extension** ，則會優先使用 **FileExtension** 。|  
|**NoHeader**|表示標頭資料列是否從輸出排除。 預設值為 **false**。|  
|**Qualifier**|要放在結果周圍的限定詞字串，包括欄位分隔符號或是記錄分隔符號。 如果結果包含分隔符號，則會重複限定詞。 **Qualifier** 設定必須與 **FieldDelimiter** 和 **RecordDelimiter** 設定不同。 預設值是引號 (")。|  
|**RecordDelimiter**|放在每個記錄結尾處的記錄分隔符號。 預設值為 \<cr>\<lf>。|  
|**SuppressLineBreaks**|指出是否從輸出中所含的資料移除分行符號。 預設值為 **false**。 如果值為 **true**，則 **FieldDelimiter**、 **RecordDelimiter**和 **Qualifier** 設定不能是空格字元。|  
|**UseFormattedValues**|指出是否將格式字串放入 CSV 輸出。 **ExcelMode** 為 **true** 時，預設值是 **true**，否則為 **false**。|  
  
## <a name="see-also"></a>另請參閱  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [將裝置資訊設定傳遞至轉譯延伸模組](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [在 RSReportServer.Config 中自訂轉譯延伸模組參數](../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [技術參考 &#40;SSRS&#41;](../reporting-services/technical-reference-ssrs.md)  
  
  
