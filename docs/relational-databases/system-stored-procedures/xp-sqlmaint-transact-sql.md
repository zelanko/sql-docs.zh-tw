---
title: xp_sqlmaint (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xp_sqlmaint
- xp_sqlmaint_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- xp_sqlmaint
ms.assetid: bda66e1b-6bbd-49be-b86e-37efc920e912
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2157462ca1f9509034f33208cce7aed2983ae4f2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62644801"
---
# <a name="xpsqlmaint-transact-sql"></a>xp_sqlmaint (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  呼叫**sqlmaint**公用程式字串，包含**sqlmaint**參數。 **Sqlmaint**公用程式會執行一組一個或多個資料庫上的維護作業。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
xp_sqlmaint 'switch_string'     
```  
  
## <a name="arguments"></a>引數  
 **'** *switch_string* **'**  
 這字串，包含**sqlmaint**公用程式參數。 參數和值必須用空格分隔。  
  
 **-嗎？** 參數不是適用於**xp_sqlmaint**。  
  
## <a name="return-code-values"></a>傳回碼值  
 無。 如果傳回錯誤**sqlmaint**公用程式會失敗。  
  
## <a name="remarks"></a>備註  
 如果使用 SQL Server 驗證，登入使用者呼叫此程序 **-U"***login_id***"** 並 **-P"***密碼***"** 參數前面會加上*switch_string*之前執行。 如果使用者使用 Windows 驗證登入時*switch_string*不會變更至傳遞**sqlmaint**。  
  
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
  
  
