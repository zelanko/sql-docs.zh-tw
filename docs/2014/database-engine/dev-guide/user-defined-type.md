---
title: 使用者定義型別 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
ms.assetid: a9b75f36-d7f5-47f7-94d6-b4448c6a2191
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 860d2f03018abae2b27367a1f41f87268affb328
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62779832"
---
# <a name="user-defined-type"></a>使用者定義型別
  這個「使用者定義資料類型」範例會示範如何從 Transact-SQL 以及使用 `System.Data.SqlClient` 的用戶端應用程式建立和使用簡單的使用者定義資料類型。  
  
## <a name="prerequisites"></a>先決條件  
 若要建立並執行這個專案，您必須安裝下列軟體：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express。 您可以從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express 文件集和範例[網站](https://go.microsoft.com/fwlink/?LinkId=31046)免費取得 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express  
  
-   您可以從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 開發人員[網站](https://go.microsoft.com/fwlink/?linkid=62796)取得 AdventureWorks 資料庫  
  
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
  
3.  在 c:\MySample 中，建立 `ComplexNumber.vb` (適用於 Visual Basic 範例) 或 `ComplexNumber.cs` (適用於 C# 範例) 並將適當的 Visual Basic 或 C# 範例程式碼 (下面) 複製到檔案中。  
  
4.  根據您選擇的語言，在命令列提示字元中執行下列其中一段程式碼，藉以編譯範例程式碼。  
  
    -   `Vbc /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Data.dll,C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.dll,C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Xml.dll /target:library ComplexNumber.vb`  
  
5.  `Csc /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Data.dll /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.dll /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.XML.dll /target:library ComplexNumber.cs`  
  
6.  將 [!INCLUDE[tsql](../../includes/tsql-md.md)] 安裝程式碼複製到檔案中，並將它儲存成範例目錄中的 `Install.sql`。  
  
7.  如果此範例安裝在 `C:\MySample\` 以外的目錄中，請依照指示編輯 `Install.sql` 檔案，以指向該位置。  
  
8.  部署組件和預存程序，方法是執行  
  
    -   `sqlcmd -E -I -i install.sql`  
  
9. 複製[!INCLUDE[tsql](../../includes/tsql-md.md)]測試命令指令碼至檔案，並將它儲存為`test.sql`範例目錄中。  
  
10. 使用下列命令來執行測試指令碼  
  
    -   `sqlcmd -E -I -i test.sql`  
  
11. 若要執行用戶端範例程式 (僅限 C#)：  
  
    -   在 c:\MySample 中，建立 `Program.cs` 並將原始程式碼複製到此檔案中。  
  
    -   執行`: Csc /reference:ComplexNumber.dll /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Data.dll /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.dll /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.XML.dll /out:Client.exe /target:exe Program.cs`  
  
    -   執行 `Client AdventureWorks`，藉以測試  
  
12. 將 [!INCLUDE[tsql](../../includes/tsql-md.md)] 清除指令碼複製到檔案中，並將它儲存成範例目錄中的 `cleanup.sql`。  
  
13. 使用下列命令來執行指令碼  
  
    -   `sqlcmd -E -I -i cleanup.sql`  
  
## <a name="sample-code"></a>範例程式碼  
 下面是此範例的程式碼清單。  
  
 C#  
  
```  
using System;  
using System.Data.Sql;  
using System.Data.SqlTypes;  
using System.Text.RegularExpressions;  
using System.Runtime.InteropServices;  
using System.Globalization;  
    [Serializable]  
    [Microsoft.SqlServer.Server.SqlUserDefinedType(Microsoft.SqlServer.Server.Format.Native, IsByteOrdered = false)]  
    public struct ComplexNumber : INullable, IComparable  
    {  
        //Regular expression used to parse values that are of the form (1,2i)  
        private static readonly Regex _parser  
            = new Regex(@"\A\(\s*(?<real>\-?\d+(\.\d+)?)\s*,\s*(?<img>\-?\d+(\.\d+)?)\s*i\s*\)\Z",  
            RegexOptions.Compiled | RegexOptions.ExplicitCapture);  
  
        double _real;  
  
        double _imaginary;  
  
        bool _isnull;  
  
        const string NULL = "<<null complex>>";  
  
        static readonly ComplexNumber NULL_INSTANCE = new ComplexNumber(true);  
  
        public ComplexNumber(double real, double imaginary)  
        {  
            this._real = real;  
            this._imaginary = imaginary;  
            this._isnull = false;  
        }  
  
        private ComplexNumber(bool isnull)  
        {  
            this._isnull = isnull;  
            this._real = this._imaginary = 0;  
        }  
  
        public double Real  
        {  
            get  
            {  
                if (this._isnull)  
                    throw new InvalidOperationException();  
  
                return this._real;  
            }  
            set  
            {  
                this._real = value;  
            }  
        }  
  
        public double Imaginary  
        {  
            get  
            {  
                if (this._isnull)  
                    throw new InvalidOperationException();  
  
                return this._imaginary;  
            }  
            set  
            {  
                this._imaginary = value;  
            }  
        }  
  
        public double Modulus  
        {  
            get  
            {  
                if (this._isnull)  
                    throw new InvalidOperationException();  
  
                return Math.Sqrt(this._real * this._real  
                    + this._imaginary * this._imaginary);  
            }  
        }  
  
        #region value-based equality  
        public int CompareTo(object obj)  
        {  
            if (!(obj is ComplexNumber))  
                return -1;  
  
            ComplexNumber c = (ComplexNumber)obj;  
  
            if (this._isnull && c._isnull)  
                return 0;  
  
            if (this._isnull || c._isnull)  
                return -1;  
  
            if (this._real == c._real && this._imaginary == c._imaginary)  
                return 0;  
  
            if (Modulus == c.Modulus) // same modulus but different r/i, force diff  
                return -1;  
  
            // arbitrary comparison...semantics for complex numbers not necessarily correct  
            return Modulus.CompareTo(c.Modulus);  
        }  
  
        public override bool Equals(object obj)  
        {  
            return this.CompareTo(obj) == 0;  
        }  
  
        public override int GetHashCode()  
        {  
            return Modulus.GetHashCode();  
        }  
  
        public static SqlBoolean operator ==(ComplexNumber c1, ComplexNumber c2)  
        {  
            return c1.Equals(c2);  
        }  
  
        public static SqlBoolean operator !=(ComplexNumber c1, ComplexNumber c2)  
        {  
            return !c1.Equals(c2);  
        }  
  
        public static SqlBoolean operator <(ComplexNumber c1, ComplexNumber c2)  
        {  
            return c1.CompareTo(c2) < 0;  
        }  
  
        public static SqlBoolean operator >(ComplexNumber c1, ComplexNumber c2)  
        {  
            return c1.CompareTo(c2) > 0;  
        }  
  
        #endregion  
  
        public override string ToString()  
        {  
            return this._isnull ? NULL : ("("  
                + this._real.ToString(CultureInfo.InvariantCulture) + ","  
                + this._imaginary.ToString(CultureInfo.InvariantCulture)  
                + "i)");  
        }  
  
        public bool IsNull  
        {  
            get  
            {  
                return this._isnull;  
            }  
        }  
  
        public static ComplexNumber Parse(SqlString sqlString)  
        {  
            string value = sqlString.ToString();  
  
if (sqlString.IsNull || value == NULL)  
return new ComplexNumber(true);  
  
            Match m = _parser.Match(value);  
  
            //Get the message from Properties.Resource.  
            if (!m.Success)  
                throw new ArgumentException("Invalid format for complex number. Format is ( n, mi ) where n and m are floating point numbers");      
  
            return new ComplexNumber(double.Parse(m.Groups[1].Value,  
                CultureInfo.InvariantCulture), double.Parse(m.Groups[2].Value,  
                CultureInfo.InvariantCulture));  
        }  
  
        public static ComplexNumber Null  
        {  
            get  
            {  
                return NULL_INSTANCE;  
            }  
        }  
    }  
  
```  
  
 Visual Basic  
  
```  
Imports Microsoft.SqlServer.Server  
Imports Microsoft.VisualBasic  
Imports System  
Imports System.Collections  
Imports System.Data  
Imports System.Data.SqlClient  
Imports System.Data.SqlTypes  
Imports System.Diagnostics  
Imports System.Globalization  
Imports System.Reflection  
Imports System.Runtime.InteropServices  
Imports System.Text  
  
''' <summary>  
''' AssemblyBrowser is a simple utility for composing sql queries over   
''' assembly metadata. It uses a table-valued-function to return  
''' a table to SqlServer.  
''' </summary>  
  
Public NotInheritable Class AssemblyBrowser  
    ''' <summary>  
    ''' Get the types in the assembly, as a table  
    ''' </summary>  
    ''' <param name="name"></param>  
    ''' <returns></returns>  
    <Microsoft.SqlServer.Server.SqlFunction(FillRowMethodName:="FillTypeRow", Name:="GetTypes", _  
        TableDefinition:="FullName nvarchar(256), BaseTypeName nvarchar(256), IsValueType bit, NumFields int, IsSerializable bit, IsISerializable bit, IsLayoutSequential bit, Namespace nvarchar(256), IsPublic bit, IsSealed bit, AssemblyName nvarchar(256)")> _  
    Public Shared Function GetTypes(ByVal name As String) As IEnumerable  
        Dim e As IEnumerable  
  
        Try  
            Dim a As [Assembly] = GetAssembly(name)  
            If a Is Nothing Then  
                e = New Type(-1) {}  
            Else  
                e = a.GetTypes()  
            End If  
  
        Catch te As ReflectionTypeLoadException  
            'could not load some of the types, just return the types that you could load  
            e = te.Types  
        End Try  
  
        Return e  
    End Function  
  
    ''' <summary>  
    ''' Called by SQL Server to populate a row in the results of the TVF.  Takes a type and  
    ''' breaks the information up into separate columns for the row being generated.  
    ''' </summary>  
    ''' <param name="row"></param>  
    ''' <param name="fullName"></param>  
    ''' <param name="baseTypeName"></param>  
    ''' <param name="isValueType"></param>  
    ''' <param name="numFields"></param>  
    ''' <param name="isSerializable"></param>  
    ''' <param name="isISerializable"></param>  
    ''' <param name="isLayoutSequential"></param>  
    ''' <param name="namespace"></param>  
    ''' <param name="isPublic"></param>  
    ''' <param name="isSealed"></param>  
    ''' <param name="assemblyName"></param>  
    ''' <remarks></remarks>  
    Public Shared Sub FillTypeRow(ByVal row As Object, <Out()> ByRef fullName As String, <Out()> ByRef baseTypeName As String, _  
        <Out()> ByRef isValueType As Boolean, <Out()> ByRef numFields As Integer, <Out()> ByRef isSerializable As Boolean, _  
        <Out()> ByRef isISerializable As Boolean, <Out()> ByRef isLayoutSequential As Boolean, <Out()> ByRef [namespace] As String, _  
        <Out()> ByRef isPublic As Boolean, <Out()> ByRef isSealed As Boolean, <Out()> ByRef assemblyName As String)  
  
        If row Is Nothing Then  
            Return  
        End If  
  
        Dim t As Type = CType(row, Type)  
  
        fullName = t.FullName  
        If (t.BaseType Is Nothing) Then  
            baseTypeName = String.Empty  
        Else  
            baseTypeName = t.BaseType.FullName  
        End If  
  
        isValueType = t.IsValueType  
  
        Dim fields As FieldInfo() = t.GetFields(BindingFlags.Instance Or BindingFlags.Public)  
  
        If (fields Is Nothing) Then  
            numFields = 0  
        Else  
            numFields = fields.Length  
        End If  
  
        isSerializable = t.IsSerializable  
        isISerializable = GetType(System.Runtime.Serialization.ISerializable).IsAssignableFrom(t)  
        isLayoutSequential = t.IsLayoutSequential  
        [namespace] = t.Namespace  
        isPublic = t.IsPublic  
        isSealed = t.IsSealed  
        assemblyName = t.Assembly.GetName().Name  
    End Sub  
  
    Friend Shared Function GetAssembly(ByVal name As String) As [Assembly]  
        Try  
            Return [Assembly].Load(name)  
        Catch  
            Return Nothing  
        End Try  
    End Function  
  
    Private Sub New()  
    End Sub  
  
    <SqlFunction(FillRowMethodName:="FillAssemblyRow", Name:="GetLoadedAssemblies", _  
        TableDefinition:="FullName nvarchar(256)")> _  
    Public Shared Function GetLoadedAssemblies() As IEnumerable  
        Dim e As IEnumerable = AppDomain.CurrentDomain.GetAssemblies()  
        'Dim schemas() As Microsoft.SqlServer.Server.SqlMetaData = _  
        '    {New Microsoft.SqlServer.Server.SqlMetaData("FullName", _  
        '    SqlDbType.NVarChar, 256)}  
  
        Return e  
    End Function  
    Public Shared Sub FillAssemblyRow(ByVal row As Object, <Out()> ByRef fullName As String)  
        If row Is Nothing Then Throw New ArgumentNullException("row")  
        fullName = CType(row, [Assembly]).FullName  
    End Sub  
End Class  
<Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute(Microsoft.SqlServer.Server.Format.Native), Serializable()> _  
Public Structure SimpleUdt  
    Implements INullable  
#Region "udt contract"  
  
    Public Overrides Function ToString() As String  
        Return Value.ToString()  
    End Function  
  
    Public ReadOnly Property IsNull() As Boolean Implements INullable.IsNull  
        Get  
            Return Me.Value.IsNull  
        End Get  
    End Property  
  
    Public Shared ReadOnly Property Null() As SimpleUdt  
        Get  
            Dim h As New SimpleUdt()  
  
            Return h  
        End Get  
    End Property  
  
    Public Shared Function Parse(ByVal sqlString As SqlString) As SimpleUdt  
        If sqlString.IsNull Then  
            Return Null  
        End If  
  
        Dim simpleUdt As New SimpleUdt()  
  
        simpleUdt.Value = New SqlInt32(Integer.Parse(sqlString.Value, _  
            System.Globalization.CultureInfo.InvariantCulture))  
  
        Return simpleUdt  
    End Function  
#End Region  
  
#Region "implementation"  
    Private privValue As SqlInt32  
  
    Private _examplePublicField As SqlInt32  
  
    Public Property ExamplePublicField() As SqlInt32  
        Get  
            Return Me._examplePublicField  
        End Get  
        Set(ByVal value As SqlInt32)  
            Me._examplePublicField = value  
        End Set  
    End Property  
  
    Public Property Value() As SqlInt32  
        Get  
            Return Me.privValue  
        End Get  
        Set(ByVal value As SqlInt32)  
            Me.privValue = value  
        End Set  
    End Property  
  
    <Microsoft.SqlServer.Server.SqlMethod(IsDeterministic:=True)> _  
    Public Function ReturnValue() As SqlInt32  
        Return Me.privValue  
    End Function  
#End Region  
End Structure  
Public NotInheritable Class UdtServices  
#Region "udt fields"  
  
    ''' <summary>  
    ''' Get the fields in the UDT callable from tsql, as a table  
    ''' </summary>  
    ''' <param name="udtName"></param>  
    ''' <returns></returns>  
    <Microsoft.SqlServer.Server.SqlFunction(FillRowMethodName:="FillFieldRow", Name:="GetFields", TableDefinition:="Name nvarchar(128), Type nvarchar(128), RoutineProperties nvarchar(128)")> _  
    Public Shared Function GetUdtFields(ByVal udtName As String) As IEnumerable  
        Dim fields As ArrayList = GetSqlFields(GetUdt(udtName))  
  
        Return fields  
    End Function  
    Public Shared Sub FillFieldRow(ByVal row As Object, ByRef [name] As String, ByRef type As String)  
        Dim fi As FieldInfo = CType(row, FieldInfo)  
  
        [name] = fi.Name  
        type = fi.FieldType.Name  
    End Sub  
  
#End Region  
  
#Region "udt properties"  
  
    ''' <summary>  
    ''' Get the properties defined in a particular UDT  
    ''' </summary>  
    ''' <param name="udtName"></param>  
    ''' <returns></returns>  
    <Microsoft.SqlServer.Server.SqlFunction(FillRowMethodName:="FillPropertyRow", Name:="GetProperties", TableDefinition:="Name nvarchar(128), Type nvarchar(128), RoutineProperties nvarchar(128)")> _  
    Public Shared Function GetUdtProperties(ByVal udtName As String) As IEnumerable  
        Dim properties As ArrayList = GetSqlProperties(GetUdt(udtName))  
  
        Return properties  
    End Function  
  
    ''' <summary>  
    ''' Called by SQL Server to populate a row of the results of the TVF.    
    ''' </summary>  
    ''' <param name="row"></param>  
    ''' <param name="name"></param>  
    ''' <param name="type"></param>  
    ''' <param name="routineProperties"></param>  
    ''' <remarks></remarks>  
    Public Shared Sub FillPropertyRow(ByVal row As Object, ByRef name As String, ByRef type As String, ByRef routineProperties As String)  
        Dim pi As PropertyInfo = CType(row, PropertyInfo)  
  
        name = pi.Name  
        type = pi.PropertyType.Name  
  
        Dim methInfo As MethodInfo = pi.GetGetMethod()  
        Dim attrs As Object() = methInfo.GetCustomAttributes( _  
            GetType(Microsoft.SqlServer.Server.SqlMethodAttribute), True)  
  
        If Not (attrs Is Nothing) AndAlso attrs.Length = 1 Then  
            Dim attr As Microsoft.SqlServer.Server.SqlMethodAttribute _  
                = CType(attrs(0), Microsoft.SqlServer.Server.SqlMethodAttribute)  
  
            routineProperties = GetRoutineProperties(attr)  
        End If  
    End Sub  
  
#End Region  
  
#Region "udt methods"  
  
    ''' <summary>  
    ''' Get the methods on the UDT callable from tsql, as a table  
    ''' </summary>  
    ''' <param name="udtName"></param>  
    ''' <returns></returns>  
    <Microsoft.SqlServer.Server.SqlFunction(FillRowMethodName:="FillMethodRow", Name:="GetMethods", TableDefinition:="Name nvarchar(128), Parameters nvarchar(4000), Type nvarchar(128), RoutineProperties nvarchar(128)")> _  
    Public Shared Function GetUdtMethods(ByVal udtName As String) As IEnumerable  
        Dim methods As ArrayList = GetSqlMethods(GetUdt(udtName))  
  
        Return methods  
    End Function  
  
    ''' <summary>  
    ''' Called by SQL Server to populate a row being returned by the TVF.  Breaks apart the   
    ''' MethodInfo object into the data which will populate each column of the row being returned.  
    ''' </summary>  
    ''' <param name="row"></param>  
    ''' <param name="name"></param>  
    ''' <param name="parameters"></param>  
    ''' <param name="type"></param>  
    ''' <param name="routineProperties"></param>  
    ''' <remarks></remarks>  
    Public Shared Sub FillMethodRow(ByVal row As Object, ByRef name As String, ByRef parameters As String, _  
        ByRef type As String, ByRef routineProperties As String)  
        Dim methInfo As MethodInfo = CType(row, MethodInfo)  
  
        name = methInfo.Name  
  
        Dim sb As New StringBuilder("(")  
        Dim first As Boolean = True  
  
        Dim pi As ParameterInfo  
        For Each pi In methInfo.GetParameters()  
            If first Then  
                first = False  
            Else  
                sb.Append(", ")  
            End If  
  
            sb.Append(pi.Name).Append(" ").Append(pi.ParameterType.Name)  
        Next pi  
  
        sb.Append(")")  
        parameters = sb.ToString()  
        type = methInfo.ReturnType.Name  
  
        Dim attrs As Object() = methInfo.GetCustomAttributes( _  
            GetType(Microsoft.SqlServer.Server.SqlMethodAttribute), True)  
  
        If Not (attrs Is Nothing) AndAlso attrs.Length = 1 Then  
            Dim attr As Microsoft.SqlServer.Server.SqlMethodAttribute _  
                = CType(attrs(0), Microsoft.SqlServer.Server.SqlMethodAttribute)  
  
            routineProperties = GetRoutineProperties(attr)  
        End If  
    End Sub  
  
#End Region  
  
#Region "internal utility functions"  
    Private Sub New()  
    End Sub  
  
    ''' <summary>  
    ''' Utility function to get the string representation of  
    ''' routine properties on a type  
    ''' </summary>  
    ''' <param name="attr"></param>  
    ''' <returns></returns>  
    Private Shared Function GetRoutineProperties(ByVal attr As Microsoft.SqlServer.Server.SqlMethodAttribute) As String  
        Dim sb As New StringBuilder()  
  
        If attr.OnNullCall Then  
            sb.Append("on_null_call ")  
        End If  
  
        If attr.IsMutator Then  
            sb.Append("mutator ")  
        End If  
  
        If attr.IsDeterministic Then  
            sb.Append("deterministic ")  
        End If  
  
        If attr.IsPrecise Then  
            sb.Append("precise ")  
        End If  
  
        If attr.DataAccess <> Microsoft.SqlServer.Server.DataAccessKind.None Then  
            sb.Append("data_access " & [Enum].GetName( _  
                GetType(Microsoft.SqlServer.Server.DataAccessKind), attr.DataAccess))  
        End If  
  
        Return sb.ToString()  
    End Function  
  
    ''' <summary>  
    ''' Is this a valid parameter type that can be accessible from tsql  
    ''' </summary>  
    ''' <param name="t"></param>  
    ''' <returns></returns>  
    Private Shared Function IsSqlParameterType(ByVal t As Type) As Boolean  
        If validParameterTypes.ContainsKey(t) Then  
            Return True  
        End If  
  
        If t.FullName.StartsWith("System.Data.SqlTypes") Then  
            Return True  
        End If  
  
        If t.GetCustomAttributes( _  
            GetType(Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute), _  
            True).Length = 1 Then  
            Return True  
        End If  
  
        Return False  
    End Function  
  
    ''' <summary>  
    ''' Is the field type valid?  
    ''' </summary>  
    ''' <param name="f"></param>  
    ''' <param name="declaringType"></param>  
    ''' <returns></returns>  
    Private Shared Function IsSqlField(ByVal f As FieldInfo, ByVal declaringType As Type) As Boolean  
        If Not f.DeclaringType Is declaringType Then  
            Return False  
        End If  
  
        Return IsSqlParameterType(f.FieldType)  
    End Function  
  
    ''' <summary>  
    ''' Is the property valid to be called from tsql?  
    ''' </summary>  
    ''' <param name="f"></param>  
    ''' <param name="declaringType"></param>  
    ''' <returns></returns>  
    Private Shared Function IsSqlProperty(ByVal f As PropertyInfo, ByVal declaringType As Type) As Boolean  
        If Not f.DeclaringType Is declaringType Then  
            Return False  
        End If  
  
        Return IsSqlParameterType(f.PropertyType)  
    End Function  
  
    ''' <summary>  
    ''' Is the method valid to be called from tsql?  
    ''' </summary>  
    ''' <param name="m"></param>  
    ''' <param name="declaringType"></param>  
    ''' <returns></returns>  
    Private Shared Function IsSqlMethod(ByVal m As MethodInfo, ByVal declaringType As Type) As Boolean  
        If Not m.DeclaringType Is declaringType Then  
            Return False  
        End If  
  
        Dim info As ParameterInfo  
        For Each info In m.GetParameters()  
            If Not IsSqlParameterType(info.ParameterType) Then  
                Return False  
            End If  
        Next info  
  
        Return IsSqlParameterType(m.ReturnType)  
    End Function  
  
    ''' <summary>  
    ''' Get the udt specified by the clr type name.  
    ''' </summary>  
    ''' <param name="udtName"></param>  
    ''' <returns></returns>  
    Private Shared Function GetUdt(ByVal udtName As String) As Type  
        Return Type.GetType(udtName, True)  
    End Function  
  
    ''' <summary>  
    ''' Get the methods on a type  
    ''' </summary>  
    ''' <param name="t"></param>  
    ''' <returns></returns>  
    Private Shared Function GetSqlMethods(ByVal t As Type) As ArrayList  
        Dim methods As MethodInfo() = t.GetMethods(BindingFlags.Instance Or BindingFlags.Public Or BindingFlags.DeclaredOnly)  
        Dim temp As New ArrayList()  
  
        Dim info As MethodInfo  
        For Each info In methods  
            If IsSqlMethod(info, t) Then  
                temp.Add(info)  
            End If  
        Next info  
  
        Return temp  
    End Function  
  
    ''' <summary>  
    ''' get the properties on a type  
    ''' </summary>  
    ''' <param name="t"></param>  
    ''' <returns></returns>  
    Private Shared Function GetSqlProperties(ByVal t As Type) As ArrayList  
        Dim props As PropertyInfo() = t.GetProperties(BindingFlags.Instance Or BindingFlags.Public Or BindingFlags.DeclaredOnly)  
        Dim temp As New ArrayList()  
  
        Dim info As PropertyInfo  
        For Each info In props  
            If IsSqlProperty(info, t) Then  
                temp.Add(info)  
            End If  
        Next info  
  
        Return temp  
    End Function  
  
    ''' <summary>  
    ''' get the fields on a type  
    ''' </summary>  
    ''' <param name="t"></param>  
    ''' <returns></returns>  
    Private Shared Function GetSqlFields(ByVal t As Type) As ArrayList  
        Dim fields As FieldInfo() = t.GetFields(BindingFlags.Instance Or BindingFlags.Public Or BindingFlags.DeclaredOnly)  
        Dim temp As New ArrayList()  
  
        Dim info As FieldInfo  
        For Each info In fields  
            If IsSqlField(info, t) Then  
                temp.Add(info)  
            End If  
        Next info  
  
        Return temp  
    End Function  
  
    ''' <summary>  
    ''' readonly static used to cache frequently used information  
    ''' </summary>  
    Private Shared ReadOnly validParameterTypes As Hashtable = GetValidParameterTypes()  
  
    ''' <summary>  
    ''' initialize the cached mapping of valid parameter types  
    ''' </summary>  
    Private Shared Function GetValidParameterTypes() As Hashtable  
        Dim validTypes As New Hashtable()  
  
        validTypes(GetType(Boolean)) = True  
        validTypes(GetType(Byte)) = True  
        validTypes(GetType(Short)) = True  
        validTypes(GetType(Char)) = True  
        validTypes(GetType(Integer)) = True  
        validTypes(GetType(Single)) = True  
        validTypes(GetType(Long)) = True  
        validTypes(GetType(Double)) = True  
        validTypes(GetType(String)) = True  
        validTypes(GetType(Guid)) = True  
  
        Return validTypes  
    End Function  
#End Region  
  
#Region "public utility functions"  
  
    <Microsoft.SqlServer.Server.SqlFunction(DataAccess:=Microsoft.SqlServer.Server.DataAccessKind.Read)> _  
    Public Shared Function GetFullAssemblyName(ByVal sqlName As String) As String  
        Using conn As New SqlConnection("context connection=true")  
            Dim cmd As SqlCommand = conn.CreateCommand()  
            cmd.CommandText = "SELECT @sqlName, " _  
                & "assemblyproperty(@sqlName, 'VersionMajor'), " _  
                & "assemblyproperty(@sqlName, 'VersionMinor'), " _  
                & "assemblyproperty(@sqlName, 'VersionBuild'), " _  
                & "assemblyproperty(@sqlName, 'VersionRevision'), " _  
                & "assemblyproperty(@sqlName, 'CultureInfo'), " _  
                & "assemblyproperty(@sqlName, 'PublicKey'), " _  
                & "assemblyproperty(@sqlName, 'Architecture');"  
  
            cmd.Parameters.AddWithValue("@sqlName", sqlName)  
            conn.Open()  
            Dim rdr As SqlDataReader = cmd.ExecuteReader()  
            If Not rdr.Read() Then  
                Throw New ArgumentException( _  
                    String.Format(System.Globalization.CultureInfo.InvariantCulture, _  
                    "Assembly {0} does not exist.", sqlName))  
            End If  
  
            Dim culture As SqlString  
            Dim publicKeyToken As SqlBinary  
  
            If (rdr.IsDBNull(5)) Then  
                culture = SqlString.Null  
            Else  
                culture = rdr.GetSqlString(5)  
            End If  
  
            If (rdr.IsDBNull(6)) Then  
                publicKeyToken = SqlBinary.Null  
            Else  
                publicKeyToken = rdr.GetSqlBinary(6)  
            End If  
  
            Return GetAssemblyName(rdr.GetString(0), rdr.GetInt32(1), rdr.GetInt32(2), _  
                rdr.GetInt32(3), rdr.GetInt32(4), culture, publicKeyToken)  
        End Using  
    End Function  
  
    ''' <summary>  
    ''' Helper function to return the assembly name from   
    ''' its components stored in sql metadata.  
    ''' </summary>  
    ''' <param name="friendlyName"></param>  
    ''' <param name="majorVersion"></param>  
    ''' <param name="minorVersion"></param>  
    ''' <param name="build"></param>  
    ''' <param name="revision"></param>  
    ''' <param name="culture"></param>  
    ''' <param name="publicKeyToken"></param>  
    ''' <returns></returns>  
    Private Shared Function GetAssemblyName(ByVal friendlyName As String, ByVal majorVersion As Integer, ByVal minorVersion As Integer, ByVal build As Integer, ByVal revision As Integer, ByVal culture As SqlString, ByVal publicKeyToken As SqlBinary) As String  
        Dim sb As New StringBuilder()  
        sb.Append(friendlyName).Append(","c)  
        sb.Append("Version=")  
        sb.Append(majorVersion).Append("."c)  
        sb.Append(minorVersion).Append("."c)  
        sb.Append(build).Append("."c)  
        sb.Append(revision).Append(","c)  
        sb.Append("Culture=")  
        If (culture.IsNull) Then  
            sb.Append("neutral")  
        Else  
            sb.Append(culture.Value)  
        End If  
  
        sb.Append(","c)  
        sb.Append("PublicKeyToken=")  
        If publicKeyToken.IsNull Then  
            sb.Append("null")  
        Else  
            Dim b As Byte  
            For Each b In publicKeyToken.Value  
                sb.Append(b.ToString("X2", CultureInfo.InvariantCulture))  
            Next b  
        End If  
  
        Return sb.ToString()  
    End Function  
  
    Private Shared Function ToHexString(ByVal value() As Byte) As String  
        If value Is Nothing Then  
            Return Nothing  
        End If  
  
        Dim sb As New StringBuilder()  
        Dim b As Byte  
  
        For Each b In value  
            sb.Append(b.ToString("X2", CultureInfo.InvariantCulture))  
        Next b  
  
        Return sb.ToString()  
    End Function  
#End Region  
End Class  
```  
  
 這是 [!INCLUDE[tsql](../../includes/tsql-md.md)] 安裝指令碼 (`Install.sql`)，它會部署組件並在資料庫中建立 UDT。  
  
```  
USE AdventureWorks  
GO  
IF EXISTS (SELECT * FROM sys.types WHERE name = N'ComplexNumber')  
DROP TYPE ComplexNumber;  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE name = N'ComplexNumber')   
DROP ASSEMBLY ComplexNumber;  
GO  
  
DECLARE @SamplesPath nvarchar(1024)  
-- You may need to modify the value of the this variable if you have installed   
-- the sample someplace other than the default location.  
SET @SamplesPath = 'C:\MySample\'  
  
CREATE ASSEMBLY ComplexNumber   
FROM @SamplesPath + 'ComplexNumber.dll'  
WITH permission_set=Safe;  
GO  
  
CREATE TYPE ComplexNumber  
EXTERNAL NAME [ComplexNumber].[ComplexNumber];  
GO  
```  
  
 這是 `test.sql`，它會執行類型，藉以測試範例。  
  
```  
USE AdventureWorks  
GO  
  
-- Get the full CLR name for UDTUtilities  
SELECT dbo.GetFullAssemblyName(N'UDTUtilities');  
GO  
  
-- Get all the types in this dll  
SELECT * FROM dbo.GetTypes(dbo.GetFullAssemblyName(N'UDTUtilities'));   
GO  
  
-- Get the full CLR name for SimpleUdt  
SELECT dbo.GetClrTypeName('SimpleUdt');  
GO  
  
-- Get the methods on the SimpleUdt type  
SELECT * FROM dbo.GetMethods(dbo.GetClrTypeName('SimpleUdt'));  
GO  
  
-- More complex query to dump all the methods for all the types in the system  
SELECT   
    st.name AS TypeName,   
    methods.Name AS MethodName,   
    methods.Parameters,   
    methods.Type,   
    methods.RoutineProperties   
FROM sys.assembly_types st   
    CROSS APPLY dbo.GetMethods(dbo.GetClrTypeName(st.name)) methods  
GO  
```  
  
 下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 會從資料庫中移除組件和類型。  
  
```  
USE AdventureWorks  
GO  
  
IF EXISTS (SELECT * FROM sys.types WHERE name = N'ComplexNumber')  
DROP TYPE ComplexNumber;  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE name = N'ComplexNumber')   
DROP ASSEMBLY ComplexNumber;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [通用語言執行平台 &#40;CLR&#41; 整合的使用案例和範例](../../../2014/database-engine/dev-guide/usage-scenarios-and-examples-for-common-language-runtime-clr-integration.md)  
  
  
