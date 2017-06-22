---
title: "大量匯入資料時保留識別值 (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 09/21/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-bulk-import-export
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- identity values [SQL Server], bulk imports
- data formats [SQL Server], identity values
- bulk importing [SQL Server], identity values
ms.assetid: 45894a3f-2d8a-4edd-9568-afa7d0d3061f
caps.latest.revision: 22
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 484b11226fbf523d7d2ba1dac47a12b04ef6eec9
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="keep-identity-values-when-bulk-importing-data-sql-server"></a>大量匯入資料時保留識別值 (SQL Server)
您可以將包含識別值的資料檔案大量匯入 Microsoft SQL Server 的執行個體中。  根據預設，會忽略所匯入資料檔案中的識別欄位值， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會自動指定唯一值。  唯一值的依據是資料表建立期間所指定的初始值及累加值。

如果資料檔不包含資料表中識別碼資料行的值，請使用格式檔案指定在匯入資料時應略過資料表中的識別碼資料行。  如需其他資訊，請參閱 [使用格式檔案以略過資料表資料行 (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md) 。

|外框|
|---|
|[保留識別值](#keep_identity)<br />[範例測試條件](#etc)<br />&emsp;&#9679;&emsp;[範例資料表](#sample_table)<br />&emsp;&#9679;&emsp;[範例資料檔案](#sample_data_file)<br />&emsp;&#9679;&emsp;[範例非 XML 格式檔案](#nonxml_format_file)<br />[範例](#examples)<br />&emsp;&#9679;&emsp;[不使用格式檔案而使用 bcp 並保留識別值](#bcp_identity)<br />&emsp;&#9679;&emsp;[透過非 XML 格式檔案使用 bcp 並保留識別值](#bcp_identity_fmt)<br />&emsp;&#9679;&emsp;[不使用格式檔案而使用 bcp 與產生的識別值](#bcp_default)<br />&emsp;&#9679;&emsp;[透過非 XML 格式檔案使用 bcp 與產生的識別值](#bcp_default_fmt)<br />&emsp;&#9679;&emsp;[不使用格式檔案而使用 BULK INSERT 並保留識別值](#bulk_identity)<br />&emsp;&#9679;&emsp;[透過非 XML 格式檔案使用 BULK INSERT 並保留識別值](#bulk_identity_fmt)<br />&emsp;&#9679;&emsp;[不使用格式檔案而使用 BULK INSERT 與產生的識別值](#bulk_default)<br />&emsp;&#9679;&emsp;[透過非 XML 格式檔案使用 BULK INSERT 與產生的識別值](#bulk_default_fmt)<br />&emsp;&#9679;&emsp;[透過非 XML 格式檔案使用 OPENROWSET 並保留識別值](#openrowset_identity_fmt)<br />&emsp;&#9679;&emsp;[透過非 XML 格式檔案使用 OPENROWSET 與產生的識別值](#openrowset_default_fmt)<br /><p>                                                                                                                                                                                                                  </p>|

## 保留識別值 <a name="keep_identity"></a>  
若要在將資料列大量匯入資料表時，不讓 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 指定識別值，請使用適當的 keep-identity 命令限定詞。  當您指定 keep-identity 限定詞時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會使用資料檔案中的識別值。  這些限定詞如下：

|Command|Keep-identity 限定詞|限定詞類型|  
|-------------|------------------------------|--------------------|  
|bcp|-E|參數|  
|BULK INSERT|KEEPIDENTITY|引數|  
|INSERT ...SELECT * FROM OPENROWSET(BULK...)|KEEPIDENTITY|資料表提示|  
   
 如需詳細資訊，請參閱 [bcp 公用程式](../../tools/bcp-utility.md)、[BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)、[OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)、[INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)、[SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md) 和[資料表提示 &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md)。  

> [!NOTE]
>  若要建立可用於多個資料表中或可在不參考任何資料表的情況下從應用程式進行呼叫的自動遞增數字，請參閱 [序號](../../relational-databases/sequence-numbers/sequence-numbers.md)。
 
## 範例測試條件<a name="etc"></a>  
本主題中的範例以下面定義的資料表、資料檔案和格式檔案為基礎。

### **範例資料表**<a name="sample_table"></a>
下列指令碼會建立測試資料庫和名為 `myIdentity`的資料表。  請在 Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) 中執行下列 Transact-SQL：
```tsql
CREATE DATABASE TestDatabase;
GO

USE TestDatabase;
CREATE TABLE dbo.myIdentity ( 
   PersonID smallint IDENTITY(1,1) NOT NULL,
   FirstName varchar(25) NOT NULL,
   LastName varchar(30) NOT NULL,
   BirthDate date
   );
```
 
### **範例資料檔案**<a name="sample_data_file"></a>
使用記事本建立空白檔案 `D:\BCP\myIdentity.bcp` ，並插入下方資料。  
```
3,Anthony,Grosse,1980-02-23
2,Alica,Fatnowna,1963-11-14
1,Stella,Rosenhain,1992-03-02
4,Miller,Dylan,1954-01-05
```
  
您也可以執行下列 PowerShell 指令碼以建立並填入資料檔案：
```powershell
cls
# revise directory as desired
$dir = 'D:\BCP\';

$bcpFile = $dir + 'myIdentity.bcp';

# Confirm directory exists
IF ((Test-Path -Path $dir) -eq 0)
{
    Write-Host "The path $dir does not exist; please create or modify the directory.";
    RETURN;
};

# clear content, will error if file does not exist, can be ignored
Clear-Content -Path $bcpFile -ErrorAction SilentlyContinue;

# Add data
Add-Content -Path $bcpFile -Value '3,Anthony,Grosse,1980-02-23';
Add-Content -Path $bcpFile -Value '2,Alica,Fatnowna,1963-11-14';
Add-Content -Path $bcpFile -Value '1,Stella,Rosenhain,1992-03-02';
Add-Content -Path $bcpFile -Value '4,Miller,Dylan,1954-01-05';

#Review content
Get-Content -Path $bcpFile;
Invoke-Item $bcpFile;
```

### **範例非 XML 格式檔案**<a name="nonxml_format_file"></a>
SQL Server 支援兩種類型的格式檔案：非 XML 格式和 XML 格式。  非 XML 格式是舊版 SQL Server 所支援的原始格式。  如需詳細資訊，請參閱 [非 XML 格式檔案 (SQL Server)](../../relational-databases/import-export/non-xml-format-files-sql-server.md) 。  下列命令將使用 [bcp 公用程式](../../tools/bcp-utility.md) ，根據 `myIdentity.fmt`的結構描述產生非 XML 格式檔案 `myIdentity`。  使用 [bcp](../../tools/bcp-utility.md) 命令建立格式檔案時，請指定 **format** 引數並使用 **nul** 取代資料檔案路徑。  format 選項也需要 **-f** 選項。  在這個範例中，另外還會使用限定詞 **c** 來指定字元資料，使用 **t,** 來指定逗號作為 [欄位結束字元](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)，並使用 **T** 來指定使用整合式安全性的信任連接。  請在命令提示字元之下，輸入下列命令：
  
```
bcp TestDatabase.dbo.myIdentity format nul -c -f D:\BCP\myIdentity.fmt -t, -T

REM Review file
Notepad D:\BCP\myIdentity.fmt
```
 
> [!IMPORTANT]
> 請確認您的非 XML 格式檔案以歸位字元\換行字元結尾。  否則您可能會收到下列錯誤訊息︰
> 
> `SQLState = S1000, NativeError = 0`  
> `Error = [Microsoft][ODBC Driver 13 for SQL Server]I/O error while reading BCP format file`

## 範例<a name="examples"></a>
下列範例會使用上面建立的資料庫、資料檔案和格式檔案。
  
### **不使用格式檔案而使用 [bcp](../../tools/bcp-utility.md) 並保留識別值**<a name="bcp_identity"></a>
**-E** 參數。  請在命令提示字元之下，輸入下列命令：
```
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myIdentity;"

REM Import data
bcp TestDatabase.dbo.myIdentity IN D:\BCP\myIdentity.bcp -T -c -t, -E

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.myIdentity;"
```

### **Using [bcp](../../tools/bcp-utility.md) and Keeping Identity Values with a [Non-XML Format File](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="bcp_identity_fmt"></a>
**-E** 與 **-f** 參數。  請在命令提示字元之下，輸入下列命令：
```
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myIdentity;"

REM Import data
bcp TestDatabase.dbo.myIdentity IN D:\BCP\myIdentity.bcp -f D:\BCP\myIdentity.fmt -T -E

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.myIdentity;"
```
 
### **不使用格式檔案而使用 [bcp](../../tools/bcp-utility.md) 與產生的預設值**<a name="bcp_default"></a>
使用預設值。  請在命令提示字元之下，輸入下列命令：
```
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myIdentity;"

REM Import data
bcp TestDatabase.dbo.myIdentity IN D:\BCP\myIdentity.bcp -T -c -t,

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.myIdentity;"
```
  
### **Using [bcp](../../tools/bcp-utility.md) and Generated Identity Values with a [Non-XML Format File](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="bcp_default_fmt"></a>
使用預設值與 **-f** 參數。  請在命令提示字元之下，輸入下列命令：
```
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myIdentity;"

REM Import data
bcp TestDatabase.dbo.myIdentity IN D:\BCP\myIdentity.bcp -f D:\BCP\myIdentity.fmt -T

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.myIdentity;"
```
  
### **不使用格式檔案而使用 [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 並保留識別值**<a name="bulk_identity"></a>
**KEEPIDENTITY** 引數。  請在 Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) 中執行下列 Transact-SQL：
```tsql
USE TestDatabase;
GO

TRUNCATE TABLE dbo.myIdentity; -- for testing
BULK INSERT dbo.myIdentity
    FROM 'D:\BCP\myIdentity.bcp'
    WITH (
        DATAFILETYPE = 'char',  
        FIELDTERMINATOR = ',',  
        KEEPIDENTITY
        );

-- review results
SELECT * FROM TestDatabase.dbo.myIdentity;
```
  
