---
title: "建立資料行主要金鑰 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/18/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
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
dev_langs: TSQL
helpviewer_keywords:
- column master key definition
- column master key, create
- CREATE COLUMN MASTER KEY statement
- Always Encrypted, create column master key
ms.assetid: f8926b95-e146-4e3f-b56b-add0c0d0a30e
caps.latest.revision: "32"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 30cf5c83de208992cb36692c0b4b7b07fabf5cb6
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="create-column-master-key-transact-sql"></a>CREATE COLUMN MASTER KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  在資料庫中建立的資料行主要金鑰中繼資料物件。 代表索引鍵，資料行主要金鑰中繼資料項目儲存在外部金鑰存放區，可用來保護 （加密） 資料行加密金鑰時使用[永遠加密 &#40; Database engine&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)功能。 進行金鑰輪替，允許多個資料行主要金鑰定期變更金鑰來加強安全性。 您也可以使用 [物件總管] 中的金鑰存放區和其對應的中繼資料物件在資料庫中建立資料行主要金鑰[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或 PowerShell。 如需詳細資訊，請參閱[的金鑰管理概觀的一律加密](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)。  
  
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
 這是資料庫中，資料行主要金鑰將已知的名稱。  
  
 *key_store_provider_name*  
 指定的金鑰存放區提供者，也就是用戶端軟體元件，可封裝包含資料行主要金鑰的金鑰存放區的名稱。 啟用永遠加密的用戶端驅動程式會使用金鑰存放區提供者名稱，來查閱的金鑰存放區提供者的驅動程式的登錄中的金鑰存放區提供者。 驅動程式會使用提供者來解密儲存在基礎的金鑰存放區中的資料行主要金鑰所保護的資料行加密金鑰。 加密來加密的資料庫資料行，對應的查詢參數，或解密來自加密資料行的查詢結果，則會使用純文字值的資料行加密金鑰。  
  
 啟用一律加密的用戶端驅動程式程式庫包含常用的金鑰存放區的金鑰存放區提供者。   
  
一組可用的提供者取決於型別和用戶端驅動程式的版本。 請參閱特定的驅動程式的永遠加密文件：

[開發應用程式使用一律加密搭配.NET Framework Provider for SQL Server](../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)


以下資料表擷取系統提供者的名稱：  
  
|金鑰存放區提供者名稱|基礎的金鑰存放區|  
    |-----------------------------|--------------------------|
    |' MSSQL_CERTIFICATE_STORE'|Windows 憑證存放區| 
    |' MSSQL_CSP_PROVIDER'|存放區，例如硬體安全性模組 (HSM)，支援 Microsoft CryptoAPI。|
    |' MSSQL_CNG_STORE'|存放區，例如硬體安全性模組 (HSM)，可支援密碼編譯 API： 新一代。|  
    |' Azure_Key_Vault'|請參閱[開始使用 Azure 金鑰保存庫](https://azure.microsoft.com/documentation/articles/key-vault-get-started/)|  
  

 您可以實作自訂金鑰存放區提供者，才能儲存它沒有任何內建金鑰存放區中的資料行主要金鑰存放區提供者啟用永遠加密的用戶端驅動程式中。  請注意，自訂金鑰存放區提供者的名稱不能以 'MSSQL_'，這是前置詞開頭保留供[!INCLUDE[msCoName](../../includes/msconame-md.md)]金鑰存放區提供者。 

  
 key_path  
 存放區中資料行主要金鑰的金鑰路徑。 機碼路徑必須是每個用戶端應用程式預期要加密或解密資料儲存在資料行 （間接） 參考的資料行主要金鑰所保護的內容中有效，而且用戶端應用程式必須能夠存取金鑰。 金鑰存放區提供者特定的金鑰路徑的格式。 下列清單描述特定的 Microsoft 系統金鑰存放區提供者的金鑰路徑的格式。  
  
-   **提供者名稱：** MSSQL_CERTIFICATE_STORE  
  
     **金鑰路徑格式：** *CertificateStoreName*/*CertificateStoreLocation*/*CertificateThumbprint*  
  
     其中：  
  
     *CertificateStoreLocation*  
     憑證存放區位置，必須是目前的使用者或本機電腦。 如需詳細資訊，請參閱[本機電腦和目前使用者憑證存放區](https://msdn.microsoft.com/library/windows/hardware/ff548653.aspx)。  
  
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
     密碼編譯服務提供者 (CSP)，實作 CAPI，資料行主要金鑰存放區的名稱。 如果您使用 HSM 金鑰存放區，這必須是名稱 CSP HSM 廠商提供。 必須在用戶端電腦上安裝提供者。  
  
     *KeyIdentifier*  
     此索引鍵，識別碼作為金鑰存放區中的資料行主要金鑰。  
  
     **範例：**  
  
    ```  
    N'My HSM CSP Provider/AlwaysEncryptedKey1'  
    ```  
  
-   **提供者名稱：** MSSQL_CNG_STORE  
  
     **金鑰路徑格式：** *ProviderName*/*KeyIdentifier*  
  
     其中：  
  
     *ProviderName*  
     名稱的金鑰儲存提供者 (KSP)，它會實作密碼編譯： Next Generation (CNG) API，針對資料行主要金鑰存放區。 如果您使用 HSM 金鑰存放區，這必須是名稱 KSP HSM 廠商提供。 必須在用戶端電腦上安裝提供者。  
  
     *KeyIdentifier*  
     此索引鍵，識別碼作為金鑰存放區中的資料行主要金鑰。  
  
     **範例：**  
  
    ```  
    N'My HSM CNG Provider/AlwaysEncryptedKey1'  
    ```  

-   **提供者名稱：** AZURE_KEY_STORE  
  
     **金鑰路徑格式：** *KeyUrl*  
  
     其中：  
  
     *KeyUrl*  
     Azure 金鑰保存庫中的索引鍵的 URL


範例：
 
`N'https://myvault.vault.azure.net:443/keys/MyCMK/4c05f1a41b12488f9cba2ea964b6a700'`  
  
## <a name="remarks"></a>備註  

需要建立資料行主要金鑰中繼資料項目，才可以建立資料行加密金鑰中繼資料項目，在資料庫中，而且之前可以使用 永遠加密來加密資料庫中的任何資料行。 請注意，中繼資料中的資料行主要金鑰的項目不包含實際的資料行主要金鑰，必須儲存在外部資料行的金鑰存放區 （之外，SQL Server)。 金鑰存放區提供者名稱和資料行主要金鑰中繼資料中的路徑必須是有效的用戶端應用程式能夠使用資料行主要金鑰來解密資料行主要金鑰加密資料行加密金鑰，並查詢加密資料行。


  
## <a name="permissions"></a>Permissions  
 需要**ALTER ANY COLUMN MASTER KEY**權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-creating-a-column-master-key"></a>A. 建立資料行主要金鑰  
 建立資料行主要金鑰儲存在憑證存放區中，使用 MSSQL_CERTIFICATE_STORE 提供者存取資料行主要金鑰的用戶端應用程式的資料行主要金鑰中繼資料項目：  
  
```  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
     KEY_STORE_PROVIDER_NAME = N'MSSQL_CERTIFICATE_STORE',   
     KEY_PATH = 'Current User/Personal/f2260f28d909d21c642a3d8e0b45a830e79a1420'  
   );  
```  
  
 建立資料行主要金鑰所使用的 MSSQL_CNG_STORE 提供者的用戶端應用程式存取的資料行主要金鑰中繼資料項目：  
  
```  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
    KEY_STORE_PROVIDER_NAME = N'MSSQL_CNG_STORE',    
    KEY_PATH = N'My HSM CNG Provider/AlwaysEncryptedKey'  
);  
```  
  
 建立儲存在 Azure 金鑰保存庫，用以 AZURE_KEY_VAULT 提供者存取資料行主要金鑰的用戶端應用程式中的資料行主要金鑰。  
  
```  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
    KEY_STORE_PROVIDER_NAME = N'AZURE_KEY_VAULT',  
    KEY_PATH = N'https://myvault.vault.azure.net:443/keys/  
        MyCMK/4c05f1a41b12488f9cba2ea964b6a700');  
```  
  
 建立自訂的資料行主要金鑰存放區中儲存 CMK:  
  
```  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
    KEY_STORE_PROVIDER_NAME = 'CUSTOM_KEY_STORE',    
    KEY_PATH = 'https://contoso.vault/sales_db_tce_key'  
);  
```  
  
## <a name="see-also"></a>請參閱＜
 
* [卸除資料行主要金鑰 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-column-master-key-transact-sql.md)   
* [CREATE COLUMN ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-column-encryption-key-transact-sql.md)
* [sys.column_master_keys (Transact-SQL)](../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md)
* [永遠加密 &#40;Database Engine&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)  
* [永遠加密的金鑰管理概觀](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)
  
