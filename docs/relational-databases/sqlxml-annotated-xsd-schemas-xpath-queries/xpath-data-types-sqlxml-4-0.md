---
title: XPath 資料型態 (SQLXML)
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
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 089b2b006d0159c63e480c8627762ac37dec98b8
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/15/2020
ms.locfileid: "75247094"
---
# <a name="xpath-data-types-sqlxml-40"></a>XPath 資料類型 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)],XPath 和 XML 架構 (XSD) 的數據類型非常不同。 例如，XPath 沒有整數或日期資料類型，但是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 XSD 則有許多。 XSD 會將奈秒的有效位數用於時間值，而 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 則至多使用 1/300 秒的有效位數。 因此，並非永遠都能將一個資料類型對應到另一個。 有關將資料類型對應到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]XSD 資料類型的詳細資訊,請參閱[資料類型強制和 sql:資料類型註解&#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/data-type-coercions-and-the-sql-datatype-annotation-sqlxml-4-0.md)。  
  
 XPath 有三種資料類型:**字串**,**數字**和**布林。** **數位**資料類型始終為 IEEE 754 雙精度浮點。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**浮點(53)** 資料型態最接近 XPath**編號**。 但是,**浮點 (53)** 不完全是 IEEE 754。 例如，不會使用 NaN (非數字的值)，也不會使用無限。 嘗試將非數位字串轉換為**數位**並嘗試除以零會導致錯誤。  
  
## <a name="xpath-conversions"></a>XPath 轉換  
 當您使用 XPath 查詢 (例如，`OrderDetail[@UnitPrice > "10.0"]`) 時，隱含和明確的資料類型轉換可能會以明顯的方式變更查詢的意義。 因此，了解如何實作 XPath 資料類型相當重要。 XPath 語言規範,XML 路徑語言 (XPath) 版本 1.0 W3C 建議http://www.w3.org/TR/1999/PR-xpath-19991008.html1999 年 10 月 8 日,可在 W3C 網站找到。  
  
 XPath 運算子分為四個類別：  
  
-   布林運算子 (and、or)  
  
-   關係運算符(、>、*、>\< \<*)  
  
-   相等運算子 (=、!=)  
  
-   算術運算子 (+、-、*、div、mod)  
  
 運算子的每個類別都會以不同的方式轉換其運算元。 如果必要，XPath 運算子會以隱含的方式轉換其運算元。 算術運算符將其操作數轉換為**數位**,併產生數位值。 布爾運算子將其操作數轉換為**布林,** 並產生布林值。 關係運算子和相等運算子會成為布林值。 不過，根據其運算元的原始資料類型，它們擁有不同的轉換規則，如下表所示。  
  
|運算元|關聯式運算子|相等運算子|  
|-------------|-------------------------|-----------------------|  
|兩個運算元都是節點集。|如果僅在一個集中有一個節點和第二個集中有一個節點,以便比較其**字串值**為 TRUE 時,才具有 TRUE。|相同。|  
|是節點集,另一個是**字串**。|TRUE,如果並且僅當節點集中有一個節點,這樣當轉換為**數位**時,它與轉換為**數位**的**字串**的比較才為 TRUE。|TRUE,如果並且僅當節點集中有一個節點,因此當轉換為**字串**時,它與**字串**的比較是 TRUE。|  
|是節點集,另一個是**數字**。|TRUE,如果並且僅當節點集中有一個節點,這樣當轉換為**數位**時,它與**數字**的比較才為 TRUE。|相同。|  
|一個是節點集,另一個是**布爾。**|TRUE,如果並且僅當節點集中有一個節點,這樣當轉換為**布爾**,然後轉換為**數位**時,它與轉換為**數位**的**布爾**的比較才為 TRUE。|TRUE,如果並且僅當節點集中有一個節點,這樣當轉換為**布爾**時,它與**布爾**的比較才是真實的。|  
|都不是節點集。|將兩個操作數轉換為**數位**,然後進行比較。|將兩個運算元同時轉換為一般類型，然後進行比較。 如果任一是布林,則轉換為布林,如果任**一數位為**「布林 **」 ,****則為 「布林」;** 如果任一數位,則為**布林**。否則,轉換為**字串**。|  
  
> [!NOTE]  
>  由於 XPath 關係運算子始終將其操作數轉換為**數位**,因此無法進行**字串**比較。 為了包括日期比較,SQL Server 2000 提供了與 XPath 規範的此變體:當關係運算元將**字串**與**字串**進行比較時,將節點集與**字串**進行比較,或者將字串值節點集與字串值節點集進行比較,則執行**字串**比較(而不是**數位**比較)。  
  
