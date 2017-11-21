---
title: "ENCRYPTBYASYMKEY (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
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
- ENCRYPTBYASYMKEY
- ENCRYPTBYASYMKEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ENCRYPTBYASYMKEY function
- encryption [SQL Server], asymmetric keys
- asymmetric keys [SQL Server], ENCRYPTBYASYMKEY function
ms.assetid: 86bb2588-ab13-4db2-8f3c-42c9f572a67b
caps.latest.revision: 35
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 711b5887a9411c10c215cc766eb0995c3e056d77
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="encryptbyasymkey-transact-sql"></a>ENCRYPTBYASYMKEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  利用非對稱金鑰為資料加密。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
EncryptByAsymKey ( Asym_Key_ID , { 'plaintext' | @plaintext } )  
```  
  
## <a name="arguments"></a>引數  
 *Asym_Key_ID*  
 這是資料庫中的非對稱金鑰識別碼。 **int**。  
  
 *純文字*  
 這是要利用非對稱金鑰加密的資料字串。  
  
 **@plaintext**  
 這類型的變數**nvarchar**， **char**， **varchar**，**二進位**， **varbinary**，或**nchar** ，其中包含要使用非對稱金鑰加密的資料。  
  
## <a name="return-types"></a>傳回類型  
 **varbinary** 8,000 個位元組的大小上限。  
  
## <a name="remarks"></a>備註  
 相較於利用對稱金鑰來加密及解密，利用非對稱金鑰來加密及解密的成本相當高。 建議您不要使用非對稱金鑰來加密大型資料集，例如資料表中的使用者資料。 您應該改用強式對稱金鑰來加密資料，並使用非對稱金鑰將該對稱金鑰加密。  
  
 **EncryptByAsymKey**傳回**NULL** ，如果輸入超過特定數目的位元組，根據演算法而定。 限制： 512 位元 RSA 金鑰可以加密 53 個位元組，1024 位元金鑰可以加密 117 最多個位元組，並在 2048 位元金鑰可以加密 245 個位元組。 (請注意，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，憑證和非對稱金鑰都是 RSA 金鑰上的包裝函式)。  
  
## <a name="examples"></a>範例  
 下列範例會利用非對稱金鑰 `@cleartext` 將儲存在 `JanainaAsymKey02` 中的文字加密。 加密的資料會插入 `ProtectedData04` 資料表中。  
  
```  
INSERT INTO AdventureWorks2012.Sales.ProtectedData04   
    VALUES( N'Data encrypted by asymmetric key ''JanainaAsymKey02''',  
    EncryptByAsymKey(AsymKey_ID('JanainaAsymKey02'), @cleartext) );  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [DECRYPTBYASYMKEY &#40;TRANSACT-SQL &#41;](../../t-sql/functions/decryptbyasymkey-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  

