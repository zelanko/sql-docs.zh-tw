---
title: 編碼使用者定義類型 |微軟文件
description: 此範例展示如何實現在 SQL Server 資料庫中使用的 UDT。 它實現 UDT 作為一個結構。
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
ms.openlocfilehash: a9d51cc0c33c8b656df176baa606a88a542ca4bc
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2020
ms.locfileid: "81486950"
---
# <a name="creating-user-defined-types---coding"></a>建立使用者定義型別 - 編碼
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  當您編碼使用者定義型別 (UDT) 定義時，您必須根據您是否將 UDT 實作為類別或結構以及您已選擇的格式和序列化選項來實作各種功能。  
  
 本節中的示例演示了將**點**UDT 實現為**結構**(或可視化基本**結構**)。 **點**UDT 由 X 和 Y 座標組成,這些座標作為屬性過程實現。  
  
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
  
 **Microsoft.SqlServer.Server.Server**命名空間包含 UDT 的各種屬性所需的物件,**而 System.Data.SqlType**命名空間包含表示[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可用於程式集的本機數據類型的類。 若要能夠正確運作，您的組件還需要其他的命名空間。 **點**UDT 還使用**System.Text**命名空間處理字串。  
  
> [!NOTE]  
>  可視C++資料庫物件(如UDT)與 **/clr:pure**編譯,不支援執行。  
  
## <a name="specifying-attributes"></a>指定屬性  
 屬性會決定如何使用序列化來建構 UDT 的儲存表示，並將 UDT 以傳值方式傳輸到用戶端。  
  
 **需要 Microsoft.SqlServer.Server.SqlUser 定義類型屬性**。 **可序列化**屬性是可選的。 您還可以指定**Microsoft.SqlServer.Server.SqlFacet 屬性**,以提供有關 UDT 的返回類型的資訊。 如需詳細資訊，請參閱 [CLR 常式的自訂屬性](../../relational-databases/clr-integration/database-objects/clr-integration-custom-attributes-for-clr-routines.md)。  
  
### <a name="point-udt-attributes"></a>Point UDT 屬性  
 **Microsoft.SqlServer.Server.SqlUser 定義類型屬性**將**點**UDT 的儲存格式設定為**本機**。 **IsByteOrdered**設置為**true**,這可確保 SQL Server 中的比較結果與託管代碼中發生的相同比較相同。 UDT 實現**System.Data.SqlType.INull 介面**,使 UDT 為 null。  
  
 以下片段顯示**點**UDT的屬性。  
  
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
 除了正確指定組件的屬性以外，UDT 還必須支援 Null 屬性。 載入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的 UDT 是 null 感知的,但為了 UDT 識別空值,UDT 必須實現**System.Data.SqlType.Inull 介面**。  
  
 您必須創建一個名為**IsNull**的屬性 ,這是確定 CLR 代碼中的值是否為空所必需的。 當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 找到 UDT 的 Null 執行個體時，便會使用正常的 Null 處理方法來保存 UDT。 除非必要，否則伺服器不會浪費時間來序列化或還原序列化 UDT，而且它也不會浪費空間來儲存 Null UDT。 每次從 CLR 引入 UDT 時都會執行 Null 檢查，這表示使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] IS NULL 建構來檢查 Null UDT 的作業一定都可運作。 伺服器還使用**IsNull**屬性來測試實例是否為空。 伺服器一旦判定 UDT 為 Null，就可以使用其原生的 Null 處理。  
  
 **IsNull**的**get()** 方法不是任何特殊大小寫方法。 如果**Point****\@** 變數 p 為**Null,** 則**\@預設情況下 p.IsNull**將計算為「NULL」,而不是「1」。。 這是因為**IsNull get()** 方法的**SqlMethod(OnNullCall)** 屬性預設為 false。 由於物件為**Null,** 因此在請求該屬性時,物件不會反序列化,因此不會呼叫該方法,並返回預設值"NULL"。  
  
