---
title: sp_syscollector_set_warehouse_instance_name （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
ms.openlocfilehash: 6e21096971b9a0891d2c51c5fce34c119b454f0b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68010596"
---
# <a name="sp_syscollector_set_warehouse_instance_name-transact-sql"></a>sp_syscollector_set_warehouse_instance_name (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對用來連接至管理資料倉儲的連接字串，指定執行個體名稱。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_syscollector_set_warehouse_instance_name [ @instance_name = ] 'instance_name'  
```  
  
## <a name="arguments"></a>引數  
 [ @instance_name = ]'*instance_name*'  
 這是執行個體名稱。 *instance_name*是**sysname** ，而且預設為本機實例（如果是 Null 的話）。  
  
> **注意：**  _instance_name_必須是完整的實例名稱，其中包含電腦名稱稱和實例名稱，其格式為*computerName*\\*instanceName*。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 您必須先停用資料收集器，然後再變更這項資料收集器範圍組態。 如果資料收集器為啟用狀態，這個程序就會失敗。  
  
 若要查看目前的實例名稱，請查詢[syscollector_config_store](../../relational-databases/system-catalog-views/syscollector-config-store-transact-sql.md)系統檢視。  
  
## <a name="permissions"></a>權限  
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
 [&#40;Transact-sql&#41;的資料收集器預存程式](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [syscollector_config_store &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-config-store-transact-sql.md)  
  
  
