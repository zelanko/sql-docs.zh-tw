---
title: sp_enum_sqlagent_subsystems （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_enum_sqlagent_subsystems
- sp_enum_sqlagent_subsystems_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_enum_sqlagent_subsystems
ms.assetid: 019a3c9d-bac3-495b-a70a-2c19f1d2e20e
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 356357df8d2c8a3202a5ff088ba2c277aa9fd73c
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82831111"
---
# <a name="sp_enum_sqlagent_subsystems-transact-sql"></a>sp_enum_sqlagent_subsystems (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  列出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 子系統。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_enum_sqlagent_subsystems  
```  
  
## <a name="arguments"></a>引數  
 無  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**子系統**|**nvarchar(40)**|子系統的名稱。|  
|**描述**|**nvarchar(512)**|子系統的描述。|  
|**subsystem_dll**|**Nvarchar （510）**|子系統所在的 DLL 模組。|  
|**agent_exe**|**Nvarchar （510）**|子系統所用的可執行模組。|  
|**start_entry_point**|**nvarchar(30)**|在作業步驟執行期間，SQL Server Agent 所呼叫的程序。|  
|**event_entry_point**|**nvarchar(30)**|在作業步驟執行期間，SQL Server Agent 所呼叫的程序。|  
|**stop_entry_point**|**nvarchar(30)**|在作業步驟執行期間，SQL Server Agent 所呼叫的程序。|  
|**max_worker_threads**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 將針對這個子系統來啟動的最大執行緒數目。|  
|**subsystem_id**|**int**|子系統的識別碼。|  
  
## <a name="remarks"></a>備註  
 這個程序會列出執行個體中可用的子系統。  
  
## <a name="permissions"></a>權限  
 依預設，只有 **系統管理員 (sysadmin)** 固定伺服器角色的成員，才能夠執行這個預存程序。 其他使用者必須被授與 **msdb** 資料庫的 **SQLAgentOperatorRole** 固定資料庫角色。  
  
 如需**SQLAgentOperatorRole**的詳細資訊，請參閱[SQL Server Agent 固定資料庫角色](../../ssms/agent/sql-server-agent-fixed-database-roles.md)。  
  
## <a name="see-also"></a>另請參閱  
 [實行 SQL Server Agent 安全性](../../ssms/agent/implement-sql-server-agent-security.md)   
 [sp_add_jobstep &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md)  
  
  
