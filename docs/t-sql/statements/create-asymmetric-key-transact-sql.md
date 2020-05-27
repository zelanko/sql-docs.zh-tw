---
title: CREATE ASYMMETRIC KEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/23/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ASYMMETRIC_KEY_TSQL
- CREATE ASYMMETRIC KEY
- CREATE_ASYMMETRIC_KEY_TSQL
- ASYMMETRIC KEY
dev_langs:
- TSQL
helpviewer_keywords:
- asymmetric keys [SQL Server], creating
- encryption [SQL Server], asymmetric keys
- CREATE ASYMMETRIC KEY statement
- asymmetric keys [SQL Server]
- cryptography [SQL Server], asymmetric keys
ms.assetid: 141bc976-7631-49f6-82bd-a235028645b1
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 009029f16d85fa82867f37e075066701dacfc375
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "73064696"
---
# <a name="create-asymmetric-key-transact-sql"></a>CREATE ASYMMETRIC KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  在資料庫中建立非對稱金鑰。  
  
 此功能與使用資料層應用程式架構 (DACFx) 的資料庫匯出不相容。 您必須在匯出之前先卸除所有非對稱金鑰。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
CREATE ASYMMETRIC KEY asym_key_name   
   [ AUTHORIZATION database_principal_name ]  
   [ FROM <asym_key_source> ]  
   [ WITH <key_option> ] 
   [ ENCRYPTION BY <encrypting_mechanism> ] 
   [ ; ]
  
<asym_key_source>::=  
     FILE = 'path_to_strong-name_file'  
   | EXECUTABLE FILE = 'path_to_executable_file'  
   | ASSEMBLY assembly_name  
   | PROVIDER provider_name  
  
<key_option> ::=  
   ALGORITHM = <algorithm>  
      |  
   PROVIDER_KEY_NAME = 'key_name_in_provider'  
      |  
      CREATION_DISPOSITION = { CREATE_NEW | OPEN_EXISTING }  
  
<algorithm> ::=  
      { RSA_4096 | RSA_3072 | RSA_2048 | RSA_1024 | RSA_512 }   
  
<encrypting_mechanism> ::=  
    PASSWORD = 'password'   
