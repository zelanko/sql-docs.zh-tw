---
title: ALTER SYMMETRIC KEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER SYMMETRIC KEY
- ALTER_SYMMETRIC_KEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- modifying symmetric keys
- encryption [SQL Server], symmetric keys
- symmetric keys [SQL Server], modifying
- cryptography [SQL Server], symmetric keys
- ALTER SYMMETRIC KEY statement
ms.assetid: d3c776a4-7d71-4e6f-84fc-1db47400c465
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 15a45b7b7ebcc9e6c9e3110dc7c0fa3439a0af10
ms.sourcegitcommit: fc6a6eedcea2d98c93e33d39c1cecd99fbc9a155
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/12/2018
ms.locfileid: "49169236"
---
# <a name="alter-symmetric-key-transact-sql"></a>ALTER SYMMETRIC KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  變更對稱金鑰的屬性。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
ALTER SYMMETRIC KEY Key_name <alter_option>  
  
<alter_option> ::=  
   ADD ENCRYPTION BY <encrypting_mechanism> [ , ... n ]  
   |   
   DROP ENCRYPTION BY <encrypting_mechanism> [ , ... n ]  
<encrypting_mechanism> ::=  
   CERTIFICATE certificate_name  
   |  
   PASSWORD = 'password'  
   |  
   SYMMETRIC KEY Symmetric_Key_Name  
   |  
   ASYMMETRIC KEY Asym_Key_Name  
```  
  
## <a name="arguments"></a>引數  
 *Key_name*  
 這是要變更之對稱金鑰在資料庫中的識別名稱。  
  
 ADD ENCRYPTION BY   
 利用指定的方法新增加密。  
  
 DROP ENCRYPTION BY  
 利用指定的方法卸除加密。 您無法從對稱金鑰移除所有加密。  
  
 CERTIFICATE *Certificate_name*  
 指定用來加密對稱金鑰的憑證。 這個憑證必須已存在於資料庫中。  
  
 PASSWORD **='**_password_**'**  
 指定用於加密對稱金鑰的密碼。 *password* 必須符合執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體之電腦的 Windows 密碼原則需求。  
  
 SYMMETRIC KEY *Symmetric_Key_Name*  
 指定用來加密所要變更之對稱金鑰的對稱金鑰。 這個對稱金鑰必須已存在於資料庫中，且必須是開啟的。  
  
 ASYMMETRIC KEY *Asym_Key_Name*  
 指定用來加密所要變更之對稱金鑰的非對稱金鑰。 這個非對稱金鑰必須已存在於資料庫中。  
  
## <a name="remarks"></a>Remarks  
  
> [!CAUTION]  
>  如果是利用密碼 (而不是利用資料庫主要金鑰的公開金鑰) 來加密對稱金鑰，則會使用 TRIPLE_DES 加密演算法。 因此，利用強式加密演算法 (如 AES) 建立的金鑰，其本身的安全是由較弱的演算法來維護的。  
  
 若要變更對稱金鑰的加密，請使用 ADD ENCRYPTION 和 DROP ENCRYPTION 片語。 金鑰不可能完全不加密。 因此，最佳作法是先加入新的加密格式，再移除舊的加密格式。  
  
 如果要變更對稱金鑰的擁有者，請使用 [ALTER AUTHORIZATION](../../t-sql/statements/alter-authorization-transact-sql.md)。  
  
> [!NOTE]  
>  只有 RC4 演算法支援回溯相容性。 只有在資料庫相容性層級為 90 或 100 時，才能使用 RC4 或 RC4_128 加密新資料  (不建議使用)。請改用較新的演算法，例如其中一個 AES 演算法。 在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 中，使用 RC4 或 RC4_128 加密的資料可以在任何相容性層級進行解密。  
  
## <a name="permissions"></a>[權限]  
 需要對稱金鑰的 ALTER 權限。 如果利用憑證或非對稱金鑰來新增加密，則需要該憑證或非對稱金鑰的 VIEW DEFINITION 權限。 如果利用憑證或非對稱金鑰來卸除加密，則需要該憑證或非對稱金鑰的 CONTROL 權限。  
  
## <a name="examples"></a>範例  
 下列範例會變更用來保護對稱金鑰的加密方法。 當建立對稱金鑰 `JanainaKey043` 時，是利用憑證 `Shipping04` 來加密該金鑰的。 因為永遠不能將該金鑰儲存為未加密，所以在這個範例中，由密碼新增加密，然後由憑證移除加密。  
  
```  
CREATE SYMMETRIC KEY JanainaKey043 WITH ALGORITHM = AES_256   
    ENCRYPTION BY CERTIFICATE Shipping04;  
-- Open the key.   
OPEN SYMMETRIC KEY JanainaKey043 DECRYPTION BY CERTIFICATE Shipping04  
    WITH PASSWORD = '<enterStrongPasswordHere>';   
-- First, encrypt the key with a password.  
ALTER SYMMETRIC KEY JanainaKey043   
    ADD ENCRYPTION BY PASSWORD = '<enterStrongPasswordHere>';  
-- Now remove encryption by the certificate.  
ALTER SYMMETRIC KEY JanainaKey043   
    DROP ENCRYPTION BY CERTIFICATE Shipping04;  
CLOSE SYMMETRIC KEY JanainaKey043;  
```  
  
## <a name="see-also"></a>另請參閱  
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [OPEN SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/open-symmetric-key-transact-sql.md)   
 [CLOSE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/close-symmetric-key-transact-sql.md)   
 [DROP SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-symmetric-key-transact-sql.md)   
 [加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
