---
title: 搭配使用 SQL Server 連接器與 SQL 加密功能 | Microsoft 文件
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: vanto
ms.suite: sql
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Connector, using
- EKM, with SQL Server Connector
ms.assetid: 58fc869e-00f1-4d7c-a49b-c0136c9add89
caps.latest.revision: 14
author: aliceku
ms.author: aliceku
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 57294027687687f72fd7ae2841a25c0e668de43a
ms.sourcegitcommit: 3762dd447ca4bb449eda8476e72f393db0851b38
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/18/2018
ms.locfileid: "46013843"
---
# <a name="use-sql-server-connector-with-sql-encryption-features"></a>搭配使用 SQL Server 連接器與 SQL 加密功能
[!INCLUDE[appliesto-xx-asdb-xxxx-xxx-md](../../../includes/appliesto-xx-asdb-xxxx-xxx-md.md)]
  使用 Azure 金鑰保存庫所保護之非對稱金鑰進行的一般 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 加密活動，包括下列三個區域。  
  
-   使用 Azure 金鑰保存庫中的非對稱金鑰進行透明資料加密  
  
-   使用金鑰保存庫中的非對稱金鑰進行備份加密  
  
-   使用金鑰保存庫中的非對稱金鑰進行資料行層級加密  
  
 請先完成 [使用 Azure 金鑰保存庫進行可延伸金鑰管理的設定步驟](../../../relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault.md)主題的第 I 部分到第 IV 部分，再遵循這個主題上的步驟。  
 
> [!NOTE]  
>  1.0.0.440 版和較舊版本皆已被取代，而且生產環境也不再支援。 請前往 [Microsoft 下載中心](https://www.microsoft.com/download/details.aspx?id=45344) ，使用＜SQL Server 連接器升級＞下 [SQL Server 連接器維護和疑難排解](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md) 頁面的指示，升級為 1.0.1.0 版或更新版本。  
  
## <a name="transparent-data-encryption-by-using-an-asymmetric-key-from-azure-key-vault"></a>使用 Azure 金鑰保存庫中的非對稱金鑰進行透明資料加密  
 完成＜使用 Azure 金鑰保存庫進行可延伸金鑰管理的設定步驟＞主題的第 I 部分到第 IV 部分之後，請使用 Azure 金鑰保存庫金鑰以使用 TDE 來加密資料庫加密金鑰。  
您需要建立認證和登入，並建立資料庫加密金鑰來加密資料和資料庫中的記錄檔。 若要加密資料庫，則需要資料庫的 **CONTROL** 權限。 下圖顯示使用 Azure 金鑰保存庫時的加密金鑰階層。  
  
 ![含有 AKV 的 EKM 金鑰階層](../../../relational-databases/security/encryption/media/ekm-key-hierarchy-with-akv.png "含有 AKV 的 EKM 金鑰階層")  
  
1.  **建立 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 認證來供 Database Engine 用於 TDE**  
  
     在資料庫載入期間，Database Engine 使用該認證來存取金鑰保存庫。 建議在第 I 部分中針對 **建立另一個 Azure Active Directory** 用戶端識別碼 **和** 機密 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]，以限制授與的金鑰保存庫權限。  
  
     使用下列方式修改下面的 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 指令碼：  
  
    -   編輯 `IDENTITY` 引數 (`ContosoDevKeyVault`)，以指向您的 Azure 金鑰保存庫。
        - 如果您使用的是 **公用 Azure**，請將 `IDENTITY` 引數取代為第 II 部分中的 Azure 金鑰保存庫名稱。
        - 如果您使用的是 **私人 Azure 雲端** (例如 Azure Government、Azure China 或 Azure Germany)，請將 `IDENTITY` 引數取代為第 II 部分的步驟 3 中所傳回的保存庫 URI。 請不要在保存庫 URI 中包括 "https://"。   
  
    -   將 `SECRET` 引數的第一個部分取代為第 I 部分中的 Azure Active Directory **用戶端識別碼** 。在此範例中， **用戶端識別碼** 是 `EF5C8E094D2A4A769998D93440D8115D`。  
  
        > [!IMPORTANT]  
        >  您必須移除 **用戶端識別碼**中的連字號。  
  
    -   使用第 I 部分中的 `SECRET` 用戶端密碼 **，完成** 引數的第二個部分。在此範例中，第 1 部分中的 **用戶端密碼** 是 `Replace-With-AAD-Client-Secret`。 `SECRET` 引數的最終字串將是一連串較長的字母和數字， *不含連字號*。  
  
    ```sql  
    USE master;  
    CREATE CREDENTIAL Azure_EKM_TDE_cred   
        WITH IDENTITY = 'ContosoDevKeyVault', -- for public Azure
        -- WITH IDENTITY = 'ContosoDevKeyVault.vault.usgovcloudapi.net', -- for Azure Government
        -- WITH IDENTITY = 'ContosoDevKeyVault.vault.azure.cn', -- for Azure China
        -- WITH IDENTITY = 'ContosoDevKeyVault.vault.microsoftazure.de', -- for Azure Germany   
        SECRET = 'EF5C8E094D2A4A769998D93440D8115DReplace-With-AAD-Client-Secret'   
    FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov;  
    ```  
  
