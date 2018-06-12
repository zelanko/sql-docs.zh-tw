---
title: DECRYPTBYKEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
caps.latest.revision: 39
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 7f9e1e678fba7a2b2d24a85f4d57f1112b3d4cb8
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2018
ms.locfileid: "34779474"
---
# <a name="decryptbykey-transact-sql"></a>DECRYPTBYKEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

此函式會使用對稱金鑰為資料解密。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
DecryptByKey ( { 'ciphertext' | @ciphertext }   
    [ , add_authenticator, { authenticator | @authenticator } ] )  
```  
  
## <a name="arguments"></a>引數  
*ciphertext*  
**varbinary** 類型的變數，其中包含以金鑰加密的資料。  
  
**@ciphertext**  
**varbinary** 類型的變數，其中包含以金鑰加密的資料。  
  
 *add_authenticator*  
指出原始加密程序是否隨純文字一同包含及加密驗證器。 必須符合資料加密期間傳遞至 [ENCRYPTBYKEY (Transact-SQL)](./encryptbykey-transact-sql.md) 的值。 *add_authenticator* 具有 **int** 資料類型。  
  
 *authenticator*  
作為驗證器產生基礎使用的資料。 必須符合提供給 [ENCRYPTBYKEY (Transact-SQL)](./encryptbykey-transact-sql.md) 的值。 *authenticator* 具有 **sysname** 資料類型。  

**@authenticator**  
含有驗證器從中產生之資料的變數。 必須符合提供給 [ENCRYPTBYKEY (Transact-SQL)](./encryptbykey-transact-sql.md) 的值。 *@authenticator* 具有 **sysname** 資料類型。  

## <a name="return-types"></a>傳回類型  
**varbinary**，大小上限為 8,000 個位元組。 如果未開啟用於資料加密的對稱金鑰，或「加密文字」為 NULL，則 `DECRYPTBYKEY` 會傳回 NULL。  
  
## <a name="remarks"></a>Remarks  
`DECRYPTBYKEY` 使用對稱金鑰。 資料庫必須已開啟此對稱金鑰。 `DECRYPTBYKEY` 允許同時開啟多個金鑰。 加密文字解密之前，您不需要立即開啟金鑰。  
  
對稱式加密和解密運作起來通常較快，而且非常適合涉及大量資料的作業。  
  
## <a name="permissions"></a>Permissions  
目前的工作階段中必須已開啟對稱金鑰。 如需詳細資訊，請參閱 [OPEN SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/open-symmetric-key-transact-sql.md)。  
  
## <a name="examples"></a>範例  
  
### <a name="a-decrypting-by-using-a-symmetric-key"></a>A. 使用對稱金鑰來解密  
此範例會使用對稱金鑰來解密加密文字。  
  
```  
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
  
```  
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
  
## <a name="see-also"></a>另請參閱  
 [ENCRYPTBYKEY &#40;Transact-SQL&#41;](../../t-sql/functions/encryptbykey-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [ALTER SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-symmetric-key-transact-sql.md)   
 [DROP SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-symmetric-key-transact-sql.md)   
 [加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [選擇加密演算法](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)  
  
  
