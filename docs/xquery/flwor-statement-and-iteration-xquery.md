---
title: FLWOR 陳述式與反覆運算 (XQuery) |Microsoft Docs
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
- return clause
- FLWOR statement
- effective Boolean value [XQuery]
- multiple variable binding
- order by clause [XQuery]
- for clause [XQuery]
- where clause [XQuery]
- iterations [XQuery]
- XQuery, FLWOR statement
- EBV
ms.assetid: d7cd0ec9-334a-4564-bda9-83487b6865cb
author: rothja
ms.author: jroth
ms.openlocfilehash: 9deb87d506e167d3de3439e0a07cfbb8bc040fac
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68038899"
---
# <a name="flwor-statement-and-iteration-xquery"></a>FLWOR 陳述式與反覆運算 (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  XQuery 定義 FLWOR 反覆運算語法。 FLWOR 是 `for`、`let`、`where`、`order by` 及 `return` 的縮寫字。  
  
 FLWOR 陳述式是由下列部份所組成：  
  
-   一或多個 FOR 子句，用以將一或多個 Iterator 變數繫結至輸入時序。  
  
     輸入時序可為其他的 XQuery 運算式，例如 XPath 運算式。 它們可為節點的時序或不可部份完成值的時序。 不可部份完成值時序可使用常式或建構函式來建構。 建構的 XML 節點在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中不允許做為輸入序列。  
  
-   選擇性的 `let` 子句。 這個子句會針對特定反覆運算的給定變數指派值。 指派的運算式可以是 XQuery 運算式 (如 XPath 運算式)，並可傳回一連串節點或是一連串不可部分完成的值。 不可部分完成的值序列可使用常值或建構函式來建構。 建構的 XML 節點在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中不允許做為輸入序列。  
  
-   Iterator 變數。 此變數可擁有使用 `as` 關鍵字的選擇性類型之判斷提示。  
  
-   選擇性的 `where` 子句。 此子句在反覆運算上套用篩選述詞。  
  
-   選擇性的 `order by` 子句。  
  
-   `return` 運算式。 在 `return` 子句中的運算式可建構 FLWOR 陳述式的結果。  
  
 例如，下列查詢會逐一查看 <`Step`> 元素的第一個製造位置，並傳回的字串值 <`Step`> 節點：  
  
```sql
declare @x xml  
set @x='<ManuInstructions ProductModelID="1" ProductModelName="SomeBike" >  
<Location LocationID="L1" >  
  <Step>Manu step 1 at Loc 1</Step>  
  <Step>Manu step 2 at Loc 1</Step>  
  <Step>Manu step 3 at Loc 1</Step>  
</Location>  
<Location LocationID="L2" >  
  <Step>Manu step 1 at Loc 2</Step>  
  <Step>Manu step 2 at Loc 2</Step>  
  <Step>Manu step 3 at Loc 2</Step>  
</Location>  
</ManuInstructions>'  
SELECT @x.query('  
   for $step in /ManuInstructions/Location[1]/Step  
   return string($step)  
')  
```  
  
 以下是結果：  
  
```  
Manu step 1 at Loc 1 Manu step 2 at Loc 1 Manu step 3 at Loc 1  
```  
  
 下列查詢與上一個查詢相似，除了它是針對 ProductModel 資料表的 Instructions 資料行 (具類型的 xml 資料行) 所指定之外。 查詢會逐一查看所有的製造步驟 <`step`> 項目，在特定產品的第一個工作中心位置。  
  
```sql
SELECT Instructions.query('  
   declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
for $Step in //AWMI:root/AWMI:Location[1]/AWMI:step  
      return  
           string($Step)   
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 請注意下列項目是從上一個查詢而來：  
  
-   `$Step` 是 Iterator 變數。  
  
-   [路徑運算式](../xquery/path-expressions-xquery.md)， `//AWMI:root/AWMI:Location[1]/AWMI:step`，產生輸入的時序。 此序列是一連串 <`step`> 元素節點子系的第一個 <`Location`> 項目節點。  
  
-   未使用選擇性述詞子句 `where`。  
  
