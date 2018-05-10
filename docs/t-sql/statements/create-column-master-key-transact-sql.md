---
title: CREATE COLUMN MASTER KEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: e5dafed981c030b5f06e41610fd3add6c4af0238
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="create-column-master-key-transact-sql"></a>CREATE COLUMN MASTER KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  在資料庫中建立資料行主要金鑰中繼資料物件。 代表金鑰的資料行主要金鑰中繼資料項目會儲存在外部金鑰存放區，可在使用 [Always Encrypted &#40;資料庫引擎&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md) 功能時，用來保護 (加密) 資料行加密金鑰。 有多個資料行主要金鑰即可進行金鑰輪替；定期變更金鑰會加強安全性。 您可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的物件總管或 PowerShell 在資料庫中建立資料行主要金鑰，及其對應的中繼資料物件。 如需詳細資訊，請參閱 [Always Encrypted 的金鑰管理概觀](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
CREATE COLUMN MASTER KEY key_name   
    WITH (  
        KEY_STORE_PROVIDER_NAME = 'key_store_provider_name',  
        KEY_PATH = 'key_path'   
         )   
[;]  
```  
  
## <a name="arguments"></a>引數  
 *key_name*  
 這是資料行主要金鑰在資料庫中的識別名稱。  
  
 *key_store_provider_name*  
 指定金鑰存放區提供者名稱，這個用戶端軟體元件會封裝包含資料行主要金鑰的金鑰存放區。 啟用 Always Encrypted 的用戶端驅動程式會使用金鑰存放區提供者名稱，在金鑰存放區提供者的驅動程式登錄中查詢金鑰存放區提供者。 驅動程式會使用提供者來解密資料行加密金鑰，其受到資料行主要金鑰保護，並儲存在基礎金鑰存放區中。 資料行加密金鑰的純文字值接著會用於加密查詢參數，對應至加密資料庫資料行，或是從加密資料行中解密查詢結果。  
  
 啟用 Always Encrypted 的用戶端驅動程式程式庫包含常用金鑰存放區的金鑰存放區提供者。   
  
可用提供者的組合取決於類型和用戶端驅動程式的版本。 針對特定驅動程式，請參閱 Always Encrypted 文件：

[搭配使用 Always Encrypted 與 .NET Framework Provider for SQL Server 開發應用程式](../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)


下表擷取了系統提供者的名稱：  
  
|金鑰存放區提供者名稱|基礎金鑰存放區|  
    |-----------------------------|--------------------------|
    |'MSSQL_CERTIFICATE_STORE'|Windows 憑證存放區| 
    |'MSSQL_CSP_PROVIDER'|支援 Microsoft CryptoAPI 的存放區，例如硬體安全性模組 (HSM)。|
    |'MSSQL_CNG_STORE'|支援 Cryptography API: Next Generation 的存放區，例如硬體安全性模組 (HSM)。|  
    |'Azure_Key_Vault'|請參閱[開始使用 Azure Key Valut](https://azure.microsoft.com/documentation/articles/key-vault-get-started/)|  
  

 您可以實作自訂金鑰存放區提供者，以將資料行主要金鑰儲存在存放區中；而此存放區在您的已啟用 Always Encrypted 用戶端驅動程式中沒有內建金鑰存放區提供者。  請注意，自訂金鑰存放區提供者的名稱不能以 'MSSQL_' 為開頭，這是為 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 金鑰存放區提供者保留的前置詞。 

  
 key_path  
 資料行主要金鑰存放區中的金鑰路徑。 金鑰路徑在每個用戶端應用程式的內容中都必須有效，這些用戶端應用程式必須加密或解密儲存在參考資料列主要金鑰所保護的資料行中 (間接) 的資料，而且用戶端應用程式必須能夠存取金鑰。 金鑰路徑的格式為金鑰存放區提供者專用。 下列清單描述特定 Microsoft 系統金鑰存放區提供者的金鑰路徑格式。  
  
-   **提供者名稱：**MSSQL_CERTIFICATE_STORE  
  
     **金鑰路徑格式：** *CertificateStoreName*/*CertificateStoreLocation*/*CertificateThumbprint*  
  
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
  
     **金鑰路徑格式：** *ProviderName*/*KeyIdentifier*  
  
     其中：  
  
     *ProviderName*  
     資料行主要金鑰存放區的密碼編譯服務提供者 (CSP) 名稱，該提供者會實作 CAPI。 如果您使用 HSM 作為金鑰存放區，這必須是您 HSM 廠商提供的 CSP 名稱。 必須在用戶端電腦上安裝提供者。  
  
     *KeyIdentifier*  
     金鑰存放區中用作資料行主要金鑰的金鑰識別碼。  
  
     **範例：**  
  
    ```  
    N'My HSM CSP Provider/AlwaysEncryptedKey1'  
    ```  
  
-   **提供者名稱：** MSSQL_CNG_STORE  
  
     **金鑰路徑格式：** *ProviderName*/*KeyIdentifier*  
  
     其中：  
  
     *ProviderName*  
     資料行主要金鑰存放區的金鑰儲存提供者 (KSP) 名稱，該提供者會實作新一代密碼編譯 (CNG)。 如果您使用 HSM 作為金鑰存放區，這必須是您 HSM 廠商提供的 KSP 名稱。 需要在用戶端電腦上安裝提供者。  
  
     *KeyIdentifier*  
     金鑰存放區中用作資料行主要金鑰的金鑰識別碼。  
  
     **範例：**  
  
    ```  
    N'My HSM CNG Provider/AlwaysEncryptedKey1'  
    ```  

-   **提供者名稱：** AZURE_KEY_STORE  
  
     **金鑰路徑格式：** *KeyUrl*  
  
     其中：  
  
     *KeyUrl*  
     Azure Key Vault 中金鑰的 URL


範例
 
`N'https://myvault.vault.azure.net:443/keys/MyCMK/4c05f1a41b12488f9cba2ea964b6a700'`  
  
## <a name="remarks"></a>Remarks  

必須要先建立資料行主要金鑰中繼資料項目，才能夠在資料庫中建立資料行加密金鑰中繼資料項目，以及使用 Always Encrypted 來為資料庫中任何資料行加密。 請注意，中繼資料中的資料行主要金鑰項目不包含實際的資料行主要金鑰，其必須儲存在外部資料行的金鑰存放區 (SQL Server 之外)。 中繼資料中的金鑰存放區提供者名稱和資料行主要金鑰路徑，必須在用戶端應用程式中有效，才能夠使用資料行主要金鑰來為已受到其加密之資料行加密金鑰進行解密，並查詢加密資料行。


  
## <a name="permissions"></a>Permissions  
 需要 **ALTER ANY COLUMN MASTER KEY** 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-creating-a-column-master-key"></a>A. 建立資料行主要金鑰  
 在憑證存放區中，為資料行主要金鑰來建立資料行主要金鑰中繼資料項目，以使用 MSSQL_CERTIFICATE_STORE 提供者的用戶端應用程式來存取資料行主要金鑰：  
  
```  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
     KEY_STORE_PROVIDER_NAME = N'MSSQL_CERTIFICATE_STORE',   
     KEY_PATH = 'Current User/Personal/f2260f28d909d21c642a3d8e0b45a830e79a1420'  
   );  
