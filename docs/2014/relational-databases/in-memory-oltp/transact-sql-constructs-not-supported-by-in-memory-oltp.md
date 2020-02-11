---
title: 記憶體內部 OLTP 不支援的 Transact-SQL 建構 | Microsoft 文件
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: e3f8009c-319d-4d7b-8993-828e55ccde11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dda74f247f9899b9e0a23d43143a5031574d8c13
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "63155308"
---
# <a name="transact-sql-constructs-not-supported-by-in-memory-oltp"></a>記憶體中的 OLTP 不支援 Transact-SQL 建構
  記憶體最佳化資料表和原生編譯預存程序並未支援磁碟資料表和解譯的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 預存程序所支援的全部 [!INCLUDE[tsql](../../includes/tsql-md.md)] 介面區。 嘗試使用其中一項不支援的功能時，伺服器會傳回錯誤。  
  
 錯誤訊息文字會說明 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式的類型 (例如功能、作業、選項等) 以及功能的名稱或 [!INCLUDE[tsql](../../includes/tsql-md.md)] 關鍵字。 大部分不支援的功能會傳回錯誤 10794，並提供錯誤訊息文字指出不支援的功能。 下表列出可能出現在錯誤訊息文字中的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 功能和關鍵字，以及解決錯誤的更正動作。  
  
 如需記憶體最佳化資料表和原生方式編譯預存程序之支援功能的詳細資訊，請參閱：  
  
-   [原生編譯預存程序的移轉問題](migration-issues-for-natively-compiled-stored-procedures.md)  
  
-   [記憶體內部 OLTP 的 Transact-SQL 支援](transact-sql-support-for-in-memory-oltp.md)  
  
-   [支援的 SQL Server 功能](unsupported-sql-server-features-for-in-memory-oltp.md)  
  
-   [原生編譯的預存程序](../in-memory-oltp/natively-compiled-stored-procedures.md)  
  
## <a name="databases-that-use-in-memory-oltp"></a>使用記憶體中 OLTP 的資料庫  
 下表列出錯誤訊息文字中，可能會出現和記憶體中 OLTP 資料庫有關的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 功能與關鍵字。  
  
|類型|名稱|解決方法|  
|----------|----------|----------------|  
|選項|AUTO_CLOSE|具有 MEMORY_OPTIMIZED_DATA 檔案群組的資料庫不支援資料庫選項 AUTO_CLOSE=ON。|  
|選項|ATTACH_REBUILD_LOG|具有 MEMORY_OPTIMIZED_DATA 檔案群組的資料庫不支援 CREATE 資料庫選項 ATTACH_REBUILD_LOG。|  
|功能|資料庫快照|具有 MEMORY_OPTIMIZED_DATA 檔案群組的資料庫無法建立資料庫快照。|  
|功能|使用 sync_method 'database snapshot' 或 'database snapshot character' 進行複寫|具有 MEMORY_OPTIMIZED_DATA 檔案群組的資料庫無法使用 sync_method 'database snapshot' 或 'database snapshot character' 進行複寫。|  
|功能|DBCC CHECKDB<br /><br /> DBCC CHECKTABLE|DBCC CHECKDB 會略過資料庫中記憶體最佳化資料表。<br /><br /> DBCC CHECKTABLE 無法檢查記憶體最佳化資料表。|  
  
## <a name="memory-optimized-tables"></a>記憶體最佳化的資料表  
 下表列出可能出現於涉及記憶體最佳化資料表之錯誤訊息文字中的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 功能和關鍵字，以及解決錯誤的更正動作。  
  
