---
title: XML 建構 (XQuery) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
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
- white space [XQuery]
- computed constructor
- construct XML structures [XQuery]
- constructors [XQuery]
- prolog
- direct constructor [SQL Server]
- XML [SQL Server], construction
- XQuery, XML construction
ms.assetid: a6330b74-4e52-42a4-91ca-3f440b3223cf
caps.latest.revision: 44
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 66dc8917b0fa80c79d385dafb4bfb4c4c96c4127
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="xml-construction-xquery"></a>XML 建構 (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  在 XQuery 中，您可以使用**直接**和**計算**建構函式來查詢中建構 XML 結構。  
  
> [!NOTE]  
>  之間沒有差異**直接**和**計算**建構函式。  
  
## <a name="using-direct-constructors"></a>使用直接建構函式  
 當您使用直接建構函式時，可以在建構 XML 時指定與 XML 相似的語法。 下列範例說明以直接建構函式建構 XML 。  
  
### <a name="constructing-elements"></a>建構元素  
 在使用 XML 註解時，您可以建構元素。 下列範例會使用直接元素建構函式運算式，並建立\<ProductModel > 項目。 此建構元素具有三個子元素  
  
-   文字節點。  
  
-   兩個項目節點，\<摘要 > 和\<功能 >。  
  
    -   \<摘要 > 項目具有一個文字子節點的值是"Some description"。  
  
    -   \<功能 > 項目具有三個元素節點子系\<色彩 >，\<加權 >，並\<擔保 >。 這些節點的每一個都有一個文字子節點，而且分別有 Red、25、2 years parts and labor 的值。  
  
```  
declare @x xml;  
set @x='';  
select @x.query('<ProductModel ProductModelID="111">;  
This is product model catalog description.  
<Summary>Some description</Summary>  
<Features>  
  <Color>Red</Color>  
  <Weight>25</Weight>  
  <Warranty>2 years parts and labor</Warranty>  
</Features></ProductModel>')  
  
```  
  
 以下是產生的 XML：  
  
```  
<ProductModel ProductModelID="111">  
  This is product model catalog description.  
  <Summary>Some description</Summary>  
  <Features>  
    <Color>Red</Color>  
    <Weight>25</Weight>  
    <Warranty>2 years parts and labor</Warranty>  
  </Features>  
</ProductModel>  
```  
  
 雖然從常數運算式建構元素 (如本範例所示) 非常有用，不過此 XQuery 語言真正強大的功能在於能夠從資料庫動態擷取資料來建構 XML。 您可以使用大括號指定查詢運算式。 在產生的 XML 中，其值將會取代運算式。 例如，下列查詢使用一個子元素 (<`e`>) 來建構 <`NewRoot`> 元素。 元素的值 <`e`> 計算所指定路徑運算式在大括號 （"{… }").  
  
```  
DECLARE @x xml;  
SET @x='<root>5</root>';  
SELECT @x.query('<NewRoot><e> { /root } </e></NewRoot>');  
```  
  
 括號是做為內容切換 Token 並將查詢從 XML 建構切換到查詢評估。 在此例中，已評估在括號中的 XQuery 路徑運算式 `/root`，且其結果將會取代它。  
  
 以下是結果：  
  
```  
<NewRoot>  
  <e>  
    <root>5</root>  
  </e>  
</NewRoot>  
```  
  
 下列查詢與上一個查詢相似。 不過，在大括號運算式指定**data （)** 函式可擷取的不可部份完成值 <`root`> 項目並將它指派給建構元素 <`e`>。  
  
```  
DECLARE @x xml;  
SET @x='<root>5</root>';  
DECLARE @y xml;  
SET @y = (SELECT @x.query('  
                           <NewRoot>  
                             <e> { data(/root) } </e>  
                           </NewRoot>' ));  
SELECT @y;  
```  
  
 以下是結果：  
  
```  
<NewRoot>  
  <e>5</e>  
</NewRoot>  
```  
  
 如果您想要使用大括號做為文字而不是內容切換 Token 的一部份，只要使用 "}}" 或 "{{" 就可以跳過它們，如本範例所示：  
  
```  
DECLARE @x xml;  
SET @x='<root>5</root>';  
DECLARE @y xml;  
SET @y = (SELECT @x.query('  
<NewRoot> Hello, I can use {{ and  }} as part of my text</NewRoot>'));  
SELECT @y;  
```  
  
 以下是結果：  
  
```  
<NewRoot> Hello, I can use { and  } as part of my text</NewRoot>  
```  
  
 下列查詢是使用直接元素建構函式來建構元素的另一個範例。 另外，<`FirstLocation`> 元素的值是由執行大括號中的運算式而取得。 查詢運算式會在第一個工作中心位置從 Production.ProductModel 資料表的 Instructions 資料行傳回製造步驟。  
  
