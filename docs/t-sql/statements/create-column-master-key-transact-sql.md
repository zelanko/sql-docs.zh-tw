---
title: CREATE COLUMN MASTER KEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SQL13.SWB.NEWCOLUMNMASTERKEYDEF.GENERAL.F1
- SQL13.SWB.COLUMNMASTERKEYDEF.GENERAL.F1
- CREATE COLUMN MASTER KEY
- COLUMN MASTER KEY
- CREATE_COLUMN_MASTER_KEY_TSQL
- COLUMN_MASTER_KEY_TSQL
- SQL13.SWB.NEWCOLUMNMASTERKEY.GENERAL.F1
- SQL13.SWB.COLUMNMASTERKEY.GENERAL.F1
dev_langs:
- TSQL
helpviewer_keywords:
- column master key definition
- column master key, create
- CREATE COLUMN MASTER KEY statement
- Always Encrypted, create column master key
ms.assetid: f8926b95-e146-4e3f-b56b-add0c0d0a30e
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 17e717fd999109390c001bdab9aeee5629c1a119
ms.sourcegitcommit: ad3b2133585bc14fc6ef8be91f8b74ee2f498b64
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/20/2019
ms.locfileid: "56425793"
---
# <a name="create-column-master-key-transact-sql"></a>CREATE COLUMN MASTER KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

