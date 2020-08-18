---
description: core.sp_add_collector_type (Transact-SQL)
title: core. sp_add_collector_type (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_collector_type
- sp_add_collector_type_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- core.sp_add_collector_type stored procedure
- management data warehouse, data collector stored procedures
- sp_add_collector_type
- data collector [SQL Server], stored procedures
ms.assetid: 1d981037-2147-464e-a456-7d8e479bce89
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: fcaf70019a38a0306d56c94e86ec6376626a2991
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88397024"
---
# <a name="coresp_add_collector_type-transact-sql"></a>core.sp_add_collector_type (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  在管理資料倉儲資料庫的 core.supported_collector_types 檢視表中加入新的項目。 此程序必須在管理資料倉儲資料庫的內容中執行。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
core.sp_add_collector_type [ @collector_type_uid = ] 'collector_type_uid'  
```  
  
## <a name="arguments"></a>引數  
 [ @collector_type_uid =] '*collector_type_uid*'  
 收集器類型的 GUID。 *collector_type_uid* 是 **uniqueidentifier**，沒有預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="permissions"></a>權限  
 需要 **mdw_admin** (中具有 EXECUTE 許可權) 固定資料庫角色的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例會將一般 T-SQL 查詢收集器型別加入 core.supported_collector_types 檢視表中。 根據預設，一般 T-SQL 查詢收集器型別已經存在。 因此，如果您在預設安裝中執行此程式碼，您將會收到一則訊息，指出此收集器型別已經存在。  
  
 如果您已經使用 core.sp_remove_collector_type 預存程序移除了一般 T-SQL 查詢收集器型別，然後想要重新加入它當做已註冊的收集器型別，以便可以將資料上傳到管理資料倉儲，此程式碼將會執行成功。  
  
```  
USE <management_data_warehouse>;  
GO  
DECLARE @RC int;  
DECLARE @collector_type_uid uniqueidentifier;  
SELECT @collector_type_uid = (SELECT collector_type_uid FROM msdb.dbo.syscollector_collector_types WHERE name = N'Generic T-SQL Query Collector Type');  
EXECUTE @RC = core.sp_add_collector_type @collector_type_uid;  
```  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的系統預存程式 ](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [資料收集器預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [管理資料倉儲](../../relational-databases/data-collection/management-data-warehouse.md)  
  
  
