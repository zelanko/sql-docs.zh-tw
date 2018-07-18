---
title: 使用者定義型別撰寫程式碼 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: clr
ms.tgt_pltfrm: ''
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- validation [CLR integration]
- UDTs [CLR integration], coding
- UserDefined serialization format [CLR integration]
- Point UDT
- Parse method
- null values [CLR integration]
- ToString method
- ValidatePoint method
- attributes [CLR integration]
- coding user-defined types [CLR integration]
- Read method
- Write method
- nullability [CLR integration]
- user-defined types [CLR integration], coding
- Currency UDT
- validating UDT values
- exposing UDT properties [CLR integration]
ms.assetid: 1e5b43b3-4971-45ee-a591-3f535e2ac722
caps.latest.revision: 36
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 25560f82b1a697618dd606f7df8393abb74727c6
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37354420"
---
# <a name="coding-user-defined-types"></a>編碼使用者定義型別
  當您編碼使用者定義型別 (UDT) 定義時，您必須根據您是否將 UDT 實作為類別或結構以及您已選擇的格式和序列化選項來實作各種功能。  
  
 本章節的範例說明如何將 `Point` UDT 實作為 `struct` (或 Visual Basic 中的 `Structure`)。 `Point` UDT 是由實作為屬性程序的 X 及 Y 座標組成。  
  
 定義 UDT 時需要下列命名空間：  
  
```vb  
Imports System  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
```  
  
```csharp  
using System;  
using System.Data.SqlTypes;  
using Microsoft.SqlServer.Server;  
```  
  
 `Microsoft.SqlServer.Server` 命名空間包含 UDT 之各種屬性所需的物件，而 `System.Data.SqlTypes` 命名空間則包含表示組件可用之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 原生資料類型的類別。 若要能夠正確運作，您的組件還需要其他的命名空間。 `Point` UDT 也使用 `System.Text` 命名空間來處理字串。  
  
> [!NOTE]  
>  使用 `/clr:pure` 編譯的 Visual C++ 資料庫物件 (例如 UDT) 不支援執行。  
  
## <a name="specifying-attributes"></a>指定屬性  
 屬性會決定如何使用序列化來建構 UDT 的儲存表示，並將 UDT 以傳值方式傳輸到用戶端。  
  
 `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute` 是必要項目。 `Serializable` 屬性是選擇性的。 您還可指定 `Microsoft.SqlServer.Server.SqlFacetAttribute`，以提供 UDT 之傳回類型的相關資訊。 如需詳細資訊，請參閱 [CLR 常式的自訂屬性](../clr-integration/database-objects/clr-integration-custom-attributes-for-clr-routines.md)。  
  
### <a name="point-udt-attributes"></a>Point UDT 屬性  
 `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute` 會將 `Point` UDT 的儲存格式設定為 `Native`。 `IsByteOrdered` 會設為 `true`，可保證 SQL Server 中比較的結果，與在 Managed 程式碼中發生的比較相同。 UDT 會實作 `System.Data.SqlTypes.INullable` 介面，好讓 UDT 可感知 null。  
  
 下列程式碼片段顯示 `Point` UDT 的屬性。  
  
```vb  
<Serializable(), SqlUserDefinedTypeAttribute(Format.Native, _  
  IsByteOrdered:=True)> _  
  Public Structure Point  
    Implements INullable  
```  
  
```csharp  
[Serializable]  
[Microsoft.SqlServer.Server.SqlUserDefinedType(Format.Native,  
  IsByteOrdered=true)]  
public struct Point : INullable  
{  
```  
  
