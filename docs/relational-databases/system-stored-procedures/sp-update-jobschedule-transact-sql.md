---
description: sp_update_jobschedule (Transact-SQL)
title: sp_update_jobschedule (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_update_jobschedule_TSQL
- sp_update_jobschedule
dev_langs:
- TSQL
helpviewer_keywords:
- sp_update_jobschedule
ms.assetid: 4df02594-4cd1-49a9-8d97-37c44e4d5423
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 92aa7a001a365ed9d24c0e856b304b723e57c9c0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88473520"
---
# <a name="sp_update_jobschedule-transact-sql"></a>sp_update_jobschedule (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  變更指定作業的排程設定。  
  
 **sp_update_jobschedule** 僅為了回溯相容性而提供。  
  
> [!IMPORTANT]
>  如需舊版 Microsoft SQL Server 中使用之語法的詳細資訊，請參閱 Transact-sql Referencefor Microsoft SQL Server 2000 *。*  
  
## <a name="remarks"></a>備註  
 現在，您可以在作業之外，獨立管理作業排程。 若要更新排程，請使用 **sp_update_schedule**。  
  
## <a name="permissions"></a>權限  
 依預設，只有 **系統管理員 (sysadmin)** 固定伺服器角色的成員，才能夠執行這個預存程序。 其他使用者必須被授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **資料庫的下列其中一個** Agent 固定資料庫角色。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 如需這些角色權限的詳細資訊，請參閱 [SQL Server Agent 固定資料庫角色](../../ssms/agent/sql-server-agent-fixed-database-roles.md)。  
  
 只有 **系統管理員（sysadmin** ）的成員可以使用此預存程式來更新其他使用者所擁有的作業排程。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的 SQL Server Agent 預存程式 ](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [sp_update_schedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-update-schedule-transact-sql.md)  
  
  
