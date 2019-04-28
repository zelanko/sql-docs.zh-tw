---
title: 擷取 UDT 資料 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SqlDataReader object
- ADO.NET [CLR integration]
- binding UDTs [CLR integration]
- UDTs [CLR integration], ADO.NET
- assemblies [CLR integration], user-defined types
- query parameters [CLR integration]
- user-defined types [CLR integration], ADO.NET
- bytes [CLR integration]
ms.assetid: 6a98ac8c-0e69-4c03-83a4-2062cb782049
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 085b1783214e7f629f1cb91084303edacd151c25
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62874637"
---
# <a name="retrieving-udt-data"></a>擷取 UDT 資料
  為了在用戶端上建立使用者定義型別 (UDT)，用戶端應用程式必須提供在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中登錄為 UDT 的組件。 您可以將 UDT 組件置於與應用程式相同的目錄中，或置於全域組件快取 (GAC) 中。 您還可以在專案中設定組件的參考。  
  
## <a name="requirements-for-using-udts-in-adonet"></a>在 ADO.NET 中使用 UDT 的需求  
 載入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的組件與用戶端上的組件必須相容，才可以在用戶端上建立 UDT。 針對以 `Native` 序列化格式定義的 UDT，組件在結構上必須相容。 針對以 `UserDefined` 格式定義的組件，組件在用戶端上必須可用。  
  
 不需藉助用戶端上的 UDT 組件複本，便可從資料表的 UDT 資料行中擷取未經處理的資料。  
  
> [!NOTE]  
>  **SqlClient**可能無法載入 UDT 版本不相符或其他問題發生時的 UDT。 在此情況下，請使用一般疑難排解機制，判斷呼叫應用程式找不到包含 UDT 之組件的原因。 如需詳細資訊，請閱讀 .NET Framework 文件集中名為＜診斷 Managed 偵錯助理的錯誤＞的主題。  
  
## <a name="accessing-udts-with-a-sqldatareader"></a>使用 SqlDataReader 存取 UDT  
 您可以從用戶端程式碼使用 `System.Data.SqlClient.SqlDataReader`，以擷取包含 UDT 資料行的結果集，其會公開為物件的執行個體。  
  
### <a name="example"></a>範例  
 此範例顯示如何使用 `Main` 方法建立新的 `SqlDataReader` 物件。 該程式碼範例內會發生下列動作：  
  
1.  Main 方法建立新的 `SqlDataReader` 物件，並擷取 Point 資料表 (擁有名為 Point 的 UDT 資料行) 的值。  
  
2.  Point UDT 公開定義為整數的 X 及 Y 座標。  
  
3.  UDT 定義 `Distance` 方法及 `GetDistanceFromXY` 方法。  
  
4.  範例程式碼會擷取主索引鍵及 UDT 資料行的值，以示範 UDT 的功能。  
  
5.  範例程式碼呼叫 `Point.Distance` 及 `Point.GetDistanceFromXY` 方法。  
  
6.  結果顯示在主控台視窗中。  
  
> [!NOTE]  
>  應用程式必須已具有對 UDT 組件的參考。  
  
```vb  
Option Explicit On  
Option Strict On  
  
Imports System  
Imports System.Data.Sql  
Imports System.Data.SqlClient  
  
Module ReadPoints  
    Sub Main()  
        Dim connectionString As String = GetConnectionString()  
        Using cnn As New SqlConnection(connectionString)  
            cnn.Open()  
            Dim cmd As New SqlCommand( _  
             "SELECT ID, Pnt FROM dbo.Points", cnn)  
            Dim rdr As SqlDataReader  
            rdr = cmd.ExecuteReader  
  
            While rdr.Read()  
                ' Retrieve the value of the Primary Key column  
                Dim id As Int32 = rdr.GetInt32(0)  
  
                ' Retrieve the value of the UDT  
                Dim pnt As Point = CType(rdr(1), Point)  
  
             ' You can also use GetSqlValue and GetValue  
             ' Dim pnt As Point = CType(rdr.GetSqlValue(1), Point)  
             ' Dim pnt As Point = CType(rdr.GetValue(1), Point)  
  
                ' Print values  
                Console.WriteLine( _  
                 "ID={0} Point={1} X={2} Y={3} DistanceFromXY={4} Distance={5}", _  
                  id, pnt, pnt.X, pnt.Y, pnt.DistanceFromXY(1, 9), pnt.Distance())  
            End While  
            rdr.Close()  
            Console.WriteLine("done")  
        End Using  
    End Sub  
    Private Function GetConnectionString() As String  
        ' To avoid storing the connection string in your code,    
        ' you can retrieve it from a configuration file.  
        Return "Data Source=(local);Initial Catalog=AdventureWorks;" _  
         & "Integrated Security=SSPI;"  
    End Function  
End Module  
```  
  
