---
title: WMI 資料讀取器工作 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.wmidatareadertask.f1
- sql13.dts.designer.wmidatareadertask.general.f1
- sql13.dts.designer.wmidatareadertask.wmiquery.f1
helpviewer_keywords:
- WQL [Integration Services]
- WMI Data Reader task [Integration Services]
ms.assetid: dae57067-0275-4ac3-8f34-1b9d169f1112
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e0c1b30985bf93ff1b04af85e45bf64e53c75853
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "71293724"
---
# <a name="wmi-data-reader-task"></a>WMI 資料讀取器工作

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  「WMI 資料讀取器」工作使用「Windows Management Instrumentation (WMI) 查詢語言」執行查詢，該查詢語言會從 WMI 傳回有關電腦系統的資訊。 您可將「WMI 資料讀取器」工作用於下列用途：  
  
-   查詢本機或遠端電腦上的 Windows 事件記錄檔，並將相關資訊寫入檔案或變數。  
  
-   取得硬體元件之存在、狀態或屬性的相關資訊，然後使用這些資訊判斷是否應該執行控制流程中的其他工作。  
  
-   取得應用程式的清單，並判斷每個應用程式的安裝版本。  
  
 您可以利用下列方式設定「WMI 資料讀取器」工作：  
  
-   指定要使用的 WMI 連接管理員。  
  
-   指定 WQL 查詢的來源。 查詢可以儲存在工作屬性中，也可以儲存在工作之外的變數或檔案中。  
  
-   定義 WQL 查詢結果的格式。 該工作支援資料表、屬性名稱/值配對或屬性值格式。  
  
-   指定查詢的目的地。 目的地可以是變數或檔案。  
  
-   指示是否覆寫、保留或附加查詢目的地。  
  
 如果來源或目的地是一個檔案，則「WMI 資料讀取器」工作會使用「檔案」連接管理員連接到該檔案。 如需相關資訊，請參閱 [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md)。  
  
 「WMI 資料讀取器」工作使用 WMI 連接管理員連接到可從中讀取 WMI 資訊的伺服器。 如需相關資訊，請參閱 [WMI Connection Manager](../../integration-services/connection-manager/wmi-connection-manager.md)。  
  
