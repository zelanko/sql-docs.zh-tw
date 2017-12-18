---
title: "使用 Windows 驗證連線至內部部署資料來源和 Azure 檔案共用 | Microsoft Docs"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: lift-shift
ms.suite: sql
ms.custom: 
ms.technology: integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9235ffd3225e76ee94067519c72e997c451d9893
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="connect-to-on-premises-data-sources-and-azure-file-shares-with-windows-authentication"></a>使用 Windows 驗證連線至內部部署資料來源和 Azure 檔案共用
本文描述如何在 Azure SQL Database 上設定 SSIS 目錄以執行套件，這些套件會使用 Windows 驗證來連線至內部部署資料來源和 Azure 檔案共用。

遵循本文步驟所提供的網域認證適用於 SQL Database 執行個體上的所有套件執行，直到您變更或移除這些認證為止。

## <a name="connect-to-on-premises-data-sources"></a>連線至內部部署資料來源

### <a name="prerequisite"></a>必要條件
在設定 Windows 驗證的網域認證之前，請檢查未加入網域的電腦是否可以在 `runas` 模式下連線至內部部署資料來源。

#### <a name="connecting-to-sql-server"></a>連線到 SQL Server
若要檢查是否可以連線至內部部署 SQL Server，請執行下列動作：

1.  若要執行這項測試，請尋找未加入網域的電腦。

2.  在未加入網域的電腦上，執行下列命令，以您想要使用的網域認證啟動 SQL Server Management Studio (SSMS)：

    ```cmd
    runas.exe /netonly /user:<domain>\<username> SSMS.exe
    ```

3.  從 SSMS 中，檢查是否可以連線至您想要使用的內部部署 SQL Server。

#### <a name="connecting-to-a-file-share"></a>連線至檔案共用
若要檢查是否可以連線至內部部署檔案共用，請執行下列動作：

1.  若要執行這項測試，請尋找未加入網域的電腦。

2.  在未加入網域的電腦上，執行下列命令。 此命令會使用您要使用的網域認證開啟命令提示字元視窗，然後藉由取得目錄清單來測試與檔案共用的連線。

    ```cmd
    runas.exe /netonly /user:<domain>\<username> cmd.exe
    dir \\fileshare
    ```

3.  檢查是否會針對您要使用的內部部署檔案共用傳回目錄清單。

### <a name="provide-domain-credentials"></a>提供網域認證
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

## <a name="connect-to-file-shares"></a>連線至檔案共用
您可以使用 Windows 驗證來連線至與 Azure SSIS Integration Runtime 相同之虛擬網路中的檔案共用 (無論是在內部部署和 Azure 虛擬機器上還是 Azure 檔案中)。 如需 Azure 檔案的詳細資訊，請參閱 [Azure 檔案](https://azure.microsoft.com/services/storage/files/)。

若要連線至 Azure 虛擬機器上的檔案共用或 Azure 檔案共用，請執行下列動作：

1.  使用 SQL Server Management Studio (SSMS) 或其他工具，連線至裝載 SSIS 目錄資料庫 (SSISDB) 的 SQL Database。

2.  使用 SSISDB 作為目前的資料庫，開啟查詢視窗。

3.  執行 `catalog.set_execution_credential` 預存程序，如下列選項中所述：

    a.  若要連線至 Azure 虛擬機器上的檔案共用，請執行下列預存程序：

    ```sql
    catalog.set_execution_credential @domain = N'.', @user = N'username of local account on Azure virtual machine', @password = N'password'
    ```

    b.  若要連線至 Azure 檔案共用 (也就是在 Azure 檔案中)，請執行下列預存程序：

    ```sql
    catalog.set_execution_credential @domain = N'Azure', @user = N'<storage-account-name>', @password = N'<storage-account-key>'
    ```

## <a name="next-steps"></a>後續的步驟
- 部署套件。 如需詳細資訊，請參閱[使用 SQL Server Management Studio (SSMS) 部署 SSIS 專案](../ssis-quickstart-deploy-ssms.md)。
- 執行套件。 如需詳細資訊，請參閱[使用 SQL Server Management Studio (SSMS) 執行 SSIS 套件](../ssis-quickstart-run-ssms.md)。
- 排程套件。 如需詳細資訊，請參閱[排程 Azure 上的 SSIS 套件執行](ssis-azure-schedule-packages.md)。
