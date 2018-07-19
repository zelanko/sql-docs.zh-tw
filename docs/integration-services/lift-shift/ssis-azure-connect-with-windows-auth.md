---
title: 使用 Windows 驗證連線至資料來源和檔案共用 | Microsoft Docs
description: 了解如何在 Azure SQL Database 與 Azure-SSIS Integration Runtime 中設定 SSIS 目錄，以執行利用 Windows 驗證來連線至資料來源和檔案共用的套件。
ms.date: 06/27/2018
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.suite: sql
ms.custom: ''
ms.technology: integration-services
author: swinarko
ms.author: sawinark
ms.reviewer: douglasl
manager: craigg
ms.openlocfilehash: c2b7a091b4bfe5add722ad224adc175b06817a74
ms.sourcegitcommit: c582de20c96242f551846fdc5982f41ded8ae9f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/28/2018
ms.locfileid: "37066018"
---
# <a name="connect-to-data-sources-and-file-shares-with-windows-authentication-from-ssis-packages-in-azure"></a>在 Azure 中從 SSIS 套件使用 Windows 驗證來連線至資料來源和檔案共用
無論是在內部部署/Azure 虛擬機器上及 Azure 檔案中，您都可以使用 Windows 驗證來連線至與 Azure SSIS Integration Runtime (IR) 相同虛擬網路中的資料來源與檔案共用。 從在 Azure-SSIS IR 上執行的 SSIS 套件，使用 Windows 驗證連線至資料來源與檔案共用的方法有三種：