### <a name="example"></a>範例  
 在下列範例中，`is_Null` 變數為私用，而且會針對 UDT 執行個體保留 Null 狀態。 您的程式碼必須維護對 `is_Null` 適當的值。 UDT 還必須具有名為**Null**的靜態屬性,該屬性傳回 UDT 的 null 值實例。 如果執行個體在資料庫中實際上為 Null，這可讓 UDT 傳回 Null 值。  
  
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
  
### <a name="is-null-vs-isnull"></a>IS NULL vs. IsNull  
 請考慮包含架構點(id int,位置點)的表,其中**Point**是 CLR UDT,以及以下查詢:  
  
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
  
 兩個查詢都返回具有非**空**位置的點的 ID。 查詢 1 會使用正常 null 處理，而且不需要還原序列化 UDT。 另一方面,查詢 2 必須取消序列化每個非**空**物件,並調用 CLR 以獲取**IsNull**屬性的值。 顯然,使用**IS NULL**將表現出更好的性能,並且不應有[!INCLUDE[tsql](../../includes/tsql-md.md)]任何理由從代碼讀取 UDT 的**IsNull**屬性。  
  
 那麼 **,IsNull**屬性的使用是什麼? 首先,需要確定 CLR 程式碼中的值是否**為空**。 其次,伺服器需要一種方法來測試實例是否**為 Null,** 因此伺服器使用此屬性。 在它確定為**Null**後,可以使用其本機 null 處理來處理它。  
  
## <a name="implementing-the-parse-method"></a>實作 Parse 方法  
 **分析**方法和**ToString**方法允許 UDT 的字串表示和轉換。 **解析**方法允許將字串轉換為 UDT。 它必須聲明為**靜態**(或在可視基本中**共用**),並採用**類型系統.Data.SqlType.SqlString 的**參數。  
  
 以下代碼實現**點**UDT 的**Parse**方法,該方法分離出 X 座標和 Y 座標。 **Parse**方法具有**類型 System.Data.SqlType.SqlString**的單個參數,並假定 X 和 Y 值作為逗號分隔字串提供。 將**Microsoft.SqlServer.Server.SqlMethod Attribute.OnNullCall**屬性設置為**false**可防止從 Point 的空實例呼叫**Parse**方法。  
  
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
 **ToString**方法將**點**UDT 轉換為字串值。 在這種情況下,為**Point**類型的 Null 實例傳回字串「NULL」。。 **ToString**方法透過使用**System.Text.StringBuilder**傳回逗號分隔**系統.String**組成的 X 和 Y 座標值來反轉**分析**方法。 由於**InvokeIfReceiverIsNull**預設為 false,因此不需要檢查**Point**的空實例。  
  
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
 **點**UDT 公開 X 和 Y 座標,這些座標作為**類型系統**的公共讀寫屬性實現。  
  
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
 當使用 UDT 資料時，[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 會自動將二進位值轉換成 UDT 值。 此轉換程序包括檢查適用於此類型之序列化格式的值，並確保可正確地將此值還原序列化。 如此可確保此值可以轉換回二進位格式。 如果是依照位元組排序的 UDT，這也可確保產生的二進位值會符合原始二進位值。 如此可防止在資料庫中保留無效的值。 在某些情況下，這個層級的檢查可能不夠。 當要求 UDT 值位於預期的網域或範圍內時，可能需要其他驗證。 例如，實作日期的 UDT 可能會要求日期值是一個正數，而且在某個有效值的範圍內。  
  
 **Microsoft.SqlServer.Server.Server.SqlUser定義類型屬性.驗證方法名稱**屬性的**Microsoft.SqlServer.Server.SqlUser 定義類型屬性**允許您提供伺服器在將數據分配給 UDT 或轉換為 UDT 時運行的驗證方法的名稱。 **驗證方法名稱**在 bcp 實用程式、BULK INSERT、DBCC CHECKDB、DBCC CHECKFILEGROUP、DBCC CHECKTABLE、分散式查詢和表格數據流 (TDS) 遠端過程調用 (RPC) 操作的運行期間也調用。 **驗證方法名稱**的預設值為 null,表示沒有驗證方法。  
  
### <a name="example"></a>範例  
 以下片段顯示**Point**類別的聲明,該類別指定**驗證點的驗證****方法名稱**。  
  
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
  
 驗證方法可以具有任何範圍,如果值有效,則應返回**true,** 否則**為 false。** 如果方法返回**false**或引發異常,則該值將被視為無效,並引發錯誤。  
  
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
  
 如果希望驗證方法在所有情況下都執行,則必須從屬性設置器和**Parse**方法顯式調用驗證方法。 這不是硬性規定，在某些情況下可能也不適當。  
  
### <a name="parse-validation-example"></a>Parse 驗證範例  
 為了確保在**Point**類中調用**ValidatePoint**方法,必須從**Parse**方法和設置 X 和 Y 座標值的屬性過程調用它。 以下片段示範如何從**Parse**函數呼叫**驗證點**驗證方法。  
  
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
 以下片段示範如何從設定 X 和 Y 座標的屬性過程呼叫**驗證點**驗證方法。  
  
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
 當編碼 UDT 方法時，請考慮使用的演算法是否可能隨著時間而改變。 如果會的話，您可能會想要考慮針對 UDT 使用的方法建立個別類別。 如果演算法變更，您可在不影響 UDT 的情況下，以新的程式碼重新編譯該類別，並將組件載入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 在許多情況下，您可使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] ALTER ASSEMBLY 陳述式重新載入 UDT，但是這樣做可能會導致現有資料發生問題。 例如 **,AdventureWorks**範例資料庫中包含的**貨幣**UDT 使用**ConvertCurrency**函數來轉換貨幣值,該幣值在單獨的類中實現。 轉換演算法在未來有可能以非預期的方式變更，或者可能需要新的功能。 在規劃未來更改時,將**ConvertCurrency**函數與**貨幣**UDT 實現分離提供了更大的靈活性。  
  
