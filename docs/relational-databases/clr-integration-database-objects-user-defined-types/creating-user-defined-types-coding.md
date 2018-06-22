---
title: 使用者定義型別撰寫程式碼 |Microsoft 文件
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: reference
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
caps.latest.revision: 37
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: b3a698c63fa5fc7e5a0802716b3112df31cf241f
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2018
ms.locfileid: "35697899"
---
# <a name="creating-user-defined-types---coding"></a>建立使用者定義型別-撰寫程式碼
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  當您編碼使用者定義型別 (UDT) 定義時，您必須根據您是否將 UDT 實作為類別或結構以及您已選擇的格式和序列化選項來實作各種功能。  
  
 本節範例說明如何實作**點**將 UDT 當做**結構**(或**結構**在 Visual Basic 中)。 **點**UDT 包含 X 和 Y 座標實作為屬性程序。  
  
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
  
 **Microsoft.SqlServer.Server**命名空間包含各種屬性的 UDT，所需的物件和**System.Data.SqlTypes**命名空間包含的類別代表[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可用組件的原生資料類型。 若要能夠正確運作，您的組件還需要其他的命名空間。 **點**UDT 也使用**System.Text**命名空間來處理字串。  
  
> [!NOTE]  
>  Visual c + + 資料庫物件，例如 Udt，以編譯 **/clr: pure**不支援執行。  
  
## <a name="specifying-attributes"></a>指定屬性  
 屬性會決定如何使用序列化來建構 UDT 的儲存表示，並將 UDT 以傳值方式傳輸到用戶端。  
  
 **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute**需要。 **Serializable**屬性是選擇性的。 您也可以指定**Microsoft.SqlServer.Server.SqlFacetAttribute**提供有關 UDT 的傳回型別資訊。 如需詳細資訊，請參閱 [CLR 常式的自訂屬性](../../relational-databases/clr-integration/database-objects/clr-integration-custom-attributes-for-clr-routines.md)。  
  
### <a name="point-udt-attributes"></a>Point UDT 屬性  
 **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute**儲存格式設定**點**UDT 到**原生**。 **IsByteOrdered**設**true**，可保證的比較的結果是 SQL Server 中的相同如同相同的比較已在 managed 程式碼。 UDT 會實作**System.Data.SqlTypes.INullable**介面，好讓 UDT null 注意。  
  
 下列程式碼片段顯示的屬性**點**UDT。  
  
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
 除了正確指定組件的屬性以外，UDT 還必須支援 Null 屬性。 載入 Udt[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]感知 null，但為了讓 UDT 能夠辨識 null 值，UDT 必須實作**System.Data.SqlTypes.INullable**介面。  
  
 您必須建立一個名為屬性**IsNull**，需要該資料行來判斷值是否為 null 的 CLR 程式碼中。 當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 找到 UDT 的 Null 執行個體時，便會使用正常的 Null 處理方法來保存 UDT。 除非必要，否則伺服器不會浪費時間來序列化或還原序列化 UDT，而且它也不會浪費空間來儲存 Null UDT。 每次從 CLR 引入 UDT 時都會執行 Null 檢查，這表示使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] IS NULL 建構來檢查 Null UDT 的作業一定都可運作。 **IsNull**屬性也伺服器用來測試例項是否為 null。 伺服器一旦判定 UDT 為 Null，就可以使用其原生的 Null 處理。  
  
 **Get （)** 方法**IsNull**不是特殊案例，以任何方式。 如果**點**變數**@p**是**Null**，然後**@p.IsNull**會依預設，會評估為"NULL"，非"1"。 這是因為**SqlMethod(OnNullCall)** 屬性**IsNull get （)** 方法預設為 false。 因為這個物件是**Null**，當物件不會還原序列化，不會呼叫方法，並預設值是"NULL"傳回要求的屬性。  
  
