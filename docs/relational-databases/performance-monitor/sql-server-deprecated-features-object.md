---
title: SQL Server 的 Deprecated Features 物件 | Microsoft Docs
description: 了解 SQLServer:Deprecated Features 物件，其所提供計數器可監視指定為已淘汰的功能。
ms.custom: ''
ms.date: 05/03/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Deprecated Features
- performance counters [SQL Server], deprecated features
- deprecation [SQL Server], performance counters
- Deprecated Features object
ms.assetid: e95de9d6-c950-41cd-8aaa-be529c6de198
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: a833e7029697693a6620ce5196a10b6ef95acc8f
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/09/2020
ms.locfileid: "91890918"
---
# <a name="sql-server-deprecated-features-object"></a>SQL Server、Deprecated Features 物件
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的 SQLServer:Deprecated Features 物件提供了計數器來監視指定為已被取代的功能。 在每一個案例中，此計數器都會提供一個使用計數，列出上一次啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之後所遇到之已被取代功能的次數。  
  
 您也可以透過執行下列陳述式來使用這些計數器的值：  
  
```  
SELECT * FROM sys.dm_os_performance_counters   
WHERE object_name = 'SQLServer:Deprecated Features';  
```  

下表描述 SQL Server **已被取代的功能** 效能物件。

|**SQL Server 已被取代的功能計數器**|描述|  
|-------------|-----------------|  
|**使用量**|自上次啟動 SQL Server 後的功能使用方式。|
  
 下表描述 SQL Server Deprecated Features 計數器執行個體。  
  