2.  **針對進行 TDE 的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 建立 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 登入**  
  
     建立 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登入，並在其中新增步驟 1 中的認證。 這個 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 範例會使用稍早匯入的相同金鑰。  
  
    ```sql  
    USE master;  
    -- Create a SQL Server login associated with the asymmetric key   
    -- for the Database engine to use when it loads a database   
    -- encrypted by TDE.  
    CREATE LOGIN TDE_Login   
    FROM ASYMMETRIC KEY CONTOSO_KEY;  
    GO   
  
    -- Alter the TDE Login to add the credential for use by the   
    -- Database Engine to access the key vault  
    ALTER LOGIN TDE_Login   
    ADD CREDENTIAL Azure_EKM_TDE_cred ;  
    GO  
    ```  
  
3.  **建立資料庫加密金鑰 (DEK)**  
  
     DEK 將加密您在資料庫執行個體中的資料和記錄檔，接著再透過 Azure 金鑰保存庫非對稱金鑰進行加密。 DEK 可以使用任何 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 支援的演算法或金鑰長度來建立。  
  
    ```sql  
    USE ContosoDatabase;  
    GO  
  
    CREATE DATABASE ENCRYPTION KEY   
    WITH ALGORITHM = AES_256   
    ENCRYPTION BY SERVER ASYMMETRIC KEY CONTOSO_KEY;  
    GO  
    ```  
  
4.  **開啟 TDE**  
  
    ```sql  
    -- Alter the database to enable transparent data encryption.  
    ALTER DATABASE ContosoDatabase   
    SET ENCRYPTION ON;  
    GO  
    ```  
  
     使用 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]，透過使用物件總管連接到您的資料庫，來確認已開啟 TDE。 以滑鼠右鍵按一下您的資料庫，指向 [工作]，然後按一下 [管理資料庫加密]。  
  
     ![EKM TDE 物件總管](../../../relational-databases/security/encryption/media/ekm-tde-object-explorer.png "EKM TDE 物件總管")  
  
     在 **[管理資料庫加密]** 對話方塊中，確認已開啟 TDE，以及哪個非對稱金鑰正在加密 DEK。  
  
     ![EKM TDE 對話方塊](../../../relational-databases/security/encryption/media/ekm-tde-dialog-box.png "EKM TDE 對話方塊")  
  
     或者，您可以執行下列 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 指令碼。 加密狀態 3 表示加密的資料庫。  
  
    ```sql  
    USE MASTER  
    SELECT * FROM sys.asymmetric_keys  
  
    -- Check which databases are encrypted using TDE  
    SELECT d.name, dek.encryption_state   
    FROM sys.dm_database_encryption_keys AS dek  
    JOIN sys.databases AS d  
         ON dek.database_id = d.database_id;  
    ```  
  
    > [!NOTE]  
    >  只要任何資料庫啟用 TDE，就會自動加密 `tempdb` 資料庫。  
  
## <a name="encrypting-backups-by-using-an-asymmetric-key-from-the-key-vault"></a>使用金鑰保存庫中的非對稱金鑰進行備份加密  
 自 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]開始，支援加密備份。 下列範例如何建立及還原以資料加密金鑰加密的備份，這個資料加密金鑰受到金鑰保存庫中非對稱金鑰的保護。  
