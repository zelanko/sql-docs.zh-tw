---
title: sp_grantdbaccess （Transact-sql） |Microsoft Docs
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
ms.openlocfilehash: 3b88badb8b1852617d9edd8acd31f2c19258cca7
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/14/2019
ms.locfileid: "72304861"
---
# <a name="sp_grantdbaccess-transact-sql"></a>sp_grantdbaccess (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  將資料庫使用者加入目前資料庫中。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 改用[CREATE USER](../../t-sql/statements/create-user-transact-sql.md) 。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
sp_grantdbaccess [ @loginame = ] 'login'  
    [ , [ @name_in_db = ] 'name_in_db' [ OUTPUT ] ]  
```  
  
## <a name="arguments"></a>引數  
`[ @loginame = ] 'login_ '` 是要對應至新資料庫使用者的 Windows 群組、Windows 登入或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入名稱。 Windows 群組和 Windows 登入的名稱必須以*domain*\\*Login*格式的 windows 功能變數名稱加以限定。例如， **LONDON\Joeb**。 登入不能已對應至資料庫中的使用者。 *登*入是**sysname**，沒有預設值。  
  
``[ @name_in_db = ] 'name_in_db' [ OUTPUT]`` 是新資料庫使用者的名稱。 *name_in_db*是輸出變數，其資料類型為**sysname**，預設值為 Null。 如果未指定，則會使用*登*入。 如果指定為具有 Null 值的輸出變數， **\@name_in_db**會設定為*login*。 *name_in_db*不能已存在於目前的資料庫中。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>Remarks  
 **sp_grantdbaccess**會呼叫 CREATE USER，以支援其他選項。 如需建立資料庫使用者的詳細資訊，請參閱[ &#40;CREATE USER&#41;transact-sql](../../t-sql/statements/create-user-transact-sql.md)。 若要從資料庫中移除資料庫使用者，請使用[DROP user](../../t-sql/statements/drop-user-transact-sql.md)。  
  
 **sp_grantdbaccess**不能在使用者自訂交易內執行。  
  
## <a name="permissions"></a>Permissions  
 需要**db_owner**固定資料庫角色或**db_accessadmin**固定資料庫角色中的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例會使用 `CREATE USER`，將 Windows 登入 `Edmonds\LolanSo` 的資料庫使用者加入至目前的資料庫。 新使用者名叫 `Lolan`。 這是建立資料庫使用者的慣用方法。  
  
```sql
CREATE USER Lolan FOR LOGIN [Edmonds\LolanSo];  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [安全性預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [DROP USER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-user-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