|類型|名稱|解決方法|  
|----------|----------|----------------|  
|功能|開啟|記憶體最佳化資料表不可放置在檔案群組或分割區配置上。 請從 `CREATE TABLE` 陳述式中移除 ON 子句。|  
|資料類型|*資料類型名稱*|不支援所指的資料類型。 請用其中一種支援的資料類型取代該類型。 如需詳細資訊，請參閱[支援的資料類型](supported-data-types-for-in-memory-oltp.md)。|  
|功能|計算資料行|記憶體最佳化資料表中不支援計算資料行。 請從 `CREATE TABLE` 陳述式中移除計算資料行。|  
|功能|複寫|記憶體最佳化資料表不支援複寫。|  
|功能|FILESTREAM|FILESTREAM 儲存體不是記憶體最佳化資料表支援的資料行。 請從資料行定義中移除 `FILESTREAM` 關鍵字。|  
|功能|SPARSE|記憶體最佳化資料表的資料行不可定義為 SPARSE。 請從資料行定義中移除 `SPARSE` 關鍵字。|  
|功能|ROWGUIDCOL|ROWGUIDCOL 選項不是記憶體最佳化資料表支援的資料行。 請從資料行定義中移除 `ROWGUIDCOL` 關鍵字。|  
|功能|FOREIGN KEY|記憶體最佳化資料表中不支援 FOREIGN KEY 條件約束。 請從資料表定義中移除條件約束。<br /><br /> 如需如何減輕條件約束支援的相關資訊，請參閱[遷移 Check 和 Foreign Key 條件約束](../../database-engine/migrating-check-and-foreign-key-constraints.md)。|  
|功能|CHECK|記憶體最佳化資料表中不支援 CHECK 條件約束。 請從資料表定義中移除條件約束。<br /><br /> 如需如何減輕條件約束支援的相關資訊，請參閱[遷移 Check 和 Foreign Key 條件約束](../../database-engine/migrating-check-and-foreign-key-constraints.md)。|  
|功能|UNIQUE|記憶體最佳化資料表不支援 UNIQUE 條件約束。 請從資料表定義中移除條件約束。<br /><br /> 如需如何減輕條件約束支援的相關資訊，請參閱[遷移 Check 和 Foreign Key 條件約束](../../database-engine/migrating-check-and-foreign-key-constraints.md)。|  
|功能|COLUMNSTORE|記憶體最佳化資料表中不支援 COLUMNSTORE 索引。 請改為指定 NONCLUSTERED 或 NONCLUSTERED HASH 索引。|  
|功能|叢集索引|指定非叢集索引。 對於主索引鍵索引，請務必指定 `PRIMARY KEY NONCLUSTERED [HASH]`。|  
|功能|非 1252 字碼頁|記憶體最佳化資料表中資料類型為 `char` 和 `varchar` 的資料行必須使用字碼頁 1252。 請使用 n(var)char 而不要 (var)char，或是使用字碼頁為 1252 的定序 (例如，Latin1_General_BIN2)。 如需詳細資訊，請參閱 [Collations and Code Pages](../../database-engine/collations-and-code-pages.md)。|  
|功能|交易內的 DDL|記憶體最佳化資料表和原生編譯預存程序無法在使用者交易內容中建立或卸除。 請不要啟動交易，並確認工作階段設定 IMPLICIT_TRANSACTIONS 為 OFF，再執行 CREATE 或 DROP 陳述式。|  
|功能|DDL 觸發程序|如果該 DDL 作業有伺服器或資料庫觸發程序，則無法建立或卸除記憶體最佳化資料表和原生編譯預存程序。 請移除 CREATE/DROP TABLE 和 CREATE/DROP PROCEDURE 上的伺服器和資料庫觸發程序。|  
|功能|EVENT NOTIFICATION|如果該 DDL 作業有伺服器或資料庫事件通知，便無法建立或卸除記憶體最佳化資料表和原生編譯的預存程序。 移除 CREATE TABLE 或 DROP TABLE 與 CREATE PROCEDURE 或 DROP PROCEDURE 上的伺服器和資料庫事件通知。|  
|功能|FileTable|記憶體最佳化資料表不可建立為檔案資料表。 請從 `AS FileTable` 陳述式中移除 `CREATE TABLE` 引數|  
|作業|主索引鍵資料行的更新。|記憶體最佳化資料表中的主索引鍵資料行和資料類型無法更新。 如果主索引鍵需要更新，請刪除舊資料列，並插入包含更新之主索引鍵的新資料列。|  
|作業|CREATE INDEX|記憶體最佳化資料表上的索引必須採用內嵌於 `CREATE TABLE` 陳述式的方式指定。 若要將索引加入至記憶體最佳化資料表，請卸除再重新建立資料表，包括新的索引指定。|  
|作業|ALTER TABLE|不支援修改記憶體最佳化資料表。 請卸除資料表，並使用更新的資料表定義重新建立資料表。|  
|作業|CREATE FULLTEXT INDEX|記憶體最佳化資料表中不支援全文檢索索引。|  
|作業|結構描述變更|記憶體最佳化資料表和原生編譯預存程序不支援結構描述變更，例如 `sp_rename`。<br /><br /> 嘗試變更結構描述 (例如重新命名資料) 將會產生錯誤 12320。記憶體最佳化資料表不支援需要變更結構描述版本 (例如重新命名) 的作業。<br /><br /> 若要變更結構描述，請卸除資料表或程序，然後使用更新的定義重新建立資料表或程序。|  
|作業|CREATE TRIGGER|記憶體最佳化資料表上不支援觸發程序。|  
|作業|TRUNCATE TABLE|記憶體最佳化資料表不支援 TRUNCATE 作業。 若要移除資料表中的所有資料列，請使用`DELETE FROM`*資料表*刪除所有資料列，或卸載並重新建立資料表。|  
|作業|ALTER AUTHORIZATION|不支援變更現有記憶體最佳化資料表或原生編譯預存程序的擁有者。 請卸除後再重新建立資料表或程序，以變更擁有權。|  
|作業|ALTER SCHEMA|不支援變更現有記憶體最佳化資料表或原生編譯之預存程序的結構描述。 必須先卸除再重新建立資料表或程序，才能變更結構描述。|  
|作業|DBCC CHECKTABLE|記憶體最佳化資料表中不支援 DBCC CHECKTABLE。|  
|功能|ANSI_PADDING OFF|建立記憶體最佳化資料表或原生編譯預存程序時，工作階段選項 `ANSI_PADDING` 必須為 ON。 執行 CREATE 陳述式之前，請先執行 `SET ANSI_PADDING ON`。|  
|選項|DATA_COMPRESSION|記憶體最佳化資料表中不支援資料壓縮。 請從資料表定義中移除此選項。|  
|功能|DTC|記憶體最佳化資料表和原生編譯預存程序無法從分散式交易中存取。 請改用 SQL 交易。|  
|功能|Multiple Active Result Set (MARS)|記憶體最佳化資料表不支援 Multiple Active Result Sets (MARS)。 此錯誤也可能表示使用連結的伺服器。 連結的伺服器可以使用 MARS。 記憶體最佳化資料表中不支援連結的伺服器。 請改為直接連接至裝載記憶體最佳化資料表的伺服器和資料庫。|  
|作業|以記憶體最佳化資料表做為 MERGE 的目標|記憶體最佳化資料表不可以是 `MERGE` 作業的目標。 請改用 `INSERT`、`UPDATE` 或 `DELETE` 陳述式。|  
  
