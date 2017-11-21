---
title: "建立認證 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 01/09/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREDENTIAL_TSQL
- SQL13.SWB.CREDENTIAL.GENERAL.F1
- CREATE CREDENTIAL
- CREATE_CREDENTIAL_TSQL
- CREDENTIAL
dev_langs:
- TSQL
helpviewer_keywords:
- SECRET clause
- authentication [SQL Server], credentials
- CREATE CREDENTIAL statement
- credentials [SQL Server], CREATE CREDENTIAL statement
ms.assetid: d5e9ae69-41d9-4e46-b13d-404b88a32d9d
caps.latest.revision: 51
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 556fa0262696075d63ee549730f2d9824c482dd4
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="create-credential-transact-sql"></a>CREATE CREDENTIAL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  建立伺服器層級的認證。 認證是包含所要連接到 SQL Server 外部資源的驗證資訊的記錄。 大部分認證都包含 Windows 使用者和密碼。 例如，將資料庫備份儲存位置，可能需要提供特殊的認證，才能存取該位置的 SQL Server。 如需詳細資訊，請參閱[認證 (Database Engine)](../../relational-databases/security/authentication-access/credentials-database-engine.md)。
  
> [!NOTE]  
>  若要在資料庫層級使用提供的認證[CREATE DATABASE SCOPED CREDENTIAL &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md). 當您需要多個資料庫伺服器上使用相同的認證，請使用伺服器層級認證。 若要讓資料庫更容易移植使用資料庫範圍認證。 當資料庫移動至新的伺服器時，會隨著一起移動的資料庫範圍認證。 使用資料庫範圍認證上[!INCLUDE[ssSDS](../../includes/sssds-md.md)]。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
CREATE CREDENTIAL credential_name   
WITH IDENTITY = 'identity_name'  
    [ , SECRET = 'secret' ]  
        [ FOR CRYPTOGRAPHIC PROVIDER cryptographic_provider_name ]  
```  
  
## <a name="arguments"></a>引數  
 *credential_name*  
 指定所要建立之認證的名稱。 *credential_name*不能以數字 （#） 符號開頭。 系統認證必須以 ## 為開頭。  當使用共用的存取簽章 (SAS)，此名稱必須符合容器路徑，開頭為 https，而且不能包含正斜線。 請參閱範例 D 下方。  
  
 識別**='***identity_name***'**  
 指定連接到伺服器外部時所要使用的帳戶名稱。 認證用來存取 Azure 金鑰保存庫中，當**識別**金鑰保存庫的名稱。 請參閱以下的範例 C。 認證使用共用的存取簽章 (SAS)，當**識別**是*共用存取簽章*。 請參閱範例 D 下方。  
  
 密碼**='***密碼***'**  
 指定外寄驗證所需的秘密。  
  
 當認證用來存取 Azure 金鑰保存庫**密碼**引數的**CREATE CREDENTIAL**需要*\<用戶端識別碼 >* （不含連字號）和*\<密碼 >*的**服務主體**它們之間不含空格一起傳遞至 Azure Active Directory 中。 請參閱以下的範例 C。 認證使用共用的存取簽章時**密碼**的共用的存取簽章語彙基元。 請參閱範例 D 下方。  如需 Azure 的容器上建立的預存的存取原則和共用的存取簽章資訊，請參閱[第 1 課： 建立 Azure 的容器上的預存的存取原則和共用的存取簽章](../../relational-databases/lesson-1-create-stored-access-policy-and-shared-access-signature.md)。  
  
 密碼編譯提供者*cryptographic_provider_name*  
 指定的名稱*企業金鑰管理 (EKM) 提供者*。 如需有關金鑰管理的詳細資訊，請參閱[可延伸金鑰管理 &#40;EKM &#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md).  
  
## <a name="remarks"></a>備註  

 當 IDENTITY 是 Windows 使用者時，秘密可以是密碼。 秘密是利用服務主要金鑰來加密的。 如果重新產生服務主要金鑰，便會利用新的服務主要金鑰來重新加密秘密。  
  
 建立認證之後, 您可以將它對應至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登入使用[CREATE LOGIN](../../t-sql/statements/create-login-transact-sql.md)或[ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md)。 A[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登入可以對應至一個認證，但單一認證可對應至多個[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登入。 如需詳細資訊，請參閱[認證 &#40; Database engine&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)。 伺服器層級認證只能對應至登入，不到資料庫使用者。 
  
 認證的相關資訊會顯示在[sys.credentials](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)目錄檢視。  
  
 如果提供者沒有任何登入對應認證，系統就會使用對應至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務帳戶的認證。  
  
 一個登入可以具有多個對應認證，只要這些認證用於不同的提供者即可。 但是，每個登入的每個提供者必須只有一個對應認證。 相同的認證可對應至其他登入。  
  
## <a name="permissions"></a>Permissions  
 需要**ALTER ANY CREDENTIAL**權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-basic-example"></a>A. 基本範例  
 下列範例會建立一個稱為 `AlterEgo` 的認證。 這個認證包含 Windows 使用者 `Mary5` 和密碼。  
  
```  
CREATE CREDENTIAL AlterEgo WITH IDENTITY = 'Mary5',   
    SECRET = '<EnterStrongPasswordHere>';  
