---
title: 大量匯入期間保留 Null 或使用預設值 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 09/20/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: import-export
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-bulk-import-export
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- bulk importing [SQL Server], null values
- bulk importing [SQL Server], default values
- data formats [SQL Server], null values
- bulk rowset providers [SQL Server]
- bcp utility [SQL Server], null values
- BULK INSERT statement
- default values
- OPENROWSET function, bulk importing
- data formats [SQL Server], default values
ms.assetid: 6b91d762-337b-4345-a159-88abb3e64a81
caps.latest.revision: 41
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 73c367d0d9f1f985c4e65cfdd821ef4534c5b2c6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="keep-nulls-or-use-default-values-during-bulk-import-sql-server"></a>大量匯入期間保留 Null 或使用預設值 (SQL Server)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

根據預設，當資料匯入資料表時， [bcp](../../tools/bcp-utility.md) 命令和 [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 陳述式會查看資料表中的資料行是否已定義預設值。  例如，若資料檔中有一個 Null 值欄位，將會以載入該資料行的預設值來取代。  [bcp](../../tools/bcp-utility.md) 命令和 [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 陳述式都可讓您指定保留 Null 值。

相對地，一般的 INSERT 陳述式會保留 Null 值，而不會插入預設值。 INSERT ...SELECT * FROM [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) 陳述式所提供的基本行為與一般 INSERT 陳述式相同，但它還支援用於插入預設值的[資料表提示](../../t-sql/queries/hints-transact-sql-table.md)。

|外框|
|---|
|[保留 Null 值](#keep_nulls)<br />[使用預設值與 INSERT ...SELECT * FROM OPENROWSET(BULK...)](#keep_default)<br />[範例測試條件](#etc)<br />&emsp;&#9679;&emsp;[範例資料表](#sample_table)<br />&emsp;&#9679;&emsp;[範例資料檔案](#sample_data_file)<br />&emsp;&#9679;&emsp;[範例非 XML 格式檔案](#nonxml_format_file)<br />[大量匯入期間保留 Null 或使用預設值](#import_data)<br />&emsp;&#9679;&emsp;[不使用格式檔案而使用 bcp 並保留 Null 值](#bcp_null)<br />&emsp;&#9679;&emsp;[透過非 XML 格式檔案使用 bcp 並保留 Null 值](#bcp_null_fmt)<br />&emsp;&#9679;&emsp;[不使用格式檔案而使用 bcp 並使用預設值](#bcp_default)<br />&emsp;&#9679;&emsp;[透過非 XML 格式檔案使用 bcp 並使用預設值](#bcp_default_fmt)<br />&emsp;&#9679;&emsp;[不使用格式檔案而使用 BULK INSERT 並保留 Null 值](#bulk_null)<br />&emsp;&#9679;&emsp;[透過非 XML 格式檔案使用 BULK INSERT 並保留 Null 值](#bulk_null_fmt)<br />&emsp;&#9679;&emsp;[不使用格式檔案而使用 BULK INSERT 並使用預設值](#bulk_default)<br />&emsp;&#9679;&emsp;[透過非 XML 格式檔案使用 BULK INSERT 並使用預設值](#bulk_default_fmt)<br />&emsp;&#9679;&emsp;[透過非 XML 格式檔案使用 OPENROWSET(BULK...) 並保留 Null 值](#openrowset__null_fmt)<br />&emsp;&#9679;&emsp;[透過非 XML 格式檔案使用 OPENROWSET(BULK...) 並使用預設值](#openrowset__default_fmt)

## 保留 Null 值<a name="keep_nulls"></a>  
下列限定詞 (qualifier) 可指定資料檔中的空白欄位，在大量匯入作業期間保留其 Null 值，而不要繼承資料表資料行的預設值 (若有的話)。  若是 [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md)，根據預設，在大量載入作業中未指定的資料行都會設定為 NULL。
  
|命令|Qualifier|限定詞類型|  
|-------------|---------------|--------------------|  
|bcp|-k|參數|  
|BULK INSERT|KEEPNULLS**\***|引數|  
|INSERT ...SELECT * FROM OPENROWSET(BULK...)|不適用|不適用|  
  
若是 **\***[BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md)，若沒有預設值可使用，必須將資料表資料行定義為允許 Null 值。 
  
> [!NOTE]
> 這些限定詞會使這些大量匯入命令不再檢查資料表上有無 DEFAULT 定義，  但對任何並行 INSERT 陳述式而言，DEFAULT 定義是可預期的。
 
## 透過 INSERT 使用預設值 ...SELECT * FROM [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md)<a name="keep_default"></a>  
您可以指定在資料檔的空白欄位中，對應的資料表資料行會使用其預設值 (若有的話)。  若要使用預設值，請使用資料表提示 [KEEPDEFAULTS](../../t-sql/queries/hints-transact-sql-table.md)。
 
> [!NOTE]
>  如需詳細資訊，請參閱 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)、[SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)、[OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md) 及 [ &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md)

## 範例測試條件<a name="etc"></a>  
本主題中的範例以下面定義的資料表、資料檔案和格式檔案為基礎。

### **範例資料表**<a name="sample_table"></a>
下列指令碼會建立測試資料庫和名為 `myNulls`的資料表。  請注意，第四個資料表資料行 `Kids`中有預設值。  請在 Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) 中執行下列 Transact-SQL：

```sql
CREATE DATABASE TestDatabase;
GO

USE TestDatabase;
CREATE TABLE dbo.myNulls ( 
   PersonID smallint not null,
   FirstName varchar(25),
   LastName varchar(30),
   Kids varchar(13) DEFAULT 'Default Value',
   BirthDate date
   );
```

### **範例資料檔案**<a name="sample_data_file"></a>
使用記事本建立空白檔案 `D:\BCP\myNulls.bcp` ，並插入下方資料。  請注意，第三個記錄的第四個資料行中沒有值。

```
1,Anthony,Grosse,Yes,1980-02-23
2,Alica,Fatnowna,No,1963-11-14
3,Stella,Rosenhain,,1992-03-02
```

您也可以執行下列 PowerShell 指令碼以建立並填入資料檔案：

```powershell
cls
# revise directory as desired
$dir = 'D:\BCP\';

$bcpFile = $dir + 'MyNulls.bcp';

# Confirm directory exists
IF ((Test-Path -Path $dir) -eq 0)
{
    Write-Host "The path $dir does not exist; please create or modify the directory.";
    RETURN;
};

# clear content, will error if file does not exist, can be ignored
Clear-Content -Path $bcpFile -ErrorAction SilentlyContinue;

# Add data
Add-Content -Path $bcpFile -Value '1,Anthony,Grosse,Yes,1980-02-23';
Add-Content -Path $bcpFile -Value '2,Alica,Fatnowna,No,1963-11-14';
Add-Content -Path $bcpFile -Value '3,Stella,Rosenhain,,1992-03-02';

#Review content
Get-Content -Path $bcpFile;
Invoke-Item $bcpFile;
```
  
### **範例非 XML 格式檔案**<a name="nonxml_format_file"></a>
SQL Server 支援兩種類型的格式檔案：非 XML 格式和 XML 格式。  非 XML 格式是舊版 SQL Server 所支援的原始格式。  如需詳細資訊，請參閱 [非 XML 格式檔案 (SQL Server)](../../relational-databases/import-export/non-xml-format-files-sql-server.md) 。  下列命令將使用 [bcp 公用程式](../../tools/bcp-utility.md) ，根據 `myNulls.fmt`的結構描述產生非 XML 格式檔案 `myNulls`。  使用 [bcp](../../tools/bcp-utility.md) 命令建立格式檔案時，請指定 **format** 引數並使用 **nul** 取代資料檔案路徑。  format 選項也需要 **-f** 選項。  在這個範例中，另外還會使用限定詞 **c** 來指定字元資料，使用 **t,** 來指定逗號作為 [欄位結束字元](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)，並使用 **T** 來指定使用整合式安全性的信任連接。  請在命令提示字元之下，輸入下列命令：

```cmd
bcp TestDatabase.dbo.myNulls format nul -c -f D:\BCP\myNulls.fmt -t, -T

REM Review file
Notepad D:\BCP\myNulls.fmt
```

> [!IMPORTANT]
> 請確認您的非 XML 格式檔案以歸位字元\換行字元結尾。  否則您可能會收到下列錯誤訊息︰
> 
> `SQLState = S1000, NativeError = 0`  
> `Error = [Microsoft][ODBC Driver 13 for SQL Server]I/O error while reading BCP format file`

 如需建立格式檔案的詳細資訊，請參閱 [建立格式檔案 &#40;SQL Server&#41;](../../relational-databases/import-export/create-a-format-file-sql-server.md)。  
  
## 大量匯入期間保留 Null 或使用預設值<a name="import_data"></a>
下列範例會使用上面建立的資料庫、資料檔案和格式檔案。

### **不使用格式檔案而使用 [bcp](../../tools/bcp-utility.md) 並保留 Null 值**<a name="bcp_null"></a>

**-k** 參數。  請在命令提示字元之下，輸入下列命令：

```cmd
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myNulls;"

REM Import data
bcp TestDatabase.dbo.myNulls IN D:\BCP\myNulls.bcp -c -t, -T -k

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.myNulls;"
```
  
### **不使用格式檔案而使用 [bcp](../../tools/bcp-utility.md) 使用 [bcp](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="bcp_null_fmt"></a>
**-k** 與 **-f** 參數。 請在命令提示字元之下，輸入下列命令：

```cmd
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myNulls;"

REM Import data
bcp TestDatabase.dbo.myNulls IN D:\BCP\myNulls.bcp -f D:\BCP\myNulls.fmt -T -k

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.myNulls;"
```

### **不使用格式檔案而使用 [bcp](../../tools/bcp-utility.md) 並使用預設值**<a name="bcp_default"></a>
請在命令提示字元之下，輸入下列命令：

```cmd
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myNulls;"

REM Import data
bcp TestDatabase.dbo.myNulls IN D:\BCP\myNulls.bcp -c -t, -T

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.myNulls;"
```
  
### **不使用格式檔案而使用 [bcp](../../tools/bcp-utility.md) 使用 [bcp](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="bcp_default_fmt"></a>
**-f** 參數。  請在命令提示字元之下，輸入下列命令：

```cmd
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myNulls;"

REM Import data
bcp TestDatabase.dbo.myNulls IN D:\BCP\myNulls.bcp -f D:\BCP\myNulls.fmt -T

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.myNulls;"
```

### **不使用格式檔案而使用 [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 並保留 Null 值**<a name="bulk_null"></a>
**KEEPNULLS** 引數。  請在 Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) 中執行下列 Transact-SQL：

```sql
USE TestDatabase;
GO
TRUNCATE TABLE dbo.myNulls; -- for testing
BULK INSERT dbo.myNulls
    FROM 'D:\BCP\myNulls.bcp'
    WITH (
        DATAFILETYPE = 'char',  
        FIELDTERMINATOR = ',',  
        KEEPNULLS
        );

-- review results
SELECT * FROM TestDatabase.dbo.myNulls;
```

### **不使用格式檔案而使用 [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 使用 [bcp](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="bulk_null_fmt"></a>
**KEEPNULLS** 和 **FORMATFILE** 引數。  請在 Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) 中執行下列 Transact-SQL：

