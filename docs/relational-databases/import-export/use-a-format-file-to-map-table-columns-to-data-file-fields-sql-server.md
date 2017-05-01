---
title: "使用格式檔案將資料表資料行對應至資料檔案欄位 (SQL Server) | Microsoft 文件"
ms.custom: 
ms.date: 09/19/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-bulk-import-export
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mapping columns to fields during import [SQL Server]
- format files [SQL Server], mapping columns to fields
ms.assetid: e7ee4f7e-24c4-4eb7-84d2-41e57ccc1ef1
caps.latest.revision: 40
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d90982485ab979118f4f7b02881aa8ea53cc9818
ms.lasthandoff: 04/11/2017

---
# <a name="use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server"></a>使用格式檔案將資料表資料行對應至資料檔欄位 (SQL Server)
資料檔中包含的欄位順序可以與資料表中對應資料行的順序不同。 此主題呈現非 XML 與 XML 格式檔案，這些檔案已經過修改，以配合欄位順序與資料表資料行不同的資料檔。 已修改的格式檔案可將資料欄位對應到與它們對應的資料表資料行。  如需其他資訊，請參閱 [建立格式檔案 (SQL Server)](../../relational-databases/import-export/create-a-format-file-sql-server.md) 。

|外框|
|---|
|[範例測試條件](#etc)<br />&emsp;&#9679;&emsp;[範例資料表](#sample_table)<br />&emsp;&#9679;&emsp;[範例資料檔案](#sample_data_file)<br />[建立格式檔案](#create_format_file)<br />&emsp;&#9679;&emsp;[建立非 XML 格式檔案](#nonxml_format_file)<br />&emsp;&#9679;&emsp;[修改非 XML 格式檔案](#modify_nonxml_format_file)<br />&emsp;&#9679;&emsp;[建立 XML 格式檔案](#xml_format_file)<br />&emsp;&#9679;&emsp;[修改 XML 格式檔案](#modify_xml_format_file)<br />[使用格式檔案匯入資料，將資料表資料行對應至資料檔案欄位](#import_data)<br />&emsp;&#9679;&emsp;[使用 BCP 和非 XML 格式檔案](#bcp_nonxml)<br />&emsp;&#9679;&emsp;[使用 BCP 和 XML 格式檔案](#bcp_xml)<br />&emsp;&#9679;&emsp;[使用 BULK INSERT 和非 XML 格式檔案](#bulk_nonxml)<br />&emsp;&#9679;&emsp;[使用 BULK INSERT 和 XML 格式檔案](#bulk_xml)<br />&emsp;&#9679;&emsp;[使用 OPENROWSET(BULK...) 和非 XML 格式檔案](#openrowset_nonxml)<br />&emsp;&#9679;&emsp;[使用 OPENROWSET(BULK...) 和 XML 格式檔案](#openrowset_xml)<p>                                                                                                                                                                                                                  </p>|

> [!NOTE]  
>  您可以透過下列項目，使用非 XML 或 XML 格式檔案，將資料檔案大量匯入至資料表：[bcp 公用程式](../../tools/bcp-utility.md)命令、[BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 陳述式或 INSERT ...SELECT * FROM [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) 陳述式。 如需詳細資訊，請參閱[使用格式檔案大量匯入資料 &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)。  

## 範例測試條件<a name="etc"></a>  
本主題中的修改格式檔案範例是以下面定義的資料表和資料檔案為基礎。

### 範例資料表<a name="sample_table"></a>
下列指令碼會建立測試資料庫和名為 `myRemap`的資料表。  在 Microsoft SQL Server Management Studio (SSMS) 中執行下列 Transact-SQL：
```tsql
CREATE DATABASE TestDatabase;
GO

USE TestDatabase;
CREATE TABLE myRemap
   (
   PersonID smallint,
   FirstName varchar(25),
   LastName varchar(30),
   Gender char(1)
   );
```

### 範例資料檔案<a name="sample_data_file"></a>
下面的資料會依照 `FirstName` 資料表所示，以相反順序顯示 `LastName` 和 `myRemap`。  使用 [記事本] 建立空白檔案 `D:\BCP\myRemap.bcp` ，並插入下列資料：
```
1,Grosse,Anthony,M
2,Fatnowna,Alica,F
3,Rosenhain,Stella,F
```

## 建立格式檔案<a name="create_format_file"></a>
若要從 `myRemap.bcp` 大量匯入資料到 `myRemap` 資料表中，格式檔案必須執行下列工作：
* 將第一個資料欄位對應到第一個資料行 `PersonID`。
* 將第二個資料欄位對應到第三個資料行 `LastName`。
* 將第三個資料欄位對應到第二個資料行 `FirstName`。
* 將第四個資料欄位對應到第四個資料行 `Gender`。

建立格式檔案的最簡單方法是使用 [bcp 公用程式](../../tools/bcp-utility.md)。  首先，從現有的資料表建立基底格式檔案。  其次，修改基底格式檔案以反映實際的資料檔案。

### 建立非 XML 格式檔案<a name="nonxml_format_file"></a>
如需詳細資訊，請參閱 [非 XML 格式檔案 (SQL Server)](../../relational-databases/import-export/non-xml-format-files-sql-server.md) 。 下列命令將使用 [bcp 公用程式](../../tools/bcp-utility.md) ，根據 `myRemap.fmt`的結構描述產生非 XML 格式檔案 `myRemap`。  另外還會使用限定詞 `c` 來指定字元資料，使用 `t,` 來指定逗號作為欄位結束字元，並使用 `T` 來指定使用整合式安全性的信任連接。  請在命令提示字元之下，輸入下列命令：
```
bcp TestDatabase.dbo.myRemap format nul -c -f D:\BCP\myRemap.fmt -t, -T
```
### 修改非 XML 格式檔案 <a name="modify_nonxml_format_file"></a>
請參閱 [非 XML 格式檔案的結構](../../relational-databases/import-export/non-xml-format-files-sql-server.md#Structure) 以了解此術語。  在 [記事本] 中開啟 `D:\BCP\myRemap.fmt` 並執行下列修改：
1) 重新排列格式檔案資料列的順序，讓資料列的順序與 `myRemap.bcp`中的資料順序相同。
2) 確定主機檔案欄位的順序值是連續的。
3) 確定最後一個格式檔案資料列後面沒有歸位字元。

