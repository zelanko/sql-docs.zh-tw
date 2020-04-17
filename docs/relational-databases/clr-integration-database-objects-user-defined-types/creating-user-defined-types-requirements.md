---
title: 使用者定義的類型要求 |微軟文件
description: 本文介紹了在創建要在 SQL Server 上安裝的 UDT 時需要做出的重要設計決策。
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
ms.openlocfilehash: 2b19a9179cba2225a2209255ce48220669e4bbef
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2020
ms.locfileid: "81486967"
---
# <a name="creating-user-defined-types---requirements"></a>建立使用者定義型別 - 需求
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  在創建要安裝在[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的使用者定義類型 (UDT) 時,必須做出幾個重要的設計決策。 對於大部分的 UDT 而言，雖然將 UDT 當做類別來建立也是一種選擇，但是建議將 UDT 當做結構來建立。 UDT 定義必須符合建立 UDT 的規格，才能讓它使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 註冊。  
  
## <a name="requirements-for-implementing-udts"></a>實作 UDT 的需求  
 若要在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中執行，UDT 必須實作 UDT 定義中的下列需求：  
  
 UDT 必須指定**Microsoft.SqlServer.Server.SqlUser 定義類型屬性**。 系統.**可序列化屬性**的使用是可選的,但建議使用。  
  
-   UDT 必須透過建立公共**靜態**(在可[!INCLUDE[msCoName](../../includes/msconame-md.md)]視基本中**共用****)Null**方法在類別或結構中實現**System.Data.SqlType.INull 介面**。 依預設，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 能夠辨識 Null。 若要讓在 UDT 中執行的程式碼能夠辨識 Null 值，此為必要選項。  
  
-   UDT 必須包含支援從中解析的公共**靜態**(或**共用**)**解析**方法,以及用於轉換為物件的字串表示形式的公共**ToString**方法。  
  
-   具有使用者定義的序列化格式的 UDT 必須實現**System.Data.IBinary 序列化**介面並提供**讀取**和**寫入**方法。  
  
-   UDT 必須實現**System.Xml.序列化.IXml 序列化**,或者所有公共欄位和屬性必須是 XML 可序列化或使用**XmlIgnore**屬性修飾的類型(如果需要重寫標準序列化)。  
  
-   一個 UDT 物件必須僅有一個序列化。 如果序列化或還原序列化常式識別一個以上的特定物件表示法，則驗證會失敗。  
  
-   **SqlUser 定義類型屬性.IsByteOrder**必須**為 true,** 才能按位元組順序比較資料。 如果未實現 I 可比較介面,並且**SqlUser 定義 Typeattribute.IsByte Orderafalse,** 位**false**元組順序比較將失敗。  
  
-   以類別定義的 UDT 必須具有不使用引數的公用建構函式。 您可以選擇性地建立其他多載類別建構函式。  
  
-   UDT 必須將資料元素公開為公用欄位或屬性程序。  
  
-   公共名稱不能超過 128 個字元,並且必須符合[資料庫標識符](../../relational-databases/databases/database-identifiers.md)中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]定義的標識符的命名規則。  
  
-   **sql_variant**列不能包含 UDT 的實例。  
  
-   因為 [!INCLUDE[tsql](../../includes/tsql-md.md)] 類型系統不會從 UDT 辨識繼承階層，所以無法從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 存取繼承成員。 不過，結構化類別時可以使用繼承，並可以在型別的 Managed 程式碼實作中呼叫此類方法。  
  
-   成員不可多載，但類別建構函式除外。 如果您有建立多載方法，則當您註冊組件或是在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中建立類型時，就不會引發錯誤。 多載方法的偵測會於執行階段發生，而不是在建立類型時發生。 在叫用之前，多載方法會一直存在於類別中。 一旦叫用多載方法，將會引發錯誤。  
  
-   任何**靜態**(或**共用**)成員都必須聲明為常量或唯讀。 靜態成員無法時常變動。  
  
-   如果**SqlUser 定義TypeAttribute.MaxByteSize**欄位設定為 -1,則序列化 UDT 可以大到大物件 (LOB) 大小限制(目前為 2 GB)。 UDT 的大小不能超過**MaxByteSize**欄位中指定的值。  
  
> [!NOTE]  
>  儘管伺服器不使用它執行比較,但您可以選擇實現**System.IThecomp 介面**,該介面公開單個方法**比較。** 在需要對 UDT 值進行精確比較或排序的情況下，將會在用戶端上使用它。  
  
