---
title: "sys.sp_xtp_control_query_exec_stats (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 10/13/2015
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
- sys.sp_xtp_control_query_exec_stats_TSQL
- sys.sp_xtp_control_query_exec_stats
dev_langs: TSQL
helpviewer_keywords: sys.sp_xtp_control_query_exec_stats
ms.assetid: 4838125d-ad1e-479e-b7d2-42655e8f4f02
caps.latest.revision: "16"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f4bcc1bb453783a38c4b23e6526de1a804bde8f1
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2017
---
# <a name="sysspxtpcontrolqueryexecstats-transact-sql"></a>sys.sp_xtp_control_query_exec_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  針對執行個體的所有原生編譯預存程序或是特定的原生編譯預存程序，啟用個別查詢統計資料收集。  
  
 啟用統計資料收集時，效能會降低。 如果您只需要對一個或少數幾個原生編譯的預存程序進行疑難排解，可以只針對這幾個原生編譯的預存程序啟用統計資料收集。  
  
 若要啟用統計資料集合程序層級的所有原生編譯的預存程序，請參閱[sys.sp_xtp_control_proc_exec_stats &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-proc-exec-stats-transact-sql.md).  
  
## <a name="syntax"></a>語法  
  
```  
sp_xtp_control_query_exec_stats [ [ @new_collection_value = ] collection_value ],  
[ [ @database_id = ] database_id   
[ , [ @xtp_object_id = ] procedure_id ] ,   
[ @old_collection_value] ]  
```  
  
## <a name="arguments"></a>引數  
 @new_collection_value=*值*  
 決定程序層級統計資料收集為開啟 (1) 或關閉 (0)。  
  
 @new_collection_value設定為零[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]啟動。  
  
 @database_id= = *database_id*， @xtp_object_id = *procedure_id*  
 原生編譯預存程序的資料庫識別碼和物件識別碼。 如果啟用統計資料收集執行個體 ([sys.sp_xtp_control_proc_exec_stats &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-proc-exec-stats-transact-sql.md))，會收集原生編譯的預存程序的統計資料。 關閉執行個體上的統計資料收集並不會關閉個別原生編譯預存程序的統計資料收集。  
  
 使用[sys.databases &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)， [sys.procedures &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-procedures-transact-sql.md)， [DB_ID &#40;TRANSACT-SQL &#41;](../../t-sql/functions/db-id-transact-sql.md)，或[OBJECT_ID &#40;TRANSACT-SQL &#41;](../../t-sql/functions/object-id-transact-sql.md)若要取得資料庫和預存程序的 Id。  
  
 @old_collection_value=*值*  
 傳回目前狀態。  
  
## <a name="return-code"></a>傳回碼  
 0 代表成功。 非零代表失敗。  
  
## <a name="permissions"></a>Permissions  
 需要固定系統管理員 (sysadmin) 角色的成員資格。  
  
## <a name="code-sample"></a>程式碼範例  
 下列程式碼範例示範如何針對執行個體的所有原生編譯預存程序啟用統計資料收集，然後是針對特定的原生編譯預存程序啟用統計資料收集。  
  
```tsql   
DECLARE @c bit  
  
EXEC [sys].[sp_xtp_control_query_exec_stats] @new_collection_value = 1;  
  
EXEC sp_xtp_control_query_exec_stats @old_collection_value=@c output;  
SELECT @c AS 'collection status';  
  
EXEC [sys].[sp_xtp_control_query_exec_stats] @new_collection_value = 1,   
@database_id = 5, @xtp_object_id = 341576255;  
  
EXEC sp_xtp_control_query_exec_stats @database_id = 5,   
@xtp_object_id = 341576255, @old_collection_value=@c output;  
  
SELECT @c AS 'collection status';  
```  
  
## <a name="see-also"></a>請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [記憶體內部 OLTP &#40;記憶體內部最佳化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