比較下列變更：     
**之前**
```
13.0
4
1       SQLCHAR    0       7       ","      1     PersonID               ""
2       SQLCHAR    0       25      ","      2     FirstName              SQL_Latin1_General_CP1_CI_AS
3       SQLCHAR    0       30      ","      3     LastName               SQL_Latin1_General_CP1_CI_AS
4       SQLCHAR    0       1       "\r\n"   4     Gender                 SQL_Latin1_General_CP1_CI_AS

```
**After**
```
13.0
4
1       SQLCHAR    0       7       ","      1     PersonID               ""
2       SQLCHAR    0       30      ","      3     LastName               SQL_Latin1_General_CP1_CI_AS
3       SQLCHAR    0       25      ","      2     FirstName              SQL_Latin1_General_CP1_CI_AS
4       SQLCHAR    0       1       "\r\n"   4     Gender                 SQL_Latin1_General_CP1_CI_AS

```
修改的格式檔案現在會反映：
* `myRemap.bcp` 中的第一個資料欄位會對應到第一個資料行 ` myRemap.. PersonID`
* `myRemap.bcp` 中的第二個資料欄位會對應到第三個資料行 `myRemap.. LastName`
* `myRemap.bcp` 中的第三個資料欄位會對應到第二個資料行 `myRemap.. FirstName`
* `myRemap.bcp` 中的第四個資料欄位會對應到第四個資料行 ` myRemap.. Gender`

