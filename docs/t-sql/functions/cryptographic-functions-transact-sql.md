---
title: 密碼編譯函式 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- functions [SQL Server], cryptographic
- crypto functions
- cryptography [SQL Server], functions
- decryption [SQL Server], functions
- security functions
- encryption [SQL Server], functions
ms.assetid: 0be5626b-5a25-4d8c-9f44-7abbfccf816c
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 7793c6b9568b53bbbe52a439ee54e0786606b324
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85732489"
---
# <a name="cryptographic-functions-transact-sql"></a>密碼編譯函式 (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

這些函數支援數字簽章、數字簽章驗證、加密和解密。
  
## <a name="symmetric-encryption-and-decryption"></a>對稱式加密和解密
  
|||  
|-|-|  
|[ENCRYPTBYKEY](../../t-sql/functions/encryptbykey-transact-sql.md)|[DECRYPTBYKEY](../../t-sql/functions/decryptbykey-transact-sql.md)|  
|[ENCRYPTBYPASSPHRASE](../../t-sql/functions/encryptbypassphrase-transact-sql.md)|[DECRYPTBYPASSPHRASE](../../t-sql/functions/decryptbypassphrase-transact-sql.md)|  
|[KEY_ID](../../t-sql/functions/key-id-transact-sql.md)|[KEY_GUID](../../t-sql/functions/key-guid-transact-sql.md)|  
|[DECRYPTBYKEYAUTOASYMKEY](../../t-sql/functions/decryptbykeyautoasymkey-transact-sql.md)|[KEY_NAME](../../t-sql/functions/key-name-transact-sql.md)|  
|[SYMKEYPROPERTY](../../t-sql/functions/symkeyproperty-transact-sql.md)||  
  
## <a name="asymmetric-encryption-and-decryption"></a>非對稱式加密和解密
  
|||  
|-|-|  
|[ENCRYPTBYASYMKEY](../../t-sql/functions/encryptbyasymkey-transact-sql.md)|[DECRYPTBYASYMKEY](../../t-sql/functions/decryptbyasymkey-transact-sql.md)|  
|[ENCRYPTBYCERT](../../t-sql/functions/encryptbycert-transact-sql.md)|[DECRYPTBYCERT](../../t-sql/functions/decryptbycert-transact-sql.md)|  
|[ASYMKEYPROPERTY](../../t-sql/functions/asymkeyproperty-transact-sql.md)|[ASYMKEY_ID](../../t-sql/functions/asymkey-id-transact-sql.md)|  
  
## <a name="signing-and-signature-verification"></a>簽署和簽章驗證
  
|||  
|-|-|  
|[SIGNBYASYMKEY](../../t-sql/functions/signbyasymkey-transact-sql.md)|[VERIFYSIGNEDBYASMKEY](../../t-sql/functions/verifysignedbyasymkey-transact-sql.md)|  
|[SIGNBYCERT](../../t-sql/functions/signbycert-transact-sql.md)|[VERIGYSIGNEDBYCERT](../../t-sql/functions/verifysignedbycert-transact-sql.md)|  
|[IS_OBJECTSIGNED](../../t-sql/functions/is-objectsigned-transact-sql.md)||  
  
## <a name="symmetric-decryption-with-automatic-key-handling"></a>對稱式解密，利用自動金鑰處理
  
|||  
|-|-|  
|[DecryptByKeyAutoCert](../../t-sql/functions/decryptbykeyautocert-transact-sql.md)||  
  
## <a name="encryption-hashing"></a>加密雜湊
  
|||  
|-|-|  
|[HASHBYTES](../../t-sql/functions/hashbytes-transact-sql.md)||  
  
## <a name="certificate-copying"></a>憑證複製
  
|||  
|-|-|  
|[CERTENCODED &#40;Transact-SQL&#41;](../../t-sql/functions/certencoded-transact-sql.md)||  
|[CERTPRIVATEKEY &#40;Transact-SQL&#41;](../../t-sql/functions/certprivatekey-transact-sql.md)||  
  
## <a name="see-also"></a>另請參閱
[函數](../../t-sql/functions/functions.md)  
[加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)  
[權限階層 &#40;Database Engine&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md)  
[CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)  
[CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)  
[CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)  
[安全性目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)
  
  
