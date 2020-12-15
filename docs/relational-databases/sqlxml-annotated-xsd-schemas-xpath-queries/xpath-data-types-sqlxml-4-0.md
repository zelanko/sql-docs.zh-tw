---
title: " (SQLXML) 的 XPath 資料類型"
description: 瞭解 SQLXML 4.0 中的 XPath 資料類型，以及它們與 Microsoft SQL Server 和 XML 架構 (XSD) 資料類型的比較方式。
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- mapping XDR types to XPath types [SQLXML]
- data types [XPath]
- arithmetic operators
- mapping data types [SQLXML]
- relational operators [SQLXML]
- node-set [SQLXML]
- data types [SQLXML], XPath
- XPath operators [SQLXML]
- XDR data type [SQLXML]
- equality operators [SQLXML]
- XPath conversions [SQLXML]
- converting data types [SQLXML]
- Boolean operators
- XPath queries [SQLXML], data types
- XPath data types [SQLXML]
- operators [SQLXML]
ms.assetid: a90374bf-406f-4384-ba81-59478017db68
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 15b308481b6622284d6f8bdd36d474b3886570d6
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97460038"
---
# <a name="xpath-data-types-sqlxml-40"></a>XPath 資料類型 (SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、XPath 和 XML 架構 (XSD) 具有非常不同的資料類型。 例如，XPath 沒有整數或日期資料類型，但是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 XSD 則有許多。 XSD 會將奈秒的有效位數用於時間值，而 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 則至多使用 1/300 秒的有效位數。 因此，並非永遠都能將一個資料類型對應到另一個。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將資料類型對應至 XSD 資料類型的詳細資訊，請參閱 [資料類型強制和 sql： datatype 注釋 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/data-type-coercions-and-the-sql-datatype-annotation-sqlxml-4-0.md)。  
  
 XPath 有三種資料類型： **字串**、 **數位** 和 **布林值**。 **Number** 資料類型一律為 IEEE 754 雙精確度浮點數。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Float (53)** 資料類型是最接近 XPath **數位** 的資料類型。 不過， **float (53)** 並不完全是 IEEE 754。 例如，不會使用 NaN (非數字的值)，也不會使用無限。 嘗試將非數值字串轉換成 **數位** ，並嘗試零除會導致錯誤。  
  
## <a name="xpath-conversions"></a>XPath 轉換  
 當您使用 XPath 查詢 (例如，`OrderDetail[@UnitPrice > "10.0"]`) 時，隱含和明確的資料類型轉換可能會以明顯的方式變更查詢的意義。 因此，了解如何實作 XPath 資料類型相當重要。  (XPath 的 XPath 語言規格、XML 路徑語言 XPath) 1.0 版 W3C 建議的建議 8 1999，可在 W3C 網站上找到 http://www.w3.org/TR/1999/PR-xpath-19991008.html 。  
  
 XPath 運算子分為四個類別：  
  
-   布林運算子 (and、or)  
  
-   關聯式運算子 (\<, > ， \<=, > =)   
  
-   相等運算子 (=、!=)  
  
-   算術運算子 (+、-、*、div、mod)  
  
 運算子的每個類別都會以不同的方式轉換其運算元。 如果必要，XPath 運算子會以隱含的方式轉換其運算元。 算術運算子會將其運算元轉換為 **數位**，並產生數位值。 布林運算子會將其運算元轉換為 **布林** 值，並產生布林值。 關係運算子和相等運算子會成為布林值。 不過，根據其運算元的原始資料類型，它們擁有不同的轉換規則，如下表所示。  
  
|運算元|關聯式運算子|等號比較運算子|  
|-------------|-------------------------|-----------------------|  
|兩個運算元都是節點集。|如果只有在一個集合中有一個節點，而第二個集合中有一個節點，使其 **字串** 值的比較為 true 時，才為 true。|相同。|  
|其中一個是節點集，另一個則是 **字串**。|若為 TRUE，則只有在節點集中有一個節點，因而將它轉換為 **數位** 時，才會將它與轉換為 **數位** 的 **字串** 進行比較是 true。|如果只有在節點集中有一個節點，而且在轉換成 **字串** 時，它與 **字串** 的比較結果為 TRUE，則為 true。|  
|其中一個是節點集，另一個則是 **數位**。|如果只有在節點集中有一個節點，而且在轉換為 **數位** 時，才會將它與 **數位** 的比較結果為 TRUE，則為 true。|相同。|  
|其中一個是節點集，另一個是 **布林值**。|如果只有在節點集中有一個節點，而將它轉換成 **布林值**，然後再轉換為 **數位**，則會將它與轉換為 **數位** 的 **布林值** 進行比較，以符合 true。|如果只有在節點集中有一個節點，讓它轉換成 **布林值**，且其與 **布林** 值的比較為 TRUE 時，才為 true。|  
|都不是節點集。|將兩個運算元轉換成 **number** ，然後比較。|將兩個運算元同時轉換為一般類型，然後進行比較。 如果任一個是 **布林值**，則轉換成 **布林值**，如果其中一個是 **數位**，則為 **數位** 否則，請轉換成 **字串**。|  
  
