---
title: 建立格式檔案 (SQL Server) | Microsoft 文件
ms.custom: ''
ms.date: 02/23/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- format files [SQL Server], creating
ms.assetid: f680b4a0-630f-4052-9c79-d348c1076f7b
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: cdf0e6510d566fbf2ad31ebf9996ca27ad444eda
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2018
ms.locfileid: "51677127"
---
# <a name="create-a-format-file-sql-server"></a>建立格式檔案 (SQL Server)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  當您將資料大量匯入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表，或從資料表大量匯出資料時，可以使用格式檔案提供可用來寫入資料檔的彈性系統，幾乎不需要進行編輯即可符合其他資料格式，或是從其他軟體程式讀取資料檔。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援兩種類型的格式檔案：非 XML 格式和 XML 格式。 非 XML 格式是舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]所支援的原始格式。  
  
 一般而言，XML 和非 XML 格式檔案可以互換使用， 但是，仍建議您在新的格式檔案中使用 XML 語法，因為 XML 比非 XML 格式檔案多了一些優點。  
  
> [!NOTE]  
>  用於讀取格式檔案的 **bcp** 公用程式 (Bcp.exe) 版本，必須與用於建立格式檔案的版本相同或比它更新。 例如， [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]**bcp** 可以讀取由 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]**bcp**產生的 10.0 版的格式檔案，但 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]**bcp** 無法讀取由 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]**bcp**所產生的 11.0 版格式檔案。  
  
 此主題描述如何使用 [bcp 公用程式](../../tools/bcp-utility.md) 來建立特定資料表的格式檔案。 格式檔案以指定的資料類型選項 (**-n**、 **-c**、 **-w**，或 **-N**) 與資料表或檢視分隔符號為基礎。  
  
## <a name="creating-a-non-xml-format-file"></a>建立非 XML 格式檔案  
 使用 **bcp** 命令建立格式檔案時，請指定 **format** 引數並使用 **nul** 取代資料檔案路徑。 **format** 選項也需要 **-f** 選項，例如：  
  
 **bcp** *table_or_view* **format** nul **-f***format_file_name*  
  
> [!NOTE]  
>  為了區分非 XML 格式檔案，建議您使用 .fmt 做為副檔名，例如 MyTable.fmt。  
  
 如需有關非 XML 格式檔案之結構與欄位的詳細資訊，請參閱 [非 XML 格式檔案 &#40;SQL Server&#41;](../../relational-databases/import-export/non-xml-format-files-sql-server.md)所支援的原始格式。  
  
### <a name="examples"></a>範例  
 本節包含下列範例，說明如何使用 **bcp** 命令建立非 XML 格式檔案：  
  
-   A. 建立原生資料的非 XML 格式檔案  
  
-   B. 建立字元資料的非 XML 格式檔案  
  
-   C. 建立 Unicode 原生資料的非 XML 格式檔案  
  
-   D. 建立 Unicode 字元資料的非 XML 格式檔案  
  
-   F. 使用格式檔案與字碼頁選項  
  
 這些範例使用 `HumanResources.Department` 範例資料庫中的 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料表。 `HumanResources.Department` 資料表包含四個資料行： `DepartmentID`、 `Name`、 `GroupName`和 `ModifiedDate`。  
  
#### <a name="a-creating-a-non-xml-format-file-for-native-data"></a>A. 建立原生資料的非 XML 格式檔案  
 下列範例會建立 `Department-n.xml`資料表的 XML 格式檔案 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]`HumanResources.Department` 。 格式檔案使用原生資料類型。 所產生之格式檔案的內容，會出現在命令之後。  
  
 **bcp** 命令包含下列限定詞。  
  
|限定詞|Description|  
|----------------|-----------------|  
|**formatnul f** *format_file*|指定非 XML 格式檔案。|  
|**-n**|指定原生資料類型。|  
|**-T**|指定 **bcp** 公用程式使用整合式安全性的信任連接，連接至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如果未指定 **-T** ，則必須指定 **-U** 與 **-P** ，才能順利登入。|  
  
 在 Windows 命令提示字元中，輸入下列 `bcp` 命令：  
  
```cmd
bcp AdventureWorks2012.HumanResources.Department format nul -T -n -f Department-n.fmt  
```  
  
 產生的格式檔案 `Department-n.fmt`包含下列資訊：  
  