### **Using [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) and Keeping Identity Values with a [Non-XML Format File](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="bulk_identity_fmt"></a>
**KEEPIDENTITY** 和 **FORMATFILE** 引數。  請在 Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) 中執行下列 Transact-SQL：
```tsql
USE TestDatabase;
GO

TRUNCATE TABLE dbo.myIdentity; -- for testing
BULK INSERT dbo.myIdentity
   FROM 'D:\BCP\myIdentity.bcp'
   WITH (
        FORMATFILE = 'D:\BCP\myIdentity.fmt',
        KEEPIDENTITY
        );

-- review results
SELECT * FROM TestDatabase.dbo.myIdentity;
```
  
### **不使用格式檔案而使用 [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 與產生的識別值**<a name="bulk_default"></a>
使用預設值。  請在 Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) 中執行下列 Transact-SQL：
```tsql
USE TestDatabase;
GO

TRUNCATE TABLE dbo.myIdentity;  -- for testing
BULK INSERT dbo.myIdentity
   FROM 'D:\BCP\myIdentity.bcp'
   WITH (
      DATAFILETYPE = 'char',  
      FIELDTERMINATOR = ','
      );

-- review results
SELECT * FROM TestDatabase.dbo.myIdentity;
```
  
### **Using [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) and Generated Identity Values with a [Non-XML Format File](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="bulk_default_fmt"></a>
使用預設值和 **FORMATFILE** 引數。  請在 Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) 中執行下列 Transact-SQL：
```tsql
USE TestDatabase;
GO

TRUNCATE TABLE dbo.myIdentity;  -- for testing
BULK INSERT dbo.myIdentity
   FROM 'D:\BCP\myIdentity.bcp'
   WITH (
        FORMATFILE = 'D:\BCP\myIdentity.fmt'
        );

-- review results
SELECT * FROM TestDatabase.dbo.myIdentity;
```
  
