---
title: DECRYPTBYPASSPHRASE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
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
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 8e5db318e700d42f92a58bfe1e4016f4ee4bc1ce
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
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
 *passphrase*  
 這是要用來產生解密金鑰的複雜密碼。  
  
 @passphrase  
 為 **nvarchar**、**char**、**varchar** 或 **nchar** 類型的變數，其中包含用來產生解密金鑰的複雜密碼。  
  
 '*ciphertext*'  
 這是要解密的加密文字。  
  
 @ciphertext  
 為包含加密文字之 **varbinary** 類型的變數。 大小上限是 8,000 位元組。  
  
 *add_authenticator*  
 指出驗證器是否要與純文字一起加密。 如果使用驗證器，則為 1。 **int**.  
  
 @add_authenticator  
 指出驗證器是否要與純文字一起加密。 如果使用驗證器，則為 1。 **int**.  
  
 *authenticator*  
 這是驗證器資料。 **sysname**.  
  
 @authenticator  
 這是含有要衍生驗證器之資料的變數。  
  
## <a name="return-types"></a>傳回類型  
 **varbinary**，大小上限為 8,000 位元組。  
  
## <a name="remarks"></a>Remarks  
 執行這個函數不需要任何權限。  
  
 如果使用錯誤的複雜密碼或驗證器資訊，則傳回 NULL。  
  
 複雜密碼是用來產生解密金鑰，它不會保存下來。  
  
 如果對加密文字進行加密時包含了驗證器，則解密時必須提供驗證器。 如果在解密時提供的驗證器值不符合與資料一起加密的驗證器值，則解密會失敗。  
  
## <a name="examples"></a>範例  
 下列範例會將 [EncryptByPassPhrase](../../t-sql/functions/encryptbypassphrase-transact-sql.md) 中更新的記錄解密。  
  
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
  
  
