---
title: SQL Server 連接器維護和疑難排解 | Microsoft Docs
ms.custom: ''
ms.date: 04/05/2017
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
- SQL Server Connector, appendix
ms.assetid: 7f5b73fc-e699-49ac-a22d-f4adcfae62b1
caps.latest.revision: 21
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 218b9c66b055d92085307bcea5ff722ddc228215
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sql-server-connector-maintenance-amp-troubleshooting"></a>SQL Server 連接器維護和疑難排解
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  本主題提供 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 連接器的補充資訊。 如需 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 連接器的詳細資訊，請參閱[使用 Azure 金鑰保存庫進行可延伸金鑰管理 &#40;SQL Server&#41;](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)、[使用 Azure 金鑰保存庫進行可延伸金鑰管理的設定步驟](../../../relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault.md)和[搭配使用 SQL Server 連接器與 SQL 加密功能](../../../relational-databases/security/encryption/use-sql-server-connector-with-sql-encryption-features.md)。  
  
  
##  <a name="AppendixA"></a> A. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 連接器的維護指示  
  
### <a name="key-rollover"></a>金鑰變換  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 連接器需要金鑰名稱僅使用字元 “a-z”、“A-Z”、“0-9” 和 “-“，且長度限制為 26 個字元。   
> Azure 金鑰保存庫中金鑰名稱相同的不同金鑰版本，將不會與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 連接器搭配運作。 若要循環使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]正在使用的 Azure 金鑰保存庫金鑰，必須建立具有新金鑰名稱的新金鑰。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 加密的伺服器非對稱金鑰，通常每隔 1-2 年便需要進行版本設定。 請務必注意，雖然金鑰保存庫允許對金鑰進行版本設定，客戶不應該使用該功能來實作版本設定。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 連接器無法處理金鑰保存庫金鑰版本中的變更。 若要實作金鑰版本設定，客戶必須在金鑰保存庫中建立新的金鑰，然後在 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]中重新加密資料加密金鑰。  
  
 針對 TDE，以下是達成此目的的方法：  
  
