---
title: 叫用 CLR 使用者定義彙總函式 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
dev_langs:
- TSQL
- VB
- CSharp
helpviewer_keywords:
- aggregate functions [CLR integration]
- invoking user-defined aggregate functions
- user-defined functions [CLR integration]
ms.assetid: 5a188b50-7170-4069-acad-5de5c915f65d
author: rothja
ms.author: jroth
ms.openlocfilehash: 81ddf552e71bdd0b83c8082c2bd84450f6088e5f
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84954669"
---
# <a name="invoking-clr-user-defined-aggregate-functions"></a>叫用 CLR 使用者定義彙總函式
  您可以在 [!INCLUDE[tsql](../../includes/tsql-md.md)] SELECT 陳述式中叫用 Common Language Runtime (CLR) 使用者定義彙總，依套用至系統彙總函式的所有規則而定。  
  
 適用下列其他規則：  
  
-   目前的使用者必須在使用者定義彙總上具有 `EXECUTE` 權限。  
  
-   使用者定義匯總必須使用*schema_name. udagg_name*格式的兩部分名稱來叫用。  
  
-   使用者定義匯總的引數類型必須符合或可以隱含地轉換成匯總的*input_type* ，如語句中所定義 `CREATE AGGREGATE` 。  
  
-   使用者定義匯總的傳回類型必須符合語句中的*return_type* `CREATE AGGREGATE` 。  
  