GO  
```  
  
### <a name="b-creating-a-credential-for-ekm"></a>B. 建立 EKM 的認證  
 下列範例會透過 EKM 的管理工具 (包含基本帳戶類型和密碼)，在 EKM 模組上使用之前建立的帳戶 `User1OnEKM`。 **Sysadmin**帳戶在伺服器上的建立的認證用來連接 EKM 帳戶，並將其指派給`User1`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]帳戶：  
  
```  
CREATE CREDENTIAL CredentialForEKM  
    WITH IDENTITY='User1OnEKM', SECRET='<EnterStrongPasswordHere>'  
    FOR CRYPTOGRAPHIC PROVIDER MyEKMProvider;  
GO  
  
/* Modify the login to assign the cryptographic provider credential */  
ALTER LOGIN Login1  
ADD CREDENTIAL CredentialForEKM;  
  
/* Modify the login to assign a non cryptographic provider credential */   
ALTER LOGIN Login1  
WITH CREDENTIAL = AlterEgo;  
GO  
```  
  
### <a name="c-creating-a-credential-for-ekm-using-the-azure-key-vault"></a>C. 使用 Azure 金鑰保存庫建立 EKM 的認證  
 下列範例會建立[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]認證，以供[!INCLUDE[ssDE](../../includes/ssde-md.md)]用於存取 Azure 金鑰保存庫使用**SQL Server Connector for Microsoft Azure Key Vault**。 如需完整的使用範例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]連接器，請參閱[可延伸使用 Azure 金鑰保存庫金鑰管理 &#40;SQL Server &#41;](../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md).  
  
> [!IMPORTANT]  
>  **CREATE CREDENTIAL** 的 **IDENTITY** 引數需要金鑰保存庫名稱。 **密碼**引數的**CREATE CREDENTIAL**需要*\<用戶端識別碼 >* （不含連字號） 和*\<密碼 >*它們之間不含空格一起傳遞。  
  
 在下列範例中， **用戶端識別碼** (`EF5C8E09-4D2A-4A76-9998-D93440D8115D`) 已移除連字號並以字串 `EF5C8E094D2A4A769998D93440D8115D` 輸入，而 **密碼** 會以字串 *SECRET_DBEngine*來表示。  
  
```  
USE master;  
CREATE CREDENTIAL Azure_EKM_TDE_cred   
    WITH IDENTITY = 'ContosoKeyVault',   
    SECRET = 'EF5C8E094D2A4A769998D93440D8115DSECRET_DBEngine'   
    FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov ;  
```  
  
 下列範例會建立相同的認證使用的變數**用戶端識別碼**和**密碼**字串，然後串連在一起以表單**密碼**引數。 **取代**函數用來從用戶端識別碼移除連字號  
  
```  
DECLARE @AuthClientId uniqueidentifier = 'EF5C8E09-4D2A-4A76-9998-D93440D8115D';  
DECLARE @AuthClientSecret varchar(200) = 'SECRET_DBEngine';  
DECLARE @pwd varchar(max) = REPLACE(CONVERT(varchar(36), @AuthClientId) , '-', '') + @AuthClientSecret;  
  
EXEC ('CREATE CREDENTIAL Azure_EKM_TDE_cred   
    WITH IDENTITY = 'ContosoKeyVault', SECRET = ''' + @PWD + '''   
    FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov ;');  
```  
  
### <a name="d-creating-a-credential-using-a-sas-token"></a>D. 建立使用 SAS 權杖的認證  
 **適用於**:[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]透過[新版](http://go.microsoft.com/fwlink/p/?LinkId=299658)。  
  
 下列範例會建立共用的存取簽章憑證使用 SAS 權杖。  如需 Azure 的容器上建立預存的存取原則和共用的存取簽章，然後再建立認證，使用共用的存取簽章的教學課程，請參閱[教學課程： 使用 SQL Server 2016 的 Microsoft Azure Blob 儲存體服務資料庫](Tutorial:%20Using%20the%20Microsoft%20Azure%20Blob%20storage%20service%20with%20SQL%20Server%202016%20databases.md)。  
  
> [!IMPORTANT]  
>  **認證名稱**引數需要的名稱符合容器路徑，開頭為 https，而且不能包含尾端斜線。 **識別**引數需要有名稱、*共用存取簽章*。 **密碼**引數需要共用的存取簽章 token。  
  
```  
USE master  
CREATE CREDENTIAL [https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>] -- this name must match the container path, start with https and must not contain a trailing forward slash.  
   WITH IDENTITY='SHARED ACCESS SIGNATURE' -- this is a mandatory string and do not change it.   
   , SECRET = 'sharedaccesssignature' –- this is the shared access signature token   
GO    
```  
  
## <a name="see-also"></a>另請參閱  
 [認證 &#40; Database engine&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [ALTER CREDENTIAL &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-credential-transact-sql.md)   
 [卸除認證 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-credential-transact-sql.md)   
 [建立 DATABASE SCOPED CREDENTIAL &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)   
 [sys.credentials &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)   
 [第 2 課： 建立使用共用的存取簽章的 SQL Server 認證](../../relational-databases/lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md)   
 [共用的存取簽章](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)  
  
  

