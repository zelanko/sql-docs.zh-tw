---
title: 使用格式檔案以略過資料表資料行 (SQL Server) | Microsoft 文件
ms.custom: ''
ms.date: 02/15/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- skipping columns when importing
- format files [SQL Server], skipping columns
ms.assetid: 30e0e7b9-d131-46c7-90a4-6ccf77e3d4f3
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4674b103ca9237867b277b09ca9d68bc45492841
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2018
ms.locfileid: "51677337"
---
# <a name="use-a-format-file-to-skip-a-table-column-sql-server"></a>使用格式檔案以略過資料表資料行 (SQL Server)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

本文說明當跳過的資料行資料不存在於來源資料檔案中時，如何使用格式檔案來跳過資料表資料行的匯入。 資料檔案可包含少於目的地資料表中資料行數量的欄位；也就是說，您可以跳過匯入資料行，但必須是目的資料表中，下列兩項條件中至少一項為 True 時：
-   跳過的資料行可為 Null。
-   跳過的資料行有預設值。  
  
## <a name="sample-table-and-data-file"></a>範例資料表與資料檔案  
 本文中的範例要求 **dbo** 結構描述下名為 `myTestSkipCol` 的資料表。 您可以在範例資料庫 (例如 *WideWorldImporters* 或 *AdventureWorks*) 或任何其他資料庫中建立此資料表。 使用如下陳述式建立此資料表：  
  
```sql
USE WideWorldImporters;  
GO  
CREATE TABLE myTestSkipCol   
   (  
   Col1 smallint,  
   Col2 nvarchar(50) NULL,  
   Col3 nvarchar(50) not NULL  
   );  
GO  
```  
  
本文中的範例也會使用範例資料檔案 `myTestSkipCol2.dat`。 此資料檔案只包含兩個欄位，但目的地資料表包含三個資料行。

```  
1,DataForColumn3  
1,DataForColumn3  
1,DataForColumn3  
```  
  
## <a name="basic-steps"></a>基本步驟

您可以使用非 XML 格式檔案或 XML 格式檔案跳過資料表資料行。 在這兩種情況下，都有兩個步驟：

1.   使用 **bcp** 命令列公用程式來建立預設格式檔案。

2.   修改文字編輯器中的預設格式檔案。

修改後的格式檔案必須將每個現有欄位對應到目的地資料表中相應的資料行。 其也必須指出要跳過哪些資料表資料行或資料行。 

例如，若要將資料從 `myTestSkipCol2.dat` 大量匯入 `myTestSkipCol` 資料表，格式檔案必須將第一個資料欄位對應到 `Col1`、跳過 `Col2`，然後將第二個欄位對應到 `Col3`。  
 
## <a name="option-1---use-a-non-xml-format-file"></a>選項 1：使用非 XML 格式檔案  
  
### <a name="step-1---create-a-default-non-xml-format-file"></a>步驟 1 - 建立預設的非 XML 格式檔案  
在命令提示字元中，執行下列 **bcp** 命令以建立 `myTestSkipCol` 範例資料表的預設非 XML 格式檔案：  
  
```cmd
bcp WideWorldImporters..myTestSkipCol format nul -f myTestSkipCol_Default.fmt -c -T  
```  

> [!IMPORTANT]  
>  您可能需要以 `-S` 引數來指定您連線至的伺服器執行個體名稱。 另外，也可能需要以 `-U` 和 `-P` 引數來指定使用者名稱和密碼。 如需相關資訊，請參閱 [bcp Utility](../../tools/bcp-utility.md)。  

上述命令會建立非 XML 格式檔案 `myTestSkipCol_Default.fmt`。 這個格式檔案稱為「預設格式檔案」(Default Format File)，因為它是 **bcp** 所產生的格式。 預設格式檔案描述資料檔案欄位與資料表資料行之間的一對一對應。  
  
 下列螢幕擷取畫面顯示了這個範例預設格式檔案中的值。 
  
 ![myTestSkipCol 的預設非 XML 格式檔案](../../relational-databases/import-export/media/mytestskipcol-f-c-default-fmt.gif "myTestSkipCol 的預設非 XML 格式檔案")  
  
