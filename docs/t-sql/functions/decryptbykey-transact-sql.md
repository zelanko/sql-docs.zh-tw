---
title: DECRYPTBYKEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DecryptByKey_TSQL
- DECRYPTBYKEY
dev_langs:
- TSQL
helpviewer_keywords:
- symmetric keys [SQL Server], DecryptByKey function
- decryption [SQL Server], keys
- decryption [SQL Server], symmetric keys
- DECRYPTBYKEY function
ms.assetid: 6edf121f-ac62-4dae-90e6-6938f32603c9
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: e67c362ba45a7b70b252eb011ec0ee1e24e54888
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85682435"
---
# <a name="decryptbykey-transact-sql"></a>DECRYPTBYKEY (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

此函式會使用對稱金鑰為資料解密。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```syntaxsql
  
DecryptByKey ( { 'ciphertext' | @ciphertext }   
    [ , add_authenticator, { authenticator | @authenticator } ] )  
```  
  
## <a name="arguments"></a>引數  
*ciphertext*  
**varbinary** 類型的變數，其中包含以金鑰加密的資料。  
  
**\@ciphertext**  
**varbinary** 類型的變數，其中包含以金鑰加密的資料。  
  
 *add_authenticator*  
指出原始加密程序是否隨純文字一同包含及加密驗證器。 必須符合資料加密期間傳遞至 [ENCRYPTBYKEY (Transact-SQL)](./encryptbykey-transact-sql.md) 的值。 *add_authenticator* 具有 **int** 資料類型。  
  
 *authenticator*  
作為驗證器產生基礎使用的資料。 必須符合提供給 [ENCRYPTBYKEY (Transact-SQL)](./encryptbykey-transact-sql.md) 的值。 *authenticator* 具有 **sysname** 資料類型。  

**\@authenticator**  
含有驗證器從中產生之資料的變數。 必須符合提供給 [ENCRYPTBYKEY (Transact-SQL)](./encryptbykey-transact-sql.md) 的值。 *\@authenticator* 具有 **sysname** 資料類型。  

## <a name="return-types"></a>傳回型別  
**varbinary**，大小上限為 8,000 個位元組。 如果未開啟用於資料加密的對稱金鑰，或「加密文字」`DECRYPTBYKEY`*為 NULL，則*  會傳回 NULL。  
  
## <a name="remarks"></a>備註  
`DECRYPTBYKEY` 使用對稱金鑰。 資料庫必須已開啟此對稱金鑰。 `DECRYPTBYKEY` 允許同時開啟多個金鑰。 加密文字解密之前，您不需要立即開啟金鑰。  
  
對稱式加密和解密運作起來通常較快，而且非常適合涉及大量資料的作業。  

`DECRYPTBYKEY` 呼叫必須發生於包含加密金鑰的資料庫內容中。 從位於資料庫的物件 (例如，檢視、預存程序或函數) 中呼叫 `DECRYPTBYKEY` 來確保這一點。 
  
## <a name="permissions"></a>權限  
目前的工作階段中必須已開啟對稱金鑰。 如需詳細資訊，請參閱 [OPEN SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/open-symmetric-key-transact-sql.md)。  
  
## <a name="examples"></a>範例  
  
### <a name="a-decrypting-by-using-a-symmetric-key"></a>A. 使用對稱金鑰來解密  
此範例會使用對稱金鑰來解密加密文字。  
  
```sql  
-- First, open the symmetric key with which to decrypt the data.  
OPEN SYMMETRIC KEY SSN_Key_01  
   DECRYPTION BY CERTIFICATE HumanResources037;  
GO  
  
-- Now list the original ID, the encrypted ID, and the   
-- decrypted ciphertext. If the decryption worked, the original  
-- and the decrypted ID will match.  
SELECT NationalIDNumber, EncryptedNationalID   
    AS 'Encrypted ID Number',  
    CONVERT(nvarchar, DecryptByKey(EncryptedNationalID))   
    AS 'Decrypted ID Number'  
    FROM HumanResources.Employee;  
GO  
```  
  
