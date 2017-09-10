---
title: "條件式運算式 (XQuery) |Microsoft 文件"
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- XQuery, conditional expressions
- expressions [XQuery], conditional
- effective Boolean value [XQuery]
- if-then-else statement [XQuery]
- conditional expressions [XQuery]
- EBV
ms.assetid: b280dd96-c80f-4c51-bc06-a88d42174acb
caps.latest.revision: 27
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5c137eb08df0eabc7a985cd13ef34a82c6e7ed49
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="conditional-expressions-xquery"></a>條件運算式 (XQuery)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  XQuery 支援下列條件**if-then-其他**陳述式：  
  
```  
if (<expression1>)  
then  
  <expression2>  
else  
  <expression3>  
```  
  
 視 `expression1` 有效的布林值而定，將評估 `expression2` 或 `expression3`。 例如：  
  
-   如果測試運算式 `expression1` 產生空白時序，結果即為 False。  
  
-   如果測試運算式 `expression1` 產生簡單的布林值，此值是運算式的結果。  
  
-   如果測試運算式 `expression1` 產生一或多個節點的時序，運算式的結果即為 True。  
  
-   否則，就會引發靜態錯誤。  
  
 同時應注意下列項目：  
  
-   測試運算式必須在括號內。  
  
-   **Else**必須是運算式。 如果您不需要它，您可以傳回 " ( ) "，如本主題中的範例所說明。  
  
 例如，下列查詢針對指定**xml**類型變數。 **如果**SQL 變數的值來測試條件 (@v) 使用 XQuery 運算式中[: variable （） 函式](../xquery/xquery-extension-functions-sql-variable.md)擴充函式。 如果變數值是 "FirstName"，它會傳回 <`FirstName`> 元素。 否則它會傳回 <`LastName`> 元素。  
  
```  
declare @x xml  
declare @v varchar(20)  
set @v='FirstName'  
set @x='  
<ROOT rootID="2">  
  <FirstName>fname</FirstName>  
  <LastName>lname</LastName>  
</ROOT>'  
SELECT @x.query('  
if ( sql:variable("@v")="FirstName" ) then  
  /ROOT/FirstName  
 else  
   /ROOT/LastName  
')  
```  
  
 以下是結果：  
  
```  
<FirstName>fname</FirstName>  
```  
  
 下列查詢會從特定產品型號的產品目錄描述擷取前兩個功能的描述。 如果在文件中有更多的功能，它會加入空內容的 <`there-is-more`> 元素。  
  
```  
SELECT CatalogDescription.query('  
     declare namespace p1="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     <Product>   
          { /p1:ProductDescription/@ProductModelID }  
          { /p1:ProductDescription/@ProductModelName }   
          {  
            for $f in /p1:ProductDescription/p1:Features/*[position()\<=2]  
            return  
            $f   
          }  
          {  
            if (count(/p1:ProductDescription/p1:Features/*) > 2)  
            then \<there-is-more/>  
            else ()  
          }   
     </Product>          
') as x  
FROM Production.ProductModel  
WHERE ProductModelID = 19  
```  
  
 在上述查詢中的條件**如果**運算式會檢查是否有兩個以上的子元素中 <`Features`>。 如果是，它會傳回結果中的 `\<there-is-more/>` 元素。  
  
 以下是結果：  
  
```  
<Product ProductModelID="19" ProductModelName="Mountain 100">  
  \<p1:Warranty xmlns:p1="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    \<p1:WarrantyPeriod>3 years\</p1:WarrantyPeriod>  
    \<p1:Description>parts and labor\</p1:Description>  
  \</p1:Warranty>  
  \<p2:Maintenance xmlns:p2="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    \<p2:NoOfYears>10 years\</p2:NoOfYears>  
    \<p2:Description>maintenance contract available through your dealer or any AdventureWorks retail store.\</p2:Description>  
  \</p2:Maintenance>  
  \<there-is-more />  
</Product>  
```  
  
 在下列查詢中，如果工作中心位置未指定安裝時間，就會傳回 <`Location`> 元素加上 LocationID 屬性。  
  
```  
SELECT Instructions.query('  
     declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        for $WC in //AWMI:root/AWMI:Location  
        return  
        if ( $WC[not(@SetupHours)] )  
        then  
          <WorkCenterLocation>  
             { $WC/@LocationID }   
          </WorkCenterLocation>  
         else  
           ()  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 以下是結果：  
  
```  
<WorkCenterLocation LocationID="30" />  
<WorkCenterLocation LocationID="45" />  
<WorkCenterLocation LocationID="60" />  
```  
  
 此查詢可以撰寫沒有**如果**子句，如下列範例所示：  
  
```  
SELECT Instructions.query('  
     declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
for $WC in //AWMI:root/AWMI:Location[not(@SetupHours)]   
        return  
          <Location>  
             { $WC/@LocationID }   
          </Location>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
## <a name="see-also"></a>另請參閱  
 [XQuery 運算式](../xquery/xquery-expressions.md)  
  
  

