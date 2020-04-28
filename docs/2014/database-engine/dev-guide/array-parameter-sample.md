---
title: 陣列參數範例 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
ms.assetid: 5d7034ca-ce88-4a7e-8dd9-82f867479e7f
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 822dc7f3d66afc44c187d199674a22f20977f535
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "74055909"
---
# <a name="array-parameter-sample"></a>陣列參數範例
  有時，在資料庫中建立、更新或刪除一組資料列非常有用。 您可以使用數種方法實現此目標。 其中之一便是從用戶端將資訊的陣列，傳遞至使用 Common Language Runtime (CLR) 整合使用者自訂資料類型之伺服器上的 CLR 整合預存程序。 此類使用者自訂資料類型的性質將提供給伺服器的資料大小限制在 8000 位元組。 因此，此方法無法滿足大型或複雜的資料。 如果管理的資料較小而且簡單，則相較於呼叫每一個資料列的預存程序，此方法會更有效。 藉由傳遞陣列，對於順序重要的那些應用程式可保留資料的順序。此範例包含下列項目：  
  
1.  `ContactTypeNames` 使用者定義資料類型。 包含所要求之連絡人類型名稱的清單。  
  
2.  實作成 Microsoft Visual C# 或 Microsoft Visual Basic 方法的 `usp_EnsureContactTypeNames` 預存程序。 這會接受 `ContactTypeNames` 使用者定義資料類型的執行個體，並在 `Person.ContactType` 資料表中插入可存放任何連絡人名稱的新資料列，這些連絡人名稱包含在該資料表所沒有的使用者定義資料類型執行個體中。  
  
3.  `TestArrayParameter` 主控台應用程式。 這會根據所傳入之命令列參數建立 `ContactTypeNames` 使用者定義資料類型的執行個體，然後叫用 `usp_EnsureContactTypeNames` 預存程序，方法是將使用者定義資料類型的執行個體做為參數進行傳遞。  
  
