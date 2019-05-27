---
title: DECRYPTBYPASSPHRASE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 55721b2b1f843ee78e8b69e4a1b99e39737ebb64
ms.sourcegitcommit: 83f061304fedbc2801d8d6a44094ccda97fdb576
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/20/2019
ms.locfileid: "65948940"
---
# <a name="decryptbypassphrase-transact-sql"></a>DECRYPTBYPASSPHRASE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

此函式會將原本以複雜密碼加密的資料解密。  
  
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
用來產生解密金鑰的複雜密碼。  
  
 @passphrase  
變數，其類型為

+ **char**
+ **nchar**
+ **nvarchar**

中的多個

+ **varchar**

其中包含用來產生解密金鑰的複雜密碼。  
  
'*ciphertext*'  
以金鑰加密的資料字串。 *ciphertext* 具有 **varbinary** 資料類型。  
 
@ciphertext  
**varbinary** 類型的變數，其中包含以金鑰加密的資料。 *@ciphertext* 變數的大小上限為 8,000 個位元組。  
  
*add_authenticator*  
指出原始加密程序是否隨純文字一同包含及加密驗證器。 如果加密程序使用驗證器，則 *add_authenticator* 的值為 1。 *add_authenticator* 具有 **int** 資料類型。  
  
@add_authenticator  
指出原始加密程序是否隨純文字一同包含及加密驗證器的變數。 如果加密程序使用驗證器，則 *@add_authenticator* 的值為 1。 *@add_authenticator* 具有 **int** 資料類型。  

*authenticator*  
作為驗證器產生基礎使用的資料。 *authenticator* 具有 **sysname** 資料類型。  
  
@authenticator  
變數，其中包含作為驗證器產生基礎使用的資料。 *@authenticator* 具有 **sysname** 資料類型。  
  
## <a name="return-types"></a>傳回類型  
**varbinary**，大小上限為 8,000 個位元組。  
  
## <a name="remarks"></a>Remarks  
執行 `DECRYPTBYPASSPHRASE` 不需要任何權限。 如果收到錯誤的複雜密碼或錯誤的驗證器資訊，則 `DECRYPTBYPASSPHRASE` 會傳回 NULL。  
  
`DECRYPTBYPASSPHRASE` 使用複雜密碼來產生解密金鑰。 此解密金鑰不會保存。  
  
如果對加密文字進行加密時包含了驗證器，`DECRYPTBYPASSPHRASE` 必須收到該相同的驗證器以用於解密程序。 如果提供給解密程序的驗證器值不符合原本用來加密的驗證器值，`DECRYPTBYPASSPHRASE` 作業會失敗。  
  
## <a name="examples"></a>範例  
此範例會將 [EncryptByPassPhrase](../../t-sql/functions/encryptbypassphrase-transact-sql.md) 中更新的記錄解密。  
  
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
  
  
