---
title: sys.dm_operation_status (Azure SQL Database) |Microsoft 文件
ms.custom: ''
ms.date: 06/05/2017
ms.prod: ''
ms.prod_service: sql-database, sql-data-warehouse
ms.reviewer: ''
ms.service: sql-database
ms.component: dmv's
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_operation_status_TSQL
- dm_operation_status
- sys.dm_operation_status
- sys.dm_operation_status_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dm_operation_status dynamic management view
- sys.dm_operation_status dynamic management view
ms.assetid: cc847784-7f61-4c69-8b78-5f971bb24d61
caps.latest.revision: 17
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 6d88b5a770363e4f34dead9ef07f3d8db5dea067
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmoperationstatus-azure-sql-database"></a>sys.dm_operation_status (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

  傳回 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 伺服器中的資料庫上所執行之作業的相關資訊。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|session_activity_id|**uniqueidentifier**|作業的識別碼。 非 Null。|  
|resource_type|**int**|表示執行作業所在資源的類型。 非 Null。 在目前的版本中，這個檢視只會追蹤 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 上所執行的作業，對應的整數值為 0。|  
|resource_type_desc|**nvarchar(2048)**|執行作業所在的資源類型描述。 在目前的版本中，這個檢視只會追蹤 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 上所執行的作業。|  
|major_resource_id|**sql_variant**|執行作業所在的 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 的名稱。 非 Null。|  
|minor_resource_id|**sql_variant**|僅供內部使用。 非 Null。|  
|operation (作業)|**nvarchar(60)**|在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 上執行的運算，例如 CREATE 或 ALTER。|  
|state|**tinyint**|作業的狀態。<br /><br /> 0 = 暫止<br />1 = 進行中<br />2 = 已完成<br />3 = 失敗<br />4 = 已取消|  
|state_desc|**nvarchar(120)**|PENDING = 作業正在等候可用的資源或配額。<br /><br /> IN_PROGRESS = 作業已開始且正在進行。<br /><br /> COMPLETED = 作業已成功完成。<br /><br /> FAILED = 作業失敗。 請參閱**error_desc**如需詳細資訊的資料行。<br /><br /> CANCELLED = 使用者要求停止作業。|  
|percent_complete|**int**|已完成作業的百分比。 值不連續且有效的值如下所列。 不是 NULL。<br/><br/>0 = 未啟動的作業<br/>50 = 作業正在進行中<br/>100 = 作業完成|  
|error_code|**int**|表示在作業失敗期間發生之錯誤的代碼。 如果這個值為 0，就表示作業已順利完成。|  
|error_desc|**nvarchar(2048)**|在作業失敗期間發生之錯誤的描述。|  
|error_severity|**int**|在作業失敗期間發生之錯誤的嚴重性層級。 如需錯誤嚴重性的詳細資訊，請參閱[Database Engine 錯誤嚴重性](http://go.microsoft.com/fwlink/?LinkId=251052)。|  
|error_state|**int**|保留供日後使用。 我們無法保證未來的相容性。|  
|start_time|**datetime**|作業啟動時的時間戳記。|  
|last_modify_time|**datetime**|上次修改長時間執行作業之記錄時的時間戳記。 如果作業順利完成，這個欄位會顯示作業完成時的時間戳記。|  
  
## <a name="permissions"></a>Permissions  
 此檢視僅供以**主要**伺服器層級主體登入的資料庫。  
  
## <a name="remarks"></a>備註  
 若要使用此檢視，您必須連接到**主要**資料庫。 使用`sys.dm_operation_status`檢視中**主要**資料庫[!INCLUDE[ssSDS](../../includes/sssds-md.md)]伺服器追蹤上執行下列作業的狀態[!INCLUDE[ssSDS](../../includes/sssds-md.md)]:  
  
-   建立資料庫  
  
-   複製資料庫。 資料庫複製會在來源和目標伺服器的這個檢視中，建立一筆記錄。  
  
-   改變資料庫  
  
-   變更服務層的效能層級  
  
-   變更資料庫的服務層，例如從 Basic 變更為 Standard。  
  
-   設定異地備援關聯性  
  
-   終止異地備援關聯性  
  
-   對話方塊的  
  
-   刪除資料庫  
  
## <a name="example"></a>範例  
 顯示與資料庫 'mydb' 相關聯的最新地理複寫作業。  
  
```  
SELECT * FROM sys.dm_ operation_status   
   WHERE major_resource_id = ‘myddb’   
   ORDER BY start_time DESC;  
```  
  
## <a name="see-also"></a>另請參閱  
 [地理複寫動態管理檢視和函數&#40;Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/geo-replication-dynamic-management-views-and-functions-azure-sql-database.md)   
 [sys.dm_geo_replication_link_status &#40;Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-geo-replication-link-status-azure-sql-database.md)   
 [sys.geo_replication_links &#40;Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/sys-geo-replication-links-azure-sql-database.md)   
 [ALTER DATABASE &#40;Azure SQL Database&#41;](../../t-sql/statements/alter-database-azure-sql-database.md)  
  
  
