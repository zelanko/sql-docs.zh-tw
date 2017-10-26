---
title: "資料表和預存程序的原生編譯 | Microsoft Docs"
ms.custom: 
ms.date: 04/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5880fbd9-a23e-464a-8b44-09750eeb2dad
caps.latest.revision: 23
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: 5f74f31531f0b3c966235396d91ce12b00428d5c
ms.openlocfilehash: 922e6a4a0df86f82012670874d49b65e1338b53c
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="native-compilation-of-tables-and-stored-procedures"></a>資料表和預存程序的原生編譯

記憶體中 OLTP 導入了原生編譯的概念。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可原生編譯用來存取記憶體最佳化資料表的預存程序。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 也可以透過原生方式編譯記憶體最佳化資料表。 與解譯的 (傳統) [!INCLUDE[tsql](../../includes/tsql-md.md)]相較之下，原生編譯可提供更快速的資料存取並且更有效率地執行查詢。 資料表和預存程序的原生編譯會產生 DLL。

另外也支援記憶體最佳化資料表類型的原生編譯。 如需詳細資訊，請參閱 [使用記憶體最佳化加快暫存資料表與資料表變數的速度](../../relational-databases/in-memory-oltp/faster-temp-table-and-table-variable-by-using-memory-optimization.md)。

原生編譯是指將程式設計結構轉換成原生程式碼的程序，包含處理器指令，而不需再進一步編譯或解譯。

記憶體內 OLTP 會在建立記憶體最佳化資料表時，以及原生編譯預存程序載入原生 DLL 時，對兩者編譯記憶體最佳化資料表。 此外，DLL 會在資料庫或伺服器重新啟動之後重新編譯。 重新建立 DLL 所需的資訊儲存在資料庫中繼資料內。 DLL 不是資料庫的一部分，不過它們與資料庫相關聯。 例如，DLL 不包含在資料庫備份中。

> [!NOTE]
> 記憶體最佳化資料表會在重新啟動伺服器期間重新編譯。 為了加速資料庫的復原，不會在啟動伺服器期間重新編譯原生編譯預存程序，而是會在第一次執行時進行編譯。 因為此延遲編譯，原生編譯預存程序只會在第一次執行後，呼叫 [sys.dm_os_loaded_modules &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-loaded-modules-transact-sql.md) 時出現。

## <a name="maintenance-of-in-memory-oltp-dlls"></a>維護記憶體中 OLTP DLL

下列查詢顯示目前載入伺服器記憶體中的所有資料表和預存程序 DLL：

```tsql
SELECT
        mod1.name,
        mod1.description
    from
        sys.dm_os_loaded_modules  as mod1
    where
        mod1.description = 'XTP Native DLL';
```

資料庫管理員不需要維護原生編譯所產生的檔案。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會在不再需要時自動移除產生的檔案。 例如，產生的檔案會在資料表和預存程序已刪除，或資料庫卸載時移除。

> [!NOTE]
> 編譯失敗或中斷時，某些產生的檔案並不會刪除。 刻意留下這些檔案是為了提供支援，而這些檔案會在資料庫卸除時移除。

> [!NOTE]
> SQL Server 會為資料庫復原所需的所有資料表編譯 DLL。 如果資料表在資料庫重新啟動之前已卸除，則檢查點檔案或交易記錄檔中可能仍有剩餘的資料表，讓資料表 DLL 可能會在資料庫啟動期間重新編譯。 重新啟動之後 DLL 將會被卸載，一般的清理程序就會移除檔案。

## <a name="native-compilation-of-tables"></a>資料表的原生編譯

使用 **CREATE TABLE** 陳述式建立記憶體最佳化資料表會導致將資料表資訊寫入資料庫中繼資料，並且在記憶體中建立資料表和索引結構。 資料表也會編譯為 DLL。

請考慮下列範例指令碼，該指令碼會建立資料庫和記憶體最佳化資料表：

```tsql
USE master;
GO

CREATE DATABASE DbMemopt3;
GO

ALTER DATABASE DbMemopt3
    add filegroup DbMemopt3_mod_memopt_1_fg
        contains memory_optimized_data
;
GO

-- You must edit the front portion of filename= path, to where your DATA\ subdirectory is,
-- keeping only the trailing portion '\DATA\DbMemopt3_mod_memopt_1_fn'!

ALTER DATABASE DbMemopt3
    add file
    (
        name     = 'DbMemopt3_mod_memopt_1_name',
        filename = 'C:\DATA\DbMemopt3_mod_memopt_1_fn'

        --filename = 'C:\Program Files\Microsoft SQL Server\MSSQL13.SQLSVR2016ID\MSSQL\DATA\DbMemopt3_mod_memopt_1_fn'
    )
        to filegroup DbMemopt3_mod_memopt_1_fg
;
GO

USE DbMemopt3;
GO

CREATE TABLE dbo.t1
(
    c1 int not null primary key nonclustered,
    c2 int
)
    with (memory_optimized = on)
;
GO



-- You can safely rerun from here to the end.

-- Retrieve the path of the DLL for table t1.


DECLARE @moduleName  nvarchar(256);

SET @moduleName =
    (
        '%xtp_t_' +
        cast(db_id() as nvarchar(16)) +
        '_' +
        cast(object_id('dbo.t1') as nvarchar(16)) +
        '%.dll'
    )
;


-- SEARCHED FOR NAME EXAMPLE:  mod1.name LIKE '%xtp_t_8_565577053%.dll'
PRINT @moduleName;


SELECT
        mod1.name,
        mod1.description
    from
        sys.dm_os_loaded_modules  as mod1
    where
        mod1.name LIKE @moduleName
    order by
        mod1.name
;
-- ACTUAL NAME EXAMPLE:  mod1.name = 'C:\Program Files\Microsoft SQL Server\MSSQL13.SQLSVR2016ID\MSSQL\DATA\xtp\8\xtp_t_8_565577053_184009305855461.dll'
GO

--   DROP DATABASE DbMemopt3;  -- Clean up.
GO
```

