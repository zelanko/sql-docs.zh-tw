---
title: 已停止的 SQL server 2014 資料庫引擎功能 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- VIA protocol
- unsupported features [SQL Server]
- SQL Mail
- discontinued functionality [SQL Server]
- RESTORE WITH DBO_ONLY
- BACKUP WITH PASSWORD
- user instances enabled
- BACKUP WITH MEDIAPASSWORD
- AWE
- SQL-DMO
- '*= and =*'
- 80 compatibility levels
- COMPUTE BY
- user instance timeout
- sp_dropalias
- COMPUTE
- WITH APPEND
- sys.database_principal_aliases
- sp_dboption
- DATABASEPROPERTY
- FASTFIRSTROW hint
- SET DISABLE_DEF_CNST_CHK
ms.assetid: d686cdf0-d11d-4dba-9ec8-de1a5f189f25
caps.latest.revision: 93
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 81ceffcd3009906b41316a7a9778a0b38ded7b29
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36036636"
---
# <a name="discontinued-database-engine-functionality-in-sql-server-2014"></a>SQL Server 2014 中已停止的 Database Engine 功能
  本主題描述 [!INCLUDE[ssDE](../includes/ssde-md.md)] 中不再可用的 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]功能。  
  
## <a name="discontinued-features-in-includesssql14includessssql14-mdmd"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 下表列出已在 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 中移除的功能。  
  
|類別目錄|已停止的功能|取代|  
|--------------|--------------------------|-----------------|  
|相容性層級|90 相容性層級|資料庫至少必須設定為相容性層級 100。 當相容性層級低於 100 的資料庫升級為 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 時，資料庫的相容性層級會在升級作業期間設定為 100。|  
  
## <a name="discontinued-features-in-includesssql11includessssql11-mdmd"></a>[!INCLUDE[ssSQL11](../includes/sssql11-md.md)]  
 下表列出已在 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 中移除的功能。  
  
|類別目錄|已停止的功能|取代|  
|--------------|--------------------------|-----------------|  
|備份與還原|**BACKUP {DATABASE&#124;記錄} WITH PASSWORD**和**備份 {資料庫&#124;記錄} WITH MEDIAPASSWORD**已停用。 **RESTORE {DATABASE&#124;記錄} 與 [MEDIA] PASSWORD**繼續被取代。|無|  
|備份與還原|**RESTORE {DATABASE&AMP;#124;記錄}...WITH DBO_ONLY**|**RESTORE {DATABASE&AMP;#124;記錄}......WITH RESTRICTED_USER**|  
|相容性層級|80 相容性層級|資料庫至少必須設定為相容性層級 90。|  
|組態選項|`sp_configure 'user instance timeout'` 和 `'user instances enabled'`|使用本機資料庫功能。 如需詳細資訊，請參閱[SqlLocalDB 公用程式](../tools/sqllocaldb-utility.md)|  
|連接通訊協定|VIA 通訊協定支援已停用。|請改用 TCP。|  
|資料庫物件|觸發程序上的 `WITH APPEND` 子句|請重新建立整個觸發程序。|  
|資料庫選項|`sp_dboption`|`ALTER DATABASE`|  
|郵件|SQL Mail|使用 Database Mail。 如需詳細資訊，請參閱[Database Mail](../relational-databases/database-mail/database-mail.md)和[Use Database Mail Instead of SQL Mail](../relational-databases/policy-based-management/use-database-mail-instead-of-sql-mail.md)。|  
|記憶體管理|32 位元 Address Windowing Extensions (AWE) 和 32 位元 Hot Add Memory 支援。|使用 64 位元作業系統。|  
|中繼資料|`DATABASEPROPERTY`|`DATABASEPROPERTYEX`|  
|可程式性|SQL Server Distributed Management Objects (SQL-DMO)|SQL Server 管理物件 (SMO)|  
|查詢提示|`FASTFIRSTROW` 提示|`OPTION (FAST` *n* `)`。|  
|遠端伺服器|使用者已無法使用 `sp_addserver` 建立新的遠端伺服器。 `sp_addserver` 與 'local' 選項仍可使用。 升級期間所保留或複寫所建立的遠端伺服器仍然可以使用。|使用連結的伺服器取代遠端伺服器。|  
|Security|`sp_dropalias`|以使用者帳戶和資料庫角色的組合來取代別名。 使用`sp_dropalias`在升級的資料庫中移除別名。|  
|Security|Version 參數**PWDCOMPARE**表示由登入值早於[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]2000年已停止。|無|  
|SMO 中的 Service Broker 可程式性|**Microsoft.SqlServer.Management.Smo.Broker.BrokerPriority** 類別不再實作 **Microsoft.SqlServer.Management.Smo.IObjectPermission** 介面。||  
|SET 選項|`SET DISABLE_DEF_CNST_CHK`|無。|  
|系統資料表|sys.database_principal_aliases|請使用角色，而非別名。|  
|Transact-SQL|`RAISERROR` 格式的 `RAISERROR integer 'string'` 已停止。|請使用目前的 **RAISERROR(…)** 語法重寫陳述式。|  
|Transact-SQL 語法|`COMPUTE / COMPUTE BY`|使用 `ROLLUP`|  
|Transact-SQL 語法|使用**\* =** 和 **=\***|使用 ANSI 聯結語法。 如需詳細資訊，請參閱 [FROM (Transact-SQL)。](http://msdn.microsoft.com/library/ms177634\(SQL.105\).aspx)|  
|XEvents|databases_data_file_size_changed databases_log_file_size_changed<br /><br /> eventdatabases_log_file_used_size_changed<br /><br /> locks_lock_timeouts_greater_than_0<br /><br /> locks_lock_timeouts|由 database_file_size_change event，database_file_size_change 取代<br /><br /> database_file_size_change event<br /><br /> lock_timeout_greater_than_0<br /><br /> lock_timeout|  
  
 **其他 XEvent 變更**  
  
 **resource_monitor_ring_buffer_record**：  
  
-   移除的欄位：single_pages_kb、multiple_pages_kb  
  
-   加入的欄位：target_kb、pages_kb  
  
 **memory_node_oom_ring_buffer_recorded**：  
  
-   移除的欄位：single_pages_kb、multiple_pages_kb  
  
-   加入的欄位：target_kb、pages_kb  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 2014 中已被取代的 Database Engine 功能](deprecated-database-engine-features-in-sql-server-2016.md)  
  
  