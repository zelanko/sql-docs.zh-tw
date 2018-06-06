---
title: 比較運算式 (XQuery) |Microsoft 文件
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: sql
ms.component: xquery
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- node comparison operators [XQuery]
- comparison expressions [XQuery]
- node order comparison operators [XQuery]
- expressions [XQuery], comparison
- comparison operators [XQuery]
- value comparison operators
ms.assetid: dc671348-306f-48ef-9e6e-81fc3c7260a6
caps.latest.revision: 40
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: f80838771b36f59f58203dfc687957ea2f208522
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="comparison-expressions-xquery"></a>比較運算式 (XQuery)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  XQuery 提供下列類型的比較運算子：  
  
-   一般比較運算子  
  
-   值比較運算子  
  
-   節點比較運算子  
  
-   節點順序比較運算子  
  
## <a name="general-comparison-operators"></a>一般比較運算子  
 一般比較運算子可用以比較不可部份完成值、序列或任兩個組合。  
  
 在下表中定義了一般運算子。  
  
|運算子|Description|  
|--------------|-----------------|  
|=|等於|  
|!=|不等於|  
|\<|小於|  
|>|大於|  
|\<=|小於或等於|  
|>=|大於或等於|  
  
 當您比較兩個序列，使用一般比較運算子，並將第一個序列中的值與第二個序列中所存在的值相比較得到 True 時，整體的結果將為 True。 否則，它將為 False。 例如，(1, 2, 3) = (3, 4) 為 True，因為值 3 同時出現在兩個序列中。  
  
```  
declare @x xml  
set @x=''  
select @x.query('(1,2,3) = (3,4)')    
```  
  
 該比較預期這些值是可比較的類型。 具體而言，它們是靜態檢查。 對於數值比較，有可能發生數值類型升級。 例如，如果將十進位數值 10 與雙精確度浮點數值 1e1 進行比較，會將十進位數值變更為雙精確度浮點數值。 請注意這可能會建立不精確的結果，因為雙精確度浮點數值的比較不可能會完全一樣。  
  
 如果有其中一個值是不具類型的，會將它轉換成其他的值類型。 在下列範例中，會將值 7 視為整數。 在比較前，會將不具類型的值 /a[1] 轉換為整數。 整數比較會傳回 True。  
  
```  
declare @x xml  
set @x='<a>6</a>'  
select @x.query('/a[1] < 7')  
```  
  
 相反的，如果不具類型的值與字串或另一個不具類型的值比較，會將它轉換成 xs:string。 在下列查詢中，字串 6 將與字串 "17" 進行比較。 以下查詢因為進行字串比較而會傳回 False。  
  
```  
declare @x xml  
set @x='<a>6</a>'  
select @x.query('/a[1] < "17"')  
```  
  
 下列查詢會從 AdventureWorks 範例資料庫所提供的產品目錄，傳回產品型號的小型圖片。 該查詢會將 `PD:ProductDescription/PD:Picture/PD:Size` 所傳回的不可部份完成值序列與單一序列 "small" 進行比較。 如果比較為 True 時，它會傳回 < 圖片\>項目。  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS PD)  
