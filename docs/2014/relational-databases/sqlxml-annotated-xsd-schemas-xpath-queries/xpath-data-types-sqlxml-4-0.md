---
title: XPath 資料類型（SQLXML 4.0） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 3cd2e8af1630fed8dd996a951e904bef0266b300
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/01/2020
ms.locfileid: "82702977"
---
# <a name="xpath-data-types-sqlxml-40"></a>XPath 資料類型 (SQLXML 4.0)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、XPath 和 XML 架構（XSD）具有非常不同的資料類型。 例如，XPath 沒有整數或日期資料類型，但是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 XSD 則有許多。 XSD 會將奈秒的有效位數用於時間值，而 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 則至多使用 1/300 秒的有效位數。 因此，並非永遠都能將一個資料類型對應到另一個。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將資料類型對應到 XSD 資料類型的詳細資訊，請參閱[資料類型強制型轉和 sql： datatype 注釋 &#40;SQLXML 4.0&#41;](../sqlxml-annotated-xsd-schemas-using/data-type-coercions-and-the-sql-datatype-annotation-sqlxml-4-0.md)。  
  
 XPath 具備三種資料類型：`string`、`number` 和 `boolean`。 `number` 資料類型永遠是 IEEE 754 雙精確度浮點數。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `float(53)` 資料類型是最接近的 XPath `number` 。 不過，`float(53)` 不完全是 IEEE 754。 例如，不會使用 NaN (非數字的值)，也不會使用無限。 嘗試將非數值字串轉換為 `number` 並嘗試除以零會導致錯誤。  
  
## <a name="xpath-conversions"></a>XPath 轉換  
 當您使用 XPath 查詢 (例如，`OrderDetail[@UnitPrice > "10.0"]`) 時，隱含和明確的資料類型轉換可能會以明顯的方式變更查詢的意義。 因此，了解如何實作 XPath 資料類型相當重要。 您可以在的 W3C 網站上找到 XPath 語言規格，XML 路徑語言（XPath）版本 1.0 W3C 提議的建議 8 1999 年10月 http://www.w3.org/TR/1999/PR-xpath-19991008.html 。  
  
 XPath 運算子分為四個類別：  
  
-   布林運算子 (and、or)  
  
-   關係運算子（ \< ，>， \< =，>=）  
  
-   相等運算子 (=、!=)  
  
-   算術運算子 (+、-、*、div、mod)  
  
 運算子的每個類別都會以不同的方式轉換其運算元。 如果必要，XPath 運算子會以隱含的方式轉換其運算元。 算術運算子會將其運算元轉換為 `number`，並成為數值。 布林運算子會將其運算元轉換為 `boolean`，並成為布林值。 關係運算子和相等運算子會成為布林值。 不過，根據其運算元的原始資料類型，它們擁有不同的轉換規則，如下表所示。  
  
|運算元|關聯式運算子|相等運算子|  
|-------------|-------------------------|-----------------------|  
|兩個運算元都是節點集。|只有在一個集合中有一個節點，而且在第二個集合中有一個節點，讓其 `string` 值的比較為 TRUE 時，才為 TRUE。|相同。|  
|一個是節點集，另一個是 `string`。|只有在節點集中有一個節點，因而轉換為 `number`，讓其與轉換為 `string` 之 `number` 的比較為 TRUE 時，才為 TRUE。|只有在節點集中有一個節點，因而轉換為 `string`，讓其與 `string` 的比較為 TRUE 時，才為 TRUE。|  
|一個是節點集，另一個是 `number`。|只有在節點集中有一個節點，因而轉換為 `number`，讓其與 `number` 的比較為 TRUE 時，才為 TRUE。|相同。|  
|一個是節點集，另一個是 `boolean`。|只有在節點集中有一個節點，因而轉換為 `boolean`，然後再轉換為 `number`，讓其與轉換為 `boolean` 之 `number` 的比較為 TRUE 時，才為 TRUE。|只有在節點集中有一個節點，因而轉換為 `boolean`，讓其與 `boolean` 的比較為 TRUE 時，才為 TRUE。|  
|都不是節點集。|將兩個運算元同時轉換為 `number`，然後進行比較。|將兩個運算元同時轉換為一般類型，然後進行比較。 如果其中一個是 `boolean`，轉換為 `boolean`，如果其中一個是 `number`，轉換為 `number`，否則，轉換為 `string`。|  
  
> [!NOTE]  
>  XPath 關係運算子會將其運算元一律轉換為 `number`，因此無法進行 `string` 比較。 若要加入日期比較，SQL Server 2000 會將此變數提供給 XPath 規格：當關係運算子將 `string` 與 `string` 相比較、將節點集與 `string` 相比較，或將兩個字串值節點集相比較時，會執行 `string` 比較 (而非 `number` 比較)。  
  
