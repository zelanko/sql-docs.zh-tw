---
title: 使用 Azure Key Vault 進行可延伸金鑰管理 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- EKM, with key vault
- TDE, EKM and key vault
- Extensible Key Management with key vault
- Key Management with key vault
- Transparent Data Encryption, using EKM and key vault
ms.assetid: 3efdc48a-8064-4ea6-a828-3fbf758ef97c
caps.latest.revision: 37
author: aliceku
ms.author: aliceku
manager: craigg
ms.openlocfilehash: ecd049528577ff5da601bf37fda3e8b356acb0e3
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37305428"
---
# <a name="extensible-key-management-using-azure-key-vault-sql-server"></a>使用 Azure Key Vault 進行可延伸金鑰管理 (SQL Server)
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Connector for [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Azure Key Vault 可讓[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]加密可以利用 Azure Key Vault 服務的身分[Extensible Key Management &#40;EKM&#41; ](extensible-key-management-ekm.md)提供者來保護其加密金鑰。  
  
 本主題內容：  
  
-   [EKM 的使用方式](#Uses)  
  
-   [步驟 1： 設定金鑰保存庫，以供 SQL Server](#Step1)  
  
-   [步驟 2： 安裝 SQL Server Connector](#Step2)  
  
-   [步驟 3： 設定 SQL Server 對金鑰保存庫使用 EKM 提供者](#Step3)  
  
-   [範例 a： 使用從 Key Vault 的非對稱金鑰的透明資料加密](#ExampleA)  
  
-   [範例 b： 使用從 Key Vault 的非對稱金鑰來加密備份](#ExampleB)  
  
-   [範例 c： 使用資料行層級加密的金鑰保存庫的非對稱金鑰](#ExampleC)  
  
##  <a name="Uses"></a> EKM 的使用方式  
 組織可以使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 加密來保護機密資料。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 加密包含[透明資料加密&#40;TDE&#41;](transparent-data-encryption.md)，[資料行層級加密](/sql/t-sql/functions/cryptographic-functions-transact-sql)(CLE) 和[備份加密](../../backup-restore/backup-encryption.md)。 在上述所有情況下，資料會使用對稱資料加密金鑰來加密。 對稱資料加密金鑰會以儲存在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中的金鑰階層加密，受到更進一步的保護。 或者，EKM 提供者架構可讓[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]使用來保護資料加密金鑰儲存在非對稱金鑰[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]外部的密碼編譯提供者中。 使用 EKM 提供者架構會多增加一層安全性，讓組織得以分開管理金鑰和資料。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Connector for Azure Key Vault 可讓[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]運用可擴充、 高效能和高可用性的金鑰保存庫服務為加密金鑰保護的 EKM 提供者。 金鑰保存庫服務可以搭配[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]上的安裝[!INCLUDE[msCoName](../../../includes/msconame-md.md)]Azure 虛擬機器和內部部署伺服器。 金鑰保存庫服務也提供選項，以使用受到緊密控制和監視的硬體安全性模組 (HSM)，對非對稱加密金鑰提供更高等級的保護。 如需金鑰保存庫的詳細資訊，請參閱 [Azure 金鑰保存庫](http://go.microsoft.com/fwlink/?LinkId=521401)。  
  
 下列影像摘要說明使用金鑰保存庫的 EKM 處理流程。 影像中的程序步驟數字並非用以比對遵循影像的安裝步驟數字。  
  
 ![使用 Azure Key Vault 的 SQL Server EKM](../../../database-engine/media/ekm-using-azure-key-vault.png "使用 Azure Key Vault 的 SQL Server EKM")  
  
##  <a name="Step1"></a> 步驟 1： 設定金鑰保存庫以供 SQL Server  
 下列步驟可用來設定金鑰保存庫，以搭配 [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)] 提供加密金鑰保護。 組織中可能已使用保存庫。 在您指定來管理加密金鑰的組織中的 Azure 系統管理員時保存庫不存在，可以建立保存庫、 產生非對稱金鑰在保存庫，和接著授權[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]來使用的金鑰。 透過檢閱 [開始使用 Azure Key Vault](http://go.microsoft.com/fwlink/?LinkId=521402)及 PowerShell [Azure Key Vault Cmdlet](http://go.microsoft.com/fwlink/?LinkId=521403) 參考，讓自己熟悉如何使用金鑰保存庫服務。  
  
> [!IMPORTANT]  
>  如果您有多個 Azure 訂用帳戶，您必須使用的訂用帳戶包含[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
1.  **建立保存庫：** 透過 **開始使用 Azure 金鑰保存庫** 中 [建立金鑰保存庫](http://go.microsoft.com/fwlink/?LinkId=521402)一節中的指示，來建立保存庫。 記錄保存庫的名稱。 本主題使用 **ContosoKeyVault** 做為金鑰保存庫名稱。  
  
2.  **保存庫中產生非對稱金鑰：** 金鑰保存庫中的非對稱金鑰來保護[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]加密金鑰。 只有非對稱金鑰的公開部分可離開保存庫，保存庫絕不會匯出私用部分。 使用非對稱金鑰的所有密碼編譯作業會委派給 Azure Key Vault，並受到金鑰保存庫安全性的保護。  
  
     您可以使用數種方式來產生非對稱金鑰，並將它儲存在保存庫。 您可以在外部產生金鑰，並將金鑰以 .pfx 檔案形式匯入到保存庫。 或使用金鑰保存庫 API 直接在保存庫中建立金鑰。  
  
     [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]連接器需要為 2048年位元 RSA 的非對稱金鑰和金鑰名稱只能使用字元"a-z"、"A-Z"、"0-9"，和 「-」。 在本文件中，非對稱金鑰的名稱會是 **ContosoMasterKey**。 請以您用於金鑰的唯一名稱來取代這個名稱。  
  
    > [!IMPORTANT]  
    >  強烈建議在生產案例中匯入非對稱金鑰，因為這樣做可讓系統管理員在金鑰委付系統中委付金鑰。 如果非對稱金鑰是在保存庫中建立，由於私密金鑰永遠不會離開保存庫，因此無法委付金鑰。 您應該委付用來保護重要資料的金鑰。 遺失非對稱金鑰會導致資料永久無法復原。  
  
    > [!IMPORTANT]  
    >  金鑰保存庫支援多種版本的相同指定金鑰。 若要使用的索引鍵[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]連接器不應建立版本或進行復原。 如果系統管理員想要復原 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 加密所使用的金鑰，應該在保存庫中建立不同名稱的新金鑰，用來加密 DEK。  
  
     如需如何將金鑰匯入金鑰保存庫或在金鑰保存庫中建立金鑰 (生產環境不建議使用) 的詳細資訊，請參閱 **開始使用 Azure Key Vault**[中的將金鑰或密碼加入金鑰保存庫](http://go.microsoft.com/fwlink/?LinkId=521402)一節。  
  
3.  **取得要用於 SQL Server 的 Azure Active Directory 服務主體：** 當組織註冊 Microsoft 雲端服務時，它會取得 Azure Active Directory。 建立**服務主體**Azure Active Directory 中的[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]存取金鑰保存庫時使用 （用來向 Azure Active Directory）。  
  
    -   一**服務主體**則需要[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]設定時存取保存庫的系統管理員[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]使用加密。  
  
    -   另一個**服務主體**則需要[!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)]中所使用的解除包裝金鑰保存庫的存取[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]加密。  
  
     如需如何註冊應用程式及產生服務主體的詳細資訊，請參閱 **開始使用 Azure Key Vault** 中的 [使用 Azure Active Directory 註冊應用程式](http://go.microsoft.com/fwlink/?LinkId=521402)一節。 註冊程序會針對每個 Azure Active Directory **服務主體** ，傳回 **應用程式識別碼**(又稱為 **用戶端識別碼** ) 和 **驗證金鑰**(又稱為 **密碼**)。 在中使用時`CREATE CREDENTIAL`陳述式，必須從移除連字號**用戶端識別碼**。 請記錄這些項目，以用於下列指令碼：  
  
    -   **sysadmin** 登入的 **服務主體** ： **CLIENTID_sysadmin_login** 和 **SECRET_sysadmin_login**  
  
    -   **服務主體**for [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)]: **CLIENTID_DBEngine**並**SECRET_DBEngine**。  
  
4.  **授與服務主體存取金鑰保存庫的權限：** 和 **和**  **服務主體** 都需要金鑰保存庫中的 **get**, **list**, **wrapKey**,  **unwrapKey** 權限。 如果您想要建立金鑰，透過[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]您也需要授與**建立**金鑰保存庫中的權限。  
  
    > [!IMPORTANT]  
    >  使用者必須至少具有這個金鑰保存庫的 **wrapKey** 和 **unwrapKey** 作業。  
  
     如需授與保存庫權限的詳細資訊，請參閱 **開始使用 Azure Key Vault**[中的授權應用程式使用金鑰或密碼](http://go.microsoft.com/fwlink/?LinkId=521402)一節。  
  
     Azure Key Vault 文件的連結  
  
    -   [何謂 Azure Key Vault？](http://go.microsoft.com/fwlink/?LinkId=521401)  
  
    -   [開始使用 Azure Key Vault](http://go.microsoft.com/fwlink/?LinkId=521402)  
  
    -   PowerShell [Azure 金鑰保存庫 Cmdlet](http://go.microsoft.com/fwlink/?LinkId=521403) 參考  
  
##  <a name="Step2"></a> 步驟 2： 安裝 SQL Server Connector  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]下載並安裝的系統管理員連接器時[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]電腦。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]連接器可從下載[Microsoft Download Center](http://go.microsoft.com/fwlink/p/?LinkId=521700)。  搜尋 **SQL Server Connector for Microsoft Azure Key Vault**，檢閱詳細資料、系統需求和安裝指示，然後選擇下載連接器並使用 [執行] 開始安裝。 檢閱授權，然後接受授權並繼續。  
  
 按照預設在 **C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault**安裝連接器。 這個位置可以在安裝期間變更。 (如果變更，請調整下列指令碼)。  
  
 完成安裝時，電腦上會安裝下列項目：  
  
-   **Microsoft.AzureKeyVaultService.EKM.dll**： 這是密碼編譯的 EKM 提供者 DLL，需要向[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]使用 CREATE CRYPTOGRAPHIC PROVIDER 陳述式。  
  
-   **Azure Key Vault SQL Server Connector**：這是 Windows 服務，可讓密碼編譯的 EKM 提供者與金鑰保存庫通訊。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]連接器安裝也可讓您選擇性地下載範例指令碼[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]加密。  
  
##  <a name="Step3"></a> 步驟 3： 設定 SQL Server 對金鑰保存庫使用 EKM 提供者  
  
###  <a name="Permissions"></a> 權限  
 若要完成這整個程序，需要 CONTROL SERVER 權限或 **sysadmin** 固定伺服器角色中的成員資格。 特定動作需要下列權限：  
  
-   若要建立密碼編譯提供者，需要 CONTROL SERVER 權限或 **sysadmin** 固定伺服器角色中的成員資格。  
  
-   若要變更組態選項及執行 RECONFIGURE 陳述式，您必須取得 ALTER SETTINGS 伺服器層級的權限。 **系統管理員 (sysadmin)** 及 **serveradmin** 固定伺服器角色會隱含 ALTER SETTINGS 權限。  
  
-   若要建立認證，需要 ALTER ANY CREDENTIAL 權限。  
  
-   若要將認證加入登入，需要 ALTER ANY LOGIN 權限。  
  
-   若要建立非對稱金鑰，需要 CREATE ASYMMETRIC KEY 權限。  
  
###  <a name="TsqlProcedure"></a> 若要設定 SQL Server 使用的密碼編譯提供者  
  
1.  設定 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 使用 EKM，並向 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 註冊 (建立) 密碼編譯提供者。  
  
    ```  
    -- Enable advanced options.  
    USE master;  
    GO  
  
    sp_configure 'show advanced options', 1 ;  
    GO  
    RECONFIGURE ;  
    GO  
    -- Enable EKM provider  
    sp_configure 'EKM provider enabled', 1 ;  
    GO  
    RECONFIGURE ;  
    GO  
  
    -- Create a cryptographic provider, using the SQL Server Connector  
    -- which is an EKM provider for the Azure Key Vault. This example uses   
    -- the name AzureKeyVault_EKM_Prov.  
  
    CREATE CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov   
    FROM FILE = 'C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault\Microsoft.AzureKeyVaultService.EKM.dll';  
    GO   
    ```  
  
2.  安裝程式[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]認證，供[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]若要使用金鑰保存庫，才能設定和管理的系統管理員登入[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]加密案例。  
  
    > [!IMPORTANT]  
    >  **身分識別**引數`CREATE CREDENTIAL`需要金鑰保存庫名稱。 **祕密**引數`CREATE CREDENTIAL`需要*\<用戶端識別碼 >* （不含連字號） 和*\<祕密 >* 傳遞在一起不之間的空格。  
  
     在下列範例中， **用戶端識別碼** (`EF5C8E09-4D2A-4A76-9998-D93440D8115D`) 已移除連字號並以字串 `EF5C8E094D2A4A769998D93440D8115D` 輸入，而 **密碼** 會以字串 *SECRET_sysadmin_login*來表示。  
  
    ```  
    USE master;  
    CREATE CREDENTIAL sysadmin_ekm_cred   
        WITH IDENTITY = 'ContosoKeyVault',   
        SECRET = 'EF5C8E094D2A4A769998D93440D8115DSECRET_sysadmin_login'   
    FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov ;  
  
    -- Add the credential to the SQL Server administrators domain login   
    ALTER LOGIN [<domain>/<login>]  
    ADD CREDENTIAL sysadmin_ekm_cred;  
    ```  
  
     如需範例使用變數`CREATE CREDENTIAL`引數和以程式設計方式從用戶端識別碼移除連字號請參閱[CREATE CREDENTIAL &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/create-credential-transact-sql)。  
  
3.  如果您已如第 3 節步驟 1 所述匯入非對稱金鑰，請在下列範例中提供您的金鑰名稱，以開啟金鑰。  
  
    ```  
    CREATE ASYMMETRIC KEY CONTOSO_KEY   
    FROM PROVIDER [AzureKeyVault_EKM_Prov]  
    WITH PROVIDER_KEY_NAME = 'ContosoMasterKey',  
    CREATION_DISPOSITION = OPEN_EXISTING;  
    ```  
  
     雖然生產環境不建議使用 (因為無法匯出金鑰)，但是您可以從 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 直接在保存庫中建立非對稱金鑰。 如果您之前沒有匯入金鑰，則可以使用下列指令碼，在金鑰保存庫中建立非對稱金鑰進行測試。 使用 **sysadmin_ekm_cred** 認證提供的登入來執行指令碼。  
  
    ```  
    CREATE ASYMMETRIC KEY CONTOSO_KEY   
    FROM PROVIDER [AzureKeyVault_EKM_Prov]  
    WITH ALGORITHM = RSA_2048,  
    PROVIDER_KEY_NAME = 'ContosoMasterKey';  
    ```  
  
> [!TIP]  
>  使用者收到錯誤**無法從提供者匯出公開金鑰。提供者錯誤碼： 2053年。** 應該檢查其金鑰保存庫中的 **get**、 **list**、 **wrapKey**、 and **unwrapKey** 權限。  
  
 如需詳細資訊，請參閱下列內容：  
  
-   [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
-   [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-cryptographic-provider-transact-sql)  
  
-   [CREATE CREDENTIAL &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-credential-transact-sql)  
  
-   [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-asymmetric-key-transact-sql)  
  
-   [CREATE LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-login-transact-sql)  
  
-   [ALTER LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-login-transact-sql)  
  
## <a name="examples"></a>範例  
  
###  <a name="ExampleA"></a> 範例 a： 使用從 Key Vault 的非對稱金鑰的透明資料加密  
 完成上述步驟之後，請建立認證和登入，並建立受到金鑰保存庫中非對稱金鑰保護的資料庫加密金鑰。 請使用資料庫加密金鑰透過 TDE 來加密資料庫。  
  
 若要加密資料庫，需要資料庫的 CONTROL 權限。  
  
##### <a name="to-enable-tde-using-ekm-and-the-key-vault"></a>使用 EKM 和金鑰保存庫啟用 TDE  
  
1.  建立 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 認證，以供 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 在資料庫載入期間用於存取金鑰保存庫 EKM。  
  
    > [!IMPORTANT]  
    >  **身分識別**引數`CREATE CREDENTIAL`需要金鑰保存庫名稱。 **祕密**引數`CREATE CREDENTIAL`需要*\<用戶端識別碼 >* （不含連字號） 和*\<祕密 >* 傳遞在一起不之間的空格。  
  
     在下列範例中， **用戶端識別碼** (`EF5C8E09-4D2A-4A76-9998-D93440D8115D`) 已移除連字號並以字串 `EF5C8E094D2A4A769998D93440D8115D` 輸入，而 **密碼** 會以字串 *SECRET_DBEngine*來表示。  
  
    ```  
    USE master;  
    CREATE CREDENTIAL Azure_EKM_TDE_cred   
        WITH IDENTITY = 'ContosoKeyVault',   
        SECRET = 'EF5C8E094D2A4A769998D93440D8115DSECRET_DBEngine'   
        FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov ;  
    ```  
  
2.  建立 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 要用於 TDE 的 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 登入，然後加入認證。 這個範例使用儲存在金鑰保存庫中的 CONTOSO_KEY 非對稱金鑰，這是稍早針對 master 資料庫匯入或建立的金鑰，如上面的 [第 3 節步驟 3](#Step3) 所述。  
  
    ```  
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
  
3.  建立要用於 TDE 的資料庫加密金鑰 (DEK)。 DEK 可使用 SQL Server 支援的任何演算法或金鑰長度來建立。 DEK 受到金鑰保存庫中非對稱金鑰的保護。  
  
     這個範例使用儲存在金鑰保存庫中的 CONTOSO_KEY 非對稱金鑰，這是稍早匯入或建立的金鑰，如上面的 [第 3 節步驟 3](#Step3) 所述。  
  
    ```  
    USE ContosoDatabase;  
    GO  
  
    CREATE DATABASE ENCRYPTION KEY   
    WITH ALGORITHM = AES_128   
    ENCRYPTION BY SERVER ASYMMETRIC KEY CONTOSO_KEY;  
    GO  
  
    -- Alter the database to enable transparent data encryption.  
    ALTER DATABASE ContosoDatabase   
    SET ENCRYPTION ON ;  
    GO  
    ```  
  
     如需詳細資訊，請參閱下列內容：  
  
    -   [CREATE DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-database-encryption-key-transact-sql)  
  
    -   [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)  
  
###  <a name="ExampleB"></a> 範例 b： 使用從 Key Vault 的非對稱金鑰來加密備份  
 自 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]開始，支援加密備份。 下列範例如何建立及還原以資料加密金鑰加密的備份，這個資料加密金鑰受到金鑰保存庫中非對稱金鑰的保護。  
  
```  
USE master;  
BACKUP DATABASE [DATABASE_TO_BACKUP]  
TO DISK = N'[PATH TO BACKUP FILE]'   
WITH FORMAT, INIT, SKIP, NOREWIND, NOUNLOAD,   
ENCRYPTION(ALGORITHM = AES_256, SERVER ASYMMETRIC KEY = [CONTOSO_KEY]);  
GO  
```  
  
 範例還原程式碼。  
  
```  
RESTORE DATABASE [DATABASE_TO_BACKUP]  
FROM DISK = N'[PATH TO BACKUP FILE]' WITH FILE = 1, NOUNLOAD, REPLACE;  
GO  
```  
  
 如需備份選項的詳細資訊，請參閱[備份&#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)。  
  
###  <a name="ExampleC"></a> 範例 c： 使用資料行層級加密的金鑰保存庫的非對稱金鑰  
 下列範例會建立受到金鑰保存庫中非對稱金鑰保護的對稱金鑰。 然後使用對稱金鑰加密資料庫中的資料。  
  
 這個範例使用儲存在金鑰保存庫中的 CONTOSO_KEY 非對稱金鑰，這是稍早匯入或建立的金鑰，如上面的 [第 3 節步驟 3](#Step3) 所述。 若要在 `ContosoDatabase` 資料庫中使用這個非對稱金鑰，您必須再執行一次 CREATE ASYMMETRIC KEY 陳述式，以提供參考這個金鑰的 `ContosoDatabase` 資料庫。  
  
```  
USE [ContosoDatabase];  
GO  
  
-- Create a reference to the key in the key vault  
CREATE ASYMMETRIC KEY CONTOSO_KEY   
FROM PROVIDER [AzureKeyVault_EKM_Prov]  
WITH PROVIDER_KEY_NAME = 'ContosoMasterKey',  
CREATION_DISPOSITION = OPEN_EXISTING;  
  
-- Create the data encryption key.  
-- The data encryption key can be created using any SQL Server   
-- supported algorithm or key length.  
-- The DEK will be protected by the asymmetric key in the key vault  
  
CREATE SYMMETRIC KEY DATA_ENCRYPTION_KEY  
    WITH ALGORITHM=AES_256  
    ENCRYPTION BY ASYMMETRIC KEY CONTOSO_KEY;  
  
DECLARE @DATA VARBINARY(MAX);  
  
--Open the symmetric key for use in this session  
OPEN SYMMETRIC KEY DATA_ENCRYPTION_KEY   
DECRYPTION BY ASYMMETRIC KEY CONTOSO_KEY;  
  
--Encrypt syntax  
SELECT @DATA = ENCRYPTBYKEY(KEY_GUID('DATA_ENCRYPTION_KEY'), CONVERT(VARBINARY,'Plain text data to encrypt'));  
  
-- Decrypt syntax  
SELECT CONVERT(VARCHAR, DECRYPTBYKEY(@DATA));  
  
--Close the symmetric key  
CLOSE SYMMETRIC KEY DATA_ENCRYPTION_KEY;  
```  
  
## <a name="see-also"></a>另請參閱  
 [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-cryptographic-provider-transact-sql)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-credential-transact-sql)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-asymmetric-key-transact-sql)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-symmetric-key-transact-sql)   
 [可延伸金鑰管理 &#40;EKM&#41;](extensible-key-management-ekm.md)   
 [使用 EKM 啟用 TDE](enable-tde-on-sql-server-using-ekm.md)   
 [備份加密](../../backup-restore/backup-encryption.md)   
 [建立加密的備份](../../backup-restore/create-an-encrypted-backup.md)  
  
  
