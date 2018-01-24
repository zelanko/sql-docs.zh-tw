---
title: "使用格式檔案以略過資料表資料行 (SQL Server) | Microsoft 文件"
ms.custom: 
ms.date: 08/05/2016
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
- skipping columns when importing
- format files [SQL Server], skipping columns
ms.assetid: 30e0e7b9-d131-46c7-90a4-6ccf77e3d4f3
caps.latest.revision: "50"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 532a6809dc01c3122efa5e46665c77569ebf060d
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/19/2018
---
# <a name="use-a-format-file-to-skip-a-table-column-sql-server"></a>使用格式檔案以略過資料表資料行 (SQL Server)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] 本主題將描述格式檔案。 當欄位不存在於資料檔案中時，您就可以使用格式檔案來略過資料表資料行的匯入。 只有在略過的資料行可為 Null 和/或有預設值時，資料檔案所包含的欄位才可以少於資料表中的資料行數目。  
  
## <a name="sample-table-and-data-file"></a>範例資料表與資料檔  
 下列範例會要求在 `myTestSkipCol` dbo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 結構描述下之 **範例資料庫中有一個名為** 的資料表。 使用如下陳述式建立此資料表：  
  
```sql
USE AdventureWorks2012;  
GO  
CREATE TABLE myTestSkipCol   
   (  
   Col1 smallint,  
   Col2 nvarchar(50) NULL,  
   Col3 nvarchar(50) not NULL  
   );  
GO  
```  
  
 下列範例會使用範例資料檔案 `myTestSkipCol2.dat`，而且這個檔案只包含兩個欄位 (雖然對應的資料表包含三個資料行)：  
  
```  
1,DataForColumn3  
1,DataForColumn3  
1,DataForColumn3  
```  
  
 若要將資料從 `myTestSkipCol2.dat` 大量匯入 `myTestSkipCol` 資料表中，格式檔案必須將第一個資料欄位對應到 `Col1`、第二個欄位對應到 `Col3`，但是要略過 `Col2`。  
  
## <a name="using-a-non-xml-format-file"></a>使用非 XML 格式檔案  
 您可以修改非 XML 格式檔案以略過資料表資料行。 一般而言，這涉及到使用 **bcp** 公用程式以建立預設的非 XML 格式檔案，以及在文字編輯器中修改預設的檔案。 修改過的格式檔案必須將每個現有欄位對應到相對的資料表資料行，並且指出要略過哪些資料表資料行或資料行。 有兩個替代方法可以修改預設的非 XML 資料檔案。 兩個替代方法都會指出資料欄位並不存在於資料檔案中，且不會將任何資料插入對應的資料表資料行。  
  
### <a name="creating-a-default-non-xml-format-file"></a>建立預設的非 XML 格式檔案  
 本主題使用 `myTestSkipCol` 範例資料表的預設非 XML 格式檔案，這是使用下列 **bcp** 命令所建立：  
  
```cmd
bcp AdventureWorks2012..myTestSkipCol format nul -f myTestSkipCol_Default.fmt -c -T  
```  
  
 上述命令會建立非 XML 格式檔案 `myTestSkipCol_Default.fmt`。 這個格式檔案稱為「預設格式檔案」(Default Format File)，因為它是 **bcp** 所產生的格式。 一般而言，預設格式檔案描述資料檔欄位與資料表資料行之間的一對一對應。  
  
> [!IMPORTANT]  
>  您可能需要指定您要連接的伺服器執行個體的名稱。 此外，也可能需要指定使用者名稱和密碼。 如需相關資訊，請參閱 [bcp Utility](../../tools/bcp-utility.md)。  
  
 下列圖解顯示了這個範例預設格式檔案中的值。 此圖解同時顯示每個格式檔欄位的名稱。  
  
 ![myTestSkipCol 的預設非 XML 格式檔案](../../relational-databases/import-export/media/mytestskipcol-f-c-default-fmt.gif "myTestSkipCol 的預設非 XML 格式檔案")  
  