### <a name="example"></a>範例  
 **Point**類別包含三種計算距離的簡單方法**Distance**:**距離、距離**和**距離距離。** 每個返回一**個雙精度**值,計算從**點**到零的距離,從指定點到**點**的距離,以及從指定的 X 和 Y 座標到**點**的距離。 **距離**和**距離從**每個調用**距離距離從XY,** 並演示如何使用不同的參數,每種方法。  
  
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
 **Microsoft.SqlServer.Server.SqlMethodattribute**類提供自定義屬性,可用於標記方法定義,以便指定確定性、空調用行為以及指定方法是否為突變體。 已假設這些屬性 (Property) 的預設值，而且只有在需要非預設值時才會使用自訂屬性 (Attribute)。  
  
> [!NOTE]  
>  **SqlMethodAttribute**類從**SqlFunctionattribute**類繼承,因此**SqlMethodattribute**從**Sql功能屬性**繼承**FillRowMethodName 和****表定義**欄位。 這意味著撰寫資料表值方法是可行的，不過情況不是這樣。 該方法編譯和程式集部署,但在運行時引發有關**IE5ble**返回類型的錯誤,並顯示以下消息:"程式\<\<\<集' 程式集>'類『類>』中的方法、屬性或欄位'名稱>'具有無效的返回類型。  
  
 下表描述了一些相關的**Microsoft.SqlServer.Server.SqlMethod Attribute**屬性,這些屬性可用於 UDT 方法,並列出了它們的預設值。  
  
 DataAccess  
 指出此函數是否包含對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 本機執行個體中儲存之使用者資料的存取權。 默認值為**數據訪問。****無**。  
  
 IsDeterministic  
 指出如果輸入值及資料庫狀態都相同，此函數是否會產生相同的輸出值。 預設值**為 false**。  
  
 IsMutator  
 指出此方法是否會導致 UDT 執行個體的狀態變更。 預設值**為 false**。  
  
 IsPrecise  
 指出此函數是否包含不精確的計算，如浮點運算。 預設值**為 false**。  
  
 OnNullCall  
 指出當指定 Null 參考輸入引數時，是否呼叫此方法。 預設值**為 true**。  
  
### <a name="example"></a>範例  
 **Microsoft.SqlServer.Server.SqlMethodattribute.IsMutator**屬性允許您標記允許更改 UDT 實例狀態的方法。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 不允許您在一個 UPDATE 陳述式的 SET 子句中，設定兩個 UDT 屬性。 但是，您可以將方法標示為 mutator，這樣會變更兩個成員。  
  