## <a name="native-serialization"></a>原生序列化  
 若要為 UDT 選擇正確的序列化屬性，必須視您嘗試建立的 UDT 型別而定。 **本機**序列化格式使用非常簡單的結構,能夠[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]在磁碟上存儲 UDT 的有效本機表示形式。 如果 UDT 簡單且只有以下類型的欄位,則建議使用**本機**格式:  
  
 **布爾**,**位元組**,**位元組**,**短**, **ushort,** **int,** **uint,****長**,**烏龍**,**浮動**,**雙**, **SqlByte,** **SqlInt16,** **SqlInt32,** **SqlInt64,** **SqlDatetime,** **SqlSingle,** **SqlDouble,** **SqlMoney,** **SqlBoolean**  
  
 由上述類型的欄位組成的值類型是**本機**格式的良好候選項,例如 Visual C# 中的**結構**(或 Visual Basic 中已知的**結構**)。 例如,使用**本機**序列化格式指定的UDT可能包含另一個UDT的欄位,該欄位也使用**本機**格式指定。 如果 UDT 定義更為複雜,並且包含不在上述清單中的數據類型,則必須改為指定 User**定義**序列化格式。  
  
 **這個機**格式具有以下要求:  
  
-   此類型不得為**Microsoft.SqlServer.Server.Server.SqlUser 定義類型屬性指定值**。  
  
-   所有欄位都必須為可序列化。  
  
-   如果 UDT 是在類中定義的,而不是結構中定義的,則必須將**系統.Runtime.InteropServices.StructLayout屬性**指定為 **"結構佈局"。LayoutKind順序**。 此屬性可以控制資料欄位的實體配置，並用於強制以成員出現的順序對成員進行配置。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會使用此屬性來判定具有多個值之 UDT 的欄位順序。  
  
 有關使用**本機**序列化定義的 UDT 的範例,請參閱[編碼使用者定義類型的](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md)點 UDT。  
  
## <a name="userdefined-serialization"></a>UserDefined 序列化  
 **Microsoft.SqlServer.Server.Server.SqlUser 定義類型屬性**的使用者**定義**格式設置使開發人員能夠完全控制二進位格式。 將**Format**屬性屬性指定為 **「使用者定義**」時,必須在代碼中執行以下操作:  
  
-   指定可選的**IsByte 順序**屬性屬性。 預設值為 **false**。  
  
-   指定**Microsoft.SqlServer.Server.Server.SqlUser 定義類型屬性**的**MaxByteSize**屬性。  
  
-   通過實現**系統.Data.Sql.IBinary 序列化介面**編寫代碼以實現 UDT 的**Read****讀寫**方法。  
  
 有關使用**使用者定義**序列化定義的 UDT 的範例,請參閱[編碼使用者定義類型](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md)中的貨幣 UDT。  
  
> [!NOTE]  
>  UDT 欄位必須使用原生序列化，或保存下來進行索引。  
  
## <a name="serialization-attributes"></a>序列化屬性  
 屬性會決定如何使用序列化來建構 UDT 的儲存表示，並將 UDT 以傳值方式傳輸到用戶端。 建立 UDT 時,您需要指定**Microsoft.SqlServer.Server.SqlUser 定義類型屬性**。 **Microsoft.SqlServer.Server.SqlUser 定義類型屬性屬性**指示該類是 UDT 並指定 UDT 的存儲。 您可以選擇指定**可序列化**屬性[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)],儘管 不需要這樣做。  
  
 **Microsoft.SqlServer.Server.SqlUser 定義類型屬性**具有以下屬性。  
  
 **格式**  
 指定序列化格式(可以是**本機**格式或**使用者定義**格式,具體取決於 UDT 的數據類型)。  
  
 **IsByteOrdered**  
 確定**Boolean**如何[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]在 UDT 上執行二進位比較的布林值。  
  
 **IsFixedLength**  
 表示此 UDT 的所有執行個體是否為相同長度。  
  
 **MaxByteSize**  
 執行個體的大小最大值 (位元組)。 您必須使用**使用者定義的**序列化格式指定**MaxByteSize。** 對於指定使用者定義的序列化的**UDT,MaxByteSize**是指使用者定義的序列化形式的 UDT 的總大小。 **MaxByteSize**的值必須在 1 到 8000 的範圍內,或設置為 -1 以指示 UDT 大於 8000 位元組(總大小不能超過最大 LOB 大小)。 考慮一個包含 10 個字元字串屬性 (**System.Char**) 的 UDT。 當 UDT 使用 BinaryWriter 序列化時，序列化字串的總大小是 UDT 個位元組：每個 Unicode 2-16 字元兩個位元組，乘以字元的最大數目，再加上序列化二進位資料流所造成的兩個控制位元組負擔。 因此,在確定**MaxByteSize**的值時,必須考慮序列化 UDT 的總大小:以二進位形式序列化的數據的大小加上序列化產生的開銷。  
  
 **驗證方法名稱**  
 用於驗證 UDT 執行個體之方法的名稱。  
  