## <a name="implementing-nullability"></a>實作 Null 屬性  
 除了正確指定組件的屬性以外，UDT 還必須支援 Null 屬性。 載入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的 UDT 可感知 Null，但是為了讓 UDT 能夠辨識 Null 值，UDT 必須實作 `System.Data.SqlTypes.INullable` 介面。  
  
 您必須建立名為 `IsNull` 的屬性，需要此屬性來判斷在 CLR 程式碼內某值是否為 Null。 當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 找到 UDT 的 Null 執行個體時，便會使用正常的 Null 處理方法來保存 UDT。 除非必要，否則伺服器不會浪費時間來序列化或還原序列化 UDT，而且它也不會浪費空間來儲存 Null UDT。 每次從 CLR 引入 UDT 時都會執行 Null 檢查，這表示使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] IS NULL 建構來檢查 Null UDT 的作業一定都可運作。 伺服器也會使用 `IsNull` 屬性，以測試執行個體是否為 Null。 伺服器一旦判定 UDT 為 Null，就可以使用其原生的 Null 處理。  
  
 `get()` 的 `IsNull` 方法在任何情況下都不是特殊案例。 如果 `Point` 變數 `@p` 是 `Null`，則根據預設會將 `@p.IsNull` 評估為 "NULL"，而非 "1"。 這是因為 `SqlMethod(OnNullCall)` 方法的 `IsNull get()` 屬性預設為 false。 因為此物件是 `Null`，所以當要求此屬性時，不會還原序列化此物件、不會呼叫此方法，而且會傳回 "NULL" 的預設值。  
  
### <a name="example"></a>範例  
 在下列範例中，`is_Null` 變數為私用，而且會針對 UDT 執行個體保留 Null 狀態。 您的程式碼必須維護對 `is_Null` 適當的值。 UDT 也必須有一個名為 `Null` 的靜態屬性，它會傳回 UDT 的 Null 值執行個體。 如果執行個體在資料庫中實際上為 Null，這可讓 UDT 傳回 Null 值。  
  
```vb  
Private is_Null As Boolean  
  
Public ReadOnly Property IsNull() As Boolean _  
   Implements INullable.IsNull  
    Get  
        Return (is_Null)  
    End Get  
End Property  
  
Public Shared ReadOnly Property Null() As Point  
    Get  
        Dim pt As New Point  
        pt.is_Null = True  
        Return (pt)  
    End Get  
End Property  
```  
  
```csharp  
private bool is_Null;  
  
public bool IsNull  
{  
    get  
    {  
        return (is_Null);  
    }  
}  
  
public static Point Null  
{  
    get  
    {  
        Point pt = new Point();  
        pt.is_Null = true;  
        return pt;  
    }  
}  
```  
  
### <a name="is-null-vs-isnull"></a>IS NULL 與IsNull  
 假設有一個資料表包含 Points(id int, location Point) 結構描述 (其中 `Point` 為 CLR UDT) 及下列查詢：  
  
```  
--Query 1  
SELECT ID  
FROM Points  
WHERE NOT (location IS NULL) -- Or, WHERE location IS NOT NULL;  
```  
  
```  
--Query 2:  
SELECT ID  
FROM Points  
WHERE location.IsNull = 0;  
```  
  
 這兩個查詢都會傳回非 `Null` 位置之點的識別碼。 查詢 1 會使用正常 null 處理，而且不需要還原序列化 UDT。 另一方面，查詢 2 則必須還原序列化每一個非 `Null` 物件及呼叫 CLR，以取得 `IsNull` 屬性的值。 我們可以清楚地看到，使用 `IS NULL` 將會呈現較佳的效能，因此絕對沒有理由要從 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式碼讀取 UDT 的 `IsNull` 屬性。  
  
 這樣為什麼要使用 `IsNull` 屬性呢？ 首先，需要用它來判斷來自 CLR 程式碼的某個值是否為 `Null`。 第二，伺服器需要一個方法來測試執行個體是否為 `Null`，所以伺服器會使用這個屬性。 當判斷出這個屬性為 `Null` 之後，它就可以使用它的原生 null 處理來加以處理。  
  
## <a name="implementing-the-parse-method"></a>實作 Parse 方法  
 `Parse` 及 `ToString` 方法允許與 UDT 的字串表示之間進行來回轉換。 `Parse` 方法允許將字串轉換成 UDT。 它必須宣告為 `static` (或 Visual Basic 中的 `Shared`)，並採用型別 `System.Data.SqlTypes.SqlString` 的參數。  
  
 下列程式碼會實作 `Parse` UDT 的 `Point` 方法，這樣會分隔 X 和 Y 座標。 `Parse` 方法具有 `System.Data.SqlTypes.SqlString` 類型的單一引數，而且假設會以逗號分隔的字串來提供 X 和 Y 值。 將 `Microsoft.SqlServer.Server.SqlMethodAttribute.OnNullCall` 屬性設定為 `false` 會避免從 Point 的 Null 執行個體呼叫 `Parse` 方法。  
  
