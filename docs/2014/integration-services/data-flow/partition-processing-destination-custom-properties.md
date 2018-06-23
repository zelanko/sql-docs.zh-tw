---
title: 資料分割處理目的地自訂屬性 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3eac4413-0c90-4b06-8f7e-d0d72f4d869d
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 2724682cebfcae1e5c6a14b9c7cd815c96ad4a7c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36035939"
---
# <a name="partition-processing-destination-custom-properties"></a>資料分割處理目的地自訂屬性
  資料分割處理目的地同時具有自訂屬性以及所有資料流程元件通用的屬性。  
  
 下表描述的是資料分割處理目的地的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性|資料類型|描述|  
|--------------|---------------|-----------------|  
|ASConnectionString|String|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案或 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]執行個體的連接字串。|  
|KeyDuplicate|整數 (列舉)|UseDefaultConfiguration 時`False`，該值指出如何處理重複索引鍵錯誤。 可能的值為`IgnoreError`(0)， `ReportAndContinue` (1)，和`ReportAndStop`(2)。 這個屬性的預設值是`IgnoreError`(0)。|  
|KeyErrorAction|整數 (列舉)|UseDefaultConfiguration 時`False`，該值指出如何處理索引鍵錯誤。 可能的值為 `ConvertToUnknown` (0) 和 `DiscardRecord` (1)。 這個屬性的預設值是`ConvertToUnknown`(0)。|  
|[KeyErrorLimit]|Integer|UseDefaultConfiguration 時`False`，允許的索引鍵錯誤上限。|  
|KeyErrorLimitAction|整數 (列舉)|UseDefaultConfiguration 時`False`，該值指出時要採取的動作`KeyErrorLimit`為止。 可能的值為`StopLogging`(1) 和`StopProcessing`(0)。 這個屬性的預設值是`StopProcessing`(0)。|  
|KeyErrorLogFile|String|UseDefaultConfiguration 時`False`，錯誤記錄檔的路徑和檔案名稱。|  
|KeyNotFound|整數 (列舉)|UseDefaultConfiguration 時`False`，該值指出如何處理遺漏索引鍵錯誤。 可能的值為`IgnoreError`(0)， `ReportAndContinue` (1)，和`ReportAndStop`(2)。 這個屬性的預設值是`ReportAndContinue`(1)。|  
|NullKeyConvertedToUnknown|整數 (列舉)|UseDefaultConfiguration 時`False`，指出如何處理 null 索引鍵的值轉換成未知的值。 可能的值為`IgnoreError`(0)， `ReportAndContinue` (1)，和`ReportAndStop`(2)。 這個屬性的預設值是`IgnoreError`(0)。|  
|NullKeyNotAllowed|整數 (列舉)|UseDefaultConfiguration 時`False`，指出如何處理不允許的 null 的值。 可能的值為`IgnoreError`(0)， `ReportAndContinue` (1)，和`ReportAndStop`(2)。 這個屬性的預設值是`ReportAndContinue`(1)。|  
|ProcessType|整數 (列舉)|轉換所使用的資料分割處理類型。 可能的值為 `ProcessAdd` (1) (累加)、`ProcessFull` (0) 和 `ProcessUpdate` (2)。|  
|UseDefaultConfiguration|布林|一個值，指定轉換是否要使用預設錯誤組態。 如果這個屬性是`False`，轉換會包括 KeyDuplicate KeyErrorAction，等下表中列出的錯誤處理自訂屬性的值。|  
  
 資料分割處理目的地的輸入和輸入資料行沒有任何自訂屬性。  
  
 如需詳細資訊，請參閱 [Partition Processing Destination](partition-processing-destination.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Common Properties](../common-properties.md)  
  
  