## <a name="example-1"></a>範例 1  
 以下是使用者定義彙總函式的範例，此函數會串連取自資料表之資料行的一組字串值：  
  
 [C#]  
  
```  
using System;  
using System.Data;  
using Microsoft.SqlServer.Server;  
using System.Data.SqlTypes;  
using System.IO;  
using System.Text;  
  
[Serializable]  
[SqlUserDefinedAggregate(  
    Format.UserDefined, //use clr serialization to serialize the intermediate result  
    IsInvariantToNulls = true, //optimizer property  
    IsInvariantToDuplicates = false, //optimizer property  
    IsInvariantToOrder = false, //optimizer property  
    MaxByteSize = 8000) //maximum size in bytes of persisted value  
]  
public class Concatenate : IBinarySerialize  
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
        this.intermediateResult = new StringBuilder();  
    }  
  
    /// <summary>  
    /// Accumulate the next value, not if the value is null  
    /// </summary>  
    /// <param name="value"></param>  
    public void Accumulate(SqlString value)  
    {  
        if (value.IsNull)  
        {  
            return;  
        }  
  
        this.intermediateResult.Append(value.Value).Append(',');  
    }  
  
    /// <summary>  
    /// Merge the partially computed aggregate with this aggregate.  
    /// </summary>  
    /// <param name="other"></param>  
    public void Merge(Concatenate other)  
    {  
        this.intermediateResult.Append(other.intermediateResult);  
    }  
  
    /// <summary>  
    /// Called at the end of aggregation, to return the results of the aggregation.  
    /// </summary>  
    /// <returns></returns>  
    public SqlString Terminate()  
    {  
        string output = string.Empty;  
        //delete the trailing comma, if any  
        if (this.intermediateResult != null  
            && this.intermediateResult.Length > 0)  
        {  
            output = this.intermediateResult.ToString(0, this.intermediateResult.Length - 1);  
        }  
  
        return new SqlString(output);  
    }  
  
    public void Read(BinaryReader r)  
    {  
        intermediateResult = new StringBuilder(r.ReadString());  
    }  
  
    public void Write(BinaryWriter w)  
    {  
        w.Write(this.intermediateResult.ToString());  
    }  
}  
```  
  
 [Visual Basic]  
  
```  
Imports System  
Imports System.Data  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlTypes  
Imports System.IO  
Imports System.Text  
  
<Serializable(), SqlUserDefinedAggregate(Format.UserDefined, IsInvariantToNulls:=True, IsInvariantToDuplicates:=False, IsInvariantToOrder:=False, MaxByteSize:=8000)> _  
Public Class Concatenate  
    Implements IBinarySerialize  
  
    ''' <summary>  
    ''' The variable that holds the intermediate result of the concatenation  
    ''' </summary>  
    Private intermediateResult As StringBuilder  
  
    ''' <summary>  
    ''' Initialize the internal data structures  
    ''' </summary>  
    Public Sub Init()  
        Me.intermediateResult = New StringBuilder()  
    End Sub  
  
    ''' <summary>  
    ''' Accumulate the next value, not if the value is null  
    ''' </summary>  
    ''' <param name="value"></param>  
    Public Sub Accumulate(ByVal value As SqlString)  
        If value.IsNull Then  
            Return  
        End If  
  
        Me.intermediateResult.Append(value.Value).Append(","c)  
    End Sub  
    ''' <summary>  
    ''' Merge the partially computed aggregate with this aggregate.  
    ''' </summary>  
    ''' <param name="other"></param>  
    Public Sub Merge(ByVal other As Concatenate)  
        Me.intermediateResult.Append(other.intermediateResult)  
    End Sub  
  
    ''' <summary>  
    ''' Called at the end of aggregation, to return the results of the aggregation.  
    ''' </summary>  
    ''' <returns></returns>  
    Public Function Terminate() As SqlString  
        Dim output As String = String.Empty  
  
        'delete the trailing comma, if any  
        If Not (Me.intermediateResult Is Nothing) AndAlso Me.intermediateResult.Length > 0 Then  
            output = Me.intermediateResult.ToString(0, Me.intermediateResult.Length - 1)  
        End If  
  
        Return New SqlString(output)  
    End Function  
  
    Public Sub Read(ByVal r As BinaryReader) Implements IBinarySerialize.Read  
        intermediateResult = New StringBuilder(r.ReadString())  
    End Sub  
  
    Public Sub Write(ByVal w As BinaryWriter) Implements IBinarySerialize.Write  
        w.Write(Me.intermediateResult.ToString())  
    End Sub  
End Class  
```  
  
 將程式碼編譯成**MyAgg.dll**之後，您就可以在中註冊匯總，如下所示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ：  
  
```  
CREATE ASSEMBLY MyAgg FROM 'C:\MyAgg.dll';  
GO  
CREATE AGGREGATE MyAgg (@input nvarchar(200)) RETURNS nvarchar(max)  
EXTERNAL NAME MyAgg.Concatenate;  
```  
  
> [!NOTE]  
>  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中不支援使用 /clr:pure 編譯器選項編譯的 Visual C++ 資料庫物件 (例如純量值函式) 執行。  
  
 與大部分的彙總相同，大部分的邏輯是位在 `Accumulate` 方法中。 此處當做參數而傳入 `Accumulate` 方法的字串會附加到以 `StringBuilder` 方法初始化的 `Init` 物件。 假設這不是初次呼叫 `Accumulate` 方法，則在附加傳入的字串之前，也會將逗號附加到 `StringBuilder`。 在計算工作結束時會呼叫 `Terminate` 方法，該方法則會將 `StringBuilder` 傳回為字串。  
  
 例如，請考慮具有下列結構描述的資料表：  
  
```  
CREATE TABLE BookAuthors  
(  
   BookID   int       NOT NULL,  
   AuthorName    nvarchar(200) NOT NULL  
);  
```  
  
 然後插入下列資料列：  
  
```  
INSERT BookAuthors VALUES(1, 'Johnson'),(2, 'Taylor'),(3, 'Steven'),(2, 'Mayler'),(3, 'Roberts'),(3, 'Michaels');  
```  
  
 接著下列查詢會產生下列結果：  
  
```  
SELECT BookID, dbo.MyAgg(AuthorName)  
FROM BookAuthors  
GROUP BY BookID;  
```  
  
|BookID|作者名稱|  
|------------|------------------|  
|1|Johnson|  
|2|Taylor, Mayler|  
|3|Roberts, Michaels, Steven|  
  
## <a name="example-2"></a>範例 2  
 下列範例示範在 `Accumulate` 方法上具有兩個參數的彙總：  
  
 [C#]  
  
```  
using System;  
using System.Data;  
using System.Data.SqlClient;  
using System.Data.SqlTypes;  
using Microsoft.SqlServer.Server;  
  
[Serializable]  
[SqlUserDefinedAggregate(  
    Format.Native,  
    IsInvariantToDuplicates = false,  
    IsInvariantToNulls = true,  
    IsInvariantToOrder = true,  
    IsNullIfEmpty = true,  
    Name = "WeightedAvg")]  
public struct WeightedAvg  
{  
    /// <summary>  
    /// The variable that holds the intermediate sum of all values multiplied by their weight  
    /// </summary>  
    private long sum;  
  
    /// <summary>  
    /// The variable that holds the intermediate sum of all weights  
    /// </summary>  
    private int count;  
  
    /// <summary>  
    /// Initialize the internal data structures  
    /// </summary>  
    public void Init()  
    {  
        sum = 0;  
        count = 0;  
    }  
  
    /// <summary>  
    /// Accumulate the next value, not if the value is null  
    /// </summary>  
    /// <param name="Value">Next value to be aggregated</param>  
    /// <param name="Weight">The weight of the value passed to Value parameter</param>  
    public void Accumulate(SqlInt32 Value, SqlInt32 Weight)  
    {  
        if (!Value.IsNull && !Weight.IsNull)  
        {  
            sum += (long)Value * (long)Weight;  
            count += (int)Weight;  
        }  
    }  
  
    /// <summary>  
    /// Merge the partially computed aggregate with this aggregate  
    /// </summary>  
    /// <param name="Group">The other partial results to be merged</param>  
    public void Merge(WeightedAvg Group)  
    {  
        sum += Group.sum;  
        count += Group.count;  
    }  
  
    /// <summary>  
    /// Called at the end of aggregation, to return the results of the aggregation.  
    /// </summary>  
    /// <returns>The weighted average of all inputed values</returns>  
    public SqlInt32 Terminate()  
    {  
        if (count > 0)  
        {  
            int value = (int)(sum / count);  
            return new SqlInt32(value);  
        }  
        else  
        {  
            return SqlInt32.Null;  
        }  
    }  
}  
```  
  
 [Visual Basic]  
  
```  
Imports System  
Imports System.Data  
Imports System.Data.SqlClient  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Runtime.InteropServices  
  
<StructLayout(LayoutKind.Sequential)> _  
<Serializable(), SqlUserDefinedAggregate(Format.Native, _  
IsInvariantToDuplicates:=False, _  
IsInvariantToNulls:=True, _  
IsInvariantToOrder:=True, _  
IsNullIfEmpty:=True, _  
Name:="WeightedAvg")> _  
Public Class WeightedAvg  
  
    ''' <summary>  
    ''' The variable that holds the intermediate sum of all values multiplied by their weight  
    ''' </summary>  
    Private sum As Long  
  
    ''' <summary>  
    ''' The variable that holds the intermediate sum of all weights  
    ''' </summary>  
    Private count As Integer  
  
    ''' <summary>  
    ''' The variable that holds the intermediate sum of all weights  
    ''' </summary>  
    Public Sub Init()  
        sum = 0  
        count = 0  
    End Sub  
  
    ''' <summary>  
    ''' Accumulate the next value, not if the value is null  
    ''' </summary>  
    ''' <param name="Value">Next value to be aggregated</param>  
    ''' <param name="Weight">The weight of the value passed to Value parameter</param>  
    Public Sub Accumulate(ByVal Value As SqlInt32, ByVal Weight As SqlInt32)  
        If Not Value.IsNull AndAlso Not Weight.IsNull Then  
            sum += CType(Value, Long) * CType(Weight, Long)  
            count += CType(Weight, Integer)  
        End If  
    End Sub  
  
    ''' <summary>  
    ''' Merge the partially computed aggregate with this aggregate.  
    ''' </summary>  
    ''' <param name="Group">The other partial results to be merged</param>  
    Public Sub Merge(ByVal Group As WeightedAvg)  
        sum = Group.sum  
        count = Group.count  
    End Sub  
  
    ''' <summary>  
    ''' Called at the end of aggregation, to return the results of the aggregation.  
    ''' </summary>  
    ''' <returns>The weighted average of all inputed values</returns>  
    Public Function Terminate() As SqlInt32  
        If count > 0 Then  
            ''                        int value = (int)(sum / count);  
            ''          return new SqlInt32(value);  
            Dim value As Integer = CType(sum / count, Integer)  
            Return New SqlInt32(value)  
        Else  
            Return SqlInt32.Null  
        End If  
    End Function  
End Class  
```  
  
 在編譯 C# 或 Visual Basic 原始程式碼之後，請執行下列 [!INCLUDE[tsql](../../includes/tsql-md.md)]。  此指令碼假設 DLL 稱為 WghtAvg.dll 且位於 C 磁碟機的根目錄。  此範例中也假設資料庫名稱為 test。  
  
```  
use test;  
go  
  
-- sp_configure 'clr enabled', 1;  
-- go  
  
--- RECONFIGURE WITH OVERRIDE;  
-- go  
  
IF EXISTS (SELECT name FROM systypes WHERE name = 'MyTableType')  
   DROP TYPE MyTableType;  
go  
  
IF EXISTS (SELECT name FROM sysobjects WHERE name = 'WeightedAvg')  
   DROP AGGREGATE WeightedAvg;  
go  
  
IF EXISTS (SELECT name FROM sys.assemblies WHERE name = 'MyClrCode')  
   DROP ASSEMBLY MyClrCode;  
go  
  
CREATE ASSEMBLY MyClrCode FROM 'C:\WghtAvg.dll';  
GO  
  
CREATE AGGREGATE WeightedAvg (@value int, @weight int) RETURNS int  
EXTERNAL NAME MyClrCode.WeightedAvg;  
go  
  
CREATE TYPE MyTableType AS table (ItemValue int, ItemWeight int);  
go  
  
DECLARE @myTable AS MyTableType;  
  
INSERT INTO @myTable VALUES(1, 4), (6, 1);  
  
SELECT dbo.WeightedAvg(ItemValue, ItemWeight) FROM @myTable;  
go  
```  
  
## <a name="see-also"></a>另請參閱  
 [CLR 使用者定義彙總](clr-user-defined-aggregates.md)  
  
  
