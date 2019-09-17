---
title: 撰寫使用者定義類型的程式碼 |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
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
author: rothja
ms.author: jroth
ms.openlocfilehash: e94662043d3801cc7088533d7f0fbadd638bec5b
ms.sourcegitcommit: f76b4e96c03ce78d94520e898faa9170463fdf4f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/10/2019
ms.locfileid: "70874809"
---
# <a name="creating-user-defined-types---coding"></a>建立使用者定義型別 - 編碼
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  當您編碼使用者定義型別 (UDT) 定義時，您必須根據您是否將 UDT 實作為類別或結構以及您已選擇的格式和序列化選項來實作各種功能。  
  
 本節中的範例說明如何將**Point** UDT 實作為**結構**（或 Visual Basic 中的**結構**）。 **Point** UDT 是由實作為屬性程式的 X 和 Y 座標所組成。  
  
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
  
 SqlTypes**命名空間包含**UDT 的各種屬性所需的物件，而**system.object**則包含代表[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可供使用之原生資料類型的類別。assembly. 若要能夠正確運作，您的組件還需要其他的命名空間。 **Point** UDT 也會使用**system.web**命名空間來處理字串。  
  
> [!NOTE]  
>  不C++支援執行以 **/clr： pure**編譯的 Visual 資料庫物件（例如 udt）。  
  
## <a name="specifying-attributes"></a>指定屬性  
 屬性會決定如何使用序列化來建構 UDT 的儲存表示，並將 UDT 以傳值方式傳輸到用戶端。  
  
 **SqlUserDefinedTypeAttribute**是必要的。 **Serializable**屬性是選擇性的。 您也可以指定**SqlFacetAttribute**來提供 UDT 之傳回類型的相關資訊。 如需詳細資訊，請參閱 [CLR 常式的自訂屬性](../../relational-databases/clr-integration/database-objects/clr-integration-custom-attributes-for-clr-routines.md)。  
  
### <a name="point-udt-attributes"></a>Point UDT 屬性  
 **SqlUserDefinedTypeAttribute**會將**Point** UDT 的儲存格式設定為**原生**。 **IsByteOrdered**會設定為**true**，以確保在 SQL Server 中的比較結果會相同，如同在 managed 程式碼中發生相同的比較。 UDT 會執行**SqlTypes. INullable**介面，讓 udt 變成 null 感知。  
  
 下列程式碼片段顯示**Point** UDT 的屬性。  
  
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
 除了正確指定組件的屬性以外，UDT 還必須支援 Null 屬性。 載入至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的 udt 可感知 null，但為了讓 udt 能夠辨識 null 值，udt 必須執行**SqlTypes. INullable**介面。  
  
 您必須建立名為**IsNull**的屬性，這是用來判斷 CLR 程式碼中的值是否為 null 的必要內容。 當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 找到 UDT 的 Null 執行個體時，便會使用正常的 Null 處理方法來保存 UDT。 除非必要，否則伺服器不會浪費時間來序列化或還原序列化 UDT，而且它也不會浪費空間來儲存 Null UDT。 每次從 CLR 引入 UDT 時都會執行 Null 檢查，這表示使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] IS NULL 建構來檢查 Null UDT 的作業一定都可運作。 伺服器也會使用**IsNull**屬性來測試實例是否為 null。 伺服器一旦判定 UDT 為 Null，就可以使用其原生的 Null 處理。  
  
 **IsNull**的**get （）** 方法不是以任何方式進行特殊大小寫。 如果**Point**變數 **\@p**是**Null**，則 **\@p. IsNull**預設會評估為 "Null"，而不是 "1"。 這是因為**IsNull get （）** 方法的**SqlMethod （OnNullCall）** 屬性預設為 false。 因為物件是**Null**，所以當要求屬性時，物件不會還原序列化，也不會呼叫方法，而且會傳回預設值 "Null"。  
  
### <a name="example"></a>範例  
 在下列範例中，`is_Null` 變數為私用，而且會針對 UDT 執行個體保留 Null 狀態。 您的程式碼必須維護對 `is_Null` 適當的值。 UDT 也必須有一個名為**Null**的靜態屬性，它會傳回 UDT 的 Null 值實例。 如果執行個體在資料庫中實際上為 Null，這可讓 UDT 傳回 Null 值。  
  
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
  