## <a name="node-set-conversions"></a>節點集轉換  
 節點集轉換並不一定直覺式。 藉由在節點集中只採用第一個節點的字串值，節點集就會轉換為 `string`。 節點集會轉換為 `number`，方法是，將其先轉換為 `string`，然後再將 `string` 轉換為 `number`。 系統會測試節點集是否存在，然後再轉換為 `boolean`。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不會在節點集上執行位置選取：例如，XPath 查詢 `Customer[3]` 表示第三個客戶；在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中不支援此種類型的位置選取。 因此，系統不會實作 XPath 規格所描述的節點集對 `string` 或節點集對 `number` 的轉換。 在 XPath 規格指定 "first" 語意的每個地方，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 都會使用 "any" 語意。 例如，根據 W3C XPath 規格，XPath 查詢 `Order[OrderDetail/@UnitPrice > 10.0]` 會選取具有大於10.0 之**單價**的第一個**OrderDetail**的訂單。 在中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，此 XPath 查詢會選取具有大於10.0 之**單價**的任何**OrderDetail**訂單。  
  
 轉換為 `boolean` 時，會產生存在測試，因此，XPath 查詢 `Products[@Discontinued=true()]` 相當於 SQL 運算式 "Products.Discontinued is not null"，而非 SQL 運算式 "Products.Discontinued = 1"。 為了讓查詢相當於後者的 SQL 運算式，請先將節點集轉換為非 `boolean` 類型，例如 `number`。 例如：`Products[number(@Discontinued) = true()]`。  
  
 對於節點集中的任何一個節點或其中一個節點，如果運算子為 TRUE，則大部分會定義為 TRUE，所以如果節點集是空的，這些運算永遠會評估為 FALSE。 因此，如果 A 是空的，`A = B` 和 `A != B` 都為 FALSE，而 `not(A=B)` 和 `not(A!=B)` 都為 TRUE。  
  
 如果資料庫中的資料行值不是 `null`，對應到該資料行的屬性或元素通常存在。 如果任何資料列的子系存在，則對應到那些資料列的元素存在。  
  
> [!NOTE]  
>  使用 `is-constant` 註解的元素永遠存在。 因此，無法在 `is-constant` 元素上使用 XPath 述詞。  
  
 當節點集轉換為 `string` 或 `number` 時，會在註解式結構描述中檢查其 XDR 類型 (如果有)，並使用該類型判斷所需的轉換。  
  
## <a name="mapping-xdr-data-types-to-xpath-data-types"></a>將 XDR 資料類型對應到 XPath 資料類型  
 節點的 XPath 資料類型衍生自架構中的 XDR 資料類型，如下表所示（節點的「**員工 id** 」用於說明用途）。  
  
|XDR 資料類型|對等用法<br /><br /> XPath 資料類型|使用的 SQL Server 轉換|  
|-------------------|------------------------------------|--------------------------------|  
|Nonebin.base64bin.hex|N/A|NoneEmployeeID|  
|boolean|boolean|CONVERT(bit, EmployeeID)|  
|number、int、float、i1、i2、i4、i8、r4、r8ui1、ui2、ui4、ui8|數字|CONVERT(float(53), EmployeeID)|  
|id、idref、idrefsentity、entities、enumerationnotation、nmtoken、nmtokens、chardate、Timedate、Time.tz、string、uri、uuid|字串|CONVERT(nvarchar(4000), EmployeeID, 126)|  
|fixed14.4|N/A (在 XPath 中沒有相當於 fixed14.4 XDR 資料類型的資料類型)|CONVERT(money, EmployeeID)|  
|date|字串|LEFT(CONVERT(nvarchar(4000), EmployeeID, 126), 10)|  
|time<br /><br /> time.tz|字串|SUBSTRING(CONVERT(nvarchar(4000), EmployeeID, 126), 1 + CHARINDEX(N'T', CONVERT(nvarchar(4000), EmployeeID, 126)), 24)|  
  
 日期和時間轉換的設計目的，是要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `datetime` 資料類型或，來處理值是否儲存在資料庫中 `string` 。 請注意， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `datetime` 資料類型不會使用 `timezone` ，而且具有比 XML 資料類型更小的有效位數 `time` 。 為包含 `timezone` 資料類型或其他有效位數，使用 `string` 類型，將資料儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中。  
  
 當節點從其 XDR 資料類型轉換為 XPath 資料類型時，有時候需要其他轉換 (從一個 XPath 資料類型轉換為另一個 XPath 資料類型)。 例如，請考量以下的 XPath 查詢：  
  
```  
(@m + 3) = 4  
```  
  
 如果 @m 屬於 `fixed14.4` xdr 資料類型，則會使用下列來完成從 xdr 資料類型轉換為 XPath 資料類型的作業：  
  
