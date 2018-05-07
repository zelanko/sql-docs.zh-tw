---
title: sys.dm_os_performance_counters (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_os_performance_counters
- sys.dm_os_performance_counters_TSQL
- dm_os_performance_counters_TSQL
- sys.dm_os_performance_counters
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_performance_counters dynamic management view
ms.assetid: a1c3e892-cd48-40d4-b6be-2a9246e8fbff
caps.latest.revision: 34
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: d8e6e2ac166151375e01302a80916903859aab5a
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="sysdmosperformancecounters-transact-sql"></a>sys.dm_os_performance_counters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  針對伺服器所維護的每個效能計數器，各傳回一個資料列。 如需每個效能計數器資訊，請參閱[使用 SQL Server 物件](../../relational-databases/performance-monitor/use-sql-server-objects.md)。  
  
> [!NOTE]  
>  若要呼叫從[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用名稱**sys.dm_pdw_nodes_os_performance_counters**。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**object_name**|**nchar(128)**|這個計數器所屬的類別目錄。|  
|**counter_name**|**nchar(128)**|計數器的名稱。 若要取得計數器的詳細資訊，這是要從中計數器的清單中選取之標題的名稱[使用 SQL Server 物件](../../relational-databases/performance-monitor/use-sql-server-objects.md)。 |  
|**instance_name**|**nchar(128)**|計數器的特定執行個體名稱。 通常包含資料庫名稱。|  
|**cntr_value**|**bigint**|計數器的目前值。<br /><br /> **注意：**每秒計數器，這個值會累計。 必須以不連續時間間隔取樣值來計算該速率值。 任何兩個連續取樣值之間的差等於所使用的時間間隔速率。|  
|**cntr_type**|**int**|Windows 效能架構所定義的計數器類型。 請參閱[WMI 效能計數器型別](http://msdn2.microsoft.com/library/aa394569.aspx)MSDN 或您的 Windows Server 文件，如需有關效能計數器型別上。|  
|**pdw_node_id**|**int**|**適用於**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此發行版本上的節點識別碼。|  
  
## <a name="remarks"></a>備註  
 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的安裝執行個體無法顯示 Windows 作業系統的效能計數器，請使用下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查詢來確認效能計數器是否已停用。  
  
```  
SELECT COUNT(*) FROM sys.dm_os_performance_counters;  
```  
  
 如果傳回值為 0 個資料列，這就表示效能計數器已停用。 然後，您應該查看安裝程式記錄並搜尋錯誤 3409「請重新為此執行個體安裝 sqlctr.ini，並確定執行個體登入帳戶具有正確的登錄權限」。  這表示效能計數器未啟用。 緊接在 3409 錯誤前面的錯誤應該會指出效能計數器啟用失敗的根本原因。 如需有關安裝程式記錄檔的詳細資訊，請參閱[檢視與讀取 SQL Server Setup Log Files](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)。  
  
## <a name="permission"></a>權限

在[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`權限。   
在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`資料庫的權限。   
 
## <a name="examples"></a>範例  
 下列範例會傳回效能計數器值。  
  
```  
SELECT object_name, counter_name, instance_name, cntr_value, cntr_type  
FROM sys.dm_os_performance_counters;  
  
```  
  
## <a name="see-also"></a>另請參閱  
  [SQL Server 作業系統相關的動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [sys.sysperfinfo &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysperfinfo-transact-sql.md)  
  
  


