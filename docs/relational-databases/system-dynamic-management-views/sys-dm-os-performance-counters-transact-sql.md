---
title: sys.databases dm_os_performance_counters （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5c7b4d78f73af003e93bc662f10f1f95acda2b6a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68265715"
---
# <a name="sysdm_os_performance_counters-transact-sql"></a>sys.dm_os_performance_counters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  針對伺服器所維護的每個效能計數器，各傳回一個資料列。 如需每個效能計數器的詳細資訊，請參閱[使用 SQL Server 物件](../../relational-databases/performance-monitor/use-sql-server-objects.md)。  
  
> [!NOTE]  
>  若要從[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]呼叫此，請使用**dm_pdw_nodes_os_performance_counters**的名稱。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**object_name**|**nchar(128)**|這個計數器所屬的類別目錄。|  
|**counter_name**|**nchar(128)**|計數器的名稱。 若要取得計數器的詳細資訊，這是[使用 SQL Server 物件](../../relational-databases/performance-monitor/use-sql-server-objects.md)的計數器清單中所要選取的主題名稱。 |  
|**instance_name**|**nchar(128)**|計數器的特定執行個體名稱。 通常包含資料庫名稱。|  
|**cntr_value**|**bigint**|計數器的目前值。<br /><br /> **注意：** 針對每秒的計數器，此值為累計。 必須以不連續時間間隔取樣值來計算該速率值。 任何兩個連續取樣值之間的差等於所使用的時間間隔速率。|  
|**cntr_type**|**int**|Windows 效能架構所定義的計數器類型。 如需效能計數器類型的詳細資訊，請參閱檔上的[WMI 效能計數器類型](https://docs.microsoft.com/windows/desktop/WmiSdk/wmi-performance-counter-types)或您的 Windows Server 檔。|  
|**pdw_node_id**|**int**|**適用**于： [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此散發所在節點的識別碼。|  
  
## <a name="remarks"></a>備註  
 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的安裝執行個體無法顯示 Windows 作業系統的效能計數器，請使用下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查詢來確認效能計數器是否已停用。  
  
```  
SELECT COUNT(*) FROM sys.dm_os_performance_counters;  
```  
  
 如果傳回值為 0 個資料列，這就表示效能計數器已停用。 然後，您應該查看安裝程式記錄並搜尋錯誤 3409「請重新為此執行個體安裝 sqlctr.ini，並確定執行個體登入帳戶具有正確的登錄權限」。  這表示效能計數器未啟用。 緊接在 3409 錯誤前面的錯誤應該會指出效能計數器啟用失敗的根本原因。 如需安裝程式記錄檔的詳細資訊，請參閱[查看和讀取 SQL Server 安裝程式記錄](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)檔。  
  
## <a name="permission"></a>權限

在[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]上， `VIEW SERVER STATE`需要許可權。   
在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]高階層級上， `VIEW DATABASE STATE`需要資料庫的許可權。 在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] [標準] 和 [基本] 層上，需要**伺服器管理員**或**Azure Active Directory 系統管理員**帳戶。   
 
## <a name="examples"></a>範例  
 下列範例會傳回效能計數器值。  
  
```  
SELECT object_name, counter_name, instance_name, cntr_value, cntr_type  
FROM sys.dm_os_performance_counters;  
  
```  
  
## <a name="see-also"></a>另請參閱  
  [SQL Server 作業系統相關的動態管理 Views &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [sys.sysperfinfo &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysperfinfo-transact-sql.md)  
  
  


