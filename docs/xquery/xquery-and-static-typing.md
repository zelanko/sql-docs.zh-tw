---
title: XQuery 與靜態輸入 |Microsoft 文件
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: sql
ms.component: xquery
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- XQuery, static typing
- static typing
- checking static types
- inference [XQuery]
ms.assetid: d599c791-200d-46f8-b758-97e761a1a5c0
caps.latest.revision: 38
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 03958536a329b59a15ceade13cac1598d97dd346
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33077935"
---
# <a name="xquery-and-static-typing"></a>XQuery 與靜態類型
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中的 XQuery 是靜態類型的語言。 也就是，它會在查詢編譯期間，當特定函數或運算子不接受運算式傳回含有類型或基數的值時，就會引發類型錯誤。 除此之外，如果在具類型的 XML 文件中的路徑運算式之類型為錯誤的，靜態類型檢查也可以偵測到。 XQuery 編譯器首先會套用加入如自動化等隱含作業的正規化階段，然後執行靜態類型推斷和靜態類型檢查。  
  
## <a name="static-type-inference"></a>靜態類型推斷  
 靜態類型推斷可決定運算式的傳回類型。 它判斷的方法是透過採用靜態類型的輸入參數與靜態語意的運算，並決定靜態類型的結果。 例如，靜態類型的運算式 1 + 2.3 是以下列方式所決定：  
  
-   靜態類型的 1 是**xs: integer**和靜態類型的 2.3 是**xs: decimal**。 根據動態語意，靜態語意**+** 作業將整數轉換成小數，然後傳回 十進位數。 推斷的靜態類型就會是**xs: decimal**。  
  
 對於不具類型的 XML 執行個體，有特殊類型可指出資料不具類型。 此資訊是在靜態類型檢查中使用並用以執行某些隱含轉換)。  
  
 對於具類型的資料而言，輸入類型是從 XML 結構描述集合所推斷，可約束 XML 資料類型的執行個體。 例如，如果結構描述允許唯一的項目類型的**xs: integer**，使用該元素的路徑運算式的結果會是零或多個類型的項目**xs: integer**。 目前使用的運算式，例如表示這`element(age,xs:integer)*`其中星號 (\*) 表示產生類型的基數。 在此範例中，運算式可能會在名為"age"和類型的零或多個項目**xs: integer**。 其他基數剛好是其中一種，並會使用類型名稱，表示零個或一個，而且表示使用問號 (**？**)，和 1 或多個則表示使用加號 (**+**).  
  
 有時，靜態類型推斷可推斷永遠會傳回空白時序的運算式。 例如，如果路徑運算式在具類型的 XML 資料類型會尋找\<名稱 > 元素內\<客戶 > 項目 （/客戶名稱），但結構描述不允許\<名稱 > 內\<客戶 >，靜態類型推斷會推斷，結果會是空的。 這會用來偵測不正確的查詢，而且除非運算式可為 （） 會報告為靜態錯誤，或**資料 （（））**。  
  
 詳細推斷規則是以正式語意的 XQuery 規格來提供。 Microsoft 僅稍微修改了這些規則，以配合具類型的 XML 資料類型執行個體的運作。 從標準所做的最重要變更，為隱含文件節點可得知 XML 資料類型執行個體的類型。 因此，該格式 / 存在時間的路徑運算式將會根據該資訊來精確的設定其類型。  
  
 使用[SQL Server Profiler 範本和權限](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)，您可以看到查詢編譯的一部分傳回的靜態類型。 若要查看這些類型，您的追蹤必須在 TSQL 事件類別中，包含 XQuery 靜態類型事件。  
  
## <a name="static-type-checking"></a>靜態類型檢查  
 靜態類型檢查可確保執行階段執行只會接收適用於運算的類型值。 因為在執行階段不必檢查這些類型，所以在編譯早期將可偵測到潛在的錯誤。 這將可改善效能。 不過，靜態類型需要查詢寫入器在形成查詢時更為小心。  
  
 以下是可使用的適當類型：  
  
-   函數或運算明確允許的類型。  
  
