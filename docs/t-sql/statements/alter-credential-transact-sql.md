---
title: "ALTER CREDENTIAL (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 08/19/2015
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER CREDENTIAL
- ALTER_CREDENTIAL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- passwords [SQL Server], credentials
- credentials [SQL Server], ALTER CREDENTIAL statement
- modifying credentials
- authentication [SQL Server], credentials
- ALTER CREDENTIAL statement
ms.assetid: b08899a6-c09e-4af4-91aa-a978ada79264
caps.latest.revision: 27
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d183da3fef3f2802803d4dc9771dbc72e601321a
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="alter-credential-transact-sql"></a>ALTER CREDENTIAL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  變更認證的屬性。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
ALTER CREDENTIAL credential_name WITH IDENTITY = 'identity_name'  
    [ , SECRET = 'secret' ]  
```  
  
## <a name="arguments"></a>引數  
 *credential_name*  
 指定正在變更的認證名稱。  
  
 識別**='***identity_name***'**  
 指定連接到伺服器外部時所要使用的帳戶名稱。  
  
 密碼**='***密碼***'**  
 指定外寄驗證所需的秘密。 *密碼*是選擇性的。  
  
## <a name="remarks"></a>備註  
 當變更認證時，兩者的值*identity_name*和*密碼*會重設。 如果未指定選擇性 SECRET 引數，預存秘密的值便會設為 NULL。  
  
 秘密是利用服務主要金鑰來加密的。 如果重新產生服務主要金鑰，便會利用新的服務主要金鑰來重新加密秘密。  
  
 認證的相關資訊會顯示在**sys.credentials**目錄檢視。  
  
## <a name="permissions"></a>Permissions  
 需要 ALTER ANY CREDENTIAL 權限。 如果認證是系統認證，則需要 CONTROL SERVER 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-changing-the-password-of-a-credential"></a>A. 變更認證的密碼  
 下列範例會變更儲存在稱為 `Saddles` 之認證中的秘密。 這個認證包含 Windows 登入 `RettigB` 及其密碼。 使用 SECRET 子句將新的密碼加入認證中。  
  
```  
ALTER CREDENTIAL Saddles WITH IDENTITY = 'RettigB',   
    SECRET = 'sdrlk8$40-dksli87nNN8';  
GO  
```  
  
### <a name="b-removing-the-password-from-a-credential"></a>B. 從認證移除密碼  
 下列範例會從稱為 `Frames` 的認證中移除密碼。 這個認證包含 Windows 登入 `Aboulrus8` 和密碼。 由於未指定 SECRET 選項，因此在執行陳述式之後，認證的密碼為 NULL。  
  
```  
ALTER CREDENTIAL Frames WITH IDENTITY = 'Aboulrus8';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [認證 &#40; Database engine&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [卸除認證 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-credential-transact-sql.md)   
 [ALTER DATABASE SCOPED CREDENTIAL &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-database-scoped-credential-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [sys.credentials &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
  
  

