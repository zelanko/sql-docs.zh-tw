---
title: "針對 Reporting Services 報表的處理進行疑難排解 | Microsoft Docs"
ms.custom: 
ms.date: 08/26/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: troubleshooting
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: bb309231-68be-4d68-a44c-c098999c67a2
caps.latest.revision: "4"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0b772d7a4a73e2aa37b35866f57064a0610c18de
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/09/2018
---
# <a name="troubleshoot-processing-of-reporting-services-reports"></a>疑難排解 Reporting Services 報表的處理
擷取報表資料之後，報表處理器會結合資料與配置資訊。 包含運算式的每一個報表項目屬性，都會在結合資料與配置的內容中進行評估。 您可以使用本主題來協助疑難排解這些問題。   
  
## <a name="my-report-definition-is-not-valid"></a>我的報表定義無效。  
在執行階段，報表處理器會結合報表定義中的資料與配置元素，然後評估報表項目屬性的運算式。   
  
報表處理器會檢查報表定義 (.rdl 檔案) 是否符合 .rdl 檔案開頭處命名空間宣告中所指定的結構描述。 如需 RDL 結構描述的詳細資訊，請參閱 [尋找報表定義結構描述版本 (SSRS)](../../reporting-services/reports/find-the-report-definition-schema-version-ssrs.md)。  
  
此外，在執行階段所評估的報表運算式必須遵循一組規則，以確保報表資料與配置可以正確結合。 當報表處理器偵測到問題時，您可能會看到下列訊息：報表 `<report name>` 的定義無效。  
  
### <a name="report-item-expressions-can-only-refer-to-fields-within-the-current-dataset-scope-or-if-inside-an-aggregate-the-specified-dataset-scope"></a>報表項目運算式僅可參考到目前資料集範圍，或指定的資料集範圍 (若報表項目運算式在彙總中時) 中的欄位。  
  
請使用下列清單來協助判斷錯誤原因：  
* 當報表包含一個以上的資料集時，位於報表主體文字方塊中的彙總運算式必須指定範圍參數。 例如， `=First(Fields!FieldName.Value, "DataSet1")`。  
  
若要指定範圍參數，請提供報表項目範圍內的資料集、資料區或群組的名稱。 如需詳細資訊，請參閱 [了解總計、彙總與內建集合的運算式範圍 (報表產生器 3.0 及 SSRS)](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md) 和 [運算式參考 (報表產生器 3.0 及 SSRS)](../../reporting-services/report-design/expression-reference-report-builder-and-ssrs.md)。  
  
### <a name="names-of-objects-must-be-greater-than-0-and-less-than-or-equal-to-256-characters"></a>物件名稱必須多於 0 個字元，並且少於或等於 256 個字元。  
報表定義中物件識別碼的長度限制為 256 個字元。 識別碼必須區分大小寫，且與 CLS 相容。 名稱必須以字母為開頭，包含字母、數字或底線 (_)，但是不含空格。 例如，文字方塊名稱或資料區名稱必須符合這些準則。   
  
若要變更物件的名稱，請在 [屬性] 窗格的工具列中，從下拉式清單中選取項目，然後捲動至 **[名稱]** 並輸入有效的物件名稱。   
  
## <a name="a-text-box-displays-error-how-do-i-fix-it"></a>如何修正顯示「#錯誤」的文字方塊？  
報表處理器在執行階段評估報表項目屬性的運算式，並偵測資料類型轉換、範圍或其他錯誤時，發生「#錯誤」訊息。   
  
資料類型錯誤通常代表預設或指定的資料類型不受支援。 範圍錯誤則代表在評估運算式時，無法使用指定的範圍。   
  
若要消除「#錯誤」訊息，您必須重新撰寫造成錯誤的運算式。 請檢視詳細的錯誤訊息，以判斷有關這個問題的詳細資訊。   
  
使用預覽，在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull.md)]中檢視 [輸出] 視窗。 在報表伺服器上檢視呼叫堆疊。 
  
  
## <a name="see-also"></a>另請參閱  
[錯誤和事件 (Reporting Services)](../../reporting-services/troubleshooting/errors-and-events-reference-reporting-services.md)
[!INCLUDE[feedback_stackoverflow_msdn_connect](../../includes/feedback-stackoverflow-msdn-connect.md)]