```vb  
<SqlMethod(OnNullCall:=False)> _  
Public Shared Function Parse(ByVal s As SqlString) As Point  
    If s.IsNull Then  
        Return Null  
    End If  
  
    ' Parse input string here to separate out points.  
    Dim pt As New Point()  
    Dim xy() As String = s.Value.Split(",".ToCharArray())  
    pt.X = Int32.Parse(xy(0))  
    pt.Y = Int32.Parse(xy(1))  
    Return pt  
End Function  
```  
  
```csharp  
[SqlMethod(OnNullCall = false)]  
public static Point Parse(SqlString s)  
{  
    if (s.IsNull)  
        return Null;  
  
    // Parse input string to separate out points.  
    Point pt = new Point();  
    string[] xy = s.Value.Split(",".ToCharArray());  
    pt.X = Int32.Parse(xy[0]);  
    pt.Y = Int32.Parse(xy[1]);  
    return pt;  
}  
```  
  
## <a name="implementing-the-tostring-method"></a>實作 ToString 方法  
 `ToString` 方法會將 `Point` UDT 轉換成字串值。 在此情況下，會針對 `Point` 類型的 Null 執行個體傳回 "NULL" 字串。 `ToString` 方法藉由使用 `Parse` 傳回以逗號分隔並包含 X 及 Y 座標值的 `System.Text.StringBuilder`，以反轉 `System.String` 方法。 因為**InvokeIfReceiverIsNull**預設值為 false，則為 null 的執行個體的核取`Point`並非必要。  
  
```vb  
Private _x As Int32  
Private _y As Int32  
  
Public Overrides Function ToString() As String  
    If Me.IsNull Then  
        Return "NULL"  
    Else  
        Dim builder As StringBuilder = New StringBuilder  
        builder.Append(_x)  
        builder.Append(",")  
        builder.Append(_y)  
        Return builder.ToString  
    End If  
End Function  
```  
  
```csharp  
private Int32 _x;  
private Int32 _y;  
  
public override string ToString()  
{  
    if (this.IsNull)  
        return "NULL";  
    else  
    {  
        StringBuilder builder = new StringBuilder();  
        builder.Append(_x);  
        builder.Append(",");  
        builder.Append(_y);  
        return builder.ToString();  
    }  
}  
```  
  
## <a name="exposing-udt-properties"></a>公開 UDT 屬性  
 `Point` UDT 會公開實作為 `System.Int32` 類型之公用讀寫屬性的 X 及 Y 座標。  
  
```vb  
Public Property X() As Int32  
    Get  
        Return (Me._x)  
    End Get  
  
    Set(ByVal Value As Int32)  
        _x = Value  
    End Set  
End Property  
  
Public Property Y() As Int32  
    Get  
        Return (Me._y)  
    End Get  
  
    Set(ByVal Value As Int32)  
        _y = Value  
    End Set  
End Property  
```  
  
```csharp  
public Int32 X  
{  
    get  
    {  
        return this._x;  
    }  
    set   
    {  
        _x = value;  
    }  
}  
  
public Int32 Y  
{  
    get  
    {  
        return this._y;  
    }  
    set  
    {  
        _y = value;  
    }  
}  
```  
  
