---
title: 使用格式檔案略過資料欄位 (SQL Server) | Microsoft 文件
ms.custom: ''
ms.date: 09/19/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- format files [SQL Server], skipping data fields
- skipping data fields when importing
ms.assetid: 6a76517e-983b-47a1-8f02-661b99859a8b
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 82df9a4dc4a7abce935e87e515cf63f71af0e4b7
ms.sourcegitcommit: bfa10c54e871700de285d7f819095d51ef70d997
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/14/2019
ms.locfileid: "54256783"
---
# <a name="use-a-format-file-to-skip-a-data-field-sql-server"></a>使用格式檔案略過資料欄位 (SQL Server)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
資料檔所包含的欄位，可以比資料表中的資料行數多。 此主題描述如何將資料表資料行對應到相對的資料欄位並忽略多餘欄位，藉以修改非 XML 格式檔案與 XML 格式檔案，讓資料檔能容納更多欄位。  如需其他資訊，請參閱 [建立格式檔案 (SQL Server)](../../relational-databases/import-export/create-a-format-file-sql-server.md) 。

|外框|
|---|
|[範例測試條件](#etc)<br />&emsp;&#9679;&emsp;[範例資料表](#sample_table)<br />&emsp;&#9679;&emsp;[範例資料檔案](#sample_data_file)<br />[建立格式檔案](#create_format_file)<br />&emsp;&#9679;&emsp;[建立非 XML 格式檔案](#nonxml_format_file)<br />&emsp;&#9679;&emsp;[修改非 XML 格式檔案](#modify_nonxml_format_file)<br />&emsp;&#9679;&emsp;[建立 XML 格式檔案](#xml_format_file)<br />&emsp;&#9679;&emsp;[修改 XML 格式檔案](#modify_xml_format_file)<br />[使用格式檔案略過資料欄位來匯入資料](#import_data)<br />&emsp;&#9679;&emsp;[使用 BCP 和非 XML 格式檔案](#bcp_nonxml)<br />&emsp;&#9679;&emsp;[使用 BCP 和 XML 格式檔案](#bcp_xml)<br />&emsp;&#9679;&emsp;[使用 BULK INSERT 和非 XML 格式檔案](#bulk_nonxml)<br />&emsp;&#9679;&emsp;[使用 BULK INSERT 和 XML 格式檔案](#bulk_xml)<br />&emsp;&#9679;&emsp;[使用 OPENROWSET(BULK...) 和非 XML 格式檔案](#openrowset_nonxml)<br />&emsp;&#9679;&emsp;[使用 OPENROWSET(BULK...) 和 XML 格式檔案](#openrowset_xml)<p>                                                                                                                                                                                                                  </p>|
  
> [!NOTE]
>  您可以透過下列項目，使用非 XML 或 XML 格式檔案，將資料檔案大量匯入至資料表：[bcp 公用程式](../../tools/bcp-utility.md)命令、[BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 陳述式或 INSERT ...SELECT * FROM [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) 陳述式。 如需詳細資訊，請參閱[使用格式檔案大量匯入資料 &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)。

## 範例測試條件<a name="etc"></a>  
本主題中的修改格式檔案範例是以下面定義的資料表和資料檔案為基礎。
  
### 範例資料表<a name="sample_table"></a>
下列指令碼會建立測試資料庫和名為 `myTestSkipField`的資料表。  在 Microsoft SQL Server Management Studio (SSMS) 中執行下列 Transact-SQL：
 
```sql
CREATE DATABASE TestDatabase;
GO

USE TestDatabase;
CREATE TABLE myTestSkipField
   (
   PersonID smallint,
   FirstName varchar(25),
   LastName varchar(30)
   );
```
  
### 範例資料檔案<a name="sample_data_file"></a>
建立空白檔案 `D:\BCP\myTestSkipField.bcp` ，並插入下列資料： 
```
1,SkipMe,Anthony,Grosse
2,SkipMe,Alica,Fatnowna
3,SkipMe,Stella,Rosenhain
```
  
## 建立格式檔案<a name="create_format_file"></a>
若要從 `myTestSkipField.bcp` 大量匯入資料到 `myTestSkipField` 資料表中，格式檔案必須執行下列工作：
* 將第一個資料欄位對應到第一個資料行 `PersonID`。
* 略過第二個資料欄位。
* 將第三個資料欄位對應到第二個資料行 `FirstName`。
* 將第四個資料欄位對應到第三個資料行 `LastName`。  

建立格式檔案的最簡單方法是使用 [bcp 公用程式](../../tools/bcp-utility.md)。  首先，從現有的資料表建立基底格式檔案。  其次，修改基底格式檔案以反映實際的資料檔案。
  
### <a name="nonxml_format_file"></a>建立非 XML 格式檔案 
如需詳細資訊，請參閱 [非 XML 格式檔案 (SQL Server)](../../relational-databases/import-export/non-xml-format-files-sql-server.md) 。 下列命令將使用 [bcp 公用程式](../../tools/bcp-utility.md) ，根據 `myTestSkipField.fmt`的結構描述產生非 XML 格式檔案 `myTestSkipField`。  另外還會使用限定詞 `c` 來指定字元資料、使用 `t,` 來指定逗號作為欄位結束字元，並使用 `T` 來指定使用整合式安全性的信任連接。  請在命令提示字元之下，輸入下列命令：

```
bcp TestDatabase.dbo.myTestSkipField format nul -c -f D:\BCP\myTestSkipField.fmt -t, -T
```

### 修改非 XML 格式檔案 <a name="modify_nonxml_format_file"></a>
請參閱 [非 XML 格式檔案的結構](../../relational-databases/import-export/non-xml-format-files-sql-server.md#Structure) 以了解此術語。 在 [記事本] 中開啟 `D:\BCP\myTestSkipField.fmt` 並執行下列修改：
1) 複製 `FirstName` 的整個格式檔資料列，並將它直接貼到下一行的 `FirstName` 後面。
2) 針對新資料列和所有後續資料列，將主機檔案欄位順序值加一。
3) 增加資料行數目值，以反映資料檔案中的實際欄位數目。
3) 針對第二個格式檔案資料列，將伺服器資料行順序從 `2` 修改為 `0` 。 

