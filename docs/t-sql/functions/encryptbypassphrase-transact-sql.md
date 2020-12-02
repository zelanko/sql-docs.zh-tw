---
description: ENCRYPTBYPASSPHRASE (Transact-SQL)
title: ENCRYPTBYPASSPHRASE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ENCRYPTBYPASSPHRASE
- ENCRYPTBYPASSPHRASE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ENCRYPTBYPASSPHRASE function
- encryption [SQL Server], symmetric keys
- symmetric keys [SQL Server], ENCRYPTBYPASSPHRASE function
ms.assetid: f8dbb9e6-94d6-40d7-8b38-6833a409d597
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: f8e11d7e9f36d6619c626d9387cce766fbce5b0d
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/25/2020
ms.locfileid: "96124745"
---
# <a name="encryptbypassphrase-transact-sql"></a>ENCRYPTBYPASSPHRASE (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  使用 TRIPLE DES 演算法搭配 128 金鑰位元長度，以複雜密碼加密資料。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```syntaxsql
EncryptByPassPhrase ( { 'passphrase' | @passphrase }   
    , { 'cleartext' | @cleartext }  
  [ , { add_authenticator | @add_authenticator }  
    , { authenticator | @authenticator } ] )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數
 *passphrase*  
 用於產生對稱金鑰的複雜密碼。  
  
 @passphrase  
 類型為 **nvarchar**、**char**、**varchar**、**binary**、**varbinary**，或 **nchar** 的變數，其中包含要用於產生對稱金鑰的複雜密碼。  
  
 *cleartext*  
 要加密的純文字。  
  
 @cleartext  
 類型為 **nvarchar**、**char**、**varchar**、**binary**、**varbinary**，或 **nchar**，包含純文字的變數。 大小上限是 8,000 位元組。  
  
 *add_authenticator*  
 指出驗證器是否要與純文字一起加密。 若要加入驗證器，則為 1。 **int**.  
  
 @add_authenticator  
 指出雜湊是否要與純文字一起加密。  
  
 *authenticator*  
 要衍生驗證器的資料。 **sysname**.  
  
 @authenticator  
 含有要衍生驗證器之資料的變數。  
  
## <a name="return-types"></a>傳回型別  
 **varbinary**，大小上限為 8,000 位元組。  
  
## <a name="remarks"></a>備註  
 複雜密碼是指包含空格的密碼。 使用複雜密碼的好處是，記住有意義的片語或句子比記住相較之下冗長的字元字串容易得多。  
  
 這個函數不會檢查密碼複雜性。  
  
## <a name="examples"></a>範例  
 下列範例會更新 `SalesCreditCard` 資料表中的記錄，並使用主索引鍵當做驗證器，加密儲存在資料行 `CardNumber_EncryptedbyPassphrase` 中的信用卡號碼之值。  
  
```sql  
USE AdventureWorks2012;  
GO  
-- Create a column in which to store the encrypted data.  
ALTER TABLE Sales.CreditCard   
    ADD CardNumber_EncryptedbyPassphrase VARBINARY(256);   
GO  
-- First get the passphrase from the user.  
DECLARE @PassphraseEnteredByUser NVARCHAR(128);  
SET @PassphraseEnteredByUser   
    = 'A little learning is a dangerous thing!';  
  
-- Update the record for the user's credit card.  
-- In this case, the record is number 3681.  
UPDATE Sales.CreditCard  
SET CardNumber_EncryptedbyPassphrase = EncryptByPassPhrase(@PassphraseEnteredByUser  
    , CardNumber, 1, CONVERT(varbinary, CreditCardID))  
WHERE CreditCardID = '3681';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [DECRYPTBYPASSPHRASE &#40;Transact-SQL&#41;](../../t-sql/functions/decryptbypassphrase-transact-sql.md)   
 [加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