```  
12.0  
4  
1  SQLSMALLINT   0       2       ""   1     DepartmentID         ""  
2  SQLNCHAR      2       100     ""   2     Name                 SQL_Latin1_General_CP1_CI_AS  
3  SQLNCHAR      2       100     ""   3     GroupName            SQL_Latin1_General_CP1_CI_AS  
4  SQLDATETIME   0       8       ""   4     ModifiedDate         ""  
```  
  
 如需詳細資訊，請參閱 [非 XML 格式檔案 &#40;SQL Server&#41;](../../relational-databases/import-export/non-xml-format-files-sql-server.md)所支援的原始格式。  
  
#### <a name="b-creating-a-non-xml-format-file-for-character-data"></a>B. 建立字元資料的非 XML 格式檔案  
 下列範例會建立 `Department.fmt`資料表的 XML 格式檔案 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]`HumanResources.Department` 。 格式檔案使用字元資料格式和非預設欄位結束字元 (`,`)。 所產生之格式檔案的內容，會出現在命令之後。  
  
 **bcp** 命令包含下列限定詞。  
  
|限定詞|Description|  
|----------------|-----------------|  
|**formatnul f** *format_file*|指定非 XML 格式檔案。|  
|**-c**|指定字元資料。|  
|**-T**|指定 **bcp** 公用程式使用整合式安全性的信任連接，連接至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如果未指定 **-T** ，則必須指定 **-U** 與 **-P** ，才能順利登入。|  
  
 在 Windows 命令提示字元中，輸入下列 `bcp` 命令：  
  
```cmd
bcp AdventureWorks2012.HumanResources.Department format nul -c -f Department-c.fmt -T  
```  
  
 產生的格式檔案 `Department-c.fmt`包含下列資訊：  
  
