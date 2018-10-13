---
title: 使用者定義型別需求 |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: acb2fe2d6c6b439295c0a6f0b7a4e233c23cb337
ms.sourcegitcommit: 08b3de02475314c07a82a88c77926d226098e23f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/12/2018
ms.locfileid: "49119746"
---
# <a name="creating-user-defined-types---requirements"></a>建立使用者定義型別 - 需求
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  建立使用者定義型別 (UDT)，在安裝時，您必須做數個重要的設計決策[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 對於大部分的 UDT 而言，雖然將 UDT 當做類別來建立也是一種選擇，但是建議將 UDT 當做結構來建立。 UDT 定義必須符合建立 UDT 的規格，才能讓它使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 註冊。  
  
## <a name="requirements-for-implementing-udts"></a>實作 UDT 的需求  
 若要在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中執行，UDT 必須實作 UDT 定義中的下列需求：  
  
 UDT 必須指定**Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute**。 善用**System.SerializableAttribute**是選擇性的但建議。  
  
-   UDT 必須實作**System.Data.SqlTypes.INullable**中的類別或結構建立公用介面**靜態**(**共用**在[!INCLUDE[msCoName](../../includes/msconame-md.md)]視覺化Basic) **Null**方法。 依預設，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 能夠辨識 Null。 若要讓在 UDT 中執行的程式碼能夠辨識 Null 值，此為必要選項。  
  
-   UDT 必須包含公用**靜態**(或**Shared**)**剖析**支援，從剖析的方法以及公用**ToString**方法將轉換成物件的字串表示。  
  
-   使用使用者定義序列化格式的 UDT 必須實作**System.Data.IBinarySerialize**介面，並提供**讀取**並**撰寫**方法。  
  
-   UDT 必須實作**System.Xml.Serialization.IXmlSerializable**，或所有公用欄位和屬性必須是 xml 序列化或與裝飾之型別的**XmlIgnore**屬性如果需要覆寫標準序列化。  
  
-   一個 UDT 物件必須僅有一個序列化。 如果序列化或還原序列化常式識別一個以上的特定物件表示法，則驗證會失敗。  
  
-   **SqlUserDefinedTypeAttribute.IsByteOrdered**必須是 **，則為 true**來比較資料的位元組順序。 如果未實作 IComparable 介面及**SqlUserDefinedTypeAttribute.IsByteOrdered**是**false**，位元組順序比較就會失敗。  
  
-   以類別定義的 UDT 必須具有不使用引數的公用建構函式。 您可以選擇性地建立其他多載類別建構函式。  
  
-   UDT 必須將資料元素公開為公用欄位或屬性程序。  
  
-   公用名稱長度不得超過 128 個字元，而且必須符合[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中所定義的識別碼命名規則[資料庫識別碼](../../relational-databases/databases/database-identifiers.md)。  
  
-   **sql_variant**資料行不能包含 UDT 的執行個體。  
  
-   因為 [!INCLUDE[tsql](../../includes/tsql-md.md)] 類型系統不會從 UDT 辨識繼承階層，所以無法從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 存取繼承成員。 不過，結構化類別時可以使用繼承，並可以在型別的 Managed 程式碼實作中呼叫此類方法。  
  
-   成員不可多載，但類別建構函式除外。 如果您有建立多載方法，則當您註冊組件或是在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中建立類型時，就不會引發錯誤。 多載方法的偵測會於執行階段發生，而不是在建立類型時發生。 在叫用之前，多載方法會一直存在於類別中。 一旦叫用多載方法，將會引發錯誤。  
  
-   任何**靜態**(或**共用**) 成員必須宣告為常數或以唯讀狀態。 靜態成員無法時常變動。  
  
-   如果**SqlUserDefinedTypeAttribute.MaxByteSize**欄位設定為-1，序列化的 UDT 可以與大型物件 (LOB) 大小限制 (目前為 2 GB) 一樣大。 UDT 的大小不能超過指定的值**MaxByteSized**欄位。  
  
> [!NOTE]  
>  雖然它不是由伺服器來執行比較，您可以選擇性地實作**System.IComparable**介面，以便公開單一方法， **CompareTo**。 在需要對 UDT 值進行精確比較或排序的情況下，將會在用戶端上使用它。  
  
## <a name="native-serialization"></a>原生序列化  
 若要為 UDT 選擇正確的序列化屬性，必須視您嘗試建立的 UDT 型別而定。 **原生**序列化格式使用很簡單的結構，可讓[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]UDT 的有效率的原生表示法儲存在磁碟上。 **原生**如果 UDT 很簡單，而且只包含下列類型的欄位，則建議格式：  
  
 **bool**，**位元組**， **sbyte**，**簡短**， **ushort**， **int**， **uint**，**長**， **ulong**， **float**， **double**， **SqlByte**，**SqlInt16**， **SqlInt32**， **SqlInt64**， **SqlDateTime**， **SqlSingle**， **SqlDouble**， **SqlMoney**， **SqlBoolean**  
  
 組成上述類型之欄位的實值類型十分適合**原生**格式，例如**結構**Visual C# (或**結構**如中Visual Basic)。 例如，使用指定的 UDT**原生**序列化格式可能包含也已經使用指定的另一個 UDT 的欄位**原生**格式。 如果 UDT 定義較為複雜，且包含不在上述清單上的資料類型，您必須指定**UserDefined**改為設定序列化的格式。  
  
 **原生**格式具有下列需求：  
  
-   類型必須為指定值**Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute.MaxByteSize**。  
  
-   所有欄位都必須為可序列化。  
  
-   **System.Runtime.InteropServices.StructLayoutAttribute**必須指定為**StructLayout.LayoutKindSequential**如果 UDT 定義於類別，而非以結構。 此屬性可以控制資料欄位的實體配置，並用於強制以成員出現的順序對成員進行配置。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會使用此屬性來判定具有多個值之 UDT 的欄位順序。  
  
 使用已定義之 UDT 的範例**原生**序列化，請參閱在 Point UDT [< 類型](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md)。  
  
## <a name="userdefined-serialization"></a>UserDefined 序列化  
 **UserDefined**格式設定**Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute**屬性可讓開發人員完全控制二進位格式。 指定時**格式**屬性為**UserDefined**，您必須執行下列程式碼中：  
  
-   指定選擇性**IsByteOrdered**屬性。 預設值為 **false**。  
  
-   指定**MaxByteSize**屬性**Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute**。  
  
-   撰寫程式碼來實作**讀取**並**撰寫**方法的實作 UDT **System.Data.Sql.IBinarySerialize**介面。  
  
 使用已定義之 UDT 的範例**UserDefined**序列化，請參閱 < Currency UDT > [< 類型](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md)。  
  
> [!NOTE]  
>  UDT 欄位必須使用原生序列化，或保存下來進行索引。  
  
## <a name="serialization-attributes"></a>序列化屬性  
 屬性會決定如何使用序列化來建構 UDT 的儲存表示，並將 UDT 以傳值方式傳輸到用戶端。 您必須指定**Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute**建立 UDT 時。 **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute**屬性會指出類別為 UDT，並指定 udt 的儲存體。 您可以選擇性地指定**Serializable**屬性，但是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不需要這個。  
  
 **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute**具有下列屬性。  
  
 **格式**  
 指定序列化格式，它可以是**原生**或是**UserDefined**，取決於資料類型的 UDT。  
  
 **IsByteOrdered**  
 A**布林**值，決定如何[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]UDT 上執行二進位比較。  
  
 **IsFixedLength**  
 表示此 UDT 的所有執行個體是否為相同長度。  
  
 **MaxByteSize**  
 執行個體的大小最大值 (位元組)。 您必須指定**MaxByteSize**具有**UserDefined**序列化格式。 使用指定的使用者定義序列化 udt **MaxByteSize**指 UDT 在其序列化形式的大小總計，如使用者所定義。 值**MaxByteSize**必須介於 1 到 8000 的範圍，或設為-1，表示 UDT 大於 8000 個位元組 （大小總計不得超過 LOB 大小的上限）。 請考量 UDT 與 10 個字元的字串屬性 (**System.Char**)。 當 UDT 使用 BinaryWriter 序列化時，序列化字串的總大小是 UDT 個位元組：每個 Unicode 2-16 字元兩個位元組，乘以字元的最大數目，再加上序列化二進位資料流所造成的兩個控制位元組負擔。 因此，判斷的值時**MaxByteSize**，必須考慮序列化 UDT 的總大小： 以二進位格式序列化資料，再加上序列化所造成的負擔的大小。  
  
 **ValidationMethodName**  
 用於驗證 UDT 執行個體之方法的名稱。  
  
### <a name="setting-isbyteordered"></a>設定 IsByteOrdered  
 當**Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute.IsByteOrdered**屬性設定為 **，則為 true**，您即已保證序列化的二進位資料，可以使用的語意順序的資訊。 因此，每個位元組排序的 UDT 物件執行個體只能有一個序列化表示法。 當在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中對已序列化的位元組執行比較作業時，其結果應與在 Managed 程式碼中執行比較作業的結果相同。 下列功能也會支援何時**IsByteOrdered**設為 **，則為 true**:  
  
-   在此型別之資料行上建立索引的功能。  
  
-   在此類型的資料行上建立主索引鍵及外部索引鍵，以及建立 CHECK 條件約束及 UNIQUE 條件約束的功能。  
  
-   使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] ORDER BY、GROUP BY 及 PARTITION BY 子句的功能。 在這些情況下，類型的二進位表示法用於決定順序。  
  
-   在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式中使用比較運算子的功能。  
  
-   保留此類型之計算資料行的功能。  
  
 請注意，同時**原生**並**UserDefined**序列化格式支援下列比較運算子時**IsByteOrdered**設為 **，則為 true**:  
  
-   等於 (=)  
  
-   不等於 (!=)  
  
-   大於 (>)  
  
-   小於 (\<)  
  
-   大於或等於 (>=)  
  
-   小於或等於 (<=)  
  
### <a name="implementing-nullability"></a>實作 Null 屬性  
 除了必須正確地指定組件的屬性外，您的類別還必須能夠支援 Null 屬性。 載入 Udt[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]感知 null，但是為了讓 UDT 能夠辨識 null 值，類別必須實作**INullable**介面。 如需詳細資訊和如何在 UDT 中實作 null 屬性的範例，請參閱[< 類型](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md)。  
  
### <a name="string-conversions"></a>字串轉換  
 為了支援 UDT 的來回的字串轉換，您必須提供**剖析**方法並**ToString**類別中的方法。 **剖析**方法允許將字串轉換成 UDT。 必須宣告為**靜態**(或**Shared** Visual Basic 中)，並採用參數的型別**System.Data.SqlTypes.SqlString**。 如需詳細資訊和如何實作的範例**剖析**並**ToString**方法，請參閱[< 類型](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md)。  
  
## <a name="xml-serialization"></a>XML 序列化  
 Udt 必須支援的轉換，來回**xml**藉由符合 XML 序列化合約的資料類型。 **System.Xml.Serialization**命名空間包含用來將物件序列化為 XML 格式的文件或資料流的類別。 您可以選擇實作**xml**使用的序列化**IXmlSerializable**介面，提供自訂格式的 XML 序列化和還原序列化。  
  
 除了執行從 UDT 到明確的轉換**xml**，XML 序列化，可讓您：  
  
-   使用**Xquery** UDT 執行個體，以轉換後的值**xml**資料型別。  
  
-   搭配 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的原生 XML Web 服務使用參數化查詢和 Web 方法中的 UDT。  
  
-   使用 UDT 接收 XML 資料的大量載入。  
  
-   序列化包含具有 UDT 資料行之資料表的 DataSet。  
  
 在 FOR XML 查詢中不會序列化 UDT。 若要執行顯示 Udt 的 XML 序列化的 FOR XML 查詢，明確轉換成每個 UDT 資料行**xml** SELECT 陳述式中的資料類型。 您可以明確地將轉換的資料行**varbinary**， **varchar**，或**nvarchar**。  
  
## <a name="see-also"></a>另請參閱  
 [建立使用者定義型別](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types.md)  
  
  