| 連線方法 | 有效範圍 | 設定步驟 | 套件中的存取方法 | 認證組數和已連線資源 | 已連線資源的類型 | 
|---|---|---|---|---|---|
| 透過 `cmdkey` 命令保存認證 | 每個 Azure SSIS IR | 佈建/重新設定 Azure-SSIS IR 時以自訂安裝指令碼 (`main.cmd`) 執行 `cmdkey` 命令，例如：`cmdkey /add:fileshareserver /user:xxx /pass:yyy`。<br/><br/> 如需詳細資訊，請參閱[自訂 Azure SSIS IR 的安裝](https://docs.microsoft.com/en-us/azure/data-factory/how-to-configure-azure-ssis-ir-custom-setup)。 | 透過 UNC 路徑 (例如：`\\fileshareserver\folder`) 直接存取套件中的資源 | 支援針對不同的連線資源使用多組認證 | - 內部部署/Azure VM 上的檔案共用<br/><br/> - Azure 檔案，請參閱[使用 Azure 檔案共用](https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-use-files-windows) <br/><br/> - SQL Server 搭配 Windows 驗證<br/><br/> - 其他資源搭配 Windows 驗證 |
| 設定目錄層級的執行內容 | 每個 Azure SSIS IR | 執行 SSISDB `catalog.set_execution_credential` 預存程序，以設定「執行身分」內容。<br/><br/> 如需詳細資訊，請參閱本文下方的其餘部分。 | 直接存取套件中的資源 | 針對所有已連線的資源只支援一組認證 | - 內部部署/Azure VM 上的檔案共用<br/><br/> - Azure 檔案，請參閱[使用 Azure 檔案共用](https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-use-files-windows) <br/><br/> - SQL Server 搭配 Windows 驗證<br/><br/> - 其他資源搭配 Windows 驗證 | 
| 在套件執行期間裝載磁碟機 (非持續性) | 每個套件 | 以在套件控制流程一開始加入的「執行處理工作」執行 `net use` 命令，例如：`net use D: \\fileshareserver\sharename` | 透過對應磁碟機存取檔案共用 | 支援不同的檔案共用使用多個磁碟機 | - 內部部署/Azure VM 上的檔案共用<br/><br/> - Azure 檔案，請參閱[使用 Azure 檔案共用](https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-use-files-windows) |
|||||||

> [!WARNING]
> 如果您不使用上述的任何方法利用 Windows 驗證來連線至資料來源與檔案共用，相依於 Windows 驗證的套件會無法與它們連線，而且會在執行階段失敗。 

本文的其餘部分描述如何在 Azure SQL Database 中設定 SSIS 目錄以執行套件，這些套件會使用 Windows 驗證來連線至資料來源和檔案共用。 

## <a name="you-can-only-use-one-set-of-credentials"></a>您只能使用一組認證
在此方法中，一個套件只能使用一組認證。 遵循本文步驟將所提供的網域認證套用於 Azure-SSIS IR 上的所有套件執行 (互動或排程)，直到您變更或移除這些認證為止。 如果您的套件必須使用不同組認證連線到多個資料來源與檔案共用，您可能必須考慮上述替代方法。

## <a name="provide-domain-credentials-for-windows-authentication"></a>提供 Windows 驗證的網域認證
若要提供網域認證，讓套件使用 Windows 驗證以連線至內部部署資料來源/檔案共用，請執行下列動作：

1.  使用 SQL Server Management Studio (SSMS) 或其他工具，連線至裝載 SSIS 目錄資料庫 (SSISDB) 的 SQL Database。 如需詳細資訊，請參閱[連線至 Azure 中的 SSIS 目錄 (SSISDB)](ssis-azure-connect-to-catalog-database.md)。

2.  使用 SSISDB 作為目前的資料庫，開啟查詢視窗。

3.  執行下列預存程序，並提供適當的網域認證：

    ```sql
    catalog.set_execution_credential @user='<your user name>', @domain='<your domain name>', @password='<your password>'
    ```

4.  執行 SSIS 套件。 套件會使用您提供的認證，使用 Windows 驗證連線至內部部署資料來源/檔案共用。

### <a name="view-domain-credentials"></a>檢視網域認證
若要檢視作用中的網域認證，請執行下列動作：

1.  使用 SQL Server Management Studio (SSMS) 或其他工具，連線至裝載 SSIS 目錄資料庫 (SSISDB) 的 SQL Database。

2.  使用 SSISDB 作為目前的資料庫，開啟查詢視窗。

3.  執行下列預存程序並檢查輸出：

    ```sql
    SELECT * 
    FROM catalog.master_properties
    WHERE property_name = 'EXECUTION_DOMAIN' OR property_name = 'EXECUTION_USER'
    ```

### <a name="clear-domain-credentials"></a>清除網域認證
若要清除並移除本文中所述您所提供的認證，請執行下列動作：

1.  使用 SQL Server Management Studio (SSMS) 或其他工具，連線至裝載 SSIS 目錄資料庫 (SSISDB) 的 SQL Database。

2.  使用 SSISDB 作為目前的資料庫，開啟查詢視窗。

3.  執行下列預存程序：

    ```sql
    catalog.set_execution_credential @user='', @domain='', @password=''
    ```

## <a name="connect-to-an-on-premises-sql-server"></a>連線到內部部署 SQL Server
若要檢查是否可以連線至內部部署 SQL Server，請執行下列動作：

1.  若要執行此測試，請尋找未加入網域的電腦。

2.  在未加入網域的電腦上，執行下列命令，以您想要使用的網域認證啟動 SQL Server Management Studio (SSMS)：

    ```cmd
    runas.exe /netonly /user:<domain>\<username> SSMS.exe
    ```

3.  從 SSMS 中，檢查是否可以連線至您想要使用的內部部署 SQL Server。

### <a name="prerequisites"></a>先決條件
若要從 Azure 上執行的套件連線到內部部署 SQL Server，您必須啟用下列先決條件：

1.  在 SQL Server 組態管理員中，啟用 TCP/IP 通訊協定。
2.  允許通過 Windows 防火牆進行存取。 如需詳細資訊，請參閱[設定 Windows 防火牆以允許 SQL Server 存取](https://docs.microsoft.com/sql/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access)。
3.  若要使用 Windows 驗證進行連線，請確定 Azure-SSIS IR 屬於同時也包含內部部署 SQL Server 的虛擬網路。  如需詳細資訊，請參閱[將 Azure-SSIS Integration Runtime 加入虛擬網路](https://docs.microsoft.com/azure/data-factory/join-azure-ssis-integration-runtime-virtual-network)。 然後，如本文所述，使用 `catalog.set_execution_credential` 來提供認證。

## <a name="connect-to-an-on-premises-file-share"></a>連線至內部部署檔案共用
若要檢查是否可以連線至內部部署檔案共用，請執行下列動作：

1.  若要執行此測試，請尋找未加入網域的電腦。

2.  在未加入網域的電腦上，執行下列命令。 此命令會使用您要使用的網域認證開啟命令提示字元視窗，然後藉由取得目錄清單來測試與檔案共用的連線。

    ```cmd
    runas.exe /netonly /user:<domain>\<username> cmd.exe
    dir \\fileshare
    ```

3.  檢查是否會針對您要使用的內部部署檔案共用傳回目錄清單。

## <a name="connect-to-a-file-share-on-an-azure-vm"></a>連線至 Azure VM 上的檔案共用
若要連線到 Azure 虛擬機器上的檔案共用，請執行下列動作：

1.  使用 SQL Server Management Studio (SSMS) 或其他工具，連線至裝載 SSIS 目錄資料庫 (SSISDB) 的 SQL Database。

2.  使用 SSISDB 作為目前的資料庫，開啟查詢視窗。

3.  執行 `catalog.set_execution_credential` 預存程序，如下列選項中所述：

    ```sql
    catalog.set_execution_credential @domain = N'.', @user = N'username of local account on Azure virtual machine', @password = N'password'
    ```

## <a name="connect-to-a-file-share-in-azure-files"></a>連線至 Azure 檔案中的檔案共用
如需 Azure 檔案的詳細資訊，請參閱 [Azure 檔案](https://azure.microsoft.com/services/storage/files/)。

若要連線至 Azure 檔案中的檔案共用，請執行下列動作：

1.  使用 SQL Server Management Studio (SSMS) 或其他工具，連線至裝載 SSIS 目錄資料庫 (SSISDB) 的 SQL Database。

2.  使用 SSISDB 作為目前的資料庫，開啟查詢視窗。

3.  執行 `catalog.set_execution_credential` 預存程序，如下列選項中所述：

    ```sql
    catalog.set_execution_credential @domain = N'Azure', @user = N'<storage-account-name>', @password = N'<storage-account-key>'
    ```

## <a name="next-steps"></a>後續步驟
- 部署套件。 如需詳細資訊，請參閱[使用 SQL Server Management Studio (SSMS) 部署 SSIS 專案](../ssis-quickstart-deploy-ssms.md)。
- 執行套件。 如需詳細資訊，請參閱[使用 SQL Server Management Studio (SSMS) 執行 SSIS 套件](../ssis-quickstart-run-ssms.md)。
- 排程套件。 如需詳細資訊，請參閱[在 Azure 中排程 SSIS 套件](ssis-azure-schedule-packages.md)。