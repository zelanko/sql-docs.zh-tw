---
title: 修改 ADO.NET 中的大型數值 (max) 資料
description: 描述如何使用大數值資料類型。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 8aca5f00-d80e-4320-81b3-016d0466f7ee
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 9acbd8fb795fe1a14e77e5d746f729d37c11cc8d
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "78896679"
---
# <a name="modifying-large-value-max-data-in-adonet"></a>修改 ADO.NET 中的大型數值 (max) 資料

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

大型物件 (LOB) 資料類型是指資料列大小上限超過 8 KB 的資料類型。 SQL Server 提供 `varchar`、`nvarchar` 和 `varbinary` 資料類型的 `max` 規範，允許儲存最大達 2^32 位元組的值。 資料表資料行和 Transact-SQL 變數可能會指定 `varchar(max)`、`nvarchar(max)` 或 `varbinary(max)` 資料類型。 在 .NET 中，`max` 資料類型可透過 `DataReader` 來擷取，也可指定為輸入及輸出參數值，並且不需要任何特殊處理。 對於大型 `varchar` 資料類型，可以使用累加方式來擷取和更新資料。  
  
`max` 資料類型可用於比較 (作為 Transact-SQL 變數) 及串連。 它們也可用於 SELECT 陳述式的 DISTINCT、ORDER BY、GROUP BY 子句中，以及彙總、聯結和子查詢中。

