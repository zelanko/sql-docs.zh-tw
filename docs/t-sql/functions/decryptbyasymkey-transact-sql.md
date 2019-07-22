---
title: DECRYPTBYASYMKEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DECRYPTBYASYMKEY
- DECRYPTBYASYMKEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- asymmetric keys [SQL Server], DECRYPTBYASYMKEY function
- DECRYPTBYASYMKEY function
- decryption [SQL Server], asymmetric keys
ms.assetid: d9ebcd30-f01c-4cfe-b95e-ffe6ea13788b
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: c187caf0dc0027d6d7fa86cbd1bee09e76f0228d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68118956"
---
# <a name="decryptbyasymkey-transact-sql"></a>DECRYPTBYASYMKEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

此函式會使用非對稱金鑰為加密資料解密。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
DecryptByAsymKey (Asym_Key_ID , { 'ciphertext' | @ciphertext }   
    [ , 'Asym_Key_Password' ] )  
```  
  
## <a name="arguments"></a>引數  
 *Asym_Key_ID*  
資料庫中的非對稱金鑰識別碼。 *Asym_Key_ID* 具有 **int** 資料類型。  
  
 *ciphertext*  
以非對稱金鑰加密的資料字串。  
  
 @ciphertext  
**varbinary** 類型的變數，其中包含以非對稱金鑰加密的資料。  
  
 *Asym_Key_Password*  
用來加密資料庫中非對稱金鑰的密碼。  
  
## <a name="return-types"></a>傳回類型  
**varbinary**，大小上限為 8,000 個位元組。  
  
## <a name="remarks"></a>Remarks  
相較於對稱式加密/解密，非對稱金鑰加密/解密具有較高的成本。 使用大型資料集時 (例如儲存在資料表中的使用者資料)，建議開發人員避免非對稱金鑰加密/解密。  
  
## <a name="permissions"></a>權限  
`DECRYPTBYASYMKEY` 需要非對稱金鑰的 CONTROL 權限。  
  
## <a name="examples"></a>範例  
此範例會解密原本以非對稱金鑰 `JanainaAsymKey02` 來加密的加密文字。 `AdventureWorks2012.ProtectedData04` 會儲存此非對稱金鑰。 此範例會以非對稱金鑰 `JanainaAsymKey02` 來解密傳回的資料。 此範例使用密碼 `pGFD4bb925DGvbd2439587y` 來解密此非對稱金鑰。 此範例會將傳回的純文字轉換成 **nvarchar** 類型。  
  
```  
SELECT CONVERT(nvarchar(max),  
    DecryptByAsymKey( AsymKey_Id('JanainaAsymKey02'),   
    ProtectedData, N'pGFD4bb925DGvbd2439587y' ))   
AS DecryptedData   
FROM [AdventureWorks2012].[Sales].[ProtectedData04]   
WHERE Description = N'encrypted by asym key''JanainaAsymKey02''';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [ENCRYPTBYASYMKEY &#40;Transact-SQL&#41;](../../t-sql/functions/encryptbyasymkey-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [ALTER ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-asymmetric-key-transact-sql.md)   
 [DROP ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-asymmetric-key-transact-sql.md)   
 [選擇加密演算法](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)   
 [加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