## <a name="prerequisites"></a>Prerequisites  
 若要建立並執行這個專案，您必須安裝下列軟體：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express。 您可以從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express 文件集和範例[網站](https://www.microsoft.com/download/details.aspx?id=42299)免費取得 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express  
  
-   您可以從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 開發人員[網站](https://archive.codeplex.com/?p=SqlServerSamples)取得 AdventureWorks 資料庫  
  
-   .NET Framework SDK 2.0 或更新版本或是 Microsoft Visual Studio 2005 或更新版本。 您可以免費取得 .NET Framework SDK。  
  
-   此外，您也必須符合下列條件：  
  
-   您所使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體必須啟用 CLR 整合。  
  
-   若要啟用 CLR 整合，請執行下列步驟：  
  
    #### <a name="enabling-clr-integration"></a>啟用 CLR 整合  
  
    -   執行下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 命令：  
  
     `sp_configure 'clr enabled', 1`  
  
     `GO`  
  
     `RECONFIGURE`  
  
     `GO`  
  
    > [!NOTE]  
    >  若要啟用 CLR 整合，您必須擁有 `ALTER SETTINGS` 伺服器層級權限，此權限是由系統管理員 (`sysadmin`) 和伺服器管理員 (`serveradmin`) 固定伺服器角色的成員以隱含方式持有。  
  
-   AdventureWorks 資料庫必須安裝在您所使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上。  
  
-   如果您不是正在使用之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的管理員，則必須讓管理員授與您 **CreateAssembly** 權限來完成安裝。  
  
## <a name="building-the-sample"></a>建立範例  
  
#### <a name="create-and-run-the-sample-by-using-the-following-instructions"></a>使用下列指示來建立並執行範例：  
  
1.  開啟 Visual Studio 或 .NET Framework 命令提示字元。  
  
2.  必要時，請建立範例的目錄。 在此範例中，我們將使用 C:\MySample。  
  
3.  在 c:\MySample 中，建立 `ContactTypeNames.vb` (適用於 Visual Basic 範例) 或 `ContactTypeNames.cs` (適用於 C# 範例) 並將適當的 Visual Basic 或 C# 範例程式碼 (下面) 複製到檔案中。  
  
4.  根據您選擇的語言，在命令列提示字元中執行下列其中一段程式碼，藉以將範例程式碼編譯成必要的組件。  
  
    -   `Vbc /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Data.dll,C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.dll,C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Xml.dll  /target:library ContactTypeNames.vb`  
  
    -   `Csc /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Data.dll /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.dll /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Xml.dll /target:library ContactTypeNames.cs`  
  
5.  在 c:\MySample 中，建立 `Program.vb` (適用於 Visual Basic 範例) 或 `Program.cs` (適用於 C# 範例) 並將適當的 Visual Basic 或 C# 範例程式碼 (下面) 複製到檔案中。  
  
6.  在 Program 檔案中找到適當的程式碼行 (大約是第 24 行) 並將 `XXX` 取代成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱。  
  
    -   `Dim connection As New SqlConnection("data source=XXX;initial catalog=AdventureWorks;Integrated Security=SSPI")`  
  
    -   `using (SqlConnection connection = new SqlConnection("data source=XXX;initial catalog=AdventureWorks;Integrated Security=SSPI"))`  
  
7.  根據您選擇的語言，在命令列提示字元中執行下列其中一段程式碼，藉以將範例程式碼編譯成必要的可執行檔。  
  
    -   `vbc /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Data.dll,C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Deployment.dll,C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.dll,C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Drawing.dll,C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Windows.Forms.dll,C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Xml.dll,C:\MySample\ContactTypeNames.dll /out:TestArrayParameter Program.vb`  
  
    -   `Csc /reference:ContactTypeNames.dll /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Data.dll /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.dll /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Xml.dll /out:TestArrayParameter.exe Program.cs`  
  
8.  將 [!INCLUDE[tsql](../../includes/tsql-md.md)] 安裝程式碼複製到檔案中，並將它儲存成範例目錄中的 `Install.sql`。  
  
9. 如果此範例安裝在 `C:\MySample\` 以外的目錄中，請依照指示編輯 `Install.sql` 檔案，以指向該位置。  
  
10. 部署組件、預存程序和函數，方法是執行  
  
    -   `sqlcmd -E -I -i install.sql`  
  
11. 在命令提示字元中執行下列程式碼行，藉以測試應用程式：  
  
    -   `TestArrayParameter "Executive Sales Representative" "Executive Sales Manager"`  
  
12. 將 [!INCLUDE[tsql](../../includes/tsql-md.md)] 清除指令碼複製到檔案中，並將它儲存成範例目錄中的 `cleanup.sql`。  
  
13. 使用下列命令來執行指令碼  
  
    -   `sqlcmd -E -I -i cleanup.sql`  
  
## <a name="sample-code"></a>範例程式碼  
 下面是此範例的程式碼清單。  
  
 這是 `ContactTypeNames.` 程式庫的程式碼。  
  
 C#  
  
```  
#region Using directives  
  
using System;  
using System.Data;  
using System.Data.Sql;  
using System.Data.SqlTypes;  
using System.Collections;  
using System.Collections.Generic;  
using System.Text;  
using System.Globalization;  
using Microsoft.SqlServer.Server;  
  
#endregion  
  
    // This class is used to demonstrate passing an array of a fairly small number of reasonably small strings  
    // to a CLR integration based stored procedure on the server.  Because a UDT is limited to 8000 bytes  
    // this approach will not work well for large numbers of strings or long strings.  See the contact  
    // creation stored procedure in the AdventureWorks CLR integration sample for an alternative approach  
    // using XML which does not have these limitations.  
    [Serializable]  
    [Microsoft.SqlServer.Server.SqlUserDefinedType(Microsoft.SqlServer.Server.Format.UserDefined, IsByteOrdered = true, MaxByteSize = 8000)]  
    public class ContactTypeNames : INullable, Microsoft.SqlServer.Server.IBinarySerialize  
    {  
  
        #region Constructors  
        private const int maxByteSize = 8000;  
  
        public ContactTypeNames()  
        {  
        }  
  
        public ContactTypeNames(string[] names)  
        {  
            int numberOfCharacters = 0;  
            foreach (string name in names)  
            {  
                if (name.Length == 0)   
                    throw new ArgumentException("Zero length names are not allowed");  
                numberOfCharacters += name.Length;  
            }  
            int dataByteSize = numberOfCharacters*2 //UTF-16 characters take 2 bytes  
                + names.Length*4  //Four byte header for each string  
                + 4                 //Four byte header for null string at end  
                + 1;                //One byte boolean for null flag  
            if (dataByteSize >= maxByteSize)  
                throw new ArgumentException(string.Format(CultureInfo.InvariantCulture, "Data provided occupies {0} bytes but only {1} bytes "  
                    + "are available", dataByteSize, maxByteSize));  
  
            this._names = names;  
        }  
        #endregion  
  
        #region Accessors  
        public string[] GetTypeNameArray()  
        {  
            //Don't let caller modify our copy of the array  
            return (string[])_names.Clone();  
        }  
  
        //This has an odd API because we can only define Transact-SQL functions on static methods.  
        [SqlFunctionAttribute(FillRowMethodName = "FillNameRow")]  
        public static IEnumerable GetContactTypeNames(ContactTypeNames names)  
        {  
            if (names == null)  
                throw new ArgumentNullException("names");  
  
            return names.GetTypeNameArray();  
        }  
  
        public static void FillNameRow(object nameArrayElement, out string contactName)  
        {  
            contactName = (string)nameArrayElement;  
        }  
  
        #endregion  
  
        #region String Conversions  
  
        /// <summary>  
        /// The string format for contact type names is a sequence of names separated by commas  
        /// </summary>  
        /// <param name="s">a string containing contact type names separated by commas</param>  
        /// <returns>An instance of contact type name containing the specified names</returns>  
        [Microsoft.SqlServer.Server.SqlMethod(DataAccess = Microsoft.SqlServer.Server.DataAccessKind.None, IsDeterministic = false, IsMutator = false, IsPrecise = false,  
        SystemDataAccess = Microsoft.SqlServer.Server.SystemDataAccessKind.None)]  
        public static ContactTypeNames Parse(SqlString s)  
        {  
            if (s.IsNull)  
                return Null;  
            return new ContactTypeNames(s.Value.Split(new char[] {','}));  
        }  
  
        /// <summary>  
        /// Convert the contact type names to a string  
        /// </summary>  
        /// <returns>The contact type names separated by commas</returns>  
        public override string ToString()  
        {  
            if (this.IsNull)  
                return null;  
  
            StringBuilder sb = new StringBuilder();  
            foreach (string name in _names)  
            {  
                if (sb.Length > 0) sb.Append(", ");  
                sb.Append(name);  
            }  
  
            return sb.ToString();  
        }  
        #endregion  
  
        #region INullable Members  
  
        public static ContactTypeNames Null  
        {  
            get  
            {  
                return new ContactTypeNames();  
            }  
        }  
        public bool IsNull  
        {  
            get   
            {   
                return _names == null;   
            }  
        }  
  
        #endregion  
  
        #region IBinarySerialize Members  
  
        //Format:   
        //Byte 1: Null flag (boolean) (true = null)  
        //Byte 2 - 7994: Strings with 4 byte length headers,  
        //               last string is a zero length string.  
        //This format is in part dictated by how the BinaryWriter serializes strings.  See  
        //the Microsoft .NET Framework documentation on System.IO.BinaryWriter for more details.  
  
        public void Read(System.IO.BinaryReader r)  
        {  
            if (r.ReadBoolean())  
            {  
                _names = null;  
                return;  
            }  
            List<String> nameList = new List<String>();  
            string name;  
            while ((name = r.ReadString()).Length != 0)  
            {  
                nameList.Add(name);  
            }  
            _names = new string[nameList.Count];  
            nameList.CopyTo(_names);  
        }  
  
        public void Write(System.IO.BinaryWriter w)  
        {  
            if (w == null)  
                throw new ArgumentNullException("w");  
  
            w.Write(this.IsNull);  
            foreach (string name in _names)  
            {  
                w.Write(name);  
            }  
            w.Write(string.Empty);              
        }  
  
        #endregion  
  
        #region Private Implementation  
  
        private string[] _names;  
        #endregion  
    }  
```  
  
 Visual Basic  
  
```  
#Region "Using directives"  
Imports System  
Imports System.Data  
Imports System.Data.Sql  
Imports System.Data.SqlTypes  
Imports System.Collections  
Imports System.Collections.Generic  
Imports System.Text  
Imports System.Globalization  
Imports Microsoft.SqlServer.Server  
Imports System.Runtime.InteropServices  
#End Region  
  
' This class is used to demonstrate passing an array of a fairly small number of reasonably small strings  
' to a CLR integration based stored procedure on the server.  Because a UDT is limited to 8000 bytes  
' this approach will not work well for large numbers of strings or long strings.  See the contact  
' creation stored procedure in the AdventureWorks CLR integration sample for an alternative approach  
' using XML which does not have these limitations.  
<Serializable()> _  
<SqlUserDefinedType(Format.UserDefined, IsByteOrdered:=True, maxByteSize:=8000), CLSCompliant(False)> _  
Public Class ContactTypeNames  
    Implements INullable, IBinarySerialize  
  
#Region "Constructors"  
    Private Const maxByteSize As Integer = 8000  
  
    Public Sub New()  
    End Sub  
  
    Public Sub New(ByVal names() As String)  
        Dim numberOfCharacters As Integer = 0  
  
        For Each name As String In names  
            If name.Length = 0 Then  
                Throw New ArgumentException("Zero length names are not allowed")  
            End If  
  
            numberOfCharacters += name.Length  
        Next  
  
        'UTF-16 characters take 2 bytes  
        'Four byte header for each string  
        'Four byte header for null string at end  
        'One byte boolean for null flag  
        Dim dataByteSize As Integer = numberOfCharacters * 2 _  
            + names.Length * 4 _  
            + 4 _  
            + 1  
  
        If dataByteSize >= maxByteSize Then  
            Throw New ArgumentException(String.Format(CultureInfo.InvariantCulture, _  
                "Data provided occupies {0} bytes but only {1} bytes are available", _  
                dataByteSize, maxByteSize))  
        End If  
  
        Me._names = names  
    End Sub  
#End Region  
  
#Region "Accessors"  
  
    Public Function GetTypeNameArray() As String()  
        'Don't let caller modify our copy of the array  
        Return CType(Me._names.Clone(), String())  
    End Function  
  
    'This has an odd API because we can only define Transact-SQL functions on static methods.  
    <SqlFunction(FillRowMethodName:="FillNameRow", TableDefinition:="[Name] [Name]")> _  
    Public Shared Function GetContactTypeNames(ByVal names As ContactTypeNames) As IEnumerable  
        If names Is Nothing Then  
            Throw New ArgumentNullException("names")  
        End If  
  
        Return names.GetTypeNameArray()  
    End Function  
  
    Public Shared Sub FillNameRow(ByVal nameArrayElement As Object, <Out()> ByRef contactName As String)  
        contactName = CStr(nameArrayElement)  
    End Sub  
  
#End Region  
  
#Region "String Conversions"  
  
    ''' <summary>  
    ''' The string format for contact type names is a sequence of names separated by commas  
    ''' </summary>  
    ''' <param name="s">a string containing contact type names separated by commas</param>  
    ''' <returns>An instance of contact type name containing the specified names</returns>  
    <Microsoft.SqlServer.Server.SqlMethod(DataAccess:=Microsoft.SqlServer.Server.DataAccessKind.None, IsDeterministic:=False, IsMutator:=False, IsPrecise:=False, SystemDataAccess:=Microsoft.SqlServer.Server.SystemDataAccessKind.None)> _  
    Public Shared Function Parse(ByVal s As SqlString) As ContactTypeNames  
        If s.IsNull Then  
            Return Nothing  
        End If  
  
        Return New ContactTypeNames(s.Value.Split(New Char() {","c}))  
    End Function  
  
    ''' <summary>  
    ''' Convert the contact type names to a string  
    ''' </summary>  
    ''' <returns>The contact type names separated by commas</returns>  
    Public Overrides Function ToString() As String  
        If Me.IsNull Then  
            Return Nothing  
        End If  
  
        Dim sb As New StringBuilder()  
  
        For Each name As String In Me._names  
            If sb.Length > 0 Then  
                sb.Append(", ")  
            End If  
  
            sb.Append(name)  
        Next name  
  
        Return sb.ToString()  
    End Function  
#End Region  
  
#Region "INullable Members"  
  
    Shared ReadOnly Property Null() As ContactTypeNames  
        Get  
            Return New ContactTypeNames()  
        End Get  
    End Property  
  
    Public ReadOnly Property IsNull() As Boolean Implements INullable.IsNull  
        Get  
            Return Me._names Is Nothing  
        End Get  
    End Property  
  
#End Region  
  
#Region "IBinarySerialize Members"  
  
    'Format:   
    'Byte 1: Null flag (boolean) (true = null)  
    'Byte 2 - 7994: Strings with 4 byte length headers,  
    '               last string is a zero length string.  
    'This format is in part dictated by how the BinaryWriter serializes strings.  See  
    'the Microsoft .NET Framework documentation on System.IO.BinaryWriter for more details.  
    Public Sub Read(ByVal r As System.IO.BinaryReader) Implements IBinarySerialize.Read  
        If r.ReadBoolean() Then  
            Me._names = Nothing  
            Return  
        End If  
  
        Dim nameList As New List(Of String)  
        Dim name As String = r.ReadString()  
        While name.Length <> 0  
            nameList.Add(name)  
            name = r.ReadString()  
        End While  
  
        Me._names = New String(nameList.Count - 1) {}  
        nameList.CopyTo(Me._names)  
    End Sub  
  
    Public Sub Write(ByVal w As System.IO.BinaryWriter) Implements IBinarySerialize.Write  
        If w Is Nothing Then  
            Throw New ArgumentNullException("w")  
        End If  
  
        w.Write(Me.IsNull)  
  
        For Each name As String In Me._names  
            w.Write(name)  
        Next  
  
        w.Write(String.Empty)  
    End Sub  
  
#End Region  
  
#Region "Private Implementation"  
    Private _names() As String  
#End Region  
  
End Class  
```  
  
 這是測試可執行檔的程式碼。  
  
 C#  
  
```  
#region Using directives  
  
using System;  
using System.Collections.Generic;  
using System.Text;  
using System.IO;  
using System.Data;  
using System.Data.Sql;  
using System.Data.SqlTypes;  
using System.Data.SqlClient;  
#endregion  
  
    class Program  
    {  
        static void Main(string[] args)  
        {  
            if (args.Length == 0)  
            {  
                Console.WriteLine("Usage: TestArrayParameter contactTypeName1 "  
                    + "contactTypeName2 ... contactTypeNamen");  
                return;  
            }  
            using (SqlConnection connection = new SqlConnection("data source=XXX;initial catalog=AdventureWorks;Integrated Security=SSPI"))  
            {  
                connection.Open();  
                ShowTypeNames(connection, "before any inserts");  
  
                SqlCommand command = connection.CreateCommand();  
                command.CommandText = "usp_EnsureContactTypeNames";  
                command.CommandType = CommandType.StoredProcedure;  
                SqlParameter namesParameter = new SqlParameter("@names", SqlDbType.Udt);  
                namesParameter.UdtTypeName = "ContactTypeNames";  
                namesParameter.Value = new ContactTypeNames(args);  
                command.Parameters.Add(namesParameter);  
                command.ExecuteNonQuery();  
  
                ShowTypeNames(connection, "after any inserts");  
  
            }  
  
        }  
  
        private static void ShowTypeNames(SqlConnection connection, string whenRan)  
        {  
            SqlCommand command = connection.CreateCommand();  
            command.CommandText = "SELECT Name FROM Person.ContactType ORDER BY Name";  
            using (SqlDataReader reader = command.ExecuteReader())  
            {  
                Console.BackgroundColor = ConsoleColor.Blue;  
                Console.Write("Contact type names {0}: ", whenRan);  
                Console.ResetColor();  
                bool first = true;  
                while (reader.Read())  
                {  
                    if (!first) Console.Write(", ");  
                    Console.Write(reader[0].ToString());  
                    first = false;  
                }  
                Console.WriteLine("");  
                Console.WriteLine("");  
            }  
  
        }  
    }  
```  
  
 Visual Basic  
  
```  
#Region "Using directives"  
Imports System  
Imports System.Collections.Generic  
Imports System.Text  
Imports System.IO  
Imports System.Data  
Imports System.Data.Sql  
Imports System.Data.SqlTypes  
Imports System.Data.SqlClient  
#End Region  
  
Class Program  
  
    Shared Sub Main(ByVal args() As String)  
        If args.Length = 0 Then  
            Console.WriteLine("Usage: TestArrayParameter contactTypeName1 " _  
                + "contactTypeName2 ... contactTypeNamen")  
            Return  
        End If  
  
        Dim connection As New SqlConnection("data source=XXX;initial catalog=AdventureWorks;Integrated Security=SSPI")  
        Try  
            connection.Open()  
            ShowTypeNames(connection, "Before any inserts")  
  
            Dim command As SqlCommand = connection.CreateCommand()  
            command.CommandText = "usp_EnsureContactTypeNames"  
            command.CommandType = CommandType.StoredProcedure  
            Dim namesParameter As New SqlParameter("@names", SqlDbType.Udt)  
            namesParameter.UdtTypeName = "ContactTypeNames"  
            namesParameter.Value = New ContactTypeNames(args)  
            command.Parameters.Add(namesParameter)  
            command.ExecuteNonQuery()  
  
            ShowTypeNames(connection, "After any inserts")  
        Finally  
            connection.Dispose()  
        End Try  
    End Sub  
  
    Private Shared Sub ShowTypeNames(ByVal connection As SqlConnection, ByVal whenRan As String)  
        Dim command As SqlCommand = connection.CreateCommand()  
        command.CommandText = "SELECT [Name] FROM [Person].[ContactType] ORDER BY Name"  
        Dim reader As SqlDataReader = command.ExecuteReader()  
        Try  
            Console.BackgroundColor = ConsoleColor.Blue  
            Console.Write("Contact type names {0}: ", whenRan)  
            Console.ResetColor()  
            Dim first As Boolean = True  
            While reader.Read()  
                If Not first Then  
                    Console.Write(", ")  
                End If  
  
                Console.Write(reader(0).ToString())  
                first = False  
            End While  
  
            Console.WriteLine("")  
            Console.WriteLine("")  
        Finally  
            reader.Dispose()  
        End Try  
  
    End Sub  
End Class  
```  
  
 這是 [!INCLUDE[tsql](../../includes/tsql-md.md)] 安裝指令碼 (`Install.sql`)，它會部署組件並在資料庫中建立預存程序和函數。  
  
```  
USE AdventureWorks  
GO  
  
-- Drop existing sprocs, type, and assemblies if any.  
  
IF EXISTS (SELECT * FROM sys.procedures WHERE [name] = 'usp_EnsureContactTypeNames')  
DROP PROCEDURE usp_EnsureContactTypeNames;  
GO  
  
IF EXISTS (SELECT * FROM sys.objects WHERE [name] = N'GetContactTypeNames' and (type = 'FS' or type = 'FT'))    
DROP FUNCTION [GetContactTypeNames];  
GO  
  
IF EXISTS (SELECT * FROM sys.types WHERE [name] = 'ContactTypeNames')  
DROP TYPE ContactTypeNames;  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'ContactTypeNames')  
DROP ASSEMBLY ContactTypeNames;  
GO  
  
-- Add assemblies, type, and sproc  
  
DECLARE @SamplesPath nvarchar(1024)  
-- You may need to modify the value of the this variable if you have installed the sample someplace other than the default location.  
set @SamplesPath= 'C:\MySample\'  
CREATE ASSEMBLY ContactTypeNames   
FROM @SamplesPath + 'ContactTypeNames.dll'  
WITH permission_set = Safe;  
  
CREATE TYPE ContactTypeNames  
EXTERNAL NAME ContactTypeNames.ContactTypeNames;  
GO  
  
CREATE FUNCTION GetContactTypeNames  
(  
@names dbo.ContactTypeNames  
)  
RETURNS TABLE  
(  
[Name] [Name]  
)  
AS EXTERNAL NAME [ContactTypeNames].[ContactTypeNames].[GetContactTypeNames];  
GO  
  
CREATE PROCEDURE usp_EnsureContactTypeNames  
(  
@names dbo.ContactTypeNames  
)  
AS  
SET NOCOUNT ON;  
  
INSERT Person.ContactType ([Name])  
SELECT [Name] FROM GetContactTypeNames(@names) AS PotentialNames  
WHERE [Name] NOT IN (SELECT [Name] FROM Person.ContactType);   
GO  
```  
  
 下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 會從資料庫中移除組件和預存程序。  
  
```  
USE AdventureWorks  
GO  
  
DELETE Person.ContactType WHERE ContactTypeID > 20;  
GO  
  
-- Drop existing sprocs, type, and assemblies if any.  
  
IF EXISTS (SELECT * FROM sys.procedures WHERE [name] = 'usp_EnsureContactTypeNames')  
DROP PROCEDURE usp_EnsureContactTypeNames;  
GO  
  
IF EXISTS (SELECT * FROM sys.objects WHERE [name] = N'GetContactTypeNames' and (type = 'FS' or type = 'FT'))    
DROP FUNCTION [GetContactTypeNames];  
GO  
  
IF EXISTS (SELECT * FROM sys.types WHERE [name] = 'ContactTypeNames')  
DROP TYPE ContactTypeNames;  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'ContactTypeNames')  
DROP ASSEMBLY ContactTypeNames;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [通用語言執行平台 &#40;CLR&#41; 整合的使用案例和範例](../../../2014/database-engine/dev-guide/usage-scenarios-and-examples-for-common-language-runtime-clr-integration.md)  
  
  
