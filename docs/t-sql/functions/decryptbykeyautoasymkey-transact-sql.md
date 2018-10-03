---
title: DECRYPTBYKEYAUTOASYMKEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/09/2015
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DECRYPTBYKEYAUTOASYMKEY_TSQL
- DECRYPTBYKEYAUTOASYMKEY
dev_langs:
- TSQL
helpviewer_keywords:
- DECRYPTBYKEYAUTOASYMSKEY function
ms.assetid: 5521d4cf-740c-4ede-98b6-4ba90b84e32d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6452ae04f35c81f6ef7beb9d379ad55a056d2021
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47664066"
---
# <a name="decryptbykeyautoasymkey-transact-sql"></a>DECRYPTBYKEYAUTOASYMKEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

此函式會為加密資料解密。 為達成此目的，它會先使用個別非對稱金鑰為對稱金鑰解密，然後使用第一個「步驟」中擷取的對稱金鑰為加密資料解密。  
  
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
用來加密對稱金鑰之非對稱金鑰的識別碼。 *akey_ID* 具有 **int** 資料類型。  
  
 *akey_password*  
保護非對稱金鑰的密碼。 如果以資料庫主要金鑰保護非對稱私密金鑰，則 *akey_password* 可以有 NULL 值。 *akey_password* 具有 **nvarchar** 資料類型。  
  
 *ciphertext* 以金鑰加密的資料。 *ciphertext* 具有 **varbinary** 資料類型。  
  
 @ciphertext  
**varbinary** 類型的變數，其中包含以對稱金鑰加密的資料。  
  
 *add_authenticator*  
指出原始加密程序是否隨純文字一同包含及加密驗證器。 必須符合資料加密期間傳遞至 [ENCRYPTBYKEY (Transact-SQL)](./encryptbykey-transact-sql.md) 的值。 如果加密程序使用驗證器，則 *add_authenticator* 的值為 1。 *add_authenticator* 具有 **int** 資料類型。  
  
 @add_authenticator  
指出原始加密程序是否隨純文字一同包含及加密驗證器的變數。 必須符合資料加密期間傳遞至 [ENCRYPTBYKEY (Transact-SQL)](./encryptbykey-transact-sql.md) 的值。 *@add_authenticator* 具有 **int** 資料類型。
  
 *authenticator*  
作為驗證器產生基礎使用的資料。 必須符合提供給 [ENCRYPTBYKEY (Transact-SQL)](./encryptbykey-transact-sql.md) 的值。 *authenticator* 具有 **sysname** 資料類型。  
  
 @authenticator  
含有驗證器從中產生之資料的變數。 必須符合提供給 [ENCRYPTBYKEY (Transact-SQL)](./encryptbykey-transact-sql.md) 的值。 *@authenticator* 具有 **sysname** 資料類型。  
  
@add_authenticator  
指出原始加密程序是否隨純文字一同包含及加密驗證器的變數。 必須符合資料加密期間傳遞至 [ENCRYPTBYKEY (Transact-SQL)](./encryptbykey-transact-sql.md) 的值。 *@add_authenticator* 具有 **int** 資料類型。  

*authenticator*  
作為驗證器產生基礎使用的資料。 必須符合提供給 [ENCRYPTBYKEY (Transact-SQL)](./encryptbykey-transact-sql.md) 的值。 *authenticator* 具有 **sysname** 資料類型。

@authenticator  
含有驗證器從中產生之資料的變數。 必須符合提供給 [ENCRYPTBYKEY (Transact-SQL)](./encryptbykey-transact-sql.md) 的值。 *@authenticator* 具有 **sysname** 資料類型。  

## <a name="return-types"></a>傳回類型  
**varbinary**，大小上限為 8,000 個位元組。  
  
## <a name="remarks"></a>Remarks  
`DECRYPTBYKEYAUTOASYMKEY` 會結合 `OPEN SYMMETRIC KEY` 和 `DECRYPTBYKEY` 的功能。 在單一作業中，它會先將對稱金鑰解密，再使用該金鑰將加密文字解密。  
  
## <a name="permissions"></a>[權限]  
需要對稱金鑰的 `VIEW DEFINITION` 權限和非對稱金鑰的 `CONTROL` 權限。  
  
## <a name="examples"></a>範例
此範例示範 `DECRYPTBYKEYAUTOASYMKEY` 如何簡化解密程式碼。 此程式碼應該在還沒有資料庫主要金鑰的 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫上執行。  

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
 [ENCRYPTBYKEY &#40;Transact-SQL&#41;](../../t-sql/functions/encryptbykey-transact-sql.md)   
 [DECRYPTBYKEY &#40;Transact-SQL&#41;](../../t-sql/functions/decryptbykey-transact-sql.md)   
 [加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
