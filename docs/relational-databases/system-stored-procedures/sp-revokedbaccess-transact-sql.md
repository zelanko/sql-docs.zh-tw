---
title: sp_revokedbaccess （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_revokedbaccess_TSQL
- sp_revokedbaccess
dev_langs:
- TSQL
helpviewer_keywords:
- sp_revokedbaccess
ms.assetid: c997cfa1-539d-485c-a664-9c6f76bfe0c2
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 5eea0129b76a7bb7825987da98be40ba4a66d6fb
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67941710"
---
# <a name="sp_revokedbaccess-transact-sql"></a>sp_revokedbaccess (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  從目前資料庫移除資料庫使用者。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]請改用[DROP USER](../../t-sql/statements/drop-user-transact-sql.md) 。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_revokedbaccess [ @name_in_db = ] 'name'  
```  
  
## <a name="arguments"></a>引數  
`[ @name_in_db = ] 'name'`這是要移除的資料庫使用者名稱。 *名稱*是沒有預設值的**sysname** 。 *name*可以是伺服器登入、windows 登入或 windows 群組的名稱，而且必須存在於目前的資料庫中。 當您指定 Windows 登入或 Windows 群組時，請指定它在資料庫中的識別名稱。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 當移除資料庫使用者時，也會移除相依於該使用者的權限和別名。  
  
 **sp_revokedbaccess**只能從目前資料庫移除資料庫使用者。 移除擁有目前資料庫中之物件的資料庫使用者之前，必須先從資料庫傳送物件的擁有權或卸除這些物件。 如需詳細資訊，請參閱 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)。  
  
 **sp_revokedbaccess**不能在使用者自訂交易內執行。  
  
## <a name="permissions"></a>權限  
 需要資料庫的 ALTER ANY USER 權限。  
  
## <a name="examples"></a>範例  
 下列範例會從目前資料庫移除對應至`Edmonds\LolanSo`的資料庫使用者。  
  
```  
EXEC sp_revokedbaccess 'Edmonds\LolanSo';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的安全性預存程式](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [&#40;Transact-sql&#41;的系統預存程式](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [DROP USER &#40;Transact-sql&#41;](../../t-sql/statements/drop-user-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)  
  
  
