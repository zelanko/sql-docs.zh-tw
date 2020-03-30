---
title: Enable Stretch Database for a database
ms.date: 08/05/2016
ms.service: sql-server-stretch-database
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Stretch Database, enabling database
- enabling database for Stretch Database
ms.assetid: 37854256-8c99-4566-a552-432e3ea7c6da
author: rothja
ms.author: jroth
ms.custom: seo-dt-2019
ms.openlocfilehash: db08d84dd1619d8c9e2e4d8e796abdd0c9d202fc
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "73844594"
---
# <a name="enable-stretch-database-for-a-database"></a>Enable Stretch Database for a database
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]


  若要設定現有的資料庫以使用 Stretch Database，請在 SQL Server Management Studio 中為資料庫選取 [工作 | 延展 | 啟用]  ，開啟 [啟用資料庫的延展功能精靈]  。 您也可以使用 Transact-SQL 來為資料庫啟用 Stretch Database。  
  
 如果您為個別資料表選取 [工作 | 延展 | 啟用]  ，而您尚未針對 Stretch Database 啟用資料庫，精靈會針對 Stretch Database 設定資料庫，並且在程序中讓您選取資料表。 請遵循本文中的步驟，而非[為資料表啟用 Stretch Database](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md) 中的步驟。  
  
 在資料庫或資料表上啟用 Stretch Database 需要 db_owner 權限。 在資料庫或資料表上啟用 Stretch Database 也需要 CONTROL DATABASE 權限。  

> [!NOTE]
> 稍後，如果您停用 Stretch Database，請記住針對資料表或資料庫停用 Stretch Database，並不會刪除遠端物件。 若您想要刪除遠端資料表或遠端資料庫，則必須使用 Azure 管理入口網站將其卸除。 遠端物件會繼續產生 Azure 成本，直到您手動將其刪除為止。 
 
## <a name="before-you-get-started"></a>開始之前  
  
-   在您設定資料庫以進行「延展」之前，我們建議您先執行 Stretch Database Advisor 以識別符合延展資格的資料庫及資料表。 Stretch Database Advisor 也能識別封鎖問題。 如需詳細資訊，請參閱 [執行 Stretch Database Advisor 以識別 Stretch Database 的資料庫和資料表](../../sql-server/stretch-database/stretch-database-databases-and-tables-stretch-database-advisor.md)。  
  
-   檢閱 [Stretch Database 的限制](../../sql-server/stretch-database/limitations-for-stretch-database.md)。  
  
-   Stretch Database 會將資料移轉至 Azure。 因此，您必須擁有 Azure 帳戶和計費用的訂閱。 若要取得 Azure 帳戶，請 [按一下這裡](https://azure.microsoft.com/pricing/free-trial/)。  
  
-   擁有建立新的 Azure 伺服器或選取現有的 Azure 伺服器所需的連線和登入資訊。  
  
##  <a name="prerequisite-enable-stretch-database-on-the-server"></a><a name="EnableTSQLServer"></a> 必要條件：在伺服器上啟用 Stretch Database  
 在您於資料庫或資料表上啟用 Stretch Database 前，您必須在本機伺服器上啟用它。 這項作業需要 sysadmin 或 serveradmin 權限。  
  
-   如果您已經有必要的系統管理權限，則 [啟用資料庫的延展功能精靈]  會設定伺服器以使用「延展」。  
  
-   如果您沒有必要的權限，系統管理員必須在您執行精靈前，執行 **sp_configure** 來手動啟用選項，否則系統管理員必須執行精靈。  
  
 若要以手動方式在伺服器上啟用 Stretch Database，請執行 **sp_configure** 並開啟 [遠端資料封存]  選項。 下列範例會將 **remote data archive** 選項的值設為 1 來啟用它。  
  
```sql
EXEC sp_configure 'remote data archive' , '1';  
GO

RECONFIGURE;  
GO  
```  
  
 如需詳細資訊，請參閱[設定遠端資料封存伺服器組態選項](../../database-engine/configure-windows/configure-the-remote-data-archive-server-configuration-option.md)和 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)。  
  
##  <a name="use-the-wizard-to-enable-stretch-database-on-a-database"></a><a name="Wizard"></a> 使用精靈在資料庫上啟用 Stretch Database  
 如需 [啟用資料庫的延展功能精靈] 的相關資訊，包括您必須輸入的資訊及必須決定的選擇，請參閱 [開始執行啟用資料庫的延展功能精靈](../../sql-server/stretch-database/get-started-by-running-the-enable-database-for-stretch-wizard.md)。  
  
##  <a name="use-transact-sql-to-enable-stretch-database-on-a-database"></a><a name="EnableTSQLDatabase"></a> 使用 Transact-SQL 在資料庫上啟用 Stretch Database  
 在您於個別資料表上啟用 Stretch Database 前，您必須在資料庫上啟用它。  
  
 在資料庫或資料表上啟用 Stretch Database 需要 db_owner 權限。 在資料庫或資料表上啟用 Stretch Database 也需要 CONTROL DATABASE 權限。  
  
