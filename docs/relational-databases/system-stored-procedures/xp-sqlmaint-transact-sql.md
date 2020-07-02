---
title: xp_sqlmaint （Transact-sql） |Microsoft Docs
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
ms.openlocfilehash: ac6461e522973b43926b66b6e525526ae6952d85
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85755514"
---
# <a name="xp_sqlmaint-transact-sql"></a>xp_sqlmaint (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  使用包含**sqlmaint**參數的字串來呼叫**sqlmaint**公用程式。 **Sqlmaint**公用程式會在一或多個資料庫上執行一組維護作業。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
xp_sqlmaint 'switch_string'     
```  
  
## <a name="arguments"></a>引數  
 **'** *switch_string* **'**  
 這是包含**sqlmaint**公用程式參數的字串。 參數和值必須用空格分隔。  
  
 **-？** 參數對**xp_sqlmaint**無效。  
  
## <a name="return-code-values"></a>傳回碼值  
 無。 如果**sqlmaint**公用程式失敗，則傳回錯誤。  
  
## <a name="remarks"></a>備註  
 如果這個程式是由使用 SQL Server Authentication 登入的使用者所呼叫，則在執行之前，會在*switch_string*前面加上 **-U "***login_id***"** 和 **-P "***password***"** 參數。 如果使用者是使用 Windows 驗證登入，則會傳遞*switch_string* ，而不會變更為**sqlmaint**。  
  
## <a name="permissions"></a>權限  
 需要**系統管理員（sysadmin** ）固定伺服器角色中的成員資格。  
  
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
  
  
