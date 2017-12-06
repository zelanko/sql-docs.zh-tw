---
title: "已更新-連接到 SQL Server 文件 |Microsoft 文件"
description: "顯示更新的內容，如需連接到 Microsoft SQL Server 中最近變更過的文件的程式碼片段。"
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 12/02/2017
ms.author: genemi
ms.workload: connect-to-sql
ms.openlocfilehash: cb0ac4b391559cfac072cff61c9f13b14fe7c952
ms.sourcegitcommit: 29265ad41fbe3326c21c6908ec4275a3a38f1c09
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/04/2017
---
# <a name="new-and-recently-updated-connect-to-sql-server"></a>新增和更新最近： 連接到 SQL Server



Microsoft 幾乎每天都會在其 [Docs.Microsoft.com](http://docs.microsoft.com/) 文件網站上更新一些現有文章。 本文會顯示最近更新文章的摘錄。 可能也會列出新文章的連結。

本文是透過定期重新執行的程式所產生。 摘錄中偶爾會出現示不完整的格式，或顯示為來自來源文章的 Markdown。 影像永遠不會顯示在這裡。

新的更新會報告下列日期範圍和主旨：



- *日期範圍的更新：* &nbsp; **2017年-09-28** &nbsp; -到- &nbsp; **2017年-12-02**
- *主旨區域：* &nbsp; **連接到 SQL Server**。




&nbsp;

## <a name="new-articles-created-recently"></a>最近建立的新文章

下列連結會跳至最近新增的新文章。


1. [資料來源精靈 畫面 1](odbc/windows/dsn-wizard-1.md)
2. [資料來源精靈螢幕 2](odbc/windows/dsn-wizard-2.md)
3. [資料來源精靈畫面 3](odbc/windows/dsn-wizard-3.md)
4. [資料來源精靈畫面 4](odbc/windows/dsn-wizard-4.md)
5. [SQL Server 登入對話方塊 (ODBC)](odbc/windows/sql-server-login-dialog.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>更新文章與摘要

本節會顯示從最近發生大規模更新的文章所收集的更新摘錄。

此處顯示的摘錄不同於其適當語意內容。 此外，有時摘錄也與實際文件四周的重要 Markdown 語法不同。 因此，這些摘錄僅適用於一般指導方針。 摘錄只能讓您知道您感興趣的項目，是否值得花時間按一下並瀏覽實際文章。

由於這些和其他原因，請勿從這些摘錄中複製程式碼，而且不要將任何文字摘錄視為確切事實。 請改瀏覽實際文章。





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>最近更新文章的壓縮清單

此壓縮清單提供＜摘要＞一節中所有更新文章的連結。

1. [PDOStatement::bindParam](#TitleNum_1)
2. [PDOStatement::bindValue](#TitleNum_2)
3. [sqlsrv_prepare](#TitleNum_3)
4. [sqlsrv_query](#TitleNum_4)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-pdostatementbindparamphppdostatement-bindparammd"></a>1.&nbsp;[Pdostatement:: Bindparam](php/pdostatement-bindparam.md)

*更新日期︰ 2017年-10-25* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([下一步](#TitleNum_2))

<!-- Source markdown line 119.  ms.author= "genemi".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 2792d149331f5326f6914721c86687d545685488 e363544e2c6f73277b7f2ca05b9269a4139d1fac  (PR=3663  ,  Filename=pdostatement-bindparam.md  ,  Dirpath=docs\connect\php\  ,  MergeCommitSha40=e9caa51a68c2f03fb9f3a0354b5eab1eed43bdf1) -->



> [!NOTE]
> 建議使用字串做為輸入，當繫結至值[十進位或數值資料行](https://docs.microsoft.com/en-us/sql/t-sql/data-types/decimal-and-numeric-transact-sql)為確保如 PHP 有限的有效位數的有效位數和精確度[浮點數](http://php.net/manual/en/language.types.float.php)。

**範例**

此程式碼範例示範如何將繫結十進位值做為輸入參數。

```php
<?php
$database = "Test";
$server = "(local)";
$conn = new PDO("sqlsrv:server=$server ; Database = $database", "", "");

// Assume TestTable exists with a decimal field
$input = 9223372036854.80000;
$stmt = $conn->prepare("INSERT INTO TestTable (DecimalCol) VALUES (?)");
// by default it is PDO::PARAM_STR, rounding of a large input value may
// occur if PDO::PARAM_INT is specified
$stmt->bindParam(1, $input, PDO::PARAM_STR);
$stmt->execute();
```




&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-pdostatementbindvaluephppdostatement-bindvaluemd"></a>2.&nbsp;[PDOStatement::bindValue](php/pdostatement-bindvalue.md)

*更新日期︰ 2017年-10-25* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([先前](#TitleNum_1) | [下一步](#TitleNum_3))

<!-- Source markdown line 77.  ms.author= "genemi".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 c1d5ff4d5bfdbfbf1635cf14d71b4d583164075a 6cd5fc88860ae9ffca25ee15e8eeaeba29991fda  (PR=3663  ,  Filename=pdostatement-bindvalue.md  ,  Dirpath=docs\connect\php\  ,  MergeCommitSha40=e9caa51a68c2f03fb9f3a0354b5eab1eed43bdf1) -->



> [!NOTE]
> 建議使用字串做為輸入，當繫結至值[十進位或數值資料行](https://docs.microsoft.com/en-us/sql/t-sql/data-types/decimal-and-numeric-transact-sql)為確保如 PHP 有限的有效位數的有效位數和精確度[浮點數](http://php.net/manual/en/language.types.float.php)。

**範例**

此程式碼範例示範如何將繫結十進位值做為輸入參數。

```php
<?php
$database = "Test";
$server = "(local)";
$conn = new PDO("sqlsrv:server=$server ; Database = $database", "", "");

// Assume TestTable exists with a decimal field
$input = 9223372036854.80000;
$stmt = $conn->prepare("INSERT INTO TestTable (DecimalCol) VALUES (?)");
// by default it is PDO::PARAM_STR, rounding of a large input value may
// occur if PDO::PARAM_INT is specified
$stmt->bindValue(1, $input, PDO::PARAM_STR);
$stmt->execute();
```



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-sqlsrvpreparephpsqlsrv-preparemd"></a>3. &nbsp; [sqlsrv_prepare](php/sqlsrv-prepare.md)

*更新日期︰ 2017年-10-25* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([先前](#TitleNum_2) | [下一步](#TitleNum_4))

<!-- Source markdown line 219.  ms.author= "genemi".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 7811e459efec90ef79340375d5fb34364130466b 3d28b3d320dc7fe5df12300da5cb9579abf6839a  (PR=3663  ,  Filename=sqlsrv-prepare.md  ,  Dirpath=docs\connect\php\  ,  MergeCommitSha40=e9caa51a68c2f03fb9f3a0354b5eab1eed43bdf1) -->



> [!NOTE]
> 建議使用字串做為輸入，當繫結至值[十進位或數值資料行](https://docs.microsoft.com/en-us/sql/t-sql/data-types/decimal-and-numeric-transact-sql)為確保如 PHP 有限的有效位數的有效位數和精確度[浮點數](http://php.net/manual/en/language.types.float.php)。

**範例**

此程式碼範例示範如何將繫結十進位值做為輸入參數。

```php
<?php
$serverName = "(local)";
$connectionInfo = array("Database"=>"YourTestDB");
$conn = sqlsrv_connect($serverName, $connectionInfo);
if ($conn === false) {
    echo "Could not connect.\n";
    die(print_r(sqlsrv_errors(), true));
}

// Assume TestTable exists with a decimal field
$input = "9223372036854.80000";
$params = array($input);
$stmt = sqlsrv_prepare($conn, "INSERT INTO TestTable (DecimalCol) VALUES (?)", $params);
sqlsrv_execute($stmt);

sqlsrv_free_stmt($stmt);
sqlsrv_close($conn);

?>
```



&nbsp;

&nbsp;

---

<a name="TitleNum_4"/>

### <a name="4-nbsp-sqlsrvqueryphpsqlsrv-querymd"></a>4. &nbsp; [sqlsrv_query](php/sqlsrv-query.md)

*更新日期︰ 2017年-10-25* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([先前](#TitleNum_3))

<!-- Source markdown line 163.  ms.author= "genemi".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 07a84878c07af0b6ad7e247337be5b4567ce03c3 127af26a8a054a45dda51d90f43f08652949ba18  (PR=3663  ,  Filename=sqlsrv-query.md  ,  Dirpath=docs\connect\php\  ,  MergeCommitSha40=e9caa51a68c2f03fb9f3a0354b5eab1eed43bdf1) -->



> [!NOTE]
> 建議使用字串做為輸入，當繫結至值[十進位或數值資料行](https://docs.microsoft.com/en-us/sql/t-sql/data-types/decimal-and-numeric-transact-sql)為確保如 PHP 有限的有效位數的有效位數和精確度[浮點數](http://php.net/manual/en/language.types.float.php)。

**範例**

此程式碼範例示範如何將繫結十進位值做為輸入參數。

```php
<?php
$serverName = "(local)";
$connectionInfo = array("Database"=>"YourTestDB");
$conn = sqlsrv_connect($serverName, $connectionInfo);
if ($conn === false) {
     echo "Could not connect.\n";
     die(print_r(sqlsrv_errors(), true));
}

// Assume TestTable exists with a decimal field
$input = "9223372036854.80000";
$params = array($input);
$stmt = sqlsrv_query($conn, "INSERT INTO TestTable (DecimalCol) VALUES (?)", $params);

sqlsrv_free_stmt($stmt);
sqlsrv_close($conn);

?>
```








## <a name="similar-articles"></a>類似的文章

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
    2017-12-02  23:00pm
-->

本節會在我們的公開 GitHub 存放庫中，列出與其他主題區中最近更新的文章十分相似的文章：[MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/)。

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>具有新文章或最近更新文章的主題區

- [新 + 更新 (3 + 14): **Advanced Analytics sql**文件](../advanced-analytics/new-updated-advanced-analytics.md)
- [新文章 + 更新文章 (1+0)：**Analysis Services for SQL** 文件](../analysis-services/new-updated-analysis-services.md)
- [新 + 更新 (87 + 0): **Analytics Platform System sql**文件](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [新 + 更新 (5 + 4):**連接到 SQL**文件](../connect/new-updated-connect.md)
- [新 + 更新 (0 + 1): **sql 資料庫引擎**文件](../database-engine/new-updated-database-engine.md)
- [新 + 更新 (2 + 2): **sql Integration Services**文件](../integration-services/new-updated-integration-services.md)
- [新 + 更新 (10 + 9): **sql Linux**文件](../linux/new-updated-linux.md)
- [新 + 更新 (2 + 4):**關聯式資料庫供 SQL**文件](../relational-databases/new-updated-relational-databases.md)
- [新 + 更新 (4 + 2): **Reporting Services SQL**文件](../reporting-services/new-updated-reporting-services.md)
- [新 + 更新 (0 + 1):**範例 sql**文件](../sample/new-updated-sample.md)
- [新 + 更新 (21 + 0): **SQL 作業 Studio**文件](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [新 + 更新 (5 + 1): **Microsoft SQL Server**文件](../sql-server/new-updated-sql-server.md)
- [新文章 + 更新文章 (0+1)：**SQL Server Data Tools (SSDT)** 文件](../ssdt/new-updated-ssdt.md)
- [新 + 更新 (1 + 0): **SQL Server 移轉小幫手 (SSMA)**文件](../ssma/new-updated-ssma.md)
- [新文章 + 更新文章 (0+1)：**SQL Server Management Studio (SSMS)** 文件](../ssms/new-updated-ssms.md)
- [新 + 更新 (0 + 2): **TRANSACT-SQL**文件](../t-sql/new-updated-t-sql.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>沒有新文章或最近更新文章的主題區

- [新 + 更新 (0 + 0):**資料移轉小幫手 (DMA) sql**文件](../dma/new-updated-dma.md)
- [新文章 + 更新文章 (0+0)：**ActiveX Data Objects (ADO) for SQL** 文件](../ado/new-updated-ado.md)
- [新文章 + 更新文章 (0+0)：**Data Quality Services for SQL** 文件](../data-quality-services/new-updated-data-quality-services.md)
- [新文章 + 更新文章 (0+0)：**SQL 資料採礦延伸模組 (DMX)** 文件](../dmx/new-updated-dmx.md)
- [新文章 + 更新文章 (0+0)：**SQL Master Data Services (MDS)** 文件](../master-data-services/new-updated-master-data-services.md)
- [新文章 + 更新文章 (0+0)：**SQL 多維度運算式 (MDX)** 文件](../mdx/new-updated-mdx.md)
- [新文章 + 更新文章 (0+0)：**SQL ODBC (開放式資料庫連接)** 文件](../odbc/new-updated-odbc.md)
- [新文章 + 更新文章 (0+0)：**PowerShell for SQL** 文件](../powershell/new-updated-powershell.md)
- [新文章 + 更新文章 (0+0)：**SQL 的工具** 文件](../tools/new-updated-tools.md)
- [新文章 + 更新文章 (0+0)：**XQuery for SQL** 文件](../xquery/new-updated-xquery.md)


