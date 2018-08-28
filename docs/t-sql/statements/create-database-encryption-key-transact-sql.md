---
title: CREATE DATABASE ENCRYPTION KEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/24/2016
ms.prod: sql
ms.prod_service: pdw, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DATABASE_ENCRYPTION_KEY_TSQL
- ENCRYPTION_KEY_TSQL
- sql13.swb.dbencryptionkeyo.f1
- ENCRYPTION KEY
- DATABASE ENCRYPTION KEY
- CREATE_DATABASE_ENCRYPTION_KEY_TSQL
- CREATE DATABASE ENCRYPTION KEY
- sql13.swb.dbencryptionkeyg.f1
- CREATE DATABASE ENCRYPTION
- CREATE_DATABASE_ENCRYPTION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- database encryption key
- CREATE DATABASE ENCRYPTION KEY statement
- database encryption key, create
ms.assetid: 2ee95a32-5140-41bd-9ab3-a947b9990688
caps.latest.revision: 30
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f476a600f4072599b23951e7b8470943ca751d5a
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43071928"
---
# <a name="create-database-encryption-key-transact-sql"></a>CREATE DATABASE ENCRYPTION KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

 建立用於以透明方式加密資料庫的加密金鑰。 如需透明資料庫加密的詳細資訊，請參閱[透明資料加密 &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md)。  
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for SQL Server  

CREATE DATABASE ENCRYPTION KEY  
       WITH ALGORITHM = { AES_128 | AES_192 | AES_256 | TRIPLE_DES_3KEY }  
   ENCRYPTION BY SERVER   
    {  
        CERTIFICATE Encryptor_Name |  
        ASYMMETRIC KEY Encryptor_Name  
    }  
[ ; ]  
```  
  
```  
-- Syntax for Parallel Data Warehouse  

CREATE DATABASE ENCRYPTION KEY  
       WITH ALGORITHM = { AES_128 | AES_192 | AES_256 | TRIPLE_DES_3KEY }  
   ENCRYPTION BY SERVER CERTIFICATE Encryptor_Name   
[ ; ]  
```  
  
## <a name="arguments"></a>引數  
WITH ALGORITHM = { AES_128 | AES_192 | AES_256 | TRIPLE_DES_3KEY  }  
指定用於加密金鑰的加密演算法。   
>  [!NOTE]
>    開頭為 SQL Server 2016，所有 AES_128、AES_192 和 AES_256 以外的演算法均已淘汰。 若要使用較舊的演算法 (不建議使用)，您必須將資料庫相容性層級設定為 120 或更低。  
  
ENCRYPTION BY SERVER CERTIFICATE Encryptor_Name  
指定用於加密資料庫加密金鑰之加密程式的名稱。  
  
ENCRYPTION BY SERVER ASYMMETRIC KEY Encryptor_Name  
指定用於加密資料庫加密金鑰之非對稱金鑰的名稱。 為了利用非對稱金鑰加密資料庫加密金鑰，非對稱金鑰必須位在可延伸金鑰管理提供者上。  
  
## <a name="remarks"></a>Remarks  
您需要具備資料庫加密金鑰，資料庫才可以使用「資料庫透明加密」(TDE) 進行加密。 當資料庫以透明方式進行加密時，會在檔案層級加密整個資料庫，而不需要修改任何特殊的程式碼。 用於加密資料庫加密金鑰的憑證或非對稱金鑰必須位於 master 系統資料庫中。  
  
資料庫加密陳述式僅允許用於使用者資料庫。  
  
資料庫加密金鑰無法從資料庫匯出。 只有系統、擁有伺服器偵錯權限的使用者，以及可存取加密和解密資料庫加密金鑰之憑證的使用者可以進行匯出。  
  
變更資料庫擁有者 (dbo) 時，不需要重新產生資料庫加密金鑰。  
  
[!INCLUDE[ssSDS](../../includes/sssds-md.md)] 資料庫會自動建立資料庫加密金鑰。 您不需要使用 CREATE DATABASE ENCRYPTION KEY 陳述式來建立金鑰。  
  
## <a name="permissions"></a>[權限]  
需要資料庫的 CONTROL 權限，以及用於加密資料庫加密金鑰之憑證或非對稱金鑰的 VIEW DEFINITION 權限。  
  
## <a name="examples"></a>範例  
如需使用 TDE 的其他範例，請參閱[透明資料加密 &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md)、[使用 EKM 在 SQL Server 上啟用 TDE](../../relational-databases/security/encryption/enable-tde-on-sql-server-using-ekm.md) 和[使用 Azure Key Vault 進行可延伸金鑰管理 &#40;SQL Server&#41;](../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)。  
  
下列範例會利用 `AES_256` 演算法建立一個資料庫加密金鑰，並且使用名稱為 `MyServerCert` 的憑證保護私密金鑰。  
  
```  
USE AdventureWorks2012;  
GO  
CREATE DATABASE ENCRYPTION KEY  
WITH ALGORITHM = AES_256  
ENCRYPTION BY SERVER CERTIFICATE MyServerCert;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
[透明資料加密 &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md)   
[SQL Server 加密](../../relational-databases/security/encryption/sql-server-encryption.md)   
[SQL Server 和資料庫加密金鑰 &#40;Database Engine&#41;](../../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)   
[加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)   
[ALTER DATABASE SET 選項 &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
[ALTER DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-encryption-key-transact-sql.md)   
[DROP DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-encryption-key-transact-sql.md)   
[sys.dm_database_encryption_keys &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md)  
    
