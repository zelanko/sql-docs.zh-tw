---
title: 使用 ADO
description: 若要使用 SQL Server 2005 引進的新功能，使用 ADO 的現有應用程式應該使用 SQL Server Native Client OLE DB 提供者。
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client, ADO
- data access [SQL Server Native Client], ADO
- ADO [SQL Server Native Client]
- SQLNCLI, ADO
ms.assetid: 118a7cac-4c0d-44fd-b63e-3d542932d239
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7c765f45b986640fd6b6a1bf1cf491e783e38ae2
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: zh-TW
ms.lasthandoff: 07/06/2020
ms.locfileid: "85998877"
---
# <a name="using-ado-with-sql-server-native-client"></a>使用 ADO 搭配 SQL Server Native Client
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  為了利用中引進的新功能 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] ，例如 multiple active result sets （MARS）、查詢通知、使用者定義型別（udt）或新的**xml**資料型別，使用 ActiveX Data Objects （ADO）的現有應用程式應該使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者做為其資料存取提供者。  
  
 如果您不需要使用 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 所導入的任何新功能，就不需要使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者。您可以繼續使用目前的資料存取提供者 (通常是 SQLOLEDB)。 如果您要強化現有的應用程式，而且需要使用 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 所導入的新功能，就應該使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者。  
  
> [!NOTE]  
>  如果您正在開發新的應用程式，建議您考慮使用 ADO.NET 和 .NET Framework Data Provider for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 來取代 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client，以便存取最新 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 版本的所有新功能。 如需有關 .NET Framework Data Provider for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的詳細資訊，請參閱 ADO.NET 的 .NET Framework SDK 文件集。  
  
 為了讓 ADO 使用最新 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 版本的新功能，我們已經對 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者新增了一些增強功能，以便擴充 OLE DB 的核心功能。 這些增強功能可讓 ADO 應用程式使用較新的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 功能，以及取用 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 所導入的兩種資料類型：**xml** 和 **udt**。 這些增強功能也會利用 **varchar**、**nvarchar** 和 **varbinary** 資料類型的增強功能。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client 會將 SSPROP_INIT_DATATYPECOMPATIBILITY 初始化屬性加入至 ADO 應用程式所使用的 DBPROPSET_SQLSERVERDBINIT 屬性集，以便以與 ADO 相容的方式來公開新的資料類型。 此外， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者也會定義在連接字串中設定的新連接字串關鍵字，名為**DataTypeCompatibility** 。  
  
> [!NOTE]  
>  現有的 ADO 應用程式可以使用 SQLOLEDB 提供者來存取並更新 XML、UDT 和大數值文字與二進位欄位值。 新的較大 **varchar(max)** 、**nvarchar(max)** 和 **varbinary(max)** 資料類型會分別傳回成 ADO 類型 **adLongVarChar**、**adLongVarWChar** 和 **adLongVarBinary**。 XML 資料行會傳回成 **adLongVarChar**，而且 UDT 資料行會傳回成 **adVarBinary**。 不過，如果您使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者（SQLNCLI11）而不是 SQLOLEDB，則必須確定將**DataTypeCompatibility**關鍵字設定為 "80"，如此新的資料類型才會正確對應至 ADO 資料類型。  
  
## <a name="enabling-sql-server-native-client-from-ado"></a>從 ADO 啟用 SQL Server Native Client  
 若要啟用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 的使用，ADO 應用程式必須在其連接字串中執行下列關鍵字：  
  
-   `Provider=SQLNCLI11`  
  
-   `DataTypeCompatibility=80`  
  
 如需 Native Client 中支援的 ADO 連接字串關鍵字的詳細資訊 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ，請參閱搭配[使用連接字串關鍵字與 SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)。  
  
 以下範例會建立完全啟用以搭配 Native Client 使用的 ADO 連接字串 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ，包括啟用 MARS 功能：  
  
```  
Dim con As New ADODB.Connection  
  
con.ConnectionString = "Provider=SQLNCLI11;" _  
         & "Server=(local);" _  
         & "Database=AdventureWorks;" _   
         & "Integrated Security=SSPI;" _  
         & "DataTypeCompatibility=80;" _  
         & "MARS Connection=True;"  
con.Open  
```  
  
## <a name="examples"></a>範例  
 下列各節提供如何使用 ADO 搭配 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者的範例。  
  
### <a name="retrieving-xml-column-data"></a>擷取 XML 資料行資料  
 在這個範例中，使用了資料錄集來擷取並顯示 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **AdventureWorks** 範例資料庫中 XML 資料行的資料。  
  
```  
Dim con As New ADODB.Connection  
Dim rst As New ADODB.Recordset  
Dim sXMLResult As String  
  
con.ConnectionString = "Provider=SQLNCLI11;" _  
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
  
con.ConnectionString = "Provider=SQLNCLI11;" _  
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
 在此範例中，連接字串的結構是為了透過 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者啟用 MARS，然後建立兩個記錄集物件，以便使用相同的連接來執行。  
  
```  
Dim con As New ADODB.Connection  
  
con.ConnectionString = "Provider=SQLNCLI11;" _  
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
  
 在舊版 OLE DB 提供者中，此程式碼會導致系統在第二次執行時建立隱含連接，因為每個單一連接只能開啟一個作用中結果集。 由於隱含連接不會在 OLE DB 連接集區中共用，所以這會產生額外的負擔。 使用 Native Client OLE DB 提供者所公開的 MARS 功能時 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ，您會在單一連接上收到多個作用中結果。  
  
## <a name="see-also"></a>另請參閱  
 [使用 SQL Server Native Client 建置應用程式](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)  
  
  
