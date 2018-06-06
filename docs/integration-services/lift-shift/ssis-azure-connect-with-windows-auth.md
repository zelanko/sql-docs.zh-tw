---
title: 使用 Windows 驗證連線至資料來源和檔案共用 | Microsoft Docs
ms.date: 02/05/2018
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.component: lift-shift
ms.suite: sql
ms.custom: ''
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0a0f1b6936644f2cae9cee469cb763696786a628
ms.sourcegitcommit: 0cc2cb281e467a13a76174e0d9afbdcf4ccddc29
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/15/2018
---
# <a name="connect-to-on-premises-data-sources-and-azure-file-shares-with-windows-authentication-in-ssis"></a>在 SSIS 中使用 Windows 驗證來連線至內部部署資料來源和 Azure 檔案共用
本文描述如何在 Azure SQL Database 上設定 SSIS 目錄以執行套件，這些套件會使用 Windows 驗證來連線至內部部署資料來源和 Azure 檔案共用。 無論是在內部部署和 Azure 虛擬機器上及 Azure 檔案中，您都可以使用 Windows 驗證來連線至與 Azure SSIS Integration Runtime 相同虛擬網路中的資料來源。

> [!WARNING]
> 如果您未如本文所述執行 `catalog`.`set_execution_credential` 為 Windows 驗證提供有效的網域認證，則相依於 Windows 驗證的套件就無法連線到資料來源，而且會在執行階段失敗。

## <a name="you-can-only-use-one-set-of-credentials"></a>您只能使用一組認證

目前，一個套件只能使用一組認證。 遵循本文步驟將所提供的網域認證套用於 SQL Database 執行個體上的所有套件執行 (互動或排程)，直到您變更或移除這些認證為止。 如果您的套件使用不同組認證連線到多個資料來源，您可能必須將套件分成多個套件。

如果您的其中一個資料來源是 Azure 檔案服務，您可於套件執行階段時使用 `net use` (或執行處理工作中的對等項目) 掛接 Azure 檔案共用，來解決這項限制。 如需詳細資訊，請參閱[掛接 Azure 檔案共用並在 Windows 中存取共用](https://docs.microsoft.com/azure/storage/files/storage-how-to-use-files-windows)。

## <a name="provide-domain-credentials-for-windows-authentication"></a>提供 Windows 驗證的網域認證
若要提供網域認證，讓套件使用 Windows 驗證以連線至內部部署資料來源，請執行下列動作：

1.  使用 SQL Server Management Studio (SSMS) 或其他工具，連線至裝載 SSIS 目錄資料庫 (SSISDB) 的 SQL Database。 如需詳細資訊，請參閱[連線至 Azure 上的 SSISDB 目錄資料庫](ssis-azure-connect-to-catalog-database.md)。

2.  使用 SSISDB 作為目前的資料庫，開啟查詢視窗。

3.  執行下列預存程序，並提供適當的網域認證：

    ```sql
    catalog.set_execution_credential @user='<your user name>', @domain='<your domain name>', @password='<your password>'
    ```

4.  執行 SSIS 套件。 套件會使用您提供的認證，透過 Windows 驗證連線至內部部署資料來源。

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

1.  若要執行這項測試，請尋找未加入網域的電腦。

2.  在未加入網域的電腦上，執行下列命令，以您想要使用的網域認證啟動 SQL Server Management Studio (SSMS)：

    ```cmd
    runas.exe /netonly /user:<domain>\<username> SSMS.exe
    ```

3.  從 SSMS 中，檢查是否可以連線至您想要使用的內部部署 SQL Server。

### <a name="prerequisites"></a>Prerequisites
若要從 Azure 上執行的套件連線到內部部署 SQL Server，您必須啟用下列必要條件：

1.  在 SQL Server 組態管理員中，啟用 TCP/IP 通訊協定。
2.  允許通過 Windows 防火牆進行存取。 如需詳細資訊，請參閱[設定 Windows 防火牆以允許 SQL Server 存取](https://docs.microsoft.com/sql/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access)。
3.  若要使用 Windows 驗證進行連線，請確定 Azure-SSIS Integration Runtime 屬於同時也包含內部部署 SQL Server 的虛擬網路 (VNet)。  如需詳細資訊，請參閱[將 Azure-SSIS Integration Runtime 加入虛擬網路](https://docs.microsoft.com/azure/data-factory/join-azure-ssis-integration-runtime-virtual-network)。 然後，如本文所述，使用 `catalog.set_execution_credential` 來提供認證。

## <a name="connect-to-an-on-premises-file-share"></a>連線至內部部署檔案共用
若要檢查是否可以連線至內部部署檔案共用，請執行下列動作：

1.  若要執行這項測試，請尋找未加入網域的電腦。

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

若要連線至 Azure 檔案共用上的檔案共用，請執行下列動作：

1.  使用 SQL Server Management Studio (SSMS) 或其他工具，連線至裝載 SSIS 目錄資料庫 (SSISDB) 的 SQL Database。

2.  使用 SSISDB 作為目前的資料庫，開啟查詢視窗。

3.  執行 `catalog.set_execution_credential` 預存程序，如下列選項中所述：

    ```sql
    catalog.set_execution_credential @domain = N'Azure', @user = N'<storage-account-name>', @password = N'<storage-account-key>'
    ```

## <a name="next-steps"></a>後續步驟
- 部署套件。 如需詳細資訊，請參閱[使用 SQL Server Management Studio (SSMS) 部署 SSIS 專案](../ssis-quickstart-deploy-ssms.md)。
- 執行套件。 如需詳細資訊，請參閱[使用 SQL Server Management Studio (SSMS) 執行 SSIS 套件](../ssis-quickstart-run-ssms.md)。
- 排程套件。 如需詳細資訊，請參閱[排程 Azure 上的 SSIS 套件執行](ssis-azure-schedule-packages.md)。