```  
  
 為受到使用 MSSQL_CNG_STORE 提供者之用戶端應用程式存取的資料行主要金鑰，來建立資料行主要金鑰中繼資料項目：  
  
```  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
    KEY_STORE_PROVIDER_NAME = N'MSSQL_CNG_STORE',    
    KEY_PATH = N'My HSM CNG Provider/AlwaysEncryptedKey'  
);  
```  
  
 對於使用 AZURE_KEY_VAULT 提供者的用戶端應用程式，建立儲存在 Azure Key Vault 的資料行主要金鑰，以存取資料行主要金鑰。  
  
```  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
    KEY_STORE_PROVIDER_NAME = N'AZURE_KEY_VAULT',  
    KEY_PATH = N'https://myvault.vault.azure.net:443/keys/  
        MyCMK/4c05f1a41b12488f9cba2ea964b6a700');  
```  
  
 建立存放於資料行主要金鑰存放區中的 CMK：  
  
```  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
    KEY_STORE_PROVIDER_NAME = 'CUSTOM_KEY_STORE',    
    KEY_PATH = 'https://contoso.vault/sales_db_tce_key'  
);  
```  
  
## <a name="see-also"></a>另請參閱
 
* [DROP COLUMN MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-column-master-key-transact-sql.md)   
* [CREATE COLUMN ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-column-encryption-key-transact-sql.md)
* [sys.column_master_keys (Transact-SQL)](../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md)
* [永遠加密 &#40;Database Engine&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)  
* [永遠加密的金鑰管理概觀](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)
  