## <a name="validating-udt-values"></a>驗證 UDT 值  
 當使用 UDT 資料時，[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 會自動將二進位值轉換成 UDT 值。 此轉換程序包括檢查適用於此類型之序列化格式的值，並確保可正確地將此值還原序列化。 這可確保，值可以轉換回二進位格式。 如果是依照位元組排序的 UDT，這也可確保產生的二進位值會符合原始二進位值。 如此可防止在資料庫中保留無效的值。 在某些情況下，這個層級的檢查可能不夠。 當要求 UDT 值位於預期的網域或範圍內時，可能需要其他驗證。 例如，實作日期的 UDT 可能會要求日期值是一個正數，而且在某個有效值的範圍內。  
  
 `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute.ValidationMethodName` 的 `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute` 屬性可在將資料指派給 UDT 或轉換成 UDT 時，讓您提供伺服器所執行之驗證方法的名稱。 在執行 bcp 公用程式、BULK INSERT、DBCC CHECKDB、DBCC CHECKFILEGROUP、DBCC CHECKTABLE、分散式查詢及表格式資料流 (TDS) 遠端程序呼叫 (RPC) 作業期間，也會呼叫 `ValidationMethodName`。 `ValidationMethodName` 的預設值是 null，表示沒有驗證方法。  
  
### <a name="example"></a>範例  
 下列程式碼片段顯示 `Point` 類別的宣告，該類別會指定 `ValidationMethodName` 的 `ValidatePoint`。  
  
```vb  
<Serializable(), SqlUserDefinedTypeAttribute(Format.Native, _  
  IsByteOrdered:=True, _  
  ValidationMethodName:="ValidatePoint")> _  
  Public Structure Point  
```  
  
```csharp  
[Serializable]  
[Microsoft.SqlServer.Server.SqlUserDefinedType(Format.Native,  
  IsByteOrdered=true,   
  ValidationMethodName = "ValidatePoint")]  
public struct Point : INullable  
{  
```  
  
 如果已指定驗證方法，它必須具有類似以下程式碼片段的簽章。  
  
```vb  
Private Function ValidationFunction() As Boolean  
    If (validation logic here) Then  
        Return True  
    Else  
        Return False  
    End If  
End Function  
```  
  
```csharp  
private bool ValidationFunction()  
{  
    if (validation logic here)  
    {  
        return true;  
    }  
    else  
    {  
        return false;  
    }  
}  
```  
  
 此驗證方法可以有任何範圍，而且應該在值為有效時傳回 `true`，否則會傳回 `false`。 如果此方法傳回 `false` 或擲回例外狀況，則該值會被視為無效，並引發錯誤。  
  
 在以下範例中，程式碼只允許零值或大於 X 及 Y 座標的值。  
  
```vb  
Private Function ValidatePoint() As Boolean  
    If (_x >= 0) And (_y >= 0) Then  
        Return True  
    Else  
        Return False  
    End If  
End Function  
```  
  
```csharp  
private bool ValidatePoint()  
{  
    if ((_x >= 0) && (_y >= 0))  
    {  
        return true;  
    }  
    else  
    {  
        return false;  
    }  
}  
```  
  
### <a name="validation-method-limitations"></a>驗證方法限制  
 伺服器呼叫此驗證方法的時機是當伺服器執行轉換時，而不是當藉由設定個別屬性插入資料，或使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] INSERT 陳述式插入資料時。  
  
 您必須明確呼叫驗證方法從屬性 setter 和`Parse`方法，如果您想要在所有情況下執行的驗證方法。 這不是硬性規定，在某些情況下可能也不適當。  
  
### <a name="parse-validation-example"></a>Parse 驗證範例  
 若要確保`ValidatePoint`方法中叫用`Point`類別，您必須呼叫從`Parse`方法和屬性程序，設定 X 和 Y 座標值。 下列程式碼片段示範如何呼叫`ValidatePoint`驗證方法，從`Parse`函式。  
  
```vb  
<SqlMethod(OnNullCall:=False)> _  
Public Shared Function Parse(ByVal s As SqlString) As Point  
    If s.IsNull Then  
        Return Null  
    End If  
  
    ' Parse input string here to separate out points.  
    Dim pt As New Point()  
    Dim xy() As String = s.Value.Split(",".ToCharArray())  
    pt.X = Int32.Parse(xy(0))  
    pt.Y = Int32.Parse(xy(1))  
  
    ' Call ValidatePoint to enforce validation  
    ' for string conversions.  
    If Not pt.ValidatePoint() Then  
        Throw New ArgumentException("Invalid XY coordinate values.")  
    End If  
    Return pt  
End Function  
```  
  
