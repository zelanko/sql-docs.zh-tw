---
title: "使用字元格式匯入或匯出資料 (SQL Server) | Microsoft 文件"
ms.custom: 
ms.date: 09/29/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-bulk-import-export
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data formats [SQL Server], character
- character formats [SQL Server]
ms.assetid: d925e66a-1a73-43cd-bc06-1cbdf8174a4d
caps.latest.revision: 42
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: dd20fe12af6f1dcaf378d737961bc2ba354aabe5
ms.openlocfilehash: 927bc546612f0d56ce857a41fbb2ba49ca32d47e
ms.contentlocale: zh-tw
ms.lasthandoff: 10/04/2017

---
# <a name="use-character-format-to-import-or-export-data-sql-server"></a>使用字元格式匯入或匯出資料 (SQL Server)
若要將資料大量匯出到用於其他程式的文字檔，或是要從其他程式產生的文字檔大量匯入資料，建議您使用字元格式。  

字元格式會在所有的資料行中使用字元資料格式。 當資料用於其他程式中，例如試算表，或當資料需要從其他資料庫供應商 (例如 Oracle) 複製到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體時，以字元格式來儲存資訊就很有用。  
  
> [!NOTE]
>  如果您要在 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體之間大量傳送資料，而資料檔包含 Unicode 字元資料，但不含任何擴充字元或 DBCS 字元，請使用 Unicode 字元格式。 如需詳細資訊，請參閱 [使用 Unicode 字元格式匯入或匯出資料 &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)。
  