```  
  
## <a name="arguments"></a>引數  
 *asym_key_name*  
 這是資料庫中非對稱金鑰的名稱。 非對稱金鑰名稱必須符合[識別碼](../../relational-databases/databases/database-identifiers.md)的規則，且在資料庫內必須是唯一的。  

 AUTHORIZATION *database_principal_name*  
 指定非對稱金鑰的擁有者。 該擁有者不能是角色或群組。 如果省略了這個選項，該擁有者便是目前的使用者。  
  
 FROM *asym_key_source*  
 指定載入非對稱金鑰組時所在的來源。  
  
 FILE = '*path_to_strong-name_file*'  
 指定載入金鑰組時所在的強式名稱檔案之路徑。 根據 Windows API 的 MAX_PATH，限制為 260 個字元。  
  
> [!NOTE]  
>  自主資料庫無法使用這個選項。  
  
 EXECUTABLE FILE = '*path_to_executable_file*'  
 指定要從中載入公開金鑰的組件檔案路徑。 根據 Windows API 的 MAX_PATH，限制為 260 個字元。  
  
> [!NOTE]  
>  自主資料庫無法使用這個選項。  
  
 ASSEMBLY *assembly_name*  
 指定已簽署的組件名稱，此組件已經載入至要從中載入公開金鑰的資料庫。  
  
 PROVIDER *provider_name*  
 指定可延伸金鑰管理 (EKM) 提供者的名稱。 您必須先使用 CREATE PROVIDER 陳述式定義提供者。 如需外部金鑰管理的詳細資訊，請參閱[可延伸金鑰管理 &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)。  
  
 ALGORITHM = \<algorithm>  
 可提供五種演算法；RSA_4096、RSA_3072、RSA_2048、RSA_1024 和 RSA_512。  
  
 RSA_1024 和 RSA_512 即將淘汰。 若要使用 RSA_1024 或 RSA_512 (不建議)，您必須將資料庫相容性層級設定為 120 或更低。  
  
 PROVIDER_KEY_NAME = '*key_name_in_provider*'  
 從外部提供者指定金鑰名稱。  
  
 CREATION_DISPOSITION = CREATE_NEW  
 在可延伸金鑰管理裝置上建立新的金鑰。 PROVIDER_KEY_NAME 必須用於指定裝置上的金鑰名稱。 如果金鑰已存在於裝置上，陳述式會失敗，並傳回錯誤。  
  
 CREATION_DISPOSITION = OPEN_EXISTING  
 將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 非對稱金鑰對應至現有的「可延伸金鑰管理」金鑰。 PROVIDER_KEY_NAME 必須用於指定裝置上的金鑰名稱。 如果未提供 CREATION_DISPOSITION = OPEN_EXISTING，預設值就是 CREATE_NEW。  
  
 ENCRYPTION BY PASSWORD = '*password*'  
 指定用來加密私密金鑰的密碼。 如果這個子句不存在，此私密金鑰將會使用資料庫主要金鑰來加密。 *password* 的上限為 128 個字元。 *password* 必須符合執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體之電腦的 Windows 密碼原則需求。  
  
## <a name="remarks"></a>備註  
 「非對稱金鑰」  是資料庫層級的安全性實體。 在它的預設格式中，這個實體同時包含公開金鑰和私密金鑰。 如果執行時不使用 FROM 子句，CREATE ASYMMETRIC KEY 會產生新金鑰組。 如果執行時使用 FROM 子句，CREATE ASYMMETRIC KEY 就會從檔案匯入金鑰組，或是從組件或 DLL 檔案匯入公開金鑰。  
  
 依預設，私密金鑰由資料庫主要金鑰保護。 如果尚未建立資料庫主要金鑰，則需要利用密碼保護私密金鑰。  
  
 私密金鑰的長度可以是 512、1024 或 2048 位元。  
  
## <a name="permissions"></a>權限  
 需要資料庫的 CREATE ASYMMETRIC KEY 權限。 如果指定了 AUTHORIZATION 子句，則需要資料庫主體的 IMPERSONATE 權限或應用程式角色的 ALTER 權限。 只有 Windows 登入、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入及應用程式角色可以擁有非對稱金鑰。 群組和角色無法擁有非對稱金鑰。  
  
## <a name="examples"></a>範例  
  
### <a name="a-creating-an-asymmetric-key"></a>A. 建立非對稱金鑰  
 下列範例會利用 `PacificSales09` 演算法建立一個名稱為 `RSA_2048` 的非對稱金鑰，並利用密碼保護私密金鑰。  
  
```sql  
CREATE ASYMMETRIC KEY PacificSales09   
    WITH ALGORITHM = RSA_2048   
    ENCRYPTION BY PASSWORD = '<enterStrongPasswordHere>';   
GO  
```  
  
### <a name="b-creating-an-asymmetric-key-from-a-file-giving-authorization-to-a-user"></a>B. 從檔案建立非對稱金鑰，並提供授權給使用者  
 下列範例會從儲存在檔案中的金鑰組建立非對稱金鑰 `PacificSales19`，然後將非對稱金鑰的擁有權指派給使用者 `Christina`。 私密金鑰會受到資料庫主要金鑰所保護，其必須在建立非對稱金鑰之前建立。  
  
```sql  
CREATE ASYMMETRIC KEY PacificSales19  
    AUTHORIZATION Christina  
    FROM FILE = 'c:\PacSales\Managers\ChristinaCerts.tmp';  
GO  
```  
  
### <a name="c-creating-an-asymmetric-key-from-an-ekm-provider"></a>C. 從 EKM 提供者建立非對稱金鑰  
 下列範例會從稱為 `EKM_Provider1` 的可延伸金鑰管理提供者中所儲存的金鑰組來建立非對稱金鑰 `EKM_askey1`，並在稱為 `key10_user1` 的提供者上建立金鑰。  
  
```sql  
CREATE ASYMMETRIC KEY EKM_askey1   
    FROM PROVIDER EKM_Provider1  
    WITH   
        ALGORITHM = RSA_2048,   
        CREATION_DISPOSITION = CREATE_NEW  
        , PROVIDER_KEY_NAME  = 'key10_user1' ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [ALTER ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-asymmetric-key-transact-sql.md)  
 [DROP ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-asymmetric-key-transact-sql.md)  
 [ASYMKEYPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/asymkeyproperty-transact-sql.md)  
 [ASYMKEY_ID &#40;Transact-SQL&#41;](../../t-sql/functions/asymkey-id-transact-sql.md)  
 [選擇加密演算法](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)  
 [加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)  
 [使用 Azure 金鑰保存庫進行可延伸金鑰管理 &#40;SQL Server&#41;](../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
  
  