|SQL Server 已被取代的功能計數器執行個體|描述|  
|------------------------------------------------------|-----------------|  
|做為暫存資料表和預存程序名稱的 '#' 和 '##'。|遇到一個不包含 # 以外之任何字元的識別碼。 請至少使用一個其他字元。 每次編譯時發生一次。|  
|'::' 函數呼叫語法|資料表值函式遇到 :: 函式呼叫語法。 取代為 `SELECT column_list FROM` <函式名稱>`()`。 例如，以 `SELECT * FROM ::fn_virtualfilestats(2,1)`取代 `SELECT * FROM sys.fn_virtualfilestats(2,1)`。 每次編譯時發生一次。|  
|'\@' 和以 '\@\@' 開頭的名稱作為 [!INCLUDE[tsql](../../includes/tsql-md.md)] 識別碼|出現了以 \@ 或 \@\@ 開頭的識別碼。 請勿使用 \@、\@v @ 或是以 \@\@ 開頭的名稱作為識別碼。 每次編譯時發生一次。|  
|ADDING TAPE DEVICE|遇到已被取代的功能 sp_addumpdevice'**tape**'。 請改用 sp_addumpdevice'**disk**'。 每次使用時發生一次。|  
|ALL 權限|遇到 GRANT ALL、DENY ALL 或 REVOKE ALL 語法的總次數。 請修改語法來拒絕特定權限。 每次查詢時發生一次。|  
|ALTER DATABASE WITH TORN_PAGE_DETECTION|上一次啟動伺服器執行個體之後，已經使用 ALTER DATABASE 的已被取代功能 TORN_PAGE_DETECTION 選項的總次數。 請改用 PAGE_VERIFY 語法。 每次在 DDL 陳述式中使用時發生一次。|  
|ALTER LOGIN WITH SET CREDENTIAL|遇到已被取代的功能語法 ALTER LOGIN WITH SET CREDENTIAL 或 ALTER LOGIN WITH NO CREDENTIAL。 請改用 ADD 或 DROP CREDENTIAL 語法。 每次編譯時發生一次。|  
|Azeri_Cyrilllic_90|每次啟動資料庫及使用定序時，事件會發生一次。 請規劃修改使用此定序的應用程式。|  
|Azeri_Latin_90|每次啟動資料庫及使用定序時，事件會發生一次。 請規劃修改使用此定序的應用程式。|  
|BACKUP DATABASE 或 LOG TO TAPE|遇到已被取代的功能 BACKUP { DATABASE &#124; LOG } TO TAPE 或 BACKUP { DATABASE &#124; LOG } TO <磁帶裝置>。<br /><br /> 請改用 BACKUP { DATABASE &#124; LOG } TO DISK 或 BACKUP { DATABASE &#124; LOG } TO <磁帶裝置>。 每次使用時發生一次。|  
|BACKUP DATABASE 或 LOG WITH MEDIAPASSWORD|遇到了已被取代的功能 BACKUP DATABASE WITH MEDIAPASSWORD 或 BACKUP LOG WITH MEDIAPASSWORD。 請勿使用 WITH MEDIAPASSWORD。|  
|BACKUP DATABASE 或 LOG WITH PASSWORD|遇到了已被取代的功能 BACKUP DATABASE WITH PASSWORD 或 BACKUP LOG WITH PASSWORD。 請勿使用 WITH PASSWORD。|  
|COMPUTE [BY]|遇到了 COMPUTE 或 COMPUTE BY 語法。 請重寫查詢，以搭配 ROLLUP 使用 GROUP BY。 每次編譯時發生一次。|  
|CREATE FULLTEXT CATLOG IN PATH|遇到了具有 IN PATH 子句的 CREATE FULLTEXT CATLOG 陳述式。 這個子句在這一版的 SQL Server 中沒有任何作用。 每次使用時發生一次。|  
|CREATE TRIGGER WITH APPEND|遇到了具有 WITH APPEND 子句的 CREATE TRIGGER 陳述式。 請改為重新建立整個觸發程序。 每次在 DDL 陳述式中使用時發生一次。|  
|CREATE_DROP_DEFAULT|遇到了 CREATE DEFAULT 或 DROP DEFAULT 語法。 請使用 CREATE TABLE 或 ALTER TABLE 的 DEFAULT 選項來重寫命令。 每次編譯時發生一次。|  
|CREATE_DROP_RULE|遇到了 CREATE RULE 語法。 請使用條件約束重寫命令。 每次編譯時發生一次。|  
|資料類型：text、ntext 或 image|遇到 **text**、 **ntext**或 **image** 資料類型。 請重寫應用程式來使用 **varchar(max)** 資料類型及移除 **text**、 **ntext**和 **image** 資料類型語法。 每次查詢時發生一次。|  
||資料庫已變更為相容性層級 80 的總次數。 請在下次發行之前，規劃升級資料庫和應用程式。 啟動相容性層級為 80 的資料庫時也會發生。|  
|資料庫相容性層級 100、110。 120|資料庫相容性層級變更的總次數。 請針對將來的版本規劃升級資料庫和應用程式。 啟動已被取代的相容性層級的資料庫時也會發生。|  
|DATABASE_MIRRORING|遇到針對資料庫鏡像功能的參考。 計劃升級至 Always On 可用性群組，如果您執行不支援 Always On 可用性群組的 SQL Server 版本，則計劃移轉至記錄傳送。|  
|database_principal_aliases|遇到了已被取代之 sys.database_principal_aliases 的參考。 請使用角色，而非別名。 每次編譯時發生一次。|  
|DATABASEPROPERTY|陳述式已參考 DATABASEPROPERTY。 將陳述式 DATABASEPROPERTY 更新為 DATABASEPROPERTYEX。 每次編譯時發生一次。|  
|DATABASEPROPERTYEX('IsFullTextEnabled')|陳述式已參考 DATABASEPROPERTYEX IsFullTextEnabled 屬性。 此屬性的值沒有任何作用。 使用者資料庫一定會啟用全文檢索搜尋。 請勿使用這個屬性。 每次編譯時發生一次。|  
|DBCC [UN]PINTABLE|遇到 DBCC PINTABLE 或 DBCC UNPINTABLE 陳述式。 這個陳述式沒有任何作用，而且應該移除。 每次查詢時發生一次。|  
|DBCC DBREINDEX|遇到 DBCC DBREINDEX 陳述式。 請重寫此陳述式來使用 ALTER INDEX 的 REBUILD 選項。 每次查詢時發生一次。|  
|DBCC INDEXDEFRAG|遇到 DBCC INDEXDEFRAG 陳述式。 請重寫此陳述式來使用 ALTER INDEX 的 REORGANIZE 選項。 每次查詢時發生一次。|  
|DBCC SHOWCONTIG|遇到 DBCC SHOWCONTIG 陳述式。 請查詢 sys.dm_db_index_physical_stats，取得這項資訊。 每次查詢時發生一次。|  
|當做預設值的 DEFAULT 關鍵字|遇到了使用 DEFAULT 關鍵字當做預設值的語法。 請勿使用。 每次編譯時發生一次。|  
|已被取代的加密演算法|下一版的 SQL Server 將會移除已被取代的加密演算法 RC4。 請避免在新的開發工作中使用此項功能，並規劃修改目前使用此項功能的應用程式。 RC4 演算法功能並不強，只是為了與舊版相容才予以支援。 只有在資料庫相容性層級為 90 或 100 時，才能使用 RC4 或 RC4_128 加密新資料 (不建議使用)。請改用較新的演算法，例如其中一個 AES 演算法。 在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 及更新版本中，使用 RC4 或 RC4_128 加密的資料可以在任何相容性層級進行解密。|  
|已被取代的雜湊演算法|使用 MD2、MD4、MD5、SHA 或 SHA1 演算法。|  
|DESX 演算法|遇到了使用 DESX 加密演算法的語法。 請使用另一種演算法進行加密。 每次編譯時發生一次。|  
|dm_fts_active_catalogs|dm_fts_active_catalogs 計數器一定會保持為 0，因為 sys.dm_fts_active_catalogs 檢視表的某些資料行未被取代。 若要監視已被取代的資料行，請使用資料行特定的計數器，例如 dm_fts_active_catalogs.is_paused。|  
|dm_fts_active_catalogs.is_paused|遇到了 [sys.dm_fts_active_catalogs](../../relational-databases/system-dynamic-management-views/sys-dm-fts-active-catalogs-transact-sql.md) 動態管理檢視的 is_paused 資料行。 請避免使用這個資料行。 每當伺服器執行個體偵測到此資料行的參考時，都會發生。|  
|dm_fts_active_catalogs.previous_status|遇到了 sys.dm_fts_active_catalogs 動態管理檢視的 previous_status 資料行。 請避免使用這個資料行。 每當伺服器執行個體偵測到此資料行的參考時，都會發生。|  
|dm_fts_active_catalogs.previous_status_description|遇到了 sys.dm_fts_active_catalogs 動態管理檢視的 previous_status_description 資料行。 請避免使用這個資料行。 每當伺服器執行個體偵測到此資料行的參考時，都會發生。|  
|dm_fts_active_catalogs.row_count_in_thousands|遇到了 sys.dm_fts_active_catalogs 動態管理檢視的 row_count_in_thousands 資料行。 請避免使用這個資料行。 每當伺服器執行個體偵測到此資料行的參考時，都會發生。|  
|dm_fts_active_catalogs.status|遇到了 sys.dm_fts_active_catalogs 動態管理檢視的 status 資料行。 請避免使用這個資料行。 每當伺服器執行個體偵測到此資料行的參考時，都會發生。|  
|dm_fts_active_catalogs.status_description|遇到了 sys.dm_fts_active_catalogs 動態管理檢視的 status_description 資料行。 請避免使用這個資料行。 每當伺服器執行個體偵測到此資料行的參考時，都會發生。|  
|dm_fts_active_catalogs.worker_count|遇到了 sys.dm_fts_active_catalogs 動態管理檢視的 worker_count 資料行。 請避免使用這個資料行。 每當伺服器執行個體偵測到此資料行的參考時，都會發生。|  
|dm_fts_memory_buffers|dm_fts_memory_buffers 計數器一定會保持為 0，因為 sys.dm_fts_memory_buffers 檢視表的大部分資料行都未被取代。 若要監視已被取代的資料行，請使用資料行特定的計數器：dm_fts_memory_buffers.row_count。|  
|dm_fts_memory_buffers.row_count|遇到了 [sys.dm_fts_memory_buffers](../../relational-databases/system-dynamic-management-views/sys-dm-fts-memory-buffers-transact-sql.md) 動態管理檢視的 row_count 資料行。 請避免使用這個資料行。 每當伺服器執行個體偵測到此資料行的參考時，都會發生。|  
|具有兩部分名稱的 DROP INDEX|DROP INDEX 語法在 DROP INDEX 中包含了 <資料表名稱>.<索引名稱> 語法格式。 在 DROP INDEX 陳述式中取代為 <索引名稱> ON <資料表名稱> 的語法。 每次編譯時發生一次。|  
|EXT_CREATE_ALTER_SOAP_ENDPOINT|遇到了 FOR SOAP 選項的 CREATE 或 ALTER ENDPOINT 陳述式。 原生 XML Web Service 已被取代。 請改用 Windows Communications Foundation (WCF) 或 ASP.NET。|  
|EXT_endpoint_webmethods|遇到 sys.endpoint_webmethods。 原生 XML Web Service 已被取代。 請改用 Windows Communications Foundation (WCF) 或 ASP.NET。|  
|EXT_soap_endpoints|遇到 sys.soap_endpoints。 原生 XML Web Service 已被取代。 請改用 Windows Communications Foundation (WCF) 或 ASP.NET。|  
|EXTPROP_LEVEL0TYPE|在 level0type 遇到 TYPE。 請使用 SCHEMA 當做 level0type，並使用 TYPE 當做 level1type。 每次查詢時發生一次。|  
|EXTPROP_LEVEL0USER|也指定 level1type 時的 level0type USER。 只有在擴充屬性中才能直接在使用者上使用 USER 當做 level0type。 每次查詢時發生一次。|  
|FASTFIRSTROW|遇到了 FASTFIRSTROW 語法。 請重寫陳述式來使用 OPTION (FAST *n*) 語法。 每次編譯時發生一次。|  
|FILE_ID|遇到了 FILE_ID 語法。 請重寫陳述式來使用 FILE_IDEX。 每次編譯時發生一次。|  
|fn_get_sql|已編譯 fn_get_sql 函數。 請改用 sys.dm_exec_sql_text。 每次編譯時發生一次。|  
|fn_servershareddrives|已編譯 fn_servershareddrives 函數。 請改用 sys.dm_io_cluster_shared_drives。 每次編譯時發生一次。|  
|fn_virtualservernodes|已編譯 fn_virtualservernodes 函數。 請改用 sys.dm_os_cluster_nodes。 每次編譯時發生一次。|  
|fulltext_catalogs|fulltext_catalogs 計數器一定會保持為 0，因為 sys.fulltext_catalogs 檢視表的某些資料行未被取代。 若要監視已被取代的資料行，請使用資料行特定的計數器，例如 fulltext_catalogs.data_space_id。 每當伺服器執行個體偵測到此資料行的參考時，都會發生。|  
|fulltext_catalogs.data_space_id|遇到了 [sys.fulltext_catalogs](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md) 目錄檢視的 data_space_id 資料行。 請勿使用這個資料行。 每當伺服器執行個體偵測到此資料行的參考時，都會發生。|  
|fulltext_catalogs.file_id|遇到了 sys.fulltext_catalogs 目錄檢視的 file_id 資料行。 請勿使用這個資料行。 每當伺服器執行個體偵測到此資料行的參考時，都會發生。|  
|fulltext_catalogs.path|遇到了 sys.fulltext_catalogs 目錄檢視的 path 資料行。 請勿使用這個資料行。 每當伺服器執行個體偵測到此資料行的參考時，都會發生。|  
|FULLTEXTCATALOGPROPERTY('LogSize')|遇到了 FULLTEXTCATALOGPROPERTY 函數的 LogSize 屬性。 請避免使用這個屬性。|  
|FULLTEXTCATALOGPROPERTY('PopulateStatus')|遇到了 FULLTEXTCATALOGPROPERTY 函數的 PopulateStatus 屬性。 請避免使用這個屬性。|  
|FULLTEXTSERVICEPROPERTY('ConnectTimeout')|遇到了 FULLTEXTSERVICEPROPERTY 函數的 ConnectTimeout 屬性。 請避免使用這個屬性。|  
|FULLTEXTSERVICEPROPERTY('DataTimeout')|遇到了 FULLTEXTSERVICEPROPERTY 函數的 DataTimeout 屬性。 請避免使用這個屬性。|  
|FULLTEXTSERVICEPROPERTY('ResourceUsage')|遇到了 FULLTEXTSERVICEPROPERTY 函數的 ResourceUsage 屬性。 請避免使用這個屬性。|  
|GROUP BY ALL|遇到 GROUP BY ALL 語法的總次數。 請修改語法來根據特定資料表分組。|  
|Hindi|每次啟動資料庫及使用定序時，事件會發生一次。 請規劃修改使用此定序的應用程式。 請改用 Indic_General_90。|  
|沒有括號的 HOLDLOCK 資料表提示。||  
|IDENTITYCOL|遇到 INDENTITYCOL 語法。 請重寫陳述式來使用 $identity 語法。 每次編譯時發生一次。|  
|沒有 COUNT_BIG(*) 的索引檢視表 SELECT 清單|彙總索引檢視表的 SELECT 清單必須包含 COUNT_BIG (\*)。|  
|INDEX_OPTION|遇到 CREATE TABLE、ALTER TABLE 或 CREATE INDEX 語法，但是選項周圍沒有括號。 請重寫陳述式來使用目前的語法。 每次查詢時發生一次。|  
|INDEXKEY_PROPERTY|遇到 INDEXKEY_PROPERTY 語法。 請重寫陳述式來查詢 sys.index_columns。 每次編譯時發生一次。|  
|間接 TVF 提示|透過檢視表將資料表提示間接套用到多重陳述式資料表值函式 (TVF) 的引動過程，將從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的未來版本中移除。|  
|INSERT NULL 到 TIMESTAMP 資料行中|已將 NULL 值插入 TIMESTAMP 資料行。 請改用預設值。 每次編譯時發生一次。|  
|INSERT_HINTS||  
|Korean_Wansung_Unicode|每次啟動資料庫及使用定序時，事件會發生一次。 請規劃修改使用此定序的應用程式。|  
|Lithuanian_Classic|每次啟動資料庫及使用定序時，事件會發生一次。 請規劃修改使用此定序的應用程式。|  
|馬其頓文|每次啟動資料庫及使用定序時，事件會發生一次。 請規劃修改使用此定序的應用程式。 請改用 Macedonian_FYROM_90。|  
|MODIFY FILEGROUP READONLY|遇到了 MODIFY FILEGROUP READONLY 語法。 請重寫陳述式來使用 READ_ONLY 語法。 每次編譯時發生一次。|  
|MODIFY FILEGROUP READWRITE|遇到了 MODIFY FILEGROUP READWRITE 語法。 請重寫陳述式來使用 READ_WRITE 語法。 每次編譯時發生一次。|  
|兩部分以上的資料行名稱|查詢在資料行清單中使用了 3 部分或 4 部分的名稱。 請將查詢變更為使用標準的 2 部分相容名稱。 每次編譯時發生一次。|  
|沒有逗號的多個資料表提示|使用空格當做資料表提示之間的分隔符號。 請改用逗號。 每次編譯時發生一次。|  
|UPDATE 或 DELETE 中的 NOLOCK 或 READUNCOMMITTED|在 UPDATE 或 DELETE 陳述式的 FROM 子句中遇到了 NOLOCK 或 READUNCOMMITTED。 請從 FROM 子句中移除 NOLOCK 或 READUNCOMMITTED 資料表提示。|  
|非 ANSI *= 或 =\* 外部聯結運算子|遇到了使用 *= 或 =\* 聯結語法的陳述式。 請重寫陳述式來使用 ANSI 聯結語法。 每次編譯時發生一次。|  
|numbered_stored_procedures||  
|numbered_procedure_parameters|遇到了已被取代之 sys.numbered_procedure_parameters 的參考。 請勿使用。 每次編譯時發生一次。|  
|numbered_procedures|遇到了已被取代之 deprecated sys.numbered_procedures 的參考。 請勿使用。 每次編譯時發生一次。|  
|Oldstyle RAISEERROR|遇到了已淘汰的 RAISERROR (格式：RAISERROR 整數字串) 語法。 請使用目前的 RAISERROR 語法重寫陳述式。 每次編譯時發生一次。|  
|隨選連接的 OLEDB。|SQLOLEDB 不是支援的提供者。 請針對隨選連接使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client。|  
|PERMISSIONS|遇到了 PERMISSIONS 內建函數的參考。 請改為查詢 sys.fn_my_permissions。 每次查詢時發生一次。|  
|ProcNums|遇到了已被取代的 ProcNums 語法。 請重寫陳述式來移除參考。 每次編譯時發生一次。|  
|READTEXT|遇到 READTEXT 語法。 請重寫應用程式來使用 **varchar(max)** 資料類型及移除 **text** 資料類型語法。 每次查詢時發生一次。|  
|RESTORE DATABASE 或 LOG WITH DBO_ONLY|RESTORE ...WITH DBO_ONLY 語法。 請改用 RESTORE ...RESTRICTED_USER。|  
|RESTORE DATABASE 或 LOG WITH MEDIAPASSWORD|RESTORE ...WITH MEDIAPASSWORD 語法。 WITH MEDIAPASSWORD 提供的安全性很弱，應該移除。|  
|RESTORE DATABASE 或 LOG WITH PASSWORD|RESTORE ...WITH PASSWORD 語法。 WITH PASSWORD 提供的安全性很弱，應該移除。|  
|從觸發程序傳回結果|每次叫用觸發程序時，都會發生這個事件。 請重寫觸發程序，好讓它不會傳回結果集。|  
|ROWGUIDCOL|遇到 ROWGUIDCOL 語法。 請重寫陳述式來使用 $rowguid 語法。 每次編譯時發生一次。|  
|SET ANSI_NULLS OFF|遇到 SET ANSI_NULLS OFF 語法。 請移除這個已被取代的語法。 每次編譯時發生一次。|  
|SET ANSI_PADDING OFF|遇到 SET ANSI_PADDING OFF 語法。 請移除這個已被取代的語法。 每次編譯時發生一次。|  
|SET CONCAT_NULL_YIELDS_NULL OFF|遇到 SET CONCAT_NULL_YIELDS_NULL OFF 語法。 請移除這個已被取代的語法。 每次編譯時發生一次。|  
|SET DISABLE_DEF_CNST_CHK|遇到 SET DISABLE_DEF_CNST_CHK 語法。 它沒有任何作用。 請移除這個已被取代的語法。 每次編譯時發生一次。|  
|SET FMTONLY ON|遇到 SET FMTONLY 語法。 請移除這個已被取代的語法。 每次編譯時發生一次。|  
|SET OFFSETS|遇到 SET OFFSETS 語法。 請移除這個已被取代的語法。 每次編譯時發生一次。|  
|SET REMOTE_PROC_TRANSACTIONS|遇到 SET REMOTE_PROC_TRANSACTIONS 語法。 請移除這個已被取代的語法。 請改用連結的伺服器和 sp_serveroption。|  
|SET ROWCOUNT|DELETE、INSERT 或 UPDATE 陳述式中遇到 SET ROWCOUNT 語法。 請使用 TOP 來重寫陳述式。 每次編譯時發生一次。|  
|SETUSER|遇到 SET USER 陳述式。 請改用 EXECUTE AS。 每次查詢時發生一次。|  
|sp_addapprole|遇到 sp_addapprole 程序。 請改用 CREATE APPLICATION ROLE。 每次查詢時發生一次。|  
|sp_addextendedproc|遇到 sp_addextendedproc 程序。 請改用 CLR。 每次編譯時發生一次。|  
|sp_addlogin|遇到 sp_addlogin 程序。 請改用 CREATE LOGIN。 每次查詢時發生一次。|  
|sp_addremotelogin|遇到 sp_addremotelogin 程序。 請改用連結的伺服器。|  
|sp_addrole|遇到 sp_addrole 程序。 請改用 CREATE ROLE。 每次查詢時發生一次。|  
|sp_addserver|遇到 sp_addserver 程序。 請改用連結的伺服器。|  
|sp_addtype|遇到 sp_addtype 程序。 請改用 CREATE TYPE。 每次編譯時發生一次。|  
|sp_adduser|遇到 sp_adduser 程序。 請改用 CREATE USER。 每次查詢時發生一次。|  
|sp_approlepassword|遇到 sp_approlepassword 程序。 請改用 ALTER APPLICATION ROLE。 每次查詢時發生一次。|  
|sp_attach_db|遇到 sp_attach_db 程序。 請改用 CREATE DATABASE FOR ATTACH。 每次查詢時發生一次。|  
|sp_attach_single_file_db|遇到 sp_single_file_db 程序。 請改用 CREATE DATABASE FOR ATTACH_REBUILD_LOG。 每次查詢時發生一次。|  
|sp_bindefault|遇到 sp_bindefault 程序。 請改用 ALTER TABLE 或 CREATE TABLE 的 DEFAULT 關鍵字。 每次編譯時發生一次。|  
|sp_bindrule|遇到 sp_bindrule 程序。 請改用檢查條件約束。 每次編譯時發生一次。|  
|sp_bindsession|遇到 sp_bindsession 程序。 請改用 Multiple Active Result Set (MARS) 或分散式交易。 每次編譯時發生一次。|  
|sp_certify_removable|遇到 sp_certify_removable 程序。 請改用 sp_detach_db。 每次查詢時發生一次。|  
|sp_changeobjectowner|遇到 sp_changeobjectowner 程序。 請改用 ALTER SCHEMA 或 ALTER AUTHORIZATION。 每次查詢時發生一次。|  
|sp_change_users_login|遇到 sp_change_users_login 程序。 請改用 ALTER USER。 每次查詢時發生一次。|  
|sp_configure 'allow updates'|遇到 sp_configure 的 allow updates 選項。 系統資料表不再可更新， 請勿使用。 每次查詢時發生一次。|  
|sp_configure 'disallow results from triggers'|遇到 sp_configure 的 disallow result sets from triggers 選項。 若不要允許來自觸發程序的結果集，請使用 sp_configure 將此選項設定為 1。 每次查詢時發生一次。|  
|sp_configure 'ft crawl bandwidth (max)'|遇到 sp_configure 的 ft crawl bandwidth (max) 選項。 請勿使用。 每次查詢時發生一次。|  
|sp_configure 'ft crawl bandwidth (min)'|遇到 sp_configure 的 ft crawl bandwidth (min) 選項。 請勿使用。 每次查詢時發生一次。|  
|sp_configure 'ft notify bandwidth (max)'|遇到 sp_configure 的 ft notify bandwidth (max) 選項。 請勿使用。 每次查詢時發生一次。|  
|sp_configure 'ft notify bandwidth (min)'|遇到 sp_configure 的 ft notify bandwidth (min) 選項。 請勿使用。 每次查詢時發生一次。|  
|sp_configure 'locks'|遇到 sp_configure 的 locks 選項。 Locks 不再可以設定， 請勿使用。 每次查詢時發生一次。|  
|sp_configure 'open objects'|遇到 sp_configure 的 open objects 選項。 open objects 的數目不再可以設定， 請勿使用。 每次查詢時發生一次。|  
|sp_configure 'priority boost'|遇到 sp_configure 的 priority boost 選項。 請勿使用。 每次查詢時發生一次。 請改用 Windows start /high ... program.exe 選項。|  
|sp_configure 'remote proc trans'|遇到 sp_configure 的 remote proc trans 選項。 請勿使用。 每次查詢時發生一次。|  
|sp_configure 'set working set size'|遇到 sp_configure 的 set working set size 選項。 working set size 不再可以設定， 請勿使用。 每次查詢時發生一次。|  
|sp_control_dbmasterkey_password|sp_control_dbmasterkey_password 預存程序不會檢查主要金鑰是否存在。 這可允許回溯相容性，但是會顯示警告。 這個行為已被取代。 在未來版本中，主要金鑰必須存在，而且預存程序 sp_control_dbmasterkey_password 中使用的密碼必須與用來加密資料庫主要金鑰的其中一個密碼相同。|  
|sp_create_removable|遇到 sp_create_removable 程序。 請改用 CREATE DATABASE。 每次查詢時發生一次。|  
|sp_db_vardecimal_storage_format|遇到了 **vardecimal** 儲存格式的使用。 請改用資料壓縮。|  
|sp_dbcmptlevel|遇到 sp_dbcmptlevel 程序。 使用 ALTER DATABASE ...SET COMPATIBILITY_LEVEL。 每次查詢時發生一次。|  
|sp_dbfixedrolepermission|遇到 sp_dbfixedrolepermission 程序。 請勿使用。 每次查詢時發生一次。|  
|sp_dboption|遇到 sp_dboption 程序。 請改用 ALTER DATABASE 和 DATABASEPROPERTYEX。 每次編譯時發生一次。|  
|sp_dbremove|遇到 sp_dbremove 程序。 請改用 DROP DATABASE。 每次查詢時發生一次。|  
|sp_defaultdb|遇到 sp_defaultdb 程序。 請改用 ALTER LOGIN。 每次編譯時發生一次。|  
|sp_defaultlanguage|遇到 sp_defaultlanguage 程序。 請改用 ALTER LOGIN。 每次編譯時發生一次。|  
|sp_denylogin|遇到 sp_denylogin 程序。 請改用 ALTER LOGIN DISABLE。 每次查詢時發生一次。|  
|sp_depends|遇到 sp_depends 程序。 請改用 sys.dm_sql_referencing_entities 和 sys.dm_sql_referenced_entities。 每次查詢時發生一次。|  
|sp_detach_db \@keepfulltextindexfile|在 sp_detach_db 陳述式中出現 \@keepfulltextindexfile 引數。 請勿使用這個引數。|  
|sp_dropalias|遇到 sp_dropalias 程序。 以使用者帳戶和資料庫角色的組合來取代別名。 請使用 sp_dropalias，在升級的資料庫中移除別名。 每次編譯時發生一次。|  
|sp_dropapprole|遇到 sp_dropapprole 程序。 請改用 DROP APPLICATION ROLE。 每次查詢時發生一次。|  
|sp_dropextendedproc|遇到 sp_dropextendedproc 程序。 請改用 CLR。 每次編譯時發生一次。|  
|sp_droplogin|遇到 sp_droplogin 程序。 請改用 DROP LOGIN。 每次查詢時發生一次。|  
|sp_dropremotelogin|遇到 sp_dropremotelogin 程序。 請改用連結的伺服器。|  
|sp_droprole|遇到 sp_droprole 程序。 請改用 DROP ROLE。 每次查詢時發生一次。|  
|sp_droptype|遇到 sp_droptype 程序。 請改用 DROP TYPE。|  
|sp_dropuser|遇到 sp_dropuser 程序。 請改用 DROP USER。 每次查詢時發生一次。|  
|sp_estimated_rowsize_reduction_for_vardecimal|遇到了 **vardecimal** 儲存格式的使用。 請改用資料壓縮及 sp_estimate_data_compression_savings。|  
|sp_fulltext_catalog|遇到 sp_fulltext_catalog 程序。 請改用 CREATE/ALTER/DROP FULLTEXT CATALOG。 每次編譯時發生一次。|  
|sp_fulltext_column|遇到 sp_fulltext_column 程序。 請改用 ALTER FULLTEXT INDEX。 每次編譯時發生一次。|  
|sp_fulltext_database|遇到 sp_fulltext_database 程序。 請改用 ALTER DATABASE。 每次編譯時發生一次。|  
|sp_fulltext_service \@action=clean_up|遇到 sp_fulltext_service 程序的 clean_up 選項。 每次查詢時發生一次。|  
|sp_fulltext_service \@action=connect_timeout|遇到 sp_fulltext_service 程序的 connect_timeout 選項。 每次查詢時發生一次。|  
|sp_fulltext_service \@action=data_timeout|遇到 sp_fulltext_service 程序的 data_timeout 選項。 每次查詢時發生一次。|  
|sp_fulltext_service \@action=resource_usage|遇到 sp_fulltext_service 程序的 resource_usage 選項。 這個選項沒有函數。 每次查詢時發生一次。|  
|sp_fulltext_table|遇到 sp_fulltext_table 程序。 請改用 CREATE/ALTER/DROP FULLTEXT INDEX。 每次編譯時發生一次。|  
|sp_getbindtoken|遇到 sp_getbindtoken 程序。 請改用 Multiple Active Result Set (MARS) 或分散式交易。 每次編譯時發生一次。|  
|sp_grantdbaccess|遇到 sp_grantdbaccess 程序。 請改用 CREATE USER。 每次查詢時發生一次。|  
|sp_grantlogin|遇到 sp_grantlogin 程序。 請改用 CREATE LOGIN。 每次查詢時發生一次。|  
|sp_help_fulltext_catalog_components|遇到 sp_help_fulltext_catalog_components 程序。 這個程序會傳回空的資料列。 請勿使用這個程序。 每次編譯時發生一次。|  
|sp_help_fulltext_catalogs|遇到 sp_help_fulltext_catalogs 程序。 請改為查詢 sys.fulltext_catalogs。 每次編譯時發生一次。|  
|sp_help_fulltext_catalogs_cursor|遇到 sp_help_fulltext_catalogs_cursor 程序。 請改為查詢 sys.fulltext_catalogs。 每次編譯時發生一次。|  
|sp_help_fulltext_columns|遇到 sp_help_fulltext_columns 程序。 請改為查詢 sys.fulltext_index_columns。 每次編譯時發生一次。|  
|sp_help_fulltext_columns_cursor|遇到 sp_help_fulltext_columns_cursor 程序。 請改為查詢 sys.fulltext_index_columns。 每次編譯時發生一次。|  
|sp_help_fulltext_tables|遇到 sp_help_fulltext_tables 程序。 請改為查詢 sys.fulltext_indexes。 每次編譯時發生一次。|  
|sp_help_fulltext_tables_cursor|遇到 sp_help_fulltext_tables_cursor 程序。 請改為查詢 sys.fulltext_indexes。 每次編譯時發生一次。|  
|sp_helpdevice|遇到 sp_helpdevice 程序。 請改為查詢 sys.backup_devices。 每次查詢時發生一次。|  
|sp_helpextendedproc|遇到 sp_helpextendedproc 程序。 請改用 CLR。 每次編譯時發生一次。|  
|sp_helpremotelogin|遇到 sp_helpremotelogin 程序。 請改用連結的伺服器。|  
|sp_indexoption|遇到 sp_indexoption 程序。 請改用 ALTER INDEX。 每次編譯時發生一次。|  
|sp_lock|遇到 sp_lock 程序。 請改為查詢 sys.dm_tran_locks。 每次查詢時發生一次。|  
|sp_password|遇到 sp_password 程序。 請改用 ALTER LOGIN。 每次查詢時發生一次。|  
|sp_remoteoption|遇到 sp_remoteoption 程序。 請改用連結的伺服器。|  
|sp_renamedb|遇到 sp_renamedb 程序。 請改用 ALTER DATABASE。 每次查詢時發生一次。|  
|sp_resetstatus|遇到 sp_resetstatus 程序。 請改用 ALTER DATABASE。 每次查詢時發生一次。|  
|sp_revokedbaccess|遇到 sp_revokedbaccess 程序。 請改用 DROP USER。 每次查詢時發生一次。|  
|sp_revokelogin|遇到 sp_revokelogin 程序。 請改用 DROP LOGIN。 每次查詢時發生一次。|  
|sp_srvrolepermission|遇到已被取代的 sp_srvrolepermission 程序。 請勿使用。 每次查詢時發生一次。|  
|sp_unbindefault|遇到 sp_unbindefault 程序。 請在 CREATE TABLE 或 ALTER TABLE 陳述式中改為使用 DEFAULT 關鍵字。 每次編譯時發生一次。|  
|sp_unbindrule|遇到 sp_unbindrule 程序。 請使用檢查條件約束來取代規則。 每次編譯時發生一次。|  
|SQL_AltDiction_CP1253_CS_AS|每次啟動資料庫及使用定序時，事件會發生一次。 請規劃修改使用此定序的應用程式。|  
|當做資料行別名的字串常值|遇到的語法包含了在 SELECT 陳述式中 (例如 `'string' = expression`) 當做資料行別名使用的字串。 請勿使用。 每次編譯時發生一次。|  
|sys.sql_dependencies|遇到 sys.sql_dependencies 的參考。 請改用 sys.sql_expression_dependencies。 每次編譯時發生一次。|  
|sysaltfiles|遇到 sysaltfiles 的參考。 請改用 sys.master_files。 每次編譯時發生一次。|  
|syscacheobjects|遇到 syscacheobjects 的參考。 請改用 sys.dm_exec_cached_plans、sys.dm_exec_plan_attributes 和 sys.dm_exec_sql_text。 每次編譯時發生一次。|  
|syscolumns|遇到 syscolumns 的參考。 請改用 sys.columns。 每次編譯時發生一次。|  
|syscomments|遇到 syscomments 的參考。 請改用 sys.sql_modules。 每次編譯時發生一次。|  
|sysconfigures|遇到 sysconfigures 資料表的參考。 請改為參考 sys.sysconfigures 檢視表。 每次編譯時發生一次。|  
|sysconstraints|遇到 sysconstraints 的參考。請改用 sys.check_constraints、sys.default_constraints、sys.key_constraints、sys.foreign_keys。 每次編譯時發生一次。|  
|syscurconfigs|遇到 syscurconfigs 的參考。 請改用 sys.configurations。 每次編譯時發生一次。|  
|sysdatabases|遇到 sysdatabases 的參考。 請改用 sys.databases。 每次編譯時發生一次。|  
|sysdepends|遇到 sysdepends 的參考。 請改用 sys.sql_dependencies。 每次編譯時發生一次。|  
|sysdevices|遇到 sysdevices 的參考。 請改用 sys.backup_devices。 每次編譯時發生一次。|  
|sysfilegroups|遇到 sysfilegroups 的參考。 請改用 sys.filegroups。 每次編譯時發生一次。|  
|sysfiles|遇到 sysfiles 的參考。 請改用 sys.database_files。 每次編譯時發生一次。|  
|sysforeignkeys|遇到 sysforeignkeys 的參考。 請改用 sys.foreign_keys。 每次編譯時發生一次。|  
|sysfulltextcatalogs|遇到 sysfulltextcatalogs 的參考。 請改用 sys.fulltext_catalogs。 每次編譯時發生一次。|  
|sysindexes|遇到 sysindexes 的參考。 請改用 sys.indexes, sys.partitions、sys.allocation_units 和 sys.dm_db_partition_stats。 每次編譯時發生一次。|  
|sysindexkeys|遇到 sysindexkeys 的參考。 請改用 sys.index_columns。 每次編譯時發生一次。|  
|syslockinfo|遇到 syslockinfo 的參考。 請改用 sys.dm_tran_locks。 每次編譯時發生一次。|  
|syslogins|遇到 syslogins 的參考。 請改用 sys.server_principals 和 sys.sql_logins。 每次編譯時發生一次。|  
|sysmembers|遇到 sysmembers 的參考。 請改用 sys.database_role_members。 每次編譯時發生一次。|  
|sysmessages|遇到 sysmessages 的參考。 請改用 sys.messages。 每次編譯時發生一次。|  
|sysobjects|遇到 sysobjects 的參考。 請改用 sys.objects。 每次編譯時發生一次。|  
|sysoledbusers|遇到 sysoledbusers 的參考。 請改用 sys.linked_logins。 每次編譯時發生一次。|  
|sysopentapes|遇到 sysopentapes 的參考。 請改用 sys.dm_io_backup_tapes。 每次編譯時發生一次。|  
|sysperfinfo|遇到 sysperfinfo 的參考。 請使用 sys.dm_os_performance_counters。 加以取代。 每次編譯時發生一次。|  
|syspermissions|遇到 syspermissions 的參考。 請改用 sys.database_permissions 和 sys.server_permissions。 每次編譯時發生一次。|  
|sysprocesses|遇到 sysprocesses 的參考。 請改用 sys.dm_exec_connections、sys.dm_exec_sessions 和 sys.dm_exec_requests。 每次編譯時發生一次。|  
|sysprotects|遇到 sysprotects 的參考。 請改用 sys.database_permissions 和 sys.server_permissions。 每次編譯時發生一次。|  
|sysreferences|遇到 sysreferences 的參考。 請改用 sys.foreign_keys。 每次編譯時發生一次。|  
|sysremotelogins|遇到 sysremotelogins 的參考。 請改用 sys.remote_logins。 每次編譯時發生一次。|  
|sysservers|遇到 sysservers 的參考。 請改用 sys.servers。 每次編譯時發生一次。|  
|systypes|遇到 systypes 的參考。 請改用 sys.types。 每次編譯時發生一次。|  
|sysusers|遇到 sysusers 的參考。 請改用 sys.database_principals。 每次編譯時發生一次。|  
|沒有 WITH 的資料表提示|遇到了一個使用資料表提示但未使用 WITH 關鍵字的陳述式。 請修改陳述式，使其包含 WITH 字。 每次編譯時發生一次。|  
|Text in row 資料表選項|遇到 'text in row' 資料表選項的參考。 請改用 sp_tableoption 'large value types out of row'。 每次查詢時發生一次。|  
|TEXTPTR|遇到 TEXTPTR 函數的參考。 請重寫應用程式來使用 **varchar(max)** 資料類型及移除 **text**、 **ntext**和 **image** 資料類型語法。 每次查詢時發生一次。|  
|TEXTVALID|遇到 TEXTVALID 函數的參考。 請重寫應用程式來使用 **varchar(max)** 資料類型及移除 **text**、 **ntext**和 **image** 資料類型語法。 每次查詢時發生一次。|  
|timestamp|DDL 陳述式中遇到之已被取代的 **timestamp** 資料類型的總次數。 請改用 **rowversion** 資料類型。|  
|UPDATETEXT 或 WRITETEXT|遇到 UPDATETEXT 或 WRITETEXT 陳述式。 請重寫應用程式來使用 **varchar(max)** 資料類型及移除 **text**、 **ntext**和 **image** 資料類型語法。 每次查詢時發生一次。|  
|USER_ID|遇到 USER_ID 函數的參考。 請改用 DATABASE_PRINCIPAL_ID 函數。 每次編譯時發生一次。|  
|針對連結的伺服器使用 OLEDB||  
|Vardecimal 儲存格式|遇到了 **vardecimal** 儲存格式的使用。 請改用資料壓縮。|  
|XMLDATA|遇到 FOR XML 語法。 針對 RAW 和 AUTO 模式使用 XSD 產生。 明確的模式不會有任何取代項目。 每次編譯時發生一次。|  
|XP_API|遇到擴充預存程序陳述式。 請勿使用。|  
|xp_grantlogin|遇到 xp_grantlogin 程序。 請改用 CREATE LOGIN。 每次編譯時發生一次。|  
|xp_loginConfig|遇到 xp_loginconfig 程序。 請改用 SERVERPROPERTY 的 IsIntegratedSecurityOnly 引數。 每次查詢時發生一次。|  
|xp_revokelogin|遇到 xp_revokelogin 程序。 請改用 ALTER LOGIN DISABLE 或 DROP LOGIN。 每次編譯時發生一次。|  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 2016 中已被取代的 Database Engine 功能](../../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)   
 [SQL Server 2016 中已被取代的全文檢索搜尋功能](../../relational-databases/search/deprecated-full-text-search-features-in-sql-server-2016.md)   
 [Deprecation Announcement 事件類別](../../relational-databases/event-classes/deprecation-announcement-event-class.md)   
 [Deprecation Final Support 事件類別](../../relational-databases/event-classes/deprecation-final-support-event-class.md)   
 [SQL Server 2016 中已停止的 Database Engine 功能](../../database-engine/discontinued-database-engine-functionality-in-sql-server.md)   
 [SQL Server 2016 內停止的全文檢索搜尋功能](../../database-engine/discontinued-database-engine-functionality-in-sql-server.md)   
 [使用 SQL Server 物件](../../relational-databases/performance-monitor/use-sql-server-objects.md)  
  