```csharp  
using System;  
using System.Data.Sql;  
using System.Data.SqlClient;  
  
namespace Microsoft.Samples.SqlServer  
{  
class ReadPoints  
{  
static void Main()  
{  
  string connectionString = GetConnectionString();  
  using (SqlConnection cnn = new SqlConnection(connectionString))  
  {  
    cnn.Open();  
    SqlCommand cmd = new SqlCommand(  
       "SELECT ID, Pnt FROM dbo.Points", cnn);  
    SqlDataReader rdr = cmd.ExecuteReader();  
  
    while (rdr.Read())  
    {  
      // Retrieve the value of the Primary Key column  
      int id = rdr.GetInt32(0);  
  
        // Retrieve the value of the UDT  
        Point pnt = (Point)rdr[1];  
  
        // You can also use GetSqlValue and GetValue  
        // Point pnt = (Point)rdr.GetSqlValue(1);  
        // Point pnt = (Point)rdr.GetValue(1);  
  
        Console.WriteLine(  
        "ID={0} Point={1} X={2} Y={3} DistanceFromXY={4} Distance={5}",   
        id, pnt, pnt.X, pnt.Y, pnt.DistanceFromXY(1, 9), pnt.Distance());  
    }  
  rdr.Close();  
  Console.WriteLine("done");  
  }  
  static private string GetConnectionString()  
  {  
    // To avoid storing the connection string in your code,   
    // you can retrieve it from a configuration file.  
    return "Data Source=(local);Initial Catalog=AdventureWorks;"  
        + "Integrated Security=SSPI";  
  }  
}  
```  
  
## <a name="binding-udts-as-bytes"></a>以位元組繫結 UDT  
 在某些情況下，您可能要從 UDT 資料行擷取未經處理資料。 可能該型別在本機不可使用，或您不想要具現化 UDT 的執行個體。 您可以讀取的未經處理位元組至位元組陣列，使用**GetBytes**方法`SqlDataReader`。 此方法可將指定資料行位移的位元組資料流，讀取至始於指定緩衝區位移的陣列緩衝區。 另一個選項是使用其中一種**GetSqlBytes**或是**GetSqlBinary**方法，讀取所有的單一作業中的內容。 在任何一種情況中，都不會具現化 UDT 物件，所以您無需設定用戶端組件的 UDT 參考。  
  
### <a name="example"></a>範例  
 此範例示範如何擷取**點**資料當做未經處理位元組到位元組陣列，使用`SqlDataReader`。 該程式碼使用 `System.Text.StringBuilder`，將未經處理位元組轉換成要顯示於主控台視窗的字串表示。  
  
```vb  
Option Explicit On  
Option Strict On  
  
Imports System  
Imports System.Data.Sql  
Imports System.Data.SqlClient  
Imports System.Data.SqlTypes  
Imports System.Text  
  
Module GetRawBytes  
    Sub Main()  
        Dim connectionString As String = GetConnectionString()  
        Using cnn As New SqlConnection(connectionString)  
            cnn.Open()  
            Dim cmd As New SqlCommand( _  
             "SELECT ID, Pnt FROM dbo.Points", cnn)  
            Dim rdr As SqlDataReader  
            rdr = cmd.ExecuteReader  
  
            While rdr.Read()  
  
                ' Retrieve the value of the Primary Key column  
                Dim id As Int32 = rdr.GetInt32(0)  
  
                ' Retrieve the raw bytes into a byte array  
                Dim buffer(31) As Byte  
                Dim byteCount As Integer = _  
                 CInt(rdr.GetBytes(1, 0, buffer, 0, 31))  
  
                ' Format and print bytes   
                Dim str As New StringBuilder  
                str.AppendFormat("ID={0} Point=", id)  
  
                Dim i As Integer  
                For i = 0 To (byteCount - 1)  
                    str.AppendFormat("{0:x}", buffer(i))  
                Next  
                Console.WriteLine(str.ToString)  
  
            End While  
            rdr.Close()  
            Console.WriteLine("done")  
        End Using  
    End Sub  
    Private Function GetConnectionString() As String  
        ' To avoid storing the connection string in your code,    
        ' you can retrieve it from a configuration file.  
        Return "Data Source=(local);Initial Catalog=AdventureWorks;" _  
           & "Integrated Security=SSPI;"  
    End Function  
End Module  
```  
  
