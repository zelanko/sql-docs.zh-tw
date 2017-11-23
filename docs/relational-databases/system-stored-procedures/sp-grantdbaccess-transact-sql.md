---
title: "sp_grantdbaccess (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_grantdbaccess
- sp_grantdbaccess_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_grantdbaccess
ms.assetid: 3eb09513-03f1-42f8-9917-3a1f3a579bec
caps.latest.revision: "33"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9e7d3f7a195f525c67d66f62faacf70b42d38492
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="spgrantdbaccess-transact-sql"></a>sp_grantdbaccess (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  將資料庫使用者加入目前資料庫中。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]使用[CREATE USER](../../t-sql/statements/create-user-transact-sql.md)改為。  
  
||  
|-|  
|**適用於**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [目前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658))。|  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_grantdbaccess [ @loginame = ] 'login'  
    [ , [ @name_in_db = ] 'name_in_db' [ OUTPUT ] ]  
```  
  
## <a name="arguments"></a>引數  
 [  **@loginame =** ] **'***登入* **'**  
 這是要對應至新資料庫使用者的 Windows 群組、Windows 登入或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入的名稱。 Windows 群組和 Windows 登入的名稱必須以在表單中的 Windows 網域名稱限定*網域*\\*登入*; 例如， **LONDON\Joeb**。 登入不能已對應至資料庫中的使用者。 *登入*是**sysname**，沒有預設值。  
  
 [  **@name_in_db=**] **'***name_in_db***'** [**輸出**]  
 這是新資料庫使用者的名稱。 *name_in_db*是 OUTPUT 變數資料類型為**sysname**，預設值為 NULL。 如果未指定，*登入*用。 如果指定為輸出變數的值是 NULL，  **@name_in_db** 設*登入*。 *name_in_db*必須存在目前資料庫中。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 **sp_grantdbaccess**呼叫建立的使用者，支援其他選項。 建立資料庫使用者的相關資訊，請參閱[CREATE USER &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-user-transact-sql.md). 若要從資料庫移除資料庫使用者，請使用[DROP USER](../../t-sql/statements/drop-user-transact-sql.md)。  
  
 **sp_grantdbaccess**無法在使用者自訂交易內執行。  
  
## <a name="permissions"></a>Permissions  
 需要的成員資格**db_owner**固定的資料庫角色或**db_accessadmin**固定的資料庫角色。  
  
## <a name="examples"></a>範例  
 下列範例會使用`CREATE USER`加入資料庫使用者的 Windows 登入`Edmonds\LolanSo`到目前的資料庫。 新使用者名叫 `Lolan`。 這是建立資料庫使用者的慣用方法。  
  
```  
CREATE USER Lolan FOR LOGIN [Edmonds\LolanSo];  
GO  
```  
  
## <a name="see-also"></a>請參閱＜  
 [安全性預存程序 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [卸除使用者 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-user-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
