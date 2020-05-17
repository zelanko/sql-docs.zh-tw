---
title: DECRYPTBYCERT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 9653e799a543dd95a7d6fb033e0a8d5b9a4484a8
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "71314526"
---
# <a name="decryptbycert-transact-sql"></a>DECRYPTBYCERT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

此函式會使用憑證的私密金鑰為加密資料解密。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
DecryptByCert ( certificate_ID , { 'ciphertext' | @ciphertext }   
    [ , { 'cert_password' | @cert_password } ] )  
```  
  
## <a name="arguments"></a>引數  
 *certificate_ID*  
資料庫中的憑證識別碼。 *certificate_ID* 具有 **int** 資料類型。  
  
 *ciphertext*  
以憑證公開金鑰加密的資料字串。  
  
 @ciphertext  
**varbinary** 類型的變數，其中包含以憑證加密的資料。  
  
 *cert_password*  
用來加密憑證私密金鑰的密碼。 *cert_password* 必須具有 Unicode 資料格式。  
  
 @cert_password  
**nchar** 或 **nvarchar** 類型的變數，其中包含用來加密憑證私密金鑰的密碼。 *\@cert_password* 必須是 Unicode 資料格式。  

## <a name="return-types"></a>傳回型別  
**varbinary**，大小上限為 8,000 個位元組。  
  
## <a name="remarks"></a>備註  
這個函數是利用憑證的私密金鑰為資料解密。 使用非對稱金鑰來轉換密碼編譯，會耗用大量資源。 因此，建議開發人員避免使用 [ENCRYPTBYCERT](./encryptbycert-transact-sql.md) 和 DECRYPTBYCERT 對常式使用者資料進行加密/解密。  

## <a name="permissions"></a>權限  
`DECRYPTBYCERT` 需要憑證的 CONTROL 權限。  
  
## <a name="examples"></a>範例  
此範例會從 `[AdventureWorks2012].[ProtectedData04]` 選取標示為憑證 `JanainaCert02` 原本加密之資料的資料列。 此範例會先使用憑證密碼 `JanainaCert02` 為憑證 `pGFD4bb925DGvbd2439587y` 的私密金鑰解密。 然後，此範例會使用此私密金鑰為加密文字解密。 此範例會將解密資料從 **varbinary** 轉換成 **nvarchar**。  

```  
SELECT convert(nvarchar(max), DecryptByCert(Cert_Id('JanainaCert02'),  
    ProtectedData, N'pGFD4bb925DGvbd2439587y'))  
FROM [AdventureWorks2012].[ProtectedData04]   
WHERE Description   
    = N'data encrypted by certificate '' JanainaCert02''';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [ENCRYPTBYCERT &#40;Transact-SQL&#41;](../../t-sql/functions/encryptbycert-transact-sql.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [ALTER CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-certificate-transact-sql.md)   
 [DROP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-certificate-transact-sql.md)   
 [BACKUP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/backup-certificate-transact-sql.md)   
 [加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