```csharp  
[SqlMethod(OnNullCall = false)]  
public static Point Parse(SqlString s)  
{  
    if (s.IsNull)  
        return Null;  
  
    // Parse input string to separate out points.  
    Point pt = new Point();  
    string[] xy = s.Value.Split(",".ToCharArray());  
    pt.X = Int32.Parse(xy[0]);  
    pt.Y = Int32.Parse(xy[1]);  
  
    // Call ValidatePoint to enforce validation  
    // for string conversions.  
    if (!pt.ValidatePoint())   
        throw new ArgumentException("Invalid XY coordinate values.");  
    return pt;  
}  
```  
  
### <a name="property-validation-example"></a>Property 驗證範例  
 下列程式碼片段示範如何呼叫`ValidatePoint`從設定 X 和 Y 座標屬性程序的驗證方法。  
  
```vb  
Public Property X() As Int32  
    Get  
        Return (Me._x)  
    End Get  
  
    Set(ByVal Value As Int32)  
        Dim temp As Int32 = _x  
        _x = Value  
        If Not ValidatePoint() Then  
            _x = temp  
            Throw New ArgumentException("Invalid X coordinate value.")  
        End If  
    End Set  
End Property  
  
Public Property Y() As Int32  
    Get  
        Return (Me._y)  
    End Get  
  
    Set(ByVal Value As Int32)  
        Dim temp As Int32 = _y  
        _y = Value  
        If Not ValidatePoint() Then  
            _y = temp  
            Throw New ArgumentException("Invalid Y coordinate value.")  
        End If  
    End Set  
End Property  
```  
  
```csharp  
    public Int32 X  
{  
    get  
    {  
        return this._x;  
    }  
    // Call ValidatePoint to ensure valid range of Point values.  
    set   
    {  
        Int32 temp = _x;  
        _x = value;  
        if (!ValidatePoint())  
        {  
            _x = temp;  
            throw new ArgumentException("Invalid X coordinate value.");  
        }  
    }  
}  
  
public Int32 Y  
{  
    get  
    {  
        return this._y;  
    }  
    set  
    {  
        Int32 temp = _y;  
        _y = value;  
        if (!ValidatePoint())  
        {  
            _y = temp;  
            throw new ArgumentException("Invalid Y coordinate value.");  
        }  
    }  
}  
```  
  
## <a name="coding-udt-methods"></a>編碼 UDT 方法  
 當編碼 UDT 方法時，請考慮使用的演算法是否可能隨著時間而改變。 如果會的話，您可能會想要考慮針對 UDT 使用的方法建立個別類別。 如果演算法變更，您可在不影響 UDT 的情況下，以新的程式碼重新編譯該類別，並將組件載入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 在許多情況下，您可使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] ALTER ASSEMBLY 陳述式重新載入 UDT，但是這樣做可能會導致現有資料發生問題。 例如， `Currency` UDT 隨附**AdventureWorks**範例資料庫會使用**ConvertCurrency**函數來轉換貨幣值，在個別的類別實作。 轉換演算法在未來有可能以非預期的方式變更，或者可能需要新的功能。 區隔**ConvertCurrency**函式`Currency`UDT 實作規劃未來的變更時，提供更大的彈性。  
  
### <a name="example"></a>範例  
 `Point`類別包含三個簡單的方法，來計算距離：**距離**， **DistanceFrom**並**DistanceFromXY**。 每一個方法都會傳回 `double`，計算從 `Point` 到零的距離、從指定點到 `Point` 的距離，以及從指定之 X 及 Y 座標到 `Point` 的距離。 **距離**並**DistanceFrom**每個呼叫**DistanceFromXY**，並示範如何使用不同的引數，每個方法。  
  
```vb  
' Distance from 0 to Point.  
<SqlMethod(OnNullCall:=False)> _  
Public Function Distance() As Double  
    Return DistanceFromXY(0, 0)  
End Function  
  
' Distance from Point to the specified point.  
<SqlMethod(OnNullCall:=False)> _  
Public Function DistanceFrom(ByVal pFrom As Point) As Double  
    Return DistanceFromXY(pFrom.X, pFrom.Y)  
End Function  
  
' Distance from Point to the specified x and y values.  
<SqlMethod(OnNullCall:=False)> _  
Public Function DistanceFromXY(ByVal ix As Int32, ByVal iy As Int32) _  
    As Double  
    Return Math.Sqrt(Math.Pow(ix - _x, 2.0) + Math.Pow(iy - _y, 2.0))  
End Function  
```  
  
