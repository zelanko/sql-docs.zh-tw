---
title: 設定 Integration Services （SSIS 服務） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services service, configuring
- configuration files [Integration Services]
- service [Integration Services], configuring
- default configuration files
ms.assetid: 36d78393-a54c-44b0-8709-7f003f44c27f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: bf81aa02bb85ca9d0941b384d6b9959e53bd7d28
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62834399"
---
# <a name="configuring-the-integration-services-service-ssis-service"></a>設定 Integration Services 服務 (SSIS 服務)
    
> [!IMPORTANT]  
>  本主題會討論 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務，即用於管理 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 封裝的 Windows 服務。 [!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)] 支援此服務能與舊版 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]回溯相容。 從 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]開始，您可以管理 Integration Services 伺服器上的物件，例如封裝。  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務會仰賴組態檔進行設定。 根據預設，此組態檔的名稱為 MsDtsSrvr.ini.xml，而且檔案位於 %ProgramFiles%\Microsoft SQL Server\120\DTS\Binn 資料夾中。  
  
 一般來說，您不必為這個組態檔做任何變更，也不必變更此檔案的預設位置。 但是，如果您的封裝儲存在 [!INCLUDE[ssDE](../includes/ssde-md.md)]的具名執行個體或遠端執行個體中，或是儲存在多個 [!INCLUDE[ssDE](../includes/ssde-md.md)]執行個體中，您就必須修改此組態檔。 另外，如果您將此組態檔移到預設位置以外的位置，就必須修改指定其檔案位置的登錄機碼。  
  
## <a name="configuration-file-contents"></a>組態檔內容  
 當您安裝 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]時，安裝程序會針對 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務建立及安裝組態檔。 此組態檔包含下列設定：  
  
-   在服務停止時傳送停止指令給封裝。  
  
-   要在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 的 [物件總管] 中顯示的 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 根資料夾為 [MSDB] 和 [檔案系統] 資料夾。  
  