## <a name="node-set-conversions"></a>節點集轉換  
 節點集轉換並不一定直覺式。 將節點集取得集中第一個節點的字串值轉換為**字串**。 將節點集會將**字串轉換為字串**, 然後將**字串**轉換為數字,將其轉換為**number****數位**。 節點集通過測試其存在轉換為**布爾。**  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不會在節點集上執行位置選取：例如，XPath 查詢 `Customer[3]` 表示第三個客戶；在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中不支援此種類型的位置選取。 因此,不實現 XPath 規範描述的節點集到**字串**或節點集到**數**轉換。 在 XPath 規格指定 "first" 語意的每個地方，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 都會使用 "any" 語意。 例如,基於 W3C XPath 規範,XPath 查詢`Order[OrderDetail/@UnitPrice > 10.0]`選擇具有**單價**大於 10.0 的第一**個訂單詳細資訊**的訂單。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中,此 XPath 查詢選擇具有**單價**大於 10.0 的任何**訂單詳細資訊**的訂單。  
  
 轉換為**布爾**生成存在測試;因此,XPath`Products[@Discontinued=true()]`查詢等效於 SQL 運算式「產品.已停產不是空」,而不是 SQL 運算式「產品.已停產 = 1」。。 要使查詢等效於後者 SQL 表示式,請先將節點集轉換為非**布林**型態,如**數位**。 例如： `Products[number(@Discontinued) = true()]` 。  
  
 對於節點集中的任何一個節點或其中一個節點，如果運算子為 TRUE，則大部分會定義為 TRUE，所以如果節點集是空的，這些運算永遠會評估為 FALSE。 因此，如果 A 是空的，`A = B` 和 `A != B` 都為 FALSE，而 `not(A=B)` 和 `not(A!=B)` 都為 TRUE。  
  
 通常,如果資料庫中該列的值不**為空**,則存在映射到列的屬性或元素。 如果任何資料列的子系存在，則對應到那些資料列的元素存在。  
  
> [!NOTE]  
>  帶有**正常量**的帶號表示的元素始終存在。 因此,XPath 謂詞不能用於**常量**元素。  
  
 當節點集轉換為**字串**或**數位**時,其 XDR 類型(如果有)在批帶的架構中檢查,該類型用於確定所需的轉換。  
  
## <a name="mapping-xdr-data-types-to-xpath-data-types"></a>將 XDR 資料類型對應到 XPath 資料類型  
 節點的 XPath 資料類型派生自架構中的 XDR 資料類型,如下表所示(節點**EmployID**用於說明目的)。  
  