## <a name="indexes-on-memory-optimized-tables"></a>記憶體最佳化資料表上的索引  
 下表列出可能出現於涉及記憶體最佳化資料表上某個索引錯誤之訊息文字中的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 功能和關鍵字，以及解決錯誤的更正動作。  
  
|類型|名稱|解決方法|  
|----------|----------|----------------|  
|功能|已篩選的索引|記憶體最佳化資料表中不支援篩選的索引。 請從索引指定中省略 `WHERE` 子句。|  
|功能|UNIQUE|記憶體最佳化資料表中不支援唯一索引。 請從索引指定中移除引數 `UNIQUE`。|  
|功能|可為 null 的資料行|記憶體最佳化資料表上索引之索引鍵中的所有資料行都必須指定為 `NOT NULL`。 請在索引鍵中的所有資料行包含 `NOT NULL` 條件約束。|  
|功能|非 bin2 定序|記憶體最佳化索引之索引鍵中的所有字元資料行都必須使用 BIN2 定序宣告。 請使用 `COLLATE` 子句設定資料行定義中的定序。 如需詳細資訊，請參閱 [Collations and Code Pages](../../database-engine/collations-and-code-pages.md)。|  
|功能|包含的資料行|記憶體最佳化資料表並不需要指定內含資料行。 記憶體最佳化資料表內所有的資料行都是隱含包含在每一個記憶體最佳化的索引中。|  
|作業|ALTER INDEX|不支援修改記憶體最佳化資料表上的索引。 請改為卸除資料表，並使用更新的索引指定重新建立資料表。|  
|作業|DROP INDEX|不支援卸除記憶體最佳化資料表上的索引。 請改為卸除資料表，並使用所需的索引重新建立資料表。|  
|索引選項|*索引選項*|記憶體最佳化資料表中的索引不支援指出的索引選項。 請從索引指定中移除該選項。|  
  
## <a name="nonclustered-hash-indexes"></a>非叢集雜湊索引  
 下表列出可能出現於涉及非叢集雜湊索引之錯誤訊息文字中的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 功能和關鍵字，以及解決錯誤的更正動作。  
  