### <a name="is-null-vs-isnull"></a>為 Null 與IsNull  
 假設有一個包含架構點（識別碼 int，location Point）的資料表，其中**Point**是 CLR UDT，而下列查詢：  
  
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
  
 這兩個查詢都會傳回具有非**Null**位置之點的識別碼。 查詢 1 會使用正常 null 處理，而且不需要還原序列化 UDT。 另一方面，查詢2必須將每個非**Null**物件還原序列化，並呼叫 CLR 以取得**IsNull**屬性的值。 很明顯地，使用**IS Null**會展現更好的效能，而且永遠不會有理由從[!INCLUDE[tsql](../../includes/tsql-md.md)]程式碼讀取 UDT 的 IsNull 屬性。  
  
 那麼， **IsNull**屬性的用途為何？ 首先，需要從 CLR 程式碼中判斷值是否為**Null** 。 第二，伺服器需要一個方法來測試實例是否為**Null**，因此伺服器會使用這個屬性。 在判斷它是**Null**之後，它可以使用其原生的 Null 處理來處理它。  
  
## <a name="implementing-the-parse-method"></a>實作 Parse 方法  
 **Parse**和**ToString**方法允許從 UDT 的字串表示來回轉換。 **Parse**方法可讓字串轉換成 UDT。 它必須宣告為**靜態**（或在 Visual Basic 中**共用**），並採用**SqlTypes. SqlString**類型的參數。  
  
 下列程式碼會針對**Point** UDT 執行**Parse**方法，以分隔 X 和 Y 座標。 **Parse**方法具有**SqlTypes. SqlString**類型的單一引數，並假設 X 和 Y 值是以逗號分隔字串的形式提供。 將**SqlMethodAttribute. OnNullCall**屬性設定為**false** ，可防止從 Point 的 null 實例呼叫**Parse**方法。  
  
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
 **ToString**方法會將**Point** UDT 轉換成字串值。 在此情況下，會針對**Point**類型的 Null 實例傳回字串 "Null"。 **ToString**方法會使用**system.object**來傳回由 X 和 Y 座標值組成的逗號分隔**system.string** ，以反轉**Parse**方法。 因為**InvokeIfReceiverIsNull**預設為 false，所以不需要檢查**點**的 null 實例。  
  
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
 **Point** UDT 會公開 X 和 Y 座標，實作為類型**system.object**的公用讀寫屬性。  
  
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
 當使用 UDT 資料時，[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 會自動將二進位值轉換成 UDT 值。 此轉換程序包括檢查適用於此類型之序列化格式的值，並確保可正確地將此值還原序列化。 這可確保此值可以轉換回二進位格式。 如果是依照位元組排序的 UDT，這也可確保產生的二進位值會符合原始二進位值。 如此可防止在資料庫中保留無效的值。 在某些情況下，這個層級的檢查可能不夠。 當要求 UDT 值位於預期的網域或範圍內時，可能需要其他驗證。 例如，實作日期的 UDT 可能會要求日期值是一個正數，而且在某個有效值的範圍內。  
  
 **SqlUserDefinedTypeAttribute**的**SqlUserDefinedTypeAttribute**屬性，可讓您提供伺服器執行之驗證方法的名稱，以供您用來進行將資料指派給 UDT 或轉換為 UDT 時。 在執行 bcp 公用程式、BULK INSERT、DBCC CHECKDB、DBCC CHECKFILEGROUP、DBCC CHECKTABLE、分散式查詢和表格式資料流程（TDS）遠端程序呼叫（RPC）作業期間，也會呼叫**ValidationMethodName** 。 **ValidationMethodName**的預設值為 null，表示沒有任何驗證方法。  
  
### <a name="example"></a>範例  
 下列程式碼片段顯示**Point**類別的宣告，其指定**ValidatePoint**的**ValidationMethodName** 。  
  
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
  
 驗證方法可以有任何範圍，如果值有效，應傳回**true** ，否則傳回**false** 。 如果方法傳回**false**或擲回例外狀況，則會將值視為無效，並引發錯誤。  
  
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
  
 如果您想要在所有情況下執行驗證方法，您必須從屬性 setter 和**Parse**方法明確呼叫驗證方法。 這不是硬性規定，在某些情況下可能也不適當。  
  
### <a name="parse-validation-example"></a>Parse 驗證範例  
 若要確保在**Point**類別中叫用**ValidatePoint**方法，您必須從**Parse**方法和設定 X 和 Y 座標值的屬性程式呼叫它。 下列程式碼片段顯示如何從**Parse**函式呼叫**ValidatePoint**驗證方法。  
  
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
 下列程式碼片段顯示如何從設定 X 和 Y 座標的屬性程式呼叫**ValidatePoint**驗證方法。  
  
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
 當編碼 UDT 方法時，請考慮使用的演算法是否可能隨著時間而改變。 如果會的話，您可能會想要考慮針對 UDT 使用的方法建立個別類別。 如果演算法變更，您可在不影響 UDT 的情況下，以新的程式碼重新編譯該類別，並將組件載入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 在許多情況下，您可使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] ALTER ASSEMBLY 陳述式重新載入 UDT，但是這樣做可能會導致現有資料發生問題。 例如，包含在**AdventureWorks**範例資料庫中的**currency** UDT 會使用**ConvertCurrency**函數來轉換貨幣值，這會在不同的類別中執行。 轉換演算法在未來有可能以非預期的方式變更，或者可能需要新的功能。 在規劃未來的變更時，將**ConvertCurrency**函數與**Currency** UDT 的實作為分隔，可提供更大的彈性。  
  
