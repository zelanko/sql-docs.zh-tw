---
title: "管理 Integration Services 服務 | Microsoft Docs"
ms.custom: ""
ms.date: "08/26/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Integration Services 服務, 設定"
  - "服務 [Integration Services], 設定"
ms.assetid: 45554117-a0df-4830-b41c-5ebb33b764a5
caps.latest.revision: 63
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 63
---
# 管理 Integration Services 服務
    
> **重要！！** 本主題會討論 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務，即用於管理 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝的 Windows 服務。 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 支援此服務能與舊版 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]回溯相容。 從 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]開始，您可以管理 Integration Services 伺服器上的物件，例如封裝。  
  
 當安裝 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]元件時，也會安裝 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務。 根據預設， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務會啟動，而且服務的啟動類型會設為自動。 不過，您也必須安裝 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 才能使用此服務來管理已儲存和執行中的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝。  
  
> **注意：**若要直接連接到舊版 Integration Services 服務的執行個體，您必須使用 SQL Server Management Studio (SSMS) 版本以及在其上執行 Integration Services 服務的 SQL Server 版本。 例如，若要連接到 SQL Server 2016 執行個體上執行的舊版 Integration Services 服務，您必須使用針對 SQL Server 2016 所發行的 SSMS 版本。 [下載 SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx)。
>
>   在 SSMS [連接到伺服器] 對話方塊中，您無法輸入執行舊版 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務的伺服器名稱。 不過，若要管理儲存在遠端伺服器上的封裝，您不必連接到該遠端伺服器上的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務執行個體。 而是要編輯 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務的組態檔，好讓 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 顯示儲存在遠端伺服器上的封裝。 如需詳細資訊，請參閱[設定 Integration Services 服務 &#40;SSIS 服務&#41;](../../integration-services/service/configuring-the-integration-services-service-ssis-service.md)。  
  
 您在一部電腦上只能安裝單一 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務的執行個體。 此服務並非特定 [!INCLUDE[ssDE](../../includes/ssde-md.md)]執行個體特有的。 您可以使用執行服務所在之電腦的名稱來連接至服務。  
  
 您可以使用下列其中一個 Microsoft Management Console (MMC) 嵌入式管理單元來管理 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務：SQL Server 組態管理員或服務。 您必須先確定服務已啟動，然後才能管理 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的封裝。  
  
 根據預設，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務設定為可管理 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體之 msdb 資料庫中的封裝，該執行個體與 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 同時安裝。 如果 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體並未同時安裝，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務會設定為可管理本機預設 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體之 msdb 資料庫中的封裝。 若要管理儲存在 [!INCLUDE[ssDE](../../includes/ssde-md.md)]具名或遠端執行個體中的封裝，或儲存在多個 [!INCLUDE[ssDE](../../includes/ssde-md.md)]執行個體中的封裝，您就必須修改此服務的組態檔。 如需詳細資訊，請參閱[設定 Integration Services 服務 &#40;SSIS 服務&#41;](../../integration-services/service/configuring-the-integration-services-service-ssis-service.md)。  
  
 依預設， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務會設定為在服務停止時停止執行中的封裝。 不過， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務不會等待封裝停止，在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務停止後，仍可能有部份封裝在執行中。  
  
 如果 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務已停止，可以使用 [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈]、[!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師、執行封裝公用程式及 **dtexec** 命令提示字元公用程式 (dtexec.exe) 繼續執行封裝。 不過，您無法監視執行中的封裝。  
  
 根據預設， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務會在 NETWORK SERVICE 帳戶內容中執行。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務會寫入 Windows 事件記錄檔。 您可以在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中檢視服務事件。 此外，您也可以使用「Windows 事件檢視器」來檢視服務事件。  
  
### 若要使用「服務」嵌入式管理單元設定 Integration Services 服務的屬性  
  
-   [設定 Integration Services 服務的屬性](../../integration-services/service/set-the-properties-of-the-integration-services-service.md)  
  
### 檢視 Integration Services 服務的服務事件  
  
-   [檢視 Integration Services 服務的事件](../../integration-services/service/view-events-for-the-integration-services-service.md)  
  
## 請參閱＜  
 [Integration Services 服務 &#40;SSIS 服務&#41;](../../integration-services/service/integration-services-service-ssis-service.md)   
 [設定 Integration Services 服務 &#40;SSIS 服務&#41;](../../integration-services/service/configuring-the-integration-services-service-ssis-service.md)   
 [SQL Server 匯入和匯出精靈](../Topic/SQL%20Server%20Import%20and%20Export%20Wizard.md)   
 [dtexec 公用程式](../../integration-services/packages/dtexec-utility.md)   
 [執行專案和封裝](https://msdn.microsoft.com/library/ms141708(v=sql.130).aspx)  
  
  