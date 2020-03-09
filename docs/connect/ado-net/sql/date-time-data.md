---
title: 日期和時間資料
description: 描述如何使用 SQL Server 2008 中引進的新日期和時間資料類型。
ms.date: 09/30/2019
dev_langs:
- csharp
ms.assetid: 6f5ff56a-a57e-49d7-8ae9-bbed697e42e3
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 75d8b98726a758e0533053dbdf8d2e03b3bfdf0d
ms.sourcegitcommit: 610e49c3e1fa97056611a85e31e06ab30fd866b1
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/07/2020
ms.locfileid: "78896995"
---
# <a name="date-and-time-data"></a>日期和時間資料

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

SQL Server 2008 引進了新的資料類型來處理日期和時間資訊。 新的資料類型包含適用於日期和時間的個別類型，以及具有更大範圍、精確度和時區感知的已擴充資料類型。 Microsoft SqlClient Data Provider for SQL Server (<xref:Microsoft.Data.SqlClient>) 會針對 SQL Server 2008 資料庫引擎的所有新功能提供完整支援。 您必須安裝 .NET Framework 3.5 SP1 (或更新版本) 或是 .NET Core 1.0 (或更新版本)，才能搭配 SqlClient 使用這些新功能。  
  
早於 SQL Server 2008 的 SQL Server 版本，只有兩種資料類型可用來處理日期和時間值：`datetime` 和 `smalldatetime`。 這兩種資料類型都同時包含日期值和時間值，所以很難只使用日期或是時間值。 此外，這些資料類型僅支援 1753 年在英國引進西曆之後的日期。 另一個限制是這些較舊的資料類型不是時區感知的，因此很難處理源自多個時區的資料。  
  
