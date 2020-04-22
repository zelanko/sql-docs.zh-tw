---
title: 利用 OLE DB Driver 使用 ADO
description: 了解如何搭配 OLE DB Driver 使用 ADO，包括 Multiple Active Result Set、查詢通知、使用者定義型別或 xml 資料型別等新功能。
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, ADO
- data access [OLE DB Driver for SQL Server], ADO
- ADO [OLE DB Driver for SQL Server]
- MSOLEDBSQL, ADO
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 72d82433e04ead61ec71eecd3c8771cbe744b751
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81633888"
---
# <a name="using-ado-with-ole-db-driver-for-sql-server"></a>利用 OLE DB Driver for SQL Server 使用 ADO
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  若要運用 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 所導入的新功能 (例如 Multiple Active Result Set (MARS)、查詢通知、使用者定義型別 (UDT) 或新的 **xml** 資料類型)，使用 ActiveX Data Objects (ADO) 的現有應用程式應該使用 OLE DB Driver for SQL Server 當做其資料存取提供者。  
  
 為了讓 ADO 使用最新 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 版本的新功能，我們已經對 OLE DB Driver for SQL Server 新增了一些增強功能，以便擴充 OLE DB 的核心功能。 這些增強功能可讓 ADO 應用程式使用較新的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 功能，以及取用 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 所導入的兩種資料類型：**xml** 和 **udt**。 這些增強功能也會利用 **varchar**、**nvarchar** 和 **varbinary** 資料類型的增強功能。 OLE DB Driver for SQL Server 會將 SSPROP_INIT_DATATYPECOMPATIBILITY 初始化屬性新增至 ADO 應用程式所使用的 DBPROPSET_SQLSERVERDBINIT 屬性集，以便使用與 ADO 相容的方式來公開這些新的資料類型。 此外，OLE DB Driver for SQL Server 也會定義名為 **DataTypeCompatibility** 而且是在連接字串中設定的新連接字串關鍵字。  

> [!NOTE]  
>  現有的 ADO 應用程式可以使用 SQLOLEDB 提供者來存取並更新 XML、UDT 和大數值文字與二進位欄位值。 新的較大 **varchar(max)** 、**nvarchar(max)** 和 **varbinary(max)** 資料類型會分別傳回成 ADO 類型 **adLongVarChar**、**adLongVarWChar** 和 **adLongVarBinary**。 XML 資料行會傳回成 **adLongVarChar**，而且 UDT 資料行會傳回成 **adVarBinary**。 不過，如果您使用 OLE DB Driver for SQL Server (MSOLEDBSQL) 而非 SQLOLEDB，請務必將 **DataTypeCompatibility** 關鍵字設定為 "80"，以便新的資料類型會正確對應至 ADO 資料類型。  

## <a name="enabling-ole-db-driver-for-sql-server-from-ado"></a>從 ADO 啟用 OLE DB Driver for SQL Server  
 若要能夠使用 OLE DB Driver for SQL Server，ADO 應用程式必須在其連接字串中實作下列關鍵字：  

-   `Provider=MSOLEDBSQL`  

-   `DataTypeCompatibility=80`  

 如需 OLE DB Driver for SQL Server 中支援之 ADO 連接字串關鍵字的詳細資訊，請參閱[利用 OLE DB Driver for SQL Server 使用連接字串關鍵字](using-connection-string-keywords-with-oledb-driver-for-sql-server.md)。  

 下列範例會建立完全啟用成可使用 OLE DB Driver for SQL Server 的 ADO 連接字串，包括啟用 MARS 功能：  

```  
Dim con As New ADODB.Connection  

con.ConnectionString = "Provider=MSOLEDBSQL;" _  
         & "Server=(local);" _  
         & "Database=AdventureWorks;" _   
         & "Integrated Security=SSPI;" _  
         & "DataTypeCompatibility=80;" _  
         & "MARS Connection=True;"  
con.Open  
```  

## <a name="examples"></a>範例  
 下列各節會提供如何使用 ADO 搭配 OLE DB Driver for SQL Server 的範例。  

### <a name="retrieving-xml-column-data"></a>擷取 XML 資料行資料  
 在這個範例中，使用了資料錄集來擷取並顯示 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **AdventureWorks** 範例資料庫中 XML 資料行的資料。  