> [!NOTE]  
>  由於 XPath 關聯式運算子一律會將其運算元轉換為 **數位**，因此不可能進行 **字串** 比較。 若要包含日期比較，SQL Server 2000 會將這種變化提供給 XPath 規格：當關聯式運算子將 **字串** 與 **字串、將** 節點設定為字串，或將字串值節點集設定為字串值節點集 **時，****字串** 比較 (不會執行 **數位** 比較) 。  
  
## <a name="node-set-conversions"></a>節點集轉換  
 節點集轉換並不一定直覺式。 節點集會轉換成 **字串** ，方法是只採用集合中第一個節點的字串值。 節點集會轉換成 **字串**，然後將 **字串** 轉換成 **數位**，以轉換成 **數位**。 節點集會藉由測試是否存在來轉換成 **布林值** 。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不會在節點集上執行位置選取：例如，XPath 查詢 `Customer[3]` 表示第三個客戶；在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中不支援此種類型的位置選取。 因此，不會實作為 XPath 規格所描述的節點集對 **字串** 或節點集對 **數位** 的轉換。 在 XPath 規格指定 "first" 語意的每個地方，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 都會使用 "any" 語意。 例如，根據 W3C XPath 規格，XPath 查詢 `Order[OrderDetail/@UnitPrice > 10.0]` 會使用 **單價** 大於10.0 的第一個 **OrderDetail** 來選取這些訂單。 在中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，此 XPath 查詢會使用 **單價** 大於10.0 的 **OrderDetail** 來選取這些訂單。  
  
 轉換成 **布林值** 會產生存在測試;因此，XPath 查詢 `Products[@Discontinued=true()]` 相當於 sql 運算式「產品。已中止不是 null」，而不是 sql 運算式「products. 已停止 = 1」。 若要讓查詢相當於後者的 SQL 運算式，請先將節點集轉換為非 **布林值** 類型，例如 **number**。 例如，`Products[number(@Discontinued) = true()]`。  
  
 對於節點集中的任何一個節點或其中一個節點，如果運算子為 TRUE，則大部分會定義為 TRUE，所以如果節點集是空的，這些運算永遠會評估為 FALSE。 因此，如果 A 是空的，`A = B` 和 `A != B` 都為 FALSE，而 `not(A=B)` 和 `not(A!=B)` 都為 TRUE。  
  
 如果資料庫中該資料行的值不是 **null**，通常會有對應至資料行的屬性或元素。 如果任何資料列的子系存在，則對應到那些資料列的元素存在。  
  
