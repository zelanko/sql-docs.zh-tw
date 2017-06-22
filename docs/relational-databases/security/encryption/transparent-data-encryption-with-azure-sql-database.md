---
title: "Azure SQL Database 的透明資料加密 | Microsoft 文件"
ms.custom:
- SQL2016_New_Updated
- MSDN content
- MSDN - SQL DB
ms.date: 09/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.service: sql-database
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- TDE, SQL Database
- encryption (SQL Database), TDE
- Transparent Data Encryption, SQL Database
ms.assetid: 0bf7e8ff-1416-4923-9c4c-49341e208c62
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1c607015f1ead5b19d4c32c5bac62eb624b0578b
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="transparent-data-encryption-with-azure-sql-database"></a>Azure SQL Database 的透明資料加密
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx_md](../../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

  [!INCLUDE[ssSDSFull](../../../includes/sssdsfull-md.md)] 透明資料加密可即時執行資料庫、相關聯備份及交易記錄檔的即時加密與解密，完全無須變更應用程式，就能協助防範惡意活動所帶來的威脅。  
  
 TDE 會使用稱為資料庫加密金鑰的對稱金鑰，將整個資料庫的儲存體加密。 在 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] 中，資料庫加密金鑰由內建的伺服器憑證保護。 每部 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] 伺服器各有其專用的內建伺服器憑證。 若資料庫具有 GeoDR 關聯性，則由每部伺服器上不同的金鑰保護。 如有 2 個資料庫同時連線到同一部伺服器，則這兩個資料庫會共用同一個內建憑證。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 會每隔 90 天自動輪換這些憑證。 如需 TDE 的一般說明，請參閱 [透明資料加密 &#40;TDE&#41;](../../../relational-databases/security/encryption/transparent-data-encryption-tde.md)。  
  
 [!INCLUDE[ssSDSFull](../../../includes/sssdsfull-md.md)] 不支援 Azure 金鑰保存庫與 TDE 整合。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 可以使用金鑰保存庫中的非對稱金鑰。 如需詳細資訊，請參閱 [使用 Azure 金鑰保存庫進行可延伸金鑰管理 &#40;SQL Server&#41;](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)處理金鑰管理 (包括加密金鑰階層和金鑰備份)。  
  
##  <a name="Permissions"></a> Permissions  
 若要透過 Azure 入口網站利用 REST API 或 PowerShell 設定 TDE，您必須以 Azure 擁有者、參與者或 SQL 安全性管理員的身分連線。  
  
 若要設定使用 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 設定 TDE，必須符合下列需求：  
  
-   若要執行 ALTER DATABASE 陳述式與 SET 選項，需要具備 **dbmanager** 角色的成員資格。  
  
##  <a name="Preview"></a> 使用入口網站在資料庫上啟用 TDE  
  
1.  請前往 Azure 入口網站 (網址是 [https://portal.azure.com](https://portal.azure.com) )，並使用您的 Azure 系統管理員或參與者帳戶登入。  
  
2.  在左邊的橫幅中，按一下 [瀏覽] ，再按一下 [SQL 資料庫] 。  
  
3.  在左窗格中選取 [SQL 資料庫]  ，然後按一下您的使用者資料庫。  
  
4.  在資料庫刀鋒視窗中，按一下 [所有設定] 。  
  
5.  在 [設定]  刀鋒視窗中，按一下 [透明資料加密]  部分，以開啟 [透明資料加密]  刀鋒視窗。  
  
6.  在 [資料加密] 刀鋒視窗中，將 [資料加密] 按鈕移至 [開啟]，然後按一下 [儲存] (位於頁面頂端)，以套用此設定。 [加密狀態]  會顯示透明資料加密的概略進度。  
  
     ![SQL 資料庫 TDE 開始加密](../../../relational-databases/security/encryption/media/sqldb-tde-encrypt.png "SQL 資料庫 TDE 開始加密")  
  
     您也可以使用查詢工具 (例如 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] )，以具有 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] VIEW DATABASE STATE **權限的資料庫使用者身分，連接到** 監視加密進度。 查詢 **sys.dm_database_encryption_keys** 檢視的 [encryption_state](../../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md) 資料行。  
  
##  <a name="Encrypt"></a> 使用 TRANSACT-SQL 啟用 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] 的 TDE  
 下列步驟會啟用 TDE。  
  
###  <a name="TsqlProcedure"></a>  
  
1.  使用 master 資料庫中之 **dbmanager** 角色的系統管理員或成員身分的登入，連接到資料庫。  
  
2.  執行下列陳述式，以加密資料庫。  
  
    ```  
    -- Enable encryption  
    ALTER DATABASE [AdventureWorks] SET ENCRYPTION ON;  
    GO  
    ```  
  
3.  若要監視 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]的加密進度，具有 **VIEW DATABASE STATE** 權限的資料庫使用者可以查詢 **sys.dm_database_encryption_keys** 檢視的 [encryption_state](../../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md) 資料行。  
  
##  <a name="EncryptPS"></a> 使用 PowerShell 在 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] 上啟用和停用 TDE  
 您可以使用 Azure PowerShell，執行下列命令開啟/關閉 TDE。 您必須先將帳戶連接到 PS 視窗，才能執行命令。 自訂範例以使用 `ServerName`、 `ResourceGroupName`和 `DatabaseName` 參數的值。 如需 PowerShell 的其他相關資訊，請參閱 [如何安裝及設定 Azure PowerShell](http://azure.microsoft.com/documentation/articles/powershell-install-configure/)。  
  
> [!NOTE]  
>  若要繼續，您應該安裝和設定 Azure PowerShell 1.0 版。 0.9.8 版雖可使用但已被取代，而且它需要使用 `PS C:\> Switch-AzureMode -Name AzureResourceManager` 命令切換至 AzureResourceManager Cmdlet。  
  
###  <a name="PSlProcedure"></a>  
  
1.  啟用 TDE、傳回 TDE 狀態及檢視加密活動：  
  
    ```  
    PS C:\> Set-AzureRMSqlDatabaseTransparentDataEncryption -ServerName "myserver" -ResourceGroupName "Default-SQL-WestUS" -DatabaseName "database1" -State "Enabled"  
  
    PS C:\> Get-AzureRMSqlDatabaseTransparentDataEncryption -ServerName "myserver" -ResourceGroupName "Default-SQL-WestUS" -DatabaseName "database1"  
  
    PS C:\> Get-AzureRMSqlDatabaseTransparentDataEncryptionActivity -ServerName "myserver" -ResourceGroupName "Default-SQL-WestUS" -DatabaseName "database1"  
    ```  
  
     如果使用 0.9.8 版，請使用 Set-AzureSqlDatabaseTransparentDataEncryption、Get-AzureSqlDatabaseTransparentDataEncryption 和 Get-AzureSqlDatabaseTransparentDataEncryptionActivity 命令。  
  
2.  若要停用 TDE：  
  
    ```  
    PS C:\> Set-AzureRMSqlDatabaseTransparentDataEncryption -ServerName "myserver" -ResourceGroupName "Default-SQL-WestUS" -DatabaseName "database1" -State "Disabled"  
  
    ```  
  
     如果使用 0.9.8 版，請使用 Set AzureSqlDatabaseTransparentDataEncryption 命令。  
  
##  <a name="Decrypt"></a> 解密 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]  
  
#### <a name="to-disable-tde-by-using-the-azure-portal"></a>使用 Azure 入口網站停用 TDE  
  
1.  請前往 Azure 入口網站 (網址是 [https://portal.azure.com](https://portal.azure.com) )，並使用您的 Azure 系統管理員或參與者帳戶登入。  
  
2.  在左邊的橫幅中，按一下 [瀏覽] ，再按一下 [SQL 資料庫] 。  
  
3.  在左窗格中選取 [SQL 資料庫]  ，然後按一下您的使用者資料庫。  
  
4.  在資料庫刀鋒視窗中，按一下 [所有設定] 。  
  
5.  在 [設定]  刀鋒視窗中，按一下 [透明資料加密]  部分，以開啟 [透明資料加密]  刀鋒視窗。  
  
6.  在 [透明資料加密] 刀鋒視窗中，將 [資料加密] 按鈕移至 [關閉]，然後按一下 [儲存] (位於頁面頂端)，以套用此設定。 [加密狀態]  會顯示透明資料解密的概略進度。  
  
     您也可以使用查詢工具 (例如 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] )，以具有 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] VIEW DATABASE STATE **權限的資料庫使用者身分，連接到** 監視解密進度。 查詢 **sys.dm_database_encryption_keys** 檢視的 [encryption_state](../../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md) 資料行。  
  
#### <a name="to-disable-tde-by-using-transact-sql"></a>使用 TRANSACT-SQL 停用 TDE  
  
1.  使用 master 資料庫中之 **dbmanager** 角色的系統管理員或成員身分的登入，連接到資料庫。  
  
2.  執行下列陳述式，以解密資料庫。  
  
    ```  
    -- Enable encryption  
    ALTER DATABASE [AdventureWorks] SET ENCRYPTION OFF;  
    GO  
    ```  
  
3.  若要監視 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]的加密進度，具有 **VIEW DATABASE STATE** 權限的資料庫使用者可以查詢 **sys.dm_database_encryption_keys** 檢視的 [encryption_state](../../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md) 資料行。  
  
##  <a name="Working"></a> 移動 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]  
 您無須解密資料庫，即可在 Azure 執行作業。 目標會自動繼承來源資料庫或主要資料庫的 TDE 設定。 這包括下列作業：  
  
-   異地複原  
  
-   自助時間點還原  
  
-   還原已刪除的資料庫  
  
-   使用中的異地複寫  
  
-   建立資料庫複本  
  
 在 [!INCLUDE[ssSDSFull](../../../includes/sssdsfull-md.md)] 入口網站中使用 [匯出資料庫] 功能或使用 [ [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 匯入和匯出精靈] 匯出受 TDE 保護的資料庫時，資料庫的匯出內容不會加密。 此匯出內容會儲存在未加密的 .bacpac 檔案中。 請務必為 .bacpac 檔案施以適當的保護措施，並在匯入新資料庫作業完成時，立即啟用 TDE。 
 
 例如，如果從內部部署 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]匯出 .bacpac 檔案，則新資料庫的匯入內容不會自動加密。 同樣地，如果從 [!INCLUDE[ssSDSFull](../../../includes/sssdsfull-md.md)] 匯出 .bacpac 檔案至內部部署 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，新資料庫也不會自動加密。  
 
 唯一的例外的是在匯出至 [!INCLUDE[ssSDSFull](../../../includes/sssdsfull-md.md)] 及從中匯出時 - TDE 會在新的資料庫中啟用，但 .bacpac 檔案本身仍不會加密。
  
## <a name="related-sql-server-topic"></a>相關的 SQL Server 主題  
 [使用 EKM 在 SQL Server 上啟用 TDE](../../../relational-databases/security/encryption/enable-tde-on-sql-server-using-ekm.md)  
  
## <a name="see-also"></a>另請參閱  
 [透明資料加密 &#40;TDE&#41;](../../../relational-databases/security/encryption/transparent-data-encryption-tde.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-credential-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-database-transact-sql.md)  
  
  

