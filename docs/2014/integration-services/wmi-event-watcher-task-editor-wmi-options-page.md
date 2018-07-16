---
title: WMI 事件監看員工作編輯器 （WMI 選項頁面） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.wmieventwatcher.wmiquery.f1
helpviewer_keywords:
- WMI Event Watcher Task Editor
ms.assetid: 525f3de7-a021-4e52-9939-3a83c88f131a
caps.latest.revision: 37
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d034c50aebceea411baee2093175c496ea16f5d8
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37203940"
---
# <a name="wmi-event-watcher-task-editor-wmi-options-page"></a>WMI 事件監看員工作編輯器 (WMI 選項頁面)
  使用 [WMI 事件監看員工作編輯器] 對話方塊的 [WMI 選項] 頁面，即可指定 Windows Management Instrumentation 查詢語言 (WQL) 查詢的來源，以及 WMI 事件監看員工作如何回應 Microsoft Windows Instrumentation (WMI) 事件。  
  
 若要了解這項工作，請參閱 [WMI 事件監看員工作](control-flow/wmi-event-watcher-task.md)。 如需 WMI 查詢語言 (WQL) 的詳細資訊，請參閱 MSDN Library 中的 Windows Management Instrumentation 主題 [Querying with WQL](http://go.microsoft.com/fwlink/?LinkId=79045)(使用 WQL 查詢)。  
  
## <a name="static-options"></a>靜態選項  
 **WMIConnectionName**  
 在清單中選取 WMI 連線管理員，或按一下 [\<新增 WMI 連線...>] 建立新的連線管理員。  
  
 **相關主題：**[WMI 連接管理員](connection-manager/wmi-connection-manager.md)、[WMI 連接管理員編輯器](../../2014/integration-services/wmi-connection-manager-editor.md)  
  
 **WQLQuerySourceType**  
 選取工作執行之 WQL 查詢的來源類型。 這個屬性具有下表中所列的選項。  
  
|值|描述|  
|-----------|-----------------|  
|**直接輸入**|設定 WQL 查詢的來源。 選取此值會顯示動態選項 [WQLQuerySource]。|  
|**檔案連接**|選取包含 WQL 查詢的檔案。 選取此值會顯示動態選項 [WQLQuerySource]。|  
|**變數**|將來源設定為定義 WQL 查詢的變數。 選取此值會顯示動態選項 [WQLQuerySource]。|  
  
 **ActionAtEvent**  
 指定 WMI 事件是否記錄事件並起始 [!INCLUDE[ssIS](../includes/ssis-md.md)] 動作，或僅記錄事件。  
  
 **AfterEvent**  
 指定工作接收到 WMI 事件之後成功或失敗，或是工作會繼續監看事件再次發生。  
  
 **ActionAtTimeout**  
 指定工作是否記錄 WMI 查詢逾時並起始 [!INCLUDE[ssIS](../includes/ssis-md.md)] 事件作為回應，或僅記錄逾時。  
  
 **AfterTimeout**  
 指定工作回應逾時成功或失敗，或是工作會繼續監看另一個逾時再次發生。  
  
 **NumberOfEvents**  
 指定要監看的事件數目。  
  
 **逾時**  
 指定要等候事件發生的秒數。 值為 0 表示沒有逾時在作用中。  
  
## <a name="wqlquerysource-dynamic-options"></a>WQLQuerySource 動態選項  
  
### <a name="wqlquerysource--direct-input"></a>WQLQuerySource = 直接輸入  
 **WQLQuerySource**  
 提供查詢，或按一下省略符號按鈕 (...)，然後使用 [WQL 查詢] 對話方塊輸入查詢。  
  
### <a name="wqlquerysource--file-connection"></a>WQLQuerySource = 檔案連接  
 **WQLQuerySource**  
 在清單中選取檔案連線管理員，或按一下 [\<新增連線...>]，即可建立新的連線管理員。  
  
 **相關主題：** [File Connection Manager](connection-manager/file-connection-manager.md)、 [File Connection Manager Editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
### <a name="wqlquerysource--variable"></a>WQLQuerySource = 變數  
 **WQLQuerySource**  
 在清單中選取變數，或按一下 [\<新增變數...>] 建立新的變數。  
  
 **相關主題**︰[Integration Services &#40;SSIS&#41; 變數](integration-services-ssis-variables.md)、[加入變數](../../2014/integration-services/add-variable.md)  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [WMI 事件監看員工作編輯器&#40;一般頁面&#41;](general-page-of-integration-services-designers-options.md)   
 [運算式頁面](expressions/expressions-page.md)   
 [WMI 資料讀取器工作](control-flow/wmi-data-reader-task.md)  
  
  