> [!NOTE]  
>  以 **-常數** 標注的元素一律會存在。 因此，XPath 述詞不能用在 **常數** 元素上。  
  
 當節點集轉換成 **字串** 或 **數位** 時，如果在批註式架構中檢查任何) ，而且該型別是用來判斷所需的轉換，則它的 XDR 型別 (。  
  
## <a name="mapping-xdr-data-types-to-xpath-data-types"></a>將 XDR 資料類型對應到 XPath 資料類型  
 節點的 XPath 資料類型衍生自架構中的 XDR 資料類型，如下表所示 **(節點擁有** 者用於說明目的) 。  
  
|XDR 資料類型|對等用法<br /><br /> XPath 資料類型|使用的 SQL Server 轉換|  
|-------------------|------------------------------------|--------------------------------|  
|Nonebin.base64bin.hex|N/A|NoneEmployeeID|  
|boolean|boolean|CONVERT(bit, EmployeeID)|  
|number、int、float、i1、i2、i4、i8、r4、r8ui1、ui2、ui4、ui8|數目|CONVERT(float(53), EmployeeID)|  
|id、idref、idrefsentity、entities、enumerationnotation、nmtoken、nmtokens、chardate、Timedate、Time.tz、string、uri、uuid|字串|CONVERT(nvarchar(4000), EmployeeID, 126)|  
|fixed14.4|N/A (在 XPath 中沒有相當於 fixed14.4 XDR 資料類型的資料類型)|CONVERT(money, EmployeeID)|  
|date|字串|LEFT(CONVERT(nvarchar(4000), EmployeeID, 126), 10)|  
|time<br /><br /> time.tz|字串|SUBSTRING(CONVERT(nvarchar(4000), EmployeeID, 126), 1 + CHARINDEX(N'T', CONVERT(nvarchar(4000), EmployeeID, 126)), 24)|  
  
 日期和時間轉換的設計目的，是要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **datetime** 資料類型或 **字串**，將值儲存在資料庫中。 請注意， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **datetime** 資料類型不會使用 **時區**，而且比 XML **時間** 資料類型的有效位數較小。 若要包含 **時區** 資料類型或其他有效位數，請 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用 **字串** 類型將資料儲存在中。  
  
 當節點從其 XDR 資料類型轉換為 XPath 資料類型時，有時候需要其他轉換 (從一個 XPath 資料類型轉換為另一個 XPath 資料類型)。 例如，請考量以下的 XPath 查詢：  
  
```  
(@m + 3) = 4  
```  
  
 如果 @m 是固定的 **14.4** XDR 資料類型，則會使用下列方式來完成從 XDR 資料類型到 XPath 資料類型的轉換：  
  
```  
CONVERT(money, m)  
```  
  
 在此轉換中，節點 `m` 會從 **固定的 14.4** 轉換成 **money**。 不過，加入 3 這個值需要其他轉換：  
  
```  
CONVERT(float(CONVERT(money, m))  
```  
  
 XPath 運算式會評估為：  
  
```  
CONVERT(float(CONVERT(money, m)) + CONVERT(float(53), 3) = CONVERT(float(53), 3)  
```  
  
 這與其他 XPath 運算式 (例如常值或複合運算式) 所套用的轉換相同，如下表所示。  
  
|   | X 不明 | X 是字串 | X 是數位 | X 是布林值 |
| - | ------------ | ----------- | ----------- | ------------ |
| **string(X)** |CONVERT (nvarchar(4000), X, 126)|-|CONVERT (nvarchar(4000), X, 126)|CASE WHEN X THEN N'true' ELSE N'false' END|  
| **number(X)** |CONVERT (float(53), X)|CONVERT (float(53), X)|-|CASE WHEN X THEN 1 ELSE 0 END|  
| **boolean(X)** |-|LEN (X) > 0|X。|-|  
  
## <a name="examples"></a>範例  
  
### <a name="a-convert-a-data-type-in-an-xpath-query"></a>A. 在 XPath 查詢中轉換資料類型  
 在針對批註式 XSD 架構指定的下列 XPath 查詢中，查詢會選取 [Employee] 屬性值為 E- **1 的所有****員工** 節點，其中 "e-" 是使用 **sql： id-prefix** 注釋指定的前置詞。  
  
 `Employee[@EmployeeID="E-1"]`  
  
 查詢中的述詞相當於 SQL 運算式：  
  
 `N'E-' + CONVERT(nvarchar(4000), Employees.EmployeeID, 126) = N'E-1'`  
  
 因為 [ **雇員** 識別碼] 是其中一個 **識別碼** (**idref**、 **idrefs**、 **nmtoken**、 **nmtokens** 等) 資料類型值，所以在 XSD 架構中，會使用先前所述的轉換規則，將 [ **雇員** 識別碼] 轉換成 **字串** XPath 資料類型。  
  
 `CONVERT(nvarchar(4000), Employees.EmployeeID, 126)`  
  
 "E-" 前述詞會加入到字串，然後結果會與 `N'E-1'` 相比較。  
  
### <a name="b-perform-several-data-type-conversions-in-an-xpath-query"></a>B. 在 XPath 查詢中執行數個資料類型轉換  
 請考慮使用針對註解式 XSD 結構描述指定的這個 XPath 查詢：`OrderDetail[@UnitPrice * @OrderQty > 98]`  
  
 此 XPath 查詢會傳回滿足述詞的所有 **\<OrderDetail>** 元素 `@UnitPrice * @OrderQty > 98` 。 如果在批註式架構中以 **固定的 14.4** 資料類型標注 **單價**，則此述詞相當於 SQL 運算式：  
  
 `CONVERT(float(53), CONVERT(money, OrderDetail.UnitPrice)) * CONVERT(float(53), OrderDetail.OrderQty) > CONVERT(float(53), 98)`  
  
 在轉換 XPath 查詢中的值時，第一個轉換會先將 XDR 資料類型轉換為 XPath 資料類型。 因為 **單價** 的 XSD 資料類型是 **固定的 14.4**（如上表所述），所以這是第一個使用的轉換：  
  
```  
CONVERT(money, OrderDetail.UnitPrice))   
```  
  
 因為算術運算子會將其運算元轉換成 **number** XPath 資料類型，所以第二個轉換 (從一個 xpath 資料類型轉換成另一個 xpath 資料類型，) 會套用該值轉換成 **float (53)** (**Float (53)** 接近 XPath **number** 資料類型) ：  
  
```  
CONVERT(float(53), CONVERT(money, OrderDetail.UnitPrice))   
```  
  
 假設 **orderqty** 屬性沒有 XSD 資料類型，則會在單一轉換中將 **orderqty** 轉換成 **數值** XPath 資料類型：  
  
```  
CONVERT(float(53), OrderDetail.OrderQty)  
```  
  
 同樣地，值98會轉換成 **數位** XPath 資料類型：  
  
```  
CONVERT(float(53), 98)  
```  
  
> [!NOTE]  
>  如果在結構描述中使用的 XSD 資料類型與資料庫中的基礎 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型不相容，或者如果執行不可能的 XPath 資料類型轉換，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可能會傳回錯誤。 例如，**如果 [擁有** 者] 屬性是以 **識別碼首碼** 批註批註，XPath 會 `Employee[@EmployeeID=1]` 產生錯誤，因為 [ 擁有者] 具有 **識別碼前置** 注釋，而且無法轉換成 **數位**。  
  
  