### <a name="b-decrypting-by-using-a-symmetric-key-and-an-authenticating-hash"></a>B. 使用對稱金鑰和驗證雜湊來解密  
此範例會解密原本隨驗證器一同加密的資料。  
  
```sql  
-- First, open the symmetric key with which to decrypt the data  
OPEN SYMMETRIC KEY CreditCards_Key11  
   DECRYPTION BY CERTIFICATE Sales09;  
GO  
  
-- Now list the original card number, the encrypted card number,  
-- and the decrypted ciphertext. If the decryption worked,   
-- the original number will match the decrypted number.  
SELECT CardNumber, CardNumber_Encrypted   
    AS 'Encrypted card number', CONVERT(nvarchar,  
    DecryptByKey(CardNumber_Encrypted, 1 ,   
    HashBytes('SHA1', CONVERT(varbinary, CreditCardID))))   
    AS 'Decrypted card number' FROM Sales.CreditCard;  
GO  
  
```  

### <a name="c-fail-to-decrypt-when-not-in-the-context-of-database-with-key"></a>C. 無法在不含金鑰的資料庫內容中解密
下列範例示範 `DECRYPTBYKEY` 必須在包含金鑰的資料庫內容中執行。 在 Master 資料庫中執行 `DECRYPTBYKEY` 時，不會將資料列解密；結果為 NULL。 

```sql
-- Create the database
CREATE DATABASE TestingDecryptByKey
GO

USE [TestingDecryptByKey]

-- Create the table and view
CREATE TABLE TestingDecryptByKey.dbo.Test(val VARBINARY(8000) NOT NULL);
GO
CREATE VIEW dbo.TestView AS SELECT CAST(DecryptByKey(val) AS VARCHAR(30)) AS DecryptedVal FROM TestingDecryptByKey.dbo.Test;
GO

-- Create the key, and certificate
USE TestingDecryptByKey;
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'ItIsreallyLong1AndSecured!Passsword#';
CREATE CERTIFICATE TestEncryptionCertificate WITH SUBJECT = 'TestEncryption';
CREATE SYMMETRIC KEY TestEncryptSymmmetricKey WITH ALGORITHM = AES_256, IDENTITY_VALUE = 'It is place for test',
KEY_SOURCE = 'It is source for test' ENCRYPTION BY CERTIFICATE TestEncryptionCertificate;

-- Insert rows into the table
DECLARE @var VARBINARY(8000), @Val VARCHAR(30);
SELECT @Val = '000-123-4567';
OPEN SYMMETRIC KEY TestEncryptSymmmetricKey DECRYPTION BY CERTIFICATE TestEncryptionCertificate;
SELECT @var = EncryptByKey(Key_GUID('TestEncryptSymmmetricKey'), @Val);
SELECT CAST(DecryptByKey(@var) AS VARCHAR(30)), @Val;
INSERT INTO dbo.Test VALUES(@var);
GO

-- Switch to master
USE [Master];
GO

-- Results show the date inserted
SELECT DecryptedVal FROM TestingDecryptByKey.dbo.TestView;

-- Results are NULL because we are not in the context of the TestingDecryptByKey Database
SELECT CAST(DecryptByKey(val) AS VARCHAR(30)) AS DecryptedVal FROM TestingDecryptByKey.dbo.Test;
GO

-- Clean up resources
USE TestingDecryptByKey;

DROP SYMMETRIC KEY TestEncryptSymmmetricKey REMOVE PROVIDER KEY;
DROP CERTIFICATE TestEncryptionCertificate;

Use [Master]
DROP DATABASE TestingDecryptByKey;
GO
```

  
## <a name="see-also"></a>另請參閱  
 [ENCRYPTBYKEY &#40;Transact-SQL&#41;](../../t-sql/functions/encryptbykey-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [ALTER SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-symmetric-key-transact-sql.md)   
 [DROP SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-symmetric-key-transact-sql.md)   
 [加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [選擇加密演算法](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)  
  
  