-   **在 PowerShell 中：**使用不同於金鑰保存庫的現有 TDE 非對稱金鑰名稱來建立新的非對稱金鑰。  
  
    ```powershell  
    Add-AzureRmKeyVaultKey -VaultName 'ContosoDevKeyVault' `  
      -Name 'Key2' -Destination 'Software'  
    ```  
  
-   **使用 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] 或 sqlcmd.exe：**使用下列陳述式 (如第 3 節步驟 3 所示)。  
  
     匯入新的非對稱金鑰。  
  
    ```sql  
    USE master  
    CREATE ASYMMETRIC KEY [MASTER_KEY2]   
    FROM PROVIDER [EKM]   
    WITH PROVIDER_KEY_NAME = 'Key2',   
    CREATION_DISPOSITION = OPEN_EXISTING   
    GO  
    ```  
  
     建立要和新的非對稱金鑰相關聯的新登入 (如 TDE 指示所示)。  
  
    ```sql  
    USE master  
    CREATE LOGIN TDE_Login2   
    FROM ASYMMETRIC KEY [MASTER_KEY2]  
    GO  
    ```  
  
     建立要對應到登入的新認證。  
  
    ```sql  
    CREATE CREDENTIAL Azure_EKM_TDE_cred2  
        WITH IDENTITY = 'ContosoDevKeyVault',   
       SECRET = 'EF5C8E094D2A4A769998D93440D8115DAADsecret123456789=’   
    FOR CRYPTOGRAPHIC PROVIDER EKM;  
  
    ALTER LOGIN TDE_Login2  
    ADD CREDENTIAL Azure_EKM_TDE_cred2;  
    GO  
    ```  
  
     選擇您想要對其資料庫加密金鑰進行重新加密的資料庫。  
  
    ```sql  
    USE [database]  
    GO  
    ```  
  
     重新加密資料庫加密金鑰。  
  
    ```sql  
    ALTER DATABASE ENCRYPTION KEY   
    ENCRYPTION BY SERVER ASYMMETRIC KEY [MASTER_KEY2];  
    GO  
    ```  
  
### <a name="upgrade-of-includessnoversionincludesssnoversion-mdmd-connector"></a>[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 連接器的升級  

1.0.0.440 版和較舊版本皆已被取代，而且生產環境也不再支援。 生產環境支援 1.0.1.0 版及更新版本。 請使用下列指示升級至 [Microsoft 下載中心](https://www.microsoft.com/download/details.aspx?id=45344)可用的最新版本。

目前使用的版本若為 1.0.1.0 版或更新版本，請執行下列步驟更新至最新版的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 連接器。 這些指示不需要重新啟動 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體。
 
1. 從 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Microsoft 下載中心 [安裝最新版的](https://www.microsoft.com/download/details.aspx?id=45344)連接器。 在安裝程式精靈中，將新的 DLL 檔案儲存在和原始 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 連接器 DLL 檔案路徑不同的檔案路徑。 例如，新的檔案路徑可能是︰ `C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault\<latest version number>\Microsoft.AzureKeyVaultService.EKM.dll`
 
2. 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]執行個體中，執行下列 Transact-SQL 命令，將您的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體指向新版的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 連接器︰

    ``` 
    ALTER CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov   
    FROM FILE =   
    'C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault\<latest version number>\Microsoft.AzureKeyVaultService.EKM.dll'
    GO  
    ```

目前使用的版本若為 1.0.0.440 版或更舊版本，請執行下列步驟更新至最新版的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 連接器。
  
1.  停止 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]的執行個體。  
  
2.  停止 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 連接器服務。  
  
3.  使用 Windows 的 [程式和功能] 功能解除安裝 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 連接器。  
  
     或者，您可以重新命名 DLL 檔案所在的資料夾。 資料夾的預設名稱是 “[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] for Microsoft Azure Key Vault”。  
  
4.  從 Microsoft 下載中心安裝最新版本的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 連接器。  
  
5.  重新啟動 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]的執行個體。  
  
6.  執行下列陳述式來改變 EKM 提供者，以開始使用最新版本的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 連接器。 請確定檔案路徑指向您下載最新版本的位置。 (如果新版本和原始版本安裝在相同的位置，可略過此步驟。) 
  
    ```sql  
    ALTER CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov   
    FROM FILE =   
    'C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault\Microsoft.AzureKeyVaultService.EKM.dll';  
    GO  
    ```  
  
7.  請檢查是否可以存取使用 TDE 的資料庫。  
  
8.  驗證更新運作之後，即可刪除舊 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 連接器資料夾 (如果您選擇將它重新命名，而不是在步驟 3 中解除安裝)。  
  
### <a name="rolling-the-includessnoversionincludesssnoversion-mdmd-service-principal"></a>復原 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服務主體  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 使用 Azure Active Directory 中所建立的服務主體作為存取金鑰保存庫的認證。  服務主體擁有用戶端識別碼和驗證金鑰。  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 認證是使用 **VaultName**、 **用戶端識別碼**和 **驗證金鑰**進行設定。  **驗證金鑰** 將於一段時間內有效 (1 或 2 年)。   在時間間隔到期之前，必須在 Azure AD 中為服務主體產生新的金鑰。  然後必須在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中變更認證。    [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] 會在目前的工作階段中為認證維持一份快取，因此認證變更時，應該重新啟動 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] 。  
  
### <a name="key-backup-and-recovery"></a>金鑰備份和復原  
金鑰保存庫應該要定期備份。 如果遺失保存庫中的非對稱金鑰，便可以從備份還原它。 必須使用與以前相同的名稱來還原金鑰，作用與 [還原 PowerShell] 命令相同 (請參閱下面的步驟)。  
如果遺失保存庫，您便需要重新建立保存庫，並使用和先前相同的名稱將非對稱金鑰還原至保存庫。 保存庫名稱可以不同 (或是和先前相同)。 您也必須在新的保存庫上設定存取權限，以授與 SQL Server 服務主體針對 SQL Server 加密案例所需的存取權限，然後調整 SQL Server 認證以反映新的保存庫名稱。  
綜上所述，以下為其步驟：  
  
* 備份保存庫金鑰 (使用 Backup-AzureKeyVaultKey Powershell Cmdlet)。  
* 如果保存庫失敗，請在相同的地理區域* 中建立新的保存庫。 進行這項建立的使用者應該位於與 SQL Server 之服務主體設定相同的預設目錄中。  
* 將金鑰還原至新的保存庫 (使用 Restore-AzureKeyVaultKey Powershell Cmdlet - 這會使用與以前相同的名稱來還原金鑰)。 如果已經有相同名稱的金鑰，則還原會失敗。  
* 授與 SQL Server 服務主體使用新保存庫的權限。  
* 修改 Database Engine 所使用的 SQL Server 認證，以反映新的保存庫名稱 (如果需要)。  
  
只要金鑰備份位於相同的地理區域或國家雲端，就可以跨 Azure 區域進行還原：美國、加拿大、日本、澳洲、印度、亞太地區 (APAC)、歐洲巴西、中國、美國政府或德國。  
  
  
##  <a name="AppendixB"></a> B. 常見問題集  
### <a name="on-azure-key-vault"></a>在 Azure 金鑰保存庫上  
  
**金鑰作業如何與 Azure 金鑰保存庫搭配運作？**  
 金鑰保存庫中的非對稱金鑰可用來保護 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 加密金鑰。 只有非對稱金鑰的公開部分可離開保存庫，保存庫絕不會匯出私用部分。 所有使用非對稱金鑰的密碼編譯作業都是在 Azure 金鑰保存庫服務內完成，並受到服務安全性的保護。  
  
 **什麼是金鑰 URI？**  
 Azure 金鑰保存庫中的每個金鑰都有統一資源識別碼 (URI)，可用來在您的應用程式中參考該金鑰。 使用 `https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey` 的格式來取得目前的版本，並使用 `https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87` 的格式來取得特定版本。  
  
### <a name="on-configuring-includessnoversionincludesssnoversion-mdmd"></a>設定時 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  

**SQL Server 連接器需要存取哪些端點？** 連接器會與兩個需要設為允許清單的端點通訊。 針對 HTTPS，這些其他服務之輸出通訊所需的唯一連接埠是 443：
-  login.microsoftonline.com/*:443
-  *.vault.azure.net/*:443
  
**什麼是 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中每個組態步驟所需的最低權限等級？**  
 雖然您能以 sysadmin 固定伺服器角色的成員身分執行所有設定步驟，但是 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 鼓勵您將自己所使用的權限降至最低。 下列清單定義每個動作的最小權限層級。  
  
-   若要建立密碼編譯提供者，需要 `CONTROL SERVER` 權限或 **sysadmin** 固定伺服器角色中的成員資格。  
  
-   若要變更組態選項並執行 `RECONFIGURE` 陳述式，您必須獲授與 `ALTER SETTINGS` 伺服器層級權限。 sysadmin 和 `ALTER SETTINGS` serveradmin **固定伺服器角色會隱含** 權限。  
  
-   若要建立認證，需要 `ALTER ANY CREDENTIAL` 權限。  
  
-   若要新增登入的認證，需要 `ALTER ANY LOGIN` 權限。  
  
-   若要建立非對稱金鑰，需要 `CREATE ASYMMETRIC KEY` 權限。  

**如何變更預設的 Active Directory，在相同的訂用帳戶中建立金鑰保存庫，讓 Active Directory 變成我為 [!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)] 連接器建立的服務主體？**

![aad-change-default-directory-helpsteps](../../../relational-databases/security/encryption/media/aad-change-default-directory-helpsteps.png)

1. 請前往 Azure 傳統入口網站：[https://manage.windowsazure.com](https://manage.windowsazure.com)  
2. 在左側的功能表中，向下捲動並選取 [設定]。
3. 選取目前使用的 Azure 訂用帳戶，並按一下畫面底部命令的 [編輯目錄]。
4. 在快顯視窗中，使用 [目錄] 下拉式清單選取您想使用的 Active Directory。 這樣即可讓它成為預設目錄。
5. 您必須是新選取之 Active Directory 的全域管理員。 如果您不是全域管理員，就可能會因為切換目錄而遺失管理權限。
6. 快顯視窗關閉後，如果沒有看到任何訂用帳戶，您可能需要更新畫面右上角功能表中 [訂用帳戶] 篩選的 [依目錄篩選] 篩選，才能看到使用剛更新之 Active Directory 的訂用帳戶。

    > [!NOTE] 
    > 您可能無權實際變更 Azure 訂用帳戶的預設目錄。 在此情況下，請在您的預設目錄中建立 AAD 服務主體，讓它和稍後要用的 Azure 金鑰保存庫位於相同的目錄。

若要深入了解 Active Directory，請參閱 [Azure 訂用帳戶如何與 Azure Active Directory 產生關聯](https://azure.microsoft.com/documentation/articles/active-directory-how-subscriptions-associated-directory/)。
  
##  <a name="AppendixC"></a> C. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 連接器的錯誤碼說明  
 **提供者錯誤碼：**  
  
錯誤碼  |符號  |描述    
---------|---------|---------  
0 | scp_err_Success | 此作業已成功。    
@shouldalert | scp_err_Failure | 作業失敗。    
2 | scp_err_InsufficientBuffer | 此錯誤會指示引擎為緩衝區配置更多記憶體。    
3 | scp_err_NotSupported | 不支援此作業。 例如，EKM 提供者不支援指定的金鑰類型或演算法。    
4 | scp_err_NotFound | EKM 提供者找不到指定的金鑰或演算法。    
5 | scp_err_AuthFailure | 向 EKM 提供者驗證失敗。    
6 | scp_err_InvalidArgument | 提供的引數無效。    
7 | scp_err_ProviderError | 在 SQL 引擎捕捉到的 EKM 提供者中發生未指定的錯誤。    
2049 | scp_err_KeyNameDoesNotFitThumbprint | 金鑰名稱太長，而無法放入 SQL 引擎的指紋。 金鑰名稱不得超過 26 個字元。    
2050 | scp_err_PasswordTooShort | 串連 AAD 用戶端識別碼和機密的機密字串小於 32 個字元。    
2051 | scp_err_OutOfMemory | SQL 引擎已用盡記憶體，且無法配置 EKM 提供者的記憶體。    
2052 | scp_err_ConvertKeyNameToThumbprint | 無法將金鑰名稱轉換成指紋。    
2053 | scp_err_ConvertThumbprintToKeyName|  無法將指紋轉換成金鑰名稱。    
3000 | ErrorSuccess | AKV 作業已成功。    
3001 | ErrorUnknown | AKV 作業失敗，發生未指定的錯誤。    
3002 | ErrorHttpCreateHttpClientOutOfMemory | 因為記憶體不足，所以無法建立 AKV 作業的 HttpClient。    
3003 | ErrorHttpOpenSession | 因為發生網路錯誤，所以無法開啟 HTTP 工作階段。    
3004 | ErrorHttpConnectSession | 因為發生網路錯誤，所以無法連接 HTTP 工作階段。    
3005 | ErrorHttpAttemptConnect | 因為發生網路錯誤，所以無法嘗試連接。    
3006 | ErrorHttpOpenRequest | 因為發生網路錯誤，所以無法開啟要求。    
3007 | ErrorHttpAddRequestHeader | 無法新增要求標頭。    
3008 | ErrorHttpSendRequest | 因為發生網路錯誤，所以無法傳送要求。    
3009 | ErrorHttpGetResponseCode | 因為發生網路錯誤，所以無法取得回應碼。    
3010 | ErrorHttpResponseCodeUnauthorized | 伺服器已針對要求回應 401。    
3011 | ErrorHttpResponseCodeThrottled | 伺服器已節流處理要求。    
3012 | ErrorHttpResponseCodeClientError | 連接器傳送的要求無效。 這通常表示索引鍵名稱無效或包含無效的字元。
3013 | ErrorHttpResponseCodeServerError | 伺服器已回應 500 與 600 之間的回應碼。    
3014 | ErrorHttpQueryHeader | 無法查詢回應標頭。    
3015 | ErrorHttpQueryHeaderOutOfMemoryCopyHeader | 因為記憶體不足，所以無法複製回應標頭。    
3016 | ErrorHttpQueryHeaderOutOfMemoryReallocBuffer | 重新配置緩衝區時，因為記憶體不足，所以無法查詢回應標頭。    
3017 | ErrorHttpQueryHeaderNotFound | 在回應中找不到查詢標頭。    
3018 | ErrorHttpQueryHeaderUpdateBufferLength | 查詢回應標頭時，無法更新緩衝區長度。    
3019 | ErrorHttpReadData | 因為發生網路錯誤，所以無法讀取回應資料。 
3076 | ErrorHttpResourceNotFound | 伺服器回應 404，因為找不到索引鍵名稱。 請確定保存庫中有索引鍵名稱。
3077 | ErrorHttpOperationForbidden | 伺服器回應 403，因為使用者沒有適當的權限，不能執行動作。 請確定您有執行指定作業的權限。 連接器至少需要「get、list、wrapKey、unwrapKey」權限，才能正確運作。   
  
如果在此表格中看不到您的錯誤代碼，以下是一些可能發生此錯誤的原因︰   
  
-   您可能沒有網際網路存取權，因此無法存取您的 Azure 金鑰保存庫 - 請檢查您的網際網路連線。  
  
-   Azure 金鑰保存庫服務可能已關閉。 請在其他時間再試一次。  
  
-   您可能已經從 Azure 金鑰保存庫或 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]卸除非對稱金鑰。 請還原金鑰。  
  
-   如果收到「無法載入程式庫」錯誤，請確定您已根據所執行之 SQL Server 版本安裝正確版本的 Visual Studio C++ 可轉散發套件。 下表會指定要從 Microsoft 下載中心安裝的版本。   
  
SQL Server 版本  |可轉散發套件的安裝連結    
---------|--------- 
2008、2008 R2、2012、2014 | [適用於 Visual Studio 2013 的 Visual C++ 可轉散發套件](https://www.microsoft.com/download/details.aspx?id=40784)    
2016 | [適用於 Visual Studio 2015 的 Visual C++ 可轉散發套件](https://www.microsoft.com/download/details.aspx?id=48145)    
  
  
## <a name="additional-references"></a>其他參考  
 深入了解可延伸金鑰管理  
  
-   [可延伸金鑰管理 &#40;EKM&#41;](../../../relational-databases/security/encryption/extensible-key-management-ekm.md)  
  
 支援 EKM 的 SQL 加密︰  
  
-   [使用 EKM 在 SQL Server 上啟用 TDE](../../../relational-databases/security/encryption/enable-tde-on-sql-server-using-ekm.md)  
  
-   [備份加密](../../../relational-databases/backup-restore/backup-encryption.md)  
  
-   [建立加密的備份](../../../relational-databases/backup-restore/create-an-encrypted-backup.md)  
  
 相關 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 命令：  
  
-   [sp_configure &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
-   [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../../t-sql/statements/create-cryptographic-provider-transact-sql.md)  
  
-   [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-credential-transact-sql.md)  
  
-   [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-asymmetric-key-transact-sql.md)  
  
-   [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-symmetric-key-transact-sql.md)  
  
-   [CREATE LOGIN &#40;Transact-SQL&#41;](../../../t-sql/statements/create-login-transact-sql.md)  
  
-   [ALTER LOGIN &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-login-transact-sql.md)  
  
 Azure 金鑰保存庫文件：  
  
-   [何謂 Azure Key Vault？](https://azure.microsoft.com/documentation/articles/key-vault-whatis/)  
  
-   [開始使用 Azure Key Vault](https://azure.microsoft.com/documentation/articles/key-vault-get-started/)  
  
-   PowerShell [Azure 金鑰保存庫 Cmdlet](https://msdn.microsoft.com/library/dn868052.aspx) 參考  
  
## <a name="see-also"></a>另請參閱  
 [使用 Azure Key Vault 進行可延伸金鑰管理](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  [搭配使用 SQL Server 連接器與 SQL 加密功能](../../../relational-databases/security/encryption/use-sql-server-connector-with-sql-encryption-features.md)   
 [EKM provider enabled 伺服器組態選項](../../../database-engine/configure-windows/ekm-provider-enabled-server-configuration-option.md)   
 [使用 Azure 金鑰保存庫進行可延伸金鑰管理的設定步驟](../../../relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault.md)  
  
  