### <a name="example"></a>範例  
 在下列範例中，`is_Null` 變數為私用，而且會針對 UDT 執行個體保留 Null 狀態。 您的程式碼必須維護對 `is_Null` 適當的值。 UDT 也必須擁有名為的靜態屬性**Null**傳回 UDT 的 null 值執行個體。 如果執行個體在資料庫中實際上為 Null，這可讓 UDT 傳回 Null 值。  
  
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
 包含結構描述點 (id int，位置點)，其中的資料表，請考慮**點**是 CLR UDT 及下列查詢：  
  
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
  
 這兩個查詢傳回的點與非識別碼**Null**位置。 查詢 1 會使用正常 null 處理，而且不需要還原序列化 UDT。 查詢 2，相反地，已還原序列化每一個非**Null**物件及呼叫 CLR，以取得的值**IsNull**屬性。 很明顯地，使用**IS NULL** ，則會展現更佳的效能，而且永遠不應該閱讀**IsNull**屬性從 UDT[!INCLUDE[tsql](../../includes/tsql-md.md)]程式碼。  
  
 因此，目標就是使用**IsNull**屬性？ 首先，需要用它來判斷值是否**Null**來自 CLR 程式碼。 第二，伺服器需要一個方法來測試例項是否為**Null**，所以伺服器會使用這個屬性。 它會判斷它之後**Null**，它就可以使用其原生 null 處理來處理它。  
  
## <a name="implementing-the-parse-method"></a>實作 Parse 方法  
 **剖析**和**ToString**方法允許與 UDT 的字串表示的轉換。 **剖析**方法允許將字串轉換成 UDT。 必須宣告為**靜態**(或**共用**在 Visual Basic 中)，而且需要型別參數**System.Data.SqlTypes.SqlString**。  
  
 下列程式碼會實作**剖析**方法**點**UDT，這樣會分隔 X 和 Y 座標。 **剖析**方法具有單一引數的型別**System.Data.SqlTypes.SqlString**，並假設 X 和 Y 值會提供以逗號分隔的字串。 設定**Microsoft.SqlServer.Server.SqlMethodAttribute.OnNullCall**屬性**false**防止**剖析**從的 null 執行個體時呼叫的方法點。  
  
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
 **ToString**方法轉換**點**UDT 的字串值。 在此情況下，傳回的 Null 執行個體的字串"NULL"**點**型別。 **ToString**方法反轉**剖析**方法藉由使用**System.Text.StringBuilder**傳回以逗號分隔**System.String**組成的 X 和 Y 座標值。 因為**InvokeIfReceiverIsNull**預設為 false，null 執行個體的核取**點**是不必要的。  
  
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
 **點**UDT 會公開為公用讀寫屬性的型別所實作的 X 和 Y 座標**System.Int32**。  
  
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
  
 **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute.ValidationMethodName**屬性**Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute**可讓您提供的名稱伺服器執行時的驗證方法是指派給 UDT 或轉換成 UDT 資料。 **ValidationMethodName**也稱為執行 bcp 公用程式、 BULK INSERT、 DBCC CHECKDB、 DBCC CHECKFILEGROUP、 DBCC CHECKTABLE、 分散式的查詢和表格式資料流 (TDS) 遠端程序呼叫 (RPC) 作業期間。 預設值為**ValidationMethodName**是 null，表示沒有驗證方法。  
  
### <a name="example"></a>範例  
 下列程式碼片段顯示的宣告**點**類別，其指定**ValidationMethodName**的**ValidatePoint**。  
  
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
  
 驗證方法可以有任何範圍，並應該傳回**true**如果值有效，以及**false**否則。 如果此方法會傳回**false**或擲回例外狀況，值會被視為無效，並發生錯誤，就會引發。  
  
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
  
 您必須明確呼叫驗證方法從屬性 setter 和**剖析**方法，如果您想要在所有情況下執行的驗證方法。 這不是硬性規定，在某些情況下可能也不適當。  
  
