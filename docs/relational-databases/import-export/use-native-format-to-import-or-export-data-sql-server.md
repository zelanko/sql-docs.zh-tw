---
title: "使用原生格式匯入或匯出資料 (SQL Server) | Microsoft 文件"
ms.custom: 
ms.date: 09/30/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-bulk-import-export
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- native data format [SQL Server]
- data formats [SQL Server], native
ms.assetid: eb279b2f-0f1f-428f-9b8f-2a7fc495b79f
caps.latest.revision: 43
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: dd20fe12af6f1dcaf378d737961bc2ba354aabe5
ms.openlocfilehash: 889a414674b3b87ca528f1af2a54261c723c4555
ms.contentlocale: zh-tw
ms.lasthandoff: 10/04/2017

---
# <a name="use-native-format-to-import-or-export-data-sql-server"></a>使用原生格式匯入或匯出資料 (SQL Server)
在多個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體之間，使用不包含任何擴充/雙位元組字集 (DBCS) 字元的資料檔傳送大量資料時，建議使用原生格式。  

> [!NOTE]
>  若要在多個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體之間，使用包含擴充或 DBCS 字元的資料檔大量傳送資料，您應該使用 Unicode 原生格式。 如需詳細資訊，請參閱 [使用 Unicode 原生格式匯入或匯出資料 &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)。

原生格式會維持資料庫的原生資料類型。 原生格式的目的是為了在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表之間進行資料的高速資料傳送。 如果您使用格式檔案，則來源與目標資料表不需要相同。 資料傳送包含兩個步驟：  
  
1.  將來源資料表中的資料大量匯出到資料檔  
  
2.  將資料檔中的資料大量匯入目標資料表  
  
在相同資料表之間使用原生格式，可避免資料類型與字元格式間進行不需要的來回轉換，因而可節省時間及空間。 不過，若要取得最佳的傳輸率，必須針對資料格式化做一些檢查。 若要防止所載入的資料發生問題，請參閱下列限制清單。  