```csharp  
using System;  
using System.Data.Sql;  
using System.Data.SqlClient;  
using System.Data.SqlTypes;  
using System.Text;  
  
class GetRawBytes  
{  
    static void Main()  
    {  
        string connectionString = GetConnectionString();  
        using (SqlConnection cnn = new SqlConnection(connectionString))  
        {  
            cnn.Open();  
            SqlCommand cmd = new SqlCommand("SELECT ID, Pnt FROM dbo.Points", cnn);  
            SqlDataReader rdr = cmd.ExecuteReader();  
  
            while (rdr.Read())  
            {  
                // Retrieve the value of the Primary Key column  
                int id = rdr.GetInt32(0);  
  
                // Retrieve the raw bytes into a byte array  
                byte[] buffer = new byte[32];  
                long byteCount = rdr.GetBytes(1, 0, buffer, 0, 32);  
  
                // Format and print bytes   
                StringBuilder str = new StringBuilder();  
                str.AppendFormat("ID={0} Point=", id);  
  
                for (int i = 0; i < byteCount; i++)  
                    str.AppendFormat("{0:x}", buffer[i]);  
                Console.WriteLine(str.ToString());  
            }  
            rdr.Close();  
            Console.WriteLine("done");  
        }  
    static private string GetConnectionString()  
    {  
        // To avoid storing the connection string in your code,   
        // you can retrieve it from a configuration file.  
        return "Data Source=(local);Initial Catalog=AdventureWorks;"  
            + "Integrated Security=SSPI";  
    }  
  }  
}  
```  
  
### <a name="example-using-getsqlbytes"></a>使用 GetSqlBytes 的範例  
 此範例示範如何擷取**點**資料當做在單一作業中使用的未經處理位元組**GetSqlBytes**方法。 該程式碼使用 `StringBuilder`，將未經處理位元組轉換成要顯示於主控台視窗的字串表示。  
  
```vb  
Option Explicit On  
Option Strict On  
  
Imports System  
Imports System.Data.Sql  
Imports System.Data.SqlClient  
Imports System.Data.SqlTypes  
Imports System.Text  
  
Module GetRawBytes  
    Sub Main()  
        Dim connectionString As String = GetConnectionString()  
        Using cnn As New SqlConnection(connectionString)  
            cnn.Open()  
            Dim cmd As New SqlCommand( _  
             "SELECT ID, Pnt FROM dbo.Points", cnn)  
            Dim rdr As SqlDataReader  
            rdr = cmd.ExecuteReader  
  
            While rdr.Read()  
                ' Retrieve the value of the Primary Key column  
                Dim id As Int32 = rdr.GetInt32(0)  
  
                ' Use SqlBytes to retrieve raw bytes  
                Dim sb As SqlBytes = rdr.GetSqlBytes(1)  
                Dim byteCount As Long = sb.Length  
  
                ' Format and print bytes   
                Dim str As New StringBuilder  
                str.AppendFormat("ID={0} Point=", id)  
  
                Dim i As Integer  
                For i = 0 To (byteCount - 1)  
                    str.AppendFormat("{0:x}", sb(i))  
                Next  
                Console.WriteLine(str.ToString)  
  
            End While  
            rdr.Close()  
            Console.WriteLine("done")  
        End Using  
    End Sub  
    Private Function GetConnectionString() As String  
        ' To avoid storing the connection string in your code,    
        ' you can retrieve it from a configuration file.  
        Return "Data Source=(local);Initial Catalog=AdventureWorks;" _  
           & "Integrated Security=SSPI;"  
    End Function  
End Module  
```  
  
```csharp  
using System;  
using System.Data.Sql;  
using System.Data.SqlClient;  
using System.Data.SqlTypes;  
using System.Text;  
  
class GetRawBytes  
{  
    static void Main()  
    {  
         string connectionString = GetConnectionString();  
        using (SqlConnection cnn = new SqlConnection(connectionString))  
        {  
            cnn.Open();  
            SqlCommand cmd = new SqlCommand(  
                "SELECT ID, Pnt FROM dbo.Points", cnn);  
            SqlDataReader rdr = cmd.ExecuteReader();  
  
            while (rdr.Read())  
            {  
                // Retrieve the value of the Primary Key column  
                int id = rdr.GetInt32(0);  
  
                // Use SqlBytes to retrieve raw bytes  
                SqlBytes sb = rdr.GetSqlBytes(1);  
                long byteCount = sb.Length;  
  
                // Format and print bytes   
                StringBuilder str = new StringBuilder();  
                str.AppendFormat("ID={0} Point=", id);  
  
                for (int i = 0; i < byteCount; i++)  
                    str.AppendFormat("{0:x}", sb[i]);  
                Console.WriteLine(str.ToString());  
            }  
            rdr.Close();  
            Console.WriteLine("done");  
        }  
    static private string GetConnectionString()  
    {  
        // To avoid storing the connection string in your code,   
        // you can retrieve it from a configuration file.  
        return "Data Source=(local);Initial Catalog=AdventureWorks;"  
            + "Integrated Security=SSPI";  
    }  
  }  
}  
```  
  
