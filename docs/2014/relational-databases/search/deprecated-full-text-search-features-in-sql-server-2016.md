---
title: SQL Server 2014 中的全文檢索搜尋功能已被取代 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: search
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- deprecated features [full-text search]
- full-text search [SQL Server], deprecated features
- full-text queries [SQL Server], proximity
ms.assetid: ab0d799c-ba79-4459-837b-c4862730dafd
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 140e7262d3cfc66e956ee0fc53ea1009d7afda0b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37179685"
---
# <a name="deprecated-full-text-search-features-in-sql-server-2014"></a>SQL Server 2014 中已被取代的全文檢索搜尋功能
  本主題描述 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中仍然可用之已被取代的全文檢索搜尋功能。 這些功能將在未來的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本中移除。 已被取代的功能不應在新應用程式中使用。  
  
 您可以使用 **SQL Server:Deprecated Features** 物件效能計數器和追蹤事件來監視已被取代之功能的使用。 如需詳細資訊，請參閱[使用 SQL Server 物件](../performance-monitor/use-sql-server-objects.md)。  
  
## <a name="features-not-supported-in-the-next-version-of-sql-server"></a>下一版的 SQL Server 不支援的功能  
 下一版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中將不支援下列全文檢索搜尋功能。  
  
|已被取代的功能|取代|功能名稱|功能識別碼|  
|------------------------|-----------------|------------------|----------------|  
|FULLTEXTCATALOGPROPERTY 屬性：LogSize|無。|FULLTEXTCATALOGPROPERTY **('LogSize')**|211|  
|FULLTEXTSERVICEPROPERTY 屬性：<br /><br /> ConnectTimeout<br /><br /> DataTimeout|無。|FULLTEXTSERVICEPROPERTY **('ConnectTimeout')**<br /><br /> FULLTEXTSERVICEPROPERTY **('DataTimeout'**)|210<br /><br /> 209|  
|sp_fulltext_catalog|CREATE FULL CATALOG<br /><br /> ALTER FULLTEXT CATALOG<br /><br /> DROP FULLTEXT CATALOG|sp_fulltext_catalog|84|  
|sp_fulltext_column<br /><br /> sp_fulltext_database<br /><br /> sp_fulltext_table|CREATE FULL INDEX<br /><br /> ALTER FULLTEXT INDEX<br /><br /> DROP FULLTEXT INDEX|sp_fulltext_column<br /><br /> sp_fulltext_database<br /><br /> sp_fulltext_table|86<br /><br /> 87<br /><br /> 85|  
|sp_help_fulltext_catalogs<br /><br /> sp_help_fulltext_catalog_components<br /><br /> sp_help_fulltext_catalogs_cursor<br /><br /> sp_help_fulltext_columns<br /><br /> sp_help_fulltext_columns_cursor<br /><br /> sp_help_fulltext_tables<br /><br /> sp_help_fulltext_tables_cursor|sys.fulltext_catalogs<br /><br /> sys.fulltext_index_columns<br /><br /> sys.fulltext_indexes|sp_help_fulltext_catalogs<br /><br /> sp_help_fulltext_catalog_components<br /><br /> sp_help_fulltext_catalogs_cursor<br /><br /> sp_help_fulltext_columns<br /><br /> sp_help_fulltext_columns_cursor<br /><br /> sp_help_fulltext_table<br /><br /> sp_help_fulltext_tables_cursor|88<br /><br /> 203<br /><br /> 90<br /><br /> 92<br /><br /> 93<br /><br /> 91<br /><br /> 89|  
|sp_fulltext_service action values：clean_up、connect_timeout 和 data_timeout 會傳回零|無|sp_fulltext_service @action=clean_up<br /><br /> sp_fulltext_service @action=connect_timeout<br /><br /> sp_fulltext_service @action=data_timeout|116<br /><br /> 117<br /><br /> 118|  
|sys.dm_fts_active_catalogs 資料行：<br /><br /> is_paused<br /><br /> previous_status<br /><br /> previous_status_description<br /><br /> row_count_in_thousands<br /><br /> status<br /><br /> status_description<br /><br /> worker_count|無。|dm_fts_active_catalogs.is_paused<br /><br /> dm_fts_active_catalogs.previous_status<br /><br /> dm_fts_active_catalogs.previous_status_description<br /><br /> dm_fts_active_catalogs.row_count_in_thousands<br /><br /> dm_fts_active_catalogs.status<br /><br /> dm_fts_active_catalogs.status_description<br /><br /> dm_fts_active_catalogs.worker_count|218<br /><br /> 221<br /><br /> 222<br /><br /> 224<br /><br /> 219<br /><br /> 220<br /><br /> 223|  
|sys.dm_fts_memory_buffers 資料行：<br /><br /> row_count|無。|dm_fts_memory_buffers.row_count|225|  
|sys.fulltext_catalogs 資料行：<br /><br /> 路徑<br /><br /> data_space_id<br /><br /> file_id 資料行|無。|fulltext_catalogs.path<br /><br /> fulltext_catalogs.data_space_id<br /><br /> fulltext_catalogs.file_id|215<br /><br /> 216<br /><br /> 217|  
  