```sql
USE TestDatabase;
GO

TRUNCATE TABLE dbo.myNulls; -- for testing
BULK INSERT dbo.myNulls
   FROM 'D:\BCP\myNulls.bcp'
   WITH (
        FORMATFILE = 'D:\BCP\myNulls.fmt',
        KEEPNULLS
        );

-- review results
SELECT * FROM TestDatabase.dbo.myNulls;
```

### **不使用格式檔案而使用 [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 並使用預設值**<a name="bulk_default"></a>
請在 Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) 中執行下列 Transact-SQL：

```sql
USE TestDatabase;
GO

TRUNCATE TABLE dbo.myNulls;  -- for testing
BULK INSERT dbo.myNulls
   FROM 'D:\BCP\myNulls.bcp'
   WITH (
      DATAFILETYPE = 'char',  
      FIELDTERMINATOR = ','
      );

-- review results
SELECT * FROM TestDatabase.dbo.myNulls;
```

### **不使用格式檔案而使用 [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 使用 [bcp](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="bulk_default_fmt"></a>
**FORMATFILE** 引數。  請在 Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) 中執行下列 Transact-SQL：

```sql
USE TestDatabase;
GO

TRUNCATE TABLE dbo.myNulls;  -- for testing
BULK INSERT dbo.myNulls
   FROM 'D:\BCP\myNulls.bcp'
   WITH (
        FORMATFILE = 'D:\BCP\myNulls.fmt'
        );

-- review results
SELECT * FROM TestDatabase.dbo.myNulls;
```