-   明確允許類型的子類型。  
  
 根據子類型規則 (使用 XML 結構描述的限制或延伸模組之衍生) 來定義的子類型。 例如，S 類型是 T 類型的子類型，如果所有含有 S 類型的值都有 T 類型的執行個體的話。  
  
 除此之外，根據 XML 結構描述類型階層，所有的整數值也是小數值。 然而，並非所有的小數值都是整數。 因此，整數是小數的子類型，但並不是反之亦然。 例如， **+** 運算只能允許某些類型，例如數值類型的值**xs: integer**， **xs: decimal**， **xs:float**，和**xs: double**。 如果其他類型的值，例如**xs: string**，會傳遞時，作業會引發類型錯誤。 這稱為強式類型。 其他類型的值 (例如用以指出不具類型的 XML 之自動類型) 可隱含轉換為作業可接受的類型值。 這稱為弱式類型。  
  
 如果在隱含轉換後需要它，靜態類型檢查可確保只會將具有正確基數的允許類型值傳遞至運算中。 它會辨識為 「 字串 」 + 1，靜態類型的 「 字串 」 是**xs: string**。 因為這不是允許的類型為**+** ，就會引發類型錯誤的作業。  
  
 在將任意運算式 E1 的結果與任意運算式 E2 相加的例子中 (E1 + E2)，靜態類型推斷首先會決定 E1 與 E2 的靜態類型，然後以運算所允許的類型來檢查靜態類型。 例如，如果 E1 的靜態類型可以是**xs: string**或**xs: integer**，靜態類型檢查就會引發類型錯誤，即使某些值在執行的階段可能是整數。 如果 E1 的靜態類型，相同便會發生**xs: integer\***。 因為**+** 作業只接受一個整數值和 E1 可傳回零或 1 個以上，靜態類型檢查就會引發錯誤。  
  
 如稍早所提及，類型推斷經常所推斷的類型，比使用者所知道的傳遞資料類型更為廣泛。 在這些情況下，使用者必須重寫查詢。 有些典型的例子包含下列項目：  
  
-   該類型推斷更廣泛的類型，例如超級類型或聯集類型。 如果類型是不可部份完成的類型，您應該使用轉換運算式或建構函式指出實際的靜態類型。 例如，如果運算式 E1 的推斷的類型之間的選擇**xs: string**或**xs: integer**而加法需要**xs: integer**，您應該撰寫`xs:integer(E1) + E2`而不是`E1+E2`。 如果遇到的字串值，這個運算式可能會在執行階段失敗，無法轉換成**xs: integer**。 不過，運算式現在會傳遞靜態類型檢查。 此運算式會對應到空白時序。  
  
-   此類型會推斷比資料實際包含的基數更高的基數。 這通常是因為**xml**資料類型可包含多個最上層項目，以及 XML 結構描述集合無法約束此。 為了減少靜態類型並保證最多只傳遞一個值，您應該使用位置性述詞 `[1]`。 例如，若要在最上層元素之下，將 1 加入元素 `c` 的屬性 `b` 值，您必須`write (/a/b/@c)[1]+1`。 除此之外，DOCUMENT 關鍵字可與 XML 結構描述集合一起使用。  
  
-   有些運算會在推斷時遺失類型資訊。 例如，如果無法判斷節點的類型，它會變成**anyType**。 這並不會隱含地轉換成任何其他類型。 在導覽期間使用父軸時，這種轉換最為明顯。 如果運算式將會建立靜態類型錯誤，您應該避免使用此種運算並重寫查詢。  
  
## <a name="type-checking-of-union-types"></a>聯集類型的類型檢查  
 因為類型檢查的關係，處理聯集類型要很小心。 下列範例將舉例說明兩個問題。  
  
### <a name="example-function-over-union-type"></a>範例：聯集類型的函數  
 請針對聯集類型的 <`r`> 來考量元素定義：  
  
```  
<xs:element name="r">  
<xs:simpleType>  
   <xs:union memberTypes="xs:int xs:float xs:double"/>  
</xs:simpleType>  
</xs:element>  
```  
  
 在 XQuery 內容中，"average"函數`fn:avg (//r)`傳回靜態錯誤，因為 XQuery 編譯器無法將不同類型的值 (**xs: int**， **xs: float**或**xs:double**) 如 <`r`> 的引數中的項目**fn:avg()**。 若要解決這個問題，請將函數引動過程改寫成 `fn:avg(for $r in //r return $r cast as xs:double ?)`。  
  
### <a name="example-operator-over-union-type"></a>範例：聯集類型的運算子  
 加法運算 ('+') 需要精確的運算元類型。 因此，運算式 `(//r)[1] + 1` 會傳回靜態錯誤，其中含有前述之元素 <`r`> 的類型定義。 有一種解決方法，就是將它改寫成 `(//r)[1] cast as xs:int? +1`，其中 "?" 表示出現次數 0 或 1。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 需要 "cast as" 含有 "?"，因為任何轉換都可能會因執行階段錯誤，而造成空的序列。  
  
## <a name="see-also"></a>另請參閱  
 [XQuery 語言參考 &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)  
  
  
