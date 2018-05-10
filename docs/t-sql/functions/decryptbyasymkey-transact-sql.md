---
title: DECRYPTBYASYMKEY (Transact-SQL) | Microsoft Docs
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
- DECRYPTBYASYMKEY
- DECRYPTBYASYMKEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- asymmetric keys [SQL Server], DECRYPTBYASYMKEY function
- DECRYPTBYASYMKEY function
- decryption [SQL Server], asymmetric keys
ms.assetid: d9ebcd30-f01c-4cfe-b95e-ffe6ea13788b
caps.latest.revision: 34
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 98b08c914c0eb74e55d2d3c8a9e032432391a054
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="decryptbyasymkey-transact-sql"></a>DECRYPTBYASYMKEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  利用非對稱金鑰為資料解密。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
DecryptByAsymKey (Asym_Key_ID , { 'ciphertext' | @ciphertext }   
    [ , 'Asym_Key_Password' ] )  
```  
  
## <a name="arguments"></a>引數  
 *Asym_Key_ID*  
 這是資料庫中的非對稱金鑰識別碼。 *Asym_Key_ID* 為 **int**。  
  
 *ciphertext*  
 這是已經利用非對稱金鑰加密的資料字串。  
  
 @ciphertext  
 為 **varbinary** 類型的變數，其中包含已使用非對稱金鑰加密的資料。  
  
 *Asym_Key_Password*  
 這是為資料庫中非對稱金鑰加密所用的密碼。  
  
## <a name="return-types"></a>傳回類型  
 **varbinary**，大小上限為 8,000 位元組。  
  
## <a name="remarks"></a>Remarks  
 相對於利用對稱金鑰來加密/解密，利用非對稱金鑰來加密/解密的成本相當高。 如果您是使用大型資料集 (例如，資料表中的使用者資料)，不建議您使用非對稱金鑰。  
  
## <a name="permissions"></a>Permissions  
 需要非對稱金鑰的 CONTROL 權限。  
  
## <a name="examples"></a>範例  
 下列範例將為已經利用非對稱金鑰 `JanainaAsymKey02` 加密的加密文字解密，該金鑰儲存在 `AdventureWorks2012.ProtectedData04` 中。 傳回的資料則是利用非對稱金鑰 `JanainaAsymKey02` 解密，而該金鑰已經利用密碼 `pGFD4bb925DGvbd2439587y` 進行解密。 純文字會轉換成 **nvarchar** 類型。  
  
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
  
  
