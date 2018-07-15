---
title: 字串公用程式函數範例 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 9623013f-15f1-4614-8dac-1155e57c880c
caps.latest.revision: 12
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 892a950795569b87f5a09d4b30aa5b171b26321e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37275094"
---
# <a name="string-utility-functions-sample"></a>字串公用程式函數範例
  這個「字串公用程式」範例包含以 Visual C# 和 Visual Basic 撰寫的資料流資料表值函式，它會將逗號分隔字串分割成具有一個資料行的資料表。 它也包含彙總函式，可將字串資料行轉換為逗號分隔字串。  另外還實作純量函數和資料表值函式，它們提供規則運算式取代和規則運算式搜尋功能。  
  
 若要實作資料流資料表值函式，請建立傳回實作 `IEnumerable` 介面之物件的方法。 此 `IEnumerable` 方法必須透過屬性與填入資料表值函式資料列的另一個方法連結。  
  
## <a name="prerequisites"></a>先決條件  
 若要建立並執行這個專案，您必須安裝下列軟體：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express。 您可以從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express 文件集和範例[網站](http://go.microsoft.com/fwlink/?LinkId=31046)免費取得 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express  
  
-   您可以從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 開發人員[網站](http://go.microsoft.com/fwlink/?linkid=62796)取得 AdventureWorks 資料庫  
  
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
  
3.  在 c:\MySample 中，建立 `StringUtils.vb` (適用於 Visual Basic 範例) 或 `StringUtils.cs` (適用於 C# 範例) 並將適當的 Visual Basic 或 C# 範例程式碼 (下面) 複製到檔案中。  
  
4.  根據您選擇的語言，在命令列提示字元中執行下列其中一段程式碼，藉以編譯範例程式碼。  
  
    -   `Vbc /target:library /reference:"C:\Program Files (x86)\Reference Assemblies\Microsoft\Framework\v3.5\System.Core.dll",C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Data.dll,C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.dll,C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Xml.dll /debug- /target:library StringUtils.vb`  
  
    -   `Csc/reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Data.dll /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.dll /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.XML.dll /target:library StringUtils.cs`  
  
5.  將 [!INCLUDE[tsql](../../includes/tsql-md.md)] 安裝程式碼複製到檔案中，並將它儲存成範例目錄中的 `Install.sql`。  
  
6.  如果此範例安裝在 `C:\MySample\` 以外的目錄中，請依照指示編輯 `Install.sql` 檔案，以指向該位置。  
  
7.  部署組件和預存程序，方法是執行  
  
    -   `sqlcmd -E -I -i install.sql`  
  
    -   複製[!INCLUDE[tsql](../../includes/tsql-md.md)]測試命令指令碼至檔案，並將它儲存為`test.sql`範例目錄中。  
  
8.  使用下列命令來執行測試指令碼  
  
    -   `sqlcmd -E -I -i test.sql`  
  
9. 將 [!INCLUDE[tsql](../../includes/tsql-md.md)] 清除指令碼複製到檔案中，並將它儲存成範例目錄中的 `cleanup.sql`。  
  
10. 使用下列命令來執行指令碼  
  
    -   `sqlcmd -E -I -i cleanup.sql`  
  
  
## <a name="sample-code"></a>範例程式碼  
 下面是此範例的程式碼清單。  
  
 C#  
  
```  
  
using System;  
using System.IO;  
using System.Collections;  
using System.Collections.Generic;  
using System.Text;  
using System.Data;  
using System.Data.SqlTypes;  
using System.Data.Sql;  
using System.Text.RegularExpressions;  
using Microsoft.SqlServer.Server;  
  
    /// <summary>  
    /// This class is provides regular expression operations for Transact-SQL callers  
    /// </summary>  
    public sealed class RegularExpression  
    {  
        private RegularExpression()  
        {  
  
        }  
  
        /// <summary>  
        /// This method returns a table of matches, groups, and captures based on the input  
        /// string and pattern string provided.  
        /// </summary>  
        /// <param name="sqlInput">What to match against</param>  
        /// <param name="sqlPattern">What to look for</param>  
        /// <returns>An object which appears to be reading from SQL Server but which in fact is reading  
        ///          from a memory based representation of the data.</returns>  
        [SqlFunction(FillRowMethodName = "FillRow")]  
        public static IEnumerable Matches(SqlString sqlInput, SqlString sqlPattern)  
        {  
            string input = (sqlInput.IsNull) ? string.Empty : sqlInput.Value;  
            string pattern = (sqlPattern.IsNull) ? string.Empty : sqlPattern.Value;  
  
            return GetMatches(input, pattern);  
        }  
  
        public static void FillRow(object obj, out int matchId, out int matchIndex, out string matchValue,  
            out int groupId, out int groupIndex, out string groupValue, out int captureIndex,  
            out string captureValue)  
        {  
            MatchResult result = (MatchResult)obj;  
            matchId = result.MatchID;  
            matchIndex = result.MatchIndex;  
            matchValue = result.MatchValue;  
            groupId = result.GroupID;  
            groupIndex = result.GroupIndex;  
            groupValue = result.GroupValue;  
            captureIndex = result.CaptureIndex;  
            captureValue = result.CaptureValue;  
        }  
  
        /// <summary>  
        ///     Generates a list of Match/Group/Capture tuples represented using the  
        ///     MatchResult struct based on the regular expression match of the input  
        ///     string and pattern string provided.  
        /// </summary>  
        /// <param name="input">What to match</param>  
        /// <param name="pattern">What to look for</param>  
        /// <returns>A list of Match/Group/Capture tuples</returns>  
        private static List<MatchResult> GetMatches(string input, string pattern)  
        {  
            List<MatchResult> result = new List<MatchResult>();  
            int matchId = 0;  
            int groupId = 0;  
            foreach (Match m in Regex.Matches(input, pattern))  
            {  
                if (m.Groups.Count < 1)  
                    result.Add(new MatchResult(matchId, m.Index, m.Value, -1, -1, string.Empty, -1, string.Empty));  
                else  
                {  
                    groupId = 0;  
                    foreach (Group g in m.Groups)  
                    {  
                        if (g.Captures.Count < 1)  
                            result.Add(new MatchResult(matchId, m.Index, m.Value,  
                                groupId, g.Index, g.Value, -1, string.Empty));  
                        else  
                        {  
                            foreach (Capture c in m.Groups)  
                            {  
                                result.Add(new MatchResult(matchId, m.Index, m.Value,  
                                    groupId, g.Index, g.Value, c.Index, c.Value));  
                            }  
                        }  
  
                        groupId += 1;  
                    }  
                }  
  
                matchId += 1;  
            }  
  
            return result;  
        }  
  
        /// <summary>  
        ///     This method performs a pattern based substitution based on the provided input string, pattern  
        ///     string, and replacement string.  
        /// </summary>  
        /// <param name="sqlInput">The source material</param>  
        /// <param name="sqlPattern">How to parse the source material</param>  
        /// <param name="sqlReplacement">What the output should look like</param>  
        /// <returns></returns>  
        public static string Replace(SqlString sqlInput, SqlString sqlPattern, SqlString sqlReplacement)  
        {  
            string input = (sqlInput.IsNull) ? string.Empty : sqlInput.Value;  
            string pattern = (sqlPattern.IsNull) ? string.Empty : sqlPattern.Value;  
            string replacement = (sqlReplacement.IsNull) ? string.Empty : sqlReplacement.Value;  
            return Regex.Replace(input, pattern, replacement);  
        }  
    }  
  
    /// <summary>  
    /// This struct is used trepresents a Match/Group/Capture tuple.  Instances of this struct are  
    /// created by the GetMatches method.  
    /// </summary>  
    internal struct MatchResult  
    {  
        /// <summary>  
        /// Which match this is  
        /// </summary>  
        private int _matchID;  
        public int MatchID  
        {  
            get  
            {  
                return this._matchID;  
            }  
        }  
  
        /// <summary>  
        /// Where the match starts in the input string  
        /// </summary>  
        private int _matchIndex;  
        public int MatchIndex  
        {  
            get  
            {  
                return this._matchIndex;  
            }  
        }  
  
        /// <summary>  
        /// What string matched the pattern  
        /// </summary>  
        private string _matchValue;  
        public string MatchValue  
        {  
            get  
            {  
                return this._matchValue;  
            }  
        }  
  
        /// <summary>  
        /// Which matching group this is  
        /// </summary>  
        private int _groupID;  
        public int GroupID  
        {  
            get  
            {  
                return this._groupID;  
            }  
        }  
  
        /// <summary>  
        /// Where this group starts in the input string  
        /// </summary>  
        private int _groupIndex;  
        public int GroupIndex  
        {  
            get  
            {  
                return this._groupIndex;  
            }  
        }  
  
        /// <summary>  
        /// What the group matched in the input string  
        /// </summary>  
        private string _groupValue;  
        public string GroupValue  
        {  
            get  
            {  
                return this._groupValue;  
            }  
        }  
  
        /// <summary>  
        /// Where this capture starts in the input string  
        /// </summary>  
        private int _captureIndex;  
        public int CaptureIndex  
        {  
            get  
            {  
                return this._captureIndex;  
            }  
        }  
  
        /// <summary>  
        /// What the capture matched in the input string  
        /// </summary>  
        private string _captureValue;  
        public string CaptureValue  
        {  
            get  
            {  
                return this._captureValue;  
            }  
        }  
  
        /// <summary>  
        ///     A convenient constructor which fills in all the fields contained in this struct.  
        /// </summary>  
        /// <param name="matchID">Which match this is</param>  
        /// <param name="matchIndex">Where the match starts in the input string</param>  
        /// <param name="matchValue">What string matched the pattern</param>  
        /// <param name="groupID">Which matching group this is</param>  
        /// <param name="groupIndex">Where this group starts in the input string</param>  
        /// <param name="groupValue">What the group matched in the input string</param>  
        /// <param name="captureIndex">Where this capture starts in the input string</param>  
        /// <param name="captureValue">What the capture matched in the input string</param>  
        public MatchResult(int matchId, int matchIndex, string matchValue,  
            int groupId, int groupIndex, string groupValue,  
            int captureIndex, string captureValue)  
        {  
            this._matchID = matchId;  
            this._matchIndex = matchIndex;  
            this._matchValue = matchValue;  
            this._groupID = groupId;  
            this._groupIndex = groupIndex;  
            this._groupValue = groupValue;  
            this._captureIndex = captureIndex;  
            this._captureValue = captureValue;  
        }  
    }  
  
    public sealed class StringSplitter  
    {  
  
        /// <summary>  
        /// The streaming table-valued function used to split the string into a relation  
        /// </summary>  
        /// <param name="argument"></param>  
        /// <returns></returns>  
        [SqlFunction(FillRowMethodName = "FillRow")]  
        public static IEnumerable Split(SqlString argument)  
        {  
            string value;  
            if (argument.IsNull)  
                value = "";  
            else  
                value = argument.Value;  
            return value.Split(',');  
        }  
  
        public static void FillRow(Object obj, out string stringElement)  
        {  
            stringElement = (string)obj;  
        }  
  
        /// <summary>  
        /// Don't allow callers to create instances of this class  
        /// </summary>  
        private StringSplitter() { }  
    }  
    [Serializable]  
    [Microsoft.SqlServer.Server.SqlUserDefinedAggregate(  
        Microsoft.SqlServer.Server.Format.UserDefined, //use clr serialization to serialize the intermediate result  
        IsInvariantToNulls = true,//optimizer property  
        IsInvariantToDuplicates = false,//optimizer property  
        IsInvariantToOrder = false,//optimizer property  
        MaxByteSize = 8000)//maximum size in bytes of persisted value  
        ]  
    public class Concatenate : Microsoft.SqlServer.Server.IBinarySerialize  
    {  
        /// <summary>  
        /// The variable that holds the intermediate result of the concatenation  
        /// </summary>  
        private StringBuilder intermediateResult;  
  
        /// <summary>  
        /// Initialize the internal data structures  
        /// </summary>  
        public void Init()  
        {  
            intermediateResult = new StringBuilder();  
        }  
  
        /// <summary>  
        /// Accumulate the next value, nop if the value is null  
        /// </summary>  
        /// <param name="value"></param>  
        public void Accumulate(SqlString value)  
        {  
  
            if (value.IsNull)  
            {  
                return;  
            }  
            intermediateResult.Append(value.Value).Append(',');  
  
        }  
  
        /// <summary>  
        /// Merge the partially computed aggregate with this aggregate.  
        /// </summary>  
        /// <param name="other"></param>  
        public void Merge(Concatenate other)  
        {  
            intermediateResult.Append(other.intermediateResult);  
        }  
  
        /// <summary>  
        /// Called at the end of aggregation, to return the results of the aggregation  
        /// </summary>  
        /// <returns></returns>  
        public SqlString Terminate()  
        {  
            string output = string.Empty;  
            //delete the trailing comma, if any  
            if (intermediateResult != null && intermediateResult.Length > 0)  
                output = intermediateResult.ToString(0, intermediateResult.Length - 1);  
            return new SqlString(output);  
        }  
  
        public void Read(BinaryReader r)  
        {  
            if (r == null) throw new ArgumentNullException("r");  
            intermediateResult = new StringBuilder(r.ReadString());  
        }  
  
        public void Write(BinaryWriter w)  
        {  
            if (w == null) throw new ArgumentNullException("w");  
            w.Write(intermediateResult.ToString());  
        }  
    }  
  
```  
  
 VB.NET  
  
```  
Imports Microsoft.VisualBasic  
Imports Microsoft.SqlServer.Server  
Imports System  
Imports System.Collections  
Imports System.Collections.Generic  
Imports System.Data  
Imports System.Data.SqlTypes  
Imports System.Diagnostics  
Imports System.IO  
Imports System.Linq  
Imports System.Runtime.InteropServices  
Imports System.Text  
Imports System.Text.RegularExpressions  
  
<Serializable(), Microsoft.SqlServer.Server.SqlUserDefinedAggregate(Microsoft.SqlServer.Server.Format.UserDefined, IsInvariantToNulls:=True, IsInvariantToDuplicates:=False, IsInvariantToOrder:=False, MaxByteSize:=8000)> _  
Public Class Concatenate  
    'use clr serialization to serialize the intermediate result  
    'optimizer property  
    'optimizer property  
    'optimizer property  
    'maximum size in bytes of persisted value  
    Implements Microsoft.SqlServer.Server.IBinarySerialize  
  
    ''' <summary>  
    ''' The variable that holds the intermediate result of the concatenation  
    ''' </summary>  
    Private intermediateResult As StringBuilder  
  
    ''' <summary>  
    ''' Initialize the internal data structures  
    ''' </summary>  
    Public Sub Init()  
        intermediateResult = New StringBuilder()  
    End Sub  
  
    ''' <summary>  
    ''' Accumulate the next value, nop if the value is null  
    ''' </summary>  
    ''' <param name="value"></param>  
    Public Sub Accumulate(ByVal value As SqlString)  
        If value.IsNull Then  
            Return  
        End If  
  
        intermediateResult.Append(value.Value).Append(","c)  
    End Sub  
  
    ''' <summary>  
    ''' Merge the partially computed aggregate with this aggregate.  
    ''' </summary>  
    ''' <param name="other"></param>  
    Public Sub Merge(ByVal other As Concatenate)  
        intermediateResult.Append(other.intermediateResult)  
    End Sub  
  
    ''' <summary>  
    ''' Called at the end of aggregation, to return the results of the aggregation  
    ''' </summary>  
    ''' <returns></returns>  
    Public Function Terminate() As SqlString  
        Dim output As String = String.Empty  
  
        'delete the trailing comma, if any  
        If Not (intermediateResult Is Nothing) AndAlso intermediateResult.Length > 0 Then  
            output = intermediateResult.ToString(0, intermediateResult.Length - 1)  
        End If  
  
        Return New SqlString(output)  
    End Function  
  
    Public Sub Read(ByVal r As BinaryReader) Implements Microsoft.SqlServer.Server.IBinarySerialize.Read  
        If r Is Nothing Then  
            Throw New ArgumentNullException("r")  
        End If  
        intermediateResult = New StringBuilder(r.ReadString())  
    End Sub  
  
    Public Sub Write(ByVal w As BinaryWriter) Implements Microsoft.SqlServer.Server.IBinarySerialize.Write  
        If w Is Nothing Then  
            Throw New ArgumentNullException("w")  
        End If  
        w.Write(intermediateResult.ToString())  
    End Sub  
End Class  
  
Public NotInheritable Class RegularExpression  
  
    Private Sub New()  
    End Sub  
  
    ''' <summary>  
    ''' This method returns a table of matches, groups, and captures based on the input  
    ''' string and pattern string provided.  
    ''' </summary>  
    ''' <param name="sqlInput">What to match against</param>  
    ''' <param name="sqlPattern">What to look for</param>  
    ''' <returns>An object which appears to be reading from SQL Server but which in fact is reading  
    '''          from a memory based representation of the data.</returns>  
    <SqlFunction(Name:="RegexMatches", FillRowMethodName:="FillMatchRow", _  
        TableDefinition:="MatchID int, MatchIndex int, MatchValue nvarchar(4000), GroupID int, GroupIndex int, GroupValue nvarchar(4000), CaptureIndex int, CaptureValue nvarchar(4000)")> _  
    Public Shared Function Matches(ByVal sqlInput As SqlString, ByVal sqlPattern As SqlString) As IEnumerable  
        Dim input As String = String.Empty  
        If Not sqlInput.IsNull Then  
            input = sqlInput.Value  
        End If  
  
        Dim pattern As String = String.Empty  
        If Not sqlPattern.IsNull Then  
            pattern = sqlPattern.Value  
        End If  
  
        Return GetMatches(input, pattern)  
    End Function  
  
    ''' <summary>  
    ''' Invoked by SQL Server when returning a row of the TVF.  Splits the MatchResult object into  
    ''' the separate pieces of data which will form the columns of the row.  
    ''' </summary>  
    ''' <param name="row"></param>  
    ''' <param name="matchID"></param>  
    ''' <param name="matchIndex"></param>  
    ''' <param name="matchValue"></param>  
    ''' <param name="groupID"></param>  
    ''' <param name="groupIndex"></param>  
    ''' <param name="groupValue"></param>  
    ''' <param name="captureIndex"></param>  
    ''' <param name="captureValue"></param>  
  
    Private Shared Sub FillMatchRow(ByVal row As Object, <Out()> ByRef matchId As Integer, _  
        <Out()> ByRef matchIndex As Integer, <Out()> ByRef matchValue As String, <Out()> ByRef groupId As Integer, _  
        <Out()> ByRef groupIndex As Integer, <Out()> ByRef groupValue As String, <Out()> ByRef captureIndex As Integer, _  
        <Out()> ByRef captureValue As String)  
  
        Dim result As MatchResult  
  
        result = CType(row, MatchResult)  
  
        matchId = result.MatchID  
        matchIndex = result.MatchIndex  
        matchValue = result.MatchValue  
        groupId = result.GroupID  
        groupIndex = result.GroupIndex  
        groupValue = result.GroupValue  
        captureIndex = result.CaptureIndex  
        captureValue = result.CaptureValue  
    End Sub  
  
    ''' <summary>  
    '''     Generates a list of Match/Group/Capture tuples represented using the  
    '''     MatchResult struct based on the regular expression match of the input  
    '''     string and pattern string provided.  
    ''' </summary>  
    ''' <param name="input">What to match</param>  
    ''' <param name="pattern">What to look for</param>  
    ''' <returns>A list of Match/Group/Capture tuples</returns>  
    Private Shared Function GetMatches(ByVal input As String, ByVal pattern As String) As List(Of MatchResult)  
        Dim result As List(Of MatchResult) = New List(Of MatchResult)()  
        Dim matchID As Integer = 0  
        Dim groupID As Integer = 0  
  
        For Each m As Match In Regex.Matches(input, pattern)  
            If m.Groups.Count < 1 Then  
                result.Add(New MatchResult(matchID, m.Index, m.Value, -1, -1, _  
                    String.Empty, -1, String.Empty))  
            Else  
                groupID = 0  
                For Each g As Group In m.Groups  
                    If g.Captures.Count < 1 Then  
                        result.Add(New MatchResult(matchID, m.Index, m.Value, _  
                            groupID, g.Index, g.Value, -1, String.Empty))  
                    Else  
                        For Each c As Capture In m.Groups  
                            result.Add(New MatchResult(matchID, m.Index, _  
                                m.Value, groupID, g.Index, g.Value, c.Index, _  
                                c.Value))  
                        Next  
                    End If  
  
                    groupID += 1  
                Next  
            End If  
  
            matchID += 1  
        Next  
  
        Return result  
    End Function  
  
    ''' <summary>  
    '''     This method performs a pattern based substitution based on the provided input string, pattern  
    '''     string, and replacement string.  
    ''' </summary>  
    ''' <param name="sqlInput">The source material</param>  
    ''' <param name="sqlPattern">How to parse the source material</param>  
    ''' <param name="sqlReplacement">What the output should look like</param>  
    ''' <returns></returns>  
    <SqlFunction(Name:="RegexReplace", DataAccess:=DataAccessKind.None)> _  
    Public Shared Function Replace(ByVal sqlInput As SqlString, ByVal sqlPattern As SqlString, ByVal sqlReplacement As SqlString) As String  
        Dim input As String = String.Empty  
  
        If Not sqlInput.IsNull Then  
            input = sqlInput.Value  
        End If  
  
        Dim pattern As String = String.Empty  
  
        If Not sqlPattern.IsNull Then  
            pattern = sqlPattern.Value.ToString()  
        End If  
  
        Dim replacement As String = String.Empty  
  
        If Not sqlReplacement.IsNull Then  
            replacement = sqlReplacement.Value.ToString()  
        End If  
  
        Return Regex.Replace(input, pattern, replacement)  
    End Function  
End Class  
  
''' <summary>  
''' This struct is used to represent a Match/Group/Capture tuple.  Instances of   
''' this struct are created by the GetMatches method.  
''' </summary>  
Friend Structure MatchResult  
    ''' <summary>  
    ''' Which match this is  
    ''' </summary>  
    Private _matchID As Integer  
  
    Friend ReadOnly Property MatchID() As Integer  
        Get  
            Return Me._matchID  
        End Get  
    End Property  
  
    ''' <summary>  
    ''' Where the match starts in the input string  
    ''' </summary>  
    Private _matchIndex As Integer  
  
    Friend ReadOnly Property MatchIndex() As Integer  
        Get  
            Return Me._matchIndex  
        End Get  
    End Property  
  
    ''' <summary>  
    ''' What string matched the pattern  
    ''' </summary>  
    Private _matchValue As String  
  
    Friend ReadOnly Property MatchValue() As String  
        Get  
            Return Me._matchValue  
        End Get  
    End Property  
  
    ''' <summary>  
    ''' Which matching group this is  
    ''' </summary>  
    Private _groupID As Integer  
  
    Friend ReadOnly Property GroupID() As Integer  
        Get  
            Return Me._groupID  
        End Get  
    End Property  
  
    ''' <summary>  
    ''' Where this group starts in the input string  
    ''' </summary>  
    Private _groupIndex As Integer  
  
    Friend ReadOnly Property GroupIndex() As Integer  
        Get  
            Return Me._groupIndex  
        End Get  
    End Property  
  
    ''' <summary>  
    ''' What the group matched in the input string  
    ''' </summary>  
    Private _groupValue As String  
  
    Friend ReadOnly Property GroupValue() As String  
        Get  
            Return Me._groupValue  
        End Get  
    End Property  
  
    ''' <summary>  
    ''' Where this capture starts in the input string  
    ''' </summary>  
    Private _captureIndex As Integer  
  
    Friend ReadOnly Property CaptureIndex() As Integer  
        Get  
            Return Me._captureIndex  
        End Get  
    End Property  
  
    ''' <summary>  
    ''' What the capture matched in the input string  
    ''' </summary>  
    Private _captureValue As String  
  
    Friend ReadOnly Property CaptureValue() As String  
        Get  
            Return Me._captureValue  
        End Get  
    End Property  
  
    ''' <summary>  
    '''     A convenient constructor which fills in all the fields contained in this struct.  
    ''' </summary>  
    ''' <param name="matchID">Which match this is</param>  
    ''' <param name="matchIndex">Where the match starts in the input string</param>  
    ''' <param name="matchValue">What string matched the pattern</param>  
    ''' <param name="groupID">Which matching group this is</param>  
    ''' <param name="groupIndex">Where this group starts in the input string</param>  
    ''' <param name="groupValue">What the group matched in the input string</param>  
    ''' <param name="captureIndex">Where this capture starts in the input string</param>  
    ''' <param name="captureValue">What the capture matched in the input string</param>  
    Friend Sub New(ByVal matchID As Integer, ByVal matchIndex As Integer, ByVal matchValue As String, ByVal groupID As Integer, ByVal groupIndex As Integer, ByVal groupValue As String, ByVal captureIndex As Integer, ByVal captureValue As String)  
        Me._matchID = matchID  
        Me._matchIndex = matchIndex  
        Me._matchValue = matchValue  
        Me._groupID = groupID  
        Me._groupIndex = groupIndex  
        Me._groupValue = groupValue  
        Me._captureIndex = captureIndex  
        Me._captureValue = captureValue  
    End Sub  
End Structure  
Public NotInheritable Class StringSplitter  
  
    ''' <summary>  
    ''' The streaming table-valued function used to split the string into a relation  
    ''' </summary>  
    ''' <param name="argument"></param>  
    ''' <returns></returns>  
    <SqlFunction(Name:="Split", DataAccess:=DataAccessKind.None, FillRowMethodName:="FillSplitRow", _  
        TableDefinition:="StringElement nvarchar(128) COLLATE Latin1_General_CI_AS")> _  
    Public Shared Function Split(ByVal argument As SqlString) As IEnumerable  
        Dim value As String  
  
        If argument.IsNull Then  
            value = String.Empty  
        Else  
            value = argument.Value  
        End If  
  
        Return value.Split(","c)  
    End Function  
  
    Private Shared Sub FillSplitRow(ByVal row As Object, ByRef stringElement As String)  
        stringElement = CType(row, String)  
    End Sub  
  
    ''' <summary>  
    ''' Don't allow callers to create instances of this class  
    ''' </summary>  
    Private Sub New()  
    End Sub  
End Class  
  
```  
  
 這是 [!INCLUDE[tsql](../../includes/tsql-md.md)] 安裝指令碼 (`Install.sql`)，它會部署組件並在資料庫中建立預存程序。  
  
```  
USE AdventureWorks  
GO  
  
IF OBJECT_ID(N'RegexMatches', N'FT') is not null  
DROP Function RegexMatches;  
GO  
  
IF OBJECT_ID(N'Split', N'FT') is not null  
DROP Function Split;  
GO  
  
IF OBJECT_ID(N'RegexReplace', N'FS') is not null  
DROP Function RegexReplace;  
GO  
  
IF OBJECT_ID(N'Concatenate', N'AF') is not null  
DROP Aggregate Concatenate;  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'StringUtils')  
DROP ASSEMBLY StringUtils;  
GO  
  
DECLARE @SamplePath nvarchar(1024)  
-- You will need to modify the value of the this variable if you have installed the sample someplace other than the default location.  
Set @SamplePath = 'C:\MySample\'  
CREATE ASSEMBLY [StringUtils]   
FROM @SamplePath + 'StringUtils.dll'  
WITH permission_set = Safe;  
GO  
  
CREATE AGGREGATE [dbo].[Concatenate](@input nvarchar(4000))  
RETURNS nvarchar(4000)  
EXTERNAL NAME [StringUtils].[Concatenate];  
GO  
  
CREATE FUNCTION [dbo].[Split](@input nvarchar(4000))   
RETURNS  TABLE(StringElement nvarchar(128) COLLATE Latin1_General_CI_AS)  
AS EXTERNAL NAME [StringUtils].[StringSplitter].[Split];  
GO  
  
CREATE FUNCTION [RegexMatches] (@input nvarchar(max), @pattern nvarchar(max))  
RETURNS TABLE(  
MatchID int,  
    MatchIndex int,  
    MatchValue nvarchar(4000),  
GroupID int,  
GroupIndex int,  
GroupValue nvarchar(4000),  
CaptureIndex int,  
CaptureValue nvarchar(4000))  
AS EXTERNAL NAME [StringUtils].[RegularExpression].[Matches];  
GO  
  
CREATE FUNCTION [RegexReplace] (@input nvarchar(max), @pattern nvarchar(max), @replacement nvarchar(max))  
RETURNS nvarchar(max)  
AS EXTERNAL NAME [StringUtils].[RegularExpression].[Replace]  
GO  
```  
  
 這是 `test.sql`，它會執行函數，藉以測試範例。  
  
```tsql  
USE AdventureWorks  
GO  
  
-- Invoke the tvf  
SELECT * FROM dbo.Split('will,this,work');  
GO  
  
-- Invoke the aggregate over the results of the tvf  
SELECT dbo.Concatenate(StringElement) FROM dbo.Split('will,this,also,work');  
GO  
  
-- Find two word pairs where the first word contains an 'r'  
SELECT MatchID, MatchIndex, MatchValue,   
  GroupID, GroupIndex, GroupValue,   
  CaptureIndex, CaptureValue  
FROM dbo.RegexMatches('The quick red fox jumped over the lazy brown dog', '(\w*r\w*)\s(\w+)');  
GO  
  
-- A variant of the above with no backtracking  
SELECT MatchID, MatchIndex, MatchValue,   
  GroupID, GroupIndex, GroupValue,   
  CaptureIndex, CaptureValue  
FROM dbo.RegexMatches('The quick red fox jumped over the lazy brown dog', '(?>\w*r\w*)\s(?>\w+)');  
GO  
  
-- Swap the subject of the sentence with the object of the sentence.  
SELECT dbo.RegexReplace('The quick red fox jumped over the lazy brown dog',   
'^The (?<fox>(?:[\w]+\s){3})jumped over the (?<dog>(?:[\w]+\s){2}(?:[\w]+))$',  
  
'The ${dog} jumped over the ${fox}');  
```  
  
 下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 會從資料庫中移除組件和函數。  
  
```  
USE AdventureWorks  
GO  
  
IF OBJECT_ID(N'RegexMatches', N'FT') is not null  
DROP Function RegexMatches;  
GO  
  
IF OBJECT_ID(N'Split', N'FT') is not null  
DROP Function Split;  
GO  
  
IF OBJECT_ID(N'RegexReplace', N'FS') is not null  
DROP Function RegexReplace;  
GO  
  
IF OBJECT_ID(N'Concatenate', N'AF') is not null  
DROP Aggregate Concatenate;  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'StringUtils')  
DROP ASSEMBLY StringUtils;  
  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [通用語言執行平台 &#40;CLR&#41; 整合的使用案例和範例](../../../2014/database-engine/dev-guide/usage-scenarios-and-examples-for-common-language-runtime-clr-integration.md)  
  
  