> [!NOTE]  
>  如需格式檔案欄位的詳細資訊，請參閱[非 XML 格式檔案 &#40;SQL Server&#41;](../../relational-databases/import-export/non-xml-format-files-sql-server.md)。  
  
### <a name="step-2---modify-a-non-xml-format-file"></a>步驟 2 - 修改非 XML 格式檔案  
若要修改預設的非 XML 格式檔案，有兩種替代方式。 兩種選項都會指出資料欄位並不存在於資料檔案中，且不會將任何資料插入對應的資料表資料行。

若要略過資料表資料行，請編輯預設的非 XML 格式檔案，並且使用下列其中一個替代方法來修改檔案：  

#### <a name="option-1---remove-the-row"></a>選項 1 - 移除資料列
建議用來跳過資料行的方法包含了下列三個步驟：

1.   首先，刪除描述來源資料檔案中遺失之欄位的任何格式檔案資料列。
2.   接著，減少所刪除的資料列之後的、每個格式檔資料列的「主檔案欄位順序」值。 目的是要產生連續的「主檔案欄位順序」值 (1 到 *n*)，以反映每個資料欄位在資料檔案中的實際位置。
3.   最後，減少 [資料行數目] 欄位中的值，以反映資料檔案中欄位的實際數目。  
  
下列範例以 `myTestSkipCol` 資料表的預設格式檔案為基礎。 這個修改過的格式檔案將第一個資料欄位對應到 `Col1`、略過 `Col2`，然後對應第二個資料欄位到 `Col3`。 `Col2` 資料列現在已經刪除。 第一個欄位之後分隔的符號也已從 `\t` 變更為 `,`。
  
```  
14.0  
2  
1       SQLCHAR       0       7       ","      1     Col1         ""  
2       SQLCHAR       0       100     "\r\n"   3     Col3         SQL_Latin1_General_CP1_CI_AS  
```  
  
#### <a name="option-2---modify-the-row-definition"></a>選項 2 - 修改資料列定義

此外，若要略過資料表資料行，您也可以修改對應於資料表資料行的格式檔資料列的定義。 在這個格式檔資料列中，[前置長度]、[主檔案資料長度] 和 [伺服器資料行順序] 值都必須設定為 0。 此外，[結束字元] 和 [資料行定序] 欄位必須設為 "" (也就是空白或 NULL 值)。 雖然不需要實際的資料行名稱，但是「伺服器資料行名稱」值仍必須為非空白字串。 其餘的格式欄位需要各自的預設值。  
  
下列範例也是從 `myTestSkipCol` 資料表的預設格式檔案衍生的。  
  
```  
14.0  
3  
1       SQLCHAR       0       7       ","      1     Col1         ""  
2       SQLCHAR       0       0       ""       0     Col2         ""  
3       SQLCHAR       0       100     "\r\n"   3     Col3         SQL_Latin1_General_CP1_CI_AS  
```  
  
### <a name="examples-with-a-non-xml-format-file"></a>非 XML 格式檔案的範例 
下列範例以本文先前說明的 `myTestSkipCol` 範例資料表及 `myTestSkipCol2.dat` 範例資料檔案為基礎。  
  
#### <a name="using-bulk-insert"></a>使用 BULK INSERT  
使用如上一節所述來建立之任一個修改的非 XML 格式檔案，此範例就可運作。 在這個範例中，修改的格式檔案命名為 `myTestSkipCol2.fmt`。 若要使用 `BULK INSERT` 大量匯入 `myTestSkipCol2.dat` 資料檔案，請在 SSMS 中執行下列程式碼。 更新您電腦上範例檔案位置的檔案系統路徑。
  
```sql  
USE WideWorldImporters;  
GO  
BULK INSERT myTestSkipCol   
   FROM 'C:\myTestSkipCol2.dat'   
   WITH (FORMATFILE = 'C:\myTestSkipCol2.fmt');  
GO  
SELECT * FROM myTestSkipCol;  
GO  
```  
  
## <a name="option-2---use-an-xml-format-file"></a>選項 2 - 使用 XML 格式檔案  
  
### <a name="step-1---create-a-default-xml-format-file"></a>步驟 1 - 建立預設的 XML 格式檔案   

在命令提示字元中，執行下列 **bcp** 命令以建立 `myTestSkipCol` 範例資料表的預設 XML 格式檔案：  
  
```cmd
bcp WideWorldImporters..myTestSkipCol format nul -f myTestSkipCol_Default.xml -c -x -T  
```  
  
> [!IMPORTANT]  
>  您可能需要以 `-S` 引數來指定您連線至的伺服器執行個體名稱。 另外，也可能需要以 `-U` 和 `-P` 引數來指定使用者名稱和密碼。 如需相關資訊，請參閱 [bcp Utility](../../tools/bcp-utility.md)。  
 
上述命令會建立 XML 格式檔案 `myTestSkipCol_Default.xml`。 這個格式檔案稱為「預設格式檔案」(Default Format File)，因為它是 **bcp** 所產生的格式。 預設格式檔案描述資料檔案欄位與資料表資料行之間的一對一對應。  
  
```xml
<?xml version="1.0"?>  
<BCPFORMAT xmlns="https://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance">  
 <RECORD>  
  <FIELD ID="1" xsi:type="CharTerm" TERMINATOR="\t" MAX_LENGTH="7"/>  
  <FIELD ID="2" xsi:type="CharTerm" TERMINATOR="\t" MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  <FIELD ID="3" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
 </RECORD>  
 <ROW>  
  <COLUMN SOURCE="1" NAME="Col1" xsi:type="SQLSMALLINT"/>  
  <COLUMN SOURCE="2" NAME="Col2" xsi:type="SQLNVARCHAR"/>  
  <COLUMN SOURCE="3" NAME="Col3" xsi:type="SQLNVARCHAR"/>  
 </ROW>  
</BCPFORMAT>  
```  
  
> [!NOTE]  
>  如需 XML 格式檔案之結構的相關資訊，請參閱 [XML 格式檔案 &#40;SQL Server&#41;](../../relational-databases/import-export/xml-format-files-sql-server.md)。  

### <a name="step-2---modify-an-xml-format-file"></a>步驟 2 - 修改 XML 格式檔案

以下是修改的 XML 格式檔案 `myTestSkipCol2.xml`，其跳過了 `Col2`。 `Col2` 的 `FIELD` 和 `ROW` 項目已移除，且項目已重新編號。 第一個欄位之後分隔的符號也已從 `\t` 變更為 `,`。

```xml
<?xml version="1.0"?>  
<BCPFORMAT xmlns="https://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance">  
 <RECORD>  
  <FIELD ID="1" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="7"/>  
  <FIELD ID="2" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
 </RECORD>  
 <ROW>  
  <COLUMN SOURCE="1" NAME="Col1" xsi:type="SQLSMALLINT"/>  
  <COLUMN SOURCE="2" NAME="Col3" xsi:type="SQLNVARCHAR"/>  
 </ROW>  
</BCPFORMAT>  
```  
 
### <a name="examples-with-an-xml-format-file"></a>使用 XML 格式檔案的範例   
下列範例以本文先前說明的 `myTestSkipCol` 範例資料表及 `myTestSkipCol2.dat` 範例資料檔案為基礎。

為了將資料從 `myTestSkipCol2.dat` 匯入 `myTestSkipCol` 資料表中，範例使用了修改過的 XML 格式檔案 `myTestSkipCol2.xml`。   
  
#### <a name="using-bulk-insert-with-a-view"></a>以檢視來使用 BULK INSERT  

如果使用 XML 格式檔案，您就不能在使用 **bcp** 命令或 `BULK INSERT` 陳述式直接匯入資料表時，跳過資料行。 不過，您可以匯入資料表最後一個資料行以外的所有資料行。 如果您必須略過最後一個資料行以外的任何資料行，就必須建立只有包含資料檔案中包含之資料行的目標資料表檢視。 然後，您就可以從該檔案將大量資料匯入檢視。  
  
下列範例會在 `myTestSkipCol` 資料表上建立 `v_myTestSkipCol` 檢視。 這個檢視會略過第二個資料表資料行 `Col2`。 然後，此範例會使用 `BULK INSERT` ，將 `myTestSkipCol2.dat` 資料檔案匯入這個檢視。  
  
請在 SSMS 中執行下列程式碼。 更新您電腦上範例檔案位置的檔案系統路徑。 
  
```sql  
USE WideWorldImporters;  
GO  

CREATE VIEW v_myTestSkipCol AS  
    SELECT Col1,Col3  
    FROM myTestSkipCol;  
GO  
  
BULK INSERT v_myTestSkipCol  
FROM 'C:\myTestSkipCol2.dat'  
WITH (FORMATFILE='C:\myTestSkipCol2.xml');  
GO  
```  

#### <a name="using-openrowsetbulk"></a>使用 OPENROWSET(BULK...)  

若要透過使用 `OPENROWSET(BULK...)` 來使用 XML 格式檔案跳過資料表資料行，您必須在選取清單和目標資料表中提供明確的資料行清單，如下所示：  
  
    ```sql
    INSERT ...<column_list> SELECT <column_list> FROM OPENROWSET(BULK...) 
    ```

下列範例會使用 `OPENROWSET` 大量資料列集提供者和 `myTestSkipCol2.xml` 格式檔案。 此範例會將 `myTestSkipCol2.dat` 資料檔案大量匯入 `myTestSkipCol` 資料表。 此陳述式會依需要，在選取清單還有目標資料表中包含明確的資料行清單。  
  
請在 SSMS 中執行下列程式碼。 更新您電腦上範例檔案位置的檔案系統路徑。
  
```sql  
USE WideWorldImporters;  
GO  
INSERT INTO myTestSkipCol  
  (Col1,Col3)  
    SELECT Col1,Col3  
      FROM  OPENROWSET(BULK  'C:\myTestSkipCol2.Dat',  
      FORMATFILE='C:\myTestSkipCol2.Xml'    
       ) as t1 ;  
GO  
```

## <a name="see-also"></a>另請參閱  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [使用格式檔案略過資料欄位 &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)   
 [使用格式檔案將資料表資料行對應至資料檔欄位 &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)   
 [使用格式檔案大量匯入資料 &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)  
  
  