## <a name="working-with-udt-parameters"></a>使用 UDT 參數  
 在 ADO.NET 程式碼中，UDT 可以同時當做輸入及輸出參數使用。  
  
## <a name="using-udts-in-query-parameters"></a>在查詢參數中使用 UDT  
 設定 `SqlParameter` 物件的 `System.Data.SqlClient.SqlCommand` 時，可以使用 UDT 做為參數值。 對 `SqlDbType.Udt` 集合呼叫 `SqlParameter` 方法時，可使用 `Add` 物件的 `Parameters` 列舉型別表示參數是 UDT。 `UdtTypeName`的屬性`SqlCommand`物件來指定 UDT 的完整的名稱在資料庫中*database.schema_name.object_name*語法。 儘管並非必須如此，但使用完整名稱可消除程式碼的模稜兩可性。  
  
> [!NOTE]  
>  UDT 組件的本機複本必須可讓用戶端專案使用。  
  
### <a name="example"></a>範例  
 此範例中的程式碼會建立 `SqlCommand` 及 `SqlParameter` 物件，以將資料插入資料表中的 UDT 資料行。 該程式碼使用 `SqlDbType.Udt` 列舉型別來指定資料型別，並使用 `UdtTypeName` 物件的 `SqlParameter` 屬性來指定資料庫中 UDT 的完整名稱。  
  
```vb  
Option Explicit On  
Option Strict On  
  
Imports System  
Imports system.Data  
Imports System.Data.Sql  
Imports System.Data.SqlClient  
  
Module Module1  
  
  Sub Main()  
    Dim ConnectionString As String = GetConnectionString()  
    Dim cnn As New SqlConnection(ConnectionString)  
    Using cnn  
      Dim cmd As SqlCommand = cnn.CreateCommand()  
      cmd.CommandText = "INSERT INTO dbo.Points (Pnt) VALUES (@Point)"  
      cmd.CommandType = CommandType.Text  
  
      Dim param As New SqlParameter("@Point", SqlDbType.Udt)      param.UdtTypeName = "TestPoint.dbo.Point"      param.Direction = ParameterDirection.Input      param.Value = New Point(5, 6)      cmd.Parameters.Add(param)  
  
      cnn.Open()  
      cmd.ExecuteNonQuery()  
      Console.WriteLine("done")  
    End Using  
  End Sub  
    Private Function GetConnectionString() As String  
        ' To avoid storing the connection string in your code,    
        ' you can retrieve it from a configuration file.  
        Return "Data Source=(local);Initial Catalog=AdventureWorks;" _  
           & "Integrated Security=SSPI;"  
    End Function  
End Module  
```  
  
```csharp  
using System;  
using System.Data;  
using System.Data.Sql;  
using System.Data.SqlClient;  
  
class Class1  
{  
static void Main()  
{  
  string ConnectionString = GetConnectionString();  
     using (SqlConnection cnn = new SqlConnection(ConnectionString))  
     {  
       SqlCommand cmd = cnn.CreateCommand();  
       cmd.CommandText =   
         "INSERT INTO dbo.Points (Pnt) VALUES (@Point)";  
       cmd.CommandType = CommandType.Text;  
  
       SqlParameter param = new SqlParameter("@Point", SqlDbType.Udt);       param.UdtTypeName = "TestPoint.dbo.Point";       param.Direction = ParameterDirection.Input;       param.Value = new Point(5, 6);       cmd.Parameters.Add(param);  
  
       cnn.Open();  
       cmd.ExecuteNonQuery();  
       Console.WriteLine("done");  
     }  
    static private string GetConnectionString()  
    {  
        // To avoid storing the connection string in your code,   
        // you can retrieve it from a configuration file.  
        return "Data Source=(local);Initial Catalog=AdventureWorks;"  
            + "Integrated Security=SSPI";  
    }  
  }  
}  
```  
  
## <a name="see-also"></a>另請參閱  
 [存取 ADO.NET 中的使用者定義型別](accessing-user-defined-types-in-ado-net.md)  
  
  
