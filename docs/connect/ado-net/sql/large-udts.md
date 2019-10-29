---
title: 大型 UDT
description: 示範如何從 SQL Server 2008 引進的大數值 Udt 中取出資料。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 420ae24e-762b-4e09-b4c3-2112c470ee49
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 4ea2c0002ceb01606cdf51f04246abcdc74429e0
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452150"
---
# <a name="large-udts"></a>大型 UDT

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[下載 ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

使用者定義類型 (UDT) 可讓開發人員將 Common Language Runtime (CLR) 物件儲存在 SQL Server 資料庫中來擴充伺服器的純量類型系統。 UDT 可包含多個項目並可具有不同的行為，與只含單一 SQL Server 系統資料類型的傳統別名資料類型有所不同。  
  
在過去，UDT 的大小上限為 8 KB。 在 SQL Server 2008 中，目前使用 <xref:Microsoft.Data.SqlClient.Server.Format.UserDefined> 格式的 UDT 已不再具有這項限制。  
  
如需使用者定義類型的完整檔，請參閱 SQL Server 線上叢書的[CLR 使用者定義型](https://go.microsoft.com/fwlink/?LinkId=98366)別。
  
## <a name="retrieving-udt-schemas-using-getschema"></a>使用 GetSchema 來抓取 UDT 架構  
<xref:Microsoft.Data.SqlClient.SqlConnection> 的 <xref:Microsoft.Data.SqlClient.SqlConnection.GetSchema%2A> 方法會傳回 <xref:System.Data.DataTable> 中的資料庫架構資訊。
  
### <a name="getschematable-column-values-for-udts"></a>Udt 的 GetSchemaTable 資料行值  
<xref:Microsoft.Data.SqlClient.SqlDataReader> 的 <xref:Microsoft.Data.SqlClient.SqlDataReader.GetSchemaTable%2A> 方法會傳回描述資料行中繼資料的 <xref:System.Data.DataTable>。 下表描述 SQL Server 2005 和 SQL Server 2008 之間的大型 Udt 之資料行中繼資料的差異。  
  
|SqlDataReader 資料行|SQL Server 2005|SQL Server 2008 及更新版本|  
|--------------------------|---------------------|-------------------------------|  
|`ColumnSize`|不定|不定|  
|`NumericPrecision`|255|255|  
|`NumericScale`|255|255|  
|`DataType`|`Byte[]`|UDT 實例|  
|`ProviderSpecificDataType`|`SqlTypes.SqlBinary`|UDT 實例|  
|`ProviderType`|21 (`SqlDbType.VarBinary`)|29 (`SqlDbType.Udt`)|  
|`NonVersionedProviderType`|29 (`SqlDbType.Udt`)|29 (`SqlDbType.Udt`)|  
|`DataTypeName`|`SqlDbType.VarBinary`|指定為 *Database.SchemaName.TypeName* 的三部分名稱。|  
|`IsLong`|不定|不定|  
  
## <a name="sqldatareader-considerations"></a>SqlDataReader 考慮  
從 SQL Server 2008 開始，<xref:Microsoft.Data.SqlClient.SqlDataReader> 已擴充，可支援大型 UDT 值的擷取。 <xref:Microsoft.Data.SqlClient.SqlDataReader> 處理大型 UDT 值的方式，取決於您所使用的 SQL Server 版本，以及連接字串中指定的 `Type System Version`。 如需詳細資訊，請參閱 <xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString%2A>為止。  
  
當 `Type System Version` 設定為 SQL Server 2005 時，下列 <xref:Microsoft.Data.SqlClient.SqlDataReader> 方法將會傳回 <xref:System.Data.SqlTypes.SqlBinary> 而不是 UDT：  
  
- <xref:Microsoft.Data.SqlClient.SqlDataReader.GetProviderSpecificFieldType%2A>  
  
- <xref:Microsoft.Data.SqlClient.SqlDataReader.GetProviderSpecificValue%2A>  
  
- <xref:Microsoft.Data.SqlClient.SqlDataReader.GetProviderSpecificValues%2A>  
  
- <xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlValue%2A>  
  
- <xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlValues%2A>  
  
當 `Type System Version` 設定為 SQL Server 2005 時，下列方法會傳回 `Byte[]` 的陣列，而不是 UDT：  
  
- <xref:Microsoft.Data.SqlClient.SqlDataReader.GetValue%2A>  
  
- <xref:Microsoft.Data.SqlClient.SqlDataReader.GetValues%2A>  
  
請注意，目前的 ADO.NET 版本不會進行任何轉換。  
  
## <a name="specifying-sqlparameters"></a>指定 SqlParameters  
下列 <xref:Microsoft.Data.SqlClient.SqlParameter> 屬性已擴充為可使用大型 Udt。  
  
|SqlParameter 屬性|Description|  
|---------------------------|-----------------|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.Value%2A>|取得或設定代表參數值的物件。 預設值是 null。 屬性可以是 `SqlBinary`、`Byte[]` 或受控物件。|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.SqlValue%2A>|取得或設定代表參數值的物件。 預設值是 null。 屬性可以是 `SqlBinary`、`Byte[]` 或受控物件。|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.Size%2A>|取得或設定要解析的參數值大小。 預設值是 0。 屬性可以是代表參數值大小的整數。 對於大型 UDT 而言，這可能是 UDT 的實際大小，-1 則代表未知。|  
  
## <a name="retrieving-data-example"></a>正在抓取資料範例  
下列程式碼片段示範如何取出大型 UDT 資料。 `connectionString` 變數會假設 SQL Server 資料庫的有效連接，而 `commandString` 變數會假設具有主鍵資料行的有效 SELECT 語句會先列出。  
  
```csharp  
using (SqlConnection connection = new SqlConnection(   
    connectionString, commandString))  
{  
  connection.Open();  
  SqlCommand command = new SqlCommand(commandString);  
  SqlDataReader reader = command.ExecuteReader();  
  while (reader.Read())  
  {  
    // Retrieve the value of the Primary Key column.  
    int id = reader.GetInt32(0);  
  
    // Retrieve the value of the UDT.  
    LargeUDT udt = (LargeUDT)reader[1];  
  
    // You can also use GetSqlValue and GetValue.  
    // LargeUDT udt = (LargeUDT)reader.GetSqlValue(1);  
    // LargeUDT udt = (LargeUDT)reader.GetValue(1);  
  
    Console.WriteLine(  
     "ID={0} LargeUDT={1}", id, udt);  
  }  
reader.close  
}  
```  
  
## <a name="next-steps"></a>後續步驟
- [SQL Server 二進位和大型數值資料](sql-server-binary-large-value-data.md)