### <a name="setting-isbyteordered"></a>設定 IsByteOrdered  
 當**Microsoft.SqlServer.Server.Server.SqlUser 定義Typeattribute.IsByteOrdered**屬性設置為**true**時,您實際上保證序列化二進位資料可用於資訊的語義排序。 因此，每個位元組排序的 UDT 物件執行個體只能有一個序列化表示法。 當在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中對已序列化的位元組執行比較作業時，其結果應與在 Managed 程式碼中執行比較作業的結果相同。 當**IsByteOrdered**設定為**true**時,還支援以下功能:  
  
-   在此型別之資料行上建立索引的功能。  
  
-   在此類型的資料行上建立主索引鍵及外部索引鍵，以及建立 CHECK 條件約束及 UNIQUE 條件約束的功能。  
  
-   使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] ORDER BY、GROUP BY 及 PARTITION BY 子句的功能。 在這些情況下，類型的二進位表示法用於決定順序。  
  
-   在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式中使用比較運算子的功能。  
  
-   保留此類型之計算資料行的功能。  
  
 請注意,當**IsByteOrdered**設定為**true**時,**本機**與**使用者定義的**序列化格式都支援以下比較運算符號:  
  
-   等於 (=)  
  
-   不等於 (!=)  
  
-   大於 (>)  
  
-   小於 (\<)  
  
-   大於或等於 (>=)  
  
-   小於或等於 (&lt;=)  
  
### <a name="implementing-nullability"></a>實作 Null 屬性  
 除了必須正確地指定組件的屬性外，您的類別還必須能夠支援 Null 屬性。 載入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的 UDT 是 null 感知的,但為了 UDT 識別 null 值,類別必須實現**INull 可介面**。 有關詳細資訊以及如何在 UDT 中實現 null 的範例,請參考[使用者定義類型](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md)。  
  
### <a name="string-conversions"></a>字串轉換  
 要支援與 UDT 的字串轉換,必須在類中提供**分析**方法和**ToString**方法。 **解析**方法允許將字串轉換為 UDT。 它必須聲明為**靜態**(或在可視基本中**共用**),並採用**類型系統.Data.SqlType.SqlString 的**參數。 有關詳細資訊以及如何實現**分析**和**ToString**方法的範例,請參考[使用者定義類型](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md)。  
  
## <a name="xml-serialization"></a>XML 序列化  
 UDT 必須支援透過遵循 XML 序列化協定來支援與**xml**資料類型轉換。 **System.Xml.序列化**命名空間包含用於將物件序列化為 XML 格式文件或串流的類。 您可以選擇使用**IXml 序列化**介面實現**xml**序列化,該介面為 XML 序列化和反序列化提供自訂格式。  
  
 除了執行從 UDT 到**xml**的繪圖轉換外,XML 序列化還使您能夠:  
  
-   轉換為**xml**資料類型後,對 UDT 實體的值使用**Xquery。**  
  
-   搭配 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的原生 XML Web 服務使用參數化查詢和 Web 方法中的 UDT。  
  
-   使用 UDT 接收 XML 資料的大量載入。  
  
-   序列化包含具有 UDT 資料行之資料表的 DataSet。  
  
 在 FOR XML 查詢中不會序列化 UDT。 要執行顯示 UDT 的 XML 序列化的 FOR XML 查詢,請顯式將每個 UDT 列轉換為 SELECT 語句中的**xml**資料類型。 您還可以顯示式轉換為**varbinary、varchar****varchar**或**nvarchar**。  
  
## <a name="see-also"></a>另請參閱  
 [建立使用者定義型別](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types.md)  
  
  