在資料庫載入期間存取金鑰保存庫時， [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 需要認證。 建議在第 I 部分中針對 Database Engine 建立另一個 Azure Active Directory 用戶端識別碼和機密，以限制授與的金鑰保存庫權限。  
  
1.  **建立 SQL Server 認證，以供 Database Engine 用於備份加密**  
  
     使用下列方式修改下面的 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 指令碼：  
  
    -   編輯 `IDENTITY` 引數 (`ContosoDevKeyVault`)，以指向您的 Azure 金鑰保存庫。
        - 如果您使用的是 **公用 Azure**，請將 `IDENTITY` 引數取代為第 II 部分中的 Azure 金鑰保存庫名稱。
        - 如果您使用的是 **私人 Azure 雲端** (例如 Azure Government、Azure China 或 Azure Germany)，請將 `IDENTITY` 引數取代為第 II 部分的步驟 3 中所傳回的保存庫 URI。 請不要在保存庫 URI 中包括 "https://"。    
  
    -   將 `SECRET` 引數的第一個部分取代為第 I 部分中的 Azure Active Directory **用戶端識別碼** 。在此範例中， **用戶端識別碼** 是 `EF5C8E094D2A4A769998D93440D8115D`。  
  
        > [!IMPORTANT]  
        >  您必須移除 **用戶端識別碼**中的連字號。  
  
    -   使用第 I 部分中的 `SECRET` 用戶端密碼 **，完成** 引數的第二個部分。在此範例中，第 I 部分中的 **用戶端密碼** 是 `Replace-With-AAD-Client-Secret`。 `SECRET` 引數的最終字串將是一連串較長的字母和數字， *不含連字號*。   
  
        ```sql  
        USE master;  
  
        CREATE CREDENTIAL Azure_EKM_Backup_cred   
            WITH IDENTITY = 'ContosoDevKeyVault', -- for public Azure
            -- WITH IDENTITY = 'ContosoDevKeyVault.vault.usgovcloudapi.net', -- for Azure Government
            -- WITH IDENTITY = 'ContosoDevKeyVault.vault.azure.cn', -- for Azure China
            -- WITH IDENTITY = 'ContosoDevKeyVault.vault.microsoftazure.de', -- for Azure Germany   
            SECRET = 'EF5C8E094D2A4A769998D93440D8115DReplace-With-AAD-Client-Secret'   
        FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov;    
        ```  
  
2.  **針對進行備份加密的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 建立 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 登入**  
  
     建立 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 用於加密備份的 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]登入，並在其中新增步驟 1 中的認證。 這個 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 範例會使用稍早匯入的相同金鑰。  
  
    > [!IMPORTANT]  
    >  如果您已經使用相同的非對稱金鑰進行 TDE (上方範例) 或資料行層級加密 (下列範例)，則無法使用該非對稱金鑰進行備份加密。  
  
     這個範例使用儲存在金鑰保存庫中的 `CONTOSO_KEY_BACKUP` 非對稱金鑰，該金鑰可以提早針對 master 資料庫進行匯入或建立 (如第 IV 部分步驟 5 中所述)。  
  
    ```sql  
    USE master;  
  
    -- Create a SQL Server login associated with the asymmetric key   
    -- for the Database engine to use when it is encrypting the backup.  
    CREATE LOGIN Backup_Login   
    FROM ASYMMETRIC KEY CONTOSO_KEY_BACKUP;  
    GO   
  
    -- Alter the Encrypted Backup Login to add the credential for use by   
    -- the Database Engine to access the key vault  
    ALTER LOGIN Backup_Login   
    ADD CREDENTIAL Azure_EKM_Backup_cred ;  
    GO  
    ```  
  
3.  **備份資料庫**  
  
     請使用儲存在金鑰保存庫中的非對稱金鑰指定加密，並備份資料庫。
     
     在下列範例中，請注意，若資料庫已使用 TDE 加密，且非對稱金鑰 `CONTOSO_KEY_BACKUP` 不同於 TDE 的非對稱金鑰，則備份將透過 TDE 非對稱金鑰和 `CONTOSO_KEY_BACKUP` 這兩者加密。 目標 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體需要這兩個金鑰來解密備份。
  
    ```sql  
    USE master;  
  
    BACKUP DATABASE [DATABASE_TO_BACKUP]  
    TO DISK = N'[PATH TO BACKUP FILE]'   
    WITH FORMAT, INIT, SKIP, NOREWIND, NOUNLOAD,   
    ENCRYPTION(ALGORITHM = AES_256,   
    SERVER ASYMMETRIC KEY = [CONTOSO_KEY_BACKUP]);  
    GO  
    ```  
  
