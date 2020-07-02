---
title: 使用者定義類型需求 |Microsoft Docs
description: 本文說明當您建立要在 SQL Server 上安裝的 UDT 時，所需進行的重要設計決策。
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
ms.openlocfilehash: b20192a3804dfba713b04706d528738ceb8768c3
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85727814"
---
# <a name="creating-user-defined-types---requirements"></a>建立使用者定義型別 - 需求
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  建立要安裝在中的使用者定義型別（UDT）時，您必須進行幾項重要的設計決策 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 對於大部分的 UDT 而言，雖然將 UDT 當做類別來建立也是一種選擇，但是建議將 UDT 當做結構來建立。 UDT 定義必須符合建立 UDT 的規格，才能讓它使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 註冊。  
  
## <a name="requirements-for-implementing-udts"></a>實作 UDT 的需求  
 若要在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中執行，UDT 必須實作 UDT 定義中的下列需求：  
  
 此 UDT 必須指定**SqlUserDefinedTypeAttribute**。 **SerializableAttribute**是選擇性的，但建議使用。  
  
-   UDT 必須藉由建立公用**靜態**（在 Visual Basic 中為**Shared** ） Null 方法，在類別或結構中執行**SqlTypes. INullable**介面 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 。 **Null** 依預設，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 能夠辨識 Null。 若要讓在 UDT 中執行的程式碼能夠辨識 Null 值，此為必要選項。  
  
-   UDT 必須包含可支援從進行剖析的公用**靜態**（或**共用**） **Parse**方法，以及用來轉換為物件之字串表示的公用**ToString**方法。  
  
-   具有使用者定義序列化格式的 UDT 必須執行**IBinarySerialize**介面，並提供**讀取**和**寫入**方法。  
  
-   UDT 必須執行**System.Xml。** 如果需要覆寫標準序列化，則序列化 IXmlSerializable 或所有公用欄位和屬性都必須是可序列化的 XML 類型，或以**XmlIgnore**屬性裝飾。  
  
-   一個 UDT 物件必須僅有一個序列化。 如果序列化或還原序列化常式識別一個以上的特定物件表示法，則驗證會失敗。  
  
-   **SqlUserDefinedTypeAttribute。 IsByteOrdered**必須為**true** ，才能以位元組順序比較資料。 如果未實 SqlUserDefinedTypeAttribute IComparable 介面，且**IsByteOrdered**為**false**，則位元組順序比較將會失敗。  
  
-   以類別定義的 UDT 必須具有不使用引數的公用建構函式。 您可以選擇性地建立其他多載類別建構函式。  
  
-   UDT 必須將資料元素公開為公用欄位或屬性程序。  
  
-   公用名稱的長度不能超過128個字元，而且必須符合 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [資料庫識別碼](../../relational-databases/databases/database-identifiers.md)中所定義之識別碼的命名規則。  
  
-   **SQL_variant**的資料行不能包含 UDT 的實例。  
  
-   因為 [!INCLUDE[tsql](../../includes/tsql-md.md)] 類型系統不會從 UDT 辨識繼承階層，所以無法從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 存取繼承成員。 不過，結構化類別時可以使用繼承，並可以在型別的 Managed 程式碼實作中呼叫此類方法。  
  
-   成員不可多載，但類別建構函式除外。 如果您有建立多載方法，則當您註冊組件或是在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中建立類型時，就不會引發錯誤。 多載方法的偵測會於執行階段發生，而不是在建立類型時發生。 在叫用之前，多載方法會一直存在於類別中。 一旦叫用多載方法，將會引發錯誤。  
  
-   任何**靜態**（或**共用**）成員都必須宣告為常數或唯讀。 靜態成員無法時常變動。  
  
-   如果**SqlUserDefinedTypeAttribute. MaxByteSize**欄位設定為-1，則序列化的 UDT 可以與大型物件（LOB）大小限制（目前為 2 GB）一樣大。 UDT 的大小不能超過**MaxByteSized**欄位中指定的值。  
  
> [!NOTE]  
>  雖然伺服器不會使用它來執行比較，但是您可以選擇性地執行**CompareTo****的 system.servicemodel 介面，** 它會公開單一方法。 在需要對 UDT 值進行精確比較或排序的情況下，將會在用戶端上使用它。  
  