> [!NOTE]  
>  查詢中不允許使用 Mutator 方法。 它們只能在指派陳述式或資料修改陳述式中呼叫。 如果標記為突變體的方法不返回**void(** 或不是可視化基本中的**子),** 則 CREATE TYPE 失敗,並出現錯誤。  
  
 以下語句假定存在具有**旋轉**方法**的三角形**UDT。 以下[!INCLUDE[tsql](../../includes/tsql-md.md)]更新敘述呼叫**Rotate**方法:  
  
```  
UPDATE Triangles SET t.RotateY(0.6) WHERE id=5  
```  
  
 **Rotate**方法使用**SqlMethod**屬性設置**IsMutator** **進行**true[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]進行修飾,以便將該方法標記為突變器方法。 代碼還將**OnNullCall**設置為**false**,它向伺服器指示,如果任何輸入參數為空引用,該方法將返回空引用(Visual Basic 中**沒有任何內容**)。  
  
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
 實現具有使用者定義的格式的 UDT 時,必須實現實現 Microsoft.SqlServer.Server.Server.IBinary 序列化介面的**讀取**和**寫入**方法,以處理序列化和反序列化 UDT 資料。 您還必須指定**Microsoft.SqlServer.Server.Server.SqlUser 定義類型屬性**的**MaxByteSize**屬性。  
  
### <a name="the-currency-udt"></a>Currency UDT  
 **貨幣**UDT 包含在 CLR 示例中,[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]該示[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]例可 隨安裝 ,以開頭。  
  
 **貨幣**UDT 支援在特定區域性的貨幣系統中處理金額。 您必須定義兩個字段:**區域性資訊**的**字串**,它指定貨幣的發行者(例如,en-us)和**貨幣價值****的小數,** 即貨幣金額。  
  
 雖然伺服器不使用它執行比較,**但貨幣**UDT 實現了**System.IThe 介面**,該介面公開了單個方法**System.ICompbe.比較。** 這會在用戶端上使用，此時需要正確地比較或排序文化特性中的貨幣值。  
  
 在 CLR 上執行的程式碼會對貨幣值與文化特性分別進行比較。 如果是 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式碼，下列動作會決定比較：  
  
1.  將**IsByteOrdered**屬性設定為[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]true, 該屬性指示在磁碟上使用持久化二進制表示形式進行比較。  
  
2.  使用**貨幣**UDT 的**寫入**方法確定 UDT 在磁碟上如何持久化,從而確定如何比較[!INCLUDE[tsql](../../includes/tsql-md.md)]UDT 值併為 操作排序。  
  
3.  使用以下二進位格式儲存**貨幣**UDT:  

    1.  針對位元組 0-19 將文化特性儲存為 UTF-16 編碼的字串，並使用 null 字元填補到右邊。  
  
    2.  使用位元組 20 以上 (含) 來包含貨幣的十進位值。  
  
 填補的目的是確保文化特性與貨幣值完全分開，以便在將 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式碼中的一個 UDT 與另一 UDT 進行比較時，會將文化特性位元組與文化特性位元組進行比較，並將貨幣位元組值與貨幣位元組值進行比較。  
  
 有關**貨幣**UDT 的完整代碼清單,請按照在[SQL Server 資料庫引擎範例中](https://msftengprodsamples.codeplex.com/)安裝 CLR 示例的說明進行操作。  
  
### <a name="currency-attributes"></a>Currency 屬性  
 **貨幣**UDT 使用以下屬性定義。  
  
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
 當您選擇**使用者定義的**序列化格式時,還必須實現**IBinary 序列化**介面並創建自己的**讀****寫**方法。 **貨幣**UDT 中的以下過程使用**System.IO.BinaryReader**和**System.IO.BinaryWriter**讀取和寫入 UDT。  
  
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
  
 有關**貨幣**UDT 的完整程式碼清單,請參考[SQL Server 資料庫引擎範例](https://msftengprodsamples.codeplex.com/)。  
  
## <a name="see-also"></a>另請參閱  
 [建立使用者定義型別](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types.md)  
  
  
