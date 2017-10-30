---
title: "連接至內部部署資料來源使用 Windows 驗證 |Microsoft 文件"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-server-2017
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1e3d9736612211038991489a4bd858d1ff89d333
ms.openlocfilehash: 1b60d877c6c75a77dd16fa8cb1704e10baf36bdb
ms.contentlocale: zh-tw
ms.lasthandoff: 10/19/2017

---
# <a name="connect-to-on-premises-data-sources-with-windows-authentication"></a>連接至內部部署資料來源使用 Windows 驗證
本文說明如何在 Azure SQL Database 執行使用 Windows 驗證來連接至內部部署資料來源的封裝上設定 SSIS 目錄。

當您遵循本文章中的步驟，您提供的網域認證適用於 SQL Database 執行個體上的所有封裝執行直到您變更或移除的認證。

## <a name="prerequisite"></a>必要條件
您設定 Windows 驗證的網域認證之前，請檢查是否未加入網域的電腦可以連線到內部部署資料來源中`runas`模式。

### <a name="connecting-to-sql-server"></a>連接到 SQL Server
若要檢查是否能連接到內部部署 SQL Server，執行下列動作：

1.  若要執行這項測試，尋找未加入網域的電腦。

2.  未加入網域的電腦上，執行下列命令以啟動 SQL Server Management Studio (SSMS) 您想要使用的網域認證：

    ```cmd
    runas.exe /netonly /user:<domain>\<username> SSMS.exe
    ```

3.  從 SSMS 中檢查是否能連接到您想要使用內部部署 SQL Server。

### <a name="connecting-to-a-file-share"></a>連線到檔案共用
若要檢查是否可以連線到內部檔案共用，執行下列動作：

1.  若要執行這項測試，尋找未加入網域的電腦。

2.  未加入網域的電腦上，執行下列命令。 此命令會開啟您要使用的網域認證，然後測試能連接到檔案共用與命令 prommpt，藉由取得目錄清單。

    ```cmd
    runas.exe /netonly /user:<domain>\<username> cmd.exe
    dir \\fileshare
    ```

3.  檢查是否要傳回的目錄清單的內部檔案您想要使用的共用。

## <a name="provide-domain-credentials"></a>提供網域認證
若要提供網域認證，可讓使用 Windows 驗證來連接至內部部署資料來源的封裝，執行下列動作：

1.  SQL Server Management Studio (SSMS) 或其他工具，連接到 SQL 資料庫裝載 SSIS 目錄資料庫 (SSISDB)。 如需詳細資訊，請參閱[連接到 Azure 上的 SSISDB 目錄資料庫](ssis-azure-connect-to-catalog-database.md)。

2.  使用 SSISDB 為目前的資料庫，開啟查詢視窗。

3.  執行下列預存程序，並提供適當的網域認證：

    ```sql
    catalog.set_execution_credential @user='<your user name>', @domain='<your domain name>', @password='<your password>'
    ```
4.  執行 SSIS 封裝。 封裝使用您提供給連接至內部部署資料來源使用 Windows 驗證的認證。

## <a name="view-domain-credentials"></a>檢視網域認證
若要檢視作用中的網域認證，執行下列動作：

1.  SQL Server Management Studio (SSMS) 或其他工具，連接到 SQL 資料庫裝載 SSIS 目錄資料庫 (SSISDB)。

2.  使用 SSISDB 為目前的資料庫，開啟查詢視窗。

3.  執行下列預存程序，並檢查輸出：

    ```sql
    SELECT * 
    FROM catalog.master_properties
    WHERE property_name = 'EXECUTION_DOMAIN' OR property_name = 'EXECUTION_USER'
    ```

## <a name="clear-domain-credentials"></a>清除的網域認證
若要清除並移除您所提供的這篇文章中所述的認證，請執行下列動作：

1.  SQL Server Management Studio (SSMS) 或其他工具，連接到 SQL 資料庫裝載 SSIS 目錄資料庫 (SSISDB)。

2.  使用 SSISDB 為目前的資料庫，開啟查詢視窗。

3.  執行下列預存程序：

    ```sql
    catalog.set_execution_credential @user='', @domain='', @password=''
    ```

## <a name="connect-to-file-shares"></a>連線到檔案共用
您可以使用 Windows 驗證來連接到相同 Azure SSIS 整合執行階段在內部部署及 Azure 虛擬機器上的虛擬網路中的檔案共用。

若要連接至 Azure 的虛擬機器上的檔案共用，執行下列動作：

1.  SQL Server Management Studio (SSMS) 或其他工具，連接到 SQL 資料庫裝載 SSIS 目錄資料庫 (SSISDB)。

2.  使用 SSISDB 為目前的資料庫，開啟查詢視窗。

3.  執行下列預存程序：

    ```sql
    catalog.set_execution_credential @domain = N'.', @user = N'username of local account on Azure virtual machine', @password = N'password'
    ```

## <a name="next-steps"></a>後續的步驟
- 部署封裝。 如需詳細資訊，請參閱[SSIS 專案部署與 SQL Server Management Studio (SSMS)](../ssis-quickstart-deploy-ssms.md)。
- 執行封裝。 如需詳細資訊，請參閱[與 SQL Server Management Studio (SSMS) 執行 SSIS 封裝](../ssis-quickstart-run-ssms.md)。
- 排程的封裝。 如需詳細資訊，請參閱[排程 SSIS 封裝在 Azure 上的執行](ssis-azure-schedule-packages.md)

