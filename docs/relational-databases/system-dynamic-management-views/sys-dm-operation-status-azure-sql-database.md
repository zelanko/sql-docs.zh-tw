---
title: sys. dm_operation_status （Azure SQL Database） |Microsoft Docs
ms.custom: ''
ms.date: 06/05/2017
ms.service: sql-database
ms.reviewer: ''
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
author: stevestein
ms.author: sstein
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: c49e4e01dd8ddaf0667546a8cc221a7918f42c81
ms.sourcegitcommit: a154b3050b6e1993f8c3165ff5011ff5fbd30a7e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/30/2019
ms.locfileid: "70911208"
---
# <a name="sysdm_operation_status-azure-sql-database"></a>sys.dm_operation_status (Azure SQL Database)

[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

  傳回 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 伺服器中的資料庫上所執行之作業的相關資訊。  
  
|Column Name|資料類型|描述|  
|-----------------|---------------|-----------------|  
|session_activity_id|**ssNoversion**|作業的識別碼。 非 Null。|  
|resource_type|**int**|表示執行作業所在資源的類型。 非 Null。 在目前的版本中，這個檢視只會追蹤 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 上所執行的作業，對應的整數值為 0。|  
|resource_type_desc|**nvarchar(2048)**|執行作業所在的資源類型描述。 在目前的版本中，這個檢視只會追蹤 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 上所執行的作業。|  
|major_resource_id|**sql_variant**|執行作業所在的 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 的名稱。 非 Null。|  
|minor_resource_id|**sql_variant**|僅供內部使用。 非 Null。|  
|operation (作業)|**nvarchar(60)**|在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 上執行的運算，例如 CREATE 或 ALTER。|  
|state|**tinyint**|作業的狀態。<br /><br /> 0 = 暫止<br />1 = 進行中<br />2 = 已完成<br />3 = 失敗<br />4 = 已取消|  
|state_desc|**nvarchar(120)**|PENDING = 作業正在等候可用的資源或配額。<br /><br /> IN_PROGRESS = 作業已開始且正在進行。<br /><br /> COMPLETED = 作業已成功完成。<br /><br /> FAILED = 作業失敗。 如需詳細資訊，請參閱**error_desc**資料行。<br /><br /> CANCELLED = 使用者要求停止作業。|  
|percent_complete|**int**|已完成作業的百分比。 值不是連續的，而且有效的值如下所示。 Not Null。<br/><br/>0 = 作業未啟動<br/>50 = 作業進行中<br/>100 = 作業完成|  
|error_code|**int**|表示在作業失敗期間發生之錯誤的代碼。 如果這個值為 0，就表示作業已順利完成。|  
|error_desc|**nvarchar(2048)**|在作業失敗期間發生之錯誤的描述。|  
|error_severity|**int**|在作業失敗期間發生之錯誤的嚴重性層級。 如需錯誤嚴重性的詳細資訊，請參閱[資料庫引擎錯誤嚴重性](https://go.microsoft.com/fwlink/?LinkId=251052)。|  
|error_state|**int**|保留供未來使用。 我們無法保證未來的相容性。|  
|start_time|**datetime**|作業啟動時的時間戳記。|  
|last_modify_time|**datetime**|上次修改長時間執行作業之記錄時的時間戳記。 如果作業順利完成，這個欄位會顯示作業完成時的時間戳記。|  
  
## <a name="permissions"></a>Permissions  
 此視圖僅適用于**master**資料庫中的伺服器層級主體登入。  
  
## <a name="remarks"></a>Remarks  
 若要使用此視圖，您必須連接到**master**資料庫。 使用 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 伺服器的**master**資料庫中的 [`sys.dm_operation_status`] 視圖，追蹤在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]上執行之下列作業的狀態：  
  
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
 顯示與資料庫 ' mydb ' 相關聯的最近異地複寫作業。  
  
```  
SELECT * FROM sys.dm_operation_status   
   WHERE major_resource_id = 'myddb'   
   ORDER BY start_time DESC;  
```  
  
## <a name="see-also"></a>另請參閱  
 [異地複寫動態管理檢視和功能&#40;Azure SQL Database&#41; ](../../relational-databases/system-dynamic-management-views/geo-replication-dynamic-management-views-and-functions-azure-sql-database.md)   
 [dm_geo_replication_link_status &#40;Azure SQL Database&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-geo-replication-link-status-azure-sql-database.md)   
 [geo_replication_links &#40;Azure SQL Database&#41; ](../../relational-databases/system-dynamic-management-views/sys-geo-replication-links-azure-sql-database.md)   
 [ALTER DATABASE &#40;Azure SQL Database&#41;](../../t-sql/statements/alter-database-azure-sql-database.md)  
  
  
