---
title: "WMI 資料讀取器工作 |Microsoft 文件"
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
- sql13.dts.designer.wmidatareadertask.f1
helpviewer_keywords:
- WQL [Integration Services]
- WMI Data Reader task [Integration Services]
ms.assetid: dae57067-0275-4ac3-8f34-1b9d169f1112
caps.latest.revision: 49
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: c3e47e4a5ae297202ba43679fba393421880a7ea
ms.openlocfilehash: 9edd5e03a79fde1aa580a47c3df294e59957e896
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="wmi-data-reader-task"></a>WMI 資料讀取器工作
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
 WQL 是 SQL 用語，其包含的延伸模組可支援 WMI 事件通知和其他 WMI 特定功能。 如需有關 WQL 的詳細資訊，請參閱 [MSDN Library](http://go.microsoft.com/fwlink/?linkid=7022)中的 Windows Management Instrumentation 文件集。  
  
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
 下表列出「WMI 資料讀取器」工作的自訂記錄項目。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 記錄](../../integration-services/performance/integration-services-ssis-logging.md)。  
  
|記錄項目|說明|  
|---------------|-----------------|  
|**WMIDataReaderGettingWMIData**|指出工作已經開始讀取 WMI 資料。|  
|**WMIDataReaderOperation**|報告工作已執行的 WQL 查詢。|  
  
## <a name="configuration-of-the-wmi-data-reader-task"></a>設定 WMI 資料讀取器工作  
 您可以程式設計方式或透過「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」設定屬性。  
  
 如需有關可以在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [WMI 資料讀取器工作編輯器 &#40;WMI 選項頁面&#41;](../../integration-services/control-flow/wmi-data-reader-task-editor-wmi-options-page.md)  
  
-   [運算式頁面](../../integration-services/expressions/expressions-page.md)  
  
 如需有關如何以程式設計方式設定這些屬性的詳細資訊，請按以下主題：  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.WmiDataReaderTask.WmiDataReaderTask>  
  
## <a name="related-tasks"></a>相關工作  
 如需有關如何在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定這些屬性的詳細資訊，請按下列主題：  
  
-   [設定工作或容器的屬性](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="see-also"></a>請參閱＜  
 [Integration Services 工作](../../integration-services/control-flow/integration-services-tasks.md)   
 [控制流程](../../integration-services/control-flow/control-flow.md)  
  
  
