---
title: DECRYPTBYKEYAUTOCERT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/09/2015
ms.prod: sql
ms.prod_service: sql-database
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DECRYPTBYKEYAUTOCERT
- DECRYPTBYKEYAUTOCERT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DECRYPTBYKEYAUTOCERT function
ms.assetid: 6b45fa2e-ffaa-46f7-86ff-5624596eda4a
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 3bf53e51d3896953e66e3360aaa810a5c13c51ee
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="decryptbykeyautocert-transact-sql"></a>DECRYPTBYKEYAUTOCERT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  使用對稱金鑰解密，而對稱金鑰則會以憑證自動解密。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
DecryptByKeyAutoCert ( cert_ID , cert_password   
    , { 'ciphertext' | @ciphertext }  
  [ , { add_authenticator | @add_authenticator }   
  [ , { authenticator | @authenticator } ] ] )  
```  
  
## <a name="arguments"></a>引數  
 *cert_ID*  
 這是用來保護對稱金鑰的憑證識別碼。 *cert_ID* 為 **int**。  
  
 *cert_password*  
 這是保護憑證私密金鑰的密碼。 如果私密金鑰受資料庫主要金鑰保護，則可以是 NULL。 *cert_password* 為 **nvarchar**。  
  
 '*ciphertext*'  
 這是以金鑰加密的資料。 *ciphertext* 為 **varbinary**。  
  
 @ciphertext  
 為 **varbinary** 類型的變數，其中包含已使用金鑰加密的資料。  
  
 *add_authenticator*  
 指出驗證器是否要與純文字一起加密。 必須是加密資料時，傳遞至 EncryptByKey 的相同值。如果使用驗證器，則為 **1**。 *add_authenticator* 為 **int**。  
  
 @add_authenticator  
 指出驗證器是否要與純文字一起加密。 必須是加密資料時傳遞至 EncryptByKey 的相同值。  
  
 *authenticator*  
 這是要產生驗證器的資料。 必須符合已提供給 EncryptByKey 的值。 *authenticator* 為 **sysname**。  
  
 @authenticator  
 這是含有要產生驗證器之資料的變數。 必須符合已提供給 EncryptByKey 的值。  
  
## <a name="return-types"></a>傳回類型  
 **varbinary**，大小上限為 8,000 位元組。  
  
## <a name="remarks"></a>Remarks  
 DecryptByKeyAutoCert 結合 OPEN SYMMETRIC KEY 和 DecryptByKey 的功能。 可以在單一作業中解密對稱金鑰並且使用該金鑰來解密加密文字。  
  
## <a name="permissions"></a>Permissions  
 需要對稱金鑰的 VIEW DEFINITION 權限和憑證的 CONTROL 權限。  
  
## <a name="examples"></a>範例  
 下列範例示範如何使用 `DecryptByKeyAutoCert` 來簡化執行解密的程式碼。 此程式碼應該在還沒有資料庫主要金鑰的 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫上執行。  
  
```  
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
  
  
