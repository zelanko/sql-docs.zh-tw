---
title: "DECRYPTBYKEYAUTOASYMKEY (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 09/09/2015
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DECRYPTBYKEYAUTOASYMKEY_TSQL
- DECRYPTBYKEYAUTOASYMKEY
dev_langs:
- TSQL
helpviewer_keywords:
- DECRYPTBYKEYAUTOASYMSKEY function
ms.assetid: 5521d4cf-740c-4ede-98b6-4ba90b84e32d
caps.latest.revision: 23
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 74aa8bad7e6d848296ef2997017758883226ac48
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="decryptbykeyautoasymkey-transact-sql"></a>DECRYPTBYKEYAUTOASYMKEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  利用使用非對稱金鑰自動解密的對稱金鑰來解密。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
DecryptByKeyAutoAsymKey ( akey_ID , akey_password   
    , { 'ciphertext' | @ciphertext }  
  [ , { add_authenticator | @add_authenticator }   
  [ , { authenticator | @authenticator } ] ] )  
```  
  
## <a name="arguments"></a>引數  
 *akey_ID*  
 這是用來保護對稱金鑰之非對稱金鑰的識別碼。 *akey_ID*是**int**。  
  
 *akey_password*  
 這是保護非對稱金鑰之私密金鑰的密碼。 如果私密金鑰受資料庫主要金鑰保護，則可以是 NULL。 *akey_password*是**nvarchar**。  
  
 '*加密文字*'  
 這是以金鑰加密的資料。 *加密文字*是**varbinary**。  
  
 @ciphertext  
 這類型的變數**varbinary**其中包含已利用金鑰加密的資料。  
  
 *add_authenticator*  
 指出驗證器是否要與純文字一起加密。 必須是加密資料時傳遞至 EncryptByKey 的相同值。 如果使用驗證器，則為 1。 *add_authenticator*是**int**。  
  
 @add_authenticator  
 指出驗證器是否要與純文字一起加密。 必須是加密資料時傳遞至 EncryptByKey 的相同值。  
  
 *驗證器*  
 這是要產生驗證器的資料。 必須符合已提供給 EncryptByKey 的值。 *驗證器*是**sysname**。  
  
 @authenticator  
 這是含有要產生驗證器之資料的變數。 必須符合已提供給 EncryptByKey 的值。  
  
## <a name="return-types"></a>傳回類型  
 **varbinary** 8,000 個位元組的大小上限。  
  
## <a name="remarks"></a>備註  
 DecryptByKeyAutoAsymKey 結合 OPEN SYMMETRIC KEY 和 DecryptByKey 的功能。 可以在單一作業中解密對稱金鑰並且使用該金鑰來解密加密文字。  
  
## <a name="permissions"></a>Permissions  
 需要對稱金鑰的 VIEW DEFINITION 權限和非對稱金鑰的 CONTROL 權限。  
  
## <a name="examples"></a>範例  
 下列範例示範如何使用 `DecryptByKeyAutoAsymKey` 來簡化執行解密的程式碼。 此程式碼應該在還沒有資料庫主要金鑰的 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫上執行。  
  
```  
--Create the keys and certificate.  
USE AdventureWorks2012;  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'mzkvdMlk979438teag$$ds987yghn)(*&4fdg^';  
OPEN MASTER KEY DECRYPTION BY PASSWORD = 'mzkvdMlk979438teag$$ds987yghn)(*&4fdg^';  
CREATE ASYMMETRIC KEY SSN_AKey   
    WITH ALGORITHM = RSA_2048 ;   
GO  
CREATE SYMMETRIC KEY SSN_Key_02 WITH ALGORITHM = DES  
    ENCRYPTION BY ASYMMETRIC KEY SSN_AKey;  
GO  
--  
--Add a column of encrypted data.  
ALTER TABLE HumanResources.Employee  
    ADD EncryptedNationalIDNumber2 varbinary(128);   
OPEN SYMMETRIC KEY SSN_Key_02  
   DECRYPTION BY ASYMMETRIC KEY SSN_AKey;  
UPDATE HumanResources.Employee  
SET EncryptedNationalIDNumber2  
    = EncryptByKey(Key_GUID('SSN_Key_02'), NationalIDNumber);  
GO  
--Close the key used to encrypt the data.  
CLOSE SYMMETRIC KEY SSN_Key_02;  
--  
--There are two ways to decrypt the stored data.  
--  
--OPTION ONE, using DecryptByKey()  
--1. Open the symmetric key.  
--2. Decrypt the data.  
--3. Close the symmetric key.  
OPEN SYMMETRIC KEY SSN_Key_02  
   DECRYPTION BY ASYMMETRIC KEY SSN_AKey;  
SELECT NationalIDNumber, EncryptedNationalIDNumber2    
    AS 'Encrypted ID Number',  
    CONVERT(nvarchar, DecryptByKey(EncryptedNationalIDNumber2))   
    AS 'Decrypted ID Number'  
    FROM HumanResources.Employee;  
CLOSE SYMMETRIC KEY SSN_Key_02;  
--  
--OPTION TWO, using DecryptByKeyAutoAsymKey()  
SELECT NationalIDNumber, EncryptedNationalIDNumber2   
    AS 'Encrypted ID Number',  
    CONVERT(nvarchar, DecryptByKeyAutoAsymKey ( AsymKey_ID('SSN_AKey') , NULL ,EncryptedNationalIDNumber2))   
    AS 'Decrypted ID Number'  
    FROM HumanResources.Employee;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [OPEN SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/open-symmetric-key-transact-sql.md)   
 [ENCRYPTBYKEY &#40;TRANSACT-SQL &#41;](../../t-sql/functions/encryptbykey-transact-sql.md)   
 [DECRYPTBYKEY &#40;TRANSACT-SQL &#41;](../../t-sql/functions/decryptbykey-transact-sql.md)   
 [加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  