## <a name="native-serialization"></a>原生序列化  
 若要為 UDT 選擇正確的序列化屬性，必須視您嘗試建立的 UDT 型別而定。 **原生**序列化格式會利用非常簡單的結構，讓 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 能夠將有效的 UDT 原生標記法儲存在磁片上。 如果 UDT 很簡單，而且只包含下列類型的欄位，則建議使用**原生**格式：  
  
 **bool**、 **byte**、 **sbyte**、 **short**、 **ushort**、 **int**、 **uint**、 **long**、 **ulong**、 **float**、 **double**、 **SqlByte**、 **SqlInt16**、 **SqlInt32**、 **SqlInt64**、 **SqlDateTime**、 **SqlSingle**、 **SqlDouble**、 **SqlMoney**、 **SqlBoolean**  
  
 由上述類型的欄位所組成的實數值型別是**原生**格式的絕佳候選項目，例如 Visual c # 中的**結構**（或在 Visual Basic 中已知的**結構**）。 例如，使用**原生**序列化格式所指定的 udt，可能會包含另一個 udt 的欄位，也就是使用**原生**格式所指定的。 如果 UDT 定義比較複雜，且包含不在上述清單中的資料類型，您就必須改為指定**使用者**定義的序列化格式。  
  
 **原生**格式具有下列需求：  
  
-   此類型不能指定**SqlUserDefinedTypeAttribute. MaxByteSize**的值。  
  
-   所有欄位都必須為可序列化。  
  
-   如果 UDT 定義于類別中，而不是結構中，則**System.runtime.interopservices.outattribute StructLayoutAttribute**必須指定為**StructLayout。** 此屬性可以控制資料欄位的實體配置，並用於強制以成員出現的順序對成員進行配置。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會使用此屬性來判定具有多個值之 UDT 的欄位順序。  
  
 如需以**原生**序列化定義之 udt 的範例，請參閱撰寫[使用者定義類型的程式碼](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md)中的 Point udt。  
  
## <a name="userdefined-serialization"></a>UserDefined 序列化  
 **SqlUserDefinedTypeAttribute**屬性的**使用者**設定格式設定，可讓開發人員完整控制二進位格式。 以**使用者**設定的形式指定**格式**屬性屬性時，您必須在程式碼中執行下列動作：  
  
-   指定選擇性的**IsByteOrdered**屬性。 預設值為 **false**。  
  
-   指定**SqlUserDefinedTypeAttribute**的 [ **MaxByteSize** ] 屬性。  
  
-   藉由執行**IBinarySerialize**介面，撰寫程式碼來為 UDT 執行**讀取**和**寫入**方法。  
  
 如**需使用使用者定義的序列化**所定義之 udt 的範例，請參閱撰寫[使用者定義型別程式碼](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md)中的 Currency udt。  
  
> [!NOTE]  
>  UDT 欄位必須使用原生序列化，或保存下來進行索引。  
  
## <a name="serialization-attributes"></a>序列化屬性  
 屬性會決定如何使用序列化來建構 UDT 的儲存表示，並將 UDT 以傳值方式傳輸到用戶端。 在建立 UDT 時，您必須指定**SqlUserDefinedTypeAttribute** 。 **SqlUserDefinedTypeAttribute**屬性會指出類別是 udt，並指定 udt 的儲存區。 您可以選擇性地指定**Serializable**屬性，但不 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 需要這個。  
  
 **SqlUserDefinedTypeAttribute**具有下列屬性：。  
  
 **編排**  
 指定序列化格式，可以是**原生**或**使用者**設定的，視 UDT 的資料類型而定。  
  
 **IsByteOrdered**  
 **布林**值，決定如何 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在 UDT 上執行二進位比較。  
  
 **IsFixedLength**  
 表示此 UDT 的所有執行個體是否為相同長度。  
  
 **MaxByteSize**  
 執行個體的大小最大值 (位元組)。 您必須以**使用者**設定的序列化格式來指定**MaxByteSize** 。 針對已指定使用者定義序列化的 UDT， **MaxByteSize**會以使用者所定義的序列化格式來參考 udt 的總大小。 **MaxByteSize**的值必須在1到8000的範圍內，或設定為-1，表示 UDT 大於8000個位元組（總大小不能超過 LOB 大小上限）。 假設有一個具有10個**字元（system.string**）之字串屬性的 UDT。 當 UDT 使用 BinaryWriter 序列化時，序列化字串的總大小是 UDT 個位元組：每個 Unicode 2-16 字元兩個位元組，乘以字元的最大數目，再加上序列化二進位資料流所造成的兩個控制位元組負擔。 因此，在判斷**MaxByteSize**的值時，必須考慮序列化 UDT 的大小總計：以二進位格式序列化的資料大小，加上序列化所產生的額外負荷。  
  
 **ValidationMethodName**  
 用於驗證 UDT 執行個體之方法的名稱。  
  