|類型|名稱|解決方法|  
|----------|----------|----------------|  
|選項|ASC/DESC|非叢集雜湊索引不會排序。 請從索引鍵指定中移除關鍵字 `ASC` 和 `DESC`。|  
  
## <a name="natively-compiled-stored-procedures"></a>原生編譯的預存程序  
 下表列出可能出現於涉及原生編譯預存程序之錯誤訊息文字中的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 功能和關鍵字，以及解決錯誤的更正動作。  
  
|類型|功能|解決方法|  
|----------|-------------|----------------|  
|功能|內嵌資料表變數|資料表類型無法以內嵌於變數宣告中的方式宣告。 資料表類型必須使用 `CREATE TYPE` 陳述式明確宣告。|  
|功能|資料指標|原生編譯預存程序上或內部不支援資料指標。<br /><br /> -從用戶端執行程式時，請使用 RPC，而不是資料指標 API。 使用 ODBC 時，避免 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式 `EXECUTE`，請改為直接指定程序的名稱。<br /><br /> -從[!INCLUDE[tsql](../../includes/tsql-md.md)]批次或另一個預存程式執行程式時，請避免將資料指標與原生編譯預存程式搭配使用。<br /><br /> -建立原生編譯的預存程式時，不要使用資料指標，而是使用以集合為`WHILE`基礎的邏輯或迴圈。|  
|功能|非常數參數的預設值|在原生編譯預存程序上使用具有參數的預設值時，值必須為常數。 請從參數宣告中移除任何萬用字元。|  
|功能|EXTERNAL|無法對 CLR 預存程序執行原生編譯。 從 CREATE PROCEDURE 陳述式中移除 AS EXTERNAL 子句或 NATIVE_COMPILATION 選項。|  
|功能|編號的預存程序|原生編譯預存程序不可編號。 請從`;` ** `CREATE PROCEDURE`語句中移除該數位。|  
|功能|多資料列插入 .。。VALUES 語句|無法使用相同的 `INSERT` 陳述式在原生編譯預存程序中插入多個資料列。 請為每個資料列建立 `INSERT` 陳述式。|  
|功能|通用資料表運算式 (CTE)|原生編譯預存程序中不支援通用資料表運算式 (CTE)。 重寫查詢。|  
|功能|子查詢|不支援子查詢 (另一個查詢中的巢狀查詢)。 重寫查詢。|  
|功能|COMPUTE|不支援 `COMPUTE` 子句。 請從查詢中將它移除。|  
|功能|SELECT INTO|不支援 `INTO` 子句與 `SELECT` 陳述式一起使用。 將查詢重寫`INSERT INTO`為*Table*`SELECT`。|  
|功能|OUTPUT|不支援 `OUTPUT` 子句。 請從查詢中將它移除。|  
|功能|不完整的插入資料行清單|在 `INSERT` 陳述式中，必須為資料表中的所有資料行指定值。|  
|函式|*函數*|原生編譯預存程序中不支援內建函數。 請從預存程序中移除函數。 如需所支援內建函數的詳細資訊，請參閱原生[編譯的預存程式](../in-memory-oltp/natively-compiled-stored-procedures.md)。|  
|功能|CASE|原生編譯預存程序內部的查詢中不支援 `CASE` 陳述式。 請為每個案例建立查詢。 如需詳細資訊，請參閱[執行 CASE 語句](implementing-a-case-expression-in-a-natively-compiled-stored-procedure.md)。|  
|功能|使用者定義函數|使用者定義函數不可在原生編譯預存程序中使用。 請從程序定義中移除函數的參考。|  
|功能|使用者定義彙總|使用者定義彙總函式不可在原生編譯預存程序中使用。 請從程序中移除函式的參考。|  
|功能|瀏覽模式中繼資料|原生編譯預存程序不支援瀏覽模式中繼資料。 請確定工作階段選項 `NO_BROWSETABLE` 設為 OFF。|  
|功能|FROM 子句中的 DELETE|原生編譯預存程序中具有資料表來源的 `FROM` 陳述式不支援 `DELETE` 子句。<br /><br /> 支援搭配使用 `DELETE` 和 `FROM` 子句來指定要刪除的資料表來源。|  
|功能|FROM 子句中的 UPDATE|原生編譯預存程序中的 `FROM` 陳述式不支援 `UPDATE` 子句。|  
|功能|暫存程序|不可對暫存預存程序進行原生編譯。 請建立永久的原生編譯預存程序，或暫存的解譯 [!INCLUDE[tsql](../../includes/tsql-md.md)] 預存程序。|  
|隔離等級|READ UNCOMMITTED|原生編譯預存程序中不支援隔離等級 READ UNCOMMITTED。 請使用支援的隔離等級，例如 SNAPSHOT。|  
|隔離等級|READ COMMITTED|原生編譯預存程序中不支援隔離等級 READ UNCOMMITTED。 請使用支援的隔離等級，例如 SNAPSHOT。|  
|功能|暫存資料表|tempdb 中的資料表不可在原生編譯預存程序中使用。 請改用 DURABILITY=SCHEMA_ONLY 的資料表變數或記憶體最佳化資料表。|  
|功能|MARS|原生編譯預存程序中不支援 Multiple Active Result Sets (MARS)。 此錯誤也可能表示使用連結的伺服器。 連結的伺服器可以使用 MARS。 原生編譯預存程序中不支援連結的伺服器。 請改為直接連接至裝載原生編譯預存程序的伺服器和資料庫。|  
|功能|DTC|記憶體最佳化資料表和原生編譯預存程序無法從分散式交易中存取。 請改用 SQL 交易。|  
|功能|非 bin2 定序|對原生編譯預存程序中的字元字串執行的比較、排序和其他作業需要使用 BIN2 定序。 請使用 COLLATE 子句，或使用具有適當定序的資料行和變數。 如需詳細資訊，請參閱 [Collations and Code Pages](../../database-engine/collations-and-code-pages.md)。|  
|功能|使用 SC 定序截斷字元字串。|具有 `_SC` 定序的字元字串使用 UTF-16 編碼。 請將 n(var)char 值轉換成具有包含截斷之縮短長度的 n(var)char 值。 原生編譯預存程序中的 UTF-16 值不支援這種做法。 請避免截斷 UTF-16 字串。|  
|功能|EXECUTE WITH RECOMPILE|原生編譯預存程序中不支援 `WITH RECOMPILE` 選項。|  
|功能|SC 定序中具有引數的 LEN 和 SUBSTRING|具有 _SC 定序的字元字串會使用 UTF-16 編碼。 在原生編譯之預存程序內使用內建函式 LEN 和 SUBSTRING 時，不支援 UTF-16 編碼。 使用不同的定序，或是避免使用這些函式。|  
|功能|從專用管理員連接執行。|原生編譯預存程序無法從專用管理員連接 (DAC) 執行。 請改用正常連接。|  
|作業|ALTER PROCEDURE|原生編譯預存程序不可修改。 若要變更程序定義，請卸除後再重新建立預存程序。|  
|作業|儲存點|原生編譯預存程序不可從擁有使用中儲存點的交易中叫用。 請從交易中移除儲存點。|  
|作業|ALTER AUTHORIZATION|不支援變更現有記憶體最佳化資料表或原生編譯預存程序的擁有者。 請卸除後再重新建立資料表或程序，以變更擁有權。|  
|運算子|OPENROWSET|不支援此運算子。 請從原生編譯預存程序中移除 `OPENROWSET`。|  
|運算子|OPENQUERY|不支援此運算子。 請從原生編譯預存程序中移除 `OPENQUERY`。|  
|運算子|OPENDATASOURCE|不支援此運算子。 請從原生編譯預存程序中移除 `OPENDATASOURCE`。|  
|運算子|OPENXML|不支援此運算子。 請從原生編譯預存程序中移除 `OPENXML`。|  
|運算子|CONTAINSTABLE|不支援此運算子。 請從原生編譯預存程序中移除 `CONTAINSTABLE`。|  
|運算子|FREETEXTTABLE|不支援此運算子。 請從原生編譯預存程序中移除 `FREETEXTTABLE`。|  
|功能|資料表值函式|資料表值函式不可從原生編譯預存程序參考。 此限制的可行因應措施是將資料表值函式內的邏輯加入程序主體中。|  
|運算子|CHANGETABLE|不支援此運算子。 請從原生編譯預存程序中移除 `CHANGETABLE`。|  
|運算子|GOTO|不支援此運算子。 請使用其他程序性建構，例如 WHILE。|  
|運算子|EXECUTE、INSERT EXEC|不支援巢狀原生編譯預存程序。 所需的作業可以用內嵌方式指定為預存程序定義的一部分。|  
|運算子|OFFSET|不支援此運算子。 請從原生編譯預存程序中移除 `OFFSET`。|  
|運算子|UNION|不支援此運算子。 請從原生編譯預存程序中移除 `UNION`。 您可以使用資料表變數將數個結果集結合到程單一結果集內。|  
|運算子|INTERSECT|不支援此運算子。 請從原生編譯預存程序中移除 `INTERSECT`。 在某些情況下，可以使用 INNER JOIN 獲得相同結果。|  
|運算子|EXCEPT|不支援此運算子。 請從原生編譯預存程序中移除 `EXCEPT`。|  
|運算子|OUTER JOIN|不支援此運算子。 請從原生編譯預存程序中移除 `OUTER JOIN`。 如需詳細資訊，請參閱[執行外部聯結](implementing-an-outer-join.md)。|  
|運算子|APPLY|不支援此運算子。 請從原生編譯預存程序中移除 `APPLY`。|  
|運算子|PIVOT|不支援此運算子。 請從原生編譯預存程序中移除 `PIVOT`。|  
|運算子|UNPIVOT|不支援此運算子。 請從原生編譯預存程序中移除 `UNPIVOT`。|  
|運算子|OR、IN|原生編譯之預存程序中查詢內的 WHERE 子句不支援分離 (OR、IN)。 請為每個案例建立查詢。|  
|運算子|CONTAINS|不支援此運算子。 請從原生編譯預存程序中移除 `CONTAINS`。|  
|運算子|FREETEXT|不支援此運算子。 請從原生編譯預存程序中移除 `FREETEXT`。|  
|運算子|NOT|不支援此運算子。 請從原生編譯預存程序中移除 `NOT`。 在某些情況下可以將 `NOT` 取代為不相等。 例如，`NOT a=b` 可以取代為 `a!=b`。|  
|運算子|TSEQUAL|不支援此運算子。 請從原生編譯預存程序中移除 `TSEQUAL`。|  
|運算子|LIKE|不支援此運算子。 請從原生編譯預存程序中移除 `LIKE`。|  
|運算子|NEXT VALUE FOR|原生編譯預存程序內可以參考順序。 請使用解譯的 [!INCLUDE[tsql](../../includes/tsql-md.md)]取得值，並將它傳遞至原生編譯預存程序。 如需詳細資訊，請參閱 [在記憶體最佳化資料表中實作 IDENTITY](implementing-identity-in-a-memory-optimized-table.md)。|  
|Set 選項|*件*|原生編譯預存程序內的 SET 選項不可變更。 某些選項可以透過 BEGIN ATOMIC 陳述式設定。 如需詳細資訊，請參閱＜ [Natively Compiled Stored Procedures](../in-memory-oltp/natively-compiled-stored-procedures.md)＞中的＜Atonic 區塊＞一節。|  
|運算元|TABLESAMPLE|不支援此運算子。 請從原生編譯預存程序中移除 `TABLESAMPLE`。|  
|選項|RECOMPILE|原生編譯預存程序是在建立時編譯。 若要重新編譯原生編譯預存程序，請將它卸除再重新建立。 請從程序定義中移除 `RECOMPILE`。|  
|選項|ENCRYPTION|不支援這個選項。 請從程序定義中移除 `ENCRYPTION`。|  
|選項|FOR REPLICATION|不可針對複寫建立原生編譯預存程序。 已從程序定義中移除 `FOR REPLICATION`。|  
|選項|FOR XML|不支援這個選項。 請從原生編譯預存程序中移除 `FOR XML`。|  
|選項|FOR BROWSE|不支援這個選項。 請從原生編譯預存程序中移除 `FOR BROWSE`。|  
|聯結提示|HASH、MERGE|原生編譯預存程序僅支援巢狀迴圈聯結。 不支援雜湊和合併聯結。 請移除聯結提示。|  
|查詢提示|*查詢提示*|此查詢提示不在原生編譯預存程序內。 如需支援的查詢提示，請參閱[查詢提示 &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-query)。|  
|選項|DISTINCT|不支援這個選項。 請從原生編譯預存程序的查詢中移除 `DISTINCT`。|  
|選項|PERCENT|
  `TOP` 子句不支援此選項。 請從原生編譯預存程序的查詢中移除 `PERCENT`。|  