### **不使用格式檔案而使用 [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) 使用 [bcp](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="openrowset__null_fmt"></a>
**FORMATFILE** 引數。  請在 Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) 中執行下列 Transact-SQL：

```sql
USE TestDatabase;
GO

TRUNCATE TABLE dbo.myNulls;  -- for testing
INSERT INTO dbo.myNulls
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myNulls.bcp', 
        FORMATFILE = 'D:\BCP\myNulls.fmt'  
        ) AS t1;

-- review results
SELECT * FROM TestDatabase.dbo.myNulls;
```

### **不使用格式檔案而使用 [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) 使用 [bcp](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="openrowset__default_fmt"></a>
**KEEPDEFAULTS** 資料表提示和 **FORMATFILE** 引數。  請在 Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) 中執行下列 Transact-SQL：

```sql
USE TestDatabase;
GO

TRUNCATE TABLE dbo.myNulls;  -- for testing
INSERT INTO dbo.myNulls
WITH (KEEPDEFAULTS) 
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myNulls.bcp', 
        FORMATFILE = 'D:\BCP\myNulls.fmt'  
        ) AS t1;

-- review results
SELECT * FROM TestDatabase.dbo.myNulls;
```

  
##  <a name="RelatedTasks"></a> 相關工作  
  
-   [大量匯入資料時保留識別值 &#40;SQL Server&#41;](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)  
  
-   [準備大量匯出或匯入的資料 &#40;SQL Server&#41;](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md)  
  
 **若要使用格式檔案**  
  
-   [建立格式檔案 &#40;SQL Server&#41;](../../relational-databases/import-export/create-a-format-file-sql-server.md)  
  
-   [使用格式檔案大量匯入資料 &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [使用格式檔案將資料表資料行對應至資料檔案欄位 &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
-   [使用格式檔案略過資料欄位 &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
-   [使用格式檔案略過資料表資料行 &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
 **若要使用大量匯入或大量匯出的資料格式**  
  
-   [從舊版 SQL Server 匯入原生與字元格式資料](../../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [使用字元格式匯入或匯出資料 &#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [使用原生格式匯入或匯出資料 &#40;SQL Server&#41;](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [使用 Unicode 字元格式匯入或匯出資料 &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [使用 Unicode 原生格式匯入或匯出資料 &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
 **若要在使用 bcp 時指定相容性的資料格式**  
  
-   [指定欄位與資料列結束字元 &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)  
  
-   [使用 bcp 指定資料檔的前置長度 &#40;SQL Server&#41;](../../relational-databases/import-export/specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)  
  
-   [使用 bcp 指定檔案儲存類型 &#40;SQL Server&#41;](../../relational-databases/import-export/specify-file-storage-type-by-using-bcp-sql-server.md)  
  
## <a name="see-also"></a>另請參閱  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [bcp 公用程式](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [資料表提示 &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md)  
  
  