### <a name="parse-validation-example"></a>Parse 驗證範例  
 為了確保**ValidatePoint**中叫用方法**點**類別，您必須呼叫從**剖析**方法並從設定 X 和 Y 屬性程序座標值。 下列程式碼片段示範如何呼叫**ValidatePoint**驗證方法，從**剖析**函式。  
  
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
 下列程式碼片段示範如何呼叫**ValidatePoint**驗證方法，從設定 X 和 Y 座標屬性程序。  
  
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
 當編碼 UDT 方法時，請考慮使用的演算法是否可能隨著時間而改變。 如果會的話，您可能會想要考慮針對 UDT 使用的方法建立個別類別。 如果演算法變更，您可在不影響 UDT 的情況下，以新的程式碼重新編譯該類別，並將組件載入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 在許多情況下，您可使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] ALTER ASSEMBLY 陳述式重新載入 UDT，但是這樣做可能會導致現有資料發生問題。 例如，**貨幣**UDT 隨附**AdventureWorks**範例資料庫會使用**ConvertCurrency**函數來轉換貨幣值實作在個別的類別。 轉換演算法在未來有可能以非預期的方式變更，或者可能需要新的功能。 區隔**ConvertCurrency**函數從**貨幣**UDT 實作規劃未來的變更時，提供更大的彈性。  
  
### <a name="example"></a>範例  
 **點**類別包含三個簡單的方法來計算距離：**距離**， **DistanceFrom**和**DistanceFromXY**。 每一個都會傳回**double**計算從**點**為零，從指定的點之間的距離**點**，而且從距離指定 X 和 Y 座標若要**點**。 **距離**和**DistanceFrom**每次呼叫**DistanceFromXY**，並示範如何使用不同的引數，每個方法。  
  
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
 **Microsoft.SqlServer.Server.SqlMethodAttribute**類別提供的自訂屬性，可以用來標示方法定義中，若要針對 null 呼叫行為指定決定性以及指定方法是否為 mutator。 已假設這些屬性 (Property) 的預設值，而且只有在需要非預設值時才會使用自訂屬性 (Attribute)。  
  
> [!NOTE]  
>  **SqlMethodAttribute**類別繼承自**SqlFunctionAttribute**類別，因此**SqlMethodAttribute**繼承**FillRowMethodName**和**TableDefinition**欄位從**SqlFunctionAttribute**。 這意味著撰寫資料表值方法是可行的，不過情況不是這樣。 方法會進行編譯和組件部署，但發生錯誤的相關**IEnumerable**傳回型別就會引發在執行階段，並出現下列訊息: 「 方法、 屬性或欄位 '\<名稱 >' 中類別\<類別>' 中的組件 '\<組件 >' 具有無效的傳回型別。 」  
  
 下表描述的部分相關**Microsoft.SqlServer.Server.SqlMethodAttribute**屬性，可在 UDT 方法，並列出其預設值。  
  
 DataAccess  
 指出此函數是否包含對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 本機執行個體中儲存之使用者資料的存取權。 預設值是**DataAccessKind**。**無**。  
  
 IsDeterministic  
 指出如果輸入值及資料庫狀態都相同，此函數是否會產生相同的輸出值。 預設值是**false**。  
  
 IsMutator  
 指出此方法是否會導致 UDT 執行個體的狀態變更。 預設值是**false**。  
  
 IsPrecise  
 指出此函數是否包含不精確的計算，如浮點運算。 預設值是**false**。  
  
 OnNullCall  
 指出當指定 Null 參考輸入引數時，是否呼叫此方法。 預設值是**true**。  
  
### <a name="example"></a>範例  
 **Microsoft.SqlServer.Server.SqlMethodAttribute.IsMutator**屬性可讓您將方法標示為允許 UDT 執行個體的狀態變更。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 不允許您在一個 UPDATE 陳述式的 SET 子句中，設定兩個 UDT 屬性。 但是，您可以將方法標示為 mutator，這樣會變更兩個成員。  
  