```csharp  
// Distance from 0 to Point.  
[SqlMethod(OnNullCall = false)]  
public Double Distance()  
{  
    return DistanceFromXY(0, 0);  
}  
  
// Distance from Point to the specified point.  
[SqlMethod(OnNullCall = false)]  
public Double DistanceFrom(Point pFrom)  
{  
    return DistanceFromXY(pFrom.X, pFrom.Y);  
}  
  
// Distance from Point to the specified x and y values.  
[SqlMethod(OnNullCall = false)]  
public Double DistanceFromXY(Int32 iX, Int32 iY)  
{  
    return Math.Sqrt(Math.Pow(iX - _x, 2.0) + Math.Pow(iY - _y, 2.0));  
}  
```  
  
### <a name="using-sqlmethod-attributes"></a>使用 SqlMethod 屬性  
 `Microsoft.SqlServer.Server.SqlMethodAttribute` 類別會提供可用來標示方法定義的自訂屬性，以便針對 Null 呼叫行為指定決定性以及指定方法是否為 mutator。 已假設這些屬性 (Property) 的預設值，而且只有在需要非預設值時才會使用自訂屬性 (Attribute)。  
  
> [!NOTE]  
>  `SqlMethodAttribute` 類別繼承自 `SqlFunctionAttribute` 類別，因此 `SqlMethodAttribute` 會繼承自 `FillRowMethodName` 而 `TableDefinition` 欄位會繼承自 `SqlFunctionAttribute`。 這意味著撰寫資料表值方法是可行的，不過情況不是這樣。 方法會進行編譯和組件進行部署，但是發生錯誤的相關`IEnumerable`傳回型別就會引發在執行階段，並出現下列訊息: 「 方法、 屬性或欄位 '\<名稱 >' 中類別\<類別 >' 的組件中'\<組件 >' 有無效的傳回類型。 」  
  
 下表說明可在 UDT 方法中使用的部分相關 `Microsoft.SqlServer.Server.SqlMethodAttribute` 屬性，並列出其預設值。  
  
 DataAccess  
 指出此函數是否包含對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 本機執行個體中儲存之使用者資料的存取權。 預設值是 `DataAccessKind`.`None`。  
  
 IsDeterministic  
 指出如果輸入值及資料庫狀態都相同，此函數是否會產生相同的輸出值。 預設值是 `false`。  
  
 IsMutator  
 指出此方法是否會導致 UDT 執行個體的狀態變更。 預設值是 `false`。  
  
 IsPrecise  
 指出此函數是否包含不精確的計算，如浮點運算。 預設值是 `false`。  
  
 OnNullCall  
 指出當指定 Null 參考輸入引數時，是否呼叫此方法。 預設值是 `true`。  
  
### <a name="example"></a>範例  
 `Microsoft.SqlServer.Server.SqlMethodAttribute.IsMutator` 屬性可讓您將方法標示為允許 UDT 執行個體的狀態變更。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 不允許您在一個 UPDATE 陳述式的 SET 子句中，設定兩個 UDT 屬性。 但是，您可以將方法標示為 mutator，這樣會變更兩個成員。  
  
> [!NOTE]  
>  查詢中不允許使用 Mutator 方法。 它們只能在指派陳述式或資料修改陳述式中呼叫。 如果標示為 mutator 的方法未傳回 `void` (或是 Visual Basic 中的 `Sub`)，CREATE TYPE 會失敗且發生錯誤。  
  
 下列陳述式假設存在著具有 `Triangles` 方法的 `Rotate` UDT。 下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] UPDATE 陳述式會叫用 `Rotate` 方法：  
  
```  
UPDATE Triangles SET t.RotateY(0.6) WHERE id=5  
```  
  
 `Rotate` 方法是以將 `SqlMethod` 設為 `IsMutator` 的 `true` 屬性來裝飾的，以便 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以將方法標示為 Mutator 方法。 該程式碼還將 `OnNullCall` 設為 `false`，如此可向伺服器指出，如果任何輸入參數為 Null 參考，則該方法會傳回 Null 參考 (Visual Basic 中則為 `Nothing`)。  
  