比較進行的變更：  
**之前**
```
13.0
3
1       SQLCHAR 0       7       ","      1     PersonID     ""
2       SQLCHAR 0       25      ","      2     FirstName    SQL_Latin1_General_CP1_CI_AS
3       SQLCHAR 0       30      "\r\n"   3     LastName     SQL_Latin1_General_CP1_CI_AS
```
**After**
```
13.0
4
1       SQLCHAR 0       7       ","      1     PersonID     ""
2       SQLCHAR 0       25      ","      0     FirstName    SQL_Latin1_General_CP1_CI_AS
3       SQLCHAR 0       25      ","      2     FirstName    SQL_Latin1_General_CP1_CI_AS
4       SQLCHAR 0       50      "\r\n"   3     LastName     SQL_Latin1_General_CP1_CI_AS

```

修改的格式檔案現在會反映：
* 4 個資料欄位
* `myTestSkipField.bcp` 中的第一個資料欄位會對應到第一個資料行、 ` myTestSkipField.. PersonID`
* `myTestSkipField.bcp` 中的第二個資料欄位未對應到任何資料行。
* `myTestSkipField.bcp` 中的第三個資料欄位會對應到第二個資料行、 `myTestSkipField.. FirstName`
* `myTestSkipField.bcp` 中的第四個資料欄位會對應到第三個資料行、 `myTestSkipField.. LastName`

### 建立 XML 格式檔案 <a name="xml_format_file"></a>  
如需詳細資訊，請參閱 [XML 格式檔案 (SQL Server)](../../relational-databases/import-export/xml-format-files-sql-server.md) 。  下列命令將使用 [bcp 公用程式](../../tools/bcp-utility.md) ，根據 `myTestSkipField.xml`的結構描述建立 XML 格式檔案 `myTestSkipField`。  另外還會使用限定詞 `c` 來指定字元資料、使用 `t,` 來指定逗號作為欄位結束字元，並使用 `T` 來指定使用整合式安全性的信任連接。  必須使用 `x` 限定詞來產生 XML 格式檔案。  請在命令提示字元之下，輸入下列命令：

```
bcp TestDatabase.dbo.myTestSkipField format nul -c -x -f D:\BCP\myTestSkipField.xml -t, -T
```

### 修改 XML 格式檔案 <a name="modify_xml_format_file"></a>
請參閱 [XML 格式檔案的結構描述語法](../../relational-databases/import-export/xml-format-files-sql-server.md#StructureOfXmlFFs) 以了解此術語。  在 [記事本] 中開啟 `D:\BCP\myTestSkipField.xml` 並執行下列修改：
1) 複製整個第二個欄位，並將它直接貼到下一行的第二個欄位後面。
2) 針對新的 FIELD 以及每個後續 FIELD，將 "FIELD ID" 值加 1。
3) 針對 `FirstName`和 `LastName` ，將 "COLUMN SOURCE" 值加 1，以反映修改過的對應。

比較進行的變更：  
**之前**
```
\<?xml version="1.0"?>
\<BCPFORMAT xmlns="https://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
 <RECORD>
  \<FIELD ID="1" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="7"/>
  \<FIELD ID="2" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="25" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
  \<FIELD ID="3" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="30" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
 </RECORD>
 <ROW>
  \<COLUMN SOURCE="1" NAME="PersonID" xsi:type="SQLSMALLINT"/>
  \<COLUMN SOURCE="2" NAME="FirstName" xsi:type="SQLVARYCHAR"/>
  \<COLUMN SOURCE="3" NAME="LastName" xsi:type="SQLVARYCHAR"/>
 </ROW>
</BCPFORMAT>
```