|選項|WITH TIES|
  `TOP` 子句不支援此選項。 請從原生編譯預存程序的查詢中移除 `WITH TIES`。|  
|彙總函式|*彙總函式*|不支援此子句。 如需原生編譯預存程序中彙總函式的詳細資訊，請參閱＜ [Natively Compiled Stored Procedures](../in-memory-oltp/natively-compiled-stored-procedures.md)＞。|  
|排名函數|*次序函數*|原生編譯預存程序中不支援排名函數。 請從程序定義中將它們移除。|  
|函式|*函數*|不支援此函數。 請從原生編譯預存程序中將它移除。|  
|引數|*陳述式*|不支援此陳述式。 請從原生編譯預存程序中將它移除。|  
|功能|MIN 和 MAX 可與二進位和字元字串並用|彙總函式 `MIN` 和 `MAX` 不可用於原生編譯預存程序內的字元和二進位字串值。|  
|功能|未使用彙總函式的 GROUP BY|在原生編譯的預存程序中，當查詢包含 `GROUP BY` 子句時，查詢也必須在 SELECT 或 HAVING 子句中使用彙總函式。 請將彙總函式加入至查詢。|  
|功能|GROUP BY ALL|在原生編譯的預存程序中，ALL 不得與 GROUP BY 子句並用。 從 GROUP BY 子句中移除 ALL。|  
|功能|GROUP BY ()|無法使用空白清單做為群組依據。 請移除 GROUP BY 子句，或在群組清單中加入資料行。|  
|功能|ROLLUP|
  `ROLLUP` 無法與原生編譯預存程序中的 `GROUP BY` 子句一起使用。 請從程序定義中移除 `ROLLUP`。|  