SELECT CatalogDescription.query('         
    for $P in /PD:ProductDescription/PD:Picture[PD:Size = "small"]         
    return $P') as Result         
FROM   Production.ProductModel         
WHERE  ProductModelID=19         
```  
  
 下列查詢會比較序列中的電話號碼 < 數字\>字串常值"112-111-1111"項目。 該查詢會比較 AdditionalContactInfo 資料行中電話號碼元素的序列，以判斷在文件中是否存在特定客戶的特定電話號碼。  
  
```  
WITH XMLNAMESPACES (  
  'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes' AS act,  
  'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo' AS aci)  
  
SELECT AdditionalContactInfo.value('         
   /aci:AdditionalContactInfo//act:telephoneNumber/act:number = "112-111-1111"', 'nvarchar(10)') as Result         
FROM Person.Contact         
WHERE ContactID=1         
```  
  
 此查詢會傳回 True。 這表示文件中存在該號碼。 下列查詢是前一個查詢的稍微修改版。 在此查詢中，將從文件中擷取的電話號碼值與兩個電話號碼值之序列進行比較。 如果該比較為 True 時，< 數字\>元素傳回。  
  
```  
WITH XMLNAMESPACES (  
  'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes' AS act,  
  'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo' AS aci)  
  
SELECT AdditionalContactInfo.query('         
  if (/aci:AdditionalContactInfo//act:telephoneNumber/act:number = ("222-222-2222","112-111-1111"))         
  then          
     /aci:AdditionalContactInfo//act:telephoneNumber/act:number         
  else         
    ()') as Result         
FROM Person.Contact         
WHERE ContactID=1  
  
```  
  
 以下是結果：  
  
```  
\<act:number   
  xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
    111-111-1111  
\</act:number>  
\<act:number   
  xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
    112-111-1111  
\</act:number>   
```  
  
## <a name="value-comparison-operators"></a>值比較運算子  
 使用值比較運算子來比較不可部份完成值。 請注意您可以在查詢中使用一般比較運算子，而不是使用值比較運算子。  
  
 在下表中定義了值比較運算子。  
  
|運算子|Description|  
|--------------|-----------------|  
|eq|等於|  
|ne|不等於|  
|lt|小於|  
|gt|大於|  
|le|小於或等於|  
|ge|大於或等於|  
  
 如果根據選擇的運算子兩個值比較起來為相同，運算式將傳回 True。 否則，它將傳回 False。 如果其中一個值是空白時序，則運算式的結果將為 False。  
  
 這些運算子只能在單一不可部份完成值上運算。 也就是，您無法將某個序列指定為其中一個運算元。  
  
 例如，下列查詢會擷取\<圖片 > 產品型號圖片大小所在位置的項目 」 小：  
  
```  
SELECT CatalogDescription.query('         
              declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";         
              for $P in /PD:ProductDescription/PD:Picture[PD:Size eq "small"]         
              return         
                    $P         
             ') as Result         
FROM Production.ProductModel         
WHERE ProductModelID=19         
```  
  
 請注意下列項目是從上一個查詢而來：  
  
-   `declare namespace` 定義後續用於查詢中的命名空間前置詞。  
  
-   \<大小 > 項目值與指定不可部分完成的值，「 小型 」。  
  
-   請注意，因為值運算子只適用於不可部份完成值， **data （)** 隱含地利用函數來擷取節點值。 也就是，`data($P/PD:Size) eq "small"` 會產生相同的結果。  
  
 以下是結果：  
  
```  
\<PD:Picture   
  xmlns:PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">  
  \<PD:Angle>front\</PD:Angle>  
  \<PD:Size>small\</PD:Size>  
  \<PD:ProductPhotoID>31\</PD:ProductPhotoID>  
\</PD:Picture>  
```  
  
 請注意值比較的類型升級規則與一般比較的類型升級規則相同。 另外，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 會在進行值比較時為不具類型的值使用與進行一般比較時所使用的轉換規則相同的規則。 相對的，XQuery 規格永遠會在進行值比較時，將不具類型的值轉換為 xs:string。  
  
## <a name="node-comparison-operator"></a>節點比較運算子  
 節點比較運算子，**是**，只適用於節點類型。 它所傳回的結果會指出，以運算元傳遞的兩個節點是否代表來源文件中的相同節點。 如果兩個運算元是相同的節點，則此運算子此會傳回 True。 否則它會傳回 False。  
  
 下列查詢會檢查工作中心位置 10 在製造特定產品型號的過程中是否為第一個。  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions' AS AWMI)  
  
SELECT ProductModelID, Instructions.query('         
    if (  (//AWMI:root/AWMI:Location[@LocationID=10])[1]         
          is          
          (//AWMI:root/AWMI:Location[1])[1] )          
    then         
          <Result>equal</Result>         
    else         
          <Result>Not-equal</Result>         
         ') as Result         
FROM Production.ProductModel         
WHERE ProductModelID=7           
```  
  
 以下是結果：  
  
```  
ProductModelID       Result          
-------------- --------------------------  
7              <Result>equal</Result>      
```  
  
## <a name="node-order-comparison-operators"></a>節點順序比較運算子  
 節點順序比較運算子會根據文件中節點的位置來比較節點組。  
  
 這些是根據文件順序所做的比較：  
  
-   `<<` : **Operand 1**前面**operand 2**文件順序。  
  
-   `>>` : **Operand 1**遵循**operand 2**文件順序。  
  
 下列查詢會傳回 True，如果產品目錄描述中的\<擔保 > 元素之前出現\<維護 > 特定產品的文件順序中的項目。  
  
```  
WITH XMLNAMESPACES (  
  'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS PD,  
  'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS WM)  
  
SELECT CatalogDescription.value('  
     (/PD:ProductDescription/PD:Features/WM:Warranty)[1] <<   
           (/PD:ProductDescription/PD:Features/WM:Maintenance)[1]', 'nvarchar(10)') as Result  
FROM  Production.ProductModel  
where ProductModelID=19  
```  
  
 請注意下列項目是從上一個查詢而來：  
  
-   **Value （)** 方法**xml**資料型別用於查詢。  
  
-   查詢的布林值的結果會轉換成**nvarchar （10)** 後傳回。  
  
-   此查詢會傳回 True。  
  
## <a name="see-also"></a>另請參閱  
 [類型系統&#40;XQuery&#41;](../xquery/type-system-xquery.md)   
 [XQuery 運算式](../xquery/xquery-expressions.md)  
  
  
