---
title: sp_cycle_agent_errorlog （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cycle_agent_errorlog
- sp_cycle_agent_errorlog_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cycle_agent_errorlog
ms.assetid: 8aa96182-60b7-4d7b-b2a7-ccce70378c6e
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 8fcb9bad5548107ef3a9294f22696abeacbdedcd
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82826242"
---
# <a name="sp_cycle_agent_errorlog-transact-sql"></a>sp_cycle_agent_errorlog (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  關閉目前的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 錯誤記錄檔，依照類似伺服器重新啟動的方式來循環處理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 錯誤記錄副檔名的號碼。 新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 錯誤記錄會有一行指出已建立新記錄。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_cycle_agent_errorlog  
```  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 每次 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 啟動代理程式時，目前的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agent 錯誤記錄檔都會重新命名為**SQLAgent。 1**;**SQLAgent**會變成**SQLAgent。 2**， **SQLAgent**會變成**SQLAgent。 3**，依此類推。 **sp_cycle_agent_errorlog**可讓您迴圈錯誤記錄檔，而不需要停止和啟動伺服器。  
  
 這個預存程式必須從**msdb**資料庫中執行。  
  
## <a name="permissions"></a>權限  
 **Sp_cycle_agent_errorlog**的執行許可權僅限於**系統管理員（sysadmin** ）固定伺服器角色的成員。  
  
## <a name="examples"></a>範例  
 下列範例會循環處理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 錯誤記錄。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_cycle_agent_errorlog ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_cycle_errorlog &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-cycle-errorlog-transact-sql.md)  
  
  
