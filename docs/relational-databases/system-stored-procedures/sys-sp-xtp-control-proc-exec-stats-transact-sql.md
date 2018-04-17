---
title: sys.sp_xtp_control_proc_exec_stats (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.sp_xtp_control_proc_exec_stats
- sys.sp_xtp_control_proc_exec_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_xtp_control_proc_exec_stats
ms.assetid: f5119808-76a1-4522-8529-9e02ee39adcb
caps.latest.revision: 15
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 36453b1ba1f148822bcf625facb3c40d438e18e4
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sysspxtpcontrolprocexecstats-transact-sql"></a>sys.sp_xtp_control_proc_exec_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  啟用執行個體的原生編譯預存程序的統計資料收集。  
  
 若要啟用原生編譯的預存程序的查詢層級的統計資料收集，請參閱[sys.sp_xtp_control_query_exec_stats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql.md)。  
  
## <a name="syntax"></a>語法  
  
```  
sp_xtp_control_proc_exec_stats [ [ @new_collection_value = ] collection_value ], [ @old_collection_value]  
```  
  
## <a name="arguments"></a>引數  
 @new_collection_value =*值*  
 決定程序層級統計資料收集為開啟 (1) 或關閉 (0)。  
  
 @new_collection_value 設定為零[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或資料庫啟動。  
  
 @old_collection_value =*值*  
 傳回目前狀態。  
  
## <a name="return-code"></a>傳回碼  
 0 代表成功。 非零代表失敗。  
  
## <a name="permissions"></a>Permissions  
 需要固定系統管理員 (sysadmin) 角色的成員資格。  
  
## <a name="code-samples"></a>程式碼範例  
 若要設定@new_collection_value和值的查詢 @new_collection_value:  
  
```  
exec [sys].[sp_xtp_control_proc_exec_stats] @new_collection_value = 1  
declare @c bit  
exec sp_xtp_control_proc_exec_stats @old_collection_value=@c output  
select @c as 'collection status'  
```  
  
## <a name="see-also"></a>另請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [記憶體內部 OLTP &#40;記憶體內部最佳化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
