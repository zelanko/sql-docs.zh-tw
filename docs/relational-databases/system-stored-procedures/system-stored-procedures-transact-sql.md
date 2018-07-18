---
title: 系統預存程序 (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 02/21/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server (starting with 2016 CTP3)
f1_keywords:
- sql13.TSQLSysNoExpandPortal.f1
- sql13.TSQLSysNoExpandPortal.f1_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- stored procedures [SQL Server]
- APIs [SQL Server]
- stored procedures [SQL Server], categories
- system stored procedures [SQL Server], categories
- system stored procedures [SQL Server]
ms.assetid: a5c4d5b8-5a24-4a2d-99b4-d003b546ee3a
caps.latest.revision: 49
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 481b0c451f5161231cf64402c5c758870a07be62
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "37979460"
---
# <a name="system-stored-procedures-transact-sql"></a>系統預存程序 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中，許多管理和參考活動，都可以利用系統預存程序加以執行。 系統預存程序是以下表所示的類別目錄加以分組。  
  
## <a name="in-this-section"></a>本節內容  
  
|類別目錄|描述|  
|--------------|-----------------|  
|[作用中異地複寫預存程序](http://msdn.microsoft.com/library/81658ee4-4422-4d73-bf7a-86a07422cb0d)|用來管理 Azure SQL Database 中的作用中異地複寫組態管理|  
|[目錄預存程序](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)|用來實作 ODBC 資料字典功能，以及隔離 ODBC 應用程式，不讓基礎系統資料表受到變更。|  
|[異動資料擷取預存程序](../../relational-databases/system-stored-procedures/change-data-capture-stored-procedures-transact-sql.md)|用來啟用、停用或報告異動資料擷取物件。|  
|[資料指標預存程序](../../relational-databases/system-stored-procedures/cursor-stored-procedures-transact-sql.md)|用來實作游標變數功能。|  
|[資料收集器預存程序](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)|可搭配資料收集器和下列元件一起使用：收集組、收集項和收集類型。|  
|[Database Engine 預存程序](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)|用於 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的一般維護。|  
|[Database Mail 預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)|在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體內，用來執行電子郵件作業。|  
|[資料庫維護計畫預存程序](../../relational-databases/system-stored-procedures/database-maintenance-plan-stored-procedures-transact-sql.md)|用來設定管理資料庫效能所需的核心維護工作。|  
|[分散式的查詢預存程序](../../relational-databases/system-stored-procedures/distributed-queries-stored-procedures-transact-sql.md)|用來實作和管理分散式查詢。|  
|[Filestream 和 FileTable 預存程序&#40;Transact SQL&#41;](http://msdn.microsoft.com/library/54beca08-c012-4ebd-aa68-d8a10d221b64)|用來設定與管理 FILESTREAM 和 FileTable 功能。|  
|[防火牆規則預存程序&#40;Azure SQL Database&#41;](../../relational-databases/system-stored-procedures/firewall-rules-stored-procedures-azure-sql-database.md)|用來設定 Azure SQL Database 防火牆。|  
|[全文檢索搜尋預存程序](../../relational-databases/system-stored-procedures/full-text-search-and-semantic-search-stored-procedures-transact-sql.md)|用來實作和查詢全文檢索索引。|  
|[一般擴充預存程序](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)|用來針對各種維護活動，提供從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體到外部程式的介面。|  
|[記錄傳送預存程序](../../relational-databases/system-stored-procedures/log-shipping-stored-procedures-transact-sql.md)|用來設定、修改和監視記錄傳送組態。|  
|[管理資料倉儲預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/management-data-warehouse-stored-procedures-transact-sql.md)|用來設定管理資料倉儲。|  
|[OLE Automation 預存程序](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)|用來啟用標準 Automation 物件，以供標準 [!INCLUDE[tsql](../../includes/tsql-md.md)] 批次使用。|  
|[以原則為基礎的管理預存程序](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)|用於以原則為基礎的管理。|  
|[PolyBase 預存程序](http://msdn.microsoft.com/library/a522b303-bd1b-410b-92d1-29c950a15ede)|新增或移除 PolyBase 向外延展群組中的電腦。|  
|[查詢存放區預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)|用來微調效能。|  
|[複寫預存程序](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)|用來管理複寫。|  
|[安全性預存程序](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)|用來管理安全性。|  
|[快照集備份的預存程序](http://msdn.microsoft.com/library/c278db87-5770-4037-a1e6-b9853a943339)|用來刪除 FILE_SNAPSHOT 備份，以及其所有快照集，或刪除的個別備份檔案快照集。|  
|[空間索引預存程序](http://msdn.microsoft.com/library/1be0f34e-3d5a-4a1f-9299-bd482362ec7a)|用來分析及改善的空間索引編製索引的效能。|  
|[SQL Server Agent 預存程序](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)|由 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 用來監視效能及活動。|  
|[SQL Server Profiler 預存程序](../../relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql.md)|由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 用來管理已排程和事件驅動的活動。|  
|[Stretch Database 預存程序](../../relational-databases/system-stored-procedures/stretch-database-extended-stored-procedures-transact-sql.md)|用來管理 stretch database。|  
|[時態表的預存程序](http://msdn.microsoft.com/library/f28ca74e-7876-4592-b794-e78e3690fff6)|使用時態表|  
|[XML 預存程序](../../relational-databases/system-stored-procedures/xml-stored-procedures-transact-sql.md)|用於 XML 文字管理。|  
  
> [!NOTE]  
>  除非特別說明，否則所有系統預存程序都會傳回 0 值，以表示成功。 若要表示失敗，則傳回非零值。  
  
## <a name="api-system-stored-procedures"></a>API 系統預存程序  
 對 ADO、OLE DB 和 ODBC 應用程式執行 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 的使用者，可能會注意到這些使用系統預存程序的應用程式沒有涵蓋在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 參考中。 這些預存程序由[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驅動程式，來實作資料庫 API 的功能。 這些預存程序只是提供者或驅動程式將使用者要求傳給 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體所用的機制。 它們只做為提供者或驅動程式內部使用。 呼叫它們明確地從[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-不支援架構的應用程式。  
  
 Sp_createorphan 和 sp_droporphans 預存程序用於 ODBC **ntext**，**文字**，並**映像**處理。  
  
 sp_reset_connection 預存程序是由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用來支援交易中的遠端預存程序呼叫。 當重複使用連接集區中的連接時，這個預存程序也會引發 Audit Login 和 Audit Logout 事件。  
  
 下列資料表中的系統預存程序，只能用在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或執行個體內，或是透過用戶端 API 使用，不供一般客戶使用。 它們隨時可以變更，而且不保證其相容性。  
  
 下列預存程序記載於《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》：  
  
|||  
|-|-|  
|sp_catalogs|sp_column_privileges|  
|sp_column_privileges_ex|sp_columns|  
|sp_columns_ex|sp_databases|  
|sp_cursor|sp_cursorclose|  
|sp_cursorexecute|sp_cursorfetch|  
|sp_cursoroption|sp_cursoropen|  
|sp_cursorprepare|sp_cursorprepexec|  
|sp_cursorunprepare|sp_execute|  
|sp_datatype_info|sp_fkeys|  
|sp_foreignkeys|sp_indexes|  
|sp_pkeys|sp_primarykeys|  
|sp_prepare|sp_prepexec|  
|sp_prepexecrpc|sp_unprepare|  
|sp_server_info|sp_special_columns|  
|sp_sproc_columns|sp_statistics|  
|sp_table_privileges|sp_table_privileges_ex|  
|sp_tables|sp_tables_ex|  
  
 沒有記載下列預存程序：  
  
|||  
|-|-|  
|sp_assemblies_rowset|sp_assemblies_rowset_rmt|  
|sp_assemblies_rowset2|sp_assembly_dependencies_rowset|  
|sp_assembly_dependencies_rowset_rmt|sp_assembly_dependencies_rowset2|  
|sp_bcp_dbcmptlevel|sp_catalogs_rowset|  
|sp_catalogs_rowset;2|sp_catalogs_rowset;5|  
|sp_catalogs_rowset_rmt|sp_catalogs_rowset2|  
|sp_check_constbytable_rowset|sp_check_constbytable_rowset;2|  
|sp_check_constbytable_rowset2|sp_check_constraints_rowset|  
|sp_check_constraints_rowset;2|sp_check_constraints_rowset2|  
|sp_column_privileges_rowset|sp_column_privileges_rowset;2|  
|sp_column_privileges_rowset;5|sp_column_privileges_rowset_rmt|  
|sp_column_privileges_rowset2|sp_columns_90|  
|sp_columns_90_rowset|sp_columns_90_rowset_rmt|  
|sp_columns_90_rowset2|sp_columns_ex_90|  
|sp_columns_rowset|sp_columns_rowset;2|  
|sp_columns_rowset;5|sp_columns_rowset_rmt|  
|sp_columns_rowset2|sp_constr_col_usage_rowset|  
|sp_datatype_info_90|sp_ddopen;1|  
|sp_ddopen;10|sp_ddopen;11|  
|sp_ddopen;12|sp_ddopen;13|  
|sp_ddopen;2|sp_ddopen;3|  
|sp_ddopen;4|sp_ddopen;5|  
|sp_ddopen;6|sp_ddopen;7|  
|sp_ddopen;8|sp_ddopen;9|  
|sp_foreign_keys_rowset|sp_foreign_keys_rowset;2|  
|sp_foreign_keys_rowset;3|sp_foreign_keys_rowset;5|  
|sp_foreign_keys_rowset_rmt|sp_foreign_keys_rowset2|  
|sp_foreign_keys_rowset3|sp_indexes_90_rowset|  
|sp_indexes_90_rowset_rmt|sp_indexes_90_rowset2|  
|sp_indexes_rowset|sp_indexes_rowset;2|  
|sp_indexes_rowset;5|sp_indexes_rowset_rmt|  
|sp_indexes_rowset2|sp_linkedservers_rowset|  
|sp_linkedservers_rowset;2|sp_linkedservers_rowset2|  
|sp_oledb_database|sp_oledb_defdb|  
|sp_oledb_deflang|sp_oledb_language|  
|sp_oledb_ro_usrname|sp_primary_keys_rowset|  
|sp_primary_keys_rowset;2|sp_primary_keys_rowset;3|  
|sp_primary_keys_rowset;5|sp_primary_keys_rowset_rmt|  
|sp_primary_keys_rowset2|sp_procedure_params_90_rowset|  
|sp_procedure_params_90_rowset2|sp_procedure_params_rowset|  
|sp_procedure_params_rowset;2|sp_procedure_params_rowset2|  
|sp_procedures_rowset|sp_procedures_rowset;2|  
|sp_procedures_rowset2|sp_provider_types_90_rowset|  
|sp_provider_types_rowset|sp_schemata_rowset|  
|sp_schemata_rowset;3|sp_special_columns_90|  
|sp_sproc_columns_90|sp_statistics_rowset|  
|sp_statistics_rowset;2|sp_statistics_rowset2|  
|sp_stored_procedures|sp_table_constraints_rowset|  
|sp_table_constraints_rowset;2|sp_table_constraints_rowset2|  
|sp_table_privileges_rowset|sp_table_privileges_rowset;2|  
|sp_table_privileges_rowset;5|sp_table_privileges_rowset_rmt|  
|sp_table_privileges_rowset2|sp_table_statistics_rowset|  
|sp_table_statistics_rowset;2|sp_table_statistics2_rowset|  
|sp_tablecollations|sp_tablecollations_90|  
|sp_tables_info_90_rowset|sp_tables_info_90_rowset_64|  
|sp_tables_info_90_rowset2|sp_tables_info_90_rowset2_64|  
|sp_tables_info_rowset|sp_tables_info_rowset;2|  
|sp_tables_info_rowset_64|sp_tables_info_rowset_64;2|  
|sp_tables_info_rowset2|sp_tables_info_rowset2_64|  
|sp_tables_rowset;2|sp_tables_rowset;5|  
|sp_tables_rowset_rmt|sp_tables_rowset2|  
|sp_usertypes_rowset|sp_usertypes_rowset_rmt|  
|sp_usertypes_rowset2|sp_views_rowset|  
|sp_views_rowset2|sp_xml_schema_rowset|  
|sp_xml_schema_rowset2||  
  
## <a name="see-also"></a>另請參閱  
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)   
 [預存程序 &#40;Database Engine&#41;](../../relational-databases/stored-procedures/stored-procedures-database-engine.md)   
 [執行預存程序&#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/stored-procedures-running.md)   
 [執行預存程序](../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)   
 [Database Engine 預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [執行預存程序](../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)  
  
  
