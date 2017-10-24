---
title: "DECRYPTBYCERT (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DecryptByCert_TSQL
- DECRYPTBYCERT
dev_langs:
- TSQL
helpviewer_keywords:
- certificates [SQL Server], decryption
- decryption [SQL Server], certificates
- DECRYPTBYCERT function
ms.assetid: 4950d787-40fa-4e26-bce8-2cb2ceca12fb
caps.latest.revision: 38
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ebdc328e49635af823cd64e8539ee5b7cfa95c76
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="decryptbycert-transact-sql"></a>DECRYPTBYCERT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  使用憑證的私密金鑰為資料解密。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
DecryptByCert ( certificate_ID , { 'ciphertext' | @ciphertext }   
    [ , { 'cert_password' | @cert_password } ] )  
```  
  
## <a name="arguments"></a>引數  
 *certificate_ID*  
 這是資料庫中憑證的識別碼。 *憑證*_ID 是**int**。  
  
 *加密文字*  
 這是已經利用憑證私密金鑰加密的資料字串。  
  
 @ciphertext  
 這類型的變數**varbinary**包含已經利用憑證加密的資料。  
  
 *cert_password*  
 這是為憑證的私密金鑰加密所用的密碼。 它必須是 Unicode。  
  
 @cert_password  
 這類型的變數**nchar**或**nvarchar**其中包含用來加密憑證的私密金鑰的密碼。 它必須是 Unicode。  
  
## <a name="return-types"></a>傳回類型  
 **varbinary** 8,000 個位元組的大小上限。  
  
## <a name="remarks"></a>備註  
 這個函數是利用憑證的私密金鑰為資料解密。 使用非對稱金鑰來轉換密碼編譯，會耗用大量資源。 因此，EncryptByCert 和 DecryptByCert 不適用於使用者資料的常式加密。  
  
## <a name="permissions"></a>Permissions  
 需要憑證的 CONTROL 權限。  
  
## <a name="examples"></a>範例  
 下列範例會從標示為 `[AdventureWorks2012].[ProtectedData04]` 的 `data encrypted by certificate JanainaCert02` 選取資料列。 這個範例使用憑證 `JanainaCert02` 的私密金鑰將加密文字解密；一開始先以憑證的密碼 `pGFD4bb925DGvbd2439587y` 將憑證解密。 解密的資料會從轉換**varbinary**至**nvarchar**。  
  
```  
SELECT convert(nvarchar(max), DecryptByCert(Cert_Id('JanainaCert02'),  
    ProtectedData, N'pGFD4bb925DGvbd2439587y'))  
FROM [AdventureWorks2012].[ProtectedData04]   
WHERE Description   
    = N'data encrypted by certificate '' JanainaCert02''';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [ENCRYPTBYCERT &#40;TRANSACT-SQL &#41;](../../t-sql/functions/encryptbycert-transact-sql.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [ALTER CERTIFICATE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-certificate-transact-sql.md)   
 [卸除憑證 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-certificate-transact-sql.md)   
 [BACKUP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/backup-certificate-transact-sql.md)   
 [加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  