《SQL Server 線上叢書》提供 SQL Server 資料類型的完整文件。 如需有關日期和時間資料的入門級主題，請參閱[使用日期和時間資料](https://go.microsoft.com/fwlink/?LinkID=98361)。
  
## <a name="datetime-data-types-introduced-in-sql-server-2008"></a>SQL Server 2008 所引進的日期/時間資料類型  
 下表描述新的日期和時間資料類型。  
  
|SQL Server 資料類型|描述|  
|--------------------------|-----------------|  
|`date`|`date` 資料類型的範圍從 01 年 1 月 1 日到 9999 年 12 月 31 日，精確度為 1 日。 預設值為 1900 年 1 月 1 日。 儲存體大小是 3 位元組。|  
|`time`|`time` 資料類型只會根據 24 小時制來儲存時間值。 `time` 資料類型的範圍從 00:00:00.0000000 到 23:59:59.9999999，精確度為 100 奈秒。 預設值是 00:00:00.0000000 (午夜)。 `time` 資料類型支援使用者定義的小數點後第二位的精確度，儲存大小則從 3 到 6 位元組不等，依指定的精確度而定。|  
|`datetime2`|`datetime2` 資料類型會將 `date` 和 `time` 資料類型的範圍和精確度結合成單一資料類型。<br /><br /> 預設值和字串常值格式會與 `date` 和 `time` 資料類型中所定義的相同。|  
|`datetimeoffset`|`datetimeoffset` 資料類型具有 `datetime2` 的所有功能，且具有額外的時區位移。 時區位移會以 [+&#124;-] HH:MM 表示。 HH 表示時區位移中的 2 位數時數，範圍介於 00 至 14 之間。 MM 是代表時區位移中額外分鐘數的 2 位數，範圍介於 00 至 59 之間。 時間格式可支援到 100 奈秒。 強制性的 + 或 - 符號指出是否要從 UTC (世界標準時間或格林威治標準時間) 增加或扣除時區位移，以取得當地時間。|  
  
> [!NOTE]
>  如需使用 `Type System Version` 關鍵字的詳細資訊，請參閱 <xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString%2A>。  
  
## <a name="date-format-and-date-order"></a>日期格式和日期順序  
SQL Server 剖析日期和時間值的方式，不僅取決於類型系統版本和伺服器版本，也會根據伺服器的預設語言和格式設定而定。 如果查詢會透過使用不同語言和日期格式設定的連線來執行，則可能無法辨識適用於某種語言之日期格式的日期字串。  
  
Transact-SQL SET LANGUAGE 陳述式會隱含地設定 DATEFORMAT，以決定日期部分的順序。 您可以利用 MDY、DMY、YMD、YDM、MYD 或 DYM 順序來排序日期部分，以在連線上使用 SET DATEFORMAT Transact-SQL 陳述式來釐清日期值。  
  
如果您未針對連線指定任何 DATEFORMAT，SQL Server 就會使用與連線相關聯的預設語言。 例如，在語言設定為「美式英文」的伺服器上，會將 '01/02/03' 的日期字串解讀為 MDY (2003 年 1 月 2 日)，而在語言設定為「英式英文」的伺服器上則會解譯為 DMY (2003 年 2 月 1 日)。 年份會使用 SQL Server 的截止年份規則來決定，這會定義用來指派世紀值的截止日期。 如需詳細資訊，請參閱《SQL Server 線上叢書》中的 [two digit year cutoff 選項](https://go.microsoft.com/fwlink/?LinkId=120473)。  
  
> [!NOTE]
>  從字串格式轉換為 `date`、`time`、`datetime2` 或 `datetimeoffset` 時，不支援 YDM 日期格式。  
  
如需 SQL Server 如何解譯日期和時間資料的詳細資訊，請參閱《SQL Server 2008 線上叢書》中的[使用日期和時間資料](https://go.microsoft.com/fwlink/?LinkID=98361)。  
  
## <a name="datetime-data-types-and-parameters"></a>日期/時間資料類型和參數  
<xref:System.Data.SqlDbType> 中新增了以下列舉來支援新的日期和時間資料類型。  
  
- `SqlDbType.Date`  
  
- `SqlDbType.Time`  
  
- `SqlDbType.DateTime2`  
  
- `SqlDbType.DateTimeOffSet`  

您可以使用上述其中一個 <xref:System.Data.SqlDbType> 列舉來指定 <xref:Microsoft.Data.SqlClient.SqlParameter> 的資料類型。 

> [!NOTE]
> 您無法將 `SqlParameter` 的 `DbType` 屬性設定為 `SqlDbType.Date`。

您也可以藉由將 `SqlParameter` 物件的 <xref:Microsoft.Data.SqlClient.SqlParameter.DbType%2A> 屬性設定為特定的 <xref:System.Data.DbType> 列舉值，以一般的方法指定 <xref:Microsoft.Data.SqlClient.SqlParameter> 的類型。 <xref:System.Data.DbType> 中新增了以下列舉值，以支援 `datetime2` 和 `datetimeoffset` 資料類型：  
  
- DbType.DateTime2  
  
- DbType.DateTimeOffset  
  
這些新的列舉會補充 `Date`、`Time` 和 `DateTime` 列舉。  
  
參數物件的 Microsoft SqlClient Data Provider 類型會從參數物件值的 .NET 類型或從參數物件的 `DbType` 推斷而來。 尚未引進任何新的 <xref:System.Data.SqlTypes> 資料類型來支援新的日期和時間資料類型。 下表描述 SQL Server 2008 日期和時間資料類型與 CLR 資料類型之間的對應。  
  
|SQL Server 資料類型|.NET 類型|System.Data.SqlDbType|System.Data.DbType|  
|--------------------------|-------------------------|---------------------------|------------------------|  
|date|System.DateTime|Date|Date|  
|time|System.TimeSpan|Time|Time|  
|datetime2|System.DateTime|DateTime2|DateTime2|  
|datetimeoffset|System.DateTimeOffset|DateTimeOffset|DateTimeOffset|  
|Datetime|System.DateTime|Datetime|Datetime|  
|smalldatetime|System.DateTime|Datetime|Datetime|  
  
### <a name="sqlparameter-properties"></a>SqlParameter 屬性  
 下表描述與日期和時間資料類型相關的 `SqlParameter` 屬性。  
  
|屬性|描述|  
|--------------|-----------------|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.IsNullable%2A>|取得或設定值是否可為 Null。 當您將 Null 參數值傳送到伺服器時，必須指定 <xref:System.DBNull>，而不是 `null` (在 Visual Basic 中為 `Nothing`)。 如需資料庫 Null 的詳細資訊，請參閱[處理 Null 值](handle-null-values.md)。|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.Precision%2A>|取得或設定用來表示值的最大位數。 系統會針對日期和時間資料類型忽略此設定。|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.Scale%2A>|取得或設定針對 `Time`、`DateTime2` 和 `DateTimeOffset` 解析之值時間部分的小數點位數。 預設值為 0，表示會從值推斷實際的小數值，並傳送到伺服器。|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.Size%2A>|已針對日期和時間資料類型加以忽略。|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.Value%2A>|取得或設定參數值。|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.SqlValue%2A>|取得或設定參數值。|  
  
> [!NOTE]
>  小於零或者大於或等於 24 小時的時間值將會擲回 <xref:System.ArgumentException>。  
  
### <a name="creating-parameters"></a>建立參數  
您可以使用其建構函式來建立 <xref:Microsoft.Data.SqlClient.SqlParameter> 物件，或將它新增到 <xref:Microsoft.Data.SqlClient.SqlCommand>.<xref:Microsoft.Data.SqlClient.SqlCommand.Parameters%2A> 集合 (透過呼叫 <xref:Microsoft.Data.SqlClient.SqlParameterCollection> 的 `Add` 方法來完成)。 `Add` 方法將會取得建構函式引數或現有參數物件作為輸入。  
  
此主題的後續小節將提供如何指定日期和時間參數的範例。
  
### <a name="date-example"></a>Date 範例  
下列程式碼片段將示範如何指定 `date` 參數。  
  
```csharp  
SqlParameter parameter = new SqlParameter();  
parameter.ParameterName = "@Date";  
parameter.SqlDbType = SqlDbType.Date;  
parameter.Value = "2007/12/1";  
```  
  
### <a name="time-example"></a>Time 範例  
下列程式碼片段將示範如何指定 `time` 參數。  
  
```csharp  
SqlParameter parameter = new SqlParameter();  
parameter.ParameterName = "@time";  
parameter.SqlDbType = SqlDbType.Time;  
parameter.Value = DateTime.Parse("23:59:59").TimeOfDay;  
```  
  
### <a name="datetime2-example"></a>Datetime2 範例  
下列程式碼片段將示範如何指定同時具備日期和時間部分的 `datetime2` 參數。  
  
```csharp  
SqlParameter parameter = new SqlParameter();  
parameter.ParameterName = "@Datetime2";  
parameter.SqlDbType = SqlDbType.DateTime2;  
parameter.Value = DateTime.Parse("1666-09-02 1:00:00");  
```  
  
### <a name="datetimeoffset-example"></a>DateTimeOffSet 範例  
下列程式碼片段將示範如何指定具備日期、時間且時區位移為 0 的 `DateTimeOffSet` 參數。  
  
```csharp  
SqlParameter parameter = new SqlParameter();  
parameter.ParameterName = "@DateTimeOffSet";  
parameter.SqlDbType = SqlDbType.DateTimeOffSet;  
parameter.Value = DateTimeOffset.Parse("1666-09-02 1:00:00+0");  
```  
  
### <a name="addwithvalue"></a>AddWithValue  
您也可以使用 <xref:Microsoft.Data.SqlClient.SqlCommand> 的 `AddWithValue` 方法來提供參數，如下列程式碼片段所示。 不過，`AddWithValue` 方法不允許您針對參數指定 <xref:Microsoft.Data.SqlClient.SqlParameter.DbType%2A> 或 <xref:Microsoft.Data.SqlClient.SqlParameter.SqlDbType%2A>。  
  
```csharp  
command.Parameters.AddWithValue(   
    "@date", DateTimeOffset.Parse("16660902"));  
```  
  
`@date` 參數可對應至伺服器上的 `date`、`datetime` 或 `datetime2` 資料類型。 使用新的 `datetime` 資料類型時，您必須將參數的 <xref:System.Data.SqlDbType> 屬性明確設定為執行個體的資料類型。 使用 <xref:System.Data.SqlDbType.Variant> 或隱含提供參數值可能會導致與 `datetime` 和 `smalldatetime` 資料類型的回溯相容性問題。  
  
下表顯示可從哪些 CLR 類型推斷出哪些 `SqlDbTypes`：  
  
|CLR 類型|推斷的 SqlDbType|  
|--------------|------------------------|  
|Datetime|SqlDbType.DateTime|  
|TimeSpan|SqlDbType.Time|  
|DateTimeOffset|SqlDbType.DateTimeOffset|  
  
## <a name="retrieving-date-and-time-data"></a>擷取日期和時間資料  
下表說明用來擷取 SQL Server 2008 日期和時間值的方法。  
  
|SqlClient 方法|描述|  
|----------------------|-----------------|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetDateTime%2A>|擷取指定的資料行值作為 <xref:System.DateTime> 結構。|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetDateTimeOffset%2A>|擷取指定的資料行值作為 <xref:System.DateTimeOffset> 結構。|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetProviderSpecificFieldType%2A>|傳回類型，其為欄位的底層提供者特定類型。 針對新的日期和時間類型，傳回與 `GetFieldType` 相同的類型。|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetProviderSpecificValue%2A>|擷取指定資料行的值。 針對新的日期和時間類型，傳回與 `GetValue` 相同的類型。|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetProviderSpecificValues%2A>|擷取指定陣列中的值。|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlString%2A>|以 <xref:System.Data.SqlTypes.SqlString> 形式擷取資料行值。 如果無法將資料表示為 `SqlString`，就會發生 <xref:System.InvalidCastException>。|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlValue%2A>|擷取資料行資料作為其預設 `SqlDbType`。 針對新的日期和時間類型，傳回與 `GetValue` 相同的類型。|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlValues%2A>|擷取指定陣列中的值。|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetString%2A>|如果 Type System Version 是設為 SQL Server 2005，則擷取資料行的值作為字串。 如果無法將資料表示為字串，就會發生 <xref:System.InvalidCastException>。|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetTimeSpan%2A>|擷取指定的資料行值作為 <xref:System.TimeSpan> 結構。|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetValue%2A>|擷取指定的資料行值作為其底層 CLR 類型。|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetValues%2A>|擷取陣列中的資料行值。|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSchemaTable%2A>|傳回 <xref:System.Data.DataTable>，其會描述結果集的中繼資料。|  
  
> [!NOTE]
>  目前正在 SQL Server 處理序中執行的程式碼不支援新的日期和時間 `SqlDbTypes`。 如果將這其中一個類型傳遞至伺服器，就會引發例外狀況。  
  
## <a name="specifying-date-and-time-values-as-literals"></a>將日期和時間值指定為常值  
您可以使用各種不同的常值字串格式來指定日期和時間資料類型，然後 SQL Server 會在執行階段進行評估，以將它們轉換成內部日期/時間結構。 SQL Server 可以辨識括在單引號 (') 中的日期和時間資料。 下列範例示範一些格式：  
  
- 字母日期格式，例如 `'October 15, 2006'`。  
  
- 數值日期格式，例如 `'10/15/2006'`。  
  
- 未分隔的字串格式，例如 `'20061015'`，如果您使用 ISO 標準日期格式，則會將其解譯為 2006 年 10 月 15 日。  
  
> [!NOTE]
>  您可以在《SQL Server 線上叢書》中找到所有常值字串格式及日期和時間資料類型之其他功能的完整文件。  
  
小於零或者大於或等於 24 小時的時間值將會擲回 <xref:System.ArgumentException>。  
  
## <a name="resources-in-sql-server-2008-books-online"></a>《SQL Server 2008 線上叢書》中的資源  
如需在 SQL Server 2008 中使用日期和時間值的詳細資訊，請參閱《SQL Server 2008 線上叢書》中的下列資源。  
  
|主題|描述|  
|-----------|-----------------|  
|[日期與時間資料類型及函式 (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=98360)|提供所有 Transact-SQL 日期和間資料類型與函式的概觀。|  
|[使用日期和時間資料](https://go.microsoft.com/fwlink/?LinkId=98361)|提供日期和時間資料類型與函式的詳細資訊，以及使用範例。|  
|[資料類型 (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=98362)|描述 SQL Server 2008 中的系統資料類型。|  
  
## <a name="next-steps"></a>後續步驟
- [SQL Server 資料類型和 ADO.NET](sql-server-data-types.md)
