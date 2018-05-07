---
title: 使用 ADO 與 OLE DB 驅動程式，適用於 SQL Server |Microsoft 文件
description: 使用 ADO 與 OLE DB 驅動程式，適用於 SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|applications
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, ADO
- data access [OLE DB Driver for SQL Server], ADO
- ADO [OLE DB Driver for SQL Server]
- MSOLEDBSQL, ADO
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: c1244669bcfeea5008640ed00b6f8e579ce71139
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="using-ado-with-ole-db-driver-for-sql-server"></a>使用 ADO 與 OLE DB 驅動程式，適用於 SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  若要利用中引進的新功能[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]例如 multiple active result set (MARS)、 查詢通知、 使用者定義型別 (Udt) 或新**xml**資料類型，使用 activex 控制項的現有應用程式Data Objects (ADO) 應該使用 SQL Server 的 OLE DB 驅動程式，做為其資料存取提供者。  
  
 為了讓 ADO 使用最新版本的新功能[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，一些增強功能已對 OLE DB 驅動程式的 SQL Server，其延伸了 OLE DB 的核心功能。 這些增強功能可讓 ADO 應用程式使用較新[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]功能，並使用兩個資料型別中導入[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]: **xml**和**udt**。 這些增強功能也會利用增強功能**varchar**， **nvarchar**，和**varbinary**資料型別。 OLE DB 驅動程式的 SQL Server 會將 SSPROP_INIT_DATATYPECOMPATIBILITY 初始化屬性加入至 DBPROPSET_SQLSERVERDBINIT 屬性集，以便使用由 ADO 應用程式與 ADO 相容的方式來公開新的資料類型。 此外，SQL Server OLE DB 驅動程式也會定義新的連接字串關鍵字，名為**DataTypeCompatibility**設定連接字串中。  

> [!NOTE]  
>  現有的 ADO 應用程式可以使用 SQLOLEDB 提供者來存取並更新 XML、UDT 和大數值文字與二進位欄位值。 新的較大**varchar （max)**， **nvarchar （max)**，和**varbinary （max)** 資料類型會傳回成 ADO 類型**adLongVarChar**，**adLongVarWChar**和**adLongVarBinary**分別。 會傳回 XML 資料行，做為**adLongVarChar**，並會傳回 UDT 資料行，做為**adVarBinary**。 不過，如果您使用 OLE DB 驅動程式的 SQL Server (MSOLEDBSQL) 來取代 SQLOLEDB，您需要確定設定**DataTypeCompatibility**關鍵字為"80"，讓新的資料類型會正確對應至 ADO 資料類型。  

## <a name="enabling-ole-db-driver-for-sql-server-from-ado"></a>啟用從 ADO 的 SQL Server 的 OLE DB 驅動程式  
 若要啟用 SQL Server 的 OLE DB 驅動程式的使用方式，ADO 應用程式必須在其連接字串中實作下列關鍵字：  

-   `Provider=MSOLEDBSQL`  

-   `DataTypeCompatibility=80`  

 如需有關之 ADO 連接字串關鍵字中 OLE DB 驅動程式支援的 SQL Server，請參閱[搭配 OLE DB 驅動程式的 SQL Server 中使用連接字串關鍵字](../../oledb/applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)。  

 建立完全啟用成可搭配 OLE DB 驅動程式用於 SQL Server，包括啟用 MARS 功能的 ADO 連接字串的範例如下：  

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
 下列章節提供如何使用 ADO 與 OLE DB 驅動程式的 SQL Server 的範例。  

### <a name="retrieving-xml-column-data"></a>擷取 XML 資料行資料  
 在此範例中，資料錄集用來擷取及顯示從 XML 資料行中資料[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **AdventureWorks**範例資料庫。  

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
 在此範例中，**命令**物件用來執行 SQL 查詢可傳回 UDT、 UDT 資料會更新，而且新的資料再插回資料庫。 這個範例假設**點**已經在資料庫中註冊 UDT。  

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
 在此範例中，以啟用 for SQL Server 的 OLE DB 驅動程式透過 MARS 建構連接字串，然後建立兩個資料錄集物件，以便執行使用相同的連接。  

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

 在舊版 OLE DB 提供者中，此程式碼會導致系統在第二次執行時建立隱含連接，因為每個單一連接只能開啟一個作用中結果集。 由於隱含連接不會在 OLE DB 連接集區中共用，所以這會產生額外的負擔。 使用 SQL server OLE DB 驅動程式所公開的 MARS 功能，您可以取得 multiple active result 在單一連接上。  

## <a name="see-also"></a>另請參閱  
 [利用 OLE DB Driver for SQL Server 建置](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
