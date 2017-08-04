---
title: "WMI 資料讀取器工作編輯器 （WMI 選項頁面） |Microsoft 文件"
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
- sql13.dts.designer.wmidatareadertask.wmiquery.f1
helpviewer_keywords:
- WMI Data Reader Task Editor
ms.assetid: 4b8d4716-882d-41b0-b77e-e0e2741a2cd5
caps.latest.revision: 40
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2d87bb0cfa2ca6a0ad103ac803e6fac662a9d385
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="wmi-data-reader-task-editor-wmi-options-page"></a>WMI 資料讀取器工作編輯器 (WMI 選項頁面)
  使用 [WMI 資料讀取器工作編輯器] 對話方塊的 [WMI 選項] 頁面，來指定 Windows Management Instrumentation 查詢語言 (WQL) 查詢的來源和查詢結果的目的地。  
  
 若要了解這個工作，請參閱＜ [WMI Data Reader Task](../../integration-services/control-flow/wmi-data-reader-task.md)＞。 如需 WMI 查詢語言 (WQL) 的詳細資訊，請參閱 MSDN Library 中的 Windows Management Instrumentation 主題： [Querying with WQL](http://go.microsoft.com/fwlink/?LinkId=79045)(使用 WQL 查詢)。  
  
## <a name="static-options"></a>靜態選項  
 **WMIConnectionName**  
 在清單中，選取 WMI 連接管理員，或按一下\<**新增 WMI 連接...**> 以建立新的連接管理員。  
  
 **相關主題：**[WMI 連接管理員](../../integration-services/connection-manager/wmi-connection-manager.md)、[WMI 連接管理員編輯器](../../integration-services/connection-manager/wmi-connection-manager-editor.md)  
  
 **WQLQuerySourceType**  
 選取工作執行之 WQL 查詢的來源類型。 這個屬性具有下表中所列的選項。  
  
|Value|說明|  
|-----------|-----------------|  
|**直接輸入**|設定 WQL 查詢的來源。 選取這個值就會顯示 **[WQLQuerySourceType]**動態選項。|  
|**檔案連接**|選取包含 WQL 查詢的檔案。 選取這個值就會顯示 **[WQLQuerySourceType]**動態選項。|  
|**變數**|將來源設定為定義 WQL 查詢的變數。 選取這個值就會顯示 **[WQLQuerySourceType]**動態選項。|  
  
 **OutputType**  
 指定輸出應為資料表、屬性值或屬性名稱和值。  
  
 **OverwriteDestination**  
 指定是要保留、覆寫還是附加至目的地檔案或變數中的原始資料。  
  
 **DestinationType**  
 選取此工作執行之 WQL 查詢的目的地類型。 這個屬性具有下表中所列的選項。  
  
|Value|說明|  
|-----------|-----------------|  
|**檔案連接**|選取檔案以儲存 WQL 查詢的結果。 選取此值會顯示動態選項 **[DestinationType]**。|  
|**變數**|設定變數以儲存 WQL 查詢的結果。 選取此值會顯示動態選項 **[DestinationType]**。|  
  
## <a name="wqlquerysourcetype-dynamic-options"></a>WQLQuerySourceType 動態選項  
  
### <a name="wqlquerysourcetype--direct-input"></a>WQLQuerySourceType = 直接輸入  
 **WQLQuerySource**  
 提供查詢，或按一下 [省略符號 (...)]，然後使用 [WQL 查詢] 對話方塊輸入查詢。  
  
### <a name="wqlquerysourcetype--file-connection"></a>WQLQuerySourceType = 檔案連接  
 **WQLQuerySource**  
 在清單中，選取檔案連接管理員，或按一下\<**新增連接...**> 以建立新的連接管理員。  
  
 **相關主題：** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md)、 [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
### <a name="wqlquerysourcetype--variable"></a>WQLQuerySourceType = 變數  
 **WQLQuerySource**  
 在清單中，選取變數，或按一下\<**新增變數...**> 若要建立新的變數。  
  
 **相關主題**：[Integration Services &#40;SSIS&#41; 變數](../../integration-services/integration-services-ssis-variables.md)、[加入變數](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
## <a name="destinationtype-dynamic-options"></a>DestinationType 動態選項  
  
### <a name="destinationtype--file-connection"></a>DestinationType = 檔案連接  
 **目的地**  
 在清單中，選取檔案連接管理員，或按一下\<**新增連接...**> 以建立新的連接管理員。  
  
 **相關主題：** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md)、 [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
### <a name="destinationtype--variable"></a>DestinationType = 變數  
 **目的地**  
 在清單中，選取變數，或按一下\<**新增變數...**> 若要建立新的變數。  
  
 **相關主題**：[Integration Services &#40;SSIS&#41; 變數](../../integration-services/integration-services-ssis-variables.md)、[加入變數](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../integration-services/integration-services-error-and-message-reference.md)   
 [WMI 資料讀取器工作編輯器 &#40;一般頁面 &#41;](../../integration-services/control-flow/wmi-data-reader-task-editor-general-page.md)   
 [運算式頁面](../../integration-services/expressions/expressions-page.md)   
 [WMI 事件監看員工作](../../integration-services/control-flow/wmi-event-watcher-task.md)  
  
  