## <a name="features-not-supported-in-a-future-version-of-sql-server"></a>SQL Server 的未來版本不支援的功能  
 下一版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可支援下列全文檢索搜尋功能，但會在更新的版本中移除。 確實的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本尚未決定。  
  
 **Feature name** 值會出現在追蹤事件中當做 ObjectName，並在效能計數器和 sys.dm_os_performance_counters 中當做執行個體名稱。 **Feature ID** 值會出現在追蹤事件中當做 ObjectId。  
  
|已被取代的功能|取代|功能名稱|功能識別碼|  
|------------------------|-----------------|------------------|----------------|  
|CONTAINS 和 CONTAINSTABLE 一般 NEAR 運算子：<br /><br /> {<simple_term> &#124; <prefix_term>}<br /><br /> {<br /><br /> { { NEAR &#124; ~ }    {<simple_term> &#124; <prefix_term>} } [...*n*]<br /><br /> }|自訂 NEAR 運算子：<br /><br /> NEAR(<br /><br /> {   {<simple_term> &#124; <prefix_term>} [ ,…*n* ]<br /><br /> &#124; ( {<simple_term> &#124; <prefix_term>} [,…*n*] )<br /><br /> [，\<距離 > [，\<順序 >]]<br /><br /> }<br /><br /> )<br /><br /> \<距離 >:: = {*整數* &#124; **MAX**}<br /><br /> \<順序 >:: = {TRUE &#124; **，則為 FALSE**}|FULLTEXT_OLD_NEAR_SYNTAX|247|  
|CREATE FULLTEXT CATALOG 選項：<br /><br /> IN PATH '*rootpath*'<br /><br /> ON FILEGROUP *filegroup*|無。|CREATE FULLTEXT CATLOG IN PATH<br /><br /> 無。*|237<br /><br /> 無。<sup>*</sup>|  
|DATABASEPROPERTYEX 屬性：IsFullTextEnabled|無。|DATABASEPROPERTYEX **('IsFullTextEnabled')**|202|  
|sp_detach_db 選項：<br /><br /> [ @keepfulltextindexfile = ] '*KeepFulltextIndexFile*'|無。|sp_detach_db @keepfulltextindexfile|226|  
|sp_fulltext_service 動作值：resource_usage 沒有函數。|無|sp_fulltext_service @action=resource_usage|200|  
  
 \***SQL Server:Deprecated Features** 物件不會監視 CREATE FULLTEXT CATLOG ON FILEGROUP *filegroup*的出現次數。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 的 Deprecated Features 物件](../performance-monitor/sql-server-deprecated-features-object.md)   
 [全文檢索搜尋的重大變更](../../database-engine/breaking-changes-to-full-text-search.md)   
 [SQL Server 2014 中已淘汰的資料庫引擎功能](../../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)  
  
  