### 建立 XML 格式檔案 <a name="xml_format_file"></a>  
如需詳細資訊，請參閱 [XML 格式檔案 (SQL Server)](../../relational-databases/import-export/xml-format-files-sql-server.md) 。  下列命令將使用 [bcp 公用程式](../../tools/bcp-utility.md) ，根據 `myRemap.xml`的結構描述建立 XML 格式檔案 `myRemap`。  另外還會使用限定詞 `c` 來指定字元資料，使用 `t,` 來指定逗號作為欄位結束字元，並使用 `T` 來指定使用整合式安全性的信任連接。  必須使用 `x` 限定詞來產生 XML 格式檔案。  請在命令提示字元之下，輸入下列命令：
```
bcp TestDatabase.dbo.myRemap format nul -c -x -f D:\BCP\myRemap.xml -t, -T
```
### 修改 XML 格式檔案 <a name="modify_xml_format_file"></a>
請參閱 [XML 格式檔案的結構描述語法](../../relational-databases/import-export/xml-format-files-sql-server.md#StructureOfXmlFFs) 以了解此術語。  在 [記事本] 中開啟 `D:\BCP\myRemap.xml` 並執行下列修改：
1) 在格式檔案中宣告 \<FIELD> 元素的順序會是這些欄位出現在資料檔案中的順序，因此請將識別碼屬性 2 和 3 的 \<FIELD> 元素順序反轉。
2) 確定 \<FIELD> 識別碼屬性值是連續的。
3) \<ROW> 元素中的 \<COLUMN> 元素順序會定義大量作業傳回這些元素的順序。  XML 格式檔案會將本機名稱指派給每個 \<COLUMN> 元素，而此名稱與大量匯入作業之目標資料表中的資料行沒有任何關聯性。  \<COLUMN> 元素的順序與 \<RECORD> 定義中的 \<FIELD> 元素順序無關。  每個 \<COLUMN> 元素都會對應到 \<FIELD> 元素 (其識別碼是在 \<COLUMN> 元素的 SOURCE 屬性中指定)。  因此，\<COLUMN> SOURCE 的值是唯一需要修訂的屬性。  將 \<COLUMN> SOURCE 屬性 2 和 3 的順序反轉。

比較下列變更  
**之前**
```
\<?xml version="1.0"?>
\<BCPFORMAT xmlns="http://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
 <RECORD>
  \<FIELD ID="1" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="7"/>
  \<FIELD ID="2" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="25" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
  \<FIELD ID="3" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="30" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
  \<FIELD ID="4" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="1" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
 </RECORD>
 <ROW>
  \<COLUMN SOURCE="1" NAME="PersonID" xsi:type="SQLSMALLINT"/>
  \<COLUMN SOURCE="2" NAME="FirstName" xsi:type="SQLVARYCHAR"/>
  \<COLUMN SOURCE="3" NAME="LastName" xsi:type="SQLVARYCHAR"/>
  \<COLUMN SOURCE="4" NAME="Gender" xsi:type="SQLCHAR"/>
 </ROW>
</BCPFORMAT>
```
**After**
```
\<?xml version="1.0"?>
\<BCPFORMAT xmlns="http://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
 <RECORD>
  \<FIELD ID="1" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="7"/>
  \<FIELD ID="2" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="30" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
  \<FIELD ID="3" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="25" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
  \<FIELD ID="4" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="1" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
 </RECORD>
 <ROW>
  \<COLUMN SOURCE="1" NAME="PersonID" xsi:type="SQLSMALLINT"/>
  \<COLUMN SOURCE="3" NAME="FirstName" xsi:type="SQLVARYCHAR"/>
  \<COLUMN SOURCE="2" NAME="LastName" xsi:type="SQLVARYCHAR"/>
  \<COLUMN SOURCE="4" NAME="Gender" xsi:type="SQLCHAR"/>
 </ROW>
</BCPFORMAT>
```
修改的格式檔案現在會反映：
* 對應到 COLUMN 1 的 FIELD 1 會對應到第一個資料表資料行 `myRemap.. PersonID`
* 對應到 COLUMN 2 的 FIELD 2 會重新對應到第三個資料表資料行 `myRemap.. LastName`
* 對應到 COLUMN 3 的 FIELD 3 會重新對應到第二個資料表資料行 `myRemap.. FirstName`
* 對應到 COLUMN 4 的 FIELD 4 會對應到第四個資料表資料行 `myRemap.. Gender`