## <a name="wql-query"></a>WQL 查詢  
 WQL 是 SQL 用語，其包含的延伸模組可支援 WMI 事件通知和其他 WMI 特定功能。 如需有關 WQL 的詳細資訊，請參閱 [MSDN Library](https://go.microsoft.com/fwlink/?linkid=7022)中的 Windows Management Instrumentation 文件集。  
  
> [!NOTE]  
>  不同 Windows 版本的 WMI 類別也有所不同。  
  
 下列 WQL 查詢會傳回「應用程式」記錄事件中的項目。  
  
```  
SELECT * FROM Win32_NTLogEvent WHERE LogFile = 'Application' AND (SourceName='SQLISService' OR SourceName='SQLISPackage') AND TimeGenerated > '20050117'  
```  
  
 以下 WQL 查詢傳回邏輯磁碟資訊。  
  
```  
SELECT FreeSpace, DeviceId, Size, SystemName, Description FROM Win32_LlogicalDisk  
```  
  
 以下 WQL 查詢將「快速修復工程」(QFE) 更新的清單傳回至作業系統。  
  
```  
Select * FROM Win32_QuickFixEngineering  
```  
  
## <a name="custom-logging-messages-available-on-the-wmi-data-reader-task"></a>WMI 資料讀取器工作上可用的自訂記錄訊息  
 下表列出「WMI 資料讀取器」工作的自訂記錄項目。 如需詳細資訊，請參閱 [集成服務 &#40;SSIS&#41; 記錄](../../integration-services/performance/integration-services-ssis-logging.md)。  
  
|記錄項目|描述|  
|---------------|-----------------|  
|**WMIDataReaderGettingWMIData**|指出工作已經開始讀取 WMI 資料。|  
|**WMIDataReaderOperation**|報告工作已執行的 WQL 查詢。|  
  
## <a name="configuration-of-the-wmi-data-reader-task"></a>設定 WMI 資料讀取器工作  
 您可以程式設計方式或透過「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」設定屬性。  
  
 如需有關可在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定之屬性的詳細資訊，請按下列主題：  
  
-   [運算式頁面](../../integration-services/expressions/expressions-page.md)  
  
 如需有關如何以程式設計方式設定這些屬性的詳細資訊，請按以下主題：  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.WmiDataReaderTask.WmiDataReaderTask>  
  
## <a name="related-tasks"></a>相關工作  
 如需有關如何在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定這些屬性的詳細資訊，請按下列主題：  
  
-   [設定工作或容器的屬性](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="wmi-data-reader-task-editor-general-page"></a>WMI 資料讀取器工作編輯器 (一般頁面)
  使用 **[WMI 資料讀取器工作編輯器]** 對話方塊的 **[一般]** 頁面，即可命名和描述 WMI 資料讀取器工作。  
  
  如需 WMI 查詢語言 (WQL) 的詳細資訊，請參閱 MSDN Library 中的 Windows Management Instrumentation 主題 [Querying with WQL](/windows/win32/wmisdk/querying-with-wql)(使用 WQL 查詢)。  
  
### <a name="options"></a>選項。  
 **名稱**  
 提供 WMI 資料讀取器工作的唯一名稱。 這個名稱是作為工作圖示中的標籤使用。  
  
> [!NOTE]  
>  工作名稱在封裝內必須是唯一的。  
  
 **說明**  
 輸入 WMI 資料讀取器工作的描述。  
  
## <a name="wmi-data-reader-task-editor-wmi-options-page"></a>WMI 資料讀取器工作編輯器 (WMI 選項頁面)
  使用 [WMI 資料讀取器工作編輯器]  對話方塊的 [WMI 選項]  頁面，來指定 Windows Management Instrumentation 查詢語言 (WQL) 查詢的來源和查詢結果的目的地。  
  
 如需 WMI 查詢語言 (WQL) 的詳細資訊，請參閱 MSDN Library 中的 Windows Management Instrumentation 主題 [Querying with WQL](/windows/win32/wmisdk/querying-with-wql)(使用 WQL 查詢)。  
  
### <a name="static-options"></a>靜態選項  
 **WMIConnectionName**  
 在清單中選取 WMI 連線管理員，或按一下 [\<新增 WMI 連線...>]  建立新的連線管理員。  
  
 **相關主題：** [WMI 連線管理員](../../integration-services/connection-manager/wmi-connection-manager.md)、[WMI 連線管理員編輯器](../../integration-services/connection-manager/wmi-connection-manager-editor.md)  
  
 **WQLQuerySourceType**  
 選取工作執行之 WQL 查詢的來源類型。 這個屬性具有下表中所列的選項。  
  
|值|描述|  
|-----------|-----------------|  
|**直接輸入**|設定 WQL 查詢的來源。 選取這個值就會顯示 **[WQLQuerySourceType]** 動態選項。|  
|**檔案連接**|選取包含 WQL 查詢的檔案。 選取這個值就會顯示 **[WQLQuerySourceType]** 動態選項。|  
|**變數**|將來源設定為定義 WQL 查詢的變數。 選取這個值就會顯示 **[WQLQuerySourceType]** 動態選項。|  
  
 **OutputType**  
 指定輸出應為資料表、屬性值或屬性名稱和值。  
  
 **OverwriteDestination**  
 指定是要保留、覆寫還是附加至目的地檔案或變數中的原始資料。  
  
 **DestinationType**  
 選取此工作執行之 WQL 查詢的目的地類型。 這個屬性具有下表中所列的選項。  
  
|值|描述|  
|-----------|-----------------|  
|**檔案連接**|選取檔案以儲存 WQL 查詢的結果。 選取此值會顯示動態選項 **[DestinationType]** 。|  
|**變數**|設定變數以儲存 WQL 查詢的結果。 選取此值會顯示動態選項 **[DestinationType]** 。|  
  
### <a name="wqlquerysourcetype-dynamic-options"></a>WQLQuerySourceType 動態選項  
  
#### <a name="wqlquerysourcetype--direct-input"></a>WQLQuerySourceType = 直接輸入  
 **WQLQuerySource**  
 提供查詢，或按一下省略符號 (...)，然後使用 [WQL 查詢]  對話方塊輸入查詢。  
  
#### <a name="wqlquerysourcetype--file-connection"></a>WQLQuerySourceType = 檔案連接  
 **WQLQuerySource**  
 在清單中選取檔案連線管理員，或按一下 [\<新增連線...>]  ，即可建立新的連線管理員。  
  
 **相關主題：** [檔案連線管理員](../../integration-services/connection-manager/file-connection-manager.md)、[檔案連線管理員編輯器](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
#### <a name="wqlquerysourcetype--variable"></a>WQLQuerySourceType = 變數  
 **WQLQuerySource**  
 在清單中選取變數，或按一下 [\<新增變數...>]  建立新的變數。  
  
 **相關主題：** [Integration Services &#40;SSIS&#41; 變數](../../integration-services/integration-services-ssis-variables.md)、[新增變數](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
### <a name="destinationtype-dynamic-options"></a>DestinationType 動態選項  
  
#### <a name="destinationtype--file-connection"></a>DestinationType = 檔案連接  
 **目的地**  
 在清單中選取檔案連線管理員，或按一下 [\<新增連線...>]  ，即可建立新的連線管理員。  
  
 **相關主題：** [檔案連線管理員](../../integration-services/connection-manager/file-connection-manager.md)、[檔案連線管理員編輯器](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
#### <a name="destinationtype--variable"></a>DestinationType = 變數  
 **目的地**  
 在清單中選取變數，或按一下 [\<新增變數...>]  建立新的變數。  
  
 **相關主題：** [Integration Services &#40;SSIS&#41; 變數](../../integration-services/integration-services-ssis-variables.md)、[新增變數](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 工作](../../integration-services/control-flow/integration-services-tasks.md)   
 [控制流程](../../integration-services/control-flow/control-flow.md)  
  
  
