---
title: "使用 Unicode 字元格式匯入或匯出資料 (SQL Server) | Microsoft 文件"
ms.custom: 
ms.date: 09/30/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: import-export
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-bulk-import-export
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data formats [SQL Server], Unicode character
- Unicode [SQL Server], bulk importing and exporting
ms.assetid: 74342a11-c1c0-4746-b482-7f3537744a70
caps.latest.revision: "37"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 5fd105a2da0e4822ee3da0b2f8929f70d0185cb5
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="use-unicode-character-format-to-import-or-export-data-sql-server"></a>使用 Unicode 字元格式匯入或匯出資料 (SQL Server)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] 使用含有擴充/DBCS 字元的資料檔案在多個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體之間大量傳送資料時，建議使用 Unicode 字元格式。 Unicode 字元資料格式可允許從伺服器匯出資料時所使用的字碼頁，與執行作業之用戶端所使用的字碼頁不同。 在此情況下，使用 Unicode 字元格式具有下列優點：  
  
* 如果來源資料和目的地資料都是 Unicode 資料類型，使用 Unicode 字元格式可保留所有的字元資料。  
  
* 若來源資料及目的地資料不是 Unicode 資料類型，則使用 Unicode 字元格式有助於將遺失來源資料中，目的地無法呈現之擴充字元的可能性降至最低。

