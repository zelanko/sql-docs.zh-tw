---
title: core. sp_remove_collector_type （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_remove_collector_type
- sp_remove_collector_type_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- core.sp_remove_collector_type stored procedure
- management data warehouse, data collector stored procedures
- sp_remove_collector_type
- data collector [SQL Server], stored procedures
ms.assetid: 88ceba25-e41a-405f-a416-bb68918a0024
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: ae6affebf2520b99fc82af17806dab8058313bc3
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82830438"
---
# <a name="coresp_remove_collector_type-transact-sql"></a>core.sp_remove_collector_type (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  從管理資料倉儲資料庫的 core.supported_collector_types 檢視表中移除項目。 此程序必須在管理資料倉儲資料庫的內容中執行。  
  
 core.supported_collector_types 檢視表會顯示可以將資料上傳到管理資料倉儲的已註冊收集器型別。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
core.sp_remove_collector_type [ @collector_type_uid = ] 'collector_type_uid'  
```  
  
## <a name="arguments"></a>引數  
 [ @collector_type_uid =] '*collector_type_uid*'  
 收集器類型的 GUID。 *collector_type_uid*是**uniqueidentifier**，沒有預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="permissions"></a>權限  
 需要**mdw_admin** （具有 EXECUTE 許可權）固定資料庫角色中的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例會從 core.supported_collector_types 檢視表中移除一般 T-SQL 查詢收集器型別。  
  
```  
USE <management_data_warehouse>;  
GO  
DECLARE @RC int;  
DECLARE @collector_type_uid uniqueidentifier;  
SELECT @collector_type_uid = (SELECT collector_type_uid FROM msdb.dbo.syscollector_collector_types WHERE name = N'Generic T-SQL Query Collector Type');  
EXECUTE @RC = core.sp_remove_collector_type @collector_type_uid;  
```  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的系統預存程式](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [&#40;Transact-sql&#41;的資料收集器預存程式](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [管理資料倉儲](../../relational-databases/data-collection/management-data-warehouse.md)  
  
  