```  
SELECT Instructions.query('  
    declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        <FirstLocation>  
           { /AWMI:root/AWMI:Location[1]/AWMI:step }  
        </FirstLocation>   
') as Result   
FROM Production.ProductModel  
WHERE ProductModelID=7;  
```  
  
 以下是結果：  
  
```  
<FirstLocation>  
  <AWMI:step xmlns:AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions">  
      Insert <AWMI:material>aluminum sheet MS-2341</AWMI:material> into the <AWMI:tool>T-85A framing tool</AWMI:tool>.   
  </AWMI:step>  
  <AWMI:step xmlns:AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions">  
      Attach <AWMI:tool>Trim Jig TJ-26</AWMI:tool> to the upper and lower right corners of the aluminum sheet.   
  </AWMI:step>  
   ...  
</FirstLocation>  
```  
  
#### <a name="element-content-in-xml-construction"></a>在 XML 建構中的元素內容  
 下列範例使用直接元素建構函式，說明運算式建構元素內容的行為。 在下列範例中，直接元素建構函式指定了一個運算式。 為了此運算式，在產生的 XML 中建立了一個文字節點。  
  
```  
declare @x xml;  
set @x='  
<root>  
  <step>This is step 1</step>  
  <step>This is step 2</step>  
  <step>This is step 3</step>  
</root>';  
select @x.query('  
<result>  
 { for $i in /root[1]/step  
    return string($i)  
 }  
</result>');  
  
```  
  
 從運算式評估所產生的不可部份完成值順序將會加入文字節點，並在相鄰的不可部份完成值之間加入空格，如下列結果所示。 建構元素具有一個子元素。 這是包含值的文字節點，如下列結果所示。  
  
```  
<result>This is step 1 This is step 2 This is step 3</result>  
```  
  
 如果您不指定一個運算式而是指定三個獨立的運算式以產生三個文字節點，相鄰的節點會在產生的 XML 中依串連合併成單一文字節點。  
  
```  
declare @x xml;  
set @x='  
<root>  
  <step>This is step 1</step>  
  <step>This is step 2</step>  
  <step>This is step 3</step>  
</root>';  
select @x.query('  
<result>  
 { string(/root[1]/step[1]) }  
 { string(/root[1]/step[2]) }  
 { string(/root[1]/step[3]) }  
</result>');  
```  
  
 建構元素節點具有一個子元素。 這是包含值的文字節點，如下列結果所示。  
  
```  
<result>This is step 1This is step 2This is step 3</result>  
```  
  
### <a name="constructing-attributes"></a>建構屬性  
 當您使用直接元素建構函式建構元素時，您也可以使用與 XML 相似的語法來指定元素的屬性，如下列範例所示：  
  
```  
declare @x xml;  
set @x='';  
select @x.query('<ProductModel ProductModelID="111">;  
This is product model catalog description.  
<Summary>Some description</Summary>  
</ProductModel>')  
```  
  
 以下是產生的 XML：  
  
```  
<ProductModel ProductModelID="111">  
  This is product model catalog description.  
  <Summary>Some description</Summary>  
</ProductModel>  
```  
  
 建構元素 <`ProductModel`> 有一個 ProductModelID 屬性，而這些子節點為：   
  
-   文字節點 `This is product model catalog description.`  
  
-   元素節點 <`Summary`>。 此節點擁有一個文字子節點 `Some description`。  
  
 當您建構屬性時，您可以在大括號中指定值與運算式。 在此情況下，將以屬性值傳回運算式的結果。  
  
 在下列範例中， **data （)** 函式不是絕對必要。 您的運算式值指派給屬性，因為**data （)** 隱含地套用至擷取指定之運算式的具類型的值。  
  
```  
DECLARE @x xml;  
SET @x='<root>5</root>';  
DECLARE @y xml;  
SET @y = (SELECT @x.query('<NewRoot attr="{ data(/root) }" ></NewRoot>'));  
SELECT @y;  
```  
  
 以下是結果：  
  
```  
<NewRoot attr="5" />  
```  
  
 以下是另一個範例，它為 LocationID 與 SetupHrs 屬性建構指定運算式。 這些運算式會針對 Instruction 資料行中的 XML 來評估運算式。 運算式中具類型的值會指派給屬性。  
  