> [!NOTE]  
>  查詢中不允許使用 Mutator 方法。 它們只能在指派陳述式或資料修改陳述式中呼叫。 如果方法標示為 mutator 不會傳回**void** (或不是**Sub**在 Visual Basic 中)，CREATE TYPE 失敗並發生錯誤。  
  
 下列陳述式假設存在**三角形**UDT**旋轉**方法。 下列[!INCLUDE[tsql](../../includes/tsql-md.md)]update 陳述式會叫用**旋轉**方法：  
  
```  
UPDATE Triangles SET t.RotateY(0.6) WHERE id=5  
```  
  
 **旋轉**方法以裝飾**SqlMethod**屬性設定**IsMutator**至**true**以便[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可以標記此方法為 mutator 方法。 程式碼也會設定**OnNullCall**至**false**，表示伺服器，方法會傳回 null 參考 (**做任何動作**在 Visual Basic 中) 如果有任何的輸入參數是 null 參考。  
  
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
 當以實作 UDT 的使用者定義的格式，您必須實作**讀取**和**寫入**處理序列化將 Microsoft.SqlServer.Server.IBinarySerialize 介面的方法和還原序列化 UDT 資料。 您也必須指定**MaxByteSize**屬性**Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute**。  
  
### <a name="the-currency-udt"></a>Currency UDT  
 **貨幣**UDT 隨附於可以使用安裝 CLR 範例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]開始[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]。  
  
 **貨幣**UDT 支援的特定文化特性的貨幣系統中的處理金額。 您必須定義兩個欄位：**字串**如**CultureInfo**，以指定發行貨幣 (en-我們為範例) 和**十進位**的**CurrencyValue**，總金額。  
  
 雖然它不是由伺服器來執行比較，**貨幣**UDT 會實作**System.IComparable**介面，以便公開單一方法， **System.IComparable.CompareTo**。 這會在用戶端上使用，此時需要正確地比較或排序文化特性中的貨幣值。  
  
 在 CLR 上執行的程式碼會對貨幣值與文化特性分別進行比較。 如果是 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式碼，下列動作會決定比較：  
  
1.  設定**IsByteOrdered**屬性設為 true，告知[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用磁碟上的保存的二進位表示進行比較。  
  
2.  使用**寫入**方法**貨幣**UDT，以判斷保存 UDT 的方式在磁碟上，因此如何比較 UDT 值，因為經過排序，[!INCLUDE[tsql](../../includes/tsql-md.md)]作業。  
  
3.  儲存**貨幣**UDT 使用下列二進位格式：  
  
    1.  針對位元組 0-19 將文化特性儲存為 UTF-16 編碼的字串，並使用 null 字元填補到右邊。  
  
    2.  使用位元組 20 以上 (含) 來包含貨幣的十進位值。  
  
 填補的目的是確保文化特性與貨幣值完全分開，以便在將 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式碼中的一個 UDT 與另一 UDT 進行比較時，會將文化特性位元組與文化特性位元組進行比較，並將貨幣位元組值與貨幣位元組值進行比較。  
  
 針對完整的程式碼清單**貨幣**UDT，有關範例的指示安裝 CLR 中的後續[SQL Server Database Engine 範例](http://msftengprodsamples.codeplex.com/)。  
  
### <a name="currency-attributes"></a>Currency 屬性  
 **貨幣**UDT 定義下列屬性。  
  
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
 當您選擇**UserDefined**序列化格式，您也必須實作**IBinarySerialize**介面，並建立您自己**讀取**和**寫入**方法。 下列程序從**貨幣**UDT 使用**System.IO.BinaryReader**和**System.IO.BinaryWriter**讀寫的 udt。  
  
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
  
 針對完整的程式碼清單**貨幣**UDT，請參閱[SQL Server Database Engine 範例](http://msftengprodsamples.codeplex.com/)。  
  
## <a name="see-also"></a>另請參閱  
 [建立使用者定義型別](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types.md)  
  
  
