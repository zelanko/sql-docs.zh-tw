---
title: "已更新 - 關聯式資料庫文件 | Microsoft Docs"
description: "針對關聯式資料庫，顯示文件最新變更之已更新內容的程式碼片段。"
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.prod_service: sql-non-specified
ms.component: relational-databases
ms.date: 02/03/2018
ms.openlocfilehash: 38f9ee55137c54adddb07fbe9f3b74dd43d51a3a
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="new-and-recently-updated-relational-databases-docs"></a>新的與最近更新的文章： 關聯式資料庫文件



Microsoft 幾乎每天都會在其 [Docs.Microsoft.com](http://docs.microsoft.com/) 文件網站上更新一些現有文章。 本文會顯示最近更新文章的摘錄。 可能也會列出新文章的連結。

本文是透過定期重新執行的程式所產生。 摘錄中偶爾會出現示不完整的格式，或顯示為來自來源文章的 Markdown。 影像永遠不會顯示在這裡。

新的更新會報告下列日期範圍和主旨：



- 更新日期範圍：&nbsp;**2017 年 12 月 3 日**&nbsp;-至-&nbsp;**2018 年 2 月 3 日**
- *主旨區域：* &nbsp; **關聯式資料庫**。




&nbsp;

## <a name="new-articles-created-recently"></a>最近建立的新文章

下列連結會跳至最近新增的新文章。


1. [將 JSON 文件儲存在 SQL Server 或 SQL Database](json/store-json-documents-in-sql-tables.md)
2. [SQL 漏洞評量](security/sql-vulnerability-assessment.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>更新文章與摘要

本節會顯示從最近發生大規模更新的文章所收集的更新摘錄。

此處顯示的摘錄不同於其適當語意內容。 此外，有時摘錄也與實際文件四周的重要 Markdown 語法不同。 因此，這些摘錄僅適用於一般指導方針。 摘錄只能讓您知道您感興趣的項目，是否值得花時間按一下並瀏覽實際文章。

由於這些和其他原因，請勿從這些摘錄中複製程式碼，而且不要將任何文字摘錄視為確切事實。 請改瀏覽實際文章。





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>最近更新文章的壓縮清單

此壓縮清單提供＜摘要＞一節中所有更新文章的連結。

1. [資料庫檔案初始化](#TitleNum_1)
2. [tempdb 資料庫](#TitleNum_2)
3. [SQL Server 中的 JSON 資料](#TitleNum_3)
4. [第 1 課：連接到資料庫引擎](#TitleNum_4)
5. [管理交易記錄檔的大小](#TitleNum_5)
6. [bcp_bind](#TitleNum_6)
7. [SQL Server 索引設計指南](#TitleNum_7)
8. [sp_execute_external_script (Transact-SQL)](#TitleNum_8)
9. [建立主索引鍵](#TitleNum_9)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-database-file-initializationdatabasesdatabase-instant-file-initializationmd"></a>1.&nbsp; [資料庫檔案初始化](databases/database-instant-file-initialization.md)

*更新日期：2018 年 1 月 23 日* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([下一個](#TitleNum_2))

<!-- Source markdown line 81.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 c5f2aa53a8b43d4c43e0602cf945cb7c7028a27d 04c261c6588af1f53cda2fce3e9a86167c50b686  (PR=4702  ,  Filename=database-instant-file-initialization.md  ,  Dirpath=docs\relational-databases\databases\  ,  MergeCommitSha40=3206a31870f8febab7d1718fa59fe0590d4d45db) -->



```
Database Instant File Initialization: disabled. For security and performance considerations see the topic 'Database Instant File Initialization' in SQL Server Books Online. This is an informational message only. No user action is required.
```

**適用於：**SQL Server (從 SQL Server 2012 SP4、SQL Server 2014 SP2 和 SQL Server 2016 開始，到 SQL Server 2017)

**安全性考量**

在使用檔案立即初始化 (IFI) 時，由於刪除的磁碟內容只有在新資料寫入檔案時才會被覆寫；因此，直到其他資料寫入資料檔特定區域之前，未經授權的主體可能得以存取刪除的內容。 當資料庫檔案附加到 SQL Server 的執行個體時，檔案上的判別存取控制清單 (DACL) 可降低上述資訊洩漏風險。 此 DACL 只允許 SQL Server 服務帳戶和本機系統管理員存取檔案。 但是，當檔案卸離後，不具備 SE\_MANAGE\_VOLUME_NAME 的使用者或服務便能存取該檔案。 在備份資料庫時，也會有類似的需要考量之處：如果備份檔案未使用適當的 DACL 保護，未經授權的使用者或服務便可存取刪除的內容。

另一個考量是當檔案使用 IFI 增長時，SQL Server 系統管理員可能會存取原始頁面內容，並查看先前刪除的內容。

如果資料庫檔案裝載在存放區域網路上，則存放區域網路也可能會一律以預先初始化方式顯示新頁面，因此讓作業系統重新初始化頁面可能是不必要的額外負荷。



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-tempdb-databasedatabasestempdb-databasemd"></a>2. &nbsp; [tempdb 資料庫](databases/tempdb-database.md)

*更新日期：2018 年 1 月 17 日* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([上一個](#TitleNum_1) | [下一個](#TitleNum_3))

<!-- Source markdown line 100.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 337555ea28f4c3fdd6b78f1bfb4d62607a6bf92d 3257c92d6e2a88968fc44e5f6262c02cd0624635  (PR=0  ,  Filename=tempdb-database.md  ,  Dirpath=docs\relational-databases\databases\  ,  MergeCommitSha40=45e6082acc29ba306525e7c08d2c22cc2b86eec3) -->



 如需這些資料庫選項的描述，請參閱 [ALTER DATABASE SET 選項 (Transact-SQL)](databases/../../t-sql/statements/alter-database-transact-sql-set-options.md)。

**SQL Database 中的 tempdb 資料庫**


|SLO|Tempdb 資料檔案大小上限 (MB)|Tempdb資料檔案數|Tempdb 資料檔案大小上限 (MB)|
|---|---:|---:|---:|
|[基本]|14,225|@shouldalert|14,225|
|S0|14,225|@shouldalert|14,225|
|S1|14,225|@shouldalert|14,225|
|S2|14,225| @shouldalert|14,225|
|S3|32,768|@shouldalert|32,768|
|S4|32,768|2|65,536|
|S6|32,768|3|98,304|
|S7|32,768|6|196,608|
|S9|32,768|12|393,216|
|S12|32,768|12|393,216|
|P1|32,768|12|393,216|
|P2|32,768|12|393,216|
|P4|32,768|12|393,216|
|P6|32,768|12|393,216|
|P11|32,768|12|393,216|
|P15|32,768|12|393,216|
|Premium 彈性集區 (所有 DTU 設定)|14,225|12|170,700|
|標準彈性集區 (所有 DTU 設定)|14,225|12|170,700|
|基本彈性集區 (所有 DTU 設定)|14,225|12|170,700|
||||




&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-json-data-in-sql-serverjsonjson-data-sql-servermd"></a>3.&nbsp; [SQL Server 中的 JSON 資料](json/json-data-sql-server.md)

更新日期：2018 年 2 月 1 日 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([上一個](#TitleNum_2) | [下一個](#TitleNum_4))

<!-- Source markdown line 233.  ms.author= "douglasl".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 62dd9c68d8cb72d6bf51b941a0731224514f0a7f 19e276637a463b412f2c29a84f9fb7d0b0f5fcc5  (PR=4783  ,  Filename=json-data-sql-server.md  ,  Dirpath=docs\relational-databases\json\  ,  MergeCommitSha40=73f18ae24a9a48234bf997ee9a2ef441bc4918b9) -->



-   [將 GeoJSON 資料載入 SQL Server 2016](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/01/05/loading-geojson-data-into-sql-server/)

**使用 SQL 查詢分析 JSON 資料**

如果您基於報表用途而必須篩選或彙總 JSON 資料，可以使用 **OPENJSON**，將 JSON 轉換為關聯式格式。 然後使用標準 Transact-SQL 和內建函式來準備報表。

```
SELECT Tab.Id, SalesOrderJsonData.Customer, SalesOrderJsonData.Date
FROM   SalesOrderRecord AS Tab
          CROSS APPLY
     OPENJSON (Tab.json, N'$.Orders.OrdersArray')
           WITH (
              Number   varchar(200) N'$.Order.Number',
              Date     datetime     N'$.Order.Date',
              Customer varchar(200) N'$.AccountNumber',
              Quantity int          N'$.Item.Quantity'
           )
  AS SalesOrderJsonData
WHERE JSON_VALUE(Tab.json, '$.Status') = N'Closed'
ORDER BY JSON_VALUE(Tab.json, '$.Group'), Tab.DateModified
```



&nbsp;

&nbsp;

---

<a name="TitleNum_4"/>

### <a name="4-nbsp-lesson-1-connecting-to-the-database-enginelesson-1-connecting-to-the-database-enginemd"></a>4.&nbsp; [第 1 課：連線到資料庫引擎](lesson-1-connecting-to-the-database-engine.md)

更新日期：2017 年 12 月 13 日 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([上一個](#TitleNum_3) | [下一個](#TitleNum_5))

<!-- Source markdown line 79.  ms.author= "rickbyh".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 3c070935895450fd2ea054e2be9e1c48f7dc2b6c 0c386e3d47fb7f8f1e63b9301f0cafec2bc88ab0  (PR=4282  ,  Filename=lesson-1-connecting-to-the-database-engine.md  ,  Dirpath=docs\relational-databases\  ,  MergeCommitSha40=6e016a4ffd28b09456008f40ff88aef3d911c7ba) -->



2.  選取 [Database Engine]。

    ![object-explorer](../relational-databases/media/object-explorer.png)

3.  在 [伺服器名稱] 方塊中，鍵入資料庫引擎執行個體的名稱。 若為 SQL Server 的預設執行個體，則伺服器名稱為電腦名稱。 若為 SQL Server 的具名執行個體，則伺服器名稱為 <電腦名稱>****\\<執行個體名稱>****，例如 **ACCTG_SRVR\SQLEXPRESS**。 下列螢幕擷取畫面顯示連線至名為 'PracticeComputer' 之電腦上的預設 (未命名) SQL Server 執行個體。 登入 Windows 的使用者是來自 Contoso 網域的 Mary。 使用 Windows 驗證時，即無法變更使用者名稱。

    ![connect-to-server](../relational-databases/media/connect-to-server.png)

4.  按一下 **[連接]**。

> [!NOTE]
> 本教學課程假設您不熟悉 SQL Server 而且沒有特殊連線問題。 這應該適用於大部分的人，並且保持本教學課程的簡單性。 如需詳細疑難排解步驟，請參閱 [針對 SQL Server Database Engine 的連接進行疑難排解](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)。

**<a name="additional"></a>授權其他連線**

以系統管理員的身分連線至 SQL Server 後，您的首要工作之一就是授權其他使用者連線。 您可以建立登入，並授權該登入以使用者身分存取資料庫，來達成此目的。 而登入可以是使用 Windows 認證的 Windows 驗證登入，或是 SQL Server 驗證登入，這種登入會將驗證資訊儲存在 SQL Server 中，而且與 Windows 認證無關。 可能的話，請盡量使用 Windows 驗證。



&nbsp;

&nbsp;

---

<a name="TitleNum_5"/>

### <a name="5-nbsp-manage-the-size-of-the-transaction-log-filelogsmanage-the-size-of-the-transaction-log-filemd"></a>5.&nbsp; [管理交易記錄檔的大小](logs/manage-the-size-of-the-transaction-log-file.md)

更新日期：2018 年 1 月 17 日 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([上一個](#TitleNum_4) | [下一個](#TitleNum_6))

<!-- Source markdown line 105.  ms.author= "jhubbard".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 5847b31cf8f6003a380f0c8aaa289efdc55be678 84e45320d81db218cde17fbf8b9668a9ac3805a7  (PR=0  ,  Filename=manage-the-size-of-the-transaction-log-file.md  ,  Dirpath=docs\relational-databases\logs\  ,  MergeCommitSha40=45e6082acc29ba306525e7c08d2c22cc2b86eec3) -->



-   小型的成長增量可能會產生太多小型 [VLF](logs/../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)，且可能會降低效能。 若要判斷指定執行個體中所有資料庫的目前交易記錄大小的最佳 VLF 分佈，以及達到所需大小的必要成長增量，請參閱此[指令碼](http://github.com/Microsoft/tigertoolbox/tree/master/Fixing-VLFs)。

-   大型的成長增量可能會產生太少且大型的 [VLF](logs/../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)，且亦可能會降低效能。 若要判斷指定執行個體中所有資料庫的目前交易記錄大小的最佳 VLF 分佈，以及達到所需大小的必要成長增量，請參閱此[指令碼](http://github.com/Microsoft/tigertoolbox/tree/master/Fixing-VLFs)。

-   如果無法成長得夠快速以滿足查詢的需求，即使已啟用 autogrow，您還是可能收到訊息，指出交易記錄檔已滿。 如需變更成長增量的詳細資訊，請參閱 [ALTER DATABASE &#40;Transact-SQL&#41; 檔案及檔案群組選項](logs/../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)

-   在資料庫中具有多個記錄檔將無法以任何方式強化效能，因為交易記錄檔不像相同檔案群組中的資料檔案那樣使用[比例填滿](logs/../../relational-databases/pages-and-extents-architecture-guide.md#ProportionalFill)。

-   可以將記錄檔設定為自動壓縮。 不過並**不建議**如此，且 **auto_shrink** 資料庫屬性預設會設定為 FALSE。 如果 **auto_shrink** 設定為 TRUE，只有當超過 25% 的空間未使用時，自動壓縮才會減少檔案的大小。



&nbsp;

&nbsp;

---

<a name="TitleNum_6"/>

### <a name="6-nbsp-bcpbindnative-client-odbc-extensions-bulk-copy-functionsbcp-bindmd"></a>6. &nbsp; [bcp_bind](native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)

更新日期：2018 年 1 月 30 日 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([上一個](#TitleNum_5) | [下一個](#TitleNum_7))

<!-- Source markdown line 127.  ms.author= "genemi".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 d50791cef948ce8b3066438e317ab4d34d535258 e6f70559e7237cfc86dfc5746d218c08bec52af6  (PR=4762  ,  Filename=bcp-bind.md  ,  Dirpath=docs\relational-databases\native-client-odbc-extensions-bulk-copy-functions\  ,  MergeCommitSha40=60006e90d03fdb75b282bbc0dad3d40571bacacc) -->



 下表列出有效的列舉資料類型和對應的 ODBC C 資料類型。

|eDataType|C 類型|
|-----------------------|------------|
|SQLTEXT|char *|
|SQLNTEXT|wchar_t *|
|SQLCHARACTER|char *|
|SQLBIGCHAR|char *|
|SQLVARCHAR|char *|
|SQLBIGVARCHAR|char *|
|SQLNCHAR|wchar_t *|
|SQLNVARCHAR|wchar_t *|
|SQLBINARY|unsigned char *|
|SQLBIGBINARY|unsigned char *|
|SQLVARBINARY|unsigned char *|
|SQLBIGVARBINARY|unsigned char *|
|SQLBIT|char|
|SQLBITN|char|
|SQLINT1|char|
|SQLINT2|short int|
|SQLINT4|ssNoversion|
|SQLINT8|_int64|
|SQLINTN|*cbIndicator*<br /> 1: SQLINT1<br /> 2: SQLINT2<br /> 4: SQLINT4<br /> 8: SQLINT8|
|SQLFLT4|FLOAT|
|SQLFLT8|FLOAT|
|SQLFLTN|*cbIndicator*<br /> 4: SQLFLT4<br /> 8: SQLFLT8|
|SQLDECIMALN|SQL_NUMERIC_STRUCT|
|SQLNUMERICN|SQL_NUMERIC_STRUCT|
|SQLMONEY|DBMONEY|
|SQLMONEY4|DBMONEY4|
|SQLMONEYN|*cbIndicator*<br /> 4: SQLMONEY4<br /> 8: SQLMONEY|
|SQLTIMEN|SQL_SS_TIME2_STRUCT|
|SQLDATEN|SQL_DATE_STRUCT|
|SQLDATETIM4|DBDATETIM4|
|SQLDATETIME|DBDATETIME|
|SQLDATETIMN|*cbIndicator*<br /> 4: SQLDATETIM4<br /> 8: SQLDATETIME|
|SQLDATETIME2N|SQL_TIMESTAMP_STRUCT|
|SQLDATETIMEOFFSETN|SQL_SS_TIMESTAMPOFFSET_STRUCT|
|SQLIMAGE|unsigned char *|
|SQLUDT|unsigned char *|
|SQLUNIQUEID|SQLGUID|
|SQLVARIANT|*除了下列以外的任何資料類型：*<br />-   text<br />-   ntext<br />-   image<br />-   varchar(max)<br />-   varbinary(max)<br />-   nvarchar(max)<br />-   xml<br />-   timestamp|
|SQLXML|*支援的 C 資料類型：*<br />-   char*<br />-   wchar_t *<br />-   unsigned char *|



&nbsp;

&nbsp;

---

<a name="TitleNum_7"/>

### <a name="7-nbsp-sql-server-index-design-guidesql-server-index-design-guidemd"></a>7.&nbsp; [SQL Server 索引設計指南](sql-server-index-design-guide.md)

更新日期：2018 年 1 月 2 日 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([上一個](#TitleNum_6) | [下一個](#TitleNum_8))

<!-- Source markdown line 700.  ms.author= "rickbyh".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 bd09c9e66cd3cf5f3ebebe7ffa6e937978353169 8e5cbbf0063971676a8bafefba75aa5c7c28be61  (PR=0  ,  Filename=sql-server-index-design-guide.md  ,  Dirpath=docs\relational-databases\  ,  MergeCommitSha40=74daee358fef75a25d75c69d971d08536c5bd2be) -->



從 SQL Server 2016 開始，您可以**在資料列存放區資料表上建立可更新的非叢集資料行存放區索引**。 資料行存放區索引會儲存資料的複本，因此您需要額外的儲存空間。 不過，資料行存放區索引中資料的壓縮大小比資料列存放區資料表所需大小還要小。  如此一來，您就可以同時在資料行存放區索引上執行分析，並在資料列存放區索引上執行交易。 當資料列存放區資料表中的資料變更時，會更新資料行存放區，讓兩個索引會針對相同的資料執行。

從 SQL Server 2016 開始，您可以**在資料行存放區索引上使用一或多個非叢集資料列存放區索引**。 如此一來，您就可以對基礎資料行存放區執行有效率的資料表搜尋。 其他選項現在也可以使用。 例如，您可以在資料列存放區資料表上使用 UNIQUE 條件約束，強制執行主索引鍵條件約束。 由於非唯一的值將無法插入資料列存放區資料表中，因此 SQL Server 無法將值插入資料行存放區中。

**效能考量**


-   非叢集資料行存放區索引定義支援使用篩選的條件。 若要將 OLTP 資料表新增資料行存放區索引對效能的影響降到最低，請只對您作業的工作負載冷資料，使用篩選的條件建立非叢集資料行存放區索引。

-   記憶體中的資料表可以有一個資料行存放區索引。 您可以在建立資料表時予以建立，或稍後使用 [ALTER TABLE &#40;Transact-SQL&#41;](../t-sql/statements/alter-table-transact-sql.md) 將其加入。 在 SQL Server 2016 之前，只有磁碟資料表可以使用資料行存放區索引。

如需詳細資訊，請參閱[資料行存放區索引 - 查詢效能](../relational-databases/indexes/columnstore-indexes-query-performance.md)。

**設計指導**


-   資料列存放區資料表可以有一個可更新的非叢集資料行存放區索引。 在 SQL Server 2014 之前，非叢集資料行存放區索引是唯讀的。



&nbsp;

&nbsp;

---

<a name="TitleNum_8"/>

### <a name="8-nbsp-spexecuteexternalscript-transact-sqlsystem-stored-proceduressp-execute-external-script-transact-sqlmd"></a>8. &nbsp; [sp_execute_external_script (Transact-SQL)](system-stored-procedures/sp-execute-external-script-transact-sql.md)

更新日期：2018 年 1 月 23 日 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([上一個](#TitleNum_7) | [下一個](#TitleNum_9))

<!-- Source markdown line 207.  ms.author= "edmaca".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 0ee4d591ae9d9a5c015eec98aad9ccbb86268761 ac9b439c23ffae5fcc77639de6ff955763cf5844  (PR=4696  ,  Filename=sp-execute-external-script-transact-sql.md  ,  Dirpath=docs\relational-databases\system-stored-procedures\  ,  MergeCommitSha40=d7dcbcebbf416298f838a39dd5de6a46ca9f77aa) -->



若要使用 Python 產生類似的模型，您需要將語言識別項從 `@language=N'R'` 變更為 `@language = N'Python'`，並對 `@script` 引數進行必要的修改。 否則，所有參數都會跟 R 的運作方式相同。

**C.建立 Python 模型，並從中產生分數**


這個範例示範如何使用 sp\_execute\_external\_ 指令碼來產生簡單 Python 模型的分數。

```
CREATE PROCEDURE [dbo].[py_generate_customer_scores]
AS
BEGIN

**Input query to generate the customer data**

DECLARE @input_query NVARCHAR(MAX) = N'SELECT customer, orders, items, cost FROM dbo.Sales.Orders`

EXEC sp_execute_external_script @language = N'Python', @script = N'
import pandas as pd
from sklearn.cluster import KMeans

**Get data from input query**

customer_data = my_input_data

**Define the model**

n_clusters = 4
est = KMeans(n_clusters=n_clusters, random_state=111).fit(customer_data[["orders","items","cost"]])
clusters = est.labels_
customer_data["cluster"] = clusters

OutputDataSet = customer_data
'
, @input_data_1 = @input_query
, @input_data_1_name = N'my_input_data'
WITH RESULT SETS (("CustomerID" int, "Orders" float,"Items" float,"Cost" float,"ClusterResult" float));
END;
GO
```

由於系統不會將 Python 程式碼中使用的資料行標題輸出至 SQL Server，因此請使用 WITH RESULTS 陳述式指定要讓 SQL 使用的資料行名稱與資料類型。

若要計分，您也可以使用原生 [PREDICT](system-stored-procedures/../../t-sql/queries/predict-transact-sql.md) 函式，其會避免呼叫 Python 或 R 執行階段，因此一般來說速度更快。




&nbsp;

&nbsp;

---

<a name="TitleNum_9"/>

### <a name="9-nbsp-create-primary-keystablescreate-primary-keysmd"></a>9.&nbsp; [建立主索引鍵](tables/create-primary-keys.md)

更新日期：2018 年 1 月 18 日 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([上一個](#TitleNum_8))

<!-- Source markdown line 102.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 d18b485f314cc005d624cab8a51650d3b8f55f89 9bd2e9453206e8940d30b0a01c43f9d8e1aed606  (PR=4652  ,  Filename=create-primary-keys.md  ,  Dirpath=docs\relational-databases\tables\  ,  MergeCommitSha40=6b4aae3706247ce9b311682774b13ac067f60a79) -->



**在新的資料表中建立具有非叢集索引的主索引鍵**


1.  在物件總管中，連線到資料庫引擎的執行個體。

2.  在標準列上，按一下 **[新增查詢]**。

3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。 此範例會建立資料表，並在 `CustomerID` 資料行上定義主索引鍵以及在 `TransactionID` 上定義叢集索引。

```
    USE AdventureWorks2012;
    GO
    CREATE TABLE Production.TransactionHistoryArchive1
    (
       CustomerID uniqueidentifier DEFAULT NEWSEQUENTIALID(),
       TransactionID int IDENTITY (1,1) NOT NULL,
       CONSTRAINT PK_TransactionHistoryArchive_TransactionID PRIMARY KEY NONCLUSTERED (uniqueidentifier)
    );
    GO

    -- Now add the clustered index
    CREATE CLUSTERED INDEX CIX_TransactionID ON Production.TransactionHistoryArchive1 (TransactionID);
    GO
```







## <a name="similar-articles-about-new-or-updated-articles"></a>新文章或更新文章的類似文章

本節會在我們的公開 GitHub 存放庫中，列出與其他主題區中最近更新的文章十分相似的文章：[MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/)。


#### <a name="subject-areas-that-do-have-new-or-recently-updated-articles"></a>具有新文章或最近更新文章的主題區


- [新文章 + 更新文章 (1+3)：&nbsp;**Advanced Analytics for SQL** 文件](../advanced-analytics/new-updated-advanced-analytics.md)
- [新文章 + 更新文章 (0+1)：&nbsp;**Analytics Platform System for SQL** 文件](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [新文章 + 更新文章 (0+1)：&nbsp;**連線到 SQL** 文件](../connect/new-updated-connect.md)
- [新文章 + 更新文章 (0+1)：&nbsp;**Database Engine for SQL** 文件](../database-engine/new-updated-database-engine.md)
- [新文章 + 更新文章 (12+1)：**Integration Services for SQL** 文件](../integration-services/new-updated-integration-services.md)
- [新文章 + 更新文章 (6+2)：&nbsp; **Linux for SQL** 文件](../linux/new-updated-linux.md)
- [新文章 + 更新文章 (15+0)：**PowerShell for SQL** 文件](../powershell/new-updated-powershell.md)
- [新文章 + 更新文章 (2+9)：&nbsp;**Relational Databases for SQL** 文件](../relational-databases/new-updated-relational-databases.md)
- [新文章 + 更新文章 (1+0)：&nbsp;**Reporting Services for SQL** 文件](../reporting-services/new-updated-reporting-services.md)
- [新文章 + 更新文章 (1+1)：&nbsp;**SQL Operations Studio** 文件](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [新文章 + 更新文章 (1+1)：&nbsp;**Microsoft SQL Server** 文件](../sql-server/new-updated-sql-server.md)
- [新文章 + 更新文章 (0+1)：&nbsp;**SQL Server Data Tools (SSDT)** 文件](../ssdt/new-updated-ssdt.md)
- [新文章 + 更新文章 (1+2)：&nbsp;**SQL Server Management Studio (SSMS)** 文件](../ssms/new-updated-ssms.md)
- [新文章 + 更新文章 (0+2)：&nbsp;**Transact-SQL** 文件](../t-sql/new-updated-t-sql.md)



#### <a name="subject-areas-that-do-not-have-any-new-or-recently-updated-articles"></a>沒有新文章或最近更新文章的主題區


- [新文章 + 更新文章 (0+0)：**SQL 資料移轉小幫手 (DMA)** 文件](../dma/new-updated-dma.md)
- [新文章 + 更新文章 (0+0)：**ActiveX Data Objects (ADO) for SQL** 文件](../ado/new-updated-ado.md)
- [新文章 + 更新文章 (0+0)：**SQL Analysis Services** 文件](../analysis-services/new-updated-analysis-services.md)
- [新文章 + 更新文章 (0+0)：**Data Quality Services for SQL** 文件](../data-quality-services/new-updated-data-quality-services.md)
- [新文章 + 更新文章 (0+0)：**SQL 資料採礦延伸模組 (DMX)** 文件](../dmx/new-updated-dmx.md)
- [新文章 + 更新文章 (0+0)：**SQL Master Data Services (MDS)** 文件](../master-data-services/new-updated-master-data-services.md)
- [新文章 + 更新文章 (0+0)：**SQL 多維度運算式 (MDX)** 文件](../mdx/new-updated-mdx.md)
- [新文章 + 更新文章 (0+0)：**SQL ODBC (開放式資料庫連接)** 文件](../odbc/new-updated-odbc.md)
- [新文章 + 更新文章 (0+0)：**SQL 範例**文件](../sample/new-updated-sample.md)
- [新文章 + 更新文章 (0+0)：**SQL Server 移轉小幫手 (SSMA)** 文件](../ssma/new-updated-ssma.md)
- [新文章 + 更新文章 (0+0)：**SQL 的工具** 文件](../tools/new-updated-tools.md)
- [新文章 + 更新文章 (0+0)：**XQuery for SQL** 文件](../xquery/new-updated-xquery.md)


