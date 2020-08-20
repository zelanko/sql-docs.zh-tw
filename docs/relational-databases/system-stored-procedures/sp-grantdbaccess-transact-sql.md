---
description: sp_grantdbaccess (Transact-SQL)
title: sp_grantdbaccess (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_grantdbaccess
- sp_grantdbaccess_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_grantdbaccess
ms.assetid: 3eb09513-03f1-42f8-9917-3a1f3a579bec
ms.author: vanto
author: VanMSFT
ms.openlocfilehash: 0425c6f4108ae48dadcead271814d99c212e8a2e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88469352"
---
# <a name="sp_grantdbaccess-transact-sql"></a>sp_grantdbaccess (Transact-SQL)

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  將資料庫使用者加入目前資料庫中。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 請改用 [CREATE USER](../../t-sql/statements/create-user-transact-sql.md) 。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
sp_grantdbaccess [ @loginame = ] 'login'  
    [ , [ @name_in_db = ] 'name_in_db' [ OUTPUT ] ]  
```  
  
## <a name="arguments"></a>引數  
`[ @loginame = ] 'login_ '` 這是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 要對應至新資料庫使用者之 windows 群組、windows 登入或登入的名稱。 Windows 群組和 windows 登入的名稱必須以*網域*登入形式的 windows 功能變數名稱限定 \\ * *，例如， **LONDON\Joeb**。 登入不能已對應至資料庫中的使用者。 *login* 是 **sysname**，沒有預設值。  
  
``[ @name_in_db = ] 'name_in_db' [ OUTPUT]`` 這是新資料庫使用者的名稱。 *name_in_db* 是資料類型為 **sysname**的輸出變數，預設值是 Null。 如果未指定，則會使用 *登* 入。 如果指定為值為 Null 的輸出變數， ** \@ name_in_db**會設定為*login*。 *name_in_db* 不能已經存在於目前的資料庫中。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 **sp_grantdbaccess** 會呼叫支援其他選項的 CREATE USER。 如需建立資料庫使用者的詳細資訊，請參閱 [建立使用者 &#40;transact-sql&#41;](../../t-sql/statements/create-user-transact-sql.md)。 若要從資料庫移除資料庫使用者，請使用 [DROP user](../../t-sql/statements/drop-user-transact-sql.md)。  
  
 **sp_grantdbaccess** 無法在使用者自訂交易內執行。  
  
## <a name="permissions"></a>權限  
 需要 **db_owner** 固定資料庫角色或 **db_accessadmin** 固定資料庫角色中的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例會使用將 `CREATE USER` Windows 登入的資料庫使用者加入 `Edmonds\LolanSo` 目前的資料庫。 新使用者名叫 `Lolan`。 這是建立資料庫使用者的慣用方法。  
  
```sql
CREATE USER Lolan FOR LOGIN [Edmonds\LolanSo];  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的安全性預存程式 ](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [DROP USER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-user-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
