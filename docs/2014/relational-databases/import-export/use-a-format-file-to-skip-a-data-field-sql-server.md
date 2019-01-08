---
title: 使用格式檔案略過資料欄位 (SQL Server) | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: bad791f1eab5fbb31976236e6d79c08e8b9adc97
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/13/2018
ms.locfileid: "53351404"
---
# <a name="use-a-format-file-to-skip-a-data-field-sql-server"></a>使用格式檔案略過資料欄位 (SQL Server)
  資料檔所包含的欄位，可以比資料表中的資料行數多。 此主題描述如何將資料表資料行對應到相對的資料欄位並忽略多餘欄位，藉以修改非 XML 格式檔案與 XML 格式檔案，讓資料檔能容納更多欄位。  
  
> [!NOTE]  
>  您可以透過下列項目，使用非 XML 或 XML 格式檔案，將資料檔大量匯入至資料表：**bcp** 命令、BULK INSERT 陳述式或 INSERT ...SELECT * FROM OPENROWSET(BULK...) 陳述式。 如需詳細資訊，請參閱[使用格式檔案大量匯入資料 &#40;SQL Server&#41;](use-a-format-file-to-bulk-import-data-sql-server.md)。  
  
## <a name="sample-data-file-and-table"></a>範例資料檔與資料表  
 此主題中的修改格式檔案的範例是以下列資料表與資料檔為基礎。  
  
### <a name="sample-table"></a>範例資料表  
 此範例需要在 `myTestSkipField` 結構描述底下的 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 範例資料庫中建立一個名為 `dbo` 的資料表。 若要建立這個資料表，請在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 查詢編輯器中執行下列程式碼：  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE myTestSkipField   
   (  
   PersonID smallint,  
   FirstName nvarchar(50) ,  
   LastName nvarchar(50)   
   );  
GO  
```  
  
### <a name="sample-data-file"></a>範例資料檔  
 資料檔 `myTestSkipField-c.dat` 包含下列記錄：  
  
```  
1,Skipme,DataField3,DataField4  
1,Skipme,DataField3,DataField4  
1,Skipme,DataField3,DataField4  
```  
  
 若要從 `myTestSkipField-c.dat` 大量匯入資料到 `myTestSkipField` 資料表中，格式檔案必須執行下列工作：  
  
-   將第一個資料欄位對應到第一個資料行 `PersonID`。  
  
-   略過第二個資料欄位。  
  
-   將第三個資料欄位對應到第二個資料行 `FirstName`。  
  
-   將第四個資料欄位對應到第三個資料行 `LastName`。  
  
## <a name="non-xml-format-file-for-more-data-fields"></a>使用非 XML 格式檔案以取得更多資料欄位  
 下列格式檔案 `myTestSkipField.fmt` 會將 `myTestSkipField-c.dat` 中的欄位對應至 `myTestSkipField` 資料表的資料行。 格式檔案使用字元資料格式。 若要略過資料行對應，就必須將其資料行順序值變更為 0，如格式檔案中的 `ExtraField` 資料行所示。  
  
 `myTestSkipField.fmt` 格式檔案包含下列資訊：  
  
```  
9.0  
4  
1       SQLCHAR       0       7       ","      1     PersonID               ""  
2       SQLCHAR       0       100       ","    0     ExtraField             SQL_Latin1_General_CP1_CI_AS  
3       SQLCHAR       0       100     ","      2     FirstName              SQL_Latin1_General_CP1_CI_AS  
4       SQLCHAR       0       100     "\r\n"   3     LastName               SQL_Latin1_General_CP1_CI_AS  
  
```  
  
> [!NOTE]  
>  如需非 XML 格式檔案語法的相關資訊，請參閱[非 XML 格式檔案 &#40;SQL Server&#41;](xml-format-files-sql-server.md)。  
  
### <a name="examples"></a>範例  
 下列範例會利用 `INSERT ... SELECT * FROM OPENROWSET(BULK...)` 格式檔案來使用 `myTestSkipField.fmt`。 此範例會將 `myTestSkipField-c.dat` 資料檔案大量匯入 `myTestSkipField` 資料表。 若要建立範例資料表和資料檔，請參閱本主題前面的「範例資料檔與資料表」。  
  
 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 查詢編輯器中，執行下列程式碼：  
  
```  
USE AdventureWorks2012;  
GO  
INSERT INTO myTestSkipField   
   SELECT *  
      FROM  OPENROWSET(BULK  'C:\myTestSkipField-c.dat',  
      FORMATFILE='C:\myTestSkipField.fmt'    
       ) AS t1;  
GO   
```  
  
## <a name="xml-format-file-for-more-data-fields"></a>使用 XML 格式檔案以取得更多資料欄位  
 此範例中的格式檔案，所根據的是另一個格式檔案 `myTestSkipField.xml`，它在整個檔案中都使用字元資料格式，且其欄位在數量與順序上都與 `myTestSkipField` 資料表中的資料行對應。 若要檢視該格式檔案的內容，請參閱[建立格式檔案 &#40;SQL Server&#41;](create-a-format-file-sql-server.md)。  
  
 下列格式檔案 `myTestSkipField.xml` 會將 `myTestSkipField-c.dat` 中的欄位對應至 `myTestSkipField` 資料表的資料行。 格式檔案使用字元資料格式。  
  
 `myTestSkipField.xml` 格式檔案包含下列資訊：  
  
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
  <COLUMN SOURCE="1" NAME="PersonID" xsi:type="SQLSMALLINT"/>  
  <COLUMN SOURCE="3" NAME="FirstName" xsi:type="SQLNVARCHAR"/>  
  <COLUMN SOURCE="4" NAME="LastName" xsi:type="SQLNVARCHAR"/>  
 </ROW>  
</BCPFORMAT>  
```  
  
### <a name="examples"></a>範例  
 下列範例會利用 `INSERT ... SELECT * FROM OPENROWSET(BULK...)` 格式檔案來使用 `myTestSkipField.Xml`。 此範例會將 `myTestSkipField-c.dat` 資料檔案大量匯入 `myTestSkipField` 資料表。 若要建立範例資料表和資料檔，請參閱本主題前面的「範例資料檔與資料表」。  
  
 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 查詢編輯器中，執行下列程式碼：  
  
```  
USE AdventureWorks2012;  
GO  
INSERT INTO myTestSkipField   
  SELECT *  
      FROM  OPENROWSET(BULK  'C:\myTestSkipField-c.dat',  
      FORMATFILE='C:\myTestSkipField.xml'    
       ) AS t1;  
GO  
  
```  
  
> [!NOTE]  
>  如需 XML 結構描述語法的相關資訊以及 XML 格式檔案的其他範例，請參閱[XML 格式檔案 &#40;SQL Server&#41;](xml-format-files-sql-server.md)。  
  
## <a name="see-also"></a>另請參閱  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [使用格式檔案略過資料表資料行 &#40;SQL Server&#41;](use-a-format-file-to-skip-a-table-column-sql-server.md)   
 [使用格式檔案將資料表資料行對應至資料檔欄位 &#40;SQL Server&#41;](use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
  