-   在檔案系統中的封裝，[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]服務管理位於 %ProgramFiles%\Microsoft SQL Server\120\DTS\Packages。  
  
 此組態檔也會指定哪一個 msdb 資料庫包含 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務將會管理的封裝。 根據預設， [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務設定為可管理 [!INCLUDE[ssDE](../includes/ssde-md.md)] 執行個體之 msdb 資料庫中的封裝，該執行個體與 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]同時安裝。 如果 [!INCLUDE[ssDE](../includes/ssde-md.md)] 執行個體並未同時安裝， [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務會設定為可管理本機預設 [!INCLUDE[ssDE](../includes/ssde-md.md)]執行個體之 msdb 資料庫中的封裝。  
  
### <a name="default-configuration-file-example"></a>預設組態檔範例  
 下列範例會顯示可指定以下設定的預設組態檔：  
  
-   當 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務停止時，封裝會停止執行。  
  
-   [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 中封裝儲存體的根資料夾為 MSDB 和檔案系統。  
  
-   此服務會管理儲存於本機預設 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]執行個體之 msdb 資料庫內的封裝。  
  
-   此服務會管理儲存於檔案系統 [封裝] 資料夾內的封裝。  
  
 **預設組態檔的範例**  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<DtsServiceConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
  <StopExecutingPackagesOnShutdown>true</StopExecutingPackagesOnShutdown>  
  <TopLevelFolders>  
    <Folder xsi:type="SqlServerFolder">  
      <Name>MSDB</Name>  
      <ServerName>.</ServerName>  
    </Folder>  
    <Folder xsi:type="FileSystemFolder">  
      <Name>File System</Name>  
      <StorePath>..\Packages</StorePath>  
    </Folder>  
  </TopLevelFolders>    
</DtsServiceConfiguration>  
```  
  
## <a name="modification-of-the-configuration-file"></a>組態檔的修改  
 您可以修改組態檔，允許封裝在服務停止時繼續執行、在 [物件總管] 中顯示其他根資料夾，或在檔案系統中指定要由 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務管理的不同資料夾或其他資料夾。 例如，您可以建立屬於 `SqlServerFolder` 類型的其他根資料夾來管理其他 [!INCLUDE[ssDE](../includes/ssde-md.md)] 執行個體之 msdb 資料庫中的封裝。  
  
> [!NOTE]  
>  某些字元在資料夾名稱中是無效的。 資料夾名稱的有效字元是由 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 類別 **System.IO.Path** 和 [GetInvalidFilenameChars]  欄位所決定。 [GetInvalidFilenameChars] 欄位提供無法在傳遞給 **Path** 類別成員之路徑字串引數中指定的平台特定字元陣列。 有效的字元集可能會因檔案系統而不同。 無效的字元通常包括引號 (")、小於 (<) 字元和縱線 (|) 字元。  
  
 但是，若要管理儲存在 [!INCLUDE[ssDE](../includes/ssde-md.md)]具名執行個體或遠端執行個體中的封裝，您就必須修改組態檔。 如果您未更新組態檔，就無法使用 **中的** 物件總管 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 來檢視儲存在具名執行個體或遠端執行個體之 msdb 資料庫中的封裝。 如果您嘗試使用 **[物件總管]** 來檢視這些封裝，您會收到下列錯誤訊息：  
  
 `Failed to retrieve data for this request. (Microsoft.SqlServer.SmoEnum)`  
  
 `The SQL Server specified in Integration Services service configuration is not present or is not available. This might occur when there is no default instance of SQL Server on the computer. For more information, see the topic "Configuring the Integration Services Service" in SQL Server 2008 Books Online.`  
  
 `Login Timeout Expired`  
  
 `An error has occurred while establishing a connection to the server. When connecting to SQL Server 2008, this failure may be caused by the fact that under the default settings SQL Server does not allow remote connections.`  
  
 `Named Pipes Provider: Could not open a connection to SQL Server [2]. (MsDtsSvr).`  
  
 若要為 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務修改此組態檔，您可使用文字編輯器。  
  
> [!IMPORTANT]  
>  在您修改服務組態檔後，必須重新啟動服務，才能使用更新的服務組態。  
  
### <a name="modified-configuration-file-example"></a>修改過的組態檔範例  
 下列範例會顯示 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]的已修改組態檔。 此檔案適用於 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的具名執行個體，該執行個體稱為 `InstanceName` 且位在名為 `ServerName`的伺服器上。  
  
 **SQL Server 具名執行個體之已修改組態檔的範例**  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<DtsServiceConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
  <StopExecutingPackagesOnShutdown>true</StopExecutingPackagesOnShutdown>  
  <TopLevelFolders>  
    <Folder xsi:type="SqlServerFolder">  
      <Name>MSDB</Name>  
      <ServerName>ServerName\InstanceName</ServerName>  
    </Folder>  
    <Folder xsi:type="FileSystemFolder">  
      <Name>File System</Name>  
      <StorePath>..\Packages</StorePath>  
    </Folder>  
  </TopLevelFolders>    
</DtsServiceConfiguration>  
```  
  
## <a name="modification-of-the-configuration-file-location"></a>組態檔位置的修改  
登錄機碼**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\SSIS\ServiceConfigFile**指定的位置和名稱的組態檔[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]服務所使用。 登錄機碼的預設值是**C:\Program Files\Microsoft SQL Server\120\DTS\Binn\MsDtsSrvr.ini.xml**。 您可以更新此登錄機碼的值，以便針對組態檔使用不同的名稱和位置。 請注意，在路徑中的版本號碼 (120 適用於 SQL Server [!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)]) 將 SQL Server 版本而有所不同。 
  
  
> [!CAUTION]  
>  不當地編輯登錄可能會造成嚴重問題，並導致您必須重新安裝作業系統。 [!INCLUDE[msCoName](../includes/msconame-md.md)] 不保證能夠解決不當編輯登錄所產生的問題。 在編輯登錄之前，請先備份重要資料。 如需有關如何備份、還原及編輯登錄的詳細資訊，請參閱 [!INCLUDE[msCoName](../includes/msconame-md.md)] 知識庫文件： [Microsoft Windows 登錄說明](https://support.microsoft.com/kb/256986)。  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務啟動時會載入組態檔。 登錄項目如有任何變更，就必須重新啟動服務。  
  
  