### <a name="setting-isbyteordered"></a>設定 IsByteOrdered  
 當**SqlUserDefinedTypeAttribute. IsByteOrdered**屬性設定為**true**時，您實際上就是保證序列化的二進位資料可以用於資訊的語義排序。 因此，每個位元組排序的 UDT 物件執行個體只能有一個序列化表示法。 當在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中對已序列化的位元組執行比較作業時，其結果應與在 Managed 程式碼中執行比較作業的結果相同。 當**IsByteOrdered**設定為**true**時，也支援下列功能：  
  
-   在此型別之資料行上建立索引的功能。  
  
-   在此類型的資料行上建立主索引鍵及外部索引鍵，以及建立 CHECK 條件約束及 UNIQUE 條件約束的功能。  
  
-   使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] ORDER BY、GROUP BY 及 PARTITION BY 子句的功能。 在這些情況下，類型的二進位表示法用於決定順序。  
  
-   在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式中使用比較運算子的功能。  
  
-   保留此類型之計算資料行的功能。  
  
 請注意，當**IsByteOrdered**設定為**True**時，**原生**和**使用者**設定的序列化格式都支援下列比較運算子：  
  
-   等於 (=)  
  
-   不等於 (!=)  
  
-   大於 (>)  
  
-   小於 (\<)  
  
-   大於或等於 (>=)  
  
-   小於或等於 (&lt;=)  
  
### <a name="implementing-nullability"></a>實作 Null 屬性  
 除了必須正確地指定組件的屬性外，您的類別還必須能夠支援 Null 屬性。 載入至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 udt 可感知 null，但為了讓 UDT 能夠辨識 null 值，此類別必須實**INullable**介面。 如需詳細資訊以及如何在 UDT 中執行 null 屬性的範例，請參閱撰寫[使用者定義類型](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md)的程式碼。  
  
### <a name="string-conversions"></a>字串轉換  
 若要支援從 UDT 來回轉換的字串，您必須在類別中提供**Parse**方法和**ToString**方法。 **Parse**方法可讓字串轉換成 UDT。 它必須宣告為**靜態**（或在 Visual Basic 中**共用**），並採用**SqlTypes. SqlString**類型的參數。 如需如何執行**Parse**和**ToString**方法的詳細資訊和範例，請參閱撰寫[使用者定義類型](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md)的程式碼。  
  
## <a name="xml-serialization"></a>XML 序列化  
 Udt 必須符合 XML 序列化的合約，才能支援**xml**資料類型的轉換。 **System.Xml。序列化**命名空間包含用來將物件序列化為 XML 格式檔或資料流程的類別。 您可以選擇使用**IXmlSerializable**介面來執行**xml**序列化，以提供 xml 序列化和還原序列化的自訂格式。  
  
 除了執行從 UDT 到**xml**的明確轉換之外，xml 序列化還可讓您：  
  
-   轉換成**xml**資料類型之後，請在 UDT 實例的值上使用**Xquery** 。  
  
-   搭配 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的原生 XML Web 服務使用參數化查詢和 Web 方法中的 UDT。  
  
-   使用 UDT 接收 XML 資料的大量載入。  
  
-   序列化包含具有 UDT 資料行之資料表的 DataSet。  
  
 在 FOR XML 查詢中不會序列化 UDT。 若要執行可顯示 Udt 之 XML 序列化的 FOR XML 查詢，請在 SELECT 語句中，將每個 UDT 資料行明確轉換成**xml**資料類型。 您也可以將資料行明確轉換成**Varbinary**、 **Varchar**或**Nvarchar**。  
  
## <a name="see-also"></a>另請參閱  
 [建立使用者定義型別](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types.md)  
  
  
