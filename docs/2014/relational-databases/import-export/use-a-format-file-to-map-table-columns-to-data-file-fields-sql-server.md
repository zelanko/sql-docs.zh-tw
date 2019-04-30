---
title: 使用格式檔案將資料表資料行對應至資料檔案欄位 (SQL Server) | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- mapping columns to fields during import [SQL Server]
- format files [SQL Server], mapping columns to fields
ms.assetid: e7ee4f7e-24c4-4eb7-84d2-41e57ccc1ef1
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 26db59ba5dbfc6f7be8d827a86dabb1cdd845d03
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63155813"
---
# <a name="use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server"></a>使用格式檔案將資料表資料行對應至資料檔欄位 (SQL Server)
  資料檔中包含的欄位順序可以與資料表中對應資料行的順序不同。 此主題呈現非 XML 與 XML 格式檔案，這些檔案已經過修改，以配合欄位順序與資料表資料行不同的資料檔。 已修改的格式檔案可將資料欄位對應到與它們對應的資料表資料行。  
  
> [!NOTE]  
>  您可以透過下列項目，使用非 XML 格式檔案或 XML 格式檔案，將資料檔案大量匯入資料表中：**bcp** 命令、BULK INSERT 陳述式或 INSERT ...SELECT * FROM OPENROWSET(BULK...) 陳述式。 如需詳細資訊，請參閱[使用格式檔案大量匯入資料 &#40;SQL Server&#41;](use-a-format-file-to-bulk-import-data-sql-server.md)。  
  
## <a name="sample-table-and-data-file"></a>範例資料表與資料檔  
 此主題中的修改格式檔案的範例是以下列資料表與資料檔為基礎。  
  
### <a name="sample-table"></a>範例資料表  
 本主題中的範例需要在 `dbo` 結構描述底下的 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 範例資料庫中建立一個名為 `myTestOrder` 的資料表。 若要建立這個資料表，請在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 查詢編輯器中，執行下列程式碼：  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE myTestOrder   
   (  
   Col1 smallint,  
   Col2 nvarchar(50) ,  
   Col3 nvarchar(50) ,   
   Col4 nvarchar(50)   
   );  
GO  
  
```  
  
### <a name="data-file"></a>資料檔  
 資料檔 `myTestOrder-c.txt` 包含下列記錄：  
  
```  
DataField3,DataField2,1,DataField4  
DataField3,DataField2,1,DataField4  
DataField3,DataField2,1,DataField4  
  
```  
  
 若要從 `myTestSkipCol2-c.dat` 大量匯入資料到 `myTestSkipCol` 資料表中，格式檔案必須對應第一個資料欄位至 `Col3`、第二個資料欄位至 `Col2`、第三個資料欄位至 `Col1`，以及第四個資料欄位至 `Col4`。  
  
## <a name="using-a-non-xml-format-file"></a>使用非 XML 格式檔案  
 您可以變更資料行的順序值，指出對應資料欄位的位置，來變更資料行對應的順序。  
  
 下列非 XML 格式檔案範例呈現格式檔案 `myTestOrder.fmt`，它會將 `myTestOrder-c.txt` 中的欄位對應到 `myTestOrder` 資料表的資料行。 如需有關如何建立範例資料表和資料檔的詳細資訊，請參閱本主題前面的「範例資料表與資料檔」。 格式檔案使用字元資料格式。  
  
 格式檔案包含下列資訊：  
  
```  
9.0  
4  
1       SQLCHAR       0       100     ","     3     Col3               SQL_Latin1_General_CP1_CI_AS  
2       SQLCHAR       0       100     ","     2     Col2               SQL_Latin1_General_CP1_CI_AS  
3       SQLCHAR       0       7       ","     1     Col1               ""  
4       SQLCHAR       0       100     "\r\n"  4     Col4               SQL_Latin1_General_CP1_CI_AS  
  
```  
  
> [!NOTE]  
>  如需非 XML 格式檔案版面配置的詳細資訊，請參閱[非 XML 格式檔案 &#40;SQL Server&#41;](xml-format-files-sql-server.md)。  
  
### <a name="example"></a>範例  
 下列範例使用 `BULK INSERT` 陳述式，利用 `myTestOrder-c.txt` 非 XML 格式檔案，將 `myTestOrder` 資料檔中的資料大量匯入 `myTestOrder.fmt` 範例資料表。  
  
 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 查詢編輯器中，執行：  
  
```  
USE AdventureWorks2012;  
GO  
BULK INSERT myTestOrder  
FROM 'C:\myTestOrder-c.txt'   
WITH (formatfile='C:\myTestOrder.fmt');  
GO  
  
```  
  
## <a name="using-an-xml-format-file"></a>使用 XML 格式檔案  
 下列非 XML 格式檔案範例呈現格式檔案 `myTestOrder.xml`，它會將 `myTestOrder-c.txt` 中的欄位對應到 `myTestOrder` 資料表的資料行。如需有關如何建立資料表和資料檔的詳細資訊，請參閱本主題前面的「範例資料表與資料檔」。  
  
 `myTestOrder.xml` 格式檔案包含下列資訊：  
  
```  
<?xml version="1.0"?>  
<BCPFORMAT xmlns="https://schemas.microsoft.com/sqlserver/2004/bulkload/format"   
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
 <RECORD>  
  <FIELD ID="1" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  <FIELD ID="2" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  <FIELD ID="3" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="7"/>  
  <FIELD ID="4" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
 </RECORD>  
 <ROW>  
  <COLUMN SOURCE="3" NAME="Col1" xsi:type="SQLSMALLINT"/>  
  <COLUMN SOURCE="2" NAME="Col2" xsi:type="SQLNVARCHAR"/>  
  <COLUMN SOURCE="1" NAME="Col3" xsi:type="SQLNVARCHAR"/>  
  <COLUMN SOURCE="4" NAME="Col4" xsi:type="SQLNVARCHAR"/>  
 </ROW>  
</BCPFORMAT>  
  
```  
  
> [!NOTE]  
>  如需 XML 結構描述語法的相關資訊以及 XML 格式檔案的其他範例，請參閱 [XML 格式檔案 &#40;SQL Server&#41;](xml-format-files-sql-server.md)。  
  
### <a name="example"></a>範例  
 下列範例使用 `OPENROWSET` 大量資料列集提供者，利用 `myTestOrder-c.txt` XML 格式檔案，將 `myTestOrder` 資料檔中的資料匯入 `myTestOrder.xml` 範例資料表。 `INSERT... SELECT`陳述式指定選取清單中的資料行清單。  
  
 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 查詢編輯器中，執行下列程式碼：  
  
```  
USE AdventureWorks2012;  
GO  
INSERT INTO myTestOrder   
  SELECT Col1, Col2, Col3, Col4  
      FROM  OPENROWSET(BULK  'C:\myTestOrder-c.txt',  
      FORMATFILE='C:\myTestOrder.Xml'    
       ) AS t1;  
GO  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [使用格式檔案略過資料表資料行 &#40;SQL Server&#41;](use-a-format-file-to-skip-a-table-column-sql-server.md)   
 [使用格式檔案略過資料欄位 &#40;SQL Server&#41;](use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
  
