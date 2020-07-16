---
title: BACKUP CERTIFICATE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/16/2020
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DUMP_CERTIFICATE_TSQL
- BACKUP CERTIFICATE
- sql13.swb.exportcertificate.f1
- DUMP CERTIFICATE
- BACKUP_CERTIFICATE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- encryption [SQL Server], certificates
- decryption [SQL Server], certificates
- exporting certificates
- certificates [SQL Server], exporting
- BACKUP CERTIFICATE statement
- backing up certificates [SQL Server]
- decryption [SQL Server]
- cryptography [SQL Server], certificates
ms.assetid: 509b9462-819b-4c45-baae-3d2d90d14a1c
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azure-sqldw-latest'
ms.openlocfilehash: 734de238f38520ad31923a9d4ed45edd5d807336
ms.sourcegitcommit: b2ab989264dd9d23c184f43fff2ec8966793a727
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/14/2020
ms.locfileid: "86380931"
---
# <a name="backup-certificate-transact-sql"></a>BACKUP CERTIFICATE (Transact-SQL)
[!INCLUDE [sql-asa-pdw](../../includes/applies-to-version/sql-asa-pdw.md)]

  將憑證匯出至檔案。  
  
 ![連結圖示](../../database-engine/configure-windows/media/topic-link.gif "連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```syntaxsql
-- Syntax for SQL Server  
  
BACKUP CERTIFICATE certname TO FILE = 'path_to_file'  
    [ WITH PRIVATE KEY   
      (   
        FILE = 'path_to_private_key_file' ,  
        ENCRYPTION BY PASSWORD = 'encryption_password'   
        [ , DECRYPTION BY PASSWORD = 'decryption_password' ]   
      )   
    ]  
```  
  
> [!Note]
> [!INCLUDE [Synapse preview note](../../includes/synapse-preview-note.md)]
   
```syntaxsql
-- Syntax for Azure Synapse Analytics and Parallel Data Warehouse  
  
BACKUP CERTIFICATE certname TO FILE ='path_to_file'  
      WITH PRIVATE KEY   
      (   
        FILE ='path_to_private_key_file',  
        ENCRYPTION BY PASSWORD ='encryption_password'   
      )   
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數
 *certname*  
 這是要備份的憑證名稱。

 TO FILE = '*path_to_file*'  
 指定儲存憑證的檔案之完整路徑，包括檔案名稱。 此路徑可以是本機路徑或通往網路位置的 UNC 路徑。 如果只指定檔案名稱，檔案將會儲存在執行個體的預設使用者資料夾 (它不一定是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DATA 資料夾)。 如果是 SQL Server Express LocalDB，執行個體的預設使用者資料夾是 `%USERPROFILE%` 環境變數為建立該執行個體的帳戶所指定路徑。  

 WITH PRIVATE KEY 指定憑證的私密金鑰要儲存到檔案。 這個子句是選擇性的。

 FILE = '*path_to_private_key_file*'  
 指定儲存私密金鑰的檔案之完整路徑，包括檔案名稱。 此路徑可以是本機路徑或通往網路位置的 UNC 路徑。 如果只指定檔案名稱，檔案將會儲存在執行個體的預設使用者資料夾 (它不一定是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DATA 資料夾)。 如果是 SQL Server Express LocalDB，執行個體的預設使用者資料夾是 `%USERPROFILE%` 環境變數為建立該執行個體的帳戶所指定路徑。  

 ENCRYPTION BY PASSWORD = '*encryption_password*'  
 這是將私密金鑰寫入備份檔之前用來加密該金鑰的密碼。 這個密碼必須遵守複雜性檢查。  
  
 DECRYPTION BY PASSWORD = '*decryption_password*'  
 這是備份私密金鑰之前用來解密該金鑰的密碼。 如果憑證由主要金鑰加密，則不需要此引數。 
  
## <a name="remarks"></a>備註  
 如果是在資料庫中利用密碼加密私密金鑰，則必須指定解密密碼。  
  
 將私密金鑰備份至檔案時，需要加密。 用以保護檔案中私密金鑰的密碼與用以加密資料庫中憑證之私密金鑰的密碼並不相同。  

 私密金鑰會以 PVK 檔案格式儲存。

 若要在使用或不使用私密金鑰的情況下還原備份憑證，請使用 [CREATE CERTIFICATE](../../t-sql/statements/create-certificate-transact-sql.md) 陳述式。
 
 若要將私密金鑰還原至資料庫中現有的憑證，請使用 [ALTER CERTIFICATE](../../t-sql/statements/alter-certificate-transact-sql.md) 陳述式。
 
 當執行備份時，該檔案對於 SQL Server 執行個體的服務帳戶將會套用存取控制清單。 如果您要將憑證還原到在其他帳戶下執行的伺服器，您將需要調整檔案的權限，這樣新帳戶才能讀取它們。 
  
## <a name="permissions"></a>權限  
 需要憑證的 CONTROL 權限，且必須知道用來加密私密金鑰的密碼。 如果只備份憑證的公開部份，此命令需要憑證的某些權限，且未對呼叫端拒絕憑證的 VIEW 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-exporting-a-certificate-to-a-file"></a>A. 將憑證匯出至檔案  
 下列範例將憑證匯出至檔案。  
  
```sql
BACKUP CERTIFICATE sales05 TO FILE = 'c:\storedcerts\sales05cert';  
GO  
```  
  
### <a name="b-exporting-a-certificate-and-a-private-key"></a>B. 匯出憑證和私密金鑰  
 在下列範例中，會利用密碼 `997jkhUbhk$w4ez0876hKHJH5gh` 加密所備份的憑證私密金鑰。  
  
```sql
BACKUP CERTIFICATE sales05 TO FILE = 'c:\storedcerts\sales05cert'  
    WITH PRIVATE KEY ( FILE = 'c:\storedkeys\sales05key' ,   
    ENCRYPTION BY PASSWORD = '997jkhUbhk$w4ez0876hKHJH5gh' );  
GO  
```  
  
### <a name="c-exporting-a-certificate-that-has-an-encrypted-private-key"></a>C. 匯出含有加密私密金鑰的憑證  
 在下列範例中，憑證的私密金鑰是在資料庫中加密的。 必須利用密碼 `9875t6#6rfid7vble7r` 來解密私密金鑰。 當憑證儲存至備份檔時，會利用密碼 `9n34khUbhk$w4ecJH5gh` 加密私密金鑰。  
  
```sql
BACKUP CERTIFICATE sales09 TO FILE = 'c:\storedcerts\sales09cert'   
    WITH PRIVATE KEY ( DECRYPTION BY PASSWORD = '9875t6#6rfid7vble7r' ,  
    FILE = 'c:\storedkeys\sales09key' ,   
    ENCRYPTION BY PASSWORD = '9n34khUbhk$w4ecJH5gh' );  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [ALTER CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-certificate-transact-sql.md)   
 [DROP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-certificate-transact-sql.md)  
 [CERTENCODED &#40;Transact-SQL&#41;](../../t-sql/functions/certencoded-transact-sql.md)  
 [CERTPRIVATEKEY &#40;Transact-SQL&#41;](../../t-sql/functions/certprivatekey-transact-sql.md)  
 [CERT_ID &#40;Transact-SQL&#41;](../../t-sql/functions/cert-id-transact-sql.md)  
 [CERTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/certproperty-transact-sql.md)  
  
  