4.  **還原資料庫**  
    
    若要還原使用 TDE 加密的資料庫備份，目標 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體必須先有一份用於加密的非對稱金鑰保存庫金鑰。 以下是達成此目的的方法：  
    
    - 若金鑰保存庫中不再有原始用於 TDE 的非對稱金鑰，請還原金鑰保存庫的金鑰備份或重新匯入本機 HSM 中的金鑰。 **重要事項︰** 為了使金鑰的指紋符合資料庫備份上記錄的指紋，金鑰必須命名為與之前原始名稱**相同的金鑰保存庫金鑰名稱**。
    
    - 將步驟 1 和 2 套用在目標 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體上。
    
    - 一旦目標 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體可存取用於加密備份的非對稱金鑰，請還原伺服器上的資料庫。
    
     範例還原程式碼：  
  
    ```sql  
    RESTORE DATABASE [DATABASE_TO_BACKUP]  
    FROM DISK = N'[PATH TO BACKUP FILE]'   
        WITH FILE = 1, NOUNLOAD, REPLACE;  
    GO  
    ```  
  
     如需備份選項的詳細資訊，請參閱 [BACKUP (Transact-SQL)](../../../t-sql/statements/backup-transact-sql.md)。  
  
## <a name="column-level-encryption-by-using-an-asymmetric-key-from-the-key-vault"></a>使用金鑰保存庫中的非對稱金鑰進行資料行層級加密  
 下列範例會建立受到金鑰保存庫中非對稱金鑰保護的對稱金鑰。 然後使用對稱金鑰加密資料庫中的資料。  
  
> [!IMPORTANT]  
>  如果您已經使用相同的非對稱金鑰進行 TDE 或備份加密 (前面的範例)，則無法使用該非對稱金鑰進行備份加密。  
  
 這個範例使用儲存在金鑰保存庫中的 `CONTOSO_KEY_COLUMNS` 非對稱金鑰，該金鑰可以提早進行匯入或建立 (如 [使用 Azure 金鑰保存庫進行可延伸金鑰管理的設定步驟](../../../relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault.md)第 3 節步驟 3 中所述)。 若要在 `ContosoDatabase` 資料庫中使用這個非對稱金鑰，您必須再執行一次 `CREATE ASYMMETRIC KEY` 陳述式，以提供參考這個金鑰的 `ContosoDatabase` 資料庫。  
  
```sql  
USE [ContosoDatabase];  
GO  
  
-- Create a reference to the key in the key vault  
CREATE ASYMMETRIC KEY CONTOSO_KEY_COLUMNS   
FROM PROVIDER [AzureKeyVault_EKM_Prov]  
WITH PROVIDER_KEY_NAME = 'ContosoDevRSAKey2',  
CREATION_DISPOSITION = OPEN_EXISTING;  
  
-- Create the data encryption key.  
-- The data encryption key can be created using any SQL Server   
-- supported algorithm or key length.  
-- The DEK will be protected by the asymmetric key in the key vault  
  
CREATE SYMMETRIC KEY DATA_ENCRYPTION_KEY  
    WITH ALGORITHM=AES_256  
    ENCRYPTION BY ASYMMETRIC KEY CONTOSO_KEY_COLUMNS;  
  
DECLARE @DATA VARBINARY(MAX);  
  
--Open the symmetric key for use in this session  
OPEN SYMMETRIC KEY DATA_ENCRYPTION_KEY   
DECRYPTION BY ASYMMETRIC KEY CONTOSO_KEY_COLUMNS;  
  
--Encrypt syntax  
SELECT @DATA = ENCRYPTBYKEY  
    (  
    KEY_GUID('DATA_ENCRYPTION_KEY'),   
    CONVERT(VARBINARY,'Plain text data to encrypt')  
    );  
  
-- Decrypt syntax  
SELECT CONVERT(VARCHAR, DECRYPTBYKEY(@DATA));  
  
--Close the symmetric key  
CLOSE SYMMETRIC KEY DATA_ENCRYPTION_KEY;  
```  
  
## <a name="see-also"></a>另請參閱  
 [使用 Azure 金鑰保存庫進行可延伸金鑰管理的設定步驟](../../../relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault.md)   
 [使用 Azure Key Vault 進行可延伸金鑰管理](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
 [EKM provider enabled 伺服器組態選項](../../../database-engine/configure-windows/ekm-provider-enabled-server-configuration-option.md)   
 [SQL Server 連接器維護和疑難排解](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md)  
  
  
