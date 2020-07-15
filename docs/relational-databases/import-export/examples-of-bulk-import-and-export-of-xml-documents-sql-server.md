---
title: 大量匯入與匯出 XML 文件
description: 使用 SQL Server 大量匯入和匯出 XML 文件的範例
ms.date: 10/24/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- field terminators [SQL Server]
- bulk importing [SQL Server], data formats
- row terminators [SQL Server]
- OPENROWSET function, XML bulk load
- terminators [SQL Server]
- bulk exporting [SQL Server], data formats
- XML bulk load [SQL Server]
ms.assetid: dff99404-a002-48ee-910e-f37f013d946d
author: MashaMSFT
ms.author: mathoma
ms.custom: seo-lt-2019
ms.openlocfilehash: babdda8ca6ced94eba21788028d8bf6e6e7eeaae
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/06/2020
ms.locfileid: "86012449"
---
# <a name="examples-of-bulk-import-and-export-of-xml-documents-sql-server"></a>大量匯入與匯出 XML 文件的範例 (SQL Server)
[!INCLUDE [sqlserver2016-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa.md)]

    
##  <a name="top"></a>
 您可以將 XML 文件大量匯入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫或從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫大量匯出它們。 本主題將提供這兩種情況的範例。  
  
 若要從資料檔將資料大量匯入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表或非資料分割檢視，您可以使用下列方式：  
  
-   **bcp** 公用程式  
    您也可以使用 **bcp** 公用程式，從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中能執行 SELECT 陳述式的任意位置 (包括資料分割檢視) 匯出資料。  
  
-   BULK INSERT  
  
-   INSERT ...SELECT * FROM OPENROWSET(BULK...)  

