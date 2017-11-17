---
title: "DECRYPTBYPASSPHRASE (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DECRYPTBYPASSPHRASE
- DECRYPTBYPASSPHRASE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- decryption [SQL Server], symmetric keys
- symmetric keys [SQL Server], DECRYPTBYPASSPHRASE function
- DECRYPTBYPASSPHRASE function
ms.assetid: ca34b5cd-07b3-4dca-b66a-ed8c6a826c95
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0af2f19acced57d722427c8f341db62dbdb34198
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="decryptbypassphrase-transact-sql"></a>DECRYPTBYPASSPHRASE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  將以複雜密碼加密的資料解密。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
DecryptByPassPhrase ( { 'passphrase' | @passphrase }   
    , { 'ciphertext' | @ciphertext }  
  [ , { add_authenticator | @add_authenticator }  
    , { authenticator | @authenticator } ] )  
```  
  
## <a name="arguments"></a>引數  
 *複雜密碼*  
 這是要用來產生解密金鑰的複雜密碼。  
  
 @passphrase  
 這類型的變數**nvarchar**， **char**， **varchar**，或**nchar** ，其中包含可用於產生的索引鍵的複雜密碼解密。  
  
 '*加密文字*'  
 這是要解密的加密文字。  
  
 @ciphertext  
 這類型的變數**varbinary**包含加密文字。 大小上限是 8,000 位元組。  
  
 *add_authenticator*  
 指出驗證器是否要與純文字一起加密。 如果使用驗證器，則為 1。 **int**。  
  
 @add_authenticator  
 指出驗證器是否要與純文字一起加密。 如果使用驗證器，則為 1。 **int**。  
  
 *驗證器*  
 這是驗證器資料。 **sysname**。  
  
 @authenticator  
 這是含有要衍生驗證器之資料的變數。  
  
## <a name="return-types"></a>傳回類型  
 **varbinary** 8,000 個位元組的大小上限。  
  
## <a name="remarks"></a>備註  
 執行這個函數不需要任何權限。  
  
 如果使用錯誤的複雜密碼或驗證器資訊，則傳回 NULL。  
  
 複雜密碼是用來產生解密金鑰，它不會保存下來。  
  
 如果對加密文字進行加密時包含了驗證器，則解密時必須提供驗證器。 如果在解密時提供的驗證器值不符合與資料一起加密的驗證器值，則解密會失敗。  
  
## <a name="examples"></a>範例  
 下列範例會解密更新中的資料錄[EncryptByPassPhrase](../../t-sql/functions/encryptbypassphrase-transact-sql.md)。  
  
```  
USE AdventureWorks2012;  
-- Get the pass phrase from the user.  
DECLARE @PassphraseEnteredByUser nvarchar(128);  
SET @PassphraseEnteredByUser   
= 'A little learning is a dangerous thing!';  
  
-- Decrypt the encrypted record.  
SELECT CardNumber, CardNumber_EncryptedbyPassphrase   
    AS 'Encrypted card number', CONVERT(nvarchar,  
    DecryptByPassphrase(@PassphraseEnteredByUser, CardNumber_EncryptedbyPassphrase, 1   
    , CONVERT(varbinary, CreditCardID)))  
    AS 'Decrypted card number' FROM Sales.CreditCard   
    WHERE CreditCardID = '3681';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [選擇加密演算法](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)   
 [ENCRYPTBYPASSPHRASE &#40;Transact-SQL&#41;](../../t-sql/functions/encryptbypassphrase-transact-sql.md)  
  
  