-   `return`運算式會傳回的字串值 <`step`> 項目。  
  
 [字串函數 (XQuery)](../xquery/data-accessor-functions-string-xquery.md)用來擷取的字串值 <`step`> 節點。  
  
 以下是部份結果：  
  
```  
Insert aluminum sheet MS-2341 into the T-85A framing tool.   
Attach Trim Jig TJ-26 to the upper and lower right corners of   
the aluminum sheet. ....         
```  
  
 這些是允許的其他輸入時序之範例：  
  
```sql
declare @x xml  
set @x=''  
SELECT @x.query('  
for $a in (1, 2, 3)  
  return $a')  
-- result = 1 2 3   
  
declare @x xml  
set @x=''  
SELECT @x.query('  
for $a in   
   for $b in (1, 2, 3)  
      return $b  
return $a')  
-- result = 1 2 3  
  
declare @x xml  
set @x='<ROOT><a>111</a></ROOT>'  
SELECT @x.query('  
  for $a in (xs:string( "test"), xs:double( "12" ), data(/ROOT/a ))  
  return $a')  
-- result test 12 111  
```  
  
 在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中，不允許異質性時序。 具體而言，不允許同時包含不可部份完成值與節點的時序。  
  
 反覆項目經常會搭配[XML 建構](../xquery/xml-construction-xquery.md)轉換 XML 的語法格式，在下一個查詢中所示。  
  
 在 AdventureWorks 範例資料庫中，製造指示儲存在**指示**資料行**Production.ProductModel**資料表具有下列格式：  
  
```xml
<Location LocationID="10" LaborHours="1.2"   
            SetupHours=".2" MachineHours=".1">  
  <step>describes 1st manu step</step>  
   <step>describes 2nd manu step</step>  
   ...  
</Location>  
...  
```  
  
 下列查詢會建構新的 XML 具有 <`Location`> 項目與工作中心以子元素傳回的位置屬性：  
  
```xml
<Location>  
   <LocationID>10</LocationID>  
   <LaborHours>1.2</LaborHours>  
   <SetupHours>.2</SetupHours>  
   <MachineHours>.1</MachineHours>  
</Location>  
...  
```  
  
 此查詢如下：  
  
```sql
SELECT Instructions.query('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        for $WC in /AWMI:root/AWMI:Location  
        return  
          <Location>  
            <LocationID> { data($WC/@LocationID) } </LocationID>  
            <LaborHours>   { data($WC/@LaborHours) }   </LaborHours>  
            <SetupHours>   { data($WC/@SetupHours) }   </SetupHours>  
            <MachineHours> { data($WC/@MachineHours) } </MachineHours>  
          </Location>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 請注意下列項目是從上一個查詢而來：  
  
-   FLWOR 陳述式所擷取的序列 <`Location`> 特定產品的項目。  
  
-   [Data 函數 (XQuery)](../xquery/data-accessor-functions-data-xquery.md)會用來擷取每個屬性的值，因此它們會以文字節點，而不是做為屬性新增至產生的 XML。  
  
-   在 RETURN 子句中的運算式可建構您所需的 XML。  
  
 以下是部份結果：  
  
```xml
<Location>  
  <LocationID>10</LocationID>  
  <LaborHours>2.5</LaborHours>  
  <SetupHours>0.5</SetupHours>  
  <MachineHours>3</MachineHours>  
</Location>  
<Location>  
   ...  
