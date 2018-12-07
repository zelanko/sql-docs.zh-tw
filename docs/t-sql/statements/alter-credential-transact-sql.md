---
title: ALTER CREDENTIAL (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/07/2018
ms.prod: sql
ms.technology: t-sql
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
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 32df63456e46fd8f522d897cd6068967bbb785b0
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2018
ms.locfileid: "52411845"
---
# <a name="alter-credential-transact-sql"></a>ALTER CREDENTIAL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  變更認證的屬性。  

> [!IMPORTANT]
> 「應該執行」資訊表示最佳做法；「必須執行」表示完成工作![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
ALTER CREDENTIAL credential_name WITH IDENTITY = 'identity_name'  
    [ , SECRET = 'secret' ]  
```  
  
## <a name="arguments"></a>引數  
 *credential_name*  
 指定正在變更的認證名稱。  
  
 IDENTITY **='***identity_name***'**  
 指定連接到伺服器外部時所要使用的帳戶名稱。  
  
 SECRET **='***secret***'**  
 指定外寄驗證所需的秘密。 *secret* 為選擇性。
  
> [!IMPORTANT]
> Azure SQL Database 只支援 Azure Key Vault 與共用存取簽章身分識別。 不支援 Windows 使用者身分識別。
  
## <a name="remarks"></a>Remarks  
 當認證變更時，*identity_name* 和 *secret* 的值都會重設。 如果未指定選擇性 SECRET 引數，預存秘密的值便會設為 NULL。  
  
 秘密是利用服務主要金鑰來加密的。 如果重新產生服務主要金鑰，便會利用新的服務主要金鑰來重新加密秘密。  
  
 您可以在 **sys.credentials** 目錄檢視中，看到認證的相關資訊。  
  
## <a name="permissions"></a>[權限]  
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
 [認證 &#40;資料庫引擎&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [DROP CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-credential-transact-sql.md)   
 [ALTER DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-credential-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [sys.credentials &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
  
  
