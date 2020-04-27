---
title: 維度處理目的地自訂屬性 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 9700f663-53f2-49b6-b1ef-92c7b752d6a1
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b63e508f87b9766507c541a7ed81e42466bbd1e8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62827369"
---
# <a name="dimension-processing-destination-custom-properies"></a>維度處理目的地自訂屬性
  維度處理目的地同時具有自訂屬性以及所有資料流程元件通用的屬性。  
  
 下表描述的是維度處理目的地的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性|資料類型|描述|  
|--------------|---------------|-----------------|  
|ASConnectionString|String|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體或 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案的連接字串。|  
|KeyDuplicate|整數 (列舉)|當 UseDefaultConfiguration 為`False`時，就是指出如何處理重複索引鍵錯誤的值。 可能的值為 `IgnoreError` (0)、`ReportAndContinue` (1) 和 `ReportAndStop` (2)。 此屬性的預設值為 `IgnoreError` (0)。|  
|KeyErrorAction|整數 (列舉)|當 UseDefaultConfiguration 為`False`時，就是指出如何處理索引鍵錯誤的值。 可能的值為 `ConvertToUnknown` (0) 和 `DiscardRecord` (1)。 此屬性的預設值為 `ConvertToUnknown` (0)。|  
|[KeyErrorLimit]|整數|當 UseDefaultConfiguration 為`False`時，就是啟用的索引鍵錯誤上限。|  
|KeyErrorLimitAction|整數 (列舉)|當 UseDefaultConfiguration 為`False`時，就是指出到達時`KeyErrorLimit`要採取之動作的值。 可能的值為 `StopLogging` (1) 和 `StopProcessing` (0)。 此屬性的預設值為 `StopProcessing` (0)。|  
|KeyErrorLogFile|String|當 UseDefaultConfiguration 為`False`時，就是錯誤記錄檔的路徑和檔案名。|  
|KeyNotFound|整數 (列舉)|當 UseDefaultConfiguration 為`False`時，就是指出如何處理遺漏索引鍵錯誤的值。 可能的值為 `IgnoreError` (0)、`ReportAndContinue` (1) 和 `ReportAndStop` (2)。 此屬性的預設值為 `IgnoreError` (0)。|  
|NullKeyConvertedToUnknown|整數 (列舉)|當 UseDefaultConfiguration 為`False`時，就是指出如何處理轉換成未知值之 null 索引鍵的值。 可能的值為 `IgnoreError` (0)、`ReportAndContinue` (1) 和 `ReportAndStop` (2)。 此屬性的預設值為 `IgnoreError` (0)。|  
|NullKeyNotAllowed|整數 (列舉)|當 UseDefaultConfiguration 為`False`時，就是指出如何處理不允許之 null 的值。 可能的值為 `IgnoreError` (0)、`ReportAndContinue` (1) 和 `ReportAndStop` (2)。 此屬性的預設值為 `IgnoreError` (0)。|  
|ProcessType|整數 (列舉)|轉換所使用的維度處理類型。 值為 `ProcessAdd` (1) (累加)、`ProcessFull` (0) 和 `ProcessUpdate` (2)。|  
|UseDefaultConfiguration|Boolean|一個值，指定轉換是否要使用預設錯誤組態。 如果此屬性為 `False`，轉換就會包含有關錯誤處理的資訊。|  
  
 維度處理目的地的輸入和輸入資料行沒有任何自訂屬性。  
  
 如需詳細資訊，請參閱 [維度處理目的地](dimension-processing-destination.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Common Properties](../common-properties.md)  
  
  
