---
title: ENCRYPTBYKEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ENCRYPTBYKEY_TSQL
- ENCRYPTBYKEY
dev_langs:
- TSQL
helpviewer_keywords:
- authenticators [SQL Server]
- encryption [SQL Server], symmetric keys
- symmetric keys [SQL Server], ENCRYPTBYKEY function
- ENCRYPTBYKEY function
ms.assetid: 0e11f8c5-f79d-46c1-ab11-b68ef05d6787
caps.latest.revision: 44
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: c648c37fc0f8446b4b3f4908a5d633b5f803cd54
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="encryptbykey-transact-sql"></a>ENCRYPTBYKEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  使用對稱金鑰加密資料。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
EncryptByKey ( key_GUID , { 'cleartext' | @cleartext }  
    [, { add_authenticator | @add_authenticator }  
     , { authenticator | @authenticator } ] )  
```  
  
## <a name="arguments"></a>引數  
 *key_GUID*  
 為用於加密 *cleartext* 之金鑰的 GUID。 **uniqueidentifier**。  
  
 '*cleartext*'  
 這是要利用金鑰加密的資料。  
  
 @cleartext  
 為類型是 **nvarchar**、**char**、**varchar**、**binary**、**varbinary** 或 **nchar** 的變數，其中包含要以金鑰加密的資料。  
  
 *add_authenticator*  
 指出驗證器是否要與 *cleartext* 一起加密。 在使用驗證器時，必須是 1。 **int**.  
  
 @add_authenticator  
 指出驗證器是否要與 *cleartext* 一起加密。 在使用驗證器時，必須是 1。 **int**.  
  
 *authenticator*  
 這是要衍生驗證器的資料。 **sysname**.  
  
 @authenticator  
 這是含有要衍生驗證器之資料的變數。  
  
## <a name="return-types"></a>傳回類型  
 **varbinary**，大小上限為 8,000 位元組。  
  
 如果索引鍵不是開啟、不存在、或索引鍵是已被取代的 RC4 索引鍵，且資料庫不在相容性層級 110 以上的話，則傳回 NULL。  
 
 如果 *cleartext* 值為 NULL，則傳回 NULL。
  
## <a name="remarks"></a>Remarks  
 EncryptByKey 會使用對稱金鑰。 因此必須開啟此金鑰。 如果目前的工作階段已經開啟對稱金鑰，即無須在查詢內容中再開啟一次。  
  
 驗證器可以幫助您防止代換已加密之欄位的全值。 例如，請參考下面的薪資資料表。  
  
|Employee_ID|Standard_Title|Base_Pay|  
|------------------|---------------------|---------------|  
|345|影印室助手|Fskj%7^edhn00|  
|697|財務長|M0x8900f56543|  
|694|排版設計總監|Cvc97824%^34f|  
  
 惡意使用者不必破解加密，就可以從儲存加密文字的內容，推斷出大量資訊。 由於財務長的薪水比影印室助理高，因而可推論加密為 M0x8900f56543 的值必然大於加密為 Fskj%7^edhn00 的值。 若是如此，則只要是對資料表具有 ALTER 權限的使用者，都可以將影印室助理的 Base_Pay 欄位資料換成財務長的 Base_Pay 欄位資料，為影印室助理加薪。 這種全值替換攻擊完全跳過加密。  
  
 若要阻止全值替換攻擊，可以在對純文字進行加密之前，先加入內容資訊。 這個內容資訊是用來確認純文字資料沒有被移動。  
  
 如果驗證器參數是在資料加密時指定，若要利用 DecryptByKey 將資料解密，必須使用同一個驗證器。 在加密時，驗證器的雜湊會與純文字一起加密。 在解密時，必須將同一個驗證器傳遞給 DecryptByKey。 如果兩者不相符，解密會失敗。 這表示值在加密後有被移動過。 我們建議您使用包含唯一且不變之值的資料行當做驗證器。 如果驗證器的值變更，您可能會遺失資料的存取權。  
  
 對稱加密和解密相當快速，而且很適合處理大量資料。  
  
> [!IMPORTANT]  
>  將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 加密函數與 ANSI_PADDING OFF 設定一起使用，可能會因為隱含轉換而造成資料遺失。 如需 ANSI_PADDING 的詳細資訊，請參閱 [SET ANSI_PADDING &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md)。  
  
## <a name="examples"></a>範例  
 下列範例所示範的功能，必須倚賴[如何：加密資料行](../../relational-databases/security/encryption/encrypt-a-column-of-data.md)中所建立的金鑰和憑證。  
  
### <a name="a-encrypting-a-string-with-a-symmetric-key"></a>A. 使用對稱金鑰加密字串  
 下列範例會在 `Employee` 資料表加入一個資料行，並將資料行 `NationalIDNumber` 中所儲存的社會保險號碼值加密。  
  
```  
USE AdventureWorks2012;  
GO  
  
-- Create a column in which to store the encrypted data.  
ALTER TABLE HumanResources.Employee  
    ADD EncryptedNationalIDNumber varbinary(128);   
GO  
  
-- Open the symmetric key with which to encrypt the data.  
OPEN SYMMETRIC KEY SSN_Key_01  
   DECRYPTION BY CERTIFICATE HumanResources037;  
  
-- Encrypt the value in column NationalIDNumber with symmetric key  
-- SSN_Key_01. Save the result in column EncryptedNationalIDNumber.  
UPDATE HumanResources.Employee  
SET EncryptedNationalIDNumber  
    = EncryptByKey(Key_GUID('SSN_Key_01'), NationalIDNumber);  
GO  
```  
  
### <a name="b-encrypting-a-record-together-with-an-authentication-value"></a>B. 加密記錄與驗證值  
  
```  
USE AdventureWorks2012;  
  
-- Create a column in which to store the encrypted data.  
ALTER TABLE Sales.CreditCard.   
    ADD CardNumber_Encrypted varbinary(128);   
GO  
  
-- Open the symmetric key with which to encrypt the data.  
OPEN SYMMETRIC KEY CreditCards_Key11  
    DECRYPTION BY CERTIFICATE Sales09;  
  
-- Encrypt the value in column CardNumber with symmetric   
-- key CreditCards_Key11.  
-- Save the result in column CardNumber_Encrypted.    
UPDATE Sales.CreditCard  
SET CardNumber_Encrypted = EncryptByKey(Key_GUID('CreditCards_Key11'),   
    CardNumber, 1, CONVERT( varbinary, CreditCardID) );  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [DECRYPTBYKEY &#40;Transact-SQL&#41;](../../t-sql/functions/decryptbykey-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [ALTER SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-symmetric-key-transact-sql.md)   
 [DROP SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-symmetric-key-transact-sql.md)   
 [加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [HASHBYTES &#40;Transact-SQL&#41;](../../t-sql/functions/hashbytes-transact-sql.md)  
  
  
