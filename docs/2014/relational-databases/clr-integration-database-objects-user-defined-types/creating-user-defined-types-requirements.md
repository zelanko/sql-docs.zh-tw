---
title: 使用者定義型別需求 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: clr
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- UDTs [CLR integration], requirements
- serialization
- Native serialization format [CLR integration]
- attributes [CLR integration]
- XML serialization [CLR integration]
- user-defined types [CLR integration], requirements
- user-defined serialization [CLR integration]
- user-defined types [CLR integration], Native serialization
- UDTs [CLR integration], Native serialization
ms.assetid: bedc3372-50eb-40f2-bcf2-d6db6a63b7e6
caps.latest.revision: 31
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: ff2d8987dee15e39a5f85e4efc01f0bdaef27e06
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37350070"
---
# <a name="user-defined-type-requirements"></a>使用者定義型別需求
  建立使用者定義型別 (UDT)，在安裝時，您必須做數個重要的設計決策[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 對於大部分的 UDT 而言，雖然將 UDT 當做類別來建立也是一種選擇，但是建議將 UDT 當做結構來建立。 UDT 定義必須符合建立 UDT 的規格，才能讓它使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 註冊。  
  
## <a name="requirements-for-implementing-udts"></a>實作 UDT 的需求  
 若要在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中執行，UDT 必須實作 UDT 定義中的下列需求：  
  
 UDT 必須指定 `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute`。 雖然 `System.SerializableAttribute` 是選擇性使用的，但仍建議使用。  
  
-   UDT 必須藉由建立公用 `System.Data.SqlTypes.INullable` ([!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic 中為 `static`) `Shared` 方法，在類別或結構中實作 `Null` 介面。 依預設，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 能夠辨識 Null。 若要讓在 UDT 中執行的程式碼能夠辨識 Null 值，此為必要選項。  
  
-   UDT 必須包含可支援從物件字串表示法進行剖析的公用 `static` (或 `Shared`) `Parse` 方法，以及轉換為物件字串表示法的公用 `ToString` 方法。  
  
-   含有使用者定義序列化格式的 UDT 必須實作 `System.Data.IBinarySerialize` 介面，並提供 `Read` 和 `Write` 方法。  
  
-   UDT 必須實作 `System.Xml.Serialization.IXmlSerializable`，或如果必須覆寫標準序列化，所有的公用欄位和屬性都必須屬於可 XML 序列化或可使用 `XmlIgnore` 屬性來修飾的類型。  
  
-   一個 UDT 物件必須僅有一個序列化。 如果序列化或還原序列化常式識別一個以上的特定物件表示法，則驗證會失敗。  
  
-   `SqlUserDefinedTypeAttribute.IsByteOrdered` 必須是 `true`，才能按照位元組順序比較資料。 如果沒有實作 IComparable 介面，而且 `SqlUserDefinedTypeAttribute.IsByteOrdered` 是 `false`，位元組順序比較就會失敗。  
  
-   以類別定義的 UDT 必須具有不使用引數的公用建構函式。 您可以選擇性地建立其他多載類別建構函式。  
  
-   UDT 必須將資料元素公開為公用欄位或屬性程序。  
  
-   公用名稱長度不得超過 128 個字元，而且必須符合[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中所定義的識別碼命名規則[資料庫識別碼](../databases/database-identifiers.md)。  
  
-   `sql_variant` 資料行無法包含 UDT 的執行個體。  
  
-   因為 [!INCLUDE[tsql](../../includes/tsql-md.md)] 類型系統不會從 UDT 辨識繼承階層，所以無法從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 存取繼承成員。 不過，結構化類別時可以使用繼承，並可以在型別的 Managed 程式碼實作中呼叫此類方法。  
  
-   成員不可多載，但類別建構函式除外。 如果您有建立多載方法，則當您註冊組件或是在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中建立類型時，就不會引發錯誤。 多載方法的偵測會於執行階段發生，而不是在建立類型時發生。 在叫用之前，多載方法會一直存在於類別中。 一旦叫用多載方法，將會引發錯誤。  
  
-   任何 `static` (或 `Shared`) 成員都必須宣告為常數或唯讀。 靜態成員無法時常變動。  
  
-   如果 `SqlUserDefinedTypeAttribute.MaxByteSize` 欄位設定為 -1，則序列化的 UDT 可以與大型物件 (LOB) 的大小限制 (目前為 2 GB) 一樣大。 UDT 的大小不得超過 `MaxByteSized` 欄位中指定的值。  
  
> [!NOTE]  
>  儘管伺服器不會使用它來執行比較，但您可以選擇性地實作能夠公開單一方法 `System.IComparable` 的 `CompareTo` 介面。 在需要對 UDT 值進行精確比較或排序的情況下，將會在用戶端上使用它。  
  
## <a name="native-serialization"></a>原生序列化  
 若要為 UDT 選擇正確的序列化屬性，必須視您嘗試建立的 UDT 型別而定。 `Native` 序列化格式使用很簡單的結構，其可以讓 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將有效率的 UDT 原生表示法儲存在磁碟上。 如果 UDT 是簡單的，並且僅包含下列型別的欄位，則建議使用 `Native` 格式：  
  
 **bool**，**位元組**， **sbyte**，**簡短**， **ushort**， **int**， **uint**，**長**， **ulong**， **float**， **double**， **SqlByte**，**SqlInt16**， **SqlInt32**， **SqlInt64**， **SqlDateTime**， **SqlSingle**， **SqlDouble**， **SqlMoney**， **SqlBoolean**  
  
 組成上述類型之欄位的值類型是 `Native` 格式很好的候選項目，如 Visual C# 中的 `structs` (或 Visual Basic 中的 `Structures`)。 例如，使用 `Native` 序列化格式指定的 UDT 可能包含也使用 `Native` 格式指定之其他 UDT 的欄位。 如果 UDT 定義較為複雜，且包含不在上面清單中的資料型別，則必須改為指定 `UserDefined` 序列化格式。  
  
 `Native` 格式具有下列需求：  
  
-   型別不可指定 `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute.MaxByteSize` 的值。  
  
-   所有欄位都必須為可序列化。  
  
-   如果 UDT 是以類別而非以結構來定義，`System.Runtime.InteropServices.StructLayoutAttribute` 就必須指定為 `StructLayout.LayoutKindSequential`。 此屬性可以控制資料欄位的實體配置，並用於強制以成員出現的順序對成員進行配置。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會使用此屬性來判定具有多個值之 UDT 的欄位順序。  
  
 使用已定義之 UDT 的範例`Native`序列化，請參閱在 Point UDT [< 類型](creating-user-defined-types-coding.md)。  
  
## <a name="userdefined-serialization"></a>UserDefined 序列化  
 `UserDefined` 屬性的 `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute` 格式設定可讓開發人員完全控制二進位格式。 將 `Format` 屬性指定為 `UserDefined` 時，您必須在程式碼中進行下列動作：  
  
-   指定選擇性的 `IsByteOrdered` 屬性。 預設值是 `false`。  
  
-   指定 `MaxByteSize` 的 `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute` 屬性。  
  
-   藉由實作 `Read` 介面，撰寫程式碼以實作 UDT 的 `Write` 及 `System.Data.Sql.IBinarySerialize` 方法。  
  
 使用已定義之 UDT 的範例`UserDefined`序列化，請參閱 < Currency UDT > [< 類型](creating-user-defined-types-coding.md)。  
  
> [!NOTE]  
>  UDT 欄位必須使用原生序列化，或保存下來進行索引。  
  
## <a name="serialization-attributes"></a>序列化屬性  
 屬性會決定如何使用序列化來建構 UDT 的儲存表示，並將 UDT 以傳值方式傳輸到用戶端。 建立 UDT 時，您必須指定 `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute`。 `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute` 屬性表示類別為 UDT，並指定該 UDT 的儲存。 您可以選擇性地指定 `Serializable` 屬性，但是在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中不需要執行這項動作。  
  
 `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute` 具有下列屬性。  
  
 `Format`  
 指定序列化格式，其可以為 `Native` 或 `UserDefined`，這必須視 UDT 的資料類型而定。  
  
 `IsByteOrdered`  
 決定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 如何在 UDT 上執行二進位比較的 `Boolean` 值。  
  
 `IsFixedLength`  
 表示此 UDT 的所有執行個體是否為相同長度。  
  
 `MaxByteSize`  
 執行個體的大小最大值 (位元組)。 您必須使用 `MaxByteSize` 序列化格式指定 `UserDefined`。 如果 UDT 已指定使用者定義的序列化，對此 UDT 而言，`MaxByteSize` 是指 UDT 在其序列化形式 (由使用者所定義) 的總大小。 `MaxByteSize` 的值必須在 1 到 8000 的範圍內，或設定為 -1，表示 UDT 大於 8000 個位元組 (總大小不得超過 LOB 大小的上限)。 以一個具有 10 個字元字串之屬性的 UDT (`System.Char`) 為例。 當 UDT 使用 BinaryWriter 序列化時，序列化字串的總大小是 UDT 個位元組：每個 Unicode 2-16 字元兩個位元組，乘以字元的最大數目，再加上序列化二進位資料流所造成的兩個控制位元組負擔。 因此，在決定 `MaxByteSize` 的值時，必須考慮序列化 UDT 的總大小：以二進位形式序列化資料的大小，加上序列化所耗用的位元組。  
  
 `ValidationMethodName`  
 用於驗證 UDT 執行個體之方法的名稱。  
  
### <a name="setting-isbyteordered"></a>設定 IsByteOrdered  
 將 `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute.IsByteOrdered` 屬性設為 `true` 時，您即已保證序列化的二進位資料可以用於資訊的語意排序。 因此，每個位元組排序的 UDT 物件執行個體只能有一個序列化表示法。 當在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中對已序列化的位元組執行比較作業時，其結果應與在 Managed 程式碼中執行比較作業的結果相同。 將 `IsByteOrdered` 設為 `true` 時，還可支援下列功能：  
  
-   在此型別之資料行上建立索引的功能。  
  
-   在此類型的資料行上建立主索引鍵及外部索引鍵，以及建立 CHECK 條件約束及 UNIQUE 條件約束的功能。  
  
-   使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] ORDER BY、GROUP BY 及 PARTITION BY 子句的功能。 在這些情況下，類型的二進位表示法用於決定順序。  
  
-   在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式中使用比較運算子的功能。  
  
-   保留此類型之計算資料行的功能。  
  
 請注意，當 `Native` 設定為 `UserDefined` 時，`IsByteOrdered` 及 `true` 序列化格式可以支援下列比較運算子：  
  
-   等於 (=)  
  
-   不等於 (!=)  
  
-   大於 (>)  
  
-   小於 (\<)  
  
-   大於或等於 (>=)  
  
-   小於或等於 (<=)  
  
### <a name="implementing-nullability"></a>實作 Null 屬性  
 除了必須正確地指定組件的屬性外，您的類別還必須能夠支援 Null 屬性。 載入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 UDT 可辨識 Null，但是為了讓 UDT 能夠辨識 Null 值，此類別必須實作 `INullable` 介面。 如需詳細資訊和如何在 UDT 中實作 null 屬性的範例，請參閱[< 類型](creating-user-defined-types-coding.md)。  
  
### <a name="string-conversions"></a>字串轉換  
 若要支援字串與 UDT 的來回轉換，則必須在您的類別中提供 `Parse` 方法及 `ToString` 方法。 `Parse` 方法允許將字串轉換成 UDT。 它必須宣告為 `static` (或 Visual Basic 中的 `Shared`)，並採用型別 `System.Data.SqlTypes.SqlString` 的參數。 如需詳細資訊和如何實作的範例`Parse`並`ToString`方法，請參閱[< 類型](creating-user-defined-types-coding.md)。  
  
## <a name="xml-serialization"></a>XML 序列化  
 UDT 必須藉由符合 XML 序列化合約，來支援 `xml` 資料類型間的轉換。 `System.Xml.Serialization` 命名空間包含用於將物件序列化為 XML 格式文件或資料流的類別。 您可以選擇使用 `xml` 介面 (該介面可提供 XML 序列化和還原序列化的自訂格式)，以便實作 `IXmlSerializable` 序列化。  
  
 除了能夠執行 UDT 到 `xml` 的明確轉換外，XML 序列化還可讓您：  
  
-   轉換至 `Xquery` 資料類型後，在 UDT 執行個體的值上使用 `xml`。  
  
-   搭配 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的原生 XML Web 服務使用參數化查詢和 Web 方法中的 UDT。  
  
-   使用 UDT 接收 XML 資料的大量載入。  
  
-   序列化包含具有 UDT 資料行之資料表的 DataSet。  
  
 在 FOR XML 查詢中不會序列化 UDT。 若要執行顯示 UDT 之 XML 序列化的 FOR XML 查詢，請在 SELECT 陳述式中將每個 UDT 資料行明確轉換為 `xml` 資料類型。 您還可以將資料行明確轉換為 `varbinary`、`varchar` 或 `nvarchar`。  
  
## <a name="see-also"></a>另請參閱  
 [建立使用者定義型別](creating-user-defined-types.md)  
  
  
