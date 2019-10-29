---
title: 處理 Null 值
description: 示範如何在 SQL Server 和 .NET 中使用 GUID 和 uniqueidentifier 值。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: f18b288f-b265-4bbe-957f-c6833c0645ef
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 6ae2bc8d816dd2bc32572447483dacd76dd967f0
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452194"
---
# <a name="handling-null-values"></a>處理 Null 值

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[下載 ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

當資料行中的值不明或遺失時，會使用關係資料庫中的 null 值。 Null 不是空字串（適用于字元或 datetime 資料類型），也不是零值（適用于數值資料類型）。 ANSI SQL-92 規格指出所有資料類型的 null 必須相同，因此所有的 null 都是以一致的方式處理。 <xref:System.Data.SqlTypes> 命名空間會藉由執行 <xref:System.Data.SqlTypes.INullable> 介面來提供 null 的語義。 <xref:System.Data.SqlTypes> 中的每個資料類型都有自己的 `IsNull` 屬性，以及可指派給該資料類型之實例的 `Null` 值。  
  
> [!NOTE]
>  .NET Framework 版本2.0 和 .NET Core 版本1.0 導入了可為 null 型別的支援，讓程式設計人員可以擴充實數值型別來代表基礎類型的所有值。 這些 CLR 可為 null 的類型代表 <xref:System.Nullable> 結構的實例。 當實數值型別已裝箱和取消裝箱時，這項功能特別有用，可提供與物件類型的增強相容性。 CLR 可為 null 的型別不適合用來儲存資料庫 null，因為 ANSI SQL null 的行為與 `null` 參考（或 Visual Basic 中的 `Nothing`）的運作方式不同。 對於使用資料庫 ANSI SQL null 值，請使用 <xref:System.Data.SqlTypes> null，而不是 <xref:System.Nullable>。 如需在中C#使用 CLR 可為 null 型別的詳細資訊，請參閱C# [可為 null](https://docs.microsoft.com/dotnet/csharp/programming-guide/nullable-types/)的型別，以及[使用可為 null](https://docs.microsoft.com/dotnet/csharp/programming-guide/nullable-types/using-nullable-types/)型別的。  
  
## <a name="nulls-and-three-valued-logic"></a>Null 和三值邏輯  
在資料行定義中允許 null 值，會在您的應用程式中引進三個值的邏輯。 比較可以評估為三個條件的其中一個：  
  
- True  
  
- False  
  
- Unknown  
  
因為 null 會被視為未知，所以與彼此比較的兩個 null 值不會視為相等。 在使用算術運算子的運算式中，如果有任何運算元是 null，結果也會是 null。  
  
## <a name="nulls-and-sqlboolean"></a>Null 和 SqlBoolean  
任何 <xref:System.Data.SqlTypes> 的比較都會傳回 <xref:System.Data.SqlTypes.SqlBoolean>。 每個 `SqlType` 的 `IsNull` 函數都會傳回一個 <xref:System.Data.SqlTypes.SqlBoolean>，而且可用來檢查是否有 null 值。 下列事實資料表顯示和、或和 NOT 運算子如何在出現 null 值的情況下運作。 （T = true、F = false 和 U = unknown，或 null）。  
  
![事實資料表](../media/truthtable-bpuedev11.gif "|::ref1::|")  
  
### <a name="understanding-the-ansi_nulls-option"></a>瞭解 ANSI_NullS 選項  
<xref:System.Data.SqlTypes> 提供與 SQL Server 中的 ANSI_NullS 選項設為 on 時相同的語義。 如果有任何運算元或引數為 Null (屬性 `IsNull` 除外)，則所有算術運算子 (+、-、*、/、%)、位元運算子 (~、&、&#124;) 及大多數函式都會傳回 Null。  
  
ANSI SQL-92 標準不支援 WHERE 子句中的 *columnName* = NULL。 在 SQL Server 中，ANSI_NullS 選項會控制資料庫中的預設 null 屬性，以及評估 null 值的比較。 如果 ANSI_NullS 已開啟（預設值），則在測試 null 值時，必須在運算式中使用 IS Null 運算子。 例如，當 ANSI_NULLS 是 ON 時，下列比較永遠都會產生未知：  
  
```console
colname > NULL  
```  
  
比較與包含 null 值的變數也會產生未知的：  
  
```console
colname > @MyVariable  
```  
  
使用 IS NULL 或 IS NOT NULL 述詞可以測試是否為 NULL 值。 不過這樣會增加 WHERE 子句的複雜度。 例如，AdventureWorks Customer 資料表中的 TerritoryID 資料行允許 null 值。 如果 SELECT 陳述式要測試其他資料行是否有 Null 值，必須包含 IS NULL 述詞：  
  
```sql
SELECT CustomerID, AccountNumber, TerritoryID  
FROM AdventureWorks.Sales.Customer  
WHERE TerritoryID IN (1, 2, 3)  
   OR TerritoryID IS NULL  
```  
  
如果您在 SQL Server 中將 ANSI_NullS 設為 off，則可以建立使用等號比較運算子來比較 null 的運算式。 不過，您無法防止不同的連接設定該連線的 null 選項。 不論連接的 ANSI_NullS 設定為何，使用 IS Null 來測試 null 值是否一律有效。  
  
`DataSet` 中不支援設定 ANSI_NullS off，其一律遵循 ANSI SQL-92 標準來處理 <xref:System.Data.SqlTypes> 中的 null 值。  
  
## <a name="assigning-null-values"></a>指派 null 值  
Null 值是特殊的，其儲存體和指派的語義在不同的類型系統和儲存系統之間有所不同。 `Dataset` 是設計來搭配不同的類型和儲存系統使用。  
  
本節說明將 null 值指派給不同類型系統之 <xref:System.Data.DataRow> 中 <xref:System.Data.DataColumn> 的 null 語法。  
  
`DBNull.Value`  
此指派對任何類型的 `DataColumn` 都有效。 如果類型會實 `INullable`，`DBNull.Value` 會強制轉型為適當的強型別 Null 值。  
  
`SqlType.Null`  
所有 <xref:System.Data.SqlTypes> 資料類型都會實 `INullable`。 如果強型別 null 值可以使用隱含轉換運算子轉換成資料行的資料型別，則指派應該會經過。 否則會擲回不正確轉換例外狀況。  
  
`null`  
如果 ' null ' 對於給定的 `DataColumn` 資料類型是合法的值，則會強制轉型為適當的 `DbNull.Value` 或與 `INullable` 型別（`SqlType.Null`）相關聯的 `Null`  
  
`derivedUdt.Null`  
如果是 UDT 資料行，則一律會根據與 `DataColumn` 相關聯的類型來儲存 null。 請考慮與 `DataColumn` 相關聯的 UDT 案例，而不會在其子類別執行 `INullable`。 在此情況下，如果已指派與衍生類別相關聯的強型別 null 值，它就會儲存為不具型別的 `DbNull.Value`，因為 null 儲存體一律與 DataColumn 的資料型別一致。  
  
> [!NOTE]
>  `DataSet` 中目前不支援 `Nullable<T>` 或 <xref:System.Nullable> 結構。  
  
### <a name="multiple-column-row-assignment"></a>多個資料行（資料列）指派  
`DataTable.Add`、`DataTable.LoadDataRow` 或其他接受對應到資料列之 <xref:System.Data.DataRow.ItemArray%2A> 的 Api，請將 ' null ' 對應至 DataColumn 的預設值。 如果陣列中的物件包含 `DbNull.Value` 或其強型別對應項，則會套用前述的相同規則。  
  
此外，下列規則適用于 `DataRow.["columnName"]` null 指派的實例：  
  
- 除了強型別 Null 資料行具有適當的強型別 Null 值之外，所有其他項目的預設 *default* 值都為 `DbNull.Value`。  
  
- Null 值在序列化至 XML 檔案（如 "xsi： nil"）時，永遠不會寫出。  
  
- 序列化為 XML 時，一律會寫出所有非 null 值（包括預設值）。 這不同于 XSD/XML 語義，其中 null 值（xsi： nil）是明確的，而預設值是隱含的（如果 XML 中沒有，驗證剖析器可以從相關聯的 XSD 架構取得）。 `DataTable` 的相反情況： null 值是隱含的，而預設值則是明確的。  
  
- 從 XML 輸入讀取之資料列的所有遺漏資料行值都會指派為 Null。 使用 <xref:System.Data.DataTable.NewRow%2A> 或類似方法建立的資料列會被指派 DataColumn 的預設值。  
  
- <xref:System.Data.DataRow.IsNull%2A> 方法會傳回 `DbNull.Value` 和 `INullable.Null` 的 `true`。  
  
## <a name="assigning-null-values"></a>指派 null 值  
任何 <xref:System.Data.SqlTypes> 實例的預設值都是 null。  
  
<xref:System.Data.SqlTypes> 中的 null 是特定類型，而且不能以單一值表示，例如 `DbNull`。 請使用 `IsNull` 屬性來檢查是否為 null。  
  
Null 值可以指派給 <xref:System.Data.DataColumn>，如下列程式碼範例所示。 您可以直接將 null 值指派給 `SqlTypes` 變數，而不會觸發例外狀況。  
  
### <a name="example"></a>範例  
下列程式碼範例會建立一個 <xref:System.Data.DataTable>，其中包含兩個定義為 <xref:System.Data.SqlTypes.SqlInt32> 和 <xref:System.Data.SqlTypes.SqlString> 的資料行。 程式碼會加入一個已知值的資料列、一個 null 值的資料列，然後逐一查看 <xref:System.Data.DataTable>，將值指派給變數，並在主控台視窗中顯示輸出。  
  
[!code-csharp[DataWorks SqlInt32_IsNull#1](~/../sqlclient/doc/samples/SqlInt32_IsNull.cs#1)]
  
這個範例會顯示下列結果：  
  
```console
isColumnNull=False, ID=123, Description=Side Mirror  
isColumnNull=True, ID=Null, Description=Null  
```  
  
## <a name="comparing-null-values-with-sqltypes-and-clr-types"></a>比較 null 值與 SqlTypes 和 CLR 類型  
比較 null 值時，請務必瞭解 `Equals` 方法在 <xref:System.Data.SqlTypes> 中評估 null 值的方式之間的差異，相較于與 CLR 型別搭配運作的方式。 所有 <xref:System.Data.SqlTypes> `Equals` 方法都會使用資料庫語義來評估 null 值：如果其中一個或兩個值都是 null，則比較會產生 null。 另一方面，在兩個 <xref:System.Data.SqlTypes> 上使用 CLR `Equals` 方法會在兩者都是 null 時產生 true。 這反映使用實例方法（例如 CLR `String.Equals` 方法）和使用靜態/共用方法（`SqlString.Equals`）之間的差異。  
  
下列範例示範在每個傳遞一對 null 值和一對空字串時，`SqlString.Equals` 方法與 `String.Equals` 方法之間的結果差異。  
  
[!code-csharp[DataWorks SqlString_Equals#1](~/../sqlclient/doc/samples/SqlString_Equals.cs#1)]
  
此程式碼會產生下列輸出：  
  
```console
SqlString.Equals shared/static method:  
  Two nulls=Null  
  
String.Equals instance method:  
  Two nulls=True  
  
SqlString.Equals shared/static method:  
  Two empty strings=True  
  
String.Equals instance method:  
  Two empty strings=True   
```  
  
## <a name="next-steps"></a>後續步驟
- [SQL Server 資料類型和 ADO.NET](sql-server-data-types.md)