```  
CONVERT(money, m)  
```  
  
 在這個轉換中，節點 `m` 會從 `fixed14.4` 轉換為 `money`。 不過，加入 3 這個值需要其他轉換：  
  
```  
CONVERT(float(CONVERT(money, m))  
```  
  
 XPath 運算式會評估為：  
  
```  
CONVERT(float(CONVERT(money, m)) + CONVERT(float(53), 3) = CONVERT(float(53), 3)  
```  
  
 這與其他 XPath 運算式 (例如常值或複合運算式) 所套用的轉換相同，如下表所示。  
  
||||||  
|-|-|-|-|-|  
||X 不明|X 是 `string`|X 是 `number`|X 是 `boolean`|  
|string(X)|CONVERT (nvarchar(4000), X, 126)|-|CONVERT (nvarchar(4000), X, 126)|CASE WHEN X THEN N'true' ELSE N'false' END|  
|number(X)|CONVERT (float(53), X)|CONVERT (float(53), X)|-|CASE WHEN X THEN 1 ELSE 0 END|  
|boolean(X)|-|LEN （X） > 0|X。|-|  
  
## <a name="examples"></a>範例  
  
### <a name="a-convert-a-data-type-in-an-xpath-query"></a>A. 在 XPath 查詢中轉換資料類型  
 在針對批註式 XSD 架構指定的下列 XPath 查詢中，查詢會選取所有**具有 [#** #] 屬性值為 E-1 的**員工**節點，其中 "E-" 是使用注釋所指定的前置詞 `sql:id-prefix` 。  
  
 `Employee[@EmployeeID="E-1"]`  
  
 查詢中的述詞相當於 SQL 運算式：  
  
 `N'E-' + CONVERT(nvarchar(4000), Employees.EmployeeID, 126) = N'E-1'`  
  
 由於「**員工 id** 」是 `id` XSD 架構中的其中一個（ `idref` 、、、等等 `idrefs` `nmtoken` `nmtokens` ）資料類型值，因此**EmployeeID**會 `string` 使用先前所述的轉換規則，將「員工」轉換為 XPath 資料類型。  
  
 `CONVERT(nvarchar(4000), Employees.EmployeeID, 126)`  
  
 "E-" 前述詞會加入到字串，然後結果會與 `N'E-1'` 相比較。  
  
### <a name="b-perform-several-data-type-conversions-in-an-xpath-query"></a>B. 在 XPath 查詢中執行數個資料類型轉換  
 請考慮使用針對註解式 XSD 結構描述指定的這個 XPath 查詢：`OrderDetail[@UnitPrice * @OrderQty > 98]`  
  
 這個 XPath 查詢會傳回滿足述詞的所有** \< OrderDetail>** 元素 `@UnitPrice * @OrderQty > 98` 。 如果在**UnitPrice** `fixed14.4` 標注架構中使用資料類型來標注單價，則此述詞相當於 SQL 運算式：  
  
 `CONVERT(float(53), CONVERT(money, OrderDetail.UnitPrice)) * CONVERT(float(53), OrderDetail.OrderQty) > CONVERT(float(53), 98)`  
  
 在轉換 XPath 查詢中的值時，第一個轉換會先將 XDR 資料類型轉換為 XPath 資料類型。 因為「**單價**」的 XSD 資料類型是 `fixed14.4` （如上表所述），所以這是第一個使用的轉換：  
  
```  
CONVERT(money, OrderDetail.UnitPrice))   
```  
  
 算數運算子會將其運算元轉換為 `number` XPath 資料類型，因此會在值轉換為 `float(53)` (`float(53)` 接近 XPath `number` 資料類型) 之處套用第二個轉換 (從一個 XPath 資料類型轉換為另一個 XPath 資料類型)：  
  
```  
CONVERT(float(53), CONVERT(money, OrderDetail.UnitPrice))   
```  
  
 假設**orderqty**屬性沒有 XSD 資料類型，則會在單一轉換中將**orderqty**轉換成 `number` XPath 資料類型：  
  
```  
CONVERT(float(53), OrderDetail.OrderQty)  
```  
  
 同樣地，值 98 會轉換為 `number` XPath 資料類型：  
  
```  
CONVERT(float(53), 98)  
```  
  
> [!NOTE]  
>  如果在結構描述中使用的 XSD 資料類型與資料庫中的基礎 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型不相容，或者如果執行不可能的 XPath 資料類型轉換，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可能會傳回錯誤。 例如，如果將 [**員工**] 屬性標注為 [ `id-prefix` 注釋]，XPath 會 `Employee[@EmployeeID=1]` 產生錯誤，因為「**員工**」具有 `id-prefix` 批註，而且無法轉換成 `number` 。  
  
  