**After**
```
\<?xml version="1.0"?>
\<BCPFORMAT xmlns="https://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
 <RECORD>
  \<FIELD ID="1" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="7"/>
  \<FIELD ID="2" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="25" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
  \<FIELD ID="3" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="25" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
  \<FIELD ID="4" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="30" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
 </RECORD>
 <ROW>
  \<COLUMN SOURCE="1" NAME="PersonID" xsi:type="SQLSMALLINT"/>
  \<COLUMN SOURCE="3" NAME="FirstName" xsi:type="SQLVARYCHAR"/>
  \<COLUMN SOURCE="4" NAME="LastName" xsi:type="SQLVARYCHAR"/>
 </ROW>
</BCPFORMAT>
```

修改的格式檔案現在會反映：
* 4 個資料欄位
* 對應到 COLUMN 1 的 FIELD 1 會對應到第一個資料表資料行、 `myTestSkipField.. PersonID`
* FIELD 2 未對應到任何 COLUMN，因此未對應至任何資料表資料行。
* 對應到 COLUMN 3 的 FIELD 3 會對應到第二個資料表資料行、 `myTestSkipField.. FirstName`
* 對應到 COLUMN 4 的 FIELD 4 會對應到第三個資料表資料行、 `myTestSkipField.. LastName`

## 使用格式檔案略過資料欄位來匯入資料<a name="import_data"></a>
下列範例會使用上面建立的資料庫、資料檔案和格式檔案。

### 使用 [bcp](../../tools/bcp-utility.md) 和 [非 XML 格式檔案](../../relational-databases/import-export/non-xml-format-files-sql-server.md)<a name="bcp_nonxml"></a>
請在命令提示字元之下，輸入下列命令：
```
bcp TestDatabase.dbo.myTestSkipField IN D:\BCP\myTestSkipField.bcp -f D:\BCP\myTestSkipField.fmt -T
```

### 使用 [bcp](../../tools/bcp-utility.md) 和 [XML 格式檔案](../../relational-databases/import-export/xml-format-files-sql-server.md)<a name="bcp_xml"></a>
請在命令提示字元之下，輸入下列命令：
```
bcp TestDatabase.dbo.myTestSkipField IN D:\BCP\myTestSkipField.bcp -f D:\BCP\myTestSkipField.xml -T
```

### 使用 [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 和 [非 XML 格式檔案](../../relational-databases/import-export/non-xml-format-files-sql-server.md)<a name="bulk_nonxml"></a>
在 Microsoft SQL Server Management Studio (SSMS) 中執行下列 Transact-SQL：
```sql
USE TestDatabase;  
GO

TRUNCATE TABLE myTestSkipField;
BULK INSERT dbo.myTestSkipField   
   FROM 'D:\BCP\myTestSkipField.bcp'   
   WITH (FORMATFILE = 'D:\BCP\myTestSkipField.fmt');  
GO  

-- review results
SELECT * FROM TestDatabase.dbo.myTestSkipField;
```

### 使用 [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 和 [XML 格式檔案](../../relational-databases/import-export/xml-format-files-sql-server.md)<a name="bulk_xml"></a>
在 Microsoft SQL Server Management Studio (SSMS) 中執行下列 Transact-SQL：
```sql
USE TestDatabase;  
GO

TRUNCATE TABLE myTestSkipField;
BULK INSERT dbo.myTestSkipField   
   FROM 'D:\BCP\myTestSkipField.bcp'   
   WITH (FORMATFILE = 'D:\BCP\myTestSkipField.xml');  
GO  

-- review results
SELECT * FROM TestDatabase.dbo.myTestSkipField;
```

### 使用 [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) 和 [非 XML 格式檔案](../../relational-databases/import-export/non-xml-format-files-sql-server.md)<a name="openrowset_nonxml"></a>    
在 Microsoft SQL Server Management Studio (SSMS) 中執行下列 Transact-SQL：
```sql
USE TestDatabase;
GO

TRUNCATE TABLE myTestSkipField;
INSERT INTO dbo.myTestSkipField
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myTestSkipField.bcp',
        FORMATFILE = 'D:\BCP\myTestSkipField.fmt'
        ) AS t1;
GO

-- review results
SELECT * FROM TestDatabase.dbo.myTestSkipField;
```

### 使用 [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) 和 [XML 格式檔案](../../relational-databases/import-export/xml-format-files-sql-server.md)<a name="openrowset_xml"></a>
在 Microsoft SQL Server Management Studio (SSMS) 中執行下列 Transact-SQL：
```sql
USE TestDatabase;  
GO

TRUNCATE TABLE myTestSkipField;
INSERT INTO dbo.myTestSkipField 
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myTestSkipField.bcp',
        FORMATFILE = 'D:\BCP\myTestSkipField.xml'  
       ) AS t1;
GO

-- review results
SELECT * FROM TestDatabase.dbo.myTestSkipField;
```

  
## <a name="see-also"></a>另請參閱  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [使用格式檔案略過資料表資料行 &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)   
 [使用格式檔案將資料表資料行對應至資料檔欄位 &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
  
