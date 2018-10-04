---
title: Azure SQL Database 的透明資料加密 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- TDE, SQL Database
- Transparent Data Encryption, SQL Database
- encryption (SQL Database) TDE
ms.assetid: 0bf7e8ff-1416-4923-9c4c-49341e208c62
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 3551cf4db3ab1b84f04ba13dea414943fbb2ef44
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48049778"
---
# <a name="transparent-data-encryption-with-azure-sql-database"></a>Azure SQL Database 的透明資料加密
  [!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)] 透明資料加密 （預覽版） 可協助防範惡意活動的威脅，而不需要變更應用程式執行即時加密和解密資料庫、 相關聯的備份和待用的交易記錄檔。  
  
 TDE 會使用稱為資料庫加密金鑰的對稱金鑰，將整個資料庫的儲存體加密。 在 [!INCLUDE[ssSDS](../includes/sssds-md.md)] 中，資料庫加密金鑰由內建的伺服器憑證保護。 每部 [!INCLUDE[ssSDS](../includes/sssds-md.md)] 伺服器各有其專用的內建伺服器憑證。 若資料庫具有 GeoDR 關聯性，則由每部伺服器上不同的金鑰保護。 如有 2 個資料庫同時連線到同一部伺服器，則這兩個資料庫會共用同一個內建憑證。 [!INCLUDE[msCoName](../includes/msconame-md.md)] 會每隔 90 天自動輪換這些憑證。 如需 TDE 的一般說明，請參閱 [透明資料加密 &#40;TDE&#41;](../relational-databases/security/encryption/transparent-data-encryption.md)。  
  
 [!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)] 不支援 Azure 金鑰保存庫與 TDE 整合。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 可以使用金鑰保存庫中的非對稱金鑰。 如需詳細資訊，請參閱 <<c0> [ 範例 a: Transparent Data Encryption by 使用非對稱金鑰從 Key Vault](../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md#ExampleA)。  
  
||  
|-|  
|**適用於**: [!INCLUDE[sqldbesa](../includes/sqldbesa-md.md)] ([某些區域中的預覽](http://azure.microsoft.com/documentation/articles/sql-database-preview-whats-new/?WT.mc_id=TSQL_GetItTag))。|  
  
> [!IMPORTANT]  
>  目前是預覽功能。 我了解並同意[!INCLUDE[ssSDS](../includes/sssds-md.md)]在我的資料庫的透明資料加密預覽條款位於我的授權合約 （例如 Enterprise 合約、 Microsoft Azure 合約或 Microsoft 線上訂用帳戶協議），以及任何適用[補充使用條款的 Microsoft Azure Preview](http://azure.microsoft.com/support/legal/preview-supplemental-terms/)。  
  
 TDE 狀態預覽即使在 [!INCLUDE[ssSDS](../includes/sssds-md.md)] 版本系列 V12 已宣佈為目前處於公開可用狀態的地理區域也適用。 在 [!INCLUDE[ssSDS](../includes/sssds-md.md)] 宣佈 TDE 從預覽版升級至 GA 前， [!INCLUDE[msCoName](../includes/msconame-md.md)] 的 TDE 並不適用於生產資料庫。 如需有關 [!INCLUDE[ssSDS](../includes/sssds-md.md)] V12 的詳細資訊，請參閱 [Azure SQL Database 的新功能](http://azure.microsoft.com/documentation/articles/sql-database-preview-whats-new/)。  
  
##  <a name="Permissions"></a> 權限  
 若要註冊預覽版，並透過 Azure 入口網站利用 REST API 或 PowerShell 設定 TDE，您必須以 Azure 擁有者、參與者或 SQL 安全性管理員的身分連線。  
  
 若要設定使用 [!INCLUDE[tsql](../includes/tsql-md.md)] 設定 TDE，必須符合下列需求：  
  
-   您必須已經註冊 TDE 預覽版。  
  
-   若要建立資料庫加密金鑰，您必須是[!INCLUDE[ssSDS](../includes/sssds-md.md)]系統管理員，或是必須隸屬**dbmanager** master 中的角色資料庫，而且擁有**控制**資料庫的權限。  
  
-   若要執行 ALTER DATABASE 陳述式與 SET 選項，便只需要具備 **dbmanager** 角色的成員資格。  
  
##  <a name="Preview"></a> 註冊資料庫的 TDE，並啟用 TDE 的預覽  
  
1.  請瀏覽 Azure 入口網站，網址[ https://portal.azure.com ](https://portal.azure.com)並使用您的 Azure 系統管理員或參與者帳戶登入。  
  
2.  在左邊的橫幅中，按一下 [瀏覽] ，再按一下 [SQL 資料庫] 。  
  
3.  在左窗格中選取 [SQL 資料庫]  ，然後按一下您的使用者資料庫。  
  
4.  在資料庫刀鋒視窗中，按一下 [所有設定] 。  
  
5.  在 [設定]  刀鋒視窗中，按一下 [透明資料加密 (預覽版)]  部分，以開啟 [透明資料加密 (預覽版)]  刀鋒視窗。 若還未註冊 TDE 預覽版，資料加密設定將會停用，直到您完成註冊為止。  
  
6.  按一下 [預覽條款] 。  
  
7.  閱讀預覽條款，如果您同意這些條款，請選取**透明資料 encryptionPreview 條款**核取方塊，然後按一下**確定**靠近頁面底部。 返回**資料 encryptionPREVIEW**刀鋒視窗中，其中**資料加密**應該已啟用 按鈕。  
  
8.  在 [資料加密預覽]  刀鋒視窗中，將 [資料加密]  按鈕移至 [開啟] ，然後按一下 [儲存]  (位於頁面頂端)，以套用此設定。 [加密狀態]  會顯示透明資料加密的概略進度。  
  
     ![SQLDB_TDE_TermsNewUI](../../2014/database-engine/media/sqldb-tde-termsnewui.png "SQLDB_TDE_TermsNewUI")  
  
     您也可以使用查詢工具 (例如 [!INCLUDE[ssSDS](../includes/sssds-md.md)] )，以具有 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] VIEW DATABASE STATE **權限的資料庫使用者身分，連接到** 監視加密進度。 查詢`encryption_state`資料行[sys.dm_database_encryption_keys](/sql/relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql)檢視。  
  
##  <a name="Encrypt"></a> 使用 TRANSACT-SQL 啟用 [!INCLUDE[ssSDS](../includes/sssds-md.md)] 的 TDE  
 下列步驟中假設您已經註冊預覽版。  
  
###  <a name="TsqlProcedure"></a>  
  
1.  使用 master 資料庫中之 **dbmanager** 角色的系統管理員或成員身分的登入，連接到資料庫。  
  
2.  執行下列陳述式，以建立資料庫加密金鑰及加密資料庫。  
  
    ```  
    -- Create the database encryption key that will be used for TDE.  
    CREATE DATABASE ENCRYPTION KEY   
    WITH ALGORITHM = AES_256   
    ENCRYPTION BY SERVER CERTIFICATE ##MS_TdeCertificate##;  
  
    -- Enable encryption  
    ALTER DATABASE [AdventureWorks] SET ENCRYPTION ON;  
    GO  
    ```  
  
3.  若要監視加密進度上[!INCLUDE[ssSDS](../includes/sssds-md.md)]，資料庫使用者**VIEW DATABASE STATE**權限可以查詢`encryption_state`資料行[sys.dm_database_encryption_keys](/sql/relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql)檢視。  
  
## <a name="enabling-tde-on-sql-database-by-using-powershell"></a>使用 PowerShell 啟用 SQL Database 的 TDE  
 您可以使用 Azure PowerShell，執行下列命令開啟/關閉 TDE。 您必須將您的帳戶連接到 PS 視窗，才能執行此命令。 下列步驟中假設您已經註冊預覽版。 如需 PowerShell 的其他相關資訊，請參閱 [如何安裝及設定 Azure PowerShell](http://azure.microsoft.com/documentation/articles/powershell-install-configure/)。  
  
1.  啟用 TDE、傳回 TDE 狀態及檢視加密活動。  
  
    ```  
    PS C:\> Switch-AzureMode -Name AzureResourceManager  
  
    PS C:\> Set-AzureSqlDatabaseTransparentDataEncryption -ServerName "myserver" -ResourceGroupName "Default-SQL-WestUS" -DatabaseName "database1" -State "Enabled"  
  
    PS C:\> Get-AzureSqlDatabaseTransparentDataEncryption -ServerName "myserver" -ResourceGroupName "Default-SQL-WestUS" -DatabaseName "database1"  
  
    PS C:\> Get-AzureSqlDatabaseTransparentDataEncryptionActivity -ServerName "myserver" -ResourceGroupName "Default-SQL-WestUS" -DatabaseName "database1"  
  
    ```  
  
2.  若要停用 TDE：  
  
    ```  
    PS C:\> Set-AzureSqlDatabaseTransparentDataEncryption -ServerName "myserver" -ResourceGroupName "Default-SQL-WestUS" -DatabaseName "database1" -State "Disabled"  
  
    PS C:\> Switch-AzureMode -Name AzureServiceManagement  
    ```  
  
##  <a name="Decrypt"></a> 解密 [!INCLUDE[ssSDS](../includes/sssds-md.md)]  
  
#### <a name="to-disable-tde-by-using-the-azure-portal"></a>使用 Azure 入口網站停用 TDE  
  
1.  請瀏覽 Azure 入口網站，網址[ https://portal.azure.com ](https://portal.azure.com)並使用您的 Azure 系統管理員或參與者帳戶登入。  
  
2.  在左邊的橫幅中，按一下 [瀏覽] ，再按一下 [SQL 資料庫] 。  
  
3.  在左窗格中選取 [SQL 資料庫]  ，然後按一下您的使用者資料庫。  
  
4.  在資料庫刀鋒視窗中，按一下 [所有設定] 。  
  
5.  在 [設定]  刀鋒視窗中，按一下 [透明資料加密 (預覽版)]  部分，以開啟 [透明資料加密 (預覽版)]  刀鋒視窗。  
  
6.  在 [透明資料加密預覽]  刀鋒視窗中，將 [資料加密]  按鈕移至 [關閉] ，然後按一下 [儲存]  (位於頁面頂端)，以套用此設定。 [加密狀態]  會顯示透明資料解密的概略進度。  
  
     您也可以使用查詢工具 (例如 [!INCLUDE[ssSDS](../includes/sssds-md.md)] )，以具有 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] VIEW DATABASE STATE **權限的資料庫使用者身分，連接到** 監視解密進度。 查詢`encryption_state`資料行[sys.dm_database_encryption_keys](/sql/relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql)檢視。  
  
#### <a name="to-disable-tde-by-using-transact-sql"></a>使用 TRANSACT-SQL 停用 TDE  
  
1.  使用 master 資料庫中之 **dbmanager** 角色的系統管理員或成員身分的登入，連接到資料庫。  
  
2.  執行下列陳述式，以解密資料庫。  
  
    ```  
    -- Enable encryption  
    ALTER DATABASE [AdventureWorks] SET ENCRYPTION OFF;  
    GO  
    ```  
  
3.  若要監視加密進度上[!INCLUDE[ssSDS](../includes/sssds-md.md)]，資料庫使用者**VIEW DATABASE STATE**權限可以查詢`encryption_state`資料行[sys.dm_database_encryption_keys](/sql/relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql)檢視。  
  
##  <a name="Working"></a> 使用受 TDE 保護的資料庫上 [!INCLUDE[ssSDS](../includes/sssds-md.md)]  
 您無須解密資料庫，即可在 Azure 執行作業。 目標會自動繼承來源資料庫或主要資料庫的 TDE 設定。 這包括下列作業：  
  
-   異地複原  
  
-   自助時間點還原  
  
-   還原已刪除的資料庫  
  
-   使用中的異地複寫  
  
-   建立資料庫複本  
  
##  <a name="Moving"></a> 移動 TDE 保護的資料庫使用。Bacpac 檔案  
 在 [!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)] 入口網站使用 [匯出資料庫] 功能或 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的 [匯入和匯出精靈] 匯出受 TDE 保護的資料庫時，資料庫內容不會加密。 該內容會儲存在未加密的 .bacpac 檔案中。  請務必為 .bacpac 檔案施以適當的保護措施，並在匯入新資料庫作業完成時，立即啟用 TDE。  
  
## <a name="related-sql-server-topic"></a>相關的 SQL Server 主題  
 [使用 EKM 啟用 TDE](../relational-databases/security/encryption/enable-tde-on-sql-server-using-ekm.md)  
  
## <a name="see-also"></a>另請參閱  
 [透明資料加密 &#40;TDE&#41;](../relational-databases/security/encryption/transparent-data-encryption.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-credential-transact-sql)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-asymmetric-key-transact-sql)   
 [CREATE DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-database-encryption-key-transact-sql)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [ALTER DATABASE SET 選項 &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)  
  
  