### <a name="example"></a>範例  
 **Point**類別包含三種計算距離的簡單方法：**距離**、 **DistanceFrom**和**DistanceFromXY**。 每個都會傳回**double** ，計算從**點**到零的距離、從指定點到**點**的距離，以及從指定的 X 和 Y 座標到**點**的距離。 **距離**和**DistanceFrom**每個呼叫**DistanceFromXY**，並示範如何針對每個方法使用不同的引數。  
  
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
 **SqlMethodAttribute**類別所提供的自訂屬性可用來標示方法定義，以指定決定性、null 呼叫行為，以及指定方法是否為轉變子。 已假設這些屬性 (Property) 的預設值，而且只有在需要非預設值時才會使用自訂屬性 (Attribute)。  
  
> [!NOTE]  
>  **SqlMethodAttribute**類別繼承自**SqlFunctionAttribute**類別，因此**SqlMethodAttribute**會從**TableDefinition**繼承**FillRowMethodName**和**SqlFunctionAttribute**欄位。 這意味著撰寫資料表值方法是可行的，不過情況不是這樣。 方法會編譯和元件部署，但在執行時間會引發有關**IEnumerable**傳回型別的錯誤，並顯示下列訊息：元件 '\< \< assembly>'中類別'class>'的「方法、屬性或欄位'name>'有不正確傳回\<型別。」  
  
 下表描述一些可在 UDT 方法中使用的相關**SqlMethodAttribute**屬性，並列出其預設值。  
  
 DataAccess  
 指出此函數是否包含對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 本機執行個體中儲存之使用者資料的存取權。 預設值為**dataaccesskind.read**。**無**。  
  
 IsDeterministic  
 指出如果輸入值及資料庫狀態都相同，此函數是否會產生相同的輸出值。 預設值為**false**。  
  
 IsMutator  
 指出此方法是否會導致 UDT 執行個體的狀態變更。 預設值為**false**。  
  
 IsPrecise  
 指出此函數是否包含不精確的計算，如浮點運算。 預設值為**false**。  
  
 OnNullCall  
 指出當指定 Null 參考輸入引數時，是否呼叫此方法。 預設值為**true**。  
  
### <a name="example"></a>範例  
 **SqlMethodAttribute. 會**屬性可讓您標記一個方法，允許 UDT 實例的狀態發生變更的情況。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 不允許您在一個 UPDATE 陳述式的 SET 子句中，設定兩個 UDT 屬性。 但是，您可以將方法標示為 mutator，這樣會變更兩個成員。  
  
