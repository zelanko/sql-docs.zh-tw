---
title: CSV 裝置資訊設定 | Microsoft Docs
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
- CSV [Reporting Services]
- device information settings [Reporting Services], CSV rendering
ms.assetid: f96f83a6-50bc-48ce-9fcd-fd9e1952d40a
caps.latest.revision: 42
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 205d1ac37c78001d4f34f4f1cbc92731b88cfd1a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36032959"
---
# <a name="csv-device-information-settings"></a>CSV 裝置資訊設定
  CSV 轉譯延伸模組的裝置資訊設定，允許變更分隔符號與限定詞，以及指定分行符號處理。 您也可以提交檔案的延伸模組，以及在輸出中編碼和包括標頭資料列。 因為分隔符號有可能是特殊的字元，所以如果設定是以 XML 來撰寫，您應該在 CDATA 區段中編碼它們。  
  
 下表列出以 Text 格式轉譯的裝置資訊設定。  
  
|設定|ReplTest1|  
|-------------|-----------|  
|`Encoding`|.NET Framework 所支援之字元編碼方式的 Internet Assigned Numbers Authority (IANA) 名稱。 預設值是 `UTF-8`。 其他值的範例包括 ASCII、UTF-7 和 UTF-16。|  
|`ExcelMode`|指定 Excel 的目標輸出。 預設值是 `true`。|  
|`FieldDelimiter`|要放置於結果中的分隔符號字串。 預設值是逗號 (,)。 當以 URL 傳遞時，您應該在 URL 中編碼此裝置資訊的值。 例如，做為分隔符號的定位字元應該是 "%09"。<br /><br /> 您可以將預設欄位分隔符號變更為所需的任何字元，包括 TAB，方法是在組態檔中變更裝置資訊設定。 例如，若要使用 TAB，請將 FieldDelimiter 設定更新為 \<FieldDelimiter xml:space="preserve">[TAB]\</FieldDelimiter><br /><br /> 在範例 [TAB] 中是實際的定位字元，這表示空白會出現在組態檔中。 "xml:space" 屬性會告知剖析器以保留空白字元。|  
|`FileExtension`|在結果上放置副檔名。 預設值是 `.CSV`。 如果同時指定 `FileExtension` 與 `Extension`，則 `FileExtension` 具有更高的優先順序。|  
|**NoHeader**|表示標頭資料列是否從輸出排除。 預設值是 `false`。|  
|`Qualifier`|要放在結果周圍的限定詞字串，包括欄位分隔符號或是記錄分隔符號。 如果結果包含分隔符號，則會重複限定詞。 `Qualifier` 設定必須不同於 `FieldDelimiter` 與 `RecordDelimiter` 設定。 預設值是引號 (")。|  
|`RecordDelimiter`|放在每個記錄結尾處的記錄分隔符號。 預設值為 \<cr>\<lf>。|  
|**SuppressLineBreaks**|指出是否從輸出中所含的資料移除分行符號。 預設值是 `false`。 如果值為`true`、 `FieldDelimiter`， `RecordDelimiter`，和`Qualifier`設定不能是空格字元。|  
|`UseFormattedValues`|指出是否將格式字串放入 CSV 輸出。 預設值是`true`時`ExcelMode`是`true`; 否則就是`false`。|  
  
## <a name="see-also"></a>另請參閱  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [將裝置資訊設定傳遞至轉譯延伸模組](report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [在 RSReportServer.Config 中自訂轉譯延伸模組參數](customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [技術參考 &#40;SSRS&#41;](../../2014/reporting-services/technical-reference-ssrs.md)  
  
  