---
title: 使用 Azure 金鑰保存庫進行可延伸金鑰管理的設定步驟 | Microsoft 文件
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: security
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- EKM, with key vault setup
- SQL Server Connector, setup
- SQL Server Connector
ms.assetid: c1f29c27-5168-48cb-b649-7029e4816906
caps.latest.revision: 34
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 563bf6957d123ac718222a53faf33ea10b2398bb
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="setup-steps-for-extensible-key-management-using-the-azure-key-vault"></a>使用 Azure 金鑰保存庫進行可延伸金鑰管理的設定步驟
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  下列步驟會逐步解說適用於 Microsoft Azure 金鑰保存庫之 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 連接器的安裝和組態。  
  
## <a name="before-you-start"></a>開始之前  
 若要搭配使用 Azure 金鑰保存庫與 SQL Server，有幾個先決條件︰  
  
-   您必須擁有 Azure 訂用帳戶  
  
-   安裝最新 [Azure PowerShell](https://azure.microsoft.com/en-us/documentation/articles/powershell-install-configure/) (1.0.1 或更高版本)。  

-   建立 Azure Active Directory  

-   檢閱[使用 Azure 金鑰保存庫進行可延伸金鑰管理 &#40;SQL Server&#41;](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)，以熟悉使用 Azure 金鑰保存庫的 EKM 儲存體主體。  

-   已根據所執行之 SQL Server 版本安裝正確版本的 Visual Studio C++ 可轉散發套件：
  
SQL Server 版本  |可轉散發套件的安裝連結    
---------|--------- 
2008、2008 R2、2012、2014 | [適用於 Visual Studio 2013 的 Visual C++ 可轉散發套件](https://www.microsoft.com/download/details.aspx?id=40784)    
2016 | [適用於 Visual Studio 2015 的 Visual C++ 可轉散發套件](https://www.microsoft.com/download/details.aspx?id=48145)    
 
  
## <a name="part-i-set-up-an-azure-active-directory-service-principal"></a>第 I 部分：設定 Azure Active Directory 服務主體  
 若要將 SQL Server 存取權限授與 Azure 金鑰保存庫，您需要 Azure Active Directory (AAD) 中的服務主體帳戶。  
  
1.  移至 [Azure 傳統入口網站](https://manage.windowsazure.com)，並登入。  
  
2.  向 Azure Active Directory 註冊應用程式。 如需註冊應用程式的詳細逐步指示，請參閱 [Azure Key Vault](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step/) (Azure 金鑰保存庫) 部落格文章的＜Get an identity for the application＞(取得應用程式的識別) 一節。  
  
3.  複製 **用戶端識別碼** 和 **用戶端機密** 以供後面的步驟使用；在其中，它們將用來授與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 對您金鑰保存庫的存取。  
  
 ![EKM 用戶端識別碼](../../../relational-databases/security/encryption/media/ekm-client-id.png "EKM 用戶端識別碼")  
  
 ![EKM 金鑰識別碼](../../../relational-databases/security/encryption/media/ekm-key-id.png "EKM 金鑰識別碼")  
  
## <a name="part-ii-create-a-key-vault-and-key"></a>第 II 部分︰建立金鑰保存庫和金鑰  
 SQL Server Database Engine 將使用此處所建立的金鑰保存庫和金鑰來進行加密金鑰保護。  
  
> [!IMPORTANT]  
>  建立金鑰保存庫的訂用帳戶所在的預設 Azure Active Directory，必須與建立 Azure Active Directory 服務主體的預設 Azure Active Directory 相同。 如果您想要使用非預設 Active Directory 的 Active Directory 建立 SQL Server 連接器的服務主體，您必須在 Azure 帳戶中變更預設 Active Directory，然後再建立金鑰保存庫。 若要了解如何將預設 Active Directory 變更為您想要使用的 Active Directory，請參閱 SQL Server 連接器 [常見問題集](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md#AppendixB)。  
  
1.  **開啟 PowerShell 並登入**  
  
     安裝並啟動 [最新 Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) (1.0.1 或更高版本)。 使用下列命令登入您的 Azure 帳戶︰  
  
    ```powershell  
    Login-AzureRmAccount  
    ```  
  
     此陳述式會傳回：  
  
    ```  
    Environment           : AzureCloud  
    Account               : <account_name>  
    TenantId              : <tenant_id>  
    SubscriptionId        : <subscription_id>  
    CurrentStorageAccount :  
    ```  
  
    > [!NOTE]  
    >  如果您擁有多個訂用帳戶，並想要指定特定的訂用帳戶來使用保存庫，請使用 `Get-AzureRmSubscription` 來查看訂用帳戶，並使用 `Select-AzureRmSubscription` 來選擇正確的訂用帳戶。 否則，PowerShell 預設會為您選取一個訂用帳戶。  
  
2.  **建立新的資源群組**  
  
     所有透過 Azure Resource Manager 建立的 Azure 資源都必須包含在資源群組中。 建立資源群組來包含您的金鑰保存庫。 此範例會使用 `ContosoDevRG`。 請自行選擇 **唯一的** 資源群組和金鑰保存庫名稱，因為所有金鑰保存庫名稱都是全域唯一的。  
  
    ```powershell  
    New-AzureRmResourceGroup -Name ContosoDevRG -Location 'East Asia'  
    ```  
  
     此陳述式會傳回：  
  
    ```  
    ResourceGroupName: ContosoDevRG  
    Location         : eastasia  
    ProvisioningState: Succeeded  
    Tags             :   
    ResourceId       : /subscriptions/<subscription_id>/  
                        resourceGroups/ContosoDevRG  
    ```  
  
    > [!NOTE]  
    >  針對 `-Location parameter`，請使用命令 `Get-AzureLocation` 以識別將這個範例中的位置指定至替代位置的方法。 如需詳細資訊，請輸入： `Get-Help Get-AzureLocation`  
  
3.  **建立金鑰保存庫**  
  
     `New-AzureRmKeyVault` Cmdlet 需要資源群組名稱、金鑰保存庫名稱和地理位置。 例如，針對名為 `ContosoDevKeyVault`的金鑰保存庫，輸入：  
  
    ```powershell  
    New-AzureRmKeyVault -VaultName 'ContosoDevKeyVault' `  
       -ResourceGroupName 'ContosoDevRG' -Location 'East Asia'  
    ```  
  
     記錄金鑰保存庫的名稱。  
  
     此陳述式會傳回：  
  
    ```  
    Vault Name                       : ContosoDevKeyVault  
    Resource Group Name              : ContosoDevRG  
    Location                         : East Asia  
    ResourceId                       : /subscriptions/<subscription_id>/  
                                        resourceGroups/ContosoDevRG/providers/  
                                        Microsoft/KeyVault/vaults/ContosoDevKeyVault  
    Vault URI: https://ContosoDevKeyVault.vault.azure.net  
    Tenant ID                        : <tenant_id>  
    SKU                              : Standard  
    Enabled For Deployment?          : False  
    Enabled For Template Deployment? : False  
    Enabled For Disk Encryption?     : False  
    Access Policies                  :  
             Tenant ID              : <tenant_id>  
             Object ID              : <object_id>  
             Application ID         :   
             Display Name           : <display_name>  
             Permissions to Keys    : get, create, delete, list, update, import,   
                                      backup, restore  
             Permissions to Secrets : all  
    Tags                             :  
    ```  
  
4.  **授與 Azure Active Directory 服務主體存取金鑰保存庫的權限**  
  
     您可以授權其他使用者和應用程式使用金鑰保存庫。   
    在此情況下，請讓我們使用第 I 部分中所建立的 Azure Active Directory 服務主體來授權 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體。  
  
    > [!IMPORTANT]  
    >  Azure Active Directory 服務主體必須具有至少金鑰保存庫的 `get`、 `list`、 `wrapKey`和 `unwrapKey` 權限。  
  
     如下所示，針對 **參數，使用第 I 部分中的** 用戶端識別碼 `ServicePrincipalName` 。 `Set-AzureRmKeyVaultAccessPolicy` 順利執行時，會以沒有輸出的無訊息模式執行。  
  
    ```powershell  
    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoDevKeyVault'`  
      -ServicePrincipalName EF5C8E09-4D2A-4A76-9998-D93440D8115D `  
      -PermissionsToKeys get, list, wrapKey, unwrapKey  
    ```  
  
     呼叫 `Get-AzureRmKeyVault` Cmdlet 來確認權限。 在 [存取原則] 的陳述式輸出中，您應該會看到您的 AAD 應用程式名稱列出有權存取此金鑰保存庫的另一個租用戶。  
  
       
5.  **在金鑰保存庫中產生非對稱金鑰**  
  
     有兩種方式可以在 Azure 金鑰保存庫中產生金鑰︰1) 匯入現有的金鑰，或 2) 建立新的金鑰。  

    ### <a name="best-practice"></a>最佳做法：
    
    若要確保快速修復金鑰，並且能夠在 Azure 之外存取資料，我們建議下列最佳作法︰
 
    1. 在本機 HSM 裝置上，本機建立加密金鑰。 (請確定這是對稱的 RSA 2048 金鑰，以便它可存放在 Azure 金鑰保存庫中。)
    2. 將加密金鑰匯入至 Azure 金鑰保存庫。 請參閱下面步驟以了解如何做到。
    3. 第一次使用 Azure 金鑰保存庫中的金鑰之前，請先備份 Azure 金鑰保存庫金鑰。 深入了解 [Backup-AzureKeyVaultKey](https://msdn.microsoft.com/library/mt126292.aspx) 命令。
    4. 每當對金鑰進行任何變更 (例如新增 ACL、新增標籤、新增金鑰屬性)，請務必先另行備份 Azure 金鑰保存庫金鑰。

        > [!NOTE]  
        >  備份金鑰是 Azure 金鑰保存庫金鑰作業，它會傳回可儲存在任何位置的檔案。

    ### <a name="types-of-keys"></a>金鑰的類型︰
    您可以在 Azure 金鑰保存庫中產生兩種類型的金鑰。 兩者都是非對稱 2048 位元 RSA 金鑰。  
  
    -   **受軟體保護** ：在軟體中處理，並在靜止時加密。 受軟體保護金鑰上的作業發生於 Azure 虛擬機器。 建議用於未在生產環境部署中使用的金鑰。  
  
    -   **受 HSM 保護** ：由硬體安全模組 (HSM) 所建立和保護，以提供額外安全性。 一個金鑰版本的成本大約美金 $1 元。  
  
        > [!IMPORTANT]  
        >  SQL Server 連接器需要金鑰名稱僅使用字元 “a-z”、“A-Z”、“0-9” 和 “-“，且長度限制為 26 個字元。   
        > Azure 金鑰保存庫中金鑰名稱相同的不同金鑰版本，將不會與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 連接器搭配運作。 若要更換 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]正在使用的 Azure 金鑰保存庫金鑰，請參閱 [SQL Server 連接器維護和疑難排解](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md)，以熟悉使用 Azure 金鑰保存庫的 EKM 儲存體主體。  

    ### <a name="import-an-existing-key"></a>匯入現有的金鑰   
  
    如果您有現有 2048 位元 RSA 受軟體保護金鑰，則可以將金鑰上傳至 Azure 金鑰保存庫。 或者，如果您的 `C:\\` 磁碟機中已儲存一個 .PFX 檔案 (名為 `softkey.pfx` )，並想要將它上傳到 Azure 金鑰保存庫，請輸入下列內容，將 .PFX 檔案的 `securepfxpwd` 變數設定為密碼 `12987553` ：  
  
    ``` powershell  
    $securepfxpwd = ConvertTo-SecureString –String '12987553' `  
      –AsPlainText –Force  
    ```  
  
    然後您可以輸入下列內容以匯入來自 .PFX 檔案的金鑰，該檔案是透過金鑰保存庫服務中的硬體 (建議選項) 來保護該金鑰︰  
  
    ``` powershell  
        Add-AzureKeyVaultKey -VaultName 'ContosoKeyVault' `  
          -Name 'ContosoFirstKey' -KeyFilePath 'c:\softkey.pfx' `  
          -KeyFilePassword $securepfxpwd $securepfxpwd  -Destination 'HSM'  
    ```  
 
    > [!IMPORTANT]  
    > 強烈建議在生產案例中匯入非對稱金鑰，因為這樣做可讓系統管理員在金鑰委付系統中委付金鑰。 如果非對稱金鑰是在保存庫中建立，由於私密金鑰永遠不會離開保存庫，因此無法委付金鑰。 您應該委付用來保護重要資料的金鑰。 遺失非對稱金鑰會導致資料永久無法復原。  

    ### <a name="create-a-new-key"></a>建立新的金鑰

    ##### <a name="example"></a>範例  
    如果您想要，可以直接在 Azure 金鑰保存庫中建立新的加密金鑰，並以軟體或 HSM 保護它。 在此範例中，我們會使用 `Add-AzureKeyVaultKey cmdlet`建立受軟體保護金鑰：  

    ``` powershell  
    Add-AzureKeyVaultKey -VaultName 'ContosoDevKeyVault' `  
      -Name 'ContosoRSAKey0' -Destination 'Software'  
    ```  
  
    此陳述式會傳回：  
  
    ```  
    Attributes : Microsoft.Azure.Commands.KeyVault.Models.KeyAttributes  
    Key        :  {"kid":"https:contosodevKeyVault.azure.net/keys/  
                   ContosoRSAKey0/<guid>","dty":"RSA:,"key_ops": ...  
    VaultName  : contosodevkeyvault  
    Name       : contosoRSAKey0  
    Version    : <guid>  
    Id         : https://contosodevkeyvault.vault.azure.net:443/  
                 keys/ContosoRSAKey0/<guid>  
    ```  

    > [!IMPORTANT]  
    >  金鑰保存庫支援多種版本的同名金鑰，但不應該復原 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 連接器所使用的金鑰或建立其版本。 如果系統管理員想要復原 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 加密所使用的金鑰，應該在保存庫中建立不同名稱的新金鑰，用來加密 DEK。  
   
  
## <a name="part-iii-install-the-includessnoversionincludesssnoversion-mdmd-connector"></a>第 III 部分：安裝 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 連接器  
 從 [Microsoft 下載中心](http://go.microsoft.com/fwlink/p/?LinkId=521700)下載 SQL Server 連接器。 (這應該由 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 電腦的系統管理員所完成)。  

> [!NOTE]  
>  1.0.0.440 版和較舊版本皆已被取代，而且生產環境也不再支援。 請前往 [Microsoft 下載中心](https://www.microsoft.com/download/details.aspx?id=45344) ，使用 [SQL Server 連接器維護和疑難排解](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md) 頁面之＜SQL Server 連接器的升級＞下的指示，升級為 1.0.1.0 版或更新版本。
  
 ![EKM 連接器安裝](../../../relational-databases/security/encryption/media/ekm-connector-install.png "EKM 連接器安裝")  
  
 連接器預設會安裝在 C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault。 這個位置可以在安裝期間變更。 (如果變更，請調整下列指令碼)。  
  
 連接器沒有介面，但如果安裝成功，電腦上會安裝 **Microsoft.AzureKeyVaultService.EKM.dll** 。 這是密碼編譯的 EKM 提供者 DLL，需要使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 陳述式向 `CREATE CRYPTOGRAPHIC PROVIDER` 註冊。  
  
 SQL Server 連接器安裝也可讓您選擇性地下載 SQL Server 加密的範例指令碼。  
  
 若要檢視 SQL Server Connector 的錯誤碼說明、組態設定或維護工作，請瀏覽位於這個主題底部的附錄︰  
  
-   [A.SQL Server Connector 的維護指示](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md#AppendixA)  
  
-   [C.SQL Server Connector 的錯誤碼說明](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md#AppendixC)  
  
  
## <a name="part-iv-configure-includessnoversionincludesssnoversion-mdmd"></a>第 IV 部分：設定 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
 請參閱 [B. 常見問題集](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md#AppendixB) ，以查看本節中每個動作所需最小權限等級的附註。  
  
1.  **啟動 sqlcmd.exe 或 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Studio**  
  
2.  **設定 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 使用 EKM**  
  
     執行下列 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 指令碼，設定 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 使用 EKM 提供者。  
  
    ```sql  
    -- Enable advanced options.  
    USE master;  
    GO  
  
    sp_configure 'show advanced options', 1;  
    GO  
    RECONFIGURE;  
    GO  
  
    -- Enable EKM provider  
    sp_configure 'EKM provider enabled', 1;  
    GO  
    RECONFIGURE;  
    ```  
  
3.  **使用下列項目來註冊 (建立) [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 連接器作為 EKM 提供者： [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]**  
  
     -- 使用本身為 Azure 金鑰保存庫之 EKM 提供者的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 連接器，建立密碼編譯提供者。    
    此範例使用名稱 `AzureKeyVault_EKM_Prov`。  
  
    ```sql  
    CREATE CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov   
    FROM FILE = 'C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault\Microsoft.AzureKeyVaultService.EKM.dll';  
    GO  
    ```  
  
    > [!NOTE]  
    >  檔案路徑長度不能超過 256 個字元。  
  
  
4.  **設定 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登入的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 認證使用金鑰保存庫**  
  
     必須將認證新增至每個將使用金鑰保存庫之金鑰執行加密的登入。 這可能包括：  
  
    -   使用金鑰保存庫才能設定和管理 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 加密案例的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 系統管理員登入。  
  
    -   可以啟用透明資料加密 (TDE) 或其他 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 加密功能的其他 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登入。  
  
     認證與登入之間的一對一對應。 也就是說，每個登入都必須具有唯一的認證。  
  
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
    CREATE CREDENTIAL sysadmin_ekm_cred   
        WITH IDENTITY = 'ContosoDevKeyVault', -- for public Azure
        -- WITH IDENTITY = 'ContosoDevKeyVault.vault.usgovcloudapi.net', -- for Azure Government
        -- WITH IDENTITY = 'ContosoDevKeyVault.vault.azure.cn', -- for Azure China
        -- WITH IDENTITY = 'ContosoDevKeyVault.vault.microsoftazure.de', -- for Azure Germany   
        SECRET = 'EF5C8E094D2A4A769998D93440D8115DReplace-With-AAD-Client-Secret'   
    FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov;  
  
    -- Add the credential to the SQL Server administrator's domain login   
    ALTER LOGIN [<domain>\<login>]  
    ADD CREDENTIAL sysadmin_ekm_cred;  
    ```  
  
     如需針對 **CREATE CREDENTIAL** 引數使用變數及以程式設計方式從用戶端識別碼移除連字號的範例，請參閱 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-credential-transact-sql.md)。  
  
5.  **開啟 Azure 金鑰保存庫金鑰於 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]**  
  
     如果您已如第 II 部分所述匯入非對稱金鑰，請在下列 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 指令碼中提供您的金鑰名稱來開啟金鑰。  
  
    -   將 `CONTOSO_KEY` 取代為 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中您想要的金鑰名稱。  
  
    -   將 `ContosoRSAKey0` 取代為 Azure 金鑰保存庫中您金鑰的名稱。  
  
    ```sql  
    CREATE ASYMMETRIC KEY CONTOSO_KEY   
    FROM PROVIDER [AzureKeyVault_EKM_Prov]  
    WITH PROVIDER_KEY_NAME = 'ContosoRSAKey0',  
    CREATION_DISPOSITION = OPEN_EXISTING;  
    ```  
## <a name="next-step"></a>下一個步驟  
  
現在您已完成基本組態，請參閱如何 [搭配使用 SQL Server 連接器與 SQL 加密功能](../../../relational-databases/security/encryption/use-sql-server-connector-with-sql-encryption-features.md)   
  
## <a name="see-also"></a>另請參閱  
 [使用 Azure Key Vault 進行可延伸金鑰管理](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)   
[SQL Server 連接器維護和疑難排解](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md)  
  
  