```  
SELECT Instructions.query('  
    declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        <FirstLocation   
         LocationID="{ (/AWMI:root/AWMI:Location[1]/@LocationID)[1] }"  
         SetupHrs = "{ (/AWMI:root/AWMI:Location[1]/@SetupHours)[1] }" >  
           { /AWMI:root/AWMI:Location[1]/AWMI:step }  
        </FirstLocation>   
') as Result   
FROM  Production.ProductModel  
where ProductModelID=7;  
```  
  
 以下是部份結果：  
  
```  
<FirstLocation LocationID="10" SetupHours="0.5" >  
  <AWMI:step …   
  </AWMI:step>  
  ...  
</FirstLocation>  
```  
  
#### <a name="implementation-limitations"></a>實作限制  
 以下為其限制：  
  
-   不支援多個或混合的 (字串與 XQuery 運算式) 屬性運算式。 例如，如下列查詢所示，您可以建構 XML，其中 `Item` 是常數，而值 `5` 是由評估查詢運算式所取得：  
  
    ```  
    <a attr="Item 5" />  
    ```  
  
     下列查詢會傳回錯誤，因為您將常數字串與運算式 ({/x}) 混用，這是不支援的：  
  
    ```  
    DECLARE @x xml  
    SET @x ='<x>5</x>'  
    SELECT @x.query( '<a attr="Item {/x}"/>' )   
    ```  
  
     在這種情形下，您有下列選擇：  
  
    -   依兩個不可部份完成值的串連組成屬性值。 這些不可部份完成值將序列化成屬性值，並在兩個不可部份完成值之間加上空格：  
  
        ```  
        SELECT @x.query( '<a attr="{''Item'', data(/x)}"/>' )   
        ```  
  
         以下是結果：  
  
        ```  
        <a attr="Item 5" />  
        ```  
  
    -   使用[concat 函數](../xquery/functions-on-string-values-concat.md)串連成產生的屬性值的兩個字串引數：  
  
        ```  
        SELECT @x.query( '<a attr="{concat(''Item'', /x[1])}"/>' )   
        ```  
  
         在此情況下，不會在兩個字串值之間加入空格。 如果您希望兩個值之間有空格，您必須明確地提供它。  
  
         以下是結果：  
  
        ```  
        <a attr="Item5" />  
        ```  
  
-   不支援做為屬性值的多個運算式。 例如，下列查詢會傳回錯誤：  
  
    ```  
    DECLARE @x xml  
    SET @x ='<x>5</x>'  
    SELECT @x.query( '<a attr="{/x}{/x}"/>' )  
    ```  
  
-   不支援異質性時序。 嘗試指派異質性時序做為屬性值將會傳回錯誤，如下列範例所示。 此範例為異質性順序，將字串 "Item" 與元素 <`x`> 指定為屬性值：   
  
    ```  
    DECLARE @x xml  
    SET @x ='<x>5</x>'  
    select @x.query( '<a attr="{''Item'', /x }" />')  
    ```  
  
     如果您套用**data （)** 函式，查詢運作，因為它會擷取運算式，不可部份完成值`/x`，這與字串串連。 下列是不可部份完成值的時序：  
  
    ```  
    SELECT @x.query( '<a attr="{''Item'', data(/x)}"/>' )   
    ```  
  
     以下是結果：  
  
    ```  
    <a attr="Item 5" />  
    ```  
  
-   屬性節點順序會在序列化期間強制執行，而非靜態類型檢查期間。 例如，由於下列查詢嘗試將節點加入非屬性節點後面，因此查詢將會失敗。  
  
    ```  
    select convert(xml, '').query('  
    element x { attribute att { "pass" }, element y { "Element text" }, attribute att2 { "fail" } }  
    ')  
    go  
    ```  
  
     上述查詢傳回的錯誤如下：  
  
    ```  
    XML well-formedness check: Attribute cannot appear outside of element declaration. Rewrite your XQuery so it returns well-formed XML.  
    ```  
  
### <a name="adding-namespaces"></a>加入命名空間  
 使用直接建構函式來建構 XML 時，可以使用命名空間前置詞來限定建構元素與屬性名稱。 您可以利用下列方式來繫結命名空間的前置詞：  
  
-   使用命名空間宣告屬性。  
  
-   使用 WITH XMLNAMESPACES 子句。  
  
-   在 XQuery 初構中。  
  
#### <a name="using-a-namespace-declaration-attribute-to-add-namespaces"></a>使用命名空間宣告屬性加入命名空間  
 下列範例在建構 <`a`> 元素時，使用命名空間宣告屬性來宣告預設的命名空間。 子元素 <`b`> 的建構會恢復在父項元素中宣告的預設命名空間宣告。  
  