在資料庫中建立資料行主要金鑰中繼資料物件。 代表金鑰的資料行主要金鑰中繼資料項目儲存在外部金鑰存放區中。 當您使用 [Always Encrypted &#40;資料庫引擎&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md) 功能時，此金鑰可保護 (加密) 資料行加密金鑰。 有多個資料行主要金鑰允許定期進行金鑰輪替，用來加強安全性。 請使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的 [物件總管] 或 PowerShell 在金鑰存放區中建立資料行主要金鑰，並在資料庫中建立其相關的中繼資料物件。 如需詳細資訊，請參閱 [Always Encrypted 的金鑰管理概觀](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)。  
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
 

> [!IMPORTANT]
> 建立已啟用記憶體保護區的金鑰 (使用 ENCLAVE_COMPUTATIONS) 需要[具有安全記憶體保護區的 Always Encrypted](../../relational-databases/security/encryption/always-encrypted-enclaves.md)。

## <a name="syntax"></a>語法  

```  
CREATE COLUMN MASTER KEY key_name   
    WITH (  
        KEY_STORE_PROVIDER_NAME = 'key_store_provider_name',  
        KEY_PATH = 'key_path'   
        [,ENCLAVE_COMPUTATIONS (SIGNATURE = signature)]
         )   
[;]  
```  
  
## <a name="arguments"></a>引數  
*key_name*  
資料行主要金鑰在資料庫中的名稱。  
  
*key_store_provider_name*  
指定金鑰存放區提供者的名稱。 金鑰存放區提供者是一種用戶端軟體元件，可保存含有資料行主要金鑰的金鑰存放區。 

啟用了 Always Encrypted 的用戶端驅動程式會：

- 使用金鑰存放區提供者名稱 
- 在金鑰存放區提供者的驅動程式登錄中搜尋金鑰存放區提供者 

驅動程式接著會使用提供者來解密資料行加密金鑰。 資料行加密金鑰受到資料行主要金鑰保護。 資料行主要金鑰會儲存在基礎金鑰存放區中。 資料行加密金鑰的純文字值，接著會用於加密對應至加密資料庫資料行的查詢參數。 或者，資料行加密金鑰會解密來自加密資料行的查詢結果。  
  
啟用 Always Encrypted 的用戶端驅動程式程式庫包含常用金鑰存放區的金鑰存放區提供者。   
  
可用提供者集合取決於用戶端驅動程式的類型和版本。 針對特定驅動程式，請參閱 Always Encrypted 文件：

[搭配使用 Always Encrypted 與 .NET Framework Provider for SQL Server 開發應用程式](../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)


下表顯示系統提供者的名稱：  
  
|金鑰存放區提供者名稱|基礎金鑰存放區|  
    |-----------------------------|--------------------------|
    |'MSSQL_CERTIFICATE_STORE'|Windows 憑證存放區| 
    |'MSSQL_CSP_PROVIDER'|支援 Microsoft CryptoAPI 的存放區，例如硬體安全性模組 (HSM)。|
    |'MSSQL_CNG_STORE'|支援新一代密碼編譯 API 的存放區，例如硬體安全性模組 (HSM)。|  
    |'Azure_Key_Vault'|請參閱[開始使用 Azure Key Valut](https://azure.microsoft.com/documentation/articles/key-vault-get-started/)|  
  

在啟用 Always Encrypted 的用戶端驅動程式中，您可以設定自訂金鑰存放區提供者，用來儲存沒有內建金鑰存放區提供者的資料行主要金鑰。 自訂金鑰存放區提供者的名稱不能以 'MSSQL_' 為開頭，這是為 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 金鑰存放區提供者保留的前置詞。 

  
key_path  
資料行主要金鑰存放區中的金鑰路徑。 金鑰路徑對於預期要加密或解密資料的每個用戶端應用程式而言都必須有效。 資料會儲存在所參考資料行主要金鑰 (間接) 保護的資料行中。 用戶端應用程式必須具有金鑰的存取權。 金鑰路徑的格式為金鑰存放區提供者專用。 下列清單描述特定 Microsoft 系統金鑰存放區提供者的金鑰路徑格式。  
  
-   **提供者名稱：** MSSQL_CERTIFICATE_STORE  
  
    **金鑰路徑格式：***CertificateStoreName*/*CertificateStoreLocation*/*CertificateThumbprint*  
  
     其中：  
  
    *CertificateStoreLocation*  
    憑證存放區位置必須是目前的使用者或本機電腦。 如需詳細資訊，請參閱 [Local Machine and Current User Certificate Stores](https://msdn.microsoft.com/library/windows/hardware/ff548653.aspx) (本機電腦和目前使用者憑證存放區)。  
  
    *CertificateStore*  
    憑證存放區名稱，例如 'My'。  
  
    *CertificateThumbprint*  
    憑證指紋。  
  
    **範例：**  
  
    ```  
    N'CurrentUser/My/BBF037EC4A133ADCA89FFAEC16CA5BFA8878FB94'  
  
    N'LocalMachine/My/CA5BFA8878FB94BBF037EC4A133ADCA89FFAEC16'  
    ```  
  
-   **提供者名稱：** MSSQL_CSP_PROVIDER  
  
    **金鑰路徑格式：***ProviderName*/*KeyIdentifier*  
  
    其中：  
  
    *ProviderName*  
    資料行主要金鑰存放區的密碼編譯服務提供者 (CSP) 名稱，該提供者會實作 CAPI。 如果您使用 HSM 作為金鑰存放區，此提供者名稱必須是您 HSM 廠商提供的 CSP 名稱。 必須在用戶端電腦上安裝提供者。  
  
    *KeyIdentifier*  
    金鑰存放區中用作資料行主要金鑰的金鑰識別碼。  
  
    **範例：**  
  
    ```  
    N'My HSM CSP Provider/AlwaysEncryptedKey1'  
    ```  
  
-   **提供者名稱：** MSSQL_CNG_STORE  
  
    **金鑰路徑格式：***ProviderName*/*KeyIdentifier*  
  
    其中：  
  
    *ProviderName*  
    資料行主要金鑰存放區的金鑰儲存提供者 (KSP) 名稱，該提供者會實作新一代密碼編譯 (CNG) API。 如果您使用 HSM 作為金鑰存放區，此提供者名稱必須是您 HSM 廠商提供的 KSP 名稱。 必須在用戶端電腦上安裝提供者。  
  
    *KeyIdentifier*  
    金鑰存放區中用作資料行主要金鑰的金鑰識別碼。  
  
    **範例：**  
  
    ```  
    N'My HSM CNG Provider/AlwaysEncryptedKey1'  
    ```  

-   **提供者名稱：** AZURE_KEY_STORE  
  
    **金鑰路徑格式：***KeyUrl*  
  
    其中：  
  
    *KeyUrl*  
    Azure Key Vault 中金鑰的 URL

ENCLAVE_COMPUTATIONS  
指定資料行主要金鑰已啟用記憶體保護區。 您可以將所有使用資料行主要金鑰加密的資料行加密金鑰與伺服器端安全記憶體保護區共用，並將它們用於記憶體保護區內部的計算。 如需詳細資訊，請參閱[具有安全記憶體保護區的 Always Encrypted](../../relational-databases/security/encryption/always-encrypted-enclaves.md)。

*signature*  
二進位常值，它是數位簽署「金鑰路徑」和使用資料行主要金鑰之 ENCLAVE_COMPUTATIONS 設定的結果。 簽章會反映是否已指定 ENCLAVE_COMPUTATIONS。 簽章會保護所簽署的值不會受到未經授權的使用者所改變。 已啟用 Always Encrypted 的用戶端驅動程式會驗證簽章，並在簽章無效時，傳回錯誤給應用程式。 簽章需使用用戶端工具予以產生。 如需詳細資訊，請參閱[具有安全記憶體保護區的 Always Encrypted](../../relational-databases/security/encryption/always-encrypted-enclaves.md)。
  
  
## <a name="remarks"></a>Remarks  

請在資料庫中建立資料行加密金鑰中繼資料項目之前，以及可在使用 Always Encrypted 為資料庫中任何資料行進行加密之前，建立資料行主要金鑰中繼資料項目。 中繼資料中的資料行主要金鑰項目不包含實際資料行主要金鑰。 資料行主要金鑰必須儲存在外部資料行金鑰存放區 (SQL Server 之外)。 中繼資料中的金鑰存放區提供者名稱和資料行主要金鑰路徑，對用戶端應用程式而言都必須有效。 用戶端應用程式必須使用資料行主要金鑰來解密資料行加密金鑰。 資料行加密金鑰會使用資料行主要金鑰進行加密。 用戶端應用程式也需要查詢加密資料行。


  
## <a name="permissions"></a>[權限]  
需要 **ALTER ANY COLUMN MASTER KEY** 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-creating-a-column-master-key"></a>A. 建立資料行主要金鑰  
下列範例會為資料行主要金鑰建立資料行主要金鑰中繼資料項目。 對於使用 MSSQL_CERTIFICATE_STORE 提供者來存取資料行主要金鑰的用戶端應用程式，資料行主要金鑰會儲存在憑證存放區中：  
  
```  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
     KEY_STORE_PROVIDER_NAME = N'MSSQL_CERTIFICATE_STORE',   
     KEY_PATH = 'Current User/Personal/f2260f28d909d21c642a3d8e0b45a830e79a1420'  
   );  
```  
  
請為資料行主要金鑰建立資料行主要金鑰中繼資料項目。 使用 MSSQL_CNG_STORE 提供者的用戶端應用程式，會存取資料行主要金鑰：  
  
```  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
    KEY_STORE_PROVIDER_NAME = N'MSSQL_CNG_STORE',    
    KEY_PATH = N'My HSM CNG Provider/AlwaysEncryptedKey'  
);  
```  
  
請為資料行主要金鑰建立資料行主要金鑰中繼資料項目。 對於使用 AZURE_KEY_VAULT 提供者來存取資料行主要金鑰的用戶端應用程式，資料行主要金鑰會儲存在 Azure Key Vault 中。  
  
```  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
    KEY_STORE_PROVIDER_NAME = N'AZURE_KEY_VAULT',  
    KEY_PATH = N'https://myvault.vault.azure.net:443/keys/  
        MyCMK/4c05f1a41b12488f9cba2ea964b6a700');  
```  
  
請為資料行主要金鑰建立資料行主要金鑰中繼資料項目。 資料行主要金鑰會儲存在自訂的資料行主要金鑰存放區中：  
  
```  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
    KEY_STORE_PROVIDER_NAME = 'CUSTOM_KEY_STORE',    
    KEY_PATH = 'https://contoso.vault/sales_db_tce_key'  
);  
```  
### <a name="b-creating-an-enclave-enabled-column-master-key"></a>B. 建立已啟用記憶體保護區的資料行主要金鑰  
下列範例會為啟用記憶體保護區的資料行主要金鑰來建立資料行主要金鑰中繼資料項目。 對於使用 MSSQL_CERTIFICATE_STORE 提供者來存取資料行主要金鑰的用戶端應用程式，啟用記憶體保護區的資料行主要金鑰會儲存在憑證存放區中：  
  
```  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
     KEY_STORE_PROVIDER_NAME = N'MSSQL_CERTIFICATE_STORE',   
     KEY_PATH = 'Current User/Personal/f2260f28d909d21c642a3d8e0b45a830e79a1420'  
     ENCLAVE_COMPUTATIONS (SIGNATURE = 0xA80F5B123F5E092FFBD6014FC2226D792746468C901D9404938E9F5A0972F38DADBC9FCBA94D9E740F3339754991B6CE26543DEB0D094D8A2FFE8B43F0C7061A1FFF65E30FDDF39A1B954F5BA206AAC3260B0657232020542419990261D878318CC38EF4E853970ED69A8D4A306693B8659AAC1C4E4109DE5EB148FD0E1FDBBC32F002C1D8199D313227AD689279D8DEEF91064DF122C19C3767C463723AB663A6F8412AE17E745922C0E3A257EAEF215532588ACCBD440A03C7BC100A38BD0609A119E1EF7C5C6F1B086C68AB8873DBC6487B270340E868F9203661AFF0492CEC436ABF7C4713CE64E38CF66C794B55636BFA55E5B6554AF570CF73F1BE1DBD)
  );  
```  
  
請為啟用記憶體保護區的資料行主要金鑰建立資料行主要金鑰中繼資料項目。 對於使用 AZURE_KEY_VAULT 提供者來存取資料行主要金鑰的用戶端應用程式，啟用記憶體保護區的資料行主要金鑰會儲存在 Azure Key Vault 中。  
  
```  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
    KEY_STORE_PROVIDER_NAME = N'AZURE_KEY_VAULT',  
    KEY_PATH = N'https://myvault.vault.azure.net:443/keys/MyCMK/4c05f1a41b12488f9cba2ea964b6a700');
    ENCLAVE_COMPUTATIONS (SIGNATURE = 0xA80F5B123F5E092FFBD6014FC2226D792746468C901D9404938E9F5A0972F38DADBC9FCBA94D9E740F3339754991B6CE26543DEB0D094D8A2FFE8B43F0C7061A1FFF65E30FDDF39A1B954F5BA206AAC3260B0657232020582413990261D878318CC38EF4E853970ED69A8D4A306693B8659AAC1C4E4109DE5EB148FD0E1FDBBC32F002C1D8199D313227AD689279D8DEEF91064DF122C19C3767C463723AB663A6F8412AE17E745922C0E3A257EAEF215532588ACCBD440A03C7BC100A38BD0609A119E1EF7C5C6F1B086C68AB8873DBC6487B270340E868F9203661AFF0492CEC436ABF7C4713CE64E38CF66C794B55636BFA55E5B6554AF570CF73F1BE1DBD)
  );
```  
  
## <a name="see-also"></a>另請參閱
 
* [DROP COLUMN MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-column-master-key-transact-sql.md)   
* [CREATE COLUMN ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-column-encryption-key-transact-sql.md)
* [sys.column_master_keys (Transact-SQL)](../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md)
* [永遠加密 &#40;Database Engine&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)  
* [永遠加密的金鑰管理概觀](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)
  
