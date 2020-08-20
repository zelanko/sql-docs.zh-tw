---
description: 系統預存程序 (Transact-SQL)
title: " (Transact-sql) 的系統預存程式 |Microsoft Docs"
ms.custom: ''
ms.date: 02/21/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
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
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 05be8467516ff84c45268357eb6ab743d5599a05
ms.sourcegitcommit: 331b8495e4ab37266945c81ff5b93d250bdaa6da
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/20/2020
ms.locfileid: "88645065"
---
# <a name="system-stored-procedures-transact-sql"></a>系統預存程序 (Transact-SQL)

[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]

  在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中，許多管理和參考活動，都可以利用系統預存程序加以執行。 系統預存程序是以下表所示的類別目錄加以分組。  
  
## <a name="in-this-section"></a>本節內容  
  
|類別|描述|  
|--------------|-----------------|  
|[主動式異地複寫預存程式](https://msdn.microsoft.com/library/81658ee4-4422-4d73-bf7a-86a07422cb0d)|用來管理 Azure SQL Database 中的主動式異地複寫設定|  
|[目錄預存程序](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)|用來實作 ODBC 資料字典功能，以及隔離 ODBC 應用程式，不讓基礎系統資料表受到變更。|  
|[異動資料擷取預存程序](../../relational-databases/system-stored-procedures/change-data-capture-stored-procedures-transact-sql.md)|用來啟用、停用或報告異動資料擷取物件。|  
|[資料指標預存程序](../../relational-databases/system-stored-procedures/cursor-stored-procedures-transact-sql.md)|用來實作游標變數功能。|  
|[資料收集器預存程序](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)|可搭配資料收集器和下列元件一起使用：收集組、收集項和收集類型。|  
|[Database Engine 預存程序](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)|用於 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的一般維護。|  
|[&#40;Transact-sql&#41;的 Database Mail 預存程式 ](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)|在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體內，用來執行電子郵件作業。|  
|[資料庫維護計畫預存程序](../../relational-databases/system-stored-procedures/database-maintenance-plan-stored-procedures-transact-sql.md)|用來設定管理資料庫效能所需的核心維護工作。|  
|[分散式查詢預存程序](../../relational-databases/system-stored-procedures/distributed-queries-stored-procedures-transact-sql.md)|用來實作和管理分散式查詢。|  
|[&#40;Transact-sql&#41;的 Filestream 和 FileTable 預存程式 ](https://msdn.microsoft.com/library/54beca08-c012-4ebd-aa68-d8a10d221b64)|用來設定與管理 FILESTREAM 和 FileTable 功能。|  
|[&#40;Azure SQL Database 的防火牆規則預存程式&#41;](../../relational-databases/system-stored-procedures/firewall-rules-stored-procedures-azure-sql-database.md)|用來設定 Azure SQL Database 防火牆。|  
|[全文檢索搜尋預存程序](../../relational-databases/system-stored-procedures/full-text-search-and-semantic-search-stored-procedures-transact-sql.md)|用來實作和查詢全文檢索索引。|  
|[一般擴充預存程序](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)|用來針對各種維護活動，提供從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體到外部程式的介面。|  
|[記錄傳送預存程序](../../relational-databases/system-stored-procedures/log-shipping-stored-procedures-transact-sql.md)|用來設定、修改和監視記錄傳送組態。|  
|[管理資料倉儲預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/management-data-warehouse-stored-procedures-transact-sql.md)|用來設定管理資料倉儲。|  
|[OLE Automation 預存程式](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)|用來啟用標準 Automation 物件，以供標準 [!INCLUDE[tsql](../../includes/tsql-md.md)] 批次使用。|  
|[以原則為基礎的管理預存程序](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)|用於以原則為基礎的管理。|  
|[PolyBase 預存程序](https://msdn.microsoft.com/library/a522b303-bd1b-410b-92d1-29c950a15ede)|在 PolyBase 向外延展群組中新增或移除電腦。|  
|[查詢存放區預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)|用來微調效能。|  
|[複寫預存程式](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)|用來管理複寫。|  
|[安全性預存程序](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)|用來管理安全性。|  
|[快照集備份預存程式](https://msdn.microsoft.com/library/c278db87-5770-4037-a1e6-b9853a943339)|用來刪除 FILE_SNAPSHOT 備份及其所有快照集，或刪除個別的備份檔案快照集。|  
|[空間索引預存程序](https://msdn.microsoft.com/library/1be0f34e-3d5a-4a1f-9299-bd482362ec7a)|用來分析和改善空間索引的索引效能。|  
|[SQL Server Agent 預存程序](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)|由 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 用來監視效能及活動。|  
|[SQL Server Profiler 預存程序](../../relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql.md)|由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 用來管理已排程和事件驅動的活動。|  
|[Stretch Database 預存程式](../../relational-databases/system-stored-procedures/stretch-database-extended-stored-procedures-transact-sql.md)|用來管理 stretch database。|  
|[時態表預存程式](https://msdn.microsoft.com/library/f28ca74e-7876-4592-b794-e78e3690fff6)|用於時態表|  
|[XML 預存程序](../../relational-databases/system-stored-procedures/xml-stored-procedures-transact-sql.md)|用於 XML 文字管理。|  
  
> [!NOTE]  
>  除非特別說明，否則所有系統預存程序都會傳回 0 值，以表示成功。 若要表示失敗，則傳回非零值。  
  
## <a name="api-system-stored-procedures"></a>API 系統預存程序  
 對 ADO、OLE DB 和 ODBC 應用程式執行 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 的使用者，可能會注意到這些使用系統預存程序的應用程式沒有涵蓋在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 參考中。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 原生用戶端 OLE DB 提供者和 NATIVE client ODBC 驅動程式會使用這些預存程式 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 來執行資料庫 API 的功能。 這些預存程序只是提供者或驅動程式將使用者要求傳給 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體所用的機制。 它們只做為提供者或驅動程式內部使用。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不支援從應用程式明確呼叫它們。  
  
 Sp_createorphan 和 sp_droporphans 預存程式用於 ODBC **Ntext**、 **text**和 **image** 處理。  
  
 sp_reset_connection 預存程序是由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用來支援交易中的遠端預存程序呼叫。 當重複使用連接集區中的連接時，這個預存程序也會引發 Audit Login 和 Audit Logout 事件。  
  
 下列資料表中的系統預存程序，只能用在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或執行個體內，或是透過用戶端 API 使用，不供一般客戶使用。 它們隨時可以變更，而且不保證其相容性。  
  
 下列預存程序記載於《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》：  
  
:::row:::
    :::column:::
        sp_catalogs
    :::column-end:::
    :::column:::
        sp_column_privileges
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_column_privileges_ex
    :::column-end:::
    :::column:::
        sp_columns
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_columns_ex
    :::column-end:::
    :::column:::
        sp_databases
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_cursor
    :::column-end:::
    :::column:::
        sp_cursorclose
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_cursorexecute
    :::column-end:::
    :::column:::
        sp_cursorfetch
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_cursoroption
    :::column-end:::
    :::column:::
        sp_cursoropen
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_cursorprepare
    :::column-end:::
    :::column:::
        sp_cursorprepexec
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_cursorunprepare
    :::column-end:::
    :::column:::
        sp_execute
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_datatype_info
    :::column-end:::
    :::column:::
        sp_fkeys
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_foreignkeys
    :::column-end:::
    :::column:::
        sp_indexes
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_pkeys
    :::column-end:::
    :::column:::
        sp_primarykeys
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_prepare
    :::column-end:::
    :::column:::
        sp_prepexec
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_prepexecrpc
    :::column-end:::
    :::column:::
        sp_unprepare
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_server_info
    :::column-end:::
    :::column:::
        sp_special_columns
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_sproc_columns
    :::column-end:::
    :::column:::
        sp_statistics
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_table_privileges
    :::column-end:::
    :::column:::
        sp_table_privileges_ex
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_tables
    :::column-end:::
    :::column:::
        sp_tables_ex
    :::column-end:::
:::row-end:::

&nbsp;
  
沒有記載下列預存程序：  

:::row:::
    :::column:::
        sp_assemblies_rowset
    :::column-end:::
    :::column:::
        sp_assemblies_rowset_rmt
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_assemblies_rowset2
    :::column-end:::
    :::column:::
        sp_assembly_dependencies_rowset
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_assembly_dependencies_rowset_rmt
    :::column-end:::
    :::column:::
        sp_assembly_dependencies_rowset2
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_bcp_dbcmptlevel
    :::column-end:::
    :::column:::
        sp_catalogs_rowset
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_catalogs_rowset;2
    :::column-end:::
    :::column:::
        sp_catalogs_rowset;5
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_catalogs_rowset_rmt
    :::column-end:::
    :::column:::
        sp_catalogs_rowset2
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_check_constbytable_rowset
    :::column-end:::
    :::column:::
        sp_check_constbytable_rowset;2
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_check_constbytable_rowset2
    :::column-end:::
    :::column:::
        sp_check_constraints_rowset
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_check_constraints_rowset;2
    :::column-end:::
    :::column:::
        sp_check_constraints_rowset2
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_column_privileges_rowset
    :::column-end:::
    :::column:::
        sp_column_privileges_rowset;2
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_column_privileges_rowset;5
    :::column-end:::
    :::column:::
        sp_column_privileges_rowset_rmt
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_column_privileges_rowset2
    :::column-end:::
    :::column:::
        sp_columns_90
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_columns_90_rowset
    :::column-end:::
    :::column:::
        sp_columns_90_rowset_rmt
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_columns_90_rowset2
    :::column-end:::
    :::column:::
        sp_columns_ex_90
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_columns_rowset
    :::column-end:::
    :::column:::
        sp_columns_rowset;2
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_columns_rowset;5
    :::column-end:::
    :::column:::
        sp_columns_rowset_rmt
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_columns_rowset2
    :::column-end:::
    :::column:::
        sp_constr_col_usage_rowset
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_datatype_info_90
    :::column-end:::
    :::column:::
        sp_ddopen;1
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_ddopen;10
    :::column-end:::
    :::column:::
        sp_ddopen;11
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_ddopen;12
    :::column-end:::
    :::column:::
        sp_ddopen;13
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_ddopen;2
    :::column-end:::
    :::column:::
        sp_ddopen;3
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_ddopen;4
    :::column-end:::
    :::column:::
        sp_ddopen;5
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_ddopen;6
    :::column-end:::
    :::column:::
        sp_ddopen;7
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_ddopen;8
    :::column-end:::
    :::column:::
        sp_ddopen;9
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_foreign_keys_rowset
    :::column-end:::
    :::column:::
        sp_foreign_keys_rowset;2
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_foreign_keys_rowset;3
    :::column-end:::
    :::column:::
        sp_foreign_keys_rowset;5
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_foreign_keys_rowset_rmt
    :::column-end:::
    :::column:::
        sp_foreign_keys_rowset2
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_foreign_keys_rowset3
    :::column-end:::
    :::column:::
        sp_indexes_90_rowset
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_indexes_90_rowset_rmt
    :::column-end:::
    :::column:::
        sp_indexes_90_rowset2
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_indexes_rowset
    :::column-end:::
    :::column:::
        sp_indexes_rowset;2
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_indexes_rowset;5
    :::column-end:::
    :::column:::
        sp_indexes_rowset_rmt
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_indexes_rowset2
    :::column-end:::
    :::column:::
        sp_linkedservers_rowset
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_linkedservers_rowset;2
    :::column-end:::
    :::column:::
        sp_linkedservers_rowset2
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_oledb_database
    :::column-end:::
    :::column:::
        sp_oledb_defdb
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_oledb_deflang
    :::column-end:::
    :::column:::
        sp_oledb_language
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_oledb_ro_usrname
    :::column-end:::
    :::column:::
        sp_primary_keys_rowset
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_primary_keys_rowset;2
    :::column-end:::
    :::column:::
        sp_primary_keys_rowset;3
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_primary_keys_rowset;5
    :::column-end:::
    :::column:::
        sp_primary_keys_rowset_rmt
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_primary_keys_rowset2
    :::column-end:::
    :::column:::
        sp_procedure_params_90_rowset
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_procedure_params_90_rowset2
    :::column-end:::
    :::column:::
        sp_procedure_params_rowset
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_procedure_params_rowset;2
    :::column-end:::
    :::column:::
        sp_procedure_params_rowset2
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_procedures_rowset
    :::column-end:::
    :::column:::
        sp_procedures_rowset;2
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_procedures_rowset2
    :::column-end:::
    :::column:::
        sp_provider_types_90_rowset
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_provider_types_rowset
    :::column-end:::
    :::column:::
        sp_schemata_rowset
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_schemata_rowset;3
    :::column-end:::
    :::column:::
        sp_special_columns_90
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_sproc_columns_90
    :::column-end:::
    :::column:::
        sp_statistics_rowset
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_statistics_rowset;2
    :::column-end:::
    :::column:::
        sp_statistics_rowset2
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_stored_procedures
    :::column-end:::
    :::column:::
        sp_table_constraints_rowset
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_table_constraints_rowset;2
    :::column-end:::
    :::column:::
        sp_table_constraints_rowset2
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_table_privileges_rowset
    :::column-end:::
    :::column:::
        sp_table_privileges_rowset;2
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_table_privileges_rowset;5
    :::column-end:::
    :::column:::
        sp_table_privileges_rowset_rmt
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_table_privileges_rowset2
    :::column-end:::
    :::column:::
        sp_table_statistics_rowset
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_table_statistics_rowset;2
    :::column-end:::
    :::column:::
        sp_table_statistics2_rowset
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_tablecollations
    :::column-end:::
    :::column:::
        sp_tablecollations_90
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_tables_info_90_rowset
    :::column-end:::
    :::column:::
        sp_tables_info_90_rowset_64
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_tables_info_90_rowset2
    :::column-end:::
    :::column:::
        sp_tables_info_90_rowset2_64
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_tables_info_rowset
    :::column-end:::
    :::column:::
        sp_tables_info_rowset;2
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_tables_info_rowset_64
    :::column-end:::
    :::column:::
        sp_tables_info_rowset_64;2
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_tables_info_rowset2
    :::column-end:::
    :::column:::
        sp_tables_info_rowset2_64
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_tables_rowset;2
    :::column-end:::
    :::column:::
        sp_tables_rowset;5
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_tables_rowset_rmt
    :::column-end:::
    :::column:::
        sp_tables_rowset2
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_usertypes_rowset
    :::column-end:::
    :::column:::
        sp_usertypes_rowset_rmt
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_usertypes_rowset2
    :::column-end:::
    :::column:::
        sp_views_rowset
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_views_rowset2
    :::column-end:::
    :::column:::
        sp_xml_schema_rowset
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        sp_xml_schema_rowset2
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  

## <a name="see-also"></a>另請參閱  
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)   
 [預存程序 &#40;Database Engine&#41;](../../relational-databases/stored-procedures/stored-procedures-database-engine.md)   
 [&#40;OLE DB&#41;執行預存程式 ](../../relational-databases/native-client/ole-db/stored-procedures-running.md)   
 [正在執行預存程式](../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)   
 [&#40;Transact-sql&#41;的資料庫引擎預存程式 ](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [執行預存程序](../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)  
  
  