建立資料表也會建立資料表 DLL 並將 DLL 載入記憶體中。 CREATE TABLE 陳述式後面緊接著的 DMV 查詢會擷取資料表 DLL 的路徑。

資料表 DLL 可理解資料表的索引結構和資料列格式。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會使用 DLL 周遊索引、擷取資料列，以及儲存資料列內容。

## <a name="native-compilation-of-stored-procedures"></a>預存程序的原生編譯

標示為 NATIVE_COMPILATION 的預存程序為原生編譯。 這表示，程序中的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式全都編譯為原生程式碼，能夠有效率地執行效能具有決定性的商務邏輯。

如需原生編譯的預存程序的詳細資訊，請參閱 [原生編譯的預存程序](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)。

請考慮下列範例預存程序，它會在上一個範例的資料表 t1 中插入資料列：

```tsql
CREATE PROCEDURE dbo.native_sp
    with native_compilation,
         schemabinding,
         execute as owner
as
begin atomic
    with (transaction isolation level = snapshot,
          language = N'us_english')

    DECLARE @i int = 1000000;

    WHILE @i > 0
    begin
        INSERT dbo.t1 values (@i, @i+1);
        SET @i -= 1;
    end
end;
GO

EXECUTE dbo.native_sp;
GO

-- Reset.

DELETE from dbo.t1;
GO
```

native_sp 的 DLL 可直接與 t1 的 DLL 以及記憶體中 OLTP 儲存引擎互動，以盡快將資料列插入。

記憶體中 OLTP 編譯器會利用查詢最佳化工具，為預存程序中的每個查詢建立有效率的執行計畫。 請注意，原生編譯的預存程序不會在資料表中的資料變更時自動重新編譯。 如需維護記憶體內部 OLTP 中的統計資料和預存程序的詳細資訊，請參閱 [記憶體最佳化資料表的統計資料](../../relational-databases/in-memory-oltp/statistics-for-memory-optimized-tables.md)。

## <a name="security-considerations-for-native-compilation"></a>原生編譯的安全性考量

資料表和預存程序的原生編譯使用記憶體中 OLTP 編譯器。 此編譯器會產生寫入磁碟並載入記憶體中的檔案。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用下列機制限制這些檔案的存取權。

### <a name="native-compiler"></a>原生編譯器

原生編譯所需的編譯器可執行檔以及二進位和標頭檔案已在 MSSQL\Binn\Xtp 資料夾之下，安裝為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的一部分。 因此，若預設執行個體安裝在 C:\Program Files 之下，編譯器檔案即安裝在 C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL13.MSSQLSERVER\MSSQL\Binn\Xtp。

若要限制編譯器的存取權， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用存取控制清單 (ACL) 限制二進位檔案的存取。 所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 二進位皆受到保護，以防止其遭到修改或透過 ACL 竄改。 原生編譯器的 ACL 也限制編譯器的使用權，僅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務帳戶和系統管理員擁有原生編譯器檔案的讀取和執行權限。

### <a name="files-generated-by-a-native-compilation"></a>原生編譯產生的檔案

當資料表或預存程序進行編譯時，所產生的檔案會包含 DLL 以及中繼檔案，而中繼檔案含有下列附檔名：.c、.obj、.xml 和 .pdb。 產生的檔案會儲存在預設資料夾的子資料夾中。 這個子資料夾名為 Xtp。 使用預設資料夾安裝預設執行個體時，產生的檔案會放置於 C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL13.MSSQLSERVER\MSSQL\DATA\Xtp。

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用三種方式防止產生的 DLL 遭竄改：

- 當資料表或預存程序編譯為 DLL 時，此 DLL 會立即載入記憶體並連結到 sqlserver.exe 處理序。 DLL 連結到處理序時無法修改。

- 當資料庫重新啟動時，所有資料表和預存程序將會依據資料庫中繼資料重新編譯 (移除並重新建立)。 這將會移除惡意代理程式對產生之檔案所做的任何變更。

- 產生的資料會視為使用者資料的一部分，並和資料庫檔案擁有相同的安全性限制 (透過 ACL)：僅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務帳戶和系統管理員能夠存取這些檔案。

管理這些檔案不需要使用者互動。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會在必要時建立和移除檔案。

## <a name="see-also"></a>另請參閱

[記憶體最佳化資料表](../../relational-databases/in-memory-oltp/memory-optimized-tables.md)

[原生編譯的預存程序](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)