## 使用格式檔案匯入資料，將資料表資料行對應至資料檔案欄位<a name="import_data"></a>
下列範例會使用上面建立的資料庫、資料檔案和格式檔案。

### 使用 [bcp](../../tools/bcp-utility.md) 和 [非 XML 格式檔案](../../relational-databases/import-export/non-xml-format-files-sql-server.md)<a name="bcp_nonxml"></a>
請在命令提示字元之下，輸入下列命令：
```
bcp TestDatabase.dbo.myRemap IN D:\BCP\myRemap.bcp -f D:\BCP\myRemap.fmt -T
```

### 使用 [bcp](../../tools/bcp-utility.md) 和 [XML 格式檔案](../../relational-databases/import-export/xml-format-files-sql-server.md)<a name="bcp_xml"></a>
請在命令提示字元之下，輸入下列命令：
```
bcp TestDatabase.dbo.myRemap IN D:\BCP\myRemap.bcp -f D:\BCP\myRemap.xml -T
```

### 使用 [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 和 [非 XML 格式檔案](../../relational-databases/import-export/non-xml-format-files-sql-server.md)<a name="bulk_nonxml"></a>
在 Microsoft SQL Server Management Studio (SSMS) 中執行下列 Transact-SQL：
```tsql
USE TestDatabase;  
GO

TRUNCATE TABLE myRemap;
BULK INSERT dbo.myRemap   
   FROM 'D:\BCP\myRemap.bcp'   
   WITH (FORMATFILE = 'D:\BCP\myRemap.fmt');  
GO  

-- review results
SELECT * FROM TestDatabase.dbo.myRemap;
```

### 使用 [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 和 [XML 格式檔案](../../relational-databases/import-export/xml-format-files-sql-server.md)<a name="bulk_xml"></a>
在 Microsoft SQL Server Management Studio (SSMS) 中執行下列 Transact-SQL：
```tsql
USE TestDatabase;  
GO

TRUNCATE TABLE myRemap;
BULK INSERT dbo.myRemap   
   FROM 'D:\BCP\myRemap.bcp'   
   WITH (FORMATFILE = 'D:\BCP\myRemap.xml');  
GO  

-- review results
SELECT * FROM TestDatabase.dbo.myRemap;
```

### 使用 [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) 和 [非 XML 格式檔案](../../relational-databases/import-export/non-xml-format-files-sql-server.md)<a name="openrowset_nonxml"></a>    
在 Microsoft SQL Server Management Studio (SSMS) 中執行下列 Transact-SQL：
```tsql
USE TestDatabase;
GO

TRUNCATE TABLE myRemap;
INSERT INTO dbo.myRemap
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myRemap.bcp',
        FORMATFILE = 'D:\BCP\myRemap.fmt'
        ) AS t1;
GO

-- review results
SELECT * FROM TestDatabase.dbo.myRemap;
```

### 使用 [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) 和 [XML 格式檔案](../../relational-databases/import-export/xml-format-files-sql-server.md)<a name="openrowset_xml"></a>
在 Microsoft SQL Server Management Studio (SSMS) 中執行下列 Transact-SQL：
```tsql
USE TestDatabase;  
GO

TRUNCATE TABLE myRemap;
INSERT INTO dbo.myRemap 
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myRemap.bcp',
        FORMATFILE = 'D:\BCP\myRemap.xml'  
       ) AS t1;
GO

-- review results
SELECT * FROM TestDatabase.dbo.myRemap;
```


  
## <a name="see-also"></a>另請參閱  
[bcp Utility](../../tools/bcp-utility.md)   
 [使用格式檔案略過資料表資料行 &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)   
 [使用格式檔案略過資料欄位 &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
  