|本主題內容：|
|---|
|[使用 Unicode 字元格式的注意事項](#considerations)|
|[使用 Unicode 字元格式、bcp 與格式檔案的特殊注意事項](#special_considerations)|
|[Unicode 字元格式的命令選項](#command_options)|
|[範例測試條件](#etc)<br />&emsp;&#9679;&emsp;[範例資料表](#sample_table)<br />&emsp;&#9679;&emsp;[範例非 XML 格式檔案](#nonxml_format_file)|
|[範例](#examples)<br />&emsp;&#9679;&emsp;[使用 BCP 與 Unicode 字元格式匯出資料](#bcp_widechar_export)<br />&emsp;&#9679;&emsp;[不使用格式檔案而使用 BCP 與 Unicode 字元格式匯入資料](#bcp_widechar_import)<br />&emsp;&#9679;&emsp;[使用 BCP 與 Unicode 字元格式匯入非 XML 格式檔案的資料](#bcp_widechar_import_fmt)<br />&emsp;&#9679;&emsp;[不使用格式檔案而使用 BULK INSERT 與 Unicode 字元格式](#bulk_widechar)<br />&emsp;&#9679;&emsp;[對非 XML 格式檔案使用 BULK INSERT 與 Unicode 字元格式](#bulk_widechar_fmt)<br />&emsp;&#9679;&emsp;[對非 XML 格式檔案使用 OPENROWSET 與 Unicode 字元格式](#openrowset_widechar_fmt)|
|[相關工作](#RelatedTasks)<p>                                                                                                                                                                                                                  </p>|
 
## 使用 Unicode 字元格式的注意事項<a name="considerations"></a>
使用字元格式時，請考慮下列事項：  

* [bcp 公用程式](../../tools/bcp-utility.md)預設會使用定位字元分隔字元資料欄位，並使用新行字元終止記錄。  如需如何指定其他結束字元的相關資訊，請參閱[指定欄位與資料列結束字元 &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)。

* 儲存在 Unicode 字元格式資料檔的 [sql_variant](../../t-sql/data-types/sql-variant-transact-sql.md) 資料，其操作方式和在字元格式資料檔中相同，不同之處在於資料是儲存為 [nchar](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)，而非 [char](../../t-sql/data-types/char-and-varchar-transact-sql.md) 資料。 如需詳細資訊，請參閱 [定序和 Unicode 支援](../../relational-databases/collations/collation-and-unicode-support.md)。  

## 使用 Unicode 字元格式、bcp 與格式檔案的特殊注意事項<a name="special_considerations"></a>
Unicode 字元格式資料檔遵循 Unicode 檔案的慣例。  檔案的前兩個位元組是十六進位數字 0xFFFE。  這些位元組會用為位元組順序標記 (BOM)，指定將高位位元組儲存到檔案中時的先後順序。  [bcp 公用程式](../../tools/bcp-utility.md) 可能會錯誤解譯 BOM，進而導致匯入程序失敗；因此，您可能會收到類似如下的錯誤訊息︰
```
Starting copy...
SQLState = 22005, NativeError = 0
Error = [Microsoft][ODBC Driver 13 for SQL Server]Invalid character value for cast specification
```

下列情況可能會致使 BOM 解譯錯誤︰
* 使用了 [bcp 公用程式](../../tools/bcp-utility.md) **-w** 參數指定 Unicode 字元。

* 使用了格式檔案。

* 資料檔案中的第一個欄位不是字元。

請考慮下列因應措施是否適用於情況︰
* 不使用格式檔案。  以下是此因應措施的範例。您可以參閱 [不使用格式檔案而使用 bcp 與 Unicode 字元格式匯入資料](#bcp_widechar_import)。

* 使用 **-c** 參數而不使用 **-w**。

* 使用原生格式重新匯出資料。

* 使用 [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 或 [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md)。  以下是這些因應措施的範例。您可以參閱 [對非 XML 格式檔案使用 BULK INSERT 與 Unicode 字元格式](#bulk_widechar_fmt) [對非 XML 格式檔案使用 OPENROWSET 與 Unicode 字元格式](#openrowset_widechar_fmt)。
 
* 在目的地資料表中手動插入第一筆記錄，然後使用 **-F 2** 參數強制匯入從第二筆記錄開始。

* 在資料檔案中手動插入虛擬的第一筆資料，然後使用 **-F 2** 參數強制匯入從第二筆記錄開始。  以下是此因應措施的範例。您可以參閱 [使用 bcp 與 Unicode 字元格式匯入非 XML 格式檔案的資料](#bcp_widechar_import_fmt)。

* 使用第一個資料行為字元資料類型的暫存資料表，或

* 重新匯出資料，並變更資料欄位順序，讓第一個資料欄位為字元。  接著使用格式檔案，將資料欄位重新對應到資料表中的實際順序。  如需範例，請參閱 [使用格式檔案將資料表資料行對應至資料檔案的欄位 (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)。
  
## Unicode 字元格式的命令選項<a name="command_options"></a>  
您可以將 Unicode 字元格式資料匯入資料表，方法是使用 [bcp](../../tools/bcp-utility.md)、[BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 或 [INSERT ...SELECT * FROM OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md)。對於 [bcp](../../tools/bcp-utility.md) 命令或 [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 陳述式，您可以在陳述式中指定資料格式。  對於 [INSERT...SELECT * FROM OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) 陳述式。您必須在格式檔案中指定資料格式。  
  
下列命令列選項支援 Unicode 字元格式：  
  
|Command|選項|描述|  
|-------------|------------|-----------------|  
|bcp|**-w**|使用 Unicode 字元格式。|  
|BULK INSERT|DATAFILETYPE **='widechar'**|大量匯入資料時，使用 Unicode 字元格式。|  
|OPENROWSET|N/A|必須使用格式檔案|
  
> [!NOTE]
>  或者，您可以在格式檔案中按照每個欄位指定格式。 如需詳細資訊，請參閱 [匯入或匯出資料的格式檔案 &#40;SQL Server&#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)＞。
  
## 範例測試條件<a name="etc"></a>  
本主題中的範例採用下列定義的資料表、資料檔案與格式檔案。

### **範例資料表**<a name="sample_table"></a>
下列指令碼會建立測試資料庫、名為 `myWidechar` 的資料表，以及在資料表中填入一些初始值。  請在 Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) 中執行下列 Transact-SQL：
```sql
CREATE DATABASE TestDatabase;
GO

USE TestDatabase;
CREATE TABLE dbo.myWidechar ( 
    PersonID smallint NOT NULL,
    FirstName nvarchar(25) NOT NULL,
    LastName nvarchar(30) NOT NULL,
    BirthDate date,
    AnnualSalary money
);

-- Populate table
INSERT TestDatabase.dbo.myWidechar
VALUES 
(1, N'ϴAnthony', N'Grosse', '02-23-1980', 65000.00),
(2, N'❤Alica', N'Fatnowna', '11-14-1963', 45000.00),
(3, N'☎Stella', N'Rossenhain', '03-02-1992', 120000.00);

-- Review Data
SELECT * FROM TestDatabase.dbo.myWidechar;
```

### **範例非 XML 格式檔案**<a name="nonxml_format_file"></a>
SQL Server 支援兩種類型的格式檔案：非 XML 格式和 XML 格式。  非 XML 格式是舊版 SQL Server 所支援的原始格式。  如需詳細資訊，請參閱 [非 XML 格式檔案 (SQL Server)](../../relational-databases/import-export/non-xml-format-files-sql-server.md) 。  下列命令將使用 [bcp 公用程式](../../tools/bcp-utility.md) ，根據 `myWidechar.fmt`的結構描述產生非 XML 格式檔案 `myWidechar`。  使用 [bcp](../../tools/bcp-utility.md) 命令建立格式檔案時，請指定 **format** 引數並使用 **nul** 取代資料檔案路徑。  format 選項也需要 **-f** 選項。  此外，以此範例為例，限定詞 **c** 會用於指定字元資料， **T** 會用於指定使用整合式安全性的信任連線。  請在命令提示字元之下，輸入下列命令：

```
bcp TestDatabase.dbo.myWidechar format nul -f D:\BCP\myWidechar.fmt -T -w

REM Review file
Notepad D:\BCP\myWidechar.fmt
```

> [!IMPORTANT]
> 請確認您的非 XML 格式檔案以歸位字元\換行字元結尾。  否則您可能會收到下列錯誤訊息︰
> 
> `SQLState = S1000, NativeError = 0`  
> `Error = [Microsoft][ODBC Driver 13 for SQL Server]I/O error while reading BCP format file`


## 範例<a name="examples"></a>
下列範例使用以上所建立的資料庫、資料檔案與格式檔案。

### **使用 bcp 與 Unicode 字元格式匯出資料**<a name="bcp_widechar_export"></a>
**-w** 參數與 **OUT** 命令。  注意︰後續所有範例皆會使用此範例中所建立的資料檔案。  請在命令提示字元之下，輸入下列命令：
```
bcp TestDatabase.dbo.myWidechar OUT D:\BCP\myWidechar.bcp -T -w

REM Review results
NOTEPAD D:\BCP\myWidechar.bcp
```

### **不使用格式檔案而使用 bcp 與 Unicode 字元格式匯入資料**<a name="bcp_widechar_import"></a>
**-w** 參數與 **IN** 命令。  請在命令提示字元之下，輸入下列命令：
```
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myWidechar;"

REM Import data
bcp TestDatabase.dbo.myWidechar IN D:\BCP\myWidechar.bcp -T -w

REM Review results is SSMS
```

### **使用 bcp 與 Unicode 字元格式匯入非 XML 格式檔案的資料**<a name="bcp_widechar_import_fmt"></a>
**-w** 與 **-f** 參數與 **IN** 命令。  因為此範例涉及 bcp、格式檔案與 Unicode 字元，以及資料檔案中的第一個資料欄位為字元，所以必須使用因應措施。  請參閱 [使用 Unicode 字元格式、bcp 與格式檔案的特殊注意事項](#special_considerations)。  資料檔案 `myWidechar.bcp` 會因為額外新增一筆 "dummy" 記錄而有所改變。 `-F 2` 參數會略過該筆記錄。

在命令提示字元中輸入下列命令，然後執行修改步驟︰
```
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myWidechar;"

REM Open data file
Notepad D:\BCP\myWidechar.bcp
REM Copy first record and then paste as new first record.  This additional record is the "dummy" record.
REM Close file.

REM Import data instructing bcp to skip dummy record with the -F 2 switch.
bcp TestDatabase.dbo.myWidechar IN D:\BCP\myWidechar.bcp -f D:\BCP\myWidechar.fmt -T -F 2

REM Review results is SSMS

REM Return data file to original state for usage in other examples
bcp TestDatabase.dbo.myWidechar OUT D:\BCP\myWidechar.bcp -T -w
```
  
### **不使用格式檔案而使用 BULK INSERT 與 Unicode 字元格式**<a name="bulk_widechar"></a>
**DATAFILETYPE** 引數。  請在 Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) 中執行下列 Transact-SQL：
```sql
TRUNCATE TABLE TestDatabase.dbo.myWidechar; -- for testing
BULK INSERT TestDatabase.dbo.myWidechar
    FROM 'D:\BCP\myWidechar.bcp'
    WITH (
        DATAFILETYPE = 'widechar'
        );

-- review results
SELECT * FROM TestDatabase.dbo.myWidechar;
```
  
### **對非 XML 格式檔案使用 BULK INSERT 與 Unicode 字元格式**<a name="bulk_widechar_fmt"></a>
**FORMATFILE** 引數。  請在 Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) 中執行下列 Transact-SQL：
```sql
TRUNCATE TABLE TestDatabase.dbo.myWidechar; -- for testing
BULK INSERT TestDatabase.dbo.myWidechar
   FROM 'D:\BCP\myWidechar.bcp'
   WITH (
        FORMATFILE = 'D:\BCP\myWidechar.fmt'
        );

-- review results
SELECT * FROM TestDatabase.dbo.myWidechar;
```
  
### **對非 XML 格式檔案使用 OPENROWSET 與 Unicode 字元格式**<a name="openrowset_widechar_fmt"></a>
**FORMATFILE** 引數。  請在 Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) 中執行下列 Transact-SQL：
```sql
TRUNCATE TABLE TestDatabase.dbo.myWidechar;  -- for testing
INSERT INTO TestDatabase.dbo.myWidechar
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myWidechar.bcp', 
        FORMATFILE = 'D:\BCP\myWidechar.fmt'  
        ) AS t1;

-- review results
SELECT * FROM TestDatabase.dbo.myWidechar;
```
 
  
## 相關工作<a name="RelatedTasks"></a>
若要使用大量匯入或大量匯出的資料格式  
-   [從舊版 SQL Server 匯入原生與字元格式資料](../../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [使用字元格式匯入或匯出資料 &#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [使用原生格式匯入或匯出資料 &#40;SQL Server&#41;](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [使用 Unicode 原生格式匯入或匯出資料 &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
## <a name="see-also"></a>另請參閱  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [定序和 Unicode 支援](../../relational-databases/collations/collation-and-unicode-support.md)  
  
  