```  
declare @x xml  
set @x ='<x>5</x>'  
select @x.query( '  
  <a xmlns="a">  
    <b xmlns=""/>  
  </a>' )   
```  
  
 以下是結果：  
  
```  
<a xmlns="a">  
  <b xmlns="" />  
</a>  
```  
  
 您可以指派前置詞給命名空間。 在建構 <`a`> 元素時會指定前置詞。  
  
```  
declare @x xml  
set @x ='<x>5</x>'  
select @x.query( '  
  <x:a xmlns:x="a">  
    <b/>  
  </x:a>' )  
```  
  
 以下是結果：  
  
```  
<x:a xmlns:x="a">  
  <b />  
</x:a>  
```  
  
 您可以取消宣告 XML 建構中的預設命名空間，但是您無法取消宣告命名空間的前置詞。 下列查詢會傳回錯誤，因為您無法取消宣告在建構 <`b`> 元素時所指定的前置詞。  
  
```  
declare @x xml  
set @x ='<x>5</x>'  
select @x.query( '  
  <x:a xmlns:x="a">  
    <b xmlns:x=""/>  
  </x:a>' )  
```  
  
 新建構的命名空間可在查詢中使用。 例如，下列查詢會在建構 <`FirstLocation`> 元素時宣告命名空間，並在 LocationID 與 SetupHrs 屬性值的運算式中指定前置詞。  
  
```  
SELECT Instructions.query('  
        <FirstLocation xmlns:AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"  
         LocationID="{ (/AWMI:root/AWMI:Location[1]/@LocationID)[1] }"  
         SetupHrs = "{ (/AWMI:root/AWMI:Location[1]/@SetupHours)[1] }" >  
           { /AWMI:root/AWMI:Location[1]/AWMI:step }  
        </FirstLocation>   
') as Result   
FROM  Production.ProductModel  
where ProductModelID=7  
```  
  
 請注意以此方式建立的新命名空間前置詞，將會覆寫此前置詞的任何已存在的命名空間宣告。 例如，<`FirstLocation`> 元素中的命名空間宣告將會覆寫在查詢初構中的命名空間宣告 `AWMI="http://someURI"`。  
  
```  
SELECT Instructions.query('  
declare namespace AWMI="http://someURI";  
        <FirstLocation xmlns:AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"  
         LocationID="{ (/AWMI:root/AWMI:Location[1]/@LocationID)[1] }"  
         SetupHrs = "{ (/AWMI:root/AWMI:Location[1]/@SetupHours)[1] }" >  
           { /AWMI:root/AWMI:Location[1]/AWMI:step }  
        </FirstLocation>   
') as Result   
FROM  Production.ProductModel  
where ProductModelID=7  
```  
  
#### <a name="using-a-prolog-to-add-namespaces"></a>使用初構加入命名空間  
 此範例說明命名空間如何加入已建構的 XML。 在查詢初構中會宣告預設的命名空間。  
  
```  
declare @x xml  
set @x ='<x>5</x>'  
select @x.query( '  
           declare default element namespace "a";  
            <a><b xmlns=""/></a>' )  
```  
  
 請注意，在建構 <`b`> 元素時，將使用空白字串來指定命名空間宣告屬性以做為其值。 這將會取消宣告在父元素中所宣告的預設命名空間。  
  
```  
This is the result:  
<a xmlns="a">  
  <b xmlns="" />  
</a>  
```  
  
### <a name="xml-construction-and-white-space-handling"></a>XML 建構與空白處理  
 在 XML 建構中的元素內容可以包含空白字元。 這些字元是以下列方式處理：  
  
-   命名空間 Uri 中的空白字元視為 XSD 類型**anyURI**。 具體而言，以下是處理它們的方式：  
  
    -   任何在開頭和結尾的空白字元都會被刪減。  
  
    -   內部空白字元值會摺疊成單一空格。  
  
-   在屬性內容中的換行字元將以空格取代。 所有其他的空白字元仍然會維持不變。  
  
-   元素內的空白將予以保留。  
  
 下列範例說明在 XML 建構中空白的處理：  
  
```  
-- line feed is repaced by space.  
declare @x xml  
set @x=''  
select @x.query('  
  
declare namespace myNS="   http://       
 abc/  
xyz  
  
";  
<test attr="    my   
test   attr   
value    " >  
  
<a>  
  
This     is  a  
  
test  
  
</a>  
</test>  
') as XML_Result  
  
```  
  
 以下是結果：  
  
```  
-- result  
<test attr="<test attr="    my test   attr  value    "><a>  
  
This     is  a  
  
test  
  
</a></test>  
"><a>  
  
This     is  a  
  
test  
  
</a></test>  
```  
  