|XDR 資料類型|對等用法<br /><br /> XPath 資料類型|使用的 SQL Server 轉換|  
|-------------------|------------------------------------|--------------------------------|  
|Nonebin.base64bin.hex|N/A|NoneEmployeeID|  
|boolean|boolean|CONVERT(bit, EmployeeID)|  
|number、int、float、i1、i2、i4、i8、r4、r8ui1、ui2、ui4、ui8|number|CONVERT(float(53), EmployeeID)|  
|id、idref、idrefsentity、entities、enumerationnotation、nmtoken、nmtokens、chardate、Timedate、Time.tz、string、uri、uuid|字串|CONVERT(nvarchar(4000), EmployeeID, 126)|  
|fixed14.4|N/A (在 XPath 中沒有相當於 fixed14.4 XDR 資料類型的資料類型)|CONVERT(money, EmployeeID)|  
|date|字串|LEFT(CONVERT(nvarchar(4000), EmployeeID, 126), 10)|  
|time<br /><br /> time.tz|字串|SUBSTRING(CONVERT(nvarchar(4000), EmployeeID, 126), 1 + CHARINDEX(N'T', CONVERT(nvarchar(4000), EmployeeID, 126)), 24)|  
  
 日期和時間轉換旨在處理該值是否使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**日期時間**資料類型或**字串**儲存在資料庫中。 請注意,[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**日期時間**資料類型不使用**時區**,其精度比 XML**時間**數據類型小。 要包括**時區**數據類型或其他精度,[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]請使用**字串**類型將數據存儲在其中。  
  
 當節點從其 XDR 資料類型轉換為 XPath 資料類型時，有時候需要其他轉換 (從一個 XPath 資料類型轉換為另一個 XPath 資料類型)。 例如，請考量以下的 XPath 查詢：  
  
```  
(@m + 3) = 4  
```  
  
 如果是@m**固定 14.4** XDR 資料類型,則使用以下途徑完成從 XDR 資料類型轉換為 XPath 資料類型的轉換:  
  
```  
CONVERT(money, m)  
```  
  
 在這裡轉換中,節點`m`從固定**14.4**轉換為**金錢**。 不過，加入 3 這個值需要其他轉換：  
  
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
||X 不明|X 是**字串**|X 是**數字**|X 是**布林**|  
|string(X)|CONVERT (nvarchar(4000), X, 126)|-|CONVERT (nvarchar(4000), X, 126)|CASE WHEN X THEN N'true' ELSE N'false' END|  
|number(X)|CONVERT (float(53), X)|CONVERT (float(53), X)|-|CASE WHEN X THEN 1 ELSE 0 END|  
|boolean(X)|-|LEN(X) > 0|X。|-|  
  
## <a name="examples"></a>範例  
  
### <a name="a-convert-a-data-type-in-an-xpath-query"></a>A. 在 XPath 查詢中轉換資料類型  
 在以下針對帶註釋的 XSD 架構指定的 XPath 查詢中,該查詢選擇所有**員工**節點,其員工**ID**屬性值為 E-1,其中「E-」是使用**sql:id 前置**字註釋指定的前置碼。  
  
 `Employee[@EmployeeID="E-1"]`  
  
 查詢中的述詞相當於 SQL 運算式：  
  
 `N'E-' + CONVERT(nvarchar(4000), Employees.EmployeeID, 126) = N'E-1'`  
  
 由於**EmployID**是 XSD 架構中的**id**id(idref、idrefs、nmtoken、nmtokens 等)數據類型值之一,因此使用**idrefs**前面描述的轉換規則將**Employid**轉換為**idref****nmtoken****nmtokens****字串**XPath 數據類型。  
  
 `CONVERT(nvarchar(4000), Employees.EmployeeID, 126)`  
  
 "E-" 前述詞會加入到字串，然後結果會與 `N'E-1'` 相比較。  
  
### <a name="b-perform-several-data-type-conversions-in-an-xpath-query"></a>B. 在 XPath 查詢中執行數個資料類型轉換  
 請考慮使用針對註解式 XSD 結構描述指定的這個 XPath 查詢：`OrderDetail[@UnitPrice * @OrderQty > 98]`  
  
 此 XPath 查詢返回滿足`@UnitPrice * @OrderQty > 98`謂詞 的所有**\<Order 詳細資訊>** 元素。 如果在註解的架構中用**固定 14.4**資料類型註釋**UnitPrice,** 則此謂詞等效於 SQL 表示式:  
  
 `CONVERT(float(53), CONVERT(money, OrderDetail.UnitPrice)) * CONVERT(float(53), OrderDetail.OrderQty) > CONVERT(float(53), 98)`  
  
 在轉換 XPath 查詢中的值時，第一個轉換會先將 XDR 資料類型轉換為 XPath 資料類型。 由於**UnitPrice**的 XSD 資料類型是固定的**14.4**,如上表中所述,這是使用的第一個轉換:  
  
```  
CONVERT(money, OrderDetail.UnitPrice))   
```  
  
 由於算術運算符將其操作數轉換為**數位**XPath 資料類型,因此應用第二次轉換(從一個 XPath 資料類型轉換為另一個 XPath 資料類型),其中將值轉換為**float(53)** **(float(53)** 接近 XPath**數位**資料類型):  
  
```  
CONVERT(float(53), CONVERT(money, OrderDetail.UnitPrice))   
```  
  
 假設**OrderQty**屬性沒有 XSD 資料型態,**則 OrderQty**在單個轉換中轉換為**數位**XPath 資料型態:  
  
```  
CONVERT(float(53), OrderDetail.OrderQty)  
```  
  
 同樣,值 98 將轉換為**數位**XPath 資料類型:  
  
```  
CONVERT(float(53), 98)  
```  
  
> [!NOTE]  
>  如果在結構描述中使用的 XSD 資料類型與資料庫中的基礎 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型不相容，或者如果執行不可能的 XPath 資料類型轉換，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可能會傳回錯誤。 例如, 如果**EmployID**屬性使用**id 前置**註解進行`Employee[@EmployeeID=1]`註解,則 XPath 將產生錯誤,因為**EmployID**具有**id 前置,** 無法轉換為**數位**。  
  
  
