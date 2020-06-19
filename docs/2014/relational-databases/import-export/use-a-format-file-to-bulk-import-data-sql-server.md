---
title: 使用格式檔案大量匯入資料 (SQL Server) | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- bulk importing [SQL Server], format files
- format files [SQL Server], importing data using
ms.assetid: 2956df78-833f-45fa-8a10-41d6522562b9
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c6d9779209b3ffb317658243c168d74740f6731b
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85026451"
---
# <a name="use-a-format-file-to-bulk-import-data-sql-server"></a>使用格式檔案大量匯入資料 (SQL Server)
  此主題說明格式檔案在大量匯入作業中的用法。 格式檔案會將資料檔案的欄位對應到資料表的資料行。  使用**bcp**命令或 BULK INSERT 或 INSERT ... 時，您可以使用非 XML 或 xml 格式檔案來大量匯入資料SELECT * FROM OPENROWSET （BULK ...） [!INCLUDE[tsql](../../includes/tsql-md.md)]命令.  
  
> [!IMPORTANT]  
>  如果格式檔案要與 Unicode 字元資料檔案搭配使用，則所有的輸入欄位都必須是 Unicode 文字字串 (也就是固定大小或以字元結束的 Unicode 字串)。  
  
> [!NOTE]  
>  如果您不熟悉格式檔案，請參閱[非 XML 格式檔案 &#40;SQL Server&#41;](xml-format-files-sql-server.md)和[xml 格式檔案 &#40;SQL Server&#41;](xml-format-files-sql-server.md)。  
  
## <a name="format-file-options-for-bulk-import-commands"></a>大量匯入命令的格式檔案選項  
 下表摘述每個大量匯入命令的格式檔案選項。  
  
|大量載入命令|使用格式檔案選項|  
|------------------------|-----------------------------------|  
|BULK INSERT|FORMATFILE = '*format_file_path*'|  
|INSERT ...SELECT * FROM OPENROWSET(BULK...)|FORMATFILE = '*format_file_path*'|  
|**bcp** .。。**中的**|**-f** *format_file*|  
  
 如需詳細資訊，請參閱 [bcp 公用程式](../../tools/bcp-utility.md)、[BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql) 或 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)。  
  
> [!NOTE]  
>  若要大量匯出或匯入 SQLXML 資料，請在格式檔案中使用下列其中一種資料類型：SQLCHAR 或 SQLVARYCHAR (資料會以用戶端字碼頁或定序所隱含的字碼頁傳送)、SQLNCHAR 或 SQLNVARCHAR (資料會以 Unicode 傳送)，或是 SQLBINARY 或 SQLVARYBIN (資料不經轉換即傳送)。  
  
## <a name="examples"></a>範例  
 本節中的範例說明如何使用格式檔案，利用**bcp**命令和 BULK INSERT 來大量匯入資料，然後插入 .。。SELECT * FROM OPENROWSET （BULK ...）語句。 執行其中一個大量匯入範例之前，必須先建立範例資料表、資料檔案與格式檔案。  
  
### <a name="sample-table"></a>範例資料表  
 這些範例在 **dbo** 結構描述下的 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] 範例資料庫中，需要建立一個名為 **myTestFormatFiles** 的資料表。 若要建立這個資料表，請在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 查詢編輯器中，執行：  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE myTestFormatFiles (  
   Col1 smallint,  
   Col2 nvarchar(50),  
   Col3 nvarchar(50),  
   Col4 nvarchar(50)  
   );  
GO  
```  
  
### <a name="sample-data-file"></a>範例資料檔  
 此範例使用範例資料檔案 `myTestFormatFiles-c.Dat`，包含下列記錄。 若要建立資料檔，請在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 命令提示字元中，輸入：  
  
```  
10,Field2,Field3,Field4  
15,Field2,Field3,Field4  
46,Field2,Field3,Field4  
58,Field2,Field3,Field4  
```  
  
### <a name="sample-format-files"></a>範例格式檔案  
 本節中有部分範例會使用 XML 格式檔案 `myTestFormatFiles-f-x-c.Xml`，而其他範例會使用非 XML 格式檔案。 兩種格式檔案都使用字元資料格式和非預設欄位結束字元 (,)。  
  
#### <a name="the-sample-non-xml-format-file"></a>非 XML 格式檔案範例  
 下列範例會使用 **bcp**，從 `myTestFormatFiles` 資料表產生 XML 格式檔案。 `myTestFormatFiles.Fmt` 檔案包含下列資訊：  
  
```  
9.0  
4  
1       SQLCHAR       0       7       ","      1     Col1         ""  
2       SQLCHAR       0       100     ","      2     Col2         SQL_Latin1_General_CP1_CI_AS  
3       SQLCHAR       0       100     ","      3     Col3         SQL_Latin1_General_CP1_CI_AS  
4       SQLCHAR       0       100     "\r\n"   4     Col4         SQL_Latin1_General_CP1_CI_AS  
```  
  
 若要使用 **bcp** 搭配 **format** 選項以建立此格式檔案，請在 Windows 命令提示字元中輸入：  
  
```  
bcp AdventureWorks2012..MyTestFormatFiles format nul -c -t, -f myTestFormatFiles.Fmt -T  
  