```vb  
<SqlMethod(IsMutator:=True, OnNullCall:=False)> _  
Public Sub Rotate(ByVal anglex as Double, _  
  ByVal angley as Double, ByVal anglez As Double)   
   RotateX(anglex)  
   RotateY(angley)  
   RotateZ(anglez)  
End Sub  
```  
  
```csharp  
[SqlMethod(IsMutator = true, OnNullCall = false)]  
public void Rotate(double anglex, double angley, double anglez)   
{  
   RotateX(anglex);  
   RotateY(angley);  
   RotateZ(anglez);  
}  
```  
  
## <a name="implementing-a-udt-with-a-user-defined-format"></a>以使用者定義的格式實作 UDT  
 以使用者定義的格式實作 UDT 時，您必須實作可將 Microsoft.SqlServer.Server.IBinarySerialize 介面實作為處理序列化及還原序列化 UDT 資料的 `Read` 及 `Write` 方法。 您也必須指定 `MaxByteSize` 的 `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute` 屬性。  
  
### <a name="the-currency-udt"></a>Currency UDT  
 `Currency` UDT 隨附在 CLR 範例中，這些範例從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 開始就可以與 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 一起安裝。  
  
 `Currency` UDT 支援在特定文化特性的貨幣系統中處理貨幣金額。 您必須定義兩個欄位：針對 `string` 定義 `CultureInfo` (指定發行貨幣的一方，例如 en-us)，以及針對 `decimal` 定義 `CurrencyValue` (貨幣金額)。  
  
 雖然伺服器不會用它來執行比較，但是 `Currency` UDT 會實作 `System.IComparable` 介面，而此介面會公開單一方法 `System.IComparable.CompareTo`。 這會在用戶端上使用，此時需要正確地比較或排序文化特性中的貨幣值。  
  
 在 CLR 上執行的程式碼會對貨幣值與文化特性分別進行比較。 如果是 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式碼，下列動作會決定比較：  
  
1.  將 `IsByteOrdered` 屬性設為 True，告知 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用磁碟上保存的二進位表示進行比較。  
  
2.  針對 `Write` UDT 使用 `Currency` 方法，以判斷如何在磁碟上保存 UDT，以及如何針對 [!INCLUDE[tsql](../../includes/tsql-md.md)] 作業來比較及排序 UDT 值。  
  
