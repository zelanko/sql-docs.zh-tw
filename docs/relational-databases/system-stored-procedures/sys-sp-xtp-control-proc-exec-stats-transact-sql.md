---
title: sys.databases sp_xtp_control_proc_exec_stats （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sp_xtp_control_proc_exec_stats
- sys.sp_xtp_control_proc_exec_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_xtp_control_proc_exec_stats
ms.assetid: f5119808-76a1-4522-8529-9e02ee39adcb
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 940caad59adf191e0ed1fe550707788de820c6b7
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82814490"
---
# <a name="syssp_xtp_control_proc_exec_stats-transact-sql"></a>sys.sp_xtp_control_proc_exec_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  啟用執行個體的原生編譯預存程序的統計資料收集。  
  
 若要在原生編譯預存程式的查詢層級啟用統計資料收集，請參閱[sys.databases &#40;transact-sql&#41;sp_xtp_control_query_exec_stats ](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql.md)。  
  
## <a name="syntax"></a>語法  
  
```  
sp_xtp_control_proc_exec_stats [ [ @new_collection_value = ] collection_value ], [ @old_collection_value]  
```  
  
## <a name="arguments"></a>引數  
 @new_collection_value=*值*  
 決定程序層級統計資料收集為開啟 (1) 或關閉 (0)。  
  
 @new_collection_value當或資料庫啟動時，會設定為零 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
 @old_collection_value=*值*  
 傳回目前狀態。  
  
## <a name="return-code"></a>傳回碼  
 0 代表成功。 非零代表失敗。  
  
## <a name="permissions"></a>權限  
 需要固定系統管理員 (sysadmin) 角色的成員資格。  
  
## <a name="code-samples"></a>程式碼範例  
 若要設定 @new_collection_value 並查詢的值@new_collection_value:  
  
```  
exec [sys].[sp_xtp_control_proc_exec_stats] @new_collection_value = 1  
declare @c bit  
exec sp_xtp_control_proc_exec_stats @old_collection_value=@c output  
select @c as 'collection status'  
```  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的系統預存程式](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [記憶體內部 OLTP &#40;記憶體內部最佳化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
