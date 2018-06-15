---
title: xp_sqlmaint (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- xp_sqlmaint
- xp_sqlmaint_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- xp_sqlmaint
ms.assetid: bda66e1b-6bbd-49be-b86e-37efc920e912
caps.latest.revision: 37
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b5509b126a88ab2500fca0509789b61182af2ad2
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
ms.locfileid: "33256646"
---
# <a name="xpsqlmaint-transact-sql"></a>xp_sqlmaint (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  呼叫**sqlmaint**公用程式包含的字串**sqlmaint**參數。 **Sqlmaint**公用程式會執行一組一個或多個資料庫的維護作業。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
xp_sqlmaint 'switch_string'     
```  
  
## <a name="arguments"></a>引數  
 **'** *switch_string* **'**  
 這一個字串包含**sqlmaint**公用程式參數。 參數和值必須用空格分隔。  
  
 **-？** 參數不是有效值**xp_sqlmaint**。  
  
## <a name="return-code-values"></a>傳回碼值  
 無。 如果傳回錯誤**sqlmaint**公用程式會失敗。  
  
## <a name="remarks"></a>備註  
 如果使用者登入使用 SQL Server 驗證時，會呼叫此程序 **-U"***login_id***"** 和 **-P"***密碼***"** 參數前面加上了*switch_string*之前執行。 如果使用者以 Windows 驗證登入*switch_string*傳遞不會變更至**sqlmaint**。  
  
## <a name="permissions"></a>Permissions  
 需要 **系統管理員 (sysadmin)** 固定伺服器角色中的成員資格。  
  
## <a name="examples"></a>範例  
 在這個範例中，`xp_sqlmaint` 會呼叫 `sqlmaint` 來執行完整性檢查、建立報表檔，以及更新 `msdb.dbo.sysdbmaintplan_history`。  
  
```  
EXEC xp_sqlmaint '-D AdventureWorks2012 -PlanID 02A52657-D546-11D1-9D8A-00A0C9054212   
   -Rpt "C:\Program Files\Microsoft SQL Server\MSSQL\LOG\DBMaintPlan2.txt" -WriteHistory  -CkDB -CkAl';   
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
The command(s) executed successfully.  
```  
  
## <a name="see-also"></a>另請參閱  
 [sqlmaint 公用程式](../../tools/sqlmaint-utility.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
