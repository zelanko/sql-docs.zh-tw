---
title: OPEN SYMMETRIC KEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- OPEN SYMMETRIC KEY
- OPEN_SYMMETRIC_KEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- symmetric keys [SQL Server], opening
- OPEN SYMMETRIC KEY statement
ms.assetid: ff019a7c-c373-46c7-ac43-ffb7e2ee60b3
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: b5fbd7c16e5150c9d547699c26038e435f1e96c0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47749604"
---
# <a name="open-symmetric-key-transact-sql"></a>OPEN SYMMETRIC KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  為對稱金鑰解密，讓它能夠使用。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
OPEN SYMMETRIC KEY Key_name DECRYPTION BY <decryption_mechanism>  
  
<decryption_mechanism> ::=  
    CERTIFICATE certificate_name [ WITH PASSWORD = 'password' ]  
    |  
    ASYMMETRIC KEY asym_key_name [ WITH PASSWORD = 'password' ]  
    |  
    SYMMETRIC KEY decrypting_Key_name  
    |  
    PASSWORD = 'decryption_password'  
```  
  
## <a name="arguments"></a>引數  
 *Key_name*  
 這是您要開啟的對稱金鑰名稱。  
  
 CERTIFICATE *certificate_name*  
 這是憑證名稱，其私密金鑰將用來為對稱金鑰解密。  
  
 ASYMMETRIC KEY *asym_key_name*  
 這是非對稱金鑰的名稱，其私密金鑰將用來為對稱金鑰解密。  
  
 WITH PASSWORD ='*password*'  
 這是為憑證或非對稱金鑰的私密金鑰加密所用的密碼。  
  
 SYMMETRIC KEY *decrypting_key_name*  
 這是為正在開啟之對稱金鑰解密所用的對稱金鑰名稱。  
  
 PASSWORD ='*password*'  
 這是保護對稱金鑰所用的密碼。  
  
## <a name="remarks"></a>Remarks  
 開啟的對稱金鑰繫結到工作階段，而非安全性內容。 開啟的金鑰將持續保持可用狀態，直到明確關閉金鑰或結束工作階段為止。 如果開啟了對稱金鑰，然後又切換內容，金鑰將保持開啟，而且可以在模擬內容中使用。 可以在 [sys.openkeys &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-openkeys-transact-sql.md) 目錄檢視中看到有關開啟對稱金鑰的資訊。  
  
 如果對稱金鑰是以另一個金鑰加密，必須先開啟該金鑰。  
  
 如果對稱金鑰已經開啟，則查詢為 **NO_OP**。  
  
 如果為對稱金鑰解密的密碼、憑證或金鑰不正確，查詢就會失敗。  
  
 無法開啟從加密提供者建立的對稱金鑰。 由於加密提供者正在開啟與關閉金鑰，使用此種對稱金鑰在沒有 **OPEN** 陳述式的情況下進行加密和解密作業會成功。  
  
## <a name="permissions"></a>[權限]  
 呼叫端必須具有金鑰的某種權限，而且絕不能被拒絕金鑰的 VIEW DEFINITION 權限。 其他需求則隨解密機制而不同：  
  
-   DECRYPTION BY CERTIFICATE：憑證的 CONTROL 權限，以及為其私密金鑰加密所用密碼的知識。  
  
-   DECRYPTION BY ASYMMETRIC KEY：非對稱金鑰的 CONTROL 權限，以及為其私密金鑰加密所用密碼的知識。  
  
-   DECRYPTION BY PASSWORD：為對稱金鑰加密所用其中一個密碼的知識。  
  
## <a name="examples"></a>範例  
  
### <a name="a-opening-a-symmetric-key-by-using-a-certificate"></a>A. 利用憑證來開啟對稱金鑰  
 下列範例會開啟對稱金鑰 `SymKeyMarketing3`，並利用憑證 `MarketingCert9` 的私密金鑰為它解密。  
  
```  
USE AdventureWorks2012;  
OPEN SYMMETRIC KEY SymKeyMarketing3   
    DECRYPTION BY CERTIFICATE MarketingCert9;  
GO  
```  
  
### <a name="b-opening-a-symmetric-key-by-using-another-symmetric-key"></a>B. 利用另一個對稱金鑰來開啟對稱金鑰  
 下列範例會開啟對稱金鑰 `MarketingKey11`，並利用對稱金鑰 `HarnpadoungsatayaSE3` 為它解密。  
  
```  
USE AdventureWorks2012;  
-- First open the symmetric key that you want for decryption.  
OPEN SYMMETRIC KEY HarnpadoungsatayaSE3   
    DECRYPTION BY CERTIFICATE sariyaCert01;  
-- Use the key that is already open to decrypt MarketingKey11.  
OPEN SYMMETRIC KEY MarketingKey11   
    DECRYPTION BY SYMMETRIC KEY HarnpadoungsatayaSE3;  
GO   
```  
  
## <a name="see-also"></a>另請參閱  
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [ALTER SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-symmetric-key-transact-sql.md)   
 [CLOSE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/close-symmetric-key-transact-sql.md)   
 [DROP SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-symmetric-key-transact-sql.md)   
 [加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [可延伸金鑰管理 &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)  
  
  