|功能|CUBE|
  `CUBE` 無法與原生編譯預存程序中的 `GROUP BY` 子句一起使用。 請從程序定義中移除 `CUBE`。|  
|功能|GROUPING SETS|
  `GROUPING SETS` 無法與原生編譯預存程序中的 `GROUP BY` 子句一起使用。 請從程序定義中移除 `GROUPING SETS`。|  
|功能|BEGIN TRANSACTION、COMMIT TRANSACTION 與 ROLLBACK TRANSACTION。|使用 ATOMIC 區塊控制交易和錯誤處理。 如需詳細資訊，請參閱 [Atomic Blocks](atomic-blocks-in-native-procedures.md)。|  
|功能|內嵌資料表變數宣告。|資料表變數必須明確參考定義的記憶體最佳化資料表類型。 您應該建立記憶體最佳化資料表的類型，並使用該類型宣告變數，而不要指定內嵌類型。|  
|功能|sp_recompile|不支援重新編譯原生編譯的預存程序。 卸除再重新建立程序。|  
|功能|EXECUTE AS CALLER|
  `EXECUTE AS` 為必要子句。 但 `EXECUTE AS CALLER` 不受支援。 使用`EXECUTE AS OWNER`、 `EXECUTE AS`*使用者*或`EXECUTE AS SELF`。|  
