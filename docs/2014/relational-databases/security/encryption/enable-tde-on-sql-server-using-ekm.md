---
title: 使用 EKM 啟用 TDE |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- encryption [SQL Server], TDE using an EKM
- TDE, EKM how to
- EKM, TDE how to
- Transparent Data Encryption, using EKM
ms.assetid: b892e7a7-95bd-4903-bf54-55ce08e225af
author: aliceku
ms.author: aliceku
manager: craigg
ms.openlocfilehash: e55afa78d82c19d9a6a09226c537ca95f65105ef
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63011512"
---
# <a name="enable-tde-using-ekm"></a>使用 EKM 啟用 TDE
  此主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] ，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中透過使用儲存在可延伸金鑰管理 (EKM) 模組中的非對稱金鑰，啟用透明資料加密 (TDE) 以保護資料庫加密金鑰。  
  
 TDE 會使用稱為資料庫加密金鑰的對稱金鑰，將整個資料庫的儲存體加密。 也可以使用憑證來保護資料庫加密金鑰，該憑證是由 master 資料庫的資料庫主要金鑰所保護。 如需有關使用資料庫主要金鑰來保護資料庫加密金鑰的詳細資訊，請參閱[透明資料加密 &#40;TDE&#41;](transparent-data-encryption.md)。 如需 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 在 Azure VM 上執行時設定 TDE 的相關資訊，請參閱[使用 Azure 金鑰保存庫進行可延伸金鑰管理 &#40;SQL Server&#41;](extensible-key-management-using-azure-key-vault-sql-server.md)。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [Security](#Security)  
  
-   [若要啟用 TDE，EKM，使用 TRANSACT-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   您必須是高權限使用者 (如系統管理員) 才能建立資料庫加密金鑰及加密資料庫。 該使用者必須能夠由 EKM 模組來驗證。  
  
-   一啟動時， [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 就必須開啟資料庫。 若要這樣做，您應該建立要由 EKM 所驗證的認證，並將它加入到根據非對稱金鑰的登入中。 使用者無法使用該登入來進行登入，但是 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 將能夠使用 EKM 裝置來驗證本身。  
  
-   如果遺失了 EKM 模組內所儲存的非對稱金鑰， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]將無法開啟資料庫。 如果 EKM 提供者可讓您備份非對稱金鑰，您應該建立備份，並將它儲存在安全的位置。  
  
-   您的 EKM 提供者所需的選項和參數可能不同於以下程式碼範例中所提供的選項和參數。 如需詳細資訊，請洽詢 EKM 提供者。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 此主題會使用以下權限：  
  
-   若要變更組態選項及執行 RECONFIGURE 陳述式，您必須取得 ALTER SETTINGS 伺服器層級的權限。 **系統管理員 (sysadmin)** 及 **serveradmin** 固定伺服器角色會隱含 ALTER SETTINGS 權限。  
  
-   需要 ALTER ANY CREDENTIAL 權限。  
  
-   需要 ALTER ANY LOGIN 權限。  
  
-   需要 CREATE ASYMMETRIC KEY 權限。  
  
-   需要資料庫的 CONTROL 權限才能加密資料庫。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-enable-tde-using-ekm"></a>若要使用 EKM 啟用 TDE  
  
1.  將 EKM 提供者提供的檔案複製到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 電腦上的適當位置。 在此範例中，我們使用 **C:\EKM** 資料夾。  
  
2.  依照 EKM 提供者的要求將憑證安裝到電腦上。  
  
    > [!NOTE]  
    >  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 未提供 EKM 提供者。 每一個 EKM 提供者都會有安裝、設定及授權使用者的不同程序。  請參閱 EKM 提供者文件集來完成這個步驟。  
  
3.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]的執行個體。  
  
4.  在標準列上，按一下 **[新增查詢]** 。  
  
5.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```  
    -- Enable advanced options.  
    sp_configure 'show advanced options', 1 ;  
    GO  
    RECONFIGURE ;  
    GO  
    -- Enable EKM provider  
    sp_configure 'EKM provider enabled', 1 ;  
    GO  
    RECONFIGURE ;  
    GO  
    -- Create a cryptographic provider, which we have chosen to call "EKM_Prov," based on an EKM provider  
  
    CREATE CRYPTOGRAPHIC PROVIDER EKM_Prov   
    FROM FILE = 'C:\EKM_Files\KeyProvFile.dll' ;  
    GO  
  
    -- Create a credential that will be used by system administrators.  
    CREATE CREDENTIAL sa_ekm_tde_cred   
    WITH IDENTITY = 'Identity1',   
    SECRET = 'q*gtev$0u#D1v'   
    FOR CRYPTOGRAPHIC PROVIDER EKM_Prov ;  
    GO  
  
    -- Add the credential to a high privileged user such as your   
    -- own domain login in the format [DOMAIN\login].  
    ALTER LOGIN Contoso\Mary  
    ADD CREDENTIAL sa_ekm_tde_cred ;  
    GO  
    -- create an asymmetric key stored inside the EKM provider  
    USE master ;  
    GO  
    CREATE ASYMMETRIC KEY ekm_login_key   
    FROM PROVIDER [EKM_Prov]  
    WITH ALGORITHM = RSA_512,  
    PROVIDER_KEY_NAME = 'SQL_Server_Key' ;  
    GO  
  
    -- Create a credential that will be used by the Database Engine.  
    CREATE CREDENTIAL ekm_tde_cred   
    WITH IDENTITY = 'Identity2'   
    , SECRET = 'jeksi84&sLksi01@s'   
    FOR CRYPTOGRAPHIC PROVIDER EKM_Prov ;  
  
    -- Add a login used by TDE, and add the new credential to the login.  
    CREATE LOGIN EKM_Login   
    FROM ASYMMETRIC KEY ekm_login_key ;  
    GO  
    ALTER LOGIN EKM_Login   
    ADD CREDENTIAL ekm_tde_cred ;  
    GO  
  
    -- Create the database encryption key that will be used for TDE.  
    USE AdventureWorks2012 ;  
    GO  
    CREATE DATABASE ENCRYPTION KEY  
    WITH ALGORITHM  = AES_128  
    ENCRYPTION BY SERVER ASYMMETRIC KEY ekm_login_key ;  
    GO  
  
    -- Alter the database to enable transparent data encryption.  
    ALTER DATABASE AdventureWorks2012   
    SET ENCRYPTION ON ;  
    GO  
    ```  
  
 如需詳細資訊，請參閱下列內容：  
  
-   [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
-   [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-cryptographic-provider-transact-sql)  
  
-   [CREATE CREDENTIAL &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-credential-transact-sql)  
  
-   [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-asymmetric-key-transact-sql)  
  
-   [CREATE LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-login-transact-sql)  
  
-   [CREATE DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-database-encryption-key-transact-sql)  
  
-   [ALTER LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-login-transact-sql)  
  
-   [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)  
  
-   [使用 Azure 金鑰保存庫進行可延伸金鑰管理 &#40;SQL Server&#41;](extensible-key-management-using-azure-key-vault-sql-server.md)  
  
-   [Azure SQL Database 的透明資料加密](../../../database-engine/transparent-data-encryption-with-azure-sql-database.md)  
  
  
