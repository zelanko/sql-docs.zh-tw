---
title: 資料庫檔案與檔案群組 | Microsoft 文件
ms.custom: ''
ms.date: 01/07/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- databases [SQL Server], files
- filegroups [SQL Server]
- transaction logs [SQL Server], about
- transaction logs [SQL Server], files
- .mdf files
- data files [SQL Server]
- default filegroups
- files [SQL Server], about files and filegroups
- secondary files [SQL Server]
- log files [SQL Server]
- .ndf files
- files [SQL Server]
- .ldf files
- database files [SQL Server]
- databases [SQL Server], filegroups
- filegroups [SQL Server], types
- primary filegroups [SQL Server]
- user-defined filegroups [SQL Server]
- filegroups [SQL Server], about filegroups
- primary files [SQL Server]
- file types [SQL Server]
ms.assetid: 9ca11918-480d-4838-9198-cec221ef6ad0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a2f78e8fbff4a5fdc896810067ad2552b59336a8
ms.sourcegitcommit: 1a5448747ccb2e13e8f3d9f04012ba5ae04bb0a3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/12/2018
ms.locfileid: "51558935"
---
# <a name="database-files-and-filegroups"></a>資料庫檔案與檔案群組
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  基本上，每個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫都有兩個作業系統檔案：資料檔與記錄檔。 資料檔包含諸如資料表、索引、預存程序以及檢視等資料和物件。 記錄檔包含復原資料庫中所有交易必要的資訊。 資料檔可以組成檔案群組，以方便配置及管理。  
  
## <a name="database-files"></a>資料庫檔案  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫有三種檔案類型，如下表所示。  
  
|檔案|Description|  
|----------|-----------------|  
|Primary|主要資料檔包含資料庫啟動資訊，並指到資料庫中的其他檔案。 使用者資料和物件可儲存於此檔案或次要的資料檔中。 每個資料庫都有一個主要資料檔案。 建議您將主要資料檔的副檔名設為 .mdf。|  
|次要|次要資料檔是選擇性且使用者自訂的，並可儲存使用者資料。 次要檔可用以將資料分散在多個磁碟上，即透過將每個檔案放在不同的磁碟機上來達成此目的。 此外，若資料庫超過了單一 Windows 檔案的大小上限，您可使用次要資料檔，以容許資料庫繼續成長。<br /><br /> 建議您將次要資料檔的副檔名設為 .ndf。|  
|交易記錄|交易記錄檔包含了用來復原資料庫的記錄資訊。 每個資料庫至少要有一個記錄檔。 建議的交易記錄檔的副檔名為 .ldf。|  
  
 例如，一個簡單的資料庫 **Sales** 可由一個包含所有資料和物件的主要檔案，以及一個包含交易記錄資訊的記錄檔所組成。 也可以建立名稱為 **Orders** 的複雜資料庫，以包含一個主要檔案和五個次要檔案。 在資料庫中的資料和物件平均分散於總共六個檔案中，而且有四個記錄檔包含交易記錄資訊。  
  
 依預設，資料和交易記錄會放置在相同的磁碟和路徑中。 這是透過處理單一磁碟系統來完成。 然而，這對於實際執行環境可能不是最合適的。 我們建議您將資料和記錄檔放在不同的磁碟上。  

### <a name="logical-and-physical-file-names"></a>邏輯與實體檔案名稱
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 檔案有兩個檔案名稱類型： 

**logical_file_name：**  logical_file_name 是用來在所有 Transact-SQL 陳述式中指稱實體檔案的名稱。 邏輯檔案名稱必須遵守 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 識別碼的規則，而且在資料庫的邏輯檔案名稱之間必須是唯一的。 這是由 `ALTER DATABASE` 中的 `NAME` 引數所設定。 如需詳細資訊，請參閱 [ALTER DATABASE 檔案及檔案群組選項 &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)。

**os_file_name：** os_file_name 是包含目錄路徑的實體檔案名稱。 它必須遵循作業系統檔案名稱的規則。 這是由 `ALTER DATABASE` 中的 `FILENAME` 引數所設定。 如需詳細資訊，請參閱 [ALTER DATABASE 檔案及檔案群組選項 &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)。

> [!IMPORTANT]
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料及記錄檔可以放在 FAT 或 NTFS 檔案系統， 在 Windows 系統上，因為 NTFS 安全性層面，我們建議使用 NTFS 檔案系統。 