|本主題內容：|
|---|
|[使用字元格式的考量](#considerations)|
|[字元格式的命令選項](#command_options)|
|[範例測試條件](#etc)<br />&emsp;&#9679;&emsp;[範例資料表](#sample_table)<br />&emsp;&#9679;&emsp;[範例非 XML 格式檔案](#nonxml_format_file)<br />|
|[範例](#examples)<br />&emsp;&#9679;&emsp;[使用 BCP 與字元格式匯出資料](#bcp_char_export)<br />&emsp;&#9679;&emsp;[不使用格式檔案而使用 BCP 與字元格式匯入資料](#bcp_char_import)<br />&emsp;&#9679;&emsp;[使用 BCP 與字元格式匯入非 XML 格式檔案的資料](#bcp_char_import_fmt)<br />&emsp;&#9679;&emsp;[不使用格式檔案而使用 BULK INSERT 與字元格式](#bulk_char)<br />&emsp;&#9679;&emsp;[對非 XML 格式檔案使用 BULK INSERT 與字元格式](#bulk_char_fmt)<br />&emsp;&#9679;&emsp;[對非 XML 格式檔案使用 OPENROWSET 與字元格式](#openrowset_char_fmt)|
|[相關工作](#RelatedTasks)<p>                                                                                                                                                                                                                  </p>|


  
## 使用字元格式的考量<a name="considerations"></a>
使用字元格式時，請考慮下列事項：  
  
-   [bcp 公用程式](../../tools/bcp-utility.md)預設會使用定位字元分隔字元資料欄位，並使用新行字元終止記錄。  如需如何指定其他結束字元的相關資訊，請參閱[指定欄位與資料列結束字元 &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)。  
  
-   依預設，在大量匯出或匯入字元模式資料之前，會執行下列轉換：  
  
    |大量作業的方向|轉換|  
    |---------------------------------|----------------|  
    |匯出|將資料轉換成字元表示法。 若有明確要求，則字元資料行中的資料會轉換成所要求的字碼頁。 若未指定字碼頁，則會使用用戶端電腦的 OEM 字碼頁來轉換字元資料。|  
    |匯入|視需要將字元資料轉換成原生表示法，並將字元資料由用戶端字碼頁轉譯成目標資料行的字碼頁。|  
  
-   若要避免在轉換期間遺失擴充字元，請使用 Unicode 字元格式，或指定字碼頁。  
  
-   所有儲存在字元格式檔案中的 [sql_variant](../../t-sql/data-types/sql-variant-transact-sql.md) 資料，會在沒有中繼資料的情況下儲存。 每個資料值會根據隱含資料轉換的規則，轉換成 [char](../../t-sql/data-types/char-and-varchar-transact-sql.md) 格式。 匯入 [sql_variant](../../t-sql/data-types/sql-variant-transact-sql.md) 資料行時，資料會以 [char](../../t-sql/data-types/char-and-varchar-transact-sql.md)格式匯入。 要匯入的資料行如果不是採用 [sql_variant](../../t-sql/data-types/sql-variant-transact-sql.md) 資料類型，則會使用隱含轉換將資料從 [char](../../t-sql/data-types/char-and-varchar-transact-sql.md) 轉換過來。 如需資料轉換的詳細資訊，請參閱[資料類型轉換 &#40;Database Engine&#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)。  
  
-   [bcp 公用程式](../../tools/bcp-utility.md)會將 [money](../../t-sql/data-types/money-and-smallmoney-transact-sql.md) 值匯出成小數點後 4 位數的字元格式資料檔案，但不會使用任何數字分位符號 (例如逗點分隔符號)。 例如， [money](../../t-sql/data-types/money-and-smallmoney-transact-sql.md) 資料行包含的值 1,234,567.123456，會採用 1234567.1235 的字元字串，大量匯出到資料檔。  
  
## 字元格式的命令選項<a name="command_options"></a>  
您可以將字元格式資料匯入資料表，方法是使用 [bcp](../../tools/bcp-utility.md)、[BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 或 [INSERT ...SELECT * FROM OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md)。對於 [bcp](../../tools/bcp-utility.md) 命令或 [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 陳述式，您可以在陳述式中指定資料格式。  對於 [INSERT...SELECT * FROM OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) 陳述式。您必須在格式檔案中指定資料格式。  
  
下列命令列選項支援字元格式：  
  
|Command|選項|描述|  
|-------------|------------|-----------------|  
|bcp|**-c**|指定 bcp 公用程式使用字元資料。*|  
|BULK INSERT|DATAFILETYPE **='char'**|於大量匯入資料時使用字元格式。|  
|OPENROWSET|N/A|必須使用格式檔案|
  
 \**若要將字元 (**-c**) 資料載入與舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用戶端相容的格式，請使用 **-V** 切換。 如需詳細資訊，請參閱 [從舊版 SQL Server 匯入原生與字元格式資料](../../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)。  
   
> [!NOTE]
>  或者，您可以在格式檔案中按照每個欄位指定格式。 如需詳細資訊，請參閱 [匯入或匯出資料的格式檔案 &#40;SQL Server&#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)＞。

## 範例測試條件<a name="etc"></a>  
本主題中的範例採用下列定義的資料表、資料檔案與格式檔案。

### **範例資料表**<a name="sample_table"></a>
下列指令碼會建立測試資料庫、名為 `myChar` 的資料表，以及在資料表中填入一些初始值。  請在 Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) 中執行下列 Transact-SQL：

```sql
CREATE DATABASE TestDatabase;
GO

USE TestDatabase;
CREATE TABLE dbo.myChar ( 
   PersonID smallint NOT NULL,
   FirstName varchar(25) NOT NULL,
   LastName varchar(30) NOT NULL,
   BirthDate date,
   AnnualSalary money
   );

-- Populate table
INSERT TestDatabase.dbo.myChar
VALUES 
(1, 'Anthony', 'Grosse', '1980-02-23', 65000.00),
(2, 'Alica', 'Fatnowna', '1963-11-14', 45000.00),
(3, 'Stella', 'Rossenhain', '1992-03-02', 120000.00);

-- Review Data
SELECT * FROM TestDatabase.dbo.myChar;
```

### **範例非 XML 格式檔案**<a name="nonxml_format_file"></a>
SQL Server 支援兩種類型的格式檔案：非 XML 格式和 XML 格式。  非 XML 格式是舊版 SQL Server 所支援的原始格式。  如需詳細資訊，請參閱 [非 XML 格式檔案 (SQL Server)](../../relational-databases/import-export/non-xml-format-files-sql-server.md) 。  下列命令將使用 [bcp 公用程式](../../tools/bcp-utility.md) ，根據 `myChar.fmt`的結構描述產生非 XML 格式檔案 `myChar`。  使用 [bcp](../../tools/bcp-utility.md) 命令建立格式檔案時，請指定 **format** 引數並使用 **nul** 取代資料檔案路徑。  format 選項也需要 **-f** 選項。  此外，以此範例為例，限定詞 **c** 會用於指定字元資料， **T** 會用於指定使用整合式安全性的信任連線。  請在命令提示字元之下，輸入下列命令：

```cmd
bcp TestDatabase.dbo.myChar format nul -f D:\BCP\myChar.fmt -T -c 

REM Review file
Notepad D:\BCP\myChar.fmt
```

> [!IMPORTANT]
> 請確認您的非 XML 格式檔案以歸位字元\換行字元結尾。  否則您可能會收到下列錯誤訊息︰
> 
> `SQLState = S1000, NativeError = 0`  
> `Error = [Microsoft][ODBC Driver 13 for SQL Server]I/O error while reading BCP format file`

## 範例<a name="examples"></a>
下列範例使用以上所建立的資料庫、資料檔案與格式檔案。

### **使用 bcp 與字元格式匯出資料**<a name="bcp_char_export"></a>
**-c** 參數與 **OUT** 命令。  注意︰後續所有範例皆會使用此範例中所建立的資料檔案。  請在命令提示字元之下，輸入下列命令：

```cmd
bcp TestDatabase.dbo.myChar OUT D:\BCP\myChar.bcp -T -c

REM Review results
NOTEPAD D:\BCP\myChar.bcp
```

### **不使用格式檔案而使用 bcp 與字元格式匯入資料**<a name="bcp_char_import"></a>
**-c** 參數與 **IN** 命令。  請在命令提示字元之下，輸入下列命令：

```cmd
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myChar;"

REM Import data
bcp TestDatabase.dbo.myChar IN D:\BCP\myChar.bcp -T -c

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.myChar;"
```

### **使用 bcp 與字元格式匯入非 XML 格式檔案的資料**<a name="bcp_char_import_fmt"></a>
**-c** 與 **-f** 參數與 **IN** 命令。  請在命令提示字元之下，輸入下列命令：

```cmd
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myChar;"

REM Import data
bcp TestDatabase.dbo.myChar IN D:\BCP\myChar.bcp -f D:\BCP\myChar.fmt -T

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.myChar;"
```

### **不使用格式檔案而使用 BULK INSERT 與字元格式**<a name="bulk_char"></a>
**DATAFILETYPE** 引數。  請在 Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) 中執行下列 Transact-SQL：

```sql
TRUNCATE TABLE TestDatabase.dbo.myChar; -- for testing
BULK INSERT TestDatabase.dbo.myChar
    FROM 'D:\BCP\myChar.bcp'
    WITH (
        DATAFILETYPE = 'Char'
        );

-- review results
SELECT * FROM TestDatabase.dbo.myChar;
```

### **對非 XML 格式檔案使用 BULK INSERT 與字元格式**<a name="bulk_char_fmt"></a>
**FORMATFILE** 引數。  請在 Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) 中執行下列 Transact-SQL：

```sql
TRUNCATE TABLE TestDatabase.dbo.myChar; -- for testing
BULK INSERT TestDatabase.dbo.myChar
   FROM 'D:\BCP\myChar.bcp'
   WITH (
        FORMATFILE = 'D:\BCP\myChar.fmt'
        );

-- review results
SELECT * FROM TestDatabase.dbo.myChar;
```

### **對非 XML 格式檔案使用 OPENROWSET 與字元格式**<a name="openrowset_char_fmt"></a>
**FORMATFILE** 引數。  請在 Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) 中執行下列 Transact-SQL：

```sql
TRUNCATE TABLE TestDatabase.dbo.myChar;  -- for testing
INSERT INTO TestDatabase.dbo.myChar
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myChar.bcp', 
        FORMATFILE = 'D:\BCP\myChar.fmt'  
        ) AS t1;

-- review results
SELECT * FROM TestDatabase.dbo.myChar;
```
  
## 相關工作<a name="RelatedTasks"></a>  
若要使用大量匯入或大量匯出的資料格式 
  
-   [從舊版 SQL Server 匯入原生與字元格式資料](../../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [使用原生格式匯入或匯出資料 &#40;SQL Server&#41;](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [使用 Unicode 字元格式匯入或匯出資料 &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [使用 Unicode 原生格式匯入或匯出資料 &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
## <a name="see-also"></a>另請參閱  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [從舊版 SQL Server 匯入原生與字元格式資料](../../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
  