|功能|磁碟型資料表|磁碟型資料表無法從原生編譯的預存程序中存取。 從原生編譯的預存程序移除磁碟型資料表類型的參考。 或是將磁碟型資料表移轉至經過最佳化的記憶體。|  
|功能|檢視|檢視無法從原生編譯的預存程序中存取。 請參考基底資料表，而不要使用檢視。|  
|功能|資料表值函式|資料表值函式無法從原生編譯的預存程序中存取。 從原生編譯的預存程序中移除資料表值函式的參考。|  
  
## <a name="transactions-that-access-memory-optimized-tables"></a>存取記憶體最佳化資料表的交易  
 下表列出可能出現於涉及存取記憶體最佳化資料表之交易錯誤的訊息文字中的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 功能和關鍵字，以及解決錯誤的更正動作。  
  
|類型|名稱|解決方法|  
|----------|----------|----------------|  
|功能|儲存點|不支援在存取記憶體最佳化資料表的交易中建立明確儲存點。|  
|功能|繫結式交易|繫結工作階段無法參與存取記憶體最佳化資料表的交易。 在執行程序之前，請不要繫結工作階段。|  
|功能|DTC|存取記憶體最佳化資料表的交易不可以是分散式交易。|  
  
## <a name="see-also"></a>另請參閱  
 [移轉至 In-Memory OLTP](migrating-to-in-memory-oltp.md)  
  
  