1.  開始之前，請為 Stretch Database 要移轉的資料選擇現有的 Azure 伺服器，或建立新的 Azure 伺服器。  
  
2.  在 Azure 伺服器上，利用 SQL Server 的 IP 位址範圍，來建立能讓 SQL Server 與遠端伺服器通訊的防火牆規則。  

    您可以透過嘗試從 SQL Server Management Studio (SSMS) 中的物件總管連接到 Azure 伺服器，輕鬆地找到您需要的值並建立防火牆規則。 SSMS 可協助您開啟下列對話方塊來建立規則，該對話方塊中已包含必要的 IP 位址值。
    
    ![Stretch 的防火牆規則](../../sql-server/stretch-database/media/firewall-rule-for-stretch.png)
  
3.  若要設定 SQL Server 資料庫以使用 Stretch Database ，該資料庫必須要有資料庫主要金鑰。 資料庫主要金鑰會保護 Stretch Database 用來連接遠端資料庫的認證。 以下範例會建立新的資料庫主要金鑰。  
  
    ```sql  
    USE <database>; 
    GO  
  
    CREATE MASTER KEY ENCRYPTION BY PASSWORD='<password>'; 
    GO
    ```  
    如需資料庫主要金鑰的詳細資訊，請參閱 [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md) 和[建立資料庫主要金鑰](../../relational-databases/security/encryption/create-a-database-master-key.md)。
    
4.  當您設定資料庫以使用 Stretch Database 時，您必須提供 Stretch Database 可使用的認證，以在內部部署 SQL Server 和遠端 Azure 伺服器之間通訊。 您有兩個選項。  
  
    -   您可以提供系統管理員認證。  
  
        -   如果您透過執行精靈來啟用 Stretch Database，您可以在當時建立認證。  
  
        -   如果您想要透過執行 **ALTER DATABASE**來啟用 Stretch Database，您必須先手動建立認證，再執行 **ALTER DATABASE** 以啟用 Stretch Database。 
        
        以下範例會建立新的認證。
  
        ```sql  
        CREATE DATABASE SCOPED CREDENTIAL <db_scoped_credential_name>  
            WITH IDENTITY = '<identity>' , SECRET = '<secret>' ;
        GO   
        ```  

         如需認證的詳細資訊，請參閱 [CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)。 建立認證需要 ALTER ANY CREDENTIAL 權限。  

    -   當下列條件成立時，您可以使用 SQL Server 的同盟服務帳戶來與遠端 Azure 伺服器通訊。  
  
        -   正在執行之 SQL Server 執行個體下的服務帳戶是網域帳戶。  
  
        -   網域帳戶所屬的網域，其 Active Directory 與 Azure Active Directory 同盟。  
  
        -   遠端 Azure 伺服器已設定支援 Azure Active Directory 驗證。  
  
        -   正在執行之 SQL Server 執行個體下的服務帳戶必須設定為遠端 Azure 伺服器上的 dbmanager 或 sysadmin 帳戶。  
  
5.  若要設定資料庫以使用 Stretch Database，請執行 ALTER DATABASE 命令。  
  
    1.  針對 SERVER 引數，提供現有 Azure 伺服器的名稱，包含名稱的 `.database.windows.net` 部分 - 例如， `MyStretchDatabaseServer.database.windows.net`。  
  
    2.  以 CREDENTIAL 引數提供現有的系統管理員認證，或指定 FEDERATED_SERVICE_ACCOUNT = ON。 下列範例提供現有的認證。  
  
    ```sql  
    ALTER DATABASE <database name>  
        SET REMOTE_DATA_ARCHIVE = ON  
            (  
                SERVER = '<server_name>' ,  
                CREDENTIAL = <db_scoped_credential_name>  
            ) ;  
    GO
    ```  
  
## <a name="next-steps"></a>後續步驟  
-   [Enable Stretch Database for a table](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md) 以啟用額外資料表。  
  
-   [監視和疑難排解資料移轉 &#40;Stretch Database&#41;](../../sql-server/stretch-database/monitor-and-troubleshoot-data-migration-stretch-database.md) 以查看資料移轉狀態。  
  
-   [暫停和繼續資料移轉 &#40;Stretch Database&#41;](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md)  
  
-   [管理 Stretch Database 並對其進行疑難排解](../../sql-server/stretch-database/manage-and-troubleshoot-stretch-database.md)  
  
-   [備份已啟用 Stretch 的資料庫](../../sql-server/stretch-database/backup-stretch-enabled-databases-stretch-database.md)  
  
-   [還原已啟用 Stretch 的資料庫](../../sql-server/stretch-database/restore-stretch-enabled-databases-stretch-database.md)  
  
## <a name="see-also"></a>另請參閱  
 [執行 Stretch Database Advisor 以識別 Stretch Database 的資料庫和資料表](../../sql-server/stretch-database/stretch-database-databases-and-tables-stretch-database-advisor.md)   
 [ALTER DATABASE SET 選項 &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)  
  
  
