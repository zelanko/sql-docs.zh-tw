---
title: 中的類型轉換規則 XQuery |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- XQuery, type casting
- casting rules [XML in SQL Server]
- explicit casting [SQL Server]
- type casting rules [XML in SQL Server]
- cast as operator
- implicit casting
ms.assetid: f2e91306-2b1b-4e1c-b6d8-a34fb9980057
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 352d6be6f924fc8285a25d3f83ef5bee74c03acb
ms.sourcegitcommit: bfa10c54e871700de285d7f819095d51ef70d997
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/14/2019
ms.locfileid: "54254673"
---
# <a name="type-casting-rules-in-xquery"></a>XQuery 中的類型轉換規則
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  下列 W3C XQuery 1.0 與 XPath 2.0 函數與運算子規格圖表顯示內建資料類型。 這包含內建基本類型與內建衍生類型。  
  
 ![XQuery 1.0 類型階層](../xquery/media/xquery-typing-rules.gif "XQuery 1.0 類型階層")  
  
 本主題說明使用下列其中一種方法，從一種類型轉換成另一種類型時，所套用的類型轉換規則：  
  
-   您可以使用明確轉換**轉換為**或 型別建構函式 (例如`xs:integer("5")`)。  
  
-   在類型升級期間所執行的隱含轉換  
  
## <a name="explicit-casting"></a>明確轉換  
 下表概略說明內建基本類型之間允許的類型轉換。  
  
 ![描述 XQuery 的轉換規則。](../xquery/media/casting-builtin-types.gif "描述 XQuery 的轉換規則。")  
  
-   根據表格中的規則，內建基本類型可轉換成另一個內建基本類型。  
  
-   基本類型可以轉換成從該基本類型所衍生的任何類型。 例如，您可以將轉換成**xs: decimal**要**xs: integer**，或從**xs: decimal**至**xs: long**。  
  
-   衍生類型可以轉換成類型階層中為其上階的任何類型，並可一直轉換至其內建基本基底類型。 例如，您可以將轉換成**xs: token**要**xs: normalizedstring**上，或者**xs: string**。  
  
-   如果其基本上階可轉換成目標類型，則衍生類型就可轉換成基本類型。 例如，您可以轉型**xs: integer**的衍生類型**xs: string**基本類型，因為**xs: decimal**， **xs: integer**的基本的上階可轉換成**xs: string**。  
  
-   如果原始類型的基本上階可以轉換成目標類型的基本上階，則衍生類型就可轉換成另一個衍生類型。 例如，您可以將轉換成**xs: integer**要**xs: token**，因為您可以將轉換成**xs: decimal**至**xs: string**。  
  
-   將使用者定義型別轉換成內建類型的規則與內建類型的規則相同。 例如，您可以定義**myInteger**型別衍生自**xs: integer**型別。 然後， **myInteger**可以轉換成**xs: token**，因為**xs: decimal**可轉換成**xs: string**。  
  
 不支援下列種類的轉換：  
  
-   不允許對清單類型進行轉換。 這包括使用者自訂清單類型和內建清單類型這類**xs: idrefs**， **xs: entities**，並**xs: nmtokens**。  
  
-   轉型來往**xs: qname**不支援。  
  
-   **xs: notation**和 持續時間，完全排序子類型**xdt: yearmonthduration**並**xdt: daytimeduration**，不支援。 因此不支援對這些類型的轉換。  
  
 下列範例說明明確類型的轉換。  
  
### <a name="example-a"></a>範例 A  
 下列範例會查詢 xml 類型的變數。 查詢將可傳回 xs:string 類型的簡單類型值序列。  
  
```  
declare @x xml  
set @x = '<e>1</e><e>2</e>'  
select @x.query('/e[1] cast as xs:string?')  
go  
```  
  