> [!NOTE]  
>  如需格式檔案欄位的詳細資訊，請參閱[非 XML 格式檔案 &#40;SQL Server&#41;](../../relational-databases/import-export/non-xml-format-files-sql-server.md)。  
  
### <a name="methods-for-modifying-a-non-xml-format-file"></a>修改非 XML 格式檔案的方法  
 若要略過資料表資料行，請編輯預設的非 XML 格式檔案，並且使用下列其中一個替代方法來修改檔案：  
  
-   慣用的方法包括三個基本步驟。 首先，刪除資料檔案中遺失的、任何描述欄位的格式檔資料列。 接著，減少所刪除的資料列之後的、每個格式檔資料列的「主檔案欄位順序」值。 目的是要產生連續的「主檔案欄位順序」值 (1 到 *n*)，以反映每個資料欄位在資料檔案中的實際位置。 最後，減少 [資料行數目] 欄位中的值，以反映資料檔案中欄位的實際數目。  
  
     下列範例根據 `myTestSkipCol` 資料表的預設格式檔案，這是本主題先前在「建立預設的非 XML 格式檔案」中建立的格式檔。 這個修改過的格式檔案將第一個資料欄位對應到 `Col1`、略過 `Col2`，然後對應第二個資料欄位到 `Col3`。 `Col2` 資料列現在已經刪除。  
  
    ```  
    9.0  
    2  
    1       SQLCHAR       0       7       "\t"     1     Col1         ""  
    2       SQLCHAR       0       100     "\r\n"   3     Col3         SQL_Latin1_General_CP1_CI_AS  
    ```  
  
-   此外，若要略過資料表資料行，您也可以修改對應於資料表資料行的格式檔資料列的定義。 在這個格式檔資料列中，[前置長度]、[主檔案資料長度] 和 [伺服器資料行順序] 值都必須設定為 0。 此外，[結束字元] 和 [資料行定序] 欄位則必須設定為 "" (NULL)。  
  
     雖然不需要實際的資料行名稱，但是 [伺服器資料行名稱] 值仍必須為非空白字串。 其餘的格式欄位需要各自的預設值。  
  
     下列範例也是從 `myTestSkipCol` 資料表的預設格式檔案衍生的。  
  
    ```  
    9.0  
    3  
    1       SQLCHAR       0       7       "\t"     1     Col1         ""  
    2       SQLCHAR       0       0       ""       0     Col2         ""  
    3       SQLCHAR       0       100     "\r\n"   3     Col3         SQL_Latin1_General_CP1_CI_AS  
    ```  
  
### <a name="examples"></a>範例  
 下列範例也是基於本主題先前在「範例資料表與資料檔」中建立的 `myTestSkipCol` 範例資料表以及 `myTestSkipCol2.dat` 範例資料檔案。  
  
#### <a name="using-bulk-insert"></a>使用 BULK INSERT  
 這個範例要使用本主題先前在「修改非 XML 格式檔案的方法」中建立的任一修改過的非 XML 格式檔案，才能運作。 在這個範例中，修改的格式檔案命名為 `C:\myTestSkipCol2.fmt`。 若要使用 `BULK INSERT` 大量匯入 `myTestSkipCol2.dat` 資料檔，請在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 查詢編輯器中執行下列程式碼：  
  
```sql  
USE AdventureWorks2012;  
GO  
BULK INSERT myTestSkipCol   
   FROM 'C:\myTestSkipCol2.dat'   
   WITH (FORMATFILE = 'C:\myTestSkipCol2.fmt');  
GO  
SELECT * FROM myTestSkipCol;  
GO  
```  
  
## <a name="using-an-xml-format-file"></a>使用 XML 格式檔案  
 如果使用 XML 格式檔案，您就不能在直接匯入至資料表時，使用 **bcp** 命令或 BULK INSERT 陳述式來略過資料行。 不過，您可以匯入資料表最後一個資料行以外的所有資料行。 如果您必須略過最後一個資料行以外的任何資料行，就必須建立只有包含資料檔案中包含之資料行的目標資料表檢視。 然後，您就可以從該檔案將大量資料匯入檢視。  
  
 若要利用 OPENROWSET(BULK...) 來使用 XML 格式檔案，以略過資料表資料行，您就必須在選取清單和目標資料表中提供明確的資料行清單，如下所示：  
  
 INSERT ...<column_list> SELECT <column_list> FROM OPENROWSET(BULK...)  
  
### <a name="creating-a-default-xml-format-file"></a>建立預設的 XML 格式檔案  
 修改的格式檔案的範例以本主題先前在＜範例資料表與資料檔＞中建立的 `myTestSkipCol` 範例資料表與資料檔為基礎。 下列 **bcp** 命令會建立 `myTestSkipCol` 資料表的預設 XML 格式檔案：  
  
```cmd
bcp AdventureWorks2012..myTestSkipCol format nul -f myTestSkipCol_Default.xml -c -x -T  
```  
  
 產生的預設非 XML 格式檔案描述的是資料檔欄位與資料表資料行之間的一對一對應，如下所示：  
  
```xml
\<?xml version="1.0"?>  
\<BCPFORMAT xmlns="http://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
 <RECORD>  
  \<FIELD ID="1" xsi:type="CharTerm" TERMINATOR="\t" MAX_LENGTH="7"/>  
  \<FIELD ID="2" xsi:type="CharTerm" TERMINATOR="\t" MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  \<FIELD ID="3" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
 </RECORD>  
 <ROW>  
  \<COLUMN SOURCE="1" NAME="Col1" xsi:type="SQLSMALLINT"/>  
  \<COLUMN SOURCE="2" NAME="Col2" xsi:type="SQLNVARCHAR"/>  
  \<COLUMN SOURCE="3" NAME="Col3" xsi:type="SQLNVARCHAR"/>  
 </ROW>  
</BCPFORMAT>  
```  
  
> [!NOTE]  
>  如需 XML 格式檔案之結構的相關資訊，請參閱 [XML 格式檔案 &#40;SQL Server&#41;](../../relational-databases/import-export/xml-format-files-sql-server.md)。  
  
### <a name="examples"></a>範例  
 本節中的範例使用本主題先前在「範例資料表與資料檔」中建立的 `myTestSkipCol` 範例資料表以及 `myTestSkipCol2.dat` 範例資料檔案。 為了將資料從 `myTestSkipCol2.dat` 匯入至 `myTestSkipCol` 資料表，這個範例使用修改過的 XML 格式檔案 `myTestSkipCol2-x.xml`。 這個檔案是以本主題先前在＜建立預設的 XML 格式檔案＞中建立的格式檔案為基礎。  
  
```xml
\<?xml version="1.0"?>  
\<BCPFORMAT xmlns="http://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
 <RECORD>  
  \<FIELD ID="1" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="7"/>  
  \<FIELD ID="2" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
 </RECORD>  
 <ROW>  
  \<COLUMN SOURCE="1" NAME="Col1" xsi:type="SQLSMALLINT"/>  
  \<COLUMN SOURCE="2" NAME="Col3" xsi:type="SQLNVARCHAR"/>  
 </ROW>  
</BCPFORMAT>  
```  
  
#### <a name="using-openrowsetbulk"></a>使用 OPENROWSET(BULK...)  
 下列範例會使用 `OPENROWSET` 大量資料列集提供者和 `myTestSkipCol2.xml` 格式檔案。 此範例會將 `myTestSkipCol2.dat` 資料檔案大量匯入 `myTestSkipCol` 資料表。 此陳述式會依需要，在選取清單還有目標資料表中包含明確的資料行清單。  
  
 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 查詢編輯器中，執行下列程式碼：  
  
```sql  
USE AdventureWorks2012;  
GO  
INSERT INTO myTestSkipCol  
  (Col1,Col3)  
    SELECT Col1,Col3  
      FROM  OPENROWSET(BULK  'C:\myTestSkipCol2.Dat',  
      FORMATFILE='C:\myTestSkipCol2.Xml'    
       ) as t1 ;  
GO  
```  
  
#### <a name="using-bulk-import-on-a-view"></a>在檢視上使用 BULK IMPORT  
 下列範例會在 `v_myTestSkipCol` 資料表上建立 `myTestSkipCol` 。 這個檢視會略過第二個資料表資料行 `Col2`。 然後，此範例會使用 `BULK INSERT` ，將 `myTestSkipCol2.dat` 資料檔案匯入這個檢視。  
  
 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 查詢編輯器中，執行下列程式碼：  
  
```sql  
CREATE VIEW v_myTestSkipCol AS  
    SELECT Col1,Col3  
    FROM myTestSkipCol;  
GO  
  
USE AdventureWorks2012;  
GO  
BULK INSERT v_myTestSkipCol  
FROM 'C:\myTestSkipCol2.dat'  
WITH (FORMATFILE='C:\myTestSkipCol2.xml');  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [使用格式檔案略過資料欄位 &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)   
 [使用格式檔案將資料表資料行對應至資料檔欄位 &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)   
 [使用格式檔案大量匯入資料 &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)  
  
  