```  
12.0  
4  
1  SQLCHAR       0       7       "\t"     1     DepartmentID            ""  
2  SQLCHAR       0       100     "\t"     2     Name                    SQL_Latin1_General_CP1_CI_AS  
3  SQLCHAR       0       100     "\t"     3     GroupName               SQL_Latin1_General_CP1_CI_AS  
4  SQLCHAR       0       24      "\r\n"   4     ModifiedDate            ""  
```  
  
 如需詳細資訊，請參閱 [非 XML 格式檔案 &#40;SQL Server&#41;](../../relational-databases/import-export/non-xml-format-files-sql-server.md)所支援的原始格式。  
  
#### <a name="c-creating-a-non-xml-format-file-for-unicode-native-data"></a>C. 建立 Unicode 原生資料的非 XML 格式檔案  
 若要針對 `HumanResources.Department` 資料表的 Unicode 原生資料建立非 XML 格式檔案，請使用下列命令：  
  
```cmd
bcp AdventureWorks2012.HumanResources.Department format nul -T -N -f Department-n.fmt  
```  
  
 如需如何使用 Unicode 原生資料的詳細資訊，請參閱[使用 Unicode 原生格式匯入或匯出資料 &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)。  
  
#### <a name="d-creating-a-non-xml-format-file-for-unicode-character-data"></a>D. 建立 Unicode 字元資料的非 XML 格式檔案  
 若要針對使用預設結束字元之 `HumanResources.Department` 資料表的 Unicode 字元資料建立非 XML 格式檔案，請使用下列命令：  
  
```cmd
bcp AdventureWorks2012.HumanResources.Department format nul -T -w -f Department-w.fmt  
```  
  
 如需如何使用 Unicode 字元資料的詳細資訊，請參閱[使用 Unicode 字元格式匯入或匯出資料 &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)。  
  
#### <a name="f-using-a-format-file-with-the-code-page-option"></a>F. 使用格式檔案與字碼頁選項  
若使用 bcp 命令 (也就是 `bcp format`) 建立格式檔案，就會在格式檔案中寫入定序/字碼頁的資訊。   
下列範例格式檔案屬於具 5 個資料行的資料表且包含定序。  
  
```  
13.0  
5  
1  SQLCHAR         0       0       "**\t**"         1     c_0          Cyrillic_General_CS_AS  
2  SQLCHAR         0       0       "**\t**"         2     c_1          Cyrillic_General_CS_AS  
3  SQLCHAR         0       3000    "**\t**"         3     c_2          Cyrillic_General_CS_AS  
4  SQLCHAR         0       5       "**\t**"         4     c_3          ""  
5  SQLCHAR         0       41      "!!!\r\r\n"      5     c_4          ""  
  
```  
  
 如果您嘗試使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ...” 將資料匯入 `bcp in –c –C65001 –f format_file` 或 “`BULK INSERT`/`OPENROWSET` … `FORMATFILE='format_file' CODEPAGE=65001` …”，則定序/字碼頁的相關資訊將會優先於 65001 選項。  
因此，如果您產生格式檔案，則必須從產生的格式檔案手動刪除定序資訊，然後才開始將資料匯回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
下列範例為不具定序資訊的格式檔案。  
  
```  
13.0  
5  
1  SQLCHAR         0       0       "**\t**"         1     c_0              ""  
2  SQLCHAR         0       0       "**\t**"         2     c_1              ""  
3  SQLCHAR         0       3000    "**\t**"         3     c_2              ""  
4  SQLCHAR         0       5       "**\t**"         4     c_3              ""  
5  SQLCHAR         0       41      "!!!\r\r\n"      5     c_4              ""  
```  
  
## <a name="creating-an-xml-format-file"></a>建立 XML 格式檔案  
 使用 **bcp** 命令建立格式檔案時，請指定 **format** 引數並使用 **nul** 取代資料檔案路徑。 **format** 選項一律需要 **-f** 選項，您也必須指定 **-x** 選項才能建立 XML 格式檔案，例如：  
  
 **bcp** *table_or_view* **format nul-f** *format_file_name* **-x**  
  
> [!NOTE]  
>  為了區分 XML 格式檔案，建議您使用 .xml 做為副檔名，例如 MyTable.xml。  
  
 如需有關 XML 格式檔案之結構與欄位的詳細資訊，請參閱 [XML 格式檔案 &#40;SQL Server&#41;](../../relational-databases/import-export/xml-format-files-sql-server.md)所支援的原始格式。  
  
### <a name="examples"></a>範例  
 本節包含下列範例，說明如何使用 **bcp** 命令建立 XML 格式檔案：  
  
-   A. 建立字元資料的 XML 格式檔案  
  
-   B. 建立原生資料的 XML 格式檔案  
  
 這些範例使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 範例資料庫中的 `HumanResources.Department` 資料表。 `HumanResources.Department` 資料表包含四個資料行： `DepartmentID`、 `Name`、 `GroupName`和 `ModifiedDate`。  
  
> [!NOTE]  
>  [!INCLUDE[ssSampleDBdesc](../../includes/sssampledbdesc-md.md)]  
  
#### <a name="a-creating-an-xml-format-file-for-character-data"></a>A. 建立字元資料的 XML 格式檔案  
 下列範例會建立 `Department.xml`資料表的 XML 格式檔案 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]`HumanResources.Department` 。 格式檔案使用字元資料格式和非預設欄位結束字元 (`,`)。 所產生之格式檔案的內容，會出現在命令之後。  
  
 **bcp** 命令包含下列限定詞。  
  
|限定詞|Description|  
|----------------|-----------------|  
|**formatnul f** *format_file* **-x**|指定 XML 格式檔案。|  
|**-c**|指定字元資料。|  
|**-t** `,`|指定逗號 (**,**) 作為欄位結束字元。<br /><br /> 注意：如果資料檔案使用預設欄位結束字元 (`\t`)，則不需要 **-t** 參數。|  
|**-T**|指定 **bcp** 公用程式使用整合式安全性的信任連接，連接至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如果未指定 **-T** ，則必須指定 **-U** 與 **-P** ，才能順利登入。|  
  
 在 Windows 命令提示字元中，輸入下列 `bcp` 命令：  
  
```cmd
bcp AdventureWorks2012.HumanResources.Department format nul -c -x -f Department-c..xml –t, -T  
```  
  
 產生的格式檔案 `Department-c.xml`包含下列 XML 元素：  
  
```xml
<?xml version="1.0"?>  
<BCPFORMAT xmlns="https://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance">  
 <RECORD>  
  <FIELD ID="1" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="7"/>  
  <FIELD ID="2" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  <FIELD ID="3" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  <FIELD ID="4" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="24"/>  
 </RECORD>  
 <ROW>  
  <COLUMN SOURCE="1" NAME="DepartmentID" xsi:type="SQLSMALLINT"/>  
  <COLUMN SOURCE="2" NAME="Name" xsi:type="SQLNVARCHAR"/>  
  <COLUMN SOURCE="3" NAME="GroupName" xsi:type="SQLNVARCHAR"/>  
  <COLUMN SOURCE="4" NAME="ModifiedDate" xsi:type="SQLDATETIME"/>  
 </ROW>  
</BCPFORMAT>  
```  
  
 如需本格式檔案語法的相關資訊，請參閱 [XML 格式檔案 &#40;SQL Server&#41;](../../relational-databases/import-export/xml-format-files-sql-server.md)。 如需字元資料的相關資訊，請參閱[使用字元格式匯入或匯出資料 &#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)。  
  
#### <a name="b-creating-an-xml-format-file-for-native-data"></a>B. 建立原生資料的 XML 格式檔案  
 下列範例會建立 `Department-n.xml`資料表的 XML 格式檔案 `HumanResources.Department` 。 格式檔案使用原生資料類型。 所產生之格式檔案的內容，會出現在命令之後。  
  
 **bcp** 命令包含下列限定詞。  
  
|限定詞|Description|  
|----------------|-----------------|  
|**formatnul f** *format_file* **-x**|指定 XML 格式檔案。|  
|**-n**|指定原生資料類型。|  
|**-T**|指定 **bcp** 公用程式使用整合式安全性的信任連接，連接至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如果未指定 **-T** ，則必須指定 **-U** 與 **-P** ，才能順利登入。|  
  
 在 Windows 命令提示字元中，輸入下列 `bcp` 命令：  
  
```cmd
bcp AdventureWorks2012.HumanResources.Department format nul -x -f Department-n..xml -n -T  
```  
  
 產生的格式檔案 `Department-n.xml`包含下列 XML 元素：  
  
```xml
<?xml version="1.0"?>  
<BCPFORMAT xmlns="https://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance">  
 <RECORD>  
  <FIELD ID="1" xsi:type="NativeFixed" LENGTH="2"/>  
  <FIELD ID="2" xsi:type="NCharPrefix" PREFIX_LENGTH="2" MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  <FIELD ID="3" xsi:type="NCharPrefix" PREFIX_LENGTH="2" MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  <FIELD ID="4" xsi:type="NativeFixed" LENGTH="8"/>  
 </RECORD>  
 <ROW>  
  <COLUMN SOURCE="1" NAME="DepartmentID" xsi:type="SQLSMALLINT"/>  
  <COLUMN SOURCE="2" NAME="Name" xsi:type="SQLNVARCHAR"/>  
  <COLUMN SOURCE="3" NAME="GroupName" xsi:type="SQLNVARCHAR"/>  
  <COLUMN SOURCE="4" NAME="ModifiedDate" xsi:type="SQLDATETIME"/>  
 </ROW>  
</BCPFORMAT>  
```  
  
 如需本格式檔案語法的相關資訊，請參閱 [XML 格式檔案 &#40;SQL Server&#41;](../../relational-databases/import-export/xml-format-files-sql-server.md)。 如需如何使用原生資料的相關資訊，請參閱[使用原生格式匯入或匯出資料 &#40;SQL Server&#41;](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)。  
  
## <a name="mapping-data-fields-to-table-columns"></a>將資料欄位對應至資料表資料行  
 格式檔案由 **bcp**建立後，便會依序描述所有的資料表資料行。 您可以修改格式檔案，重新排列或省略資料表資料列。 這可讓您針對欄位未直接對應至資料表資料行的資料檔來自訂格式檔案。 如需詳細資訊，請參閱下列主題：  
  
-   [使用格式檔案略過資料表資料行 &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
-   [使用格式檔案略過資料欄位 &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
-   [使用格式檔案將資料表資料行對應至資料檔案欄位 &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
## <a name="see-also"></a>另請參閱  
 [bcp 公用程式](../../tools/bcp-utility.md)   
 [使用格式檔案將資料表資料行對應至資料檔案欄位 &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)   
 [使用格式檔案略過資料表資料行 &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)   
 [使用格式檔案略過資料欄位 &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)   
 [非 XML 格式檔案 &#40;SQL Server&#41;](../../relational-databases/import-export/non-xml-format-files-sql-server.md)   
 [XML 格式檔案 &#40;SQL Server&#41;](../../relational-databases/import-export/xml-format-files-sql-server.md)  
  
  