|本主題內容：|
|---|
|[限制](#restrictions)|
|[bcp 如何處理原生格式的資料](#considerations)|
|[原生格式的命令選項](#command_options)|
|[範例測試條件](#etc)<br /><br />&emsp;&#9679;&emsp;[範例資料表](#sample_table)<br />&emsp;&#9679;&emsp;[範例非 XML 格式檔案](#nonxml_format_file)|
|[範例](#examples)<br />&emsp;&#9679;&emsp;[使用 BCP 與原生格式匯出資料](#bcp_native_export)<br />&emsp;&#9679;&emsp;[不使用格式檔案而使用 BCP 與原生格式匯入資料](#bcp_native_import)<br />&emsp;&#9679;&emsp;[使用 BCP 與原生格式匯入非 XML 格式檔案的資料](#bcp_native_import_fmt)<br />&emsp;&#9679;&emsp;[不使用格式檔案而使用 BULK INSERT 與原生格式](#bulk_native)<br />&emsp;&#9679;&emsp;[對非 XML 格式檔案使用 BULK INSERT 與原生格式](#bulk_native_fmt)<br />&emsp;&#9679;&emsp;[對非 XML 格式檔案使用 OPENROWSET 與原生格式](#openrowset_native_fmt)|
|[相關工作](#RelatedTasks)<p>                                                                                                                                                                                                                  </p>|

## 限制<a name="restrictions"></a>  
若要以原生格式成功匯入資料，請確定：  
  
-   資料檔具有原生格式。  
  
-   目標資料表必須與資料檔相容 (具有正確的資料行數目、資料類型、長度、NULL 狀態等等)，否則您必須使用格式檔案，將每一個欄位對應到它的對應資料行。  
  
    > [!NOTE]
    >  如果您從與目標資料表不相符的檔案匯入資料，匯入作業或許會成功，但是插入目標資料表的資料值可能不正確。 原因是檔案中的資料是使用目標資料表的格式來解譯。 因此，任何不相符都會導致插入的值不正確。 不過，這樣的不相符在任何情況下，都不會導致資料庫中發生邏輯或實體不一致性。  
  
     如需使用格式檔案的詳細資訊，請參閱[匯入或匯出資料的格式檔案 &#40;SQL Server&#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)。  
  
 成功的匯入作業不會損毀目標資料表。  
  
## bcp 如何處理原生格式的資料<a name="considerations"></a>
 本節討論 **bcp** 公用程式如何匯出及匯入原生格式資料的特殊考量。  
  
-   非字元資料  
  
     [bcp 公用程式](../../tools/bcp-utility.md) 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的內部二進位資料格式，將資料表中的非字元資料寫入資料檔案。  
  
-   [char](../../t-sql/data-types/char-and-varchar-transact-sql.md) 或 [varchar](../../t-sql/data-types/char-and-varchar-transact-sql.md) 資料  
  
     在每一個 [char](../../t-sql/data-types/char-and-varchar-transact-sql.md) 或 [varchar](../../t-sql/data-types/char-and-varchar-transact-sql.md) 欄位的開頭， [bcp](../../tools/bcp-utility.md) 都會加入前置長度。  
  
    > [!IMPORTANT]
    >  使用原生模式時， [bcp 公用程式](../../tools/bcp-utility.md) 會先將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的字元轉換為 OEM 字元，然後再複製到資料檔案。 [bcp 公用程式](../../tools/bcp-utility.md) 會先將資料檔案中的字元轉換為 ANSI 字元，然後再大量匯入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表。 在進行這些轉換期間，可能會遺失擴充字元。 如有擴充字元，請使用 Unicode 原生格式或指定字碼頁。
  
-   [sql_variant](../../t-sql/data-types/sql-variant-transact-sql.md) 資料  
  
     如果 [sql_variant](../../t-sql/data-types/sql-variant-transact-sql.md) 資料以原生格式資料檔儲存為 SQLVARIANT，則資料會維持它所有的特性。 用來記錄每一個資料值的資料類型的中繼資料，會與資料值一起儲存。 中繼資料是用來以目的地 [sql_variant](../../t-sql/data-types/sql-variant-transact-sql.md) 資料行中相同的資料類型，重新建立資料值。  
  
     如果目的地資料行的資料類型不是 [sql_variant](../../t-sql/data-types/sql-variant-transact-sql.md)，則每一個資料值將依照隱含資料轉換的一般規則，轉換為目的地資料行的資料類型。 如果資料轉換期間發生錯誤，將會回復目前批次。 任何在 [sql_variant](../../t-sql/data-types/char-and-varchar-transact-sql.md) 資料行之間傳送的 [char](../../t-sql/data-types/char-and-varchar-transact-sql.md) 及 [varchar](../../t-sql/data-types/sql-variant-transact-sql.md) 值，都可能有字碼頁轉換問題。  
  
     如需資料轉換的詳細資訊，請參閱[資料類型轉換 &#40;Database Engine&#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)。  
  
## 原生格式的命令選項<a name="command_options"></a>  
您可以將原生格式資料匯入資料表，方法是使用 [bcp](../../tools/bcp-utility.md)、[BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 或 [INSERT ...SELECT * FROM OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md)。對於 [bcp](../../tools/bcp-utility.md) 命令或 [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 陳述式，您可以在陳述式中指定資料格式。  對於 [INSERT...SELECT * FROM OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) 陳述式，您必須在格式檔案中指定資料格式。  

下列命令選項支援原生格式：  

|Command|選項|描述|  
|-------------|------------|-----------------|  
|bcp|**-n**|指定 bcp 公用程式使用資料的原生資料類型。*|  
|BULK INSERT|DATAFILETYPE **='native'**|使用資料的原生或 widenative 資料類型。 請注意，如果利用了格式檔案指定資料類型，就不需要 DATAFILETYPE。|  
|OPENROWSET|N/A|必須使用格式檔案|

  
 \*若要將原生 (**-n**) 資料載入與舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用戶端相容的格式，請使用 **-V** 參數。 如需詳細資訊，請參閱 [從舊版 SQL Server 匯入原生與字元格式資料](../../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)。  
  
> [!NOTE]
>  或者，您可以在格式檔案中按照每個欄位指定格式。 如需詳細資訊，請參閱 [匯入或匯出資料的格式檔案 &#40;SQL Server&#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)＞。
  

## 範例測試條件<a name="etc"></a>  
本主題中的範例採用下列定義的資料表、資料檔案與格式檔案。

### **範例資料表**<a name="sample_table"></a>
下列指令碼會建立測試資料庫、名為 `myNative` 的資料表，以及在資料表中填入一些初始值。  請在 Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) 中執行下列 Transact-SQL：

```sql
CREATE DATABASE TestDatabase;
GO

USE TestDatabase;
CREATE TABLE dbo.myNative ( 
   PersonID smallint NOT NULL,
   FirstName varchar(25) NOT NULL,
   LastName varchar(30) NOT NULL,
   BirthDate date,
   AnnualSalary money
   );

-- Populate table
INSERT TestDatabase.dbo.myNative
VALUES 
(1, 'Anthony', 'Grosse', '1980-02-23', 65000.00),
(2, 'Alica', 'Fatnowna', '1963-11-14', 45000.00),
(3, 'Stella', 'Rossenhain', '1992-03-02', 120000.00);

-- Review Data
SELECT * FROM TestDatabase.dbo.myNative;
```

### **範例非 XML 格式檔案**<a name="nonxml_format_file"></a>
SQL Server 支援兩種類型的格式檔案：非 XML 格式和 XML 格式。  非 XML 格式是舊版 SQL Server 所支援的原始格式。  如需詳細資訊，請參閱 [非 XML 格式檔案 (SQL Server)](../../relational-databases/import-export/non-xml-format-files-sql-server.md) 。  下列命令將使用 [bcp 公用程式](../../tools/bcp-utility.md) ，根據 `myNative.fmt`的結構描述產生非 XML 格式檔案 `myNative`。  使用 [bcp](../../tools/bcp-utility.md) 命令建立格式檔案時，請指定 **format** 引數並使用 **nul** 取代資料檔案路徑。  format 選項也需要 **-f** 選項。  此外，以此範例為例，限定詞 **c** 會用於指定字元資料， **T** 會用於指定使用整合式安全性的信任連線。  請在命令提示字元之下，輸入下列命令：

```cmd
bcp TestDatabase.dbo.myNative format nul -f D:\BCP\myNative.fmt -T -n 

REM Review file
Notepad D:\BCP\myNative.fmt
```

> [!IMPORTANT]
> 請確認您的非 XML 格式檔案以歸位字元\換行字元結尾。  否則您可能會收到下列錯誤訊息︰
> 
> `SQLState = S1000, NativeError = 0`  
> `Error = [Microsoft][ODBC Driver 13 for SQL Server]I/O error while reading BCP format file`

## 範例<a name="examples"></a>
下列範例使用以上所建立的資料庫、資料檔案與格式檔案。

### **使用 bcp 與原生格式匯出資料**<a name="bcp_native_export"></a>
**-n** 參數與 **OUT** 命令。  注意︰後續所有範例皆會使用此範例中所建立的資料檔案。  請在命令提示字元之下，輸入下列命令：

```cmd
bcp TestDatabase.dbo.myNative OUT D:\BCP\myNative.bcp -T -n

REM Review results
NOTEPAD D:\BCP\myNative.bcp
```

### **使用 bcp 與原生格式匯入資料**<a name="bcp_native_import"></a>
**-n** 參數與 **IN** 命令。  請在命令提示字元之下，輸入下列命令：

```cmd
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myNative;"

REM Import data
bcp TestDatabase.dbo.myNative IN D:\BCP\myNative.bcp -T -n

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.myNative;"
```

### **使用 bcp 與原生格式匯入非 XML 格式檔案的資料**<a name="bcp_native_import_fmt"></a>
**-n** 資料行之間傳送的 **-f** 參數與 **IN** 命令。  請在命令提示字元之下，輸入下列命令：

```cmd
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myNative;"

REM Import data
bcp TestDatabase.dbo.myNative IN D:\BCP\myNative.bcp -f D:\BCP\myNative.fmt -T

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.myNative;"
```

### **不使用格式檔案而使用 BULK INSERT 與原生格式**<a name="bulk_native"></a>
**DATAFILETYPE** 引數。  請在 Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) 中執行下列 Transact-SQL：

```sql
TRUNCATE TABLE TestDatabase.dbo.myNative; -- for testing
BULK INSERT TestDatabase.dbo.myNative
    FROM 'D:\BCP\myNative.bcp'
    WITH (
        DATAFILETYPE = 'native'
        );

-- review results
SELECT * FROM TestDatabase.dbo.myNative;
```

### **對非 XML 格式檔案使用 BULK INSERT 與原生格式**<a name="bulk_native_fmt"></a>
**FORMATFILE** 引數。  請在 Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) 中執行下列 Transact-SQL：

```sql
TRUNCATE TABLE TestDatabase.dbo.myNative; -- for testing
BULK INSERT TestDatabase.dbo.myNative
   FROM 'D:\BCP\myNative.bcp'
   WITH (
        FORMATFILE = 'D:\BCP\myNative.fmt'
        );

-- review results
SELECT * FROM TestDatabase.dbo.myNative;
```

### **對非 XML 格式檔案使用 OPENROWSET 與原生格式**<a name="openrowset_native_fmt"></a>
**FORMATFILE** 引數。  請在 Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) 中執行下列 Transact-SQL：

```sql
TRUNCATE TABLE TestDatabase.dbo.myNative;  -- for testing
INSERT INTO TestDatabase.dbo.myNative
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myNative.bcp', 
        FORMATFILE = 'D:\BCP\myNative.fmt'  
        ) AS t1;

-- review results
SELECT * FROM TestDatabase.dbo.myNative;
```
  
## 相關工作<a name="RelatedTasks"></a>
若要使用大量匯入或大量匯出的資料格式 
  
-   [從舊版 SQL Server 匯入原生與字元格式資料](../../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [使用字元格式匯入或匯出資料 &#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [使用 Unicode 字元格式匯入或匯出資料 &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [使用 Unicode 原生格式匯入或匯出資料 &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
## <a name="see-also"></a>另請參閱  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [sql_variant &#40;Transact-SQL&#41;](../../t-sql/data-types/sql-variant-transact-sql.md)   
 [從舊版 SQL Server 匯入原生與字元格式資料](../../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [使用 Unicode 原生格式匯入或匯出資料 &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
  