```  
  
 如需建立格式檔案的詳細資訊，請參閱[建立格式檔案 &#40;SQL Server&#41;](create-a-format-file-sql-server.md)。  
  
#### <a name="the-sample-xml-format-file"></a>XML 格式檔案範例  
 下列範例使用 **bcp**，從 `myTestFormatFiles` 資料表建立以產生 XML 格式檔案。 `myTestFormatFiles.Xml` 檔案包含下列資訊：  
  
```  
<?xml version="1.0"?>  
<BCPFORMAT xmlns="https://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
 <RECORD>  
  <FIELD ID="1" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="7"/>  
  <FIELD ID="2" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  <FIELD ID="3" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  <FIELD ID="4" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
 </RECORD>  
 <ROW>  
  <COLUMN SOURCE="1" NAME="Col1" xsi:type="SQLSMALLINT"/>  
  <COLUMN SOURCE="2" NAME="Col2" xsi:type="SQLNVARCHAR"/>  
  <COLUMN SOURCE="3" NAME="Col3" xsi:type="SQLNVARCHAR"/>  
  <COLUMN SOURCE="4" NAME="Col4" xsi:type="SQLNVARCHAR"/>  
 </ROW>  
</BCPFORMAT>  
```  
  
 若要使用 **bcp** 搭配 **format** 選項以建立此格式檔案，請在 Windows 命令提示字元中輸入：  
  
```  
bcp AdventureWorks2012..MyTestFormatFiles format nul -c -t, -x -f myTestFormatFiles.Xml -T  
```  
  
### <a name="using-bcp"></a>使用 bcp  
 下列範例使用 **bcp**，將 `myTestFormatFiles-c.Dat` 資料檔中的資料大量匯入到範例資料庫中的 `HumanResources.myTestFormatFiles` 資料表。 這個範例使用 XML 格式檔案 `MyTestFormatFiles.Xml`。 這個範例會在匯入資料檔之前，刪除任何現有的資料表資料列。  
  
 請在 Windows 命令提示字元之下，輸入：  
  
```  
bcp AdventureWorks2012..myTestFormatFiles in C:\myTestFormatFiles-c.Dat -f C:\myTestFormatFiles.Xml -T  
```  
  
> [!NOTE]  
>  如需此命令的詳細資訊，請參閱 [bcp 公用程式](../../tools/bcp-utility.md)。  
  
### <a name="using-bulk-insert"></a>使用 BULK INSERT  
 下列範例使用 BULK INSERT，將 `myTestFormatFiles-c.Dat` 資料檔中的資料大量匯入到 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] 範例資料庫中的 `HumanResources.myTestFormatFiles` 資料表。 這個範例使用非 XML 格式檔案 `MyTestFormatFiles.Fmt`。 這個範例會在匯入資料檔之前，刪除任何現有的資料表資料列。  
  
 在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 查詢編輯器中，執行：  
  
```  
USE AdventureWorks2012;  
GO  
DELETE myTestFormatFiles;  
GO  
BULK INSERT myTestFormatFiles   
   FROM 'C:\myTestFormatFiles-c.Dat'   
   WITH (FORMATFILE = 'C:\myTestFormatFiles.Fmt');  
GO  
SELECT * FROM myTestFormatFiles;  
GO  
```  
  
> [!NOTE]  
>  如需此陳述式的詳細資訊，請參閱 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)。  
  
### <a name="using-the-openrowset-bulk-rowset-provider"></a>使用 OPENROWSET Bulk 資料列集提供者  
 下列範例使用 `INSERT ... SELECT * FROM OPENROWSET(BULK...)`，將 `myTestFormatFiles-c.Dat` 資料檔中的資料大量匯入到 `HumanResources.myTestFormatFiles` 範例資料庫中的 `AdventureWorks` 資料表。 這個範例使用 XML 格式檔案 `MyTestFormatFiles.Xml`。 這個範例會在匯入資料檔之前，刪除任何現有的資料表資料列。  
  
 在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 查詢編輯器中，執行：  
  
```  
USE AdventureWorks2012;  
DELETE myTestFormatFiles;  
GO  
INSERT INTO myTestFormatFiles  
    SELECT *  
      FROM  OPENROWSET(BULK  'C:\myTestFormatFiles-c.Dat',  
      FORMATFILE='C:\myTestFormatFiles.Xml'       
      ) as t1 ;  
GO  
SELECT * FROM myTestFormatFiles;  
GO  
```  
  
 結束使用範例資料表時，可使用以下陳述式卸除該資料表：  
  
```  
DROP TABLE myTestFormatFiles  
```  
  
> [!NOTE]  
>  如需有關 OPENROWSET BULK 子句的詳細資訊，請參閱 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)。  
  
## <a name="additional-examples"></a>其他範例  
 [建立格式檔案 &#40;SQL Server&#41;](create-a-format-file-sql-server.md)  
  
 [使用格式檔案略過資料表資料行 &#40;SQL Server&#41;](use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
 [使用格式檔案略過資料欄位 &#40;SQL Server&#41;](use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
 [使用格式檔案將資料表資料行對應至資料檔案欄位 &#40;SQL Server&#41;](use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
## <a name="see-also"></a>另請參閱  
 [bcp 公用程式](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [非 XML 格式檔案 &#40;SQL Server&#41;](xml-format-files-sql-server.md)   
 [XML 格式檔案 &#40;SQL Server&#41;](xml-format-files-sql-server.md)  
  
  
