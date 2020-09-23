---
description: DECRYPTBYKEYAUTOCERT (Transact-SQL)
title: DECRYPTBYKEYAUTOCERT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/09/2015
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DECRYPTBYKEYAUTOCERT
- DECRYPTBYKEYAUTOCERT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DECRYPTBYKEYAUTOCERT function
ms.assetid: 6b45fa2e-ffaa-46f7-86ff-5624596eda4a
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: e45c856ee8ce1942840f47f5878de57525426c94
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/23/2020
ms.locfileid: "91111085"
---
# <a name="decryptbykeyautocert-transact-sql"></a>DECRYPTBYKEYAUTOCERT (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

此函式使用對稱金鑰將資料解密。 該對稱金鑰會使用憑證來自動解密。  

 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```syntaxsql
DecryptByKeyAutoCert ( cert_ID , cert_password   
    , { 'ciphertext' | @ciphertext }  
  [ , { add_authenticator | @add_authenticator }   
  [ , { authenticator | @authenticator } ] ] )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數
 *cert_ID*  
用來保護對稱金鑰的憑證識別碼。 *cert_ID* 具有 **int** 資料類型。  
  
*cert_password*  
用來加密憑證私密金鑰的密碼。 如果以資料庫主要金鑰來保護私密金鑰，則可以有 `NULL` 值。 *cert_password* 具有 **nvarchar** 資料類型。  

'*ciphertext*'  
以金鑰加密的資料字串。 *ciphertext* 具有 **varbinary** 資料類型。  

@ciphertext  
**varbinary** 類型的變數，其中包含以金鑰加密的資料。  

*add_authenticator*  
指出原始加密程序是否隨純文字一同包含及加密驗證器。 必須符合資料加密期間傳遞至 [ENCRYPTBYKEY (Transact-SQL)](./encryptbykey-transact-sql.md) 的值。 如果加密程序使用驗證器，則 *add_authenticator* 的值為 1。 *add_authenticator* 具有 **int** 資料類型。  
  
@add_authenticator  
指出原始加密程序是否隨純文字一同包含及加密驗證器的變數。 必須符合資料加密期間傳遞至 [ENCRYPTBYKEY (Transact-SQL)](./encryptbykey-transact-sql.md) 的值。 *\@add_authenticator* 具有 **int** 資料類型。  
  
*authenticator*  
作為驗證器產生基礎使用的資料。 必須符合提供給 [ENCRYPTBYKEY (Transact-SQL)](./encryptbykey-transact-sql.md) 的值。 *authenticator* 具有 **sysname** 資料類型。  
  
@authenticator  
含有驗證器從中產生之資料的變數。 必須符合提供給 [ENCRYPTBYKEY (Transact-SQL)](./encryptbykey-transact-sql.md) 的值。 *\@authenticator* 具有 **sysname** 資料類型。  
  
## <a name="return-types"></a>傳回型別  
**varbinary**，大小上限為 8,000 個位元組。  
  
## <a name="remarks"></a>備註  
`DECRYPTBYKEYAUTOCERT` 會結合 `OPEN SYMMETRIC KEY` 和 `DECRYPTBYKEY` 的功能。 在單一作業中，它會先將對稱金鑰解密，再使用該金鑰將加密文字解密。  
  
## <a name="permissions"></a>權限  
需要對稱金鑰的 `VIEW DEFINITION` 權限和憑證的 `CONTROL` 權限。   
  
## <a name="examples"></a>範例  
此範例示範 `DECRYPTBYKEYAUTOCERT` 如何簡化解密程式碼。 此程式碼應該在還沒有資料庫主要金鑰的 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫上執行。  
  
```sql  
--Create the keys and certificate.  
USE AdventureWorks2012;  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'mzkvdlk979438teag$$ds987yghn)(*&4fdg^';  
OPEN MASTER KEY DECRYPTION BY PASSWORD = 'mzkvdlk979438teag$$ds987yghn)(*&4fdg^';  
CREATE CERTIFICATE HumanResources037   
   WITH SUBJECT = 'Sammamish HR',   
   EXPIRY_DATE = '10/31/2009';  
CREATE SYMMETRIC KEY SSN_Key_01 WITH ALGORITHM = DES  
    ENCRYPTION BY CERTIFICATE HumanResources037;  
GO  
----Add a column of encrypted data.  
ALTER TABLE HumanResources.Employee  
    ADD EncryptedNationalIDNumber varbinary(128);   
OPEN SYMMETRIC KEY SSN_Key_01  
   DECRYPTION BY CERTIFICATE HumanResources037 ;  
UPDATE HumanResources.Employee  
SET EncryptedNationalIDNumber  
    = EncryptByKey(Key_GUID('SSN_Key_01'), NationalIDNumber);  
GO  
--  
--Close the key used to encrypt the data.  
CLOSE SYMMETRIC KEY SSN_Key_01;  
--  
--There are two ways to decrypt the stored data.  
--  
--OPTION ONE, using DecryptByKey()  
--1. Open the symmetric key  
--2. Decrypt the data  
--3. Close the symmetric key  
OPEN SYMMETRIC KEY SSN_Key_01  
   DECRYPTION BY CERTIFICATE HumanResources037;  
SELECT NationalIDNumber, EncryptedNationalIDNumber    
    AS 'Encrypted ID Number',  
    CONVERT(nvarchar, DecryptByKey(EncryptedNationalIDNumber))   
    AS 'Decrypted ID Number'  
    FROM HumanResources.Employee;  
CLOSE SYMMETRIC KEY SSN_Key_01;  
--  
--OPTION TWO, using DecryptByKeyAutoCert()  
SELECT NationalIDNumber, EncryptedNationalIDNumber   
    AS 'Encrypted ID Number',  
    CONVERT(nvarchar, DecryptByKeyAutoCert ( cert_ID('HumanResources037') , NULL ,EncryptedNationalIDNumber))   
    AS 'Decrypted ID Number'  
    FROM HumanResources.Employee;  
```  
  
## <a name="see-also"></a>另請參閱  
 [OPEN SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/open-symmetric-key-transact-sql.md)   
 [ENCRYPTBYKEY &#40;Transact-SQL&#41;](../../t-sql/functions/encryptbykey-transact-sql.md)   
 [DECRYPTBYKEY &#40;Transact-SQL&#41;](../../t-sql/functions/decryptbykey-transact-sql.md)   
 [加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