### <a name="example-b"></a>範例 B  
 下列範例會查詢具類型的 xml 變數。 該範例會先建立 XML 結構描述的集合。 它接著會使用 XML 結構描述集合以建立具類型的 xml 變數。 結構描述提供了指派給變數的 XML 執行個體之類型資訊。 接著會針對變數指定查詢。  
  
```  
create xml schema collection myCollection as N'  
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">  
      <xs:element name="root">  
            <xs:complexType>  
                  <xs:sequence>  
                        <xs:element name="A" type="xs:string"/>  
                        <xs:element name="B" type="xs:string"/>  
                        <xs:element name="C" type="xs:string"/>  
                  </xs:sequence>  
            </xs:complexType>  
      </xs:element>  
</xs:schema>'  
go  
```  
  
 下列查詢會傳回靜態錯誤，因為您不知道在文件執行個體中有多少最上層的 <`root`> 元素。  
  
```  
declare @x xml(myCollection)  
set @x = '<root><A>1</A><B>2</B><C>3</C></root>  
          <root><A>4</A><B>5</B><C>6</baz></C>'  
select @x.query('/root/A cast as xs:string?')  
go  
```  
  
 在運算式中指定單一 <`root`> 元素，查詢就會成功。 查詢將可傳回 xs:string 類型的簡單類型值序列。  
  
```  
declare @x xml(myCollection)  
set @x = '<root><A>1</A><B>2</B><C>3</C></root>  
              <root><A>4</A><B>5</B><C>6</C></root>'  
select @x.query('/root[1]/A cast as xs:string?')  
go  
```  
  
 在下列範例中，xml 類型的變數包含指定 XML 結構描述集合的文件關鍵字。 這指出 XML 執行個體必須是包含單一最上層元素的文件。 如果您在 XML 執行個體中建立兩個 <`root`> 元素，它將會傳回錯誤。  
  
```  
declare @x xml(document myCollection)  
set @x = '<root><A>1</A><B>2</B><C>3</C></root>  
              <root><A>4</A><B>5</B><C>6</C></root>'  
go  
```  
  
 您可以變更執行個體以便只包含一個最上層元素，該查詢仍可成功執行。 查詢將會再次傳回 xs:string 類型的簡單類型值序列。  
  
```  
declare @x xml(document myCollection)  
set @x = '<root><A>1</A><B>2</B><C>3</C></root>'  
select @x.query('/root/A cast as xs:string?')  
go  
```  
  
## <a name="implicit-casting"></a>隱含轉換  
 隱含轉換只允許數值類型與不具類型的不可部份完成類型。 例如，下列**min （)** 函式會傳回兩個值的最小值：  
  
```  
min(xs:integer("1"), xs:double("1.1"))  
```  
  
 在此範例中，兩個值傳遞至 XQuery **min （)** 函式為不同的類型。 因此，會執行隱含轉換，其中**整數**類型升級至**雙精度浮點**兩個**double**值進行比較。  
  
 此範例中所描述的類型升級是依照下列規則來進行：  
  
-   內建衍生的數值類型可升級至其基本類型。 例如，**整數**可升級至**十進位**。  
  
-   A**十進位**可升級至**float**和**float**可升級至**double**。  
  
 因為隱含轉換只允許數值類型，所以下列類型是不允許的：  
  
-   不允許字串類型的隱含轉換。 比方說，如果兩個**字串**預期型別，而您傳遞**字串**並**k**不執行隱含轉換，則會傳回錯誤。  
  
-   不允將數值類型許隱含轉換成字串類型。 例如，如果您傳遞整數類型值至必須是字串類型參數的函數，將不會執行隱含轉換，並且會傳回錯誤。  
  
## <a name="casting-values"></a>轉換值  
 當從一個類型轉換至另一個類型，實際值將從來源類型的值空間轉換成目標類型的值空間。 例如，從 xs:decimal 轉換成 xs:double 會將十進位值轉換成雙精確度浮點數值。  
  
 以下為一些轉換規則。  
  
