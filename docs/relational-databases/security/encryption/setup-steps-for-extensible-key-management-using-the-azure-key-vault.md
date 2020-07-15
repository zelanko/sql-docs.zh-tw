---
title: 使用 Azure Key Vault 設定透明資料加密 (TDE) 可延伸金鑰管理
description: 安裝及設定適用於 Azure Key Vault 的 SQL Server 連接器。
ms.custom: seo-lt-2019
ms.date: 06/15/2020
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Extensible Key Management
- EKM, with key vault setup
- SQL Server Connector, setup
- SQL Server Connector
ms.assetid: c1f29c27-5168-48cb-b649-7029e4816906
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: f0be0697b0820b2d134e69742a7ffc50048b94e7
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85883048"
---
# <a name="set-up-sql-server-tde-extensible-key-management-by-using-azure-key-vault"></a>使用 Azure Key Vault 設定 SQL Server TDE 可延伸金鑰管理
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

在本文中，您將安裝及設定適用於 Azure Key Vault 的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 連接器。  
  
## <a name="prerequisites"></a>必要條件

在開始搭配 SQL Server 執行個體使用 Azure Key Vault 前，請確認已符合下列必要條件：  
  
- 您必須擁有 Azure 訂用帳戶。
  
- 安裝 [Azure PowerShell 5.2.0 或更新版本](https://azure.microsoft.com/documentation/articles/powershell-install-configure/)。  

- 建立 Azure Active Directory (Azure AD) 執行個體。

- 檢閱[具備 Azure Key Vault (SQL Server) 的 EKM](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)，以熟悉使用 Azure Key Vault 的可延伸金鑰管理 (EKM) 儲存體主體。  

- 根據正在執行的 SQL Server 版本安裝 Visual Studio C++ 可轉散發套件版本：
  
  SQL Server 版本  | Visual Studio C++ 可轉散發套件版本    
  ---------|--------- 
  2008、2008 R2、2012、2014 | [適用於 Visual Studio 2013 的 Visual C++ 可轉散發套件](https://www.microsoft.com/download/details.aspx?id=40784)    
  2016 | [適用於 Visual Studio 2015 的 Visual C++ 可轉散發套件](https://www.microsoft.com/download/details.aspx?id=48145)    
 
  
## <a name="step-1-set-up-an-azure-ad-service-principal"></a>步驟 1:設定 Azure AD 服務主體

若要將 SQL Server 執行個體存取權限授與 Azure 金鑰保存庫，則需要 Azure AD 中的服務主體帳戶。  
  
1.  登入 [Azure 入口網站](https://ms.portal.azure.com/)並執行下列任一步驟：

    * 選取 [Azure Active Directory] 按鈕。

      ![[Azure 服務] 窗格的螢幕擷取畫面](../../../relational-databases/security/encryption/media/ekm/ekm-part1-login-portal.png)

    * 選取 [更多服務]，然後在 [所有服務] 方塊中鍵入 **Azure Active Directory**。

      ![[所有 Azure 服務] 窗格的螢幕擷取畫面](../../../relational-databases/security/encryption/media/ekm/ekm-part1-select-aad.png)  

1. 執行下列動作，向 Azure Active Directory 註冊應用程式。 (如需詳細逐步指示，請參閱 [Azure Key Vault 部落格文章](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step/)的 "Get an identity for the application" 一節。)

    a. 在 [Azure Active Directory 概觀] 窗格中，選取 [應用程式註冊]。 

    ![[Azure Active Directory 概觀] 窗格的螢幕擷取畫面](../../../relational-databases/security/encryption/media/ekm/ekm-part1-aad-app-register.png)

    b. 在 [應用程式註冊] 窗格上，選取 [新增註冊]。

    ![[應用程式註冊] 窗格的螢幕擷取畫面](../../../relational-databases/security/encryption/media/ekm/ekm-part1-aad-new-registration.png)  

    c. 在 [註冊應用程式] 窗格中，輸入應用程式的使用者對應名稱，然後選取 [註冊]。

    ![[註冊應用程式] 窗格的螢幕擷取畫面](../../../relational-databases/security/encryption/media/ekm/ekm-part1-aad-register.png)

    d. 從左側窗格中，選取 [憑證和祕密]，然後選取 [新增用戶端密碼]。

    ![[憑證和祕密] 窗格的螢幕擷取畫面](../../../relational-databases/security/encryption/media/ekm/ekm-part1-aad-certs-secrets.png)  

    e. 在 [新增用戶端密碼] 中輸入描述和適當的到期日，然後選取 [新增]。

    ![[新增用戶端密碼] 區段的螢幕擷取畫面](../../../relational-databases/security/encryption/media/ekm/ekm-part1-aad-add-secret.png)  

    f. 在 [憑證和祕密] 窗格的 [值] 下方，選取用戶端密碼值旁的 [複製] 按鈕，以用於在 SQL Server 中建立非對稱金鑰。

    ![[憑證和祕密] 窗格的螢幕擷取畫面](../../../relational-databases/security/encryption/media/ekm/ekm-part1-aad-new-secret.png)  

    g. 在左窗格中選取 [概觀]，然後在 [應用程式 (用戶端) 識別碼] 方塊中，複製要用來在 SQL Server 中建立非對稱金鑰的值。

    ![[概觀] 窗格上 [應用程式 (用戶端) 識別碼] 值的螢幕擷取畫面](../../../relational-databases/security/encryption/media/ekm/ekm-part1-aad-appid.png)  

## <a name="step-2-create-a-key-vault"></a>步驟 2:建立金鑰保存庫

選取要用來建立金鑰保存庫的方法。

## <a name="azure-portal"></a>[Azure 入口網站](#tab/portal)

### <a name="create-a-key-vault-by-using-the-azure-portal"></a>使用 Azure 入口網站來建立金鑰保存庫 

您可使用 Azure 入口網站來建立金鑰保存庫，並在其中新增 Azure AD 主體。

1. 建立資源群組。

   您透過 Azure 入口網站所建立所有 Azure 資源都必須包含在可建立用來存放金鑰保存庫的資源群組中。 在此範例中，資源名稱是 *ContosoDevRG*。 請自行選擇資源群組和金鑰保存庫名稱，因為所有金鑰保存庫名稱都是全域唯一的。

   在 [建立資源群組] 窗格的 [專案詳細資料] 下方輸入值，然後選取 [檢閱 + 建立]。
      
      ![[建立資源群組] 窗格的螢幕擷取畫面](../../../relational-databases/security/encryption/media/ekm/ekm-part2-create-resource-group.png)  

1.  建立金鑰保存庫。

    在 [建立金鑰保存庫] 窗格上，選取 [基本] 索引標籤並輸入適當的值，然後選取 [檢閱 + 建立]。

    ![[建立金鑰保存庫] 窗格的螢幕擷取畫面](../../../relational-databases/security/encryption/media/ekm/ekm-part2-create-key-vault.png)  

1.  在 [存取原則] 窗格上，選取 [新增存取原則]。

    ![[存取原則] 窗格上 [新增存取原則] 連結的螢幕擷取畫面](../../../relational-databases/security/encryption/media/ekm/ekm-part2-add-access-policy.png)  

1.  在 [新增存取原則] 窗格上執行下列動作：
  
    a. 在 [從範本設定 (選用)] 下拉式清單中，選取 [金鑰管理]。
    
    b. 在左窗格中，選取 [金鑰權限] 索引標籤，然後確認已選取 [取得]、[列出]、[解除包裝金鑰] 和 [包裝金鑰] 核取方塊。

    c. 選取 [新增]。
   
    ![[新增存取原則] 窗格的螢幕擷取畫面](../../../relational-databases/security/encryption/media/ekm/ekm-part2-access-policy-permission.png)

1.  在左窗格中，選取 [選取主體] 索引標籤，然後執行下列動作：

    a. 在 [主體] 窗格的 [選取] 下方，開始鍵入 Azure AD 應用程式的名稱，然後在結果清單中選取想要新增的應用程式。

    ![[主體] 窗格上應用程式搜尋方塊的螢幕擷取畫面](../../../relational-databases/security/encryption/media/ekm/ekm-part2-select-principal.png)  

    b. 選取 [選取] 按鈕，將主體新增至金鑰保存庫。

    ![[主體] 窗格上 [選取] 按鈕的螢幕擷取畫面](../../../relational-databases/security/encryption/media/ekm/ekm-part2-save-principal.png)

    c. 在左下方，選取 [新增] 以儲存變更。

    ![[新增存取原則] 窗格上 [新增] 按鈕的螢幕擷取畫面](../../../relational-databases/security/encryption/media/ekm/ekm-part2-add-principal.png)
 
1. 在 [存取原則] 窗格上選取 [儲存]。
   
   ![[新增存取原則] 窗格上 [儲存] 按鈕的螢幕擷取畫面](../../../relational-databases/security/encryption/media/ekm/ekm-part2-save-access-policy.png)  
 
## <a name="powershell"></a>[PowerShell](#tab/powershell)

### <a name="create-a-key-vault-and-key-by-using-powershell"></a>使用 PowerShell 建立金鑰保存庫和金鑰

SQL Server Database Engine 將使用在此處建立的金鑰保存庫和金鑰來進行加密金鑰保護。  
  
> [!IMPORTANT] 
> 建立金鑰保存庫的訂用帳戶所在預設 Azure AD 執行個體，必須與建立 Azure AD 服務主體的預設 Azure AD 執行個體相同。 如果想要使用並非預設執行個體的 Azure AD 執行個體來建立 SQL Server 連接器服務主體，則必須在 Azure 帳戶中變更預設 Azure AD 執行個體才能建立金鑰保存庫。 若要了解如何將預設 Azure AD 執行個體變更為想要使用的執行個體，請參閱 [SQL Server 連接器維護和疑難排解](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md#AppendixB)的＜常見問題集＞一節。  
  
  
1.  使用下列命令來安裝並登入 [Azure PowerShell 5.2.0 或更新版本](https://azure.microsoft.com/documentation/articles/powershell-install-configure/)：  
  
    ```powershell  
    Connect-AzAccount  
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
    > 如果擁有多個訂用帳戶，並想要指定一個訂用帳戶來使用保存庫，請執行 `Get-AzSubscription` 來檢視訂用帳戶，並使用 `Select-AzSubscription` 來選擇正確的訂用帳戶。 否則，PowerShell 預設會為您選取一個訂用帳戶。  
  
1.  建立資源群組。   

    您透過 PowerShell 建立的所有 Azure 資源，都必須包含在可建立用來存放金鑰保存庫的資源群組中。 在此範例中，資源名稱是 *ContosoDevRG*。 請自行選擇資源群組和金鑰保存庫名稱，因為所有金鑰保存庫名稱都是全域唯一的。  
  
    ```powershell  
    New-AzResourceGroup -Name ContosoDevRG -Location 'East Asia'  
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
    > 針對 `-Location` 參數，請使用命令 `Get-AzureLocation` 以了解如何指定此範例中位置以外的位置。 如果需要詳細資訊，請鍵入 **Get-Help Get-AzureLocation**。  
  
1.  建立金鑰保存庫。    

    `New-AzKeyVault` Cmdlet 需要資源群組名稱、金鑰保存庫名稱和地理位置。 例如，針對名為 `ContosoEKMKeyVault` 的金鑰保存庫，請執行：  
  
    ```powershell  
    New-AzKeyVault -VaultName 'ContosoEKMKeyVault' `  
       -ResourceGroupName 'ContosoDevRG' -Location 'East Asia'  
    ```  
  
    記錄金鑰保存庫的名稱。  
  
    此陳述式會傳回：

    ```  
    Vault Name                       : ContosoEKMKeyVault  
    Resource Group Name              : ContosoDevRG  
    Location                         : East Asia  
    ResourceId                       : /subscriptions/<subscription_id>/  
                                        resourceGroups/ContosoDevRG/providers/  
                                        Microsoft/KeyVault/vaults/ContosoEKMKeyVault  
    Vault URI: https://ContosoEKMKeyVault.vault.azure.net  
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
  
1.  授與 Azure AD 服務主體存取 Azure 金鑰保存庫的權限。  
  
    您可以授權其他使用者和應用程式使用金鑰保存庫。  在範例中，我們將使用在[步驟 1：設定 Azure AD 服務主體](#step-1-set-up-an-azure-ad-service-principal)中建立的服務主體來授權 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體。  
  
    > [!IMPORTANT] 
    > Azure AD 服務主體必須至少具有金鑰保存庫 [取得]、[列出]、[包裝金鑰] 和 [解除包裝金鑰] 的權限。  
  
    如下列命令所示，您可將**應用程式 (用戶端) 識別碼** ([步驟 1：設定 Azure AD 服務主體](#step-1-set-up-an-azure-ad-service-principal)) 用於 `ServicePrincipalName` 參數。 `Set-AzKeyVaultAccessPolicy` 順利執行時，會以沒有輸出的無訊息模式執行。  
  
    ```powershell  
    Set-AzKeyVaultAccessPolicy -VaultName 'ContosoEKMKeyVault' `  
      -ServicePrincipalName 9A57CBC5-4C4C-40E2-B517-EA677 `  
      -PermissionsToKeys get, list, wrapKey, unwrapKey  
    ```  
  
    呼叫 `Get-AzKeyVault` Cmdlet 來確認權限。 在 `Access Policies` 的陳述式輸出中，您應該會看到 Azure AD 應用程式名稱列為有權存取此金鑰保存庫的另一個租用戶。  
  
       
1.  在金鑰保存庫中產生非對稱金鑰。 您可使用兩種方式的其中一種來執行此動作：匯入現有金鑰或建立新的金鑰。  
                  
     > [!NOTE] 
     > SQL Server 僅支援 2048 位元的 RSA 金鑰。
        
### <a name="best-practices"></a>最佳作法
    
若要確保快速修復金鑰，且能夠在 Azure 之外存取資料，建議採用下列最佳做法︰
 
- 在本機硬體安全模組 (HSM) 裝置上建立加密金鑰。 請確認使用對稱的 RSA 2048 金鑰，以支援 SQL Server。
- 將加密金鑰匯入至 Azure 金鑰保存庫。 下一節將描述這個程序。
- 在第一次使用 Azure 金鑰保存庫中的金鑰之前，請先備份 Azure 金鑰保存庫金鑰。 如需詳細資訊，請參閱 [Backup-AzureKeyVaultKey](/sql/relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault) 命令。
- 每當對金鑰進行任何變更時 (例如新增 ACL、新增標籤、新增金鑰屬性)，請務必先另行備份 Azure Key Vault 金鑰。

  > [!NOTE]
  > 備份金鑰是 Azure Key Vault 金鑰作業，它會傳回可儲存在任何位置的檔案。

### <a name="types-of-keys"></a>金鑰的類型

您可在可搭配 SQL Server 使用的 Azure 金鑰保存庫中產生兩種類型的金鑰。 這兩種類型都是非對稱 2048 位元 RSA 金鑰。  
  
  - **受軟體保護**：在軟體中處理，並在靜止時加密。 受軟體保護金鑰上的作業發生在 Azure 虛擬機器上。 針對未在生產環境部署中使用的金鑰，建議使用這種類型。  

  - **受 HSM 保護**：由硬體安全模組所建立和保護，以提供額外安全性。 每個金鑰版本的成本大約美金 $1 元。  
  
    > [!IMPORTANT] 
    > 針對 SQL Server 連接器，請僅使用字元 "a-z"、"A-Z"、"0-9" 和連字號 "-"，且長度限制為 26 個字元。   
    > Azure 金鑰保存庫中金鑰名稱相同的不同金鑰版本無法與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 連接器搭配運作。 若要輪替 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 正在使用的 Azure 金鑰保存庫金鑰，請參閱＜A. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 連接器的維護指示＞一節 ([SQL Server 連接器維護和疑難排解](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md))。  

### <a name="import-an-existing-key"></a>匯入現有的金鑰   
  
如果具有現存的 2048 位元 RSA 受軟體保護金鑰，則可將金鑰上傳至 Azure 金鑰保存庫。 或者，如果 `C:\\` 磁碟機中已儲存一個 PFX 檔案 (名為 *softkey.pfx*)，且想要將其上傳至 Azure 金鑰保存庫，請執行下列內容，以將 PFX 檔案的 `securepfxpwd` 變數設定為密碼 `12987553`：  
  
``` powershell  
$securepfxpwd = ConvertTo-SecureString -String '12987553' `  
  -AsPlainText -Force  
```  

然後可執行下列命令以匯入來自 PFX 檔案的金鑰，該檔案是透過金鑰保存庫服務中的硬體 (建議選項) 來保護該金鑰︰  
  
``` powershell  
    Add-AzureKeyVaultKey -VaultName 'ContosoKeyVault' `  
      -Name 'ContosoFirstKey' -KeyFilePath 'c:\softkey.pfx' `  
      -KeyFilePassword $securepfxpwd $securepfxpwd  -Destination 'HSM'  
```  
 
> [!CAUTION]
> 強烈建議在生產案例中匯入非對稱金鑰，因為這樣做可讓系統管理員在金鑰委付系統中委付金鑰。 如果非對稱金鑰是在保存庫中建立，由於私密金鑰永遠不會離開保存庫，因此無法委付金鑰。 您應該委付用來保護重要資料的金鑰。 遺失非對稱金鑰會導致資料永久遺失。  

### <a name="create-a-new-key"></a>建立新的金鑰 

或者，您可直接在 Azure 金鑰保存庫中建立新的加密金鑰，並以軟體或 HSM 加以保護。  在此範例中，我們會使用 `Add-AzureKeyVaultKey` Cmdlet 來建立受軟體保護金鑰：  

``` powershell  
Add-AzureKeyVaultKey -VaultName 'ContosoEKMKeyVault' `  
  -Name 'ContosoRSAKey0' -Destination 'Software'  
```  
  
此陳述式會傳回：  
  
```
Attributes : Microsoft.Azure.Commands.KeyVault.Models.KeyAttributes  
Key        :  {"kid":"https:contosoekmkeyvault.azure.net/keys/  
                ContosoRSAKey0/<guid>","dty":"RSA:,"key_ops": ...  
VaultName  : contosodevkeyvault  
Name       : contosoRSAKey0  
Version    : <guid>  
Id         : https://contosoekmkeyvault.vault.azure.net:443/  
              keys/ContosoRSAKey0/<guid>  
```  

> [!IMPORTANT] 
> 金鑰保存庫支援多種版本的同名金鑰，但不應該復原 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 連接器所使用的金鑰或建立其版本。 如果系統管理員想要復原 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 加密所使用的金鑰，則應該在金鑰保存庫中建立不同名稱的新金鑰並用來加密 DEK。  

---
       
## <a name="step-3-install-the-ssnoversion-connector"></a>步驟 3：安裝 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 連接器  

從 [Microsoft 下載中心](https://go.microsoft.com/fwlink/p/?LinkId=521700)下載 SQL Server 連接器。 下載應該由 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 電腦的系統管理員來完成。  

> [!NOTE] 
> 1\.0.0.440 版和較舊版本皆已取代，且生產環境也不再支援。 請前往 [Microsoft 下載中心](https://www.microsoft.com/download/details.aspx?id=45344)以升級至版本 1.0.1.0 版或更新版本。 請遵循 [SQL Server 連接器維護和疑難排解](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md)頁面中＜SQL Server 連接器的升級＞一節下方的指示。

> [!NOTE]
> 1\.0.5.0 版中的憑證指紋演算法有重大變更。 您在升級至 1.0.5.0 版之後可能會遇到資料庫還原失敗。 如需詳細資訊，請參閱[知識庫文章 447099](https://support.microsoft.com/help/4470999/db-backup-problems-to-sql-server-connector-for-azure-1-0-5-0)。
  
  ![[SQL Server 連接器安裝精靈] 的螢幕擷取畫面](../../../relational-databases/security/encryption/media/ekm/ekm-connector-install.png)  
  
根據預設，連接器會安裝在 C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault。 這個位置可以在安裝期間變更。 如果將其變更，請調整下一節中的指令碼。  
  
連接器沒有介面，但如果安裝成功，即會在電腦上安裝 *Microsoft.AzureKeyVaultService.EKM.dll*。 此組件是密碼編譯的 EKM 提供者 DLL，需要使用 `CREATE CRYPTOGRAPHIC PROVIDER` 陳述式向 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 註冊。  
  
SQL Server 連接器安裝也可讓您選擇性地下載 SQL Server 加密的範例指令碼。  
  
若要檢視 SQL Server Connector 的錯誤碼說明、組態設定或維護工作，請參閱：  
  
- [A.SQL Server Connector 的維護指示](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md#AppendixA)  
- [C.SQL Server Connector 的錯誤碼說明](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md#AppendixC)  
  
  
## <a name="step-4-configure-ssnoversion"></a>步驟 4：設定 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  

如需本節中每個動作所需最小權限等級的附註。請參閱 [B. 常見問題集](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md#AppendixB)。  
  
1.  執行 *sqlcmd.exe* 或 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Studio。  
  
1.  請執行下列 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 指令碼，將 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 設定為使用 EKM：  
  
    ```sql  
    -- Enable advanced options.  
    USE master;  
    GO  

    EXEC sp_configure 'show advanced options', 1;  
    GO  
    RECONFIGURE;  
    GO  

    -- Enable EKM provider  
    EXEC sp_configure 'EKM provider enabled', 1;  
    GO  
    RECONFIGURE;  
    ```  
  
1. 使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 將 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 連接器註冊為 EKM 提供者。  
  
    使用 Azure 金鑰保存庫 EKM 提供者的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 連接器來建立密碼編譯提供者。    
    
    在此範例中，提供者名稱為 `AzureKeyVault_EKM`。  
  
    ```sql  
    CREATE CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM   
    FROM FILE = 'C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault\Microsoft.AzureKeyVaultService.EKM.dll';  
    GO  
    ```  
    
    > [!NOTE]
    > 檔案路徑長度不能超過 256 個字元。  
  
1. 設定 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登入的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 認證來使用金鑰保存庫。  
  
    必須將認證新增至每個將使用金鑰保存庫中金鑰來執行加密的登入。 這可能包括：  
  
    - 使用金鑰保存庫以設定和管理 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 加密案例的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 系統管理員登入。  
  
    - 可能會啟用 TDE 或其他 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 加密功能的其他 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登入。  
  
    認證與登入之間的一對一對應。 也就是說，每個登入都必須具有唯一的認證。  
  
    以下列方式修改此 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 指令碼：  
  
    - 編輯 `IDENTITY` 引數 (`ContosoEKMKeyVault`)，以指向 Azure 金鑰保存庫。
      - 如果使用的是*全域 Azure*，請使用 Azure 金鑰保存庫名稱來取代 `IDENTITY` 引數 ([步驟 2：建立金鑰保存庫](#step-2-create-a-key-vault))。
      - 如果使用的是「私人 Azure 雲端」(例如 Azure Government、Azure China 21Vianet 或 Azure 德國)，請將 `IDENTITY` 引數取代為[＜使用 PowerShell 建立金鑰保存庫和金鑰＞](#create-a-key-vault-and-key-by-using-powershell)一節的步驟 3 中所傳回保存庫 URI。 請不要在保存庫 URI 中包括 "https://"。   
    - 將 `SECRET` 引數的第一個部分取代為 Azure Active Directory 用戶端識別碼 ([步驟 1：設定 Azure AD 服務主體](#step-1-set-up-an-azure-ad-service-principal))。 在此範例中，**用戶端識別碼**為 `9A57CBC54C4C40E2B517EA677E0EFA00`。  
  
      > [!IMPORTANT] 
      > 請務必移除應用程式 (用戶端) 識別碼中的連字號。  
  
    - 使用**用戶端密碼**完成 `SECRET` 引數的第二個部分 ([步驟 1：設定 Azure AD 服務主體](#step-1-set-up-an-azure-ad-service-principal))。  在此範例中，用戶端密碼為 `08:k?[:XEZFxcwIPvVVZhTjHWXm7w1?m`。 `SECRET` 引數最終字串會是一連串較長的字母和數字，不含連字號。  
  
    ```sql  
    USE master;  
    CREATE CREDENTIAL sysadmin_ekm_cred   
        WITH IDENTITY = 'ContosoEKMKeyVault',                            -- for public Azure
        -- WITH IDENTITY = 'ContosoEKMKeyVault.vault.usgovcloudapi.net', -- for Azure Government
        -- WITH IDENTITY = 'ContosoEKMKeyVault.vault.azure.cn',          -- for Azure China 21Vianet
        -- WITH IDENTITY = 'ContosoEKMKeyVault.vault.microsoftazure.de', -- for Azure Germany
               --<----Application (Client) ID ---><--Azure AD app (Client) ID secret-->
        SECRET = '9A57CBC54C4C40E2B517EA677E0EFA0008:k?[:XEZFxcwIPvVVZhTjHWXm7w1?m'   
    FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM;  
  
    -- Add the credential to the SQL Server administrator's domain login   
    ALTER LOGIN [<domain>\<login>]  
    ADD CREDENTIAL sysadmin_ekm_cred;  
    ```  
  
    如需針對 `CREATE CREDENTIAL` 引數使用變數及以程式設計方式從用戶端識別碼移除連字號的範例，請參閱 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-credential-transact-sql.md)。  
  
1. 在 SQL Server 執行個體中開啟 Azure 金鑰保存庫金鑰。  

    無論建立了新的金鑰，或匯入了如[步驟 2：建立金鑰保存庫](#step-2-create-a-key-vault)中所述的非對稱金鑰，都需要開啟金鑰。 請在下列 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 指令碼中提供金鑰名稱來開啟金鑰。  
  
    - 將 `EKMSampleASYKey` 取代為 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中您想要的金鑰名稱。  
    - 將 `ContosoRSAKey0` 取代為 Azure 金鑰保存庫中金鑰的名稱。  
  
    ```sql  
    CREATE ASYMMETRIC KEY EKMSampleASYKey   
    FROM PROVIDER [AzureKeyVault_EKM]  
    WITH PROVIDER_KEY_NAME = 'ContosoRSAKey0',  
    CREATION_DISPOSITION = OPEN_EXISTING;  
    ```  
    
1. 使用在上一個步驟中所建立 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 內的非對稱金鑰來建立新登入。

     ```sql  
    --Create a Login that will associate the asymmetric key to this login
    CREATE LOGIN TDE_Login
    FROM ASYMMETRIC KEY EKMSampleASYKey;
    ```  

1. 從 SQL Server 中的非對稱金鑰來建立新登入。 卸除步驟 4 中的認證對應：設定 SQL Server，以便認證可對應至新的登入。

     ```sql  
    --Now drop the credential mapping from the original association
    ALTER LOGIN [<domain>\<login>]
    DROP CREDENTIAL sysadmin_ekm_cred;
    ```     

1. 改變新的登入，並將 EKM 認證對應至新的登入。

     ```sql  
    --Now drop the credential mapping from the original association
    ALTER LOGIN TDE_Login
    ADD CREDENTIAL sysadmin_ekm_cred;
    ```  

1. 建立將使用 Azure 金鑰保存庫金鑰來進行加密的測試資料庫。

     ```sql
    --Create a test database that will be encrypted with the Azure key vault key
    CREATE DATABASE TestTDE
    ```  

1. 使用非對稱金鑰 (EKMSampleASYKey) 來建立資料庫加密金鑰。

    ```sql  
    --Create an ENCRYPTION KEY using the ASYMMETRIC KEY (EKMSampleASYKey)
    CREATE DATABASE ENCRYPTION KEY   
    WITH ALGORITHM = AES_256   
    ```  
  
1. 加密測試資料庫。 將加密設為開啟以啟用 TDE。

     ```sql  
    --Enable TDE by setting ENCRYPTION ON
    ALTER DATABASE TestTDE   
    SET ENCRYPTION ON;  
     ```  
    
1. 清除測試物件。 刪除在此測試指令碼中建立的所有物件。

    ```sql  
    -- CLEAN UP
    USE Master
    ALTER DATABASE [TestTDE] SET SINGLE_USER WITH ROLLBACK IMMEDIATE
    DROP DATABASE [TestTDE]

    ALTER LOGIN [TDE_Login] DROP CREDENTIAL [sysadmin_ekm_cred]
    DROP LOGIN [TDE_Login]

    DROP CREDENTIAL [sysadmin_ekm_cred]  

    USE MASTER
    DROP ASYMMETRIC KEY [EKMSampleASYKey]
    DROP CRYPTOGRAPHIC PROVIDER [AzureKeyVault_EKM]
    ```  
    
如需範例指令碼，請參閱 [SQL Server 透明資料加密和使用 Azure Key Vault 進行可延伸金鑰管理](https://techcommunity.microsoft.com/t5/sql-server/intro-sql-server-transparent-data-encryption-and-extensible-key/ba-p/1427549)部落格文章 (英文)。


## <a name="next-steps"></a>後續步驟  
  
現在已完成基本組態，請參閱[搭配使用 SQL Server 連接器與 SQL 加密功能](../../../relational-databases/security/encryption/use-sql-server-connector-with-sql-encryption-features.md)。
  
## <a name="see-also"></a>另請參閱  

* [使用 Azure Key Vault 進行可延伸金鑰管理](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)   
* [SQL Server 連接器維護和疑難排解](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md)

