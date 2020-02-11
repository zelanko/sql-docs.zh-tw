---
title: 針對 xml 資料類型的 XQuery 運算子 |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- XQuery, operators
- operators [XQuery]
- xml data type [SQL Server], XQuery
ms.assetid: 39ca3d2e-e928-4333-872b-75c4ccde8e79
author: rothja
ms.author: jroth
ms.openlocfilehash: b113fbd8111072790d1f0904b3e751c6629725b2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67945950"
---
# <a name="xquery-operators-against-the-xml-data-type"></a>針對 xml 資料類型的 XQuery 運算子
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  XQuery 支援下列運算子：  
  
-   數值運算子 (+, -, *, div, mod)  
  
-   用於值比較的運算子 (eq, ne, lt, gt, le, ge)  
  
-   一般比較的運算子（=，！ =， \<，>， \<=，>=）  
  
 如需這些運算子的詳細資訊，請參閱[&#40;XQuery 的比較運算式&#41;](../xquery/comparison-expressions-xquery.md)  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-general-operators"></a>A. 使用一般運算子  
 此查詢會說明套用到序列與比較序列的一般運算子使用方式。 此查詢會從**Contact**資料表的**AdditionalContactInfo**資料行中，抓取每個客戶的電話號碼序列。 然後，將此序列和這兩個電話號碼的序列 ("111-111-1111", "222-2222") 比較。  
  
 查詢會使用**=** 比較運算子。 **=** 運算子右邊順序中的每個節點會與左側序列中的每個節點進行比較。 如果節點相符，節點的比較就會是**TRUE**。 接著會轉換為整數並和 1 進行比較，然後查詢會傳回客戶識別碼。  
  
```sql
WITH XMLNAMESPACES (  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo' AS ACI,  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes' AS ACT)  
SELECT ContactID   
FROM   Person.Contact  
WHERE  AdditionalContactInfo.value('  
      //ACI:AdditionalContactInfo//ACT:telephoneNumber/ACT:number =   
          ("111-111-1111", "222-2222")',  
      'bit')= cast(1 as bit)  
```  
  
 還有另一種方式可以觀察前一個查詢的運作方式：每個從**AdditionalContactInfo**資料行取出的電話電話號碼值都會與兩個電話號碼的集合進行比較。 如果值位於集合中，則結果中就會傳回該客戶。  
  
### <a name="b-using-a-numeric-operator"></a>B. 使用數值運算子  
 此查詢中的 + 運算子是值運算子，因為它會套用到單一項目。 例如，值 1 會加入到查詢傳回的配置大小：  
  
```sql
SELECT ProductModelID, Instructions.query('  
     declare namespace   
 AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
     for $i in (/AWMI:root/AWMI:Location)[1]  
     return   
       <Location LocationID="{ ($i/@LocationID) }"  
                   LotSize  = "{  number($i/@LotSize) }"  
                   LotSize2 = "{ number($i/@LotSize) + 1 }"  
                   LotSize3 = "{ number($i/@LotSize) + 2 }" >  
  
       </Location>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
### <a name="c-using-a-value-operator"></a>C. 使用值運算子  
 下列查詢會抓取產品型號`Picture`的 <> 元素，其中的圖片大小為「小型」：  
  
```sql
SELECT CatalogDescription.query('  
     declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     for $P in /PD:ProductDescription/PD:Picture[PD:Size eq "small"]  
     return  
           $P  
    ') as Result  
FROM Production.ProductModel  
where ProductModelID=19  
```  
  
 因為**eq**運算子的兩個運算元都是不可部分完成的值，所以在查詢中會使用 value 運算子。 您可以使用一般比較運算子（ **=** ）撰寫相同的查詢。  
  
## <a name="see-also"></a>另請參閱  
 [針對 xml 資料類型的 XQuery 函數](../xquery/xquery-functions-against-the-xml-data-type.md)   
 [XML 資料 &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [XQuery 語言參考 &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)  
  
  