### <a name="other-direct-xml-constructors"></a>其他直接 XML 建構函式  
 處理指示和 XML 註解的建構函式使用與對應 XML 建構語法相同的語法。 也支援文字節點的計算建構函式，但主要用於 XML DML 以建構文字節點。  
  
 **請注意**使用明確文字節點建構函式的範例，請參閱中的特定範例[插入&#40;XML DML&#41;](../t-sql/xml/insert-xml-dml.md)。  
  
 在下列查詢中，已建構的 XML 包含一個元素、兩個屬性、註解以及處理指示。 請注意在 <`FirstLocation`> 前面使用了一個逗號，因為正在建構時序。  
  
```  
SELECT Instructions.query('  
  declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
   <?myProcessingInstr abc="value" ?>,   
   <FirstLocation   
        WorkCtrID = "{ (/AWMI:root/AWMI:Location[1]/@LocationID)[1] }"  
        SetupHrs = "{ (/AWMI:root/AWMI:Location[1]/@SetupHours)[1] }" >  
       <!-- some comment -->  
       <?myPI some processing instructions ?>  
       { (/AWMI:root/AWMI:Location[1]/AWMI:step) }  
    </FirstLocation>   
') as Result   
FROM Production.ProductModel  
where ProductModelID=7;  
  
```  
  
 以下是部份結果：  
  
```  
<?myProcessingInstr abc="value" ?>  
<FirstLocation WorkCtrID="10" SetupHrs="0.5">  
  <!-- some comment -->  
  <?myPI some processing instructions ?>  
  <AWMI:step xmlns:AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions">I  
  nsert <AWMI:material>aluminum sheet MS-2341</AWMI:material> into the <AWMI:tool>T-85A framing tool</AWMI:tool>.   
  </AWMI:step>  
    ...  
/FirstLocation>  
  
```  
  
## <a name="using-computed-constructors"></a>使用計算建構函式  
 。 在此情況下，您可以指定關鍵字，以識別您要建構的節點類型。 只支援下列關鍵字：  
  
-   element  
  
-   屬性  
  
-   text  
  
 對於元素和屬性節點而言，這些關鍵字後面接著括在括號中的節點名稱及運算式，它們將會產生該節點的內容。 在以下範例中，您正在建構此 XML：  
  
```  
<root>  
  <ProductModel PID="5">Some text <summary>Some Summary</summary></ProductModel>  
</root>  
```  
  
 以下查詢是使用計算建構函式產生 XML：  
  
```  
declare @x xml  
set @x=''  
select @x.query('element root   
               {   
                  element ProductModel  
     {  
attribute PID { 5 },  
text{"Some text "},  
    element summary { "Some Summary" }  
 }  
               } ')  
  
```  
  
 產生節點內容的運算式可以指定查詢運算式。  
  
```  
declare @x xml  
set @x='<a attr="5"><b>some summary</b></a>'  
select @x.query('element root   
               {   
                  element ProductModel  
     {  
attribute PID { /a/@attr },  
text{"Some text "},  
    element summary { /a/b }  
 }  
               } ')  
```  
  
 請注意計算元素與屬性建構函式 (如 XQuery 規格所定義) 允許您計算節點名稱。 當您使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中的直接建構函式時，節點名稱 (例如元素與屬性) 必須以常值指定。 因此，元素和屬性的直接建構函式與計算建構函式之間並沒有差異。  
  
 在下列範例中，建構節點的內容從 XML 製造指示儲存在資料行中取得**xml** ProductModel 資料表的資料類型。  
  
```  
SELECT Instructions.query('  
  declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
   element FirstLocation   
     {  
        attribute LocationID { (/AWMI:root/AWMI:Location[1]/@LocationID)[1] },  
        element   AllTheSteps { /AWMI:root/AWMI:Location[1]/AWMI:step }  
     }  
') as Result   
FROM  Production.ProductModel  
where ProductModelID=7  
```  
  
 以下是部份結果：  
  
```  
<FirstLocation LocationID="10">  
  <AllTheSteps>  
    <AWMI:step> ... </AWMI:step>  
    <AWMI:step> ... </AWMI:step>  
    ...  
  </AllTheSteps>  
</FirstLocation>    
```  
  
## <a name="additional-implementation-limitations"></a>其他的實作限制  
 計算屬性建構函式無法用以宣告新命名空間。 另外，下列計算建構函式不支援 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]：  
  
-   計算文件節點建構函式  
  
-   計算處理指示建構函式  
  
-   計算註解建構函式  
  
## <a name="see-also"></a>另請參閱  
 [XQuery 運算式](../xquery/xquery-expressions.md)  
  
  