如需大數值資料類型的詳細資訊，請參閱《SQL Server 線上叢書》的[使用大數值資料類型](https://go.microsoft.com/fwlink/?LinkId=120498)。
  
## <a name="large-value-type-restrictions"></a>大數值類型限制  
下列限制適用於 `max` 資料類型，較小的資料類型則不存在這些限制：  
  
- `sql_variant` 不能包含大型 `varchar` 資料類型。  
  
- 大型 `varchar` 資料行不能指定為索引中的索引鍵資料行。 但能夠在非叢集索引的內含資料行中加以使用。  
  
- 大型 `varchar` 資料行不能用來作為資料分割索引鍵資料行。  
  
## <a name="working-with-large-value-types-in-transact-sql"></a>在 Transact-SQL 中使用大數值類型  
Transact-SQL `OPENROWSET` 函數是連線和存取遠端資料的一次性方法。 您可以依照資料表名稱的相同方式，在查詢的 FROM 子句中參考 `OPENROWSET`。 其也可以當作 INSERT、UPDATE 或 DELETE 陳述式的目標資料表加以參考。  
  
`OPENROWSET` 函數包含 `BULK` 資料列集提供者，可讓您直接從檔案讀取資料，而不需要將資料載入到目標資料表中。 這可讓您在簡單的 INSERT SELECT 陳述式中使用 `OPENROWSET`。  
  
`OPENROWSET BULK` 選項引數可有效地控制何處開始及結束讀取資料、如何處理錯誤，以及如何解譯資料。 例如，您可以指定讓資料檔案當作 `varbinary`、`varchar` 或 `nvarchar` 類型的單一資料列、單一資料行資料列集加以讀取。 如需完整的語法和選項，請參閱《SQL Server 線上叢書》。  
  
下列範例會在 AdventureWorks 範例資料庫的 ProductPhoto 資料表中插入相片。 使用 `BULK OPENROWSET` 提供者時，即使未將值插入每個資料行，也必須提供資料行的具名清單。 此案例中的主索引鍵會定義為識別資料行，而且可能會從資料行清單中省略。 請注意，您也必須在 `OPENROWSET` 陳述式的結尾提供相互關聯名稱，在此案例中為 ThumbnailPhoto。 這會與載入檔案之 `ProductPhoto` 資料表中的資料行相互關聯。  
  
```sql
INSERT Production.ProductPhoto (  
    ThumbnailPhoto,   
    ThumbnailPhotoFilePath,   
    LargePhoto,   
    LargePhotoFilePath)  
SELECT ThumbnailPhoto.*, null, null, N'tricycle_pink.gif'  
FROM OPENROWSET   
    (BULK 'c:\images\tricycle.jpg', SINGLE_BLOB) ThumbnailPhoto  
```  
  
## <a name="updating-data-using-update-write"></a>使用 UPDATE .WRITE 更新資料  
Transact-SQL UPDATE 陳述式具有新的 WRITE 語法，可用於修改 `varchar(max)`、`nvarchar(max)` 或 `varbinary(max)` 資料行的內容。 這可讓您執行資料的部分更新。 此處會以縮寫形式顯示 UPDATE .WRITE 語法：  
  
UPDATE  
  
{ *\<object>* }  
  
SET  
  
{ *column_name* = { .WRITE ( *expression* , @Offset , @Length ) }  
  
WRITE 方法指定將對 *column_name* 值的某個區段進行修改。 其中，expression 是要複製到 *column_name* 的值；`@Offset` 是要寫入運算式的起點；`@Length` 引數是資料行中區段的長度。  
  
|If|結果為|  
|--------|----------|  
|運算式會設定為 NULL|系統會忽略 `@Length`，並會將 *column_name* 中的值在指定的 `@Offset` 處截斷。|  
|`@Offset` 是 NULL|更新作業會在現有 *column_name* 值的結尾處附加運算式，並且會忽略 `@Length`。|  
|`@Offset` 大於 column_name 值的長度|SQL Server 會傳回錯誤。|  
|`@Length` 是 NULL|更新作業會移除從 `@Offset` 到 `column_name` 值結尾的所有資料。|  
  
> [!NOTE]
>  `@Offset` 和 `@Length` 都不能是負數。  
  
## <a name="example"></a>範例  
這個 Transact-SQL 範例會更新 DocumentSummary 中的部分值，這是 AdventureWorks 資料庫內 Document 資料表中的 `nvarchar(max)` 資料行。 'components' 一字藉由指定取代文字、現有資料中要取代之文字的起始位置 (位移)，以及要取代的字元數 (長度) 來取代為 'features' 一字。 此範例會在 UPDATE 陳述式前後包含 SELECT 陳述式來比較結果。  
  
```sql
USE AdventureWorks;  
GO  
--View the existing value.  
SELECT DocumentSummary  
FROM Production.Document  
WHERE DocumentID = 3;  
GO  
-- The first sentence of the results will be:  
-- Reflectors are vital safety components of your bicycle.  
  
--Modify a single word in the DocumentSummary column  
UPDATE Production.Document  
SET DocumentSummary .WRITE (N'features',28,10)  
WHERE DocumentID = 3 ;  
GO   
--View the modified value.  
SELECT DocumentSummary  
FROM Production.Document  
WHERE DocumentID = 3;  
GO  
-- The first sentence of the results will be:  
-- Reflectors are vital safety features of your bicycle.  
```  
  
## <a name="working-with-large-value-types-in-adonet"></a>在 ADO.NET 中使用大數值類型  
您可以在 ADO.NET 中使用大數值類型，方法是將大數值類型指定為 <xref:Microsoft.Data.SqlClient.SqlDataReader> 中的 <xref:Microsoft.Data.SqlClient.SqlParameter> 物件以傳回結果集，或使用 <xref:Microsoft.Data.SqlClient.SqlDataAdapter> 來填滿 `DataSet`/`DataTable`。 您使用大數值類型及其相關且較小數值資料類型的方式並無任何差異。  
  
### <a name="using-getsqlbytes-to-retrieve-data"></a>使用 GetSqlBytes 來擷取資料  
<xref:Microsoft.Data.SqlClient.SqlDataReader> 的 `GetSqlBytes` 方法可以用來擷取 `varbinary(max)` 資料行的內容。 下列程式碼片段會假設一個名為 `cmd` 的 <xref:Microsoft.Data.SqlClient.SqlCommand> 物件 (此物件會從資料表中選取 `varbinary(max)` 資料)，以及一個名為 `reader` 的 <xref:Microsoft.Data.SqlClient.SqlDataReader> 物件 (此物件會以 <xref:System.Data.SqlTypes.SqlBytes> 形式來擷取資料)。  
  
```csharp  
reader = cmd.ExecuteReader(CommandBehavior.CloseConnection);  
while (reader.Read())  
    {  
        SqlBytes bytes = reader.GetSqlBytes(0);  
    }  
```  
  
### <a name="using-getsqlchars-to-retrieve-data"></a>使用 GetSqlChars 來擷取資料  
<xref:Microsoft.Data.SqlClient.SqlDataReader> 的 `GetSqlChars` 方法可以用來擷取 `varchar(max)` 或 `nvarchar(max)` 資料行的內容。 下列程式碼片段會假設一個名為 `cmd` 的 <xref:Microsoft.Data.SqlClient.SqlCommand> 物件 (此物件會從資料表中選取 `nvarchar(max)` 資料)，以及一個名為 `reader` 的 <xref:Microsoft.Data.SqlClient.SqlDataReader> 物件 (此物件會擷取資料)。   
  
```csharp  
reader = cmd.ExecuteReader(CommandBehavior.CloseConnection);  
while (reader.Read())  
{  
    SqlChars buffer = reader.GetSqlChars(0);  
}  
```  
  
### <a name="using-getsqlbinary-to-retrieve-data"></a>使用 GetSqlBinary 來擷取資料  
<xref:Microsoft.Data.SqlClient.SqlDataReader> 的 `GetSqlBinary` 方法可以用來擷取 `varbinary(max)` 資料行的內容。 下列程式碼片段會假設一個名為 `cmd` 的 <xref:Microsoft.Data.SqlClient.SqlCommand> 物件 (此物件會從資料表中選取 `varbinary(max)` 資料)，以及一個名為 `reader` 的 <xref:Microsoft.Data.SqlClient.SqlDataReader> 物件 (此物件會以 <xref:System.Data.SqlTypes.SqlBinary> 資料流形式來擷取資料)。  
  
```csharp  
reader = cmd.ExecuteReader(CommandBehavior.CloseConnection);  
while (reader.Read())  
    {  
        SqlBinary binaryStream = reader.GetSqlBinary(0);  
    }  
```  
  
### <a name="using-getbytes-to-retrieve-data"></a>使用 GetBytes 來擷取資料  
<xref:Microsoft.Data.SqlClient.SqlDataReader> 的 `GetBytes` 方法可將指定資料行位移的位元組資料流，讀取到始於指定陣列位移的位元組陣列。 下列程式碼片段會假設一個名為 `reader` 的 <xref:Microsoft.Data.SqlClient.SqlDataReader> 物件，此物件可將位元組擷取到位元組陣列。 請注意，不同於 `GetSqlBytes`，`GetBytes` 需要陣列緩衝區的大小。  
  
```csharp  
while (reader.Read())  
{  
    byte[] buffer = new byte[4000];  
    long byteCount = reader.GetBytes(1, 0, buffer, 0, 4000);  
}  
```  
  
### <a name="using-getvalue-to-retrieve-data"></a>使用 GetValue 來擷取資料  
<xref:Microsoft.Data.SqlClient.SqlDataReader> 的 `GetValue` 方法會將指定資料行位移中的值讀取到陣列。 下列程式碼片段會假設一個名為 `reader` 的 <xref:Microsoft.Data.SqlClient.SqlDataReader> 物件，此物件會從第一個資料行位移中擷取二進位資料，然後從第二個資料行位移中擷取字串資料。  
  
```csharp  
while (reader.Read())  
{  
    // Read the data from varbinary(max) column  
    byte[] binaryData = (byte[])reader.GetValue(0);  
  
    // Read the data from varchar(max) or nvarchar(max) column  
    String stringData = (String)reader.GetValue(1);  
}  
```  
  
## <a name="converting-from-large-value-types-to-clr-types"></a>從大數值類型轉換為 CLR 類型  
您可以使用任何字串轉換方法 (例如 `ToString`)，來轉換 `varchar(max)` 或 `nvarchar(max)` 資料行的內容。 下列程式碼片段會假設一個名為 `reader` 的 <xref:Microsoft.Data.SqlClient.SqlDataReader> 物件，此物件會擷取資料。  
  
```csharp  
while (reader.Read())  
{  
     string str = reader[0].ToString();  
     Console.WriteLine(str);  
}  
```  
  
### <a name="example"></a>範例  
下列程式碼會從 `AdventureWorks` 資料庫中的 `ProductPhoto` 資料表，擷取名稱和 `LargePhoto` 物件，並將其儲存到檔案。 此組件必須以 <xref:System.Drawing> 命名空間的參考進行編譯。  <xref:Microsoft.Data.SqlClient.SqlDataReader> 的 <xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlBytes%2A> 方法會傳回 <xref:System.Data.SqlTypes.SqlBytes> 物件，此物件會公開 `Stream` 屬性。 該程式碼會使用此物件來建立新的 `Bitmap` 物件，然後將其儲存為 Gif `ImageFormat`。  
  
[!code-csharp[DataWorks SqlBytes_Stream#1](~/../sqlclient/doc/samples/SqlBytes_Stream.cs#1)]
  
## <a name="using-large-value-type-parameters"></a>使用大數值類型參數  
大數值類型可以用於 <xref:Microsoft.Data.SqlClient.SqlParameter> 物件中，就像您在 <xref:Microsoft.Data.SqlClient.SqlParameter> 物件中使用較小數值類型一樣。 您可以將大數值類型擷取為 <xref:Microsoft.Data.SqlClient.SqlParameter> 值，如下列範例所示。 此程式碼假設下列 GetDocumentSummary 預存程序存在於 AdventureWorks 範例資料庫中。 預存程序會接受名為 @DocumentID 的輸入參數，並在 @DocumentSummary 輸出參數中傳回 DocumentSummary 資料行的內容。  
  
```sql
CREATE PROCEDURE GetDocumentSummary   
(  
    @DocumentID int,  
    @DocumentSummary nvarchar(MAX) OUTPUT  
)  
AS  
SET NOCOUNT ON  
SELECT  @DocumentSummary=Convert(nvarchar(MAX), DocumentSummary)  
FROM    Production.Document  
WHERE   DocumentID=@DocumentID  
```  
  
### <a name="example"></a>範例  
ADO.NET 程式碼會建立 <xref:Microsoft.Data.SqlClient.SqlConnection> 和 <xref:Microsoft.Data.SqlClient.SqlCommand> 物件來執行 GetDocumentSummary 預存程序，並擷取要儲存為大數值類型的文件摘要。 該程式碼會傳遞 @DocumentID 輸入參數的值，並會在 [主控台] 視窗中顯示 @DocumentSummary 輸出參數中傳回的結果。  
  
[!code-csharp[DataWorks SqlParameter_Value#1](~/../sqlclient/doc/samples/SqlParameter_Value.cs#1)]
  
## <a name="next-steps"></a>後續步驟
- [SQL Server 二進位和大型數值資料](sql-server-binary-large-value-data.md)
- [ADO.NET 中的 SQL Server 資料作業](sql-server-data-operations.md)