3.  使用下列二進位格式，儲存 `Currency` UDT：  
  
    1.  針對位元組 0-19 將文化特性儲存為 UTF-16 編碼的字串，並使用 null 字元填補到右邊。  
  
    2.  使用位元組 20 以上 (含) 來包含貨幣的十進位值。  
  
 填補的目的是確保文化特性與貨幣值完全分開，以便在將 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式碼中的一個 UDT 與另一 UDT 進行比較時，會將文化特性位元組與文化特性位元組進行比較，並將貨幣位元組值與貨幣位元組值進行比較。  
  
 針對完整的程式碼清單`Currency`UDT 中的指示，說明如何安裝 CLR 範例的後續[SQL Server Database Engine 範例](http://msftengprodsamples.codeplex.com/)。  
  
### <a name="currency-attributes"></a>Currency 屬性  
 使用下列屬性定義 `Currency` UDT。  
  
```vb  
<Serializable(), Microsoft.SqlServer.Server.SqlUserDefinedType( _  
    Microsoft.SqlServer.Server.Format.UserDefined, _  
    IsByteOrdered:=True, MaxByteSize:=32), _  
    CLSCompliant(False)> _  
Public Structure Currency  
Implements INullable, IComparable, _  
Microsoft.SqlServer.Server.IBinarySerialize  
```  
  
```csharp  
[Serializable]  
[SqlUserDefinedType(Format.UserDefined,   
    IsByteOrdered = true, MaxByteSize = 32)]  
    [CLSCompliant(false)]  
    public struct Currency : INullable, IComparable, IBinarySerialize  
    {  
```  
  
## <a name="creating-read-and-write-methods-with-ibinaryserialize"></a>使用 IBinarySerialize 建立 Read 和 Write 方法  
 當您選擇 `UserDefined` 序列化格式時，您也必須實作 `IBinarySerialize` 介面，並建立您自己的 `Read` 和 `Write` 方法。 下列來自 `Currency` UDT 的程序會使用 `System.IO.BinaryReader` 和 `System.IO.BinaryWriter`，從 UDT 讀取並寫入 UDT。  
  
```vb  
' IBinarySerialize methods  
' The binary layout is as follow:  
'    Bytes 0 - 19: Culture name, padded to the right with null  
'    characters, UTF-16 encoded  
'    Bytes 20+: Decimal value of money  
' If the culture name is empty, the currency is null.  
Public Sub Write(ByVal w As System.IO.BinaryWriter) _  
  Implements Microsoft.SqlServer.Server.IBinarySerialize.Write  
    If Me.IsNull Then  
        w.Write(nullMarker)  
        w.Write(System.Convert.ToDecimal(0))  
        Return  
    End If  
  
    If cultureName.Length > cultureNameMaxSize Then  
        Throw New ApplicationException(String.Format(CultureInfo.CurrentUICulture, _  
           "{0} is an invalid culture name for currency as it is too long.", cultureNameMaxSize))  
    End If  
  
    Dim paddedName As String = cultureName.PadRight(cultureNameMaxSize, CChar(vbNullChar))  
  
    For i As Integer = 0 To cultureNameMaxSize - 1  
        w.Write(paddedName(i))  
    Next i  
  
    ' Normalize decimal value to two places  
    currencyVal = Decimal.Floor(currencyVal * 100) / 100  
    w.Write(currencyVal)  
End Sub  
  
Public Sub Read(ByVal r As System.IO.BinaryReader) _  
  Implements Microsoft.SqlServer.Server.IBinarySerialize.Read  
    Dim name As Char() = r.ReadChars(cultureNameMaxSize)  
    Dim stringEnd As Integer = Array.IndexOf(name, CChar(vbNullChar))  
  
    If stringEnd = 0 Then  
        cultureName = Nothing  
        Return  
    End If  
  
    cultureName = New String(name, 0, stringEnd)  
    currencyVal = r.ReadDecimal()  
End Sub  
  
```  
  
```csharp  
// IBinarySerialize methods  
// The binary layout is as follow:  
//    Bytes 0 - 19:Culture name, padded to the right   
//    with null characters, UTF-16 encoded  
//    Bytes 20+:Decimal value of money  
// If the culture name is empty, the currency is null.  
public void Write(System.IO.BinaryWriter w)  
{  
    if (this.IsNull)  
    {  
        w.Write(nullMarker);  
        w.Write((decimal)0);  
        return;  
    }  
  
    if (cultureName.Length > cultureNameMaxSize)  
    {  
        throw new ApplicationException(string.Format(  
            CultureInfo.InvariantCulture,   
            "{0} is an invalid culture name for currency as it is too long.",   
            cultureNameMaxSize));  
    }  
  
    String paddedName = cultureName.PadRight(cultureNameMaxSize, '\0');  
    for (int i = 0; i < cultureNameMaxSize; i++)  
    {  
        w.Write(paddedName[i]);  
    }  
  
    // Normalize decimal value to two places  
    currencyValue = Decimal.Floor(currencyValue * 100) / 100;  
    w.Write(currencyValue);  
}  
public void Read(System.IO.BinaryReader r)  
{  
    char[] name = r.ReadChars(cultureNameMaxSize);  
    int stringEnd = Array.IndexOf(name, '\0');  
  
    if (stringEnd == 0)  
    {  
        cultureName = null;  
        return;  
    }  
  
    cultureName = new String(name, 0, stringEnd);  
    currencyValue = r.ReadDecimal();  
}  
```  
  
 針對完整的程式碼清單`Currency`UDT，請參閱 < [SQL Server Database Engine 範例](http://msftengprodsamples.codeplex.com/)。  
  
## <a name="see-also"></a>另請參閱  
 [建立使用者定義型別](creating-user-defined-types.md)  
  
  
