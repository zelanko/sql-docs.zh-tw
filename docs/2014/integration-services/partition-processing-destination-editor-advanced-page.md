---
title: 資料分割處理目的地編輯器 （進階頁面） |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.designer.partprocessingtransformation.advanced.f1
helpviewer_keywords:
- Partition Processing Destination Editor
ms.assetid: 2039ee0f-069d-479d-90b2-2a12481b1162
caps.latest.revision: 32
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 7f81cc34213d2288512a8d063b1e11e4dfd49d53
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36022931"
---
# <a name="partition-processing-destination-editor-advanced-page"></a>資料分割處理目的地編輯器 (進階頁面)
  使用 **[資料分割處理目的地編輯器]** 對話方塊的 **[進階]** 頁面，來設定錯誤處理。  
  
 若要深入了解資料分割處理目的地，請參閱＜ [Partition Processing Destination](data-flow/partition-processing-destination.md)＞。  
  
> [!NOTE]  
>  此處描述的工作不適用於 Analysis Services 表格式模型。  您無法針對表格式模型，將輸入資料行對應至資料分割資料行。 您可以改用 Analysis Services 執行 DDL 工作 ( [Analysis Services Execute DDL Task](control-flow/analysis-services-execute-ddl-task.md) ) 來處理資料分割。  
  
## <a name="options"></a>選項。  
 **使用預設錯誤組態。**  
 指定是否要使用預設的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 錯誤處理。 依預設，此值為 `True`。  
  
 **索引鍵錯誤動作**  
 指定如何處理具有無法接受之索引鍵值的記錄。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**ConvertToUnknown**|將無法接受的索引鍵值轉換為未知值。|  
|**DiscardRecord**|捨棄記錄。|  
  
 **忽略錯誤**  
 指定應該忽略的錯誤。  
  
 **發生錯誤時停止**  
 指定發生錯誤時，應該停止處理。  
  
 **錯誤數目**  
 如果您已選取 [發生錯誤時停止]，請指定處理應該停止的錯誤臨界值。  
  
 **發生錯誤時要執行的動作**  
 如果您已選取 [發生錯誤時停止]，請指定到達錯誤臨界值時要採取的動作。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**StopProcessing**|停止處理。|  
|**StopLogging**|停止記錄錯誤。|  
  
 **找不到索引鍵**  
 針對找不到索引鍵錯誤，指定要採取的動作。 依預設，此值為 **ReportAndContinue**。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**IgnoreError**|忽略錯誤並繼續處理。|  
|**ReportAndContinue**|報告錯誤並繼續處理。|  
|**ReportAndStop**|報告錯誤並停止處理。|  
  
 **重複的索引鍵**  
 針對重複索引鍵錯誤，指定要採取的動作。 依預設，此值為 **IgnoreError**。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**IgnoreError**|忽略錯誤並繼續處理。|  
|**ReportAndContinue**|報告錯誤並繼續處理。|  
|**ReportAndStop**|報告錯誤並停止處理。|  
  
 **Null 索引鍵已轉換為未知**  
 指定當 Null 索引鍵轉換為未知值的時候應採取的動作。 依預設，此值為 **IgnoreError**。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**IgnoreError**|忽略錯誤並繼續處理。|  
|**ReportAndContinue**|報告錯誤並繼續處理。|  
|**ReportAndStop**|報告錯誤並停止處理。|  
  
 **不允許 Null 索引鍵**  
 指定在不允許 Null 索引鍵的情況下如果發現 Null 索引鍵，所要採取的動作。 依預設，此值為 **ReportAndContinue**。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**IgnoreError**|忽略錯誤並繼續處理。|  
|**ReportAndContinue**|報告錯誤並繼續處理。|  
|**ReportAndStop**|報告錯誤並停止處理。|  
  
 **錯誤記錄路徑**  
 輸入錯誤記錄檔的路徑，或者使用瀏覽 **(...)** 按鈕來選取目的地。  
  
 **瀏覽 (...)**  
 選取錯誤記錄的路徑。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [資料分割處理目的地編輯器&#40;[對應] 頁面&#41;](../../2014/integration-services/partition-processing-destination-editor-mappings-page.md)  
  
  