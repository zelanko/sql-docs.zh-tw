---
title: "sp_syscollector_set_warehouse_instance_name (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_syscollector_set_warehouse_instance_name_TSQL
- sp_syscollector_set_warehouse_instance_name
dev_langs:
- TSQL
helpviewer_keywords:
- data collector [SQL Server], stored procedures
- sp_syscollector_set_warehouse_instance_name
ms.assetid: 5320fcd4-bed1-468f-b784-a5e10fcfaeb6
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6d82ac58a086f09b104515300d92704e62b6aea1
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/03/2018
---
# <a name="spsyscollectorsetwarehouseinstancename-transact-sql"></a>sp_syscollector_set_warehouse_instance_name (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對用來連接至管理資料倉儲的連接字串，指定執行個體名稱。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_syscollector_set_warehouse_instance_name [ @instance_name = ] 'instance_name'  
```  
  
## <a name="arguments"></a>引數  
 [ @instance_name = ] '*instance_name*'  
 這是執行個體名稱。 *instance_name*是**sysname** ，預設值為本機執行個體，如果是 NULL。  
  
> **注意：***instance_name*必須是完整的執行個體名稱，其中包含電腦名稱與執行個體名稱，表單*computerName* \\ *instanceName*。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 您必須先停用資料收集器，然後再變更這項資料收集器範圍組態。 如果資料收集器為啟用狀態，這個程序就會失敗。  
  
 若要檢視目前的執行個體名稱，請查詢[syscollector_config_store](../../relational-databases/system-catalog-views/syscollector-config-store-transact-sql.md)系統檢視表。  
  
## <a name="permissions"></a>Permissions  
 需要 dc_admin (具有 EXECUTE 權限) 固定資料庫角色中的成員資格，才能執行此程序。  
  
## <a name="examples"></a>範例  
 下列範例將說明如何在遠端伺服器上設定資料收集器使用管理資料倉儲執行個體。 在這個範例中，遠端伺服器名為 `RemoteSERVER`，而且資料庫安裝在預設執行個體上。  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_set_warehouse_instance_name N'RemoteSERVER'; -- the default instance is assumed on the remote server  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料收集器預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [syscollector_config_store &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-config-store-transact-sql.md)  
  
  
