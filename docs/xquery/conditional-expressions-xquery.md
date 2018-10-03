---
title: 條件運算式 (XQuery) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology:
- database-engine
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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 00ea3657da6f40c0a21b08d8c33338eaaba5142f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47616516"
---
# <a name="conditional-expressions-xquery"></a>條件運算式 (XQuery)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  XQuery 支援下列的條件式**if--e**陳述式：  
  
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
  
-   **其他**必須是運算式。 如果您不需要它，您可以傳回 " ( ) "，如本主題中的範例所說明。  
  
 例如，下列查詢針對所指定**xml**類型變數。 **如果**測試條件的 SQL 變數的值 (@v) 內使用中的 XQuery 運算式[（） 函數](../xquery/xquery-extension-functions-sql-variable.md)擴充程式函式。 如果變數值是 "FirstName"，它會傳回 <`FirstName`> 元素。 否則它會傳回 <`LastName`> 元素。  
  
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
  
 在上一個查詢中中的條件**如果**運算式會檢查是否有兩個以上的子元素中 <`Features`>。 如果是，它會傳回結果中的 `\<there-is-more/>` 元素。  
  
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
  
  
