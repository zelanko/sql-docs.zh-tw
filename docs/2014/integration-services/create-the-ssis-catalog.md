---
title: 建立 SSIS 目錄 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 6ed56d36-18d9-40c2-b51f-f2a4c71d1e73
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 38f2e94ab794accb8f3b951d0affab2451624748
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84917198"
---
# <a name="create-the-ssis-catalog"></a>建立 SSIS 目錄
  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中設計和測試封裝之後，可以將包含封裝的專案，部署到 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 伺服器。 在您將專案部署至 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 伺服器之前，該伺服器必須包含 `SSISDB` 目錄。 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 的安裝程式不會自動建立目錄，您必須依照下列指示手動建立目錄。  
  
 您可以在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]中建立 SSISDB 目錄。 您也可以使用 Windows PowerShell 以程式設計方式建立目錄。  
  
### <a name="to-create-the-ssisdb-catalog-in-sql-server-management-studio"></a>若要在 SQL Server Management Studio 中建立 SSISDB 目錄  
  
1.  開啟 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]。  
  
2.  連接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Database Engine。  
  
3.  在物件總管中，展開伺服器節點，以滑鼠右鍵按一下 [Integration Services 目錄] **** 節點，然後按一下 [建立目錄] ****。  
  
4.  按一下 **[啟用 CLR 整合]**。  
  
     目錄便會使用 CLR 預存程序。  
  
5.  按一下 [在 SQL Server 啟動時允許自動執行 Integration Services 預存程序]****，讓 [catalog.startup](/sql/integration-services/system-stored-procedures/catalog-startup) 預存程序會在每次 [!INCLUDE[ssIS](../includes/ssis-md.md)] 伺服器執行個體重新啟動時執行。  
  
     預存程序會執行 SSISDB 目錄之作業狀態的維護。 它會在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 伺服器執行個體效能降低時，修正正在執行之任何封裝的狀態。  
  
6.  輸入密碼，然後按一下 **[確定]**。  
  
     此密碼保護用來加密目錄資料的資料庫主要金鑰。 請將密碼儲存在安全位置。 建議您同時備份資料庫主要金鑰。 如需相關資訊，請參閱 [Back Up a Database Master Key](../relational-databases/security/encryption/back-up-a-database-master-key.md)。  
  
### <a name="to-create-the-ssisdb-catalog-programmatically"></a>若要以程式設計方式建立 SSISDB 目錄  
  
1.  執行下列 PowerShell 指令碼：  
  
    ```powershell
    # Load the IntegrationServices Assembly  
    [Reflection.Assembly]::LoadWithPartialName("Microsoft.SqlServer.Management.IntegrationServices")  
  
    # Store the IntegrationServices Assembly namespace to avoid typing it every time  
    $ISNamespace = "Microsoft.SqlServer.Management.IntegrationServices"  
  
    Write-Host "Connecting to server ..."  
  
    # Create a connection to the server  
    $sqlConnectionString = "Data Source=localhost;Initial Catalog=master;Integrated Security=SSPI;"  
    $sqlConnection = New-Object System.Data.SqlClient.SqlConnection $sqlConnectionString  
  
    # Create the Integration Services object  
    $integrationServices = New-Object $ISNamespace".IntegrationServices" $sqlConnection  
  
    # Provision a new SSIS Catalog  
    $catalog = New-Object $ISNamespace".Catalog" ($integrationServices, "SSISDB", "P@assword1")  
    $catalog.Create()
    ```  
  
     如需如何使用 Windows PowerShell 和 <xref:Microsoft.SqlServer.Management.IntegrationServices> 命名空間的其他範例，請參閱 blogs.msdn.com 上的部落格文章：[SQL Server 2012 中的 SSIS 和 PowerShell](https://go.microsoft.com/fwlink/?LinkId=242539)。 如需此命名空間的概觀和程式碼範例，請參閱 blogs.msdn.com 上的部落格文章： [SSIS 目錄管理物件模型初探](https://techcommunity.microsoft.com/t5/sql-server-integration-services/a-glimpse-of-the-ssis-catalog-managed-object-model/ba-p/387892)。  
  
## <a name="see-also"></a>另請參閱  
 [SSIS 目錄](catalog/ssis-catalog.md)   
 [備份、 還原和移動的 SSIS 目錄](../../2014/integration-services/backup-restore-and-move-the-ssis-catalog.md)  