> [!NOTE]  
>  查詢中不允許使用 Mutator 方法。 它們只能在指派陳述式或資料修改陳述式中呼叫。 如果標記為轉變子的方法未傳回**void** （或不是 Visual Basic 中的**SUB** ），CREATE 類型會失敗並出現錯誤。  
  
 下列語句假設有一個具有**旋轉**方法的**三角形**UDT 存在。 下列[!INCLUDE[tsql](../../includes/tsql-md.md)] update 語句會叫用**輪替**方法：  
  
```  
UPDATE Triangles SET t.RotateY(0.6) WHERE id=5  
```  
  
 **旋轉**方法會使用**SqlMethod**屬性設定**會**為**true**來裝飾，因此[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可將方法標示為轉變子方法。 此程式碼也會將**OnNullCall**設定為**false**，這會向伺服器表示如果任何輸入參數為 null 參考，則方法會傳回 null 參考（在 Visual Basic 中為**任何內容**）。  
  
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
 使用使用者定義格式來執行 UDT 時，您必須執行 IBinarySerialize 介面的**讀取**和**寫入**方法，以處理 UDT 資料的序列化和還原序列化。 您也必須指定**SqlUserDefinedTypeAttribute**的**MaxByteSize**屬性。  
  
### <a name="the-currency-udt"></a>Currency UDT  
 **Currency** UDT 包含在可以與一起[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安裝的 CLR 範例中，從開始。 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]  
  
 **Currency** UDT 支援在特定文化特性的貨幣系統中處理 money 金額。 您必須定義兩個欄位： **CultureInfo**的**字串**，它會指定發行貨幣的物件（例如 En-us），以及**CurrencyValue**的**十進位**數（以 money 為單位）。  
  
 雖然伺服器不會使用它來執行比較，但**Currency** UDT 會實作為**CompareTo** **的 system.servicemodel 介面，** 它會公開單一方法。 這會在用戶端上使用，此時需要正確地比較或排序文化特性中的貨幣值。  
  
 在 CLR 上執行的程式碼會對貨幣值與文化特性分別進行比較。 如果是 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式碼，下列動作會決定比較：  
  
1.  將**IsByteOrdered**屬性設定為 true，這會[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]指示在磁片上使用保存的二進位表示來進行比較。  
  
2.  使用**Currency** udt 的[!INCLUDE[tsql](../../includes/tsql-md.md)] **Write**方法來判斷 udt 如何保存在磁片上，因此 udt 值的比較和排序方式以進行作業。  
  
3.  使用下列二進位格式來儲存**貨幣**UDT：  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

    1.  針對位元組 0-19 將文化特性儲存為 UTF-16 編碼的字串，並使用 null 字元填補到右邊。  
  
    2.  使用位元組 20 以上 (含) 來包含貨幣的十進位值。  
  
 填補的目的是確保文化特性與貨幣值完全分開，以便在將 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式碼中的一個 UDT 與另一 UDT 進行比較時，會將文化特性位元組與文化特性位元組進行比較，並將貨幣位元組值與貨幣位元組值進行比較。  
  
 如需**貨幣**UDT 的完整程式代碼清單，請遵循在[SQL Server 資料庫引擎範例](https://msftengprodsamples.codeplex.com/)中安裝 CLR 範例的指示。  
  
### <a name="currency-attributes"></a>Currency 屬性  
 **Currency** UDT 是使用下列屬性來定義。  
  
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
 當您選擇**使用者**定義的序列化格式時，您也必須執行**IBinarySerialize**介面，並建立自己的**讀取**和**寫入**方法。 下列來自**貨幣**udt 的程式會使用**BinaryReader**和**BinaryWriter** ，來讀取和寫入 UDT 中。  
  
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
  
 如需**貨幣**UDT 的完整程式代碼清單，請參閱[SQL Server 資料庫引擎範例](https://msftengprodsamples.codeplex.com/)。  
  
## <a name="see-also"></a>另請參閱  
 [建立使用者定義型別](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types.md)  
  
  
