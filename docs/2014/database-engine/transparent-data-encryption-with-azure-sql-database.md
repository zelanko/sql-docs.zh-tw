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
ms.openlocfilehash: 541d6d27dc5dbc31dad98840e7ed6654f48a8dfc
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "78175388"
---
# <a name="transparent-data-encryption-with-azure-sql-database"></a>Azure SQL Database 的透明資料加密
  [!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)] 透明資料加密 (預覽版) 可即時執行資料庫、相關聯備份及交易檔的即時加密與解密，完全無須變更應用程式，就能協助防範惡意活動所帶來的威脅。

 TDE 會使用稱為資料庫加密金鑰的對稱金鑰來加密整個資料庫的儲存體。 在 [!INCLUDE[ssSDS](../includes/sssds-md.md)] 中，資料庫加密金鑰由內建的伺服器憑證保護。 每部 [!INCLUDE[ssSDS](../includes/sssds-md.md)] 伺服器各有其專用的內建伺服器憑證。 若資料庫具有 GeoDR 關聯性，則由每部伺服器上不同的金鑰保護。 如有 2 個資料庫同時連線到同一部伺服器，則這兩個資料庫會共用同一個內建憑證。 [!INCLUDE[msCoName](../includes/msconame-md.md)] 會每隔 90 天自動輪換這些憑證。 如需 TDE 的一般說明，請參閱 [透明資料加密 &#40;TDE&#41;](../relational-databases/security/encryption/transparent-data-encryption.md)。

 [!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)] 不支援 Azure 金鑰保存庫與 TDE 整合。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 可以使用金鑰保存庫中的非對稱金鑰。 如需詳細資訊，請參閱＜ [Example A: Transparent Data Encryption by Using an Asymmetric Key from the Key Vault](../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md#ExampleA)＞。

||
|-|
|**適用**于： [!INCLUDE[sqldbesa](../includes/sqldbesa-md.md)] （[某些區域中的預覽](https://azure.microsoft.com/documentation/articles/sql-database-preview-whats-new/?WT.mc_id=TSQL_GetItTag)）。|

> [!IMPORTANT]
>  目前是預覽功能。 我了解並同意在我的資料庫中實作 [!INCLUDE[ssSDS](../includes/sssds-md.md)] 透明資料加密必須遵守授權合約之預覽條款 (例如 Enterprise 合約、Microsoft Azure 合約或 Microsoft 線上訂用帳戶合約) 及任何適行 [Microsoft Azure Preview 增補使用條款](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)的規定。

 TDE 狀態預覽即使在 [!INCLUDE[ssSDS](../includes/sssds-md.md)] 版本系列 V12 已宣佈為目前處於公開可用狀態的地理區域也適用。 在 [!INCLUDE[ssSDS](../includes/sssds-md.md)] 宣佈 TDE 從預覽版升級至 GA 前， [!INCLUDE[msCoName](../includes/msconame-md.md)] 的 TDE 並不適用於生產資料庫。 如需有關 [!INCLUDE[ssSDS](../includes/sssds-md.md)] V12 的詳細資訊，請參閱 [Azure SQL Database 的新功能](https://azure.microsoft.com/documentation/articles/sql-database-preview-whats-new/)。

##  <a name="permissions"></a><a name="Permissions"></a> 權限
 若要註冊預覽版，並透過 Azure 入口網站利用 REST API 或 PowerShell 設定 TDE，您必須以 Azure 擁有者、參與者或 SQL 安全性管理員的身分連線。

 若要設定使用 [!INCLUDE[tsql](../includes/tsql-md.md)] 設定 TDE，必須符合下列需求：

-   您必須已經註冊 TDE 預覽版。

-   若要建立資料庫的加密金鑰，您必須是 [!INCLUDE[ssSDS](../includes/sssds-md.md)] 系統管理員，或是 master 資料庫中之 **dbmanager** 角色的成員，並具備該資料庫的 **CONTROL** 權限。

-   若要執行 ALTER DATABASE 陳述式與 SET 選項，便只需要具備 **dbmanager** 角色的成員資格。

##  <a name="sign-up-for-the-preview-of-tde-and-enable-tde-on-a-database"></a><a name="Preview"></a>註冊 TDE 的預覽，並在資料庫上啟用 TDE

1.  請造訪 Azure 入口網站[https://portal.azure.com](https://portal.azure.com) ，並使用您的 Azure 系統管理員或參與者帳戶登入。

2.  在左邊的橫幅中，按一下以**瀏覽**，然後按一下 [**SQL 資料庫**]。

3.  利用左窗格中選取的 [**SQL 資料庫**]，按一下您的使用者資料庫。

4.  在資料庫刀鋒視窗中，按一下 [所有設定] ****。

5.  在 [設定] **** 刀鋒視窗中，按一下 [透明資料加密 (預覽版)] **** 部分，以開啟 [透明資料加密 (預覽版)] **** 刀鋒視窗。 若還未註冊 TDE 預覽版，資料加密設定將會停用，直到您完成註冊為止。

6.  按一下 [預覽條款] ****。

7.  閱讀預覽的條款，如果您同意這些條款，請選取 [**透明資料 encryptionPreview 詞彙**] 核取方塊，然後按一下頁面底部附近的 **[確定]** 。 返回 [**資料 encryptionPREVIEW** ] 分頁，此時應該會啟用 [**資料加密**] 按鈕。

8.  在 [資料加密預覽] **** 刀鋒視窗中，將 [資料加密] **** 按鈕移至 [開啟] ****，然後按一下 [儲存] **** (位於頁面頂端)，以套用此設定。 [加密狀態] **** 會顯示透明資料加密的概略進度。

     ![SQLDB_TDE_TermsNewUI](../../2014/database-engine/media/sqldb-tde-termsnewui.png "SQLDB_TDE_TermsNewUI")

     您也可以使用查詢工具 (例如 [!INCLUDE[ssSDS](../includes/sssds-md.md)] )，以具有 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] VIEW DATABASE STATE **權限的資料庫使用者身分，連接到** 監視加密進度。 查詢`encryption_state` [sys.databases dm_database_encryption_keys](/sql/relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql)視圖的資料行。

##  <a name="enabling-tde-on-sssds-by-using-transact-sql"></a><a name="Encrypt"></a>使用 Transact-sql 啟用[!INCLUDE[ssSDS](../includes/sssds-md.md)]的 TDE
 下列步驟中假設您已經註冊預覽版。

###  <a name="TsqlProcedure"></a>

1.  使用 master 資料庫中之 **dbmanager** 角色的系統管理員或成員身分的登入，連接到資料庫。

2.  執行下列陳述式，以建立資料庫加密金鑰及加密資料庫。

    ```sql
    -- Create the database encryption key that will be used for TDE.
    CREATE DATABASE ENCRYPTION KEY 
    WITH ALGORITHM = AES_256 
    ENCRYPTION BY SERVER CERTIFICATE ##MS_TdeCertificate##;

    -- Enable encryption
    ALTER DATABASE [AdventureWorks] SET ENCRYPTION ON;
    GO
    ```

3.  [!INCLUDE[ssSDS](../includes/sssds-md.md)]若要監視的加密進度，具有**VIEW database STATE**許可權的資料庫使用者可以查詢`encryption_state` [sys.databases dm_database_encryption_keys](/sql/relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql)視圖的資料行。

## <a name="enabling-tde-on-sql-database-by-using-powershell"></a>使用 PowerShell 啟用 SQL Database 的 TDE
 您可以使用 Azure PowerShell，執行下列命令開啟/關閉 TDE。 您必須將您的帳戶連接到 PS 視窗，才能執行此命令。 下列步驟中假設您已經註冊預覽版。 如需 PowerShell 的其他相關資訊，請參閱 [如何安裝及設定 Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/)。

1.  啟用 TDE、傳回 TDE 狀態及檢視加密活動。

    ```powershell
    Switch-AzureMode -Name AzureResourceManager
    Set-AzureSqlDatabaseTransparentDataEncryption -ServerName "myserver" -ResourceGroupName "Default-SQL-WestUS" -DatabaseName "database1" -State "Enabled"

    Get-AzureSqlDatabaseTransparentDataEncryption -ServerName "myserver" -ResourceGroupName "Default-SQL-WestUS" -DatabaseName "database1"
    Get-AzureSqlDatabaseTransparentDataEncryptionActivity -ServerName "myserver" -ResourceGroupName "Default-SQL-WestUS" -DatabaseName "database1"
    ```

2.  若要停用 TDE：

    ```powershell
    Set-AzureSqlDatabaseTransparentDataEncryption -ServerName "myserver" -ResourceGroupName "Default-SQL-WestUS" -DatabaseName "database1" -State "Disabled"
    Switch-AzureMode -Name AzureServiceManagement
    ```

##  <a name="decrypting-a-tde-protected-database-on-sssds"></a><a name="Decrypt"></a>解密上受 TDE 保護的資料庫[!INCLUDE[ssSDS](../includes/sssds-md.md)]

#### <a name="to-disable-tde-by-using-the-azure-portal"></a>使用 Azure 入口網站停用 TDE

1.  請造訪 Azure 入口網站[https://portal.azure.com](https://portal.azure.com) ，並使用您的 Azure 系統管理員或參與者帳戶登入。

2.  在左邊的橫幅中，按一下以**瀏覽**，然後按一下 [**SQL 資料庫**]。

3.  利用左窗格中選取的 [**SQL 資料庫**]，按一下您的使用者資料庫。

4.  在資料庫刀鋒視窗中，按一下 [所有設定] ****。

5.  在 [設定] **** 刀鋒視窗中，按一下 [透明資料加密 (預覽版)] **** 部分，以開啟 [透明資料加密 (預覽版)] **** 刀鋒視窗。

6.  在 [透明資料加密預覽] **** 刀鋒視窗中，將 [資料加密] **** 按鈕移至 [關閉] ****，然後按一下 [儲存] **** (位於頁面頂端)，以套用此設定。 [加密狀態] **** 會顯示透明資料解密的概略進度。

     您也可以使用查詢工具 (例如 [!INCLUDE[ssSDS](../includes/sssds-md.md)] )，以具有 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] VIEW DATABASE STATE **權限的資料庫使用者身分，連接到** 監視解密進度。 查詢`encryption_state` [sys.databases dm_database_encryption_keys](/sql/relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql)視圖的資料行。

#### <a name="to-disable-tde-by-using-transact-sql"></a>使用 TRANSACT-SQL 停用 TDE

1.  使用 master 資料庫中之 **dbmanager** 角色的系統管理員或成員身分的登入，連接到資料庫。

2.  執行下列陳述式，以解密資料庫。

    ```sql
    -- Enable encryption
    ALTER DATABASE [AdventureWorks] SET ENCRYPTION OFF;
    GO
    ```

3.  [!INCLUDE[ssSDS](../includes/sssds-md.md)]若要監視的加密進度，具有**VIEW database STATE**許可權的資料庫使用者可以查詢`encryption_state` [sys.databases dm_database_encryption_keys](/sql/relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql)視圖的資料行。

##  <a name="working-with-tde-protected-databases-on-sssds"></a><a name="Working"></a>使用上的 TDE 受保護資料庫[!INCLUDE[ssSDS](../includes/sssds-md.md)]
 您無須解密資料庫，即可在 Azure 執行作業。 目標會自動繼承來源資料庫或主要資料庫的 TDE 設定。 這包括下列作業：

-   異地複原

-   自助時間點還原

-   還原已刪除的資料庫

-   使用中的異地複寫

-   建立資料庫複本

##  <a name="moving-a-tde-protected-database-on-using-bacpac-files"></a><a name="Moving"></a>使用在上移動 TDE 保護的資料庫。Bacpac 檔案
 在 [!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)] 入口網站使用 [匯出資料庫] 功能或 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的 [匯入和匯出精靈] 匯出受 TDE 保護的資料庫時，資料庫內容不會加密。 該內容會儲存在未加密的 .bacpac 檔案中。  請務必為 .bacpac 檔案施以適當的保護措施，並在匯入新資料庫作業完成時，立即啟用 TDE。

## <a name="related-sql-server-topic"></a>相關的 SQL Server 主題
 [使用 EKM 啟用 TDE](../relational-databases/security/encryption/enable-tde-on-sql-server-using-ekm.md)

## <a name="see-also"></a>另請參閱
 [透明資料加密 &#40;TDE&#41;](../relational-databases/security/encryption/transparent-data-encryption.md) [建立認證 &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/create-credential-transact-sql) [建立非對稱金鑰 &#40;](/sql/t-sql/statements/create-asymmetric-key-transact-sql) transact-sql&#41;[建立資料庫加密金鑰](/sql/t-sql/statements/create-database-encryption-key-transact-sql)&#40;TRANSACT-SQL&#41;[alter Database &#40;transact-sql&#41;](/sql/t-sql/statements/alter-database-transact-sql) [alter database SET 選項 &#40;transact-sql&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)
