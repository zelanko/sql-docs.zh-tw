---
title: 含使用者指定設定的 XML 輸入檔案範例 (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- sample applications [DTA]
ms.assetid: b29c9716-e5c3-4003-9efb-3ade2197b630
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4fefcec96100a9848810bc37a7b02760a3005cc3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63188094"
---
# <a name="xml-input-file-sample-with-user-specified-configuration-dta"></a>含使用者指定組態的 XML 輸入檔範例 (DTA)
  請複製利用 **Configuration** 元素指定使用者指定組態的這個 XML 輸入檔範例，再將它貼到您喜愛的 XML 編輯器或文字編輯器中。 這可讓您進行「假設」分析。 「假設」分析包括利用 **Configuration** 元素來指定您要微調之資料庫的一組假設性實體設計結構。 之後，您再利用 Database Engine Tuning Advisor 來分析針對這個假設性組態來執行工作負載的效果，以了解它是否能夠改進查詢的處理效能。 這類分析的好處是既能夠評估新的組態，又免除了實際實作的負擔。 如果假設性組態所改進的效能不符需求，您很容易改變它，再分析它，直到產生的結果符合需求的組態出現為止。  
  
 將這個範例複製到編輯工具之後，請利用您的特定微調工作階段的各個值來取代指定給 **Server**、 **Database**、 **Schema**、 **Table**、 **Workload**、 **TuningOptions**和 **Configuration** 等元素的值。 如需可以搭配這些元素來使用的所有屬性和子元素的詳細資訊，請參閱 [XML 輸入檔參考 &#40;Database Engine Tuning Advisor&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)。 下列範例只用到部份可用的屬性及子元素選項。  
  
## <a name="code"></a>程式碼  
 [!code-xml[InputFileSamples#UserSpecifiedConfigInputFile](../../snippets/xml/SQL14/dta_xml/inputfilesamples/xml/dta_xml_input_file_samples.xml#userspecifiedconfiginputfile)]  
  
## <a name="comments"></a>註解  
  
-   如果您指定了 **Configuration** 元素的 **Absolute** 模式 (`Configuration SpecificationMode="Absolute"`)，便不支援卸除實體設計結構。  
  
-   您無法在**Configuration** 元素的任何一個模式 ( **Relative**或 **Absolute** ) 中，建立和卸除相同的實體設計結構。  
  
## <a name="see-also"></a>另請參閱  
 [啟動及使用 Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)   
 [檢視及處理 Database Engine Tuning Advisor 的輸出](../../relational-databases/performance/view-and-work-with-the-output-from-the-database-engine-tuning-advisor.md)   
 [XML 輸入檔參考 &#40;Database Engine Tuning Advisor&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
