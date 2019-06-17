---
title: XPath 資料類型 (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
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
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0c5cb588e96bcabad464339b7227ada3aef86221
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62678056"
---
# <a name="xpath-data-types-sqlxml-40"></a>XPath 資料類型 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、XPath 和 XML 結構描述 (XSD) 所擁有的資料類型非常不同。 例如，XPath 沒有整數或日期資料類型，但是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 XSD 則有許多。 XSD 會將奈秒的有效位數用於時間值，而 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 則至多使用 1/300 秒的有效位數。 因此，並非永遠都能將一個資料類型對應到另一個。 如需有關對應[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料類型到 XSD 資料類型，請參閱[資料類型強制型轉和 sql: datatype 註解&#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/data-type-coercions-and-the-sql-datatype-annotation-sqlxml-4-0.md)。  
  
 XPath 具備三種資料類型：**字串**，**數目**，並**布林**。 **數字**資料類型一定是 IEEE 754 雙精確度浮點數。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Float(53)** 資料類型是最接近 XPath**數目**。 不過， **float(53)** 不完全是 IEEE 754。 例如，不會使用 NaN (非數字的值)，也不會使用無限。 嘗試將非數字的字串來轉換**數字**並嘗試除以零產生錯誤。  
  
## <a name="xpath-conversions"></a>XPath 轉換  
 當您使用 XPath 查詢 (例如，`OrderDetail[@UnitPrice > "10.0"]`) 時，隱含和明確的資料類型轉換可能會以明顯的方式變更查詢的意義。 因此，了解如何實作 XPath 資料類型相當重要。 XPath 語言規格，XML 路徑語言 (XPath) 1.0 版，W3C 提出的建議 8 1999 年，請參閱 W3C 網站上 http://www.w3.org/TR/1999/PR-xpath-19991008.html 。  
  
 XPath 運算子分為四個類別：  
  
-   布林運算子 (and、or)  
  
-   關係運算子 (\<，>， \<=、 > =)  
  
-   相等運算子 (=、!=)  
  
-   算術運算子 (+、-、*、div、mod)  
  
 運算子的每個類別都會以不同的方式轉換其運算元。 如果必要，XPath 運算子會以隱含的方式轉換其運算元。 算術運算子轉換其運算元**數字**，和數字的值中的結果。 布林運算子進行轉換其運算元**布林**，和布林值的結果。 關係運算子和相等運算子會成為布林值。 不過，根據其運算元的原始資料類型，它們擁有不同的轉換規則，如下表所示。  
  
|運算元|關聯式運算子|相等運算子|  
|-------------|-------------------------|-----------------------|  
|兩個運算元都是節點集。|只有在一個集合中沒有節點，而且在第二個節點集這類，則為 TRUE。 該比較其**字串**值為 TRUE。|相同。|  
|其中一個是節點集，另**字串**。|才為節點集內沒有節點，則為 TRUE，當轉換成**數字**，比較它與**字串**轉換成**數目**為 TRUE，否則。|才為節點集內沒有節點，則為 TRUE，當轉換成**字串**，它使用的比較**字串**為 TRUE，否則。|  
|其中一個是節點集，另**數字**。|才為節點集內沒有節點，則為 TRUE，當轉換成**數字**，比較它與**數目**為 TRUE，否則。|相同。|  
|其中一個是節點集，另**布林**。|才為節點集內沒有節點，則為 TRUE，當轉換成**布林**然後**數目**，比較它與**布林**轉換成**數字**為 TRUE。|才為節點集內沒有節點，則為 TRUE，當轉換成**布林**，比較它與**布林**為 TRUE。|  
|都不是節點集。|轉換兩個運算元**數字**，然後進行比較。|將兩個運算元同時轉換為一般類型，然後進行比較。 轉換成**布林**如果任何一種**布林**，**數目**如果任何一種**數目**; 否則轉換成**字串**.|  
  
> [!NOTE]  
>  因為 XPath 關係運算子一律轉換其運算元**數字**，**字串**不能進行比較。 若要加入日期比較，SQL Server 2000 此變數提供給 XPath 規格：當關係運算子比較**字串**要**字串**的節點集**字串**，或字串值節點集字串值節點集， **字串**比較 (沒有**數字**比較) 會執行。  
  
## <a name="node-set-conversions"></a>節點集轉換  
 節點集轉換並不一定直覺式。 節點集轉換成**字串**採取集中的第一個節點的字串值。 節點集轉換成**數字**藉由將它轉換成**字串**，然後將轉換**字串**至**數目**。 節點集轉換成**布林**藉由測試它是否存在。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不會在節點集上執行位置選取：例如，XPath 查詢 `Customer[3]` 表示第三個客戶；在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中不支援此種類型的位置選取。 因此，節點-設定-到-**字串**或節點-設定-至-**數目**不會實作 XPath 規格所描述的轉換。 在 XPath 規格指定 "first" 語意的每個地方，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 都會使用 "any" 語意。 例如，根據 W3C XPath 規格，XPath 查詢`Order[OrderDetail/@UnitPrice > 10.0]`的第一個選取這些順序**OrderDetail**具有**UnitPrice**大於 10.0。 在  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，此 XPath 查詢會選取任何這些訂單**OrderDetail**具有**UnitPrice**大於 10.0。  
  
 轉換成**布林**會產生存在測試，因此，XPath 查詢`Products[@Discontinued=true()]`相當於 SQL 運算式"Products.Discontinued is not null"，不是 SQL 運算式"Products.Discontinued = 1"。 若要使查詢相當於後者的 SQL 運算式，第一次將轉換為節點集設為非**布林**類型，例如**數目**。 例如， `Products[number(@Discontinued) = true()]` 。  
  
 對於節點集中的任何一個節點或其中一個節點，如果運算子為 TRUE，則大部分會定義為 TRUE，所以如果節點集是空的，這些運算永遠會評估為 FALSE。 因此，如果 A 是空的，`A = B` 和 `A != B` 都為 FALSE，而 `not(A=B)` 和 `not(A!=B)` 都為 TRUE。  
  
 通常是，屬性或對應至資料行的項目存在，如果該資料庫中的資料行的值不是**null**。 如果任何資料列的子系存在，則對應到那些資料列的元素存在。  
  
> [!NOTE]  
>  項目將附註**是常數**永遠存在。 因此，XPath 述詞不能用在**是常數**項目。  
  
 當節點集轉換成**字串**或是**數目**、 註解式結構描述中檢查其 XDR 類型 （如果有的話），和該型別用來判斷所需要的轉換。  
  
## <a name="mapping-xdr-data-types-to-xpath-data-types"></a>將 XDR 資料類型對應到 XPath 資料類型  
 節點的 XPath 資料型別衍生自結構描述中的 XDR 資料類型下, 表所示 (節點**EmployeeID**用於說明用途)。  
  
|XDR 資料類型|對等用法<br /><br /> XPath 資料類型|使用的 SQL Server 轉換|  
|-------------------|------------------------------------|--------------------------------|  
|Nonebin.base64bin.hex|N/A|NoneEmployeeID|  
|boolean|boolean|CONVERT(bit, EmployeeID)|  
|number、int、float、i1、i2、i4、i8、r4、r8ui1、ui2、ui4、ui8|number|CONVERT(float(53), EmployeeID)|  
|id、idref、idrefsentity、entities、enumerationnotation、nmtoken、nmtokens、chardate、Timedate、Time.tz、string、uri、uuid|string|CONVERT(nvarchar(4000), EmployeeID, 126)|  
|fixed14.4|N/A (在 XPath 中沒有相當於 fixed14.4 XDR 資料類型的資料類型)|CONVERT(money, EmployeeID)|  
|日期|string|LEFT(CONVERT(nvarchar(4000), EmployeeID, 126), 10)|  
|time<br /><br /> time.tz|string|SUBSTRING(CONVERT(nvarchar(4000), EmployeeID, 126), 1 + CHARINDEX(N'T', CONVERT(nvarchar(4000), EmployeeID, 126)), 24)|  
  
 日期和時間轉換專為搭配值是儲存在資料庫中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **datetime**資料型別或**字串**。 請注意， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **datetime**資料類型不會使用**時區**且具有較小的有效位數比 XML**時間**資料型別。 若要包含**時區**資料類型或其他有效位數，將資料儲存在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用**字串**型別。  
  
 當節點從其 XDR 資料類型轉換為 XPath 資料類型時，有時候需要其他轉換 (從一個 XPath 資料類型轉換為另一個 XPath 資料類型)。 例如，請考量以下的 XPath 查詢：  
  
```  
(@m + 3) = 4  
```  
  
 如果@m屬於 **fixed14.4** XDR 資料類型，從 XDR 資料類型轉換為 XPath 資料型別使用來完成：  
  
```  
CONVERT(money, m)  
```  
  
 在此轉換中，節點`m`會從轉換**fixed14.4**要**money**。 不過，加入 3 這個值需要其他轉換：  
  
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
||X 不明|X 是**字串**|X 是**數目**|X 是**布林**|  
|string(X)|CONVERT (nvarchar(4000), X, 126)|-|CONVERT (nvarchar(4000), X, 126)|CASE WHEN X THEN N'true' ELSE N'false' END|  
|number(X)|CONVERT (float(53), X)|CONVERT (float(53), X)|-|CASE WHEN X THEN 1 ELSE 0 END|  
|boolean(X)|-|LEN(X) > 0|X。|-|  
  
## <a name="examples"></a>範例  
  
### <a name="a-convert-a-data-type-in-an-xpath-query"></a>A. 在 XPath 查詢中轉換資料類型  
 在針對註解式 XSD 結構描述指定的下列 XPath 查詢，查詢會選取所有**員工**具備**EmployeeID**屬性利用 E-1，其中"E-"是使用指定的前置詞的值**sql: id-prefix-前置詞**註釋。  
  
 `Employee[@EmployeeID="E-1"]`  
  
 查詢中的述詞相當於 SQL 運算式：  
  
 `N'E-' + CONVERT(nvarchar(4000), Employees.EmployeeID, 126) = N'E-1'`  
  
 因為**EmployeeID**是其中一個**識別碼**(**idref**， **idrefs**， **nmtoken**， **nmtokens**等等) 資料類型值在 XSD 結構描述**EmployeeID**轉換成**字串**使用先前所述的轉換規則的 XPath 資料類型。  
  
 `CONVERT(nvarchar(4000), Employees.EmployeeID, 126)`  
  
 "E-" 前述詞會加入到字串，然後結果會與 `N'E-1'` 相比較。  
  
### <a name="b-perform-several-data-type-conversions-in-an-xpath-query"></a>B. 在 XPath 查詢中執行數個資料類型轉換  
 請考慮使用針對註解式 XSD 結構描述指定的這個 XPath 查詢：`OrderDetail[@UnitPrice * @OrderQty > 98]`  
  
 此 XPath 查詢會傳回所有 **\<OrderDetail >** 滿足述詞的項目`@UnitPrice * @OrderQty > 98`。 如果**UnitPrice**附註**fixed14.4**資料類型的註解式結構描述，此述詞相當於 SQL 運算式：  
  
 `CONVERT(float(53), CONVERT(money, OrderDetail.UnitPrice)) * CONVERT(float(53), OrderDetail.OrderQty) > CONVERT(float(53), 98)`  
  
 在轉換 XPath 查詢中的值時，第一個轉換會先將 XDR 資料類型轉換為 XPath 資料類型。 因為 XSD 資料類型**UnitPrice**是**fixed14.4**，如上表所述，這是所使用的第一個轉換：  
  
```  
CONVERT(money, OrderDetail.UnitPrice))   
```  
  
 因為算術的運算子轉換其運算元**數字**XPath 資料類型，第二個 （一個 XPath 資料類型轉換成另一個 XPath 資料類型） 會套用在其值會轉換成**float(53)** (**float(53)** 接近 XPath**數目**資料類型):  
  
```  
CONVERT(float(53), CONVERT(money, OrderDetail.UnitPrice))   
```  
  
 假設**OrderQty**屬性有任何 XSD 資料型別中， **OrderQty**轉換成**數目**單一轉換中的 XPath 資料類型：  
  
```  
CONVERT(float(53), OrderDetail.OrderQty)  
```  
  
 同樣地，值 98 會轉換成**數字**XPath 資料類型：  
  
```  
CONVERT(float(53), 98)  
```  
  
> [!NOTE]  
>  如果在結構描述中使用的 XSD 資料類型與資料庫中的基礎 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型不相容，或者如果執行不可能的 XPath 資料類型轉換，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可能會傳回錯誤。 例如，如果**EmployeeID**附註屬性**識別碼首碼**註解，XPath`Employee[@EmployeeID=1]`會產生錯誤，因為**EmployeeID**具有**識別碼首碼**註解，所以無法轉換成**數目**。  
  
  