```  
Dim con As New ADODB.Connection  
Dim rst As New ADODB.Recordset  
Dim sXMLResult As String  

con.ConnectionString = "Provider=MSOLEDBSQL;" _  
         & "Server=(local);" _  
         & "Database=AdventureWorks;" _   
         & "Integrated Security=SSPI;" _   
         & "DataTypeCompatibility=80;"  

con.Open  

' Get the xml data as a recordset.  
Set rst.ActiveConnection = con  
rst.Source = "SELECT AdditionalContactInfo FROM Person.Contact " _  
   & "WHERE AdditionalContactInfo IS NOT NULL"  
rst.Open  

' Display the data in the recordset.  
While (Not rst.EOF)  
   sXMLResult = rst.Fields("AdditionalContactInfo").Value  
   Debug.Print (sXMLResult)  
   rst.MoveNext  
End While  

con.Close  
Set con = Nothing  
```  

> [!NOTE]  
>  XML 資料行不支援資料錄集篩選。 如果已使用，就會傳回錯誤。  

### <a name="retrieving-udt-column-data"></a>擷取 UDT 資料行資料  
 在這個範例中，使用了 **Command** 物件來執行可傳回 UDT 的 SQL 查詢、更新 UDT 資料，然後將新的資料插回資料庫中。 這個範例會假設已經在資料庫中註冊了 **Point** UDT。  

```  
Dim con As New ADODB.Connection  
Dim cmd As New ADODB.Command  
Dim rst As New ADODB.Recordset  
Dim strOldUDT As String  
Dim strNewUDT As String  
Dim aryTempUDT() As String  
Dim strTempID As String  
Dim i As Integer  

con.ConnectionString = "Provider=MSOLEDBSQL;" _  
         & "Server=(local);" _  
         & "Database=AdventureWorks;" _   
         & "Integrated Security=SSPI;" _  
         & "DataTypeCompatibility=80;"  

con.Open  

' Get the UDT value.  
Set cmd.ActiveConnection = con  
cmd.CommandText = "SELECT ID, Pnt FROM dbo.Points.ToString()"  
Set rst = cmd.Execute  
strTempID = rst.Fields(0).Value  
strOldUDT = rst.Fields(1).Value  

' Do something with the UDT by adding i to each point.  
arytempUDT = Split(strOldUDT, ",")  
i = 3  
strNewUDT = LTrim(Str(Int(aryTempUDT(0)) + i)) + "," + _  
   LTrim(Str(Int(aryTempUDT(1)) + i))  

' Insert the new value back into the database.  
cmd.CommandText = "UPDATE dbo.Points SET Pnt = '" + strNewUDT + _  
   "' WHERE ID = '" + strTempID + "'"  
cmd.Execute  

con.Close  
Set con = Nothing  
```  

### <a name="enabling-and-using-mars"></a>啟用並使用 MARS  
 在這個範例中，建構了透過 OLE DB Driver for SQL Server 啟用 MARS 的連接字串，然後建立兩個資料錄集物件，以便使用相同的連接執行。  

```  
Dim con As New ADODB.Connection  

con.ConnectionString = "Provider=MSOLEDBSQL;" _  
         & "Server=(local);" _  
         & "Database=AdventureWorks;" _   
         & "Integrated Security=SSPI;" _  
         & "DataTypeCompatibility=80;" _  
         & "MARS Connection=True;"  
con.Open  

Dim recordset1 As New ADODB.Recordset  
Dim recordset2 As New ADODB.Recordset  

Dim recordsaffected As Integer  
Set recordset1 =  con.Execute("SELECT * FROM Table1", recordsaffected, adCmdText)  
Set recordset2 =  con.Execute("SELECT * FROM Table2", recordsaffected, adCmdText)  

con.Close  
Set con = Nothing  
```  

 在舊版 OLE DB 提供者中，此程式碼會導致系統在第二次執行時建立隱含連接，因為每個單一連接只能開啟一個作用中結果集。 由於隱含連接不會在 OLE DB 連接集區中共用，所以這會產生額外的負擔。 使用 OLE DB Driver for SQL Server 所公開的 MARS 功能時，您會在單一連接上收到多個作用中結果。  

## <a name="see-also"></a>另請參閱  
 [利用 OLE DB Driver for SQL Server 建置](building-applications-with-oledb-driver-for-sql-server.md)  
