---
title: "維度處理目的地編輯器 （進階頁面） |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.dimprocessingtransformation.advanced.f1
helpviewer_keywords:
- Dimension Processing Destination Editor
ms.assetid: 2b30835a-2680-4d98-89a4-4f17e29e3818
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 81e97a5a5e653fb02f0e8a1ccc5741bb3e86acf1
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="dimension-processing-destination-editor-advanced-page"></a>維度處理目的地編輯器 (進階頁面)
  使用 **[維度處理目的地編輯器]** 對話方塊的 **[進階]** 頁面，來設定錯誤處理。  
  
 若要深入了解維度處理目的地，請參閱＜ [Dimension Processing Destination](../../integration-services/data-flow/dimension-processing-destination.md)＞。  
  
## <a name="options"></a>選項。  
 **使用預設錯誤組態。**  
 指定是否要使用預設的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 錯誤處理。 依預設，此值為 **True**。  
  
 **索引鍵錯誤動作**  
 指定如何處理具有無法接受之索引鍵值的記錄。  
  
|Value|說明|  
|-----------|-----------------|  
|**ConvertToUnknown**|將無法接受的索引鍵值轉換為 **UnknownMember** 值。|  
|**DiscardRecord**|捨棄記錄。|  
  
 **忽略錯誤**  
 指定應該忽略的錯誤。  
  
 **發生錯誤時停止**  
 指定發生錯誤時，應該停止處理。  
  
 **錯誤數目**  
 如果您已選取 [發生錯誤時停止]，則指定處理應該停止的錯誤臨界值。  
  
 **發生錯誤時要執行的動作**  
 如果您已選取 [發生錯誤時停止]，則指定到達錯誤臨界值時要採取的動作。  
  
|Value|說明|  
|-----------|-----------------|  
|**StopProcessing**|停止處理。|  
|**StopLogging**|停止記錄錯誤。|  
  
 **找不到索引鍵**  
 針對找不到索引鍵錯誤，指定要採取的動作。 依預設，此值為 **ReportAndContinue**。  
  
|Value|說明|  
|-----------|-----------------|  
|**IgnoreError**|忽略錯誤並繼續處理。|  
|**ReportAndContinue**|報告錯誤並繼續處理。|  
|**ReportAndStop**|報告錯誤並停止處理。|  
  
 **重複的索引鍵**  
 針對重複索引鍵錯誤，指定要採取的動作。 依預設，此值為 **IgnoreError**。  
  
|Value|說明|  
|-----------|-----------------|  
|**IgnoreError**|忽略錯誤並繼續處理。|  
|**ReportAndContinue**|報告錯誤並繼續處理。|  
|**ReportAndStop**|報告錯誤並停止處理。|  
  
 **Null 索引鍵已轉換為未知**  
 指定當 Null 索引鍵轉換為 **UnknownMember** 值的時候應採取的動作。 依預設，此值為 **IgnoreError**。  
  
|Value|說明|  
|-----------|-----------------|  
|**IgnoreError**|忽略錯誤並繼續處理。|  
|**ReportAndContinue**|報告錯誤並繼續處理。|  
|**ReportAndStop**|報告錯誤並停止處理。|  
  
 **不允許 Null 索引鍵**  
 指定在不允許 Null 索引鍵的情況下如果發現 Null 索引鍵，所要採取的動作。 依預設，此值為 **ReportAndContinue**。  
  
|Value|說明|  
|-----------|-----------------|  
|**IgnoreError**|忽略錯誤並繼續處理。|  
|**ReportAndContinue**|報告錯誤並繼續處理。|  
|**ReportAndStop**|報告錯誤並停止處理。|  
  
 **錯誤記錄路徑**  
 輸入錯誤記錄路徑，或者按一下 [瀏覽] \(…) 按鈕以選取目的地。  
  
 **瀏覽 (...)**  
 選取錯誤記錄的路徑。  
  
## <a name="see-also"></a>請參閱＜  
 [Integration Services 錯誤和訊息參考](../../integration-services/integration-services-error-and-message-reference.md)   
 [維度處理目的地編輯器 &#40;連接管理員頁面 &#41;](../../integration-services/data-flow/dimension-processing-destination-editor-connection-manager-page.md)   
 [維度處理目的地編輯器 &#40;[對應] 頁面 &#41;](../../integration-services/data-flow/dimension-processing-destination-editor-mappings-page.md)  
  
  