##### <a name="casting-a-value-from-a-string-or-untypedatomic-type"></a>從字串或 untypedAtomic 類型轉換值。  
 轉換成 string 或 untypedAtomic 類型的值，所採用的轉換方式與根據目標類型的規則來驗證值的方式相同。 這包含最終的模式與空白處理規則。 例如，下列程式碼將會成功並產生 double 值 1.1e0：  
  
 `xs:double("1.1")`  
  
 當從字串或 untypedAtomic 類型轉換成如 xs:base64Binary 或 xs:hexBinary 的二進位類型時，輸入值必須分別為 Base64 或已編碼的十六進位。  
  
##### <a name="casting-a-value-to-a-string-or-untypedatomic-type"></a>將值轉換成字串或 untypedAtomic 類型。  
 轉換成 string 或 untypedAtomic 類型會將值轉換成其 XQuery 標準語彙表示法。 具體而言，這意謂著在輸入期間已遵守特定模式或其他條件約束的值，將不會根據該條件約束來表示。  若要告知使用者有這，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]加上旗標的類型條件約束可以的問題在這些類型載入結構描述集合時提供警告。  
  
 當將 xs:float 或 xs:double 類型或它其中任何一個子類型的值，轉換成 string 或 untypedAtomic 類型時，該值會以科學記號表示。 只有當值的絕對值小於 1.0E-6，或大於或等於 1.0E6 時才會這麼做。 這意謂著 0 是以科學記號序列化成 0.0E0。  
  
 例如，`xs:string(1.11e1)` 將會傳回字串值 `"11.1"`，而 `xs:string(-0.00000000002e0)` 將會傳回字串值 `"-2.0E-11"`。  
  
 當將 xs:base64Binary 或 xs:hexBinary 的二進位類型轉換成字串或 untypedAtomic 類型時，二進位值將會分別以 Base64 或已編碼的十六進位格式來表示。  
  
##### <a name="casting-a-value-to-a-numeric-type"></a>將值轉換成數值類型。  
 當將一個數值類型的值轉換成另一個數值類型的值時，會從一個值空間將該值對應至其他沒有經過字串序列化的值。 如果值不符合目標類型的條件約束，就適用下列規則：  
  
-   如果來源值已經是數值，而目標類型為 xs:float 或子類型因而可允許 -INF 或 INF 值，且來源數值的轉換將產生溢位，如果值為正數，該值就會對應至 INF，如果值為負數就會對應至 -INF。 如果目標類型不允許 INF 或 -INF 且將會發生溢位，則轉換會失敗且在此版的 SQL Server 中所產生的結果將為空白時序。  
  
-   如果來源值已經是數值，且目標類型為數值類型並在其可接受的值範圍內包含 0、-0e0 或 0e0，則來源數值的轉換將產生反向溢位，該值會以下列方式對應：  
  
    -   對於十進位目標類型，該值會對應至 0。  
  
    -   當值是負值反向溢位時，該值會對應至 -0e0。  
  
    -   當值是浮點數或雙精確度浮點數目標類型的正值反向溢位時，該值會對應至 0e0。  
  
     如果目標類型在其值空間中不包含零，轉換就會失敗且其結果將為空白時序。  
  
     請注意將值轉換成二進位浮點類型 (例如 xs:float、xs:double) 或任一個它的子類型，都將遺失有效位數。  
  
## <a name="implementation-limitations"></a>實作限制  
 以下為其限制：  
  
-   不支援浮點值 NaN。  
  
-   可轉換的值會受到目標型別實作的限制。 比方說，您無法轉換為日期字串，含有負數年份來**xs: date**。 如果此值是在執行階段提供，這樣的轉換將會產生空的序列 (而不是引發執行階段錯誤)。  
  
## <a name="see-also"></a>另請參閱  
 [定義 XML 資料的序列化](../relational-databases/xml/define-the-serialization-of-xml-data.md)  
  
  