> [!WARNING]
> 但是讀寫資料檔案群組及記錄檔不能放在 NTFS 壓縮檔案系統。 只有唯讀資料庫及唯讀次要檔案群組，才能放在 NTFS 壓縮檔案系統。
> 為節省空間，強烈建議使用[資料壓縮](../../relational-databases/data-compression/data-compression.md)，而不要使用檔案系統壓縮。

若有多個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體執行於同一部電腦上，每個執行個體都會收到不同的預設目錄來包含建立於執行個體中的資料庫檔案。 如需詳細資訊，請參閱 [SQL Server 預設和具名執行個體的檔案位置](../../sql-server/install/file-locations-for-default-and-named-instances-of-sql-server.md)。

### <a name="data-file-pages"></a>資料檔分頁
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料檔中的分頁是循序編號，從零 (0) 開始，表示檔案中的第一頁。 資料庫中的每一個檔案都具有唯一的檔案識別碼。 若要唯一地識別資料庫中的分頁，則同時需要檔案識別碼及頁碼。 下例顯示了擁有 4-MB 主要資料檔與 1-MB 次要資料檔之資料庫中的頁數。

![data_file_pages](../../relational-databases/databases/media/data-file-pages.gif)

每個檔案的第一個分頁，是包含了檔案屬性相關資訊的檔案標頭分頁。 檔案開頭的幾個其他分頁中也包含系統資訊，如配置對應。 同時儲存於主要資料檔與第一個記錄檔的系統分頁中，有一個是資料庫開機分頁，其中包含了資料庫屬性的相關資訊。 如需頁面及頁面類型的詳細資訊，請參閱[頁面與範圍架構指南](../..//relational-databases/pages-and-extents-architecture-guide.md)。

### <a name="file-size"></a>檔案大小
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 檔案可以從它們原本指定的大小自動成長。 當您定義檔案時，可指定特定的成長遞增。 每次檔案填滿時，它就會根據成長遞增值來增加其大小。 若檔案群組中有多個檔案，則必須等到所有檔案都填滿之後，才會開始自動成長。 接著成長會使用[比例填滿](../../relational-databases/pages-and-extents-architecture-guide.md#ProportionalFill)，以循環配置的方式來進行。

也可為每個檔案指定最大的大小。 若並未指定最大的大小，檔案將持續成長，直到它用完磁碟中所有可用的空間為止。 當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 是用做應用程式中內嵌的資料庫，而且使用者不是那麼容易聯繫到系統管理員時，此項功能會特別有用。 使用者可以讓檔案依需要自動成長，以減輕監視資料庫中可用空間以及手動配置額外空間的管理負擔。  

如果已針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 啟用[立即檔案初始化 (IFI)](../../relational-databases/databases/database-instant-file-initialization.md)，配置資料檔案的新空間時額外負荷會最少。

如需交易記錄檔管理的詳細資訊，請參閱[管理交易記錄檔的大小](../../relational-databases/logs/manage-the-size-of-the-transaction-log-file.md#Recommendations)。   

## <a name="database-snapshot-files"></a>資料庫快照集檔案
資料庫快照集用來儲存其「寫入時複製」資料的檔案格式，視快照集是由使用者建立或是內部使用而定：

* 使用者所建立的資料庫快照集是將其資料儲存在一個或多個疏鬆檔案。 疏鬆檔案技術是 NTFS 檔案系統的一項功能。 一開始，疏鬆檔案未包含使用者資料，而且也尚未配置使用者資料的磁碟空間給疏鬆檔案。 如需有關使用資料庫快照集中的疏鬆檔案，以及資料庫快照集如何成長的一般資訊，請參閱 [檢視資料庫快照集的疏鬆檔案大小](../../relational-databases/databases/view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql.md)。 
* 資料庫快照集是由特定 DBCC 命令內部使用。 這些命令包括 DBCC CHECKDB、DBCC CHECKTABLE、DBCC CHECKALLOC 和 DBCC CHECKFILEGROUP。 內部資料庫快照集使用原始資料庫檔案的疏鬆替代資料流。 和疏鬆檔案一樣，替代資料流也是 NTFS 檔案系統的一項功能。 使用疏鬆替代資料流可讓多個資料配置與單一檔案或資料夾相關聯，但不影響檔案大小或磁碟區統計資料。 
  
## <a name="filegroups"></a>檔案群組  
 每個資料庫有一個主要的檔案群組。 此檔案群組可能包含主要資料檔和未放入其他檔案群組的次要檔案。 可建立使用者自訂檔案群組來將資料檔群組在一起，以利管理、資料配置和放置之用。  
  
 例如，您以可將三個檔案 (`Data1.ndf`、`Data2.ndf` 以及 `Data3.ndf`) 分別建立於三部磁碟機內，並將它們指派至檔案群組 `fgroup1`。 接著您可根據檔案群組 `fgroup1` 來建立資料表。 資料表的資料查詢可分散至三個磁碟，藉此改善效能。 另一個改善效能的作法是將單一檔案建立在 RAID (獨立磁碟的重複陣列，通稱磁碟陣列) 的條狀磁碟組上。 然而，檔案和檔案群組都可讓您輕鬆地將新的檔案加至新的磁碟內。  
  
 所有儲存在檔案群組中的資料檔列於下表。  
  
|檔案群組|Description|  
|---------------|-----------------|  
|Primary|包含主要檔案的檔案群組。 所有的系統資料表都配置於主要檔案群組內。|  
|記憶體最佳化資料|記憶體最佳化檔案群組是根據檔案資料流檔案群組|  
|檔案資料流||    
|使用者自訂|使用者在初次建立資料庫或之後修改資料庫時，特別建立的檔案群組。|  
  
### <a name="default-primary-filegroup"></a>預設 (主要) 檔案群組  
 若在資料庫中建立物件時未指明屬於哪個檔案群組，就會將物件指定至預設的檔案群組。 在任何時候，都只有一個檔案群組指定為預設檔案群組。 在預設檔案群組中的檔案必須夠大，才能容納未配置到其他檔案群組的新物件。  
  
 除非使用 ALTER DATABASE 陳述式加以變更，否則 PRIMARY 檔案群組就是預設的檔案群組。 系統物件和資料表仍配置於 PRIMARY 檔案群組內，而非新的預設檔案群組之中。  
 
### <a name="memory-optimized-data-filegroup"></a>記憶體最佳化資料檔案群組

如需記憶體最佳化檔案群組的詳細資訊，請參閱[記憶體最佳化檔案群組](../../relational-databases/in-memory-oltp/the-memory-optimized-filegroup.md)。

### <a name="filestream-filegroup"></a>檔案資料流檔案群組

如需檔案資料流檔案群組的詳細資訊，請參閱 [FILESTREAM](../../relational-databases/blob/filestream-sql-server.md#filestream-storage) 和[建立啟用 FILESTREAM 的資料庫](../../relational-databases/blob/create-a-filestream-enabled-database.md)。

### <a name="file-and-filegroup-example"></a>檔案與檔案群組範例
 下例會在 SQL Server 的執行個體上建立資料庫。 資料庫會有主要資料檔、使用者自訂的檔案群組以及記錄檔。 主要資料檔位於主要的檔案群組中，而使用者自訂的檔案群組則擁有兩個次要資料檔。 ALTER DATABASE 陳述式可讓使用者自訂的檔案群組成為預設的檔案群組。 接著系統將建立一個資料表來指定使用者自訂的檔案群組。 (本例會使用一般路徑 `c:\Program Files\Microsoft SQL Server\MSSQL.1` 以避免指定 SQL Server 版本。)

```sql
USE master;
GO
-- Create the database with the default data
-- filegroup, filstream filegroup and a log file. Specify the
-- growth increment and the max size for the
-- primary data file.
CREATE DATABASE MyDB
ON PRIMARY
  ( NAME='MyDB_Primary',
    FILENAME=
       'c:\Program Files\Microsoft SQL Server\MSSQL.1\MSSQL\data\MyDB_Prm.mdf',
    SIZE=4MB,
    MAXSIZE=10MB,
    FILEGROWTH=1MB),
FILEGROUP MyDB_FG1
  ( NAME = 'MyDB_FG1_Dat1',
    FILENAME =
       'c:\Program Files\Microsoft SQL Server\MSSQL.1\MSSQL\data\MyDB_FG1_1.ndf',
    SIZE = 1MB,
    MAXSIZE=10MB,
    FILEGROWTH=1MB),
  ( NAME = 'MyDB_FG1_Dat2',
    FILENAME =
       'c:\Program Files\Microsoft SQL Server\MSSQL.1\MSSQL\data\MyDB_FG1_2.ndf',
    SIZE = 1MB,
    MAXSIZE=10MB,
    FILEGROWTH=1MB),
FILEGROUP FileStreamGroup1 CONTAINS FILESTREAM
  ( NAME = 'MyDB_FG_FS',
    FILENAME = 'c:\Data\filestream1')
LOG ON
  ( NAME='MyDB_log',
    FILENAME =
       'c:\Program Files\Microsoft SQL Server\MSSQL.1\MSSQL\data\MyDB.ldf',
    SIZE=1MB,
    MAXSIZE=10MB,
    FILEGROWTH=1MB);
GO
ALTER DATABASE MyDB 
  MODIFY FILEGROUP MyDB_FG1 DEFAULT;
GO

-- Create a table in the user-defined filegroup.
USE MyDB;
CREATE TABLE MyTable
  ( cola int PRIMARY KEY,
    colb char(8) )
ON MyDB_FG1;
GO

-- Create a table in the filestream filegroup
CREATE TABLE MyFSTable
(
    cola int PRIMARY KEY,
  colb VARBINARY(MAX) FILESTREAM NULL
)
GO
```

下圖摘要說明上述範例的結果 (但不包含檔案資料流資料)。

![filegroup_example](../../relational-databases/databases/media/filegroup-example.gif)

## <a name="file-and-filegroup-fill-strategy"></a>檔案與檔案群組填滿策略
檔案群組針對每個檔案群組內的所有檔案，使用比例性的填滿策略。 當資料寫入檔案群組時，[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 不會將所有資料都寫入第一個檔案，直到該檔案滿了為止；而是在檔案群組內的每一個檔案中，寫入與檔案可用空間等比例的量， 然後再寫入下一個檔案。 例如，若檔案 f1 有 100 MB 可用空間、檔案 f2 有 200 MB 可用空間，系統就會從檔案 f1 配置 1 份範圍，再從檔案 f2 配置 2 份範圍，其餘依此類推。 如此一來，兩個檔案大約會在相同的時間填滿，而達成簡易等量配置。

檔案群組中的所有檔案都填滿之後，[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 會以循環配置的方式，自動一次擴充一個檔案，以容納更多資料，但前提是資料庫必須設定為自動成長。 例如，檔案群組由 3 個檔案組成，全部都設為自動成長。 當檔案群組中所有檔案的空間都用完時，只會先擴充第 1 個檔案。 當第 1 個檔案已滿，不能再寫入更多資料到檔案群組時，再擴充第 2 個檔案。 當第 2 個檔案已滿，不能再寫入更多資料到檔案群組時，再擴充第 3 個檔案。 如果第 3 個檔案已滿，不能再寫入更多資料到檔案群組時，再重新擴充第 1 個檔案，依此類推。

## <a name="rules-for-designing-files-and-filegroups"></a>設計檔案與檔案群組的規則
下列規則是關於檔案和檔案群組：
- 檔案或檔案群組無法由多個資料庫所使用。 例如，sales.mdf 和 sales.ndf 檔案包含來自 sales 資料庫的資料和物件，其他的資料庫並無法使用它們。
- 檔案只能作為一個檔案群組的成員。
- 交易記錄檔不能為任何檔案群組的一部分。

## <a name="Recommendations"></a> 建議
以下是關於使用檔案和檔案群組時的一般建議： 
- 大多數的資料庫只需要一個資料檔和一個交易記錄檔即可順利運作。
- 若使用多個資料檔案，可替額外的檔案建立第二個檔案群組，並讓該檔案群組成為預設的檔案群組。 如此一來，主要檔案將只包含系統資料表和物件。
- 若要使效能達到最大，請盡量在不同的可用磁碟上建立檔案或檔案群組。 並把極佔空間的物件放在不同的檔案群組中。
- 使用檔案群組，將物件放置在特定的實體磁碟上。
- 將同一個聯結查詢用到的不同資料表，放在不同的檔案群組內。 這樣可改進效能，因為可用平行磁碟 I/O 搜尋聯結資料。
- 把存取量大的資料表和屬於這些資料表的非叢集索引，放在不同的檔案群組中。 這樣可改進效能，因為檔案如果位於不同實體磁碟上，可進行平行 I/O。
- 請勿將交易記錄檔放在有其他檔案和檔案群組的同一個實體磁碟上。

如需交易記錄檔管理建議的詳細資訊，請參閱[管理交易記錄檔的大小](../../relational-databases/logs/manage-the-size-of-the-transaction-log-file.md#Recommendations)。   

## <a name="related-content"></a>相關內容  
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)    
 [ALTER DATABASE 檔案及檔案群組選項 &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)      
 [資料庫卸離與附加 &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)  
 [SQL Server 交易記錄架構與管理指南](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md)    
 [分頁與範圍架構指南](../../relational-databases/pages-and-extents-architecture-guide.md)    
 [管理交易記錄檔的大小](../../relational-databases/logs/manage-the-size-of-the-transaction-log-file.md)     