如需詳細資訊，請參閱下列主題。
- [使用 bcp 公用程式匯入及匯出大量資料 (SQL Server)。](../../relational-databases/import-export/import-and-export-bulk-data-by-using-the-bcp-utility-sql-server.md)
- [使用 BULK INSERT 或 OPENROWSET (BULK...) 匯入大量資料 (SQL Server)。](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md) 
- [如何使用 XML 大量載入元件將 XML 匯入 SQL Server。](https://support.microsoft.com/kb/316005)
- [XML 結構描述集合 (SQL Server)](../xml/xml-schema-collections-sql-server.md)
  
## <a name="examples"></a>範例  
 此範例如下：  
  
-  [A.以二進位位元組資料流大量匯入 XML 資料](#binary_byte_stream)  
  
-  [B.在現有資料列中大量匯入 XML 資料](#existing_row)  
  
-  [C.從包含 DTD 的檔案大量匯入 XML 資料](#file_contains_dtd)  
  
- [D.使用格式檔案明確指定欄位結束字元](#field_terminator_in_format_file)  
  
-  [E.大量匯出 XML 資料](#bulk_export_xml_data)  
  
## <a name="bulk-importing-xml-data-as-a-binary-byte-stream"></a><a name="binary_byte_stream"></a>以二進位位元組資料流大量匯入 XML 資料  
 從包含您要套用的編碼宣告之檔案大量匯入 XML 資料時，請在 OPENROWSET(BULK…) 子句中指定 SINGLE_BLOB 選項。 SINGLE_BLOB 選項可確保 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的 XML 剖析器，會根據 XML 宣告中指定的編碼配置來匯入資料。  
  
#### <a name="sample-table"></a>範例資料表  
 若要測試範例 A，您必須建立範例資料表 `T`。  
  
```sql
USE tempdb  
CREATE TABLE T (IntCol int, XmlCol xml);  
GO  
```  
  
#### <a name="sample-data-file"></a>範例資料檔  
 在執行範例 A 之前，您必須先建立 UTF-8 編碼檔 (`C:\SampleFolder\SampleData3.txt`)，其中包含指定 `UTF-8` 編碼配置的下列範例執行個體。  
  
```xml  
<?xml version="1.0" encoding="UTF-8"?>  
<Root>  
          <ProductDescription ProductModelID="5">  
             <Summary>Some Text</Summary>  
          </ProductDescription>  
</Root>  
```  
  
#### <a name="example-a"></a>範例 A  
 這個範例在 `SINGLE_BLOB` 陳述式中使用 `INSERT ... SELECT * FROM OPENROWSET(BULK...)` 選項，以從名為 `SampleData3.txt` 的檔案匯入資料，並將 XML 執行個體插入範例資料表 `T`這個單一資料行資料表。  
  
```sql
INSERT INTO T(XmlCol)  
SELECT * FROM OPENROWSET(  
   BULK 'c:\SampleFolder\SampleData3.txt',  
   SINGLE_BLOB) AS x;  
```  
  
#### <a name="remarks"></a>備註  
 以此方式使用 SINGLE_BLOB 時，可以避免 XML 文件編碼 (由 XML 編碼宣告指定) 與伺服器隱含的字串字碼頁不相符。  
  
 如果在使用 NCLOB 或 CLOB 時發生字碼頁或編碼衝突，您必須執行下列其中一個動作：  
  
-   移除 XML 宣告以順利匯入 XML 資料檔的內容。  
  
-   在查詢的 CODEPAGE 選項指定符合 XML 宣告中使用之編碼配置的字碼頁。  
  
-   比對或解析資料庫定序設定與非 Unicode XML 編碼配置。  
  
 [[頁首]](#top)  
  
##  <a name="bulk-importing-xml-data-in-an-existing-row"></a><a name="existing_row"></a> 在現有資料列中大量匯入 XML 資料  
 這個範例使用 `OPENROWSET` 大量資料列集提供者，將 XML 執行個體加入範例資料表 `T`中的現有資料列。  
  
> [!NOTE]  
>  若要執行這個範例，首先必須完成範例 A 提供的測試指令碼。該範例會建立 `tempdb.dbo.T` 資料表，並從 `SampleData3.txt`大量匯入資料。  
  
#### <a name="sample-data-file"></a>範例資料檔  
 範例 B 使用前面範例中的 `SampleData3.txt` 範例資料檔的修改版本。 若要執行此範例，請將此檔案的內容修改如下：  
  
```xml
<Root>  
          <ProductDescription ProductModelID="10">  
             <Summary>Some New Text</Summary>  
          </ProductDescription>  
</Root>  
```  
  
#### <a name="example-b"></a>範例 B  
  
```sql  
-- Query before update shows initial state of XmlCol values.  
SELECT * FROM T  
UPDATE T  
SET XmlCol =(  
SELECT * FROM OPENROWSET(  
   BULK 'C:\SampleFolder\SampleData3.txt',  
           SINGLE_BLOB  
) AS x  
)  
WHERE IntCol = 1;  
GO  
```  
  
 [[頁首]](#top)  
  
## <a name="bulk-importing-xml-data-from-a-file-that-contains-a-dtd"></a><a name="file_contains_dtd"></a> 從包含 DTD 的檔案大量匯入 XML 資料  
  
> [!IMPORTANT]  
>  如果您的 XML 環境不需要文件類型定義 (DTD)，我們建議您不要啟用這項支援。 開啟 DTD 支援會增加您伺服器受攻擊的介面區，以及將它暴露於阻絕服務攻擊的危險。 如果您必須啟用 DTD 支援，可以藉由只處理信任的 XML 文件來減輕此安全性風險。  
  
 在嘗試使用 [bcp](../../tools/bcp-utility.md) 命令，從包含 DTD 的檔案匯入 XML 資料期間，可能會發生類似下列的錯誤：  
  
 「SQLState = 42000、NativeError = 6359」  
  
 「錯誤 = [Microsoft][SQL Server Native Client][ SQL Server]不允許以內部子集 DTD 剖析 XML。 請使用 CONVERT 配合樣式選項 2，啟用有限的內部子集 DTD 支援。」  
  
 「BCP 複製 %s 失敗」  
  
 若要解決這個問題，您可以從包含 DTD 的資料檔匯入 XML 資料，方法是使用 `OPENROWSET(BULK...)` 函數，然後在命令的 `CONVERT` 子句中指定 `SELECT` 選項。 此命令的基本語法如下：  
  
 `INSERT ... SELECT CONVERT(...) FROM OPENROWSET(BULK...)`  
  
#### <a name="sample-data-file"></a>範例資料檔  
 在測試這個大量匯入範例之前，請建立包含下列範例執行個體的檔案 (`C:\temp\Dtdfile.xml`)：  
  
```xml 
<!DOCTYPE DOC [<!ATTLIST elem1 attr1 CDATA "defVal1">]><elem1>January</elem1>  
```  
  
#### <a name="sample-table"></a>範例資料表  
 範例 C 使用由下列 `T1` 陳述式所建立的 `CREATE TABLE` 範例資料表：  
  
```sql  
USE tempdb;  
CREATE TABLE T1(XmlCol xml);  
GO  
```  
  
#### <a name="example-c"></a>範例 C  
 這個範例使用 `OPENROWSET(BULK...)` ，並在 `CONVERT` 子句中指定 `SELECT` 選項，將 XML 資料從 `Dtdfile.xml` 匯入範例資料表 `T1`。  
  
```sql
INSERT T1  
  SELECT CONVERT(xml, BulkColumn, 2) FROM   
    OPENROWSET(Bulk 'c:\temp\Dtdfile.xml', SINGLE_BLOB) [rowsetresults];  
```  
  
 在執行 `INSERT` 陳述式之後，會從 XML 移除 DTD，並將它儲存在 `T1` 資料表中。  
  
 [[頁首]](#top)  
  
## <a name="specifying-the-field-terminator-explicitly-using-a-format-file"></a><a name="field_terminator_in_format_file"></a> 使用格式檔案明確指定欄位結束字元  
 下列範例顯示如何大量匯入下列 XML 文件 `Xmltable.dat`。  
  
#### <a name="sample-data-file"></a>範例資料檔  
 `Xmltable.dat` 中的文件包含兩個 XML 值，每列各有一個值。 第一個 XML 值是以 UTF-16 編碼，而第二個值則是以 UTF-8 編碼。  
  
 這個資料檔的內容顯示在下列十六進位傾印中：  
  
```  
FF FE 3C 00 3F 00 78 00-6D 00 6C 00 20 00 76 00  *..\<.?.x.m.l. .v.*  
65 00 72 00 73 00 69 00-6F 00 6E 00 3D 00 22 00  *e.r.s.i.o.n.=.".*  
31 00 2E 00 30 00 22 00-20 00 65 00 6E 00 63 00  *1...0.". .e.n.c.*  
6F 00 64 00 69 00 6E 00-67 00 3D 00 22 00 75 00  *o.d.i.n.g.=.".u.*  
74 00 66 00 2D 00 31 00-36 00 22 00 3F 00 3E 00  *t.f.-.1.6.".?.>.*  
3C 00 72 00 6F 00 6F 00-74 00 3E 00 A2 4F 9C 76  *\<.r.o.o.t.>..O.v*  
0C FA 77 E4 80 00 89 00-00 06 90 06 91 2E 9B 2E  *..w.............*  
99 34 A2 34 86 00 83 02-92 20 7F 02 4E C5 E4 A3  *.4.4..... ..N...*  
34 B2 B7 B3 B7 FE F8 FF-F8 00 3C 00 2F 00 72 00  *4.........\<./.r.*  
6F 00 6F 00 74 00 3E 00-00 00 00 00 7A EF BB BF  *o.o.t.>.....z...*  
3C 3F 78 6D 6C 20 76 65-72 73 69 6F 6E 3D 22 31  *\<?xml version="1*  
2E 30 22 20 65 6E 63 6F-64 69 6E 67 3D 22 75 74  *.0" encoding="ut*  
66 2D 38 22 3F 3E 3C 72-6F 6F 74 3E E4 BE A2 E7  *f-8"?><root>....*  
9A 9C EF A8 8C EE 91 B7-C2 80 C2 89 D8 80 DA 90  *................*  
E2 BA 91 E2 BA 9B E3 92-99 E3 92 A2 C2 86 CA 83  *................*  
E2 82 92 C9 BF EC 95 8E-EA 8F A4 EB 88 B4 EB 8E  *................*  
B7 EF BA B7 EF BF B8 C3-B8 3C 2F 72 6F 6F 74 3E  *.........</root>*  
00 00 00 00 7A                                   *....z*  
```  
  
#### <a name="sample-table"></a>範例資料表  
 當大量匯入或匯出 XML 文件時，您應該使用任何文件都無法顯示的 [欄位結束字元](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md) ；例如，連續四個 Null (`\0`) 後面接著字母 `z`： `\0\0\0\0z`。  
  
 這個範例顯示如何將這個欄位結束字元使用於 `xTable` 範例資料表。 若要建立這個範例資料表，請使用下列 `CREATE TABLE` 陳述式：  
  
```sql
USE tempdb;  
CREATE TABLE xTable (xCol xml);  
GO  
```  
  
#### <a name="sample-format-file"></a>範例格式檔案  
 在格式檔案中必須指定欄位結束字元。 範例 D 使用名為 `Xmltable.fmt` 的非 XML 格式檔案，其中包含下列內容：  
  
```  
9.0  
1  
1       SQLBINARY     0       0       "\0\0\0\0z"    1     xCol         ""  
```  
  
 您可以使用這個格式檔案，將 XML 文件大量匯入 `xTable` 資料表，方法是使用 `bcp` 命令或 `BULK INSERT` 或 `INSERT ... SELECT * FROM OPENROWSET(BULK...)` 陳述式。  
  
#### <a name="example-d"></a>範例 D  
 這個範例在 `Xmltable.fmt` 陳述式中使用 `BULK INSERT` 格式檔案，以匯入名為 `Xmltable.dat`之 XML 資料檔的內容。  
  
```sql
BULK INSERT xTable   
FROM 'C:\Xmltable.dat'  
WITH (FORMATFILE = 'C:\Xmltable.fmt');  
GO  
```  
  
 [[頁首]](#top)  
  
## <a name="bulk-exporting-xml-data"></a><a name="bulk_export_xml_data"></a> 大量匯出 XML 資料  
 下列範例使用 [bcp](../../tools/bcp-utility.md) 從前面範例所建立的資料表 (使用相同的 XML 格式檔案) 大量匯入 XML 資料。 在下列 `bcp` 命令中， `<server_name>` 和 `<instance_name>` 代表必須以適當值取代的預留位置：  
  
```cmd
bcp bulktest..xTable out a-wn.out -N -T -S<server_name>\<instance_name>  
```  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 當 XML 資料保存於資料庫時，並不會儲存 XML 編碼。 因此，一旦匯出 XML 資料之後，便無法使用 XML 欄位的原始編碼。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會在匯出 XML 資料時使用 UTF-16 編碼。  
  

## <a name="see-also"></a>另請參閱  
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [SELECT 子句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-clause-transact-sql.md)   
 [bcp 公用程式](../../tools/bcp-utility.md)   
 [資料的大量匯入及匯出 &#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)  
  
  