### **Using [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) and Keeping Identity Values with a [Non-XML Format File](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="openrowset_identity_fmt"></a>
**KEEPIDENTITY** 資料表提示和 **FORMATFILE** 引數。  請在 Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) 中執行下列 Transact-SQL：
```tsql
USE TestDatabase;
GO

TRUNCATE TABLE dbo.myIdentity;  -- for testing
INSERT INTO dbo.myIdentity
WITH (KEEPIDENTITY) 
(PersonID, FirstName, LastName, BirthDate)
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myIdentity.bcp', 
        FORMATFILE = 'D:\BCP\myIdentity.fmt'  
        ) AS t1;

-- review results
SELECT * FROM TestDatabase.dbo.myIdentity;
```
 
### **Using [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) and Generated Identity Values with a [Non-XML Format File](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="openrowset_default_fmt"></a>
使用預設值和 **FORMATFILE** 引數。  請在 Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) 中執行下列 Transact-SQL：
```tsql
USE TestDatabase;
GO

TRUNCATE TABLE dbo.myIdentity;  -- for testing
INSERT INTO dbo.myIdentity
(FirstName, LastName, BirthDate)
    SELECT FirstName, LastName, BirthDate
    FROM OPENROWSET (
        BULK 'D:\BCP\myIdentity.bcp', 
        FORMATFILE = 'D:\BCP\myIdentity.fmt'  
        ) AS t1;

-- review results
SELECT * FROM TestDatabase.dbo.myIdentity;
```
  
##  <a name="RelatedTasks"></a> 相關工作  
  
-   [大量匯入期間保留 Null 或使用預設值 &#40;SQL Server&#41;](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)  
  
-   [準備大量匯出或匯入的資料 &#40;SQL Server&#41;](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md)  
  
 **若要使用格式檔案**  
  
-   [建立格式檔案 &#40;SQL Server&#41;](../../relational-databases/import-export/create-a-format-file-sql-server.md)  
  
-   [使用格式檔案大量匯入資料 &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [使用格式檔案將資料表資料行對應至資料檔欄位 &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
-   [使用格式檔案略過資料欄位 &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
-   [使用格式檔案略過資料表資料行 &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
 **若要使用大量匯入或大量匯出的資料格式**  
  
-   [從舊版 SQL Server 匯入原生與字元格式資料](../../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [使用字元格式匯入或匯出資料 &#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [使用原生格式匯入或匯出資料 &#40;SQL Server&#41;](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [使用 Unicode 字元格式匯入或匯出資料 &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [使用 Unicode 原生格式匯入或匯出資料 &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
 **若要在使用 bcp 時指定相容性的資料格式**  
  
1.  [指定欄位與資料列結束字元 &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)  
  
2.  [使用 bcp 指定資料檔的前置長度 &#40;SQL Server&#41;](../../relational-databases/import-export/specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)  
  
3.  [使用 bcp 指定檔案儲存類型 &#40;SQL Server&#41;](../../relational-databases/import-export/specify-file-storage-type-by-using-bcp-sql-server.md)  
  
## <a name="see-also"></a>另請參閱  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [bcp 公用程式](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [資料表提示 &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md)  
[匯入或匯出資料的格式檔案 (SQL Server)](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)  
  

