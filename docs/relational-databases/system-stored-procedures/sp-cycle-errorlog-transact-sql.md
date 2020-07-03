---
title: sp_cycle_errorlog （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cycle_errorlog_TSQL
- sp_cycle_errorlog
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cycle_errorlog
ms.assetid: 61a12cbf-78a3-4052-8604-3b29d07573fd
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: ad631a10998f3628084581ea25faa53151f12af0
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85868256"
---
# <a name="sp_cycle_errorlog-transact-sql"></a>sp_cycle_errorlog (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  關閉目前的錯誤記錄檔，依照類似伺服器重新啟動的方式來循環處理錯誤記錄副檔名的號碼。 新的錯誤記錄包含版本和著作權資訊，還會有一行指出已建立新記錄。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_cycle_errorlog  
```  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 每次 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 啟動時，目前的錯誤記錄檔都會重新命名為錯誤記錄檔 **。 1**;**錯誤**記錄檔。1變成錯誤記錄檔 **。 2**，錯誤記錄檔。 **2**會變成錯誤記錄檔 **。 3**，依此類推。 **sp_cycle_errorlog**可讓您迴圈錯誤記錄檔，而不需要停止和啟動伺服器。  
  
## <a name="permissions"></a>權限  
 **Sp_cycle_errorlog**的執行許可權僅限於**系統管理員（sysadmin** ）固定伺服器角色的成員。  
  
## <a name="examples"></a>範例  
 下列範例會循環處理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔。  
  
```  
EXEC sp_cycle_errorlog ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的系統預存程式](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sp_cycle_agent_errorlog &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-cycle-agent-errorlog-transact-sql.md)  
  
  