<Location>  
...  
```  
  
## <a name="using-the-let-clause"></a>使用 let 子句  
 您可以使用 `let` 子句命名您可以藉由參考此變數進行參考的重複運算式。 每次在查詢中參考 `let` 變數時，指派給此變數的運算式都會插入此查詢中。 這表示陳述式會在每次參考運算式時執行。  
  
 在 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 資料庫中，製造指示包含所需工具及工具使用位置的詳細資訊。 下列查詢會使用 `let` 子句列出建立生產模型所需的工具，以及需要每一個工具的位置。  
  
```sql
SELECT Instructions.query('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        for $T in //AWMI:tool  
            let $L := //AWMI:Location[.//AWMI:tool[.=data($T)]]  
        return  
          <tool desc="{data($T)}" Locations="{data($L/@LocationID)}"/>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
## <a name="using-the-where-clause"></a>使用 where 子句  
 您可以使用`where`子句篩選反覆運算的結果。 下一個範例會加以說明。  
  
 在製造腳踏車時，製造程序將經過一系列的工作中心位置。 每個工作中心位置都會定義一系列的製造步驟。 下列查詢只會擷取那些製造腳踏車型號以及少於三個製造步驟的工作中心位置。 這就是它們具有少於三個 <`step`> 項目。  
  
```sql
SELECT Instructions.query('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
for $WC in /AWMI:root/AWMI:Location  
      where count($WC/AWMI:step) < 3  
      return  
          <Location >  
           { $WC/@LocationID }   
          </Location>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 下列為上一個查詢的注意事項：  
  
-   `where`關鍵字會使用**count （)** 函式來計算數目 <`step`> 子元素，在每個工作中心位置。  
  
-   `return` 運算式可從反覆運算的結果建構 XML。  
  
 以下是結果：  
  
```  
<Location LocationID="30"/>   
```  
  
 在 `where` 子句中的運算式結果將依指定順序使用下列規則轉換成布林值。 這些規則與在路徑運算式中的述詞規則相同，除了不允許整數以外：  
  
1.  如果 `where` 運算式傳回空白時序，其有效的布林值為 False。  
  
2.  如果 `where` 運算式傳回一個簡單的布林類型值，該值為有效的布林值。  
  
3.  如果 `where` 運算式傳回包含至少一個節點的時序，有效的布林值則為 True。  
  
4.  否則，就會引發靜態錯誤。  
  
## <a name="multiple-variable-binding-in-flwor"></a>在 FLWOR 中繫結多個變數  
 您可以在單一 FLWOR 運算式中，將多個變數繫結至輸入時序。 在下列範例中，查詢是針對不具類型的 xml 變數所指定。 FLOWR 運算式會傳回第一個 <`Step`> 元素子系，在每個 <`Location`> 項目。  
  
```sql
declare @x xml  
set @x='<ManuInstructions ProductModelID="1" ProductModelName="SomeBike" >  
<Location LocationID="L1" >  
  <Step>Manu step 1 at Loc 1</Step>  
  <Step>Manu step 2 at Loc 1</Step>  
  <Step>Manu step 3 at Loc 1</Step>  
</Location>  
<Location LocationID="L2" >  
  <Step>Manu step 1 at Loc 2</Step>  
  <Step>Manu step 2 at Loc 2</Step>  
  <Step>Manu step 3 at Loc 2</Step>  
</Location>  
</ManuInstructions>'  
SELECT @x.query('  
   for $Loc in /ManuInstructions/Location,  
       $FirstStep in $Loc/Step[1]  
   return   
       string($FirstStep)  
')  
```  
  
 請注意下列項目是從上一個查詢而來：  
  
-   `for`運算式會定義`$Loc`和 $`FirstStep`變數。  
  
-   `two` 運算式 `/ManuInstructions/Location` 及 `$FirstStep in $Loc/Step[1]`，與 `$FirstStep` 值相依的 `$Loc` 值相互關聯。  
  
-   與相關聯的運算式`$Loc`產生的序列 <`Location`> 項目。 每個 <`Location`> 項目，`$FirstStep`會產生一連串的其中一個 <`Step`> 項目，即單一。  
  
-   在運算式中指定的 `$Loc` 與 `$FirstStep` 變數關聯。  
  
 以下是結果：  
  
```  
Manu step 1 at Loc 1   
Manu step 1 at Loc 2  
```  
  
 下列查詢很類似，不同之處在於它針對具類型的 Instructions 資料行所指定**xml**資料行的**ProductModel**資料表。 [XML 建構 (XQuery)](../xquery/xml-construction-xquery.md)用來產生您想要的 XML。  
  
```sql
SELECT Instructions.query('  
     declare default element namespace "https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
for $WC in /root/Location,  
            $S  in $WC/step  
      return  
          <Step LocationID= "{$WC/@LocationID }" >  
            { $S/node() }  
          </Step>  
') as Result  
FROM  Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 下列為上一個查詢的注意事項：  
  
-   `for` 子句定義兩個變數 `$WC` 與 `$S`。 與 `$WC` 關聯的運算式會產生製造腳踏車產品型號的工作中心位置序列。 指派給 `$S` 變數的路徑運算式會為 `$WC` 中的每個工作中心位置產生步驟的序列。  
  
-   Return 陳述式會建構具有的 XML <`Step`> 元素包含製造步驟，而**LocationID**做為其屬性。  
  
-   **宣告預設元素命名空間**用在 XQuery 初構中，以便在產生的 XML 中的所有命名空間宣告會出現在最上層的項目。 這將使結果更具可讀性。 如需有關預設命名空間的詳細資訊，請參閱 <<c0> [ 處理 XQuery 中的命名空間](../xquery/handling-namespaces-in-xquery.md)。  
  
 以下是部份結果：  
  
```xml
<Step xmlns=  
    "https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"     
  LocationID="10">  
     Insert <material>aluminum sheet MS-2341</material> into the <tool>T-   
     85A framing tool</tool>.   
</Step>  
...  
<Step xmlns=  
      "https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"     
    LocationID="20">  
        Assemble all frame components following blueprint   
        <blueprint>1299</blueprint>.  
</Step>  
...  
```  
  
## <a name="using-the-order-by-clause"></a>使用依子句排序的順序  
 利用 FLWOR 運算式中的 `order by` 子句執行 XQuery 的排序。 排序運算式傳遞至`order by`子句必須傳回的值的類型都適用於**gt**運算子。 每個排序運算式必須一個項目產生一個序列。 依預設，會以遞增順序執行順序。 您可以為每個排序運算式選擇性地指定遞增或遞減順序。  
  
> [!NOTE]  
>  在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中由 XQuery 實作所執行的字串值排序比較，永遠都會使用二進位的 Unicode 字碼指標定序來執行。  
  
 下列查詢會從 AdditionalContactInfo 資料行擷取特定客戶的所有電話號碼。 結果將依電話號碼進行排序。  
  
```sql
USE AdventureWorks2012;  
GO  
SELECT AdditionalContactInfo.query('  
   declare namespace act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
   declare namespace aci="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo";  
   for $a in /aci:AdditionalContactInfo//act:telephoneNumber   
   order by $a/act:number[1] descending  
   return $a  
') As Result  
FROM Person.Person  
WHERE BusinessEntityID=291;  
```  
  
 請注意，[自動化 (XQuery)](../xquery/atomization-xquery.md)程序擷取的不可部份完成值 <`number`> 項目，再傳遞給`order by`。 您可以藉由撰寫運算式**data （)** 函式，但不需要。  
  
```  
order by data($a/act:number[1]) descending  
```  
  
 以下是結果：  
  
```xml
<act:telephoneNumber xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
  <act:number>333-333-3334</act:number>  
</act:telephoneNumber>  
<act:telephoneNumber xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
  <act:number>333-333-3333</act:number>  
</act:telephoneNumber>  
```  
  
 您可以使用 WITH XMLNAMESPACES 來宣告前置詞，而不是在查詢初構中宣告命名空間。  
  
```sql
WITH XMLNAMESPACES (  
   'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes' AS act,  
   'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo'  AS aci)  
  
SELECT AdditionalContactInfo.query('  
   for $a in /aci:AdditionalContactInfo//act:telephoneNumber   
   order by $a/act:number[1] descending  
   return $a  
') As Result  
FROM Person.Person  
WHERE BusinessEntityID=291;  
```  
  
 您也可以依屬性值進行排序。 例如，下列查詢會擷取新建立 <`Location`> 依 LaborHours 屬性的遞減順序排序的 LocationID 與 LaborHours 屬性的項目。 因此，會先傳回包含工時最大值的工作中心位置。  
  
```sql
SELECT Instructions.query('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
for $WC in /AWMI:root/AWMI:Location   
order by $WC/@LaborHours descending  
        return  
          <Location>  
             { $WC/@LocationID }   
             { $WC/@LaborHours }   
          </Location>  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7;  
```  
  
 以下是結果：  
  
```  
<Location LocationID="60" LaborHours="4"/>  
<Location LocationID="50" LaborHours="3"/>  
<Location LocationID="10" LaborHours="2.5"/>  
<Location LocationID="20" LaborHours="1.75"/>  
<Location LocationID="30" LaborHours="1"/>  
<Location LocationID="45" LaborHours=".5"/>  
```  
  
 在下列查詢中，會依元素名稱排序結果。 該查詢會從產品目錄擷取特定產品的規格。 規格是子系 <`Specifications`> 項目。  
  
```sql
SELECT CatalogDescription.query('  
     declare namespace  
 pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
      for $a in /pd:ProductDescription/pd:Specifications/*   
     order by local-name($a)  
      return $a  
    ') as Result  
FROM Production.ProductModel  
where ProductModelID=19;  
```  
  
 請注意下列項目是從上一個查詢而來：  
  
-   `/p1:ProductDescription/p1:Specifications/*`運算式會傳回的項目子系 <`Specifications`>。  
  
-   `order by (local-name($a))` 運算式會依元素名稱的本機部份排序。  
  
 以下是結果：  
  
```xml
<Color>Available in most colors</Color>  
<Material>Almuminum Alloy</Material>  
<ProductLine>Mountain bike</ProductLine>  
<RiderExperience>Advanced to Professional riders</RiderExperience>  
<Style>Unisex</Style>    
```  
  
 在排序運算式中的節點會傳回排序在序列開頭的空白，如下列範例所示：  
  
```sql
declare @x xml  
set @x='<root>  
  <Person Name="A" />  
  <Person />  
  <Person Name="B" />  
</root>  
'  
select @x.query('  
  for $person in //Person  
  order by $person/@Name  
  return   $person  
')  
```  
  
 以下是結果：  
  
```xml
<Person />  
<Person Name="A" />  
<Person Name="B" />  
```  
  
 您可以指定多個排序條件，如下列範例所示。 在此範例查詢會排序 <`Employee`> 項目先依 Title 然後再依 Administrator 屬性值。  
  
```sql
declare @x xml  
set @x='<root>  
  <Employee ID="10" Title="Teacher"        Gender="M" />  
  <Employee ID="15" Title="Teacher"  Gender="F" />  
  <Employee ID="5" Title="Teacher"         Gender="M" />  
  <Employee ID="11" Title="Teacher"        Gender="F" />  
  <Employee ID="8" Title="Administrator"   Gender="M" />  
  <Employee ID="4" Title="Administrator"   Gender="F" />  
  <Employee ID="3" Title="Teacher"         Gender="F" />  
  <Employee ID="125" Title="Administrator" Gender="F" /></root>'  
SELECT @x.query('for $e in /root/Employee  
order by $e/@Title ascending, $e/@Gender descending  
  
  return  
     $e  
')  
```  
  
 以下是結果：  
  
```xml
<Employee ID="8" Title="Administrator" Gender="M" />  
<Employee ID="4" Title="Administrator" Gender="F" />  
<Employee ID="125" Title="Administrator" Gender="F" />  
<Employee ID="10" Title="Teacher" Gender="M" />  
<Employee ID="5" Title="Teacher" Gender="M" />  
<Employee ID="11" Title="Teacher" Gender="F" />  
<Employee ID="15" Title="Teacher" Gender="F" />  
<Employee ID="3" Title="Teacher" Gender="F" />  
```  
  
### <a name="implementation-limitations"></a>實作限制  
 以下為其限制：  
  
-   排序運算式的類型必須相同。 將會靜態地檢查。  
  
-   排序空白時序是無法加以控制的。  
  
-   在 `order by` 上不支援最少空白、最多空白以及定序關鍵字  
  
## <a name="see-also"></a>另請參閱  
 [XQuery 運算式](../xquery/xquery-expressions.md)  
  
  
