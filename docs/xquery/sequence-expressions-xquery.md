---
title: "序列運算式 (XQuery) |Microsoft 文件"
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: xquery
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- sequence [XQuery]
- expressions [XQuery], sequence
- filtering sequences [XQuery]
ms.assetid: 41e18b20-526b-45d2-9bd9-e3b7d7fbce4e
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 50ed3ac28bad010247c8d117c950bb898305807a
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="sequence-expressions-xquery"></a>序列運算式 (XQuery)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 支援用來建構、 篩選和結合項目序列的 XQuery 運算子。 項目可以是不可部份完成值或節點。  
  
## <a name="constructing-sequences"></a>建構序列  
 您可以使用逗號運算子，建構將項目串連成單一序列的序列。  
  
 序列可以包含重複的值。 巢狀序列 (即在序列內的序列) 將會被摺疊起來。 例如，序列 (1, 2, (3, 4, (5))) 會變成 (1, 2, 3, 4, 5)。 這些是建構序列的範例。  
  
### <a name="example-a"></a>範例 A  
 下列查詢傳回的序列包含五個不可部份完成的值：  
  
```  
declare @x xml  
set @x=''  
select @x.query('(1,2,3,4,5)')  
go  
-- result 1 2 3 4 5  
```  
  
 下列查詢傳回的序列包含兩個節點：  
  
```  
-- sequence of 2 nodes  
declare @x xml  
set @x=''  
select @x.query('(<a/>, <b/>)')  
go  
-- result  
<a />  
<b />  
```  
  
 因為您建構的序列包含不可部份完成的值和節點，下列查詢將傳回錯誤。 此為異質性序列，並且不受支援。  
  
```  
declare @x xml  
set @x=''  
select @x.query('(1, 2, <a/>, <b/>)')  
go  
```  
  
### <a name="example-b"></a>範例 B  
 下列查詢會將四個長度不同的時序組合成單一時序，建構一連串不可部份完成的值。  
  
```  
declare @x xml  
set @x=''  
select @x.query('(1,2),10,(),(4, 5, 6)')  
go  
-- result = 1 2 10 4 5 6  
```  
  
 您可以使用 FLOWR 和 ORDER BY 將序列排序：  
  
```  
declare @x xml  
set @x=''  
select @x.query('for $i in ((1,2),10,(),(4, 5, 6))  
                  order by $i  
                  return $i')  
go  
```  
  
 您可以使用計算序列中的項目**fn**函式。  
  
```  
declare @x xml  
set @x=''  
select @x.query('count( (1,2,3,(),4) )')  
go  
-- result = 4  
```  
  
### <a name="example-c"></a>範例 C  
 下列查詢針對 AdditionalContactInfo 資料行指定**xml** Contact 資料表中的型別。 這個資料行會儲存其他的連絡資訊，例如一或多個其他的電話號碼、呼叫器號碼和地址。 \<TelephoneNumber >，\<頁面巡覽區 >，且其他節點可以任何位置出現在文件。 此查詢會建構序列，其中包含所有\<telephoneNumber > 子系內容節點，後面接著\<頁面巡覽區 > 子系。 請注意，在 return 運算式 (`($a//act:telephoneNumber, $a//act:pager)`) 中使用逗號序列運算子。  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes' AS act,  
 'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo' AS aci)  
  
SELECT AdditionalContactInfo.query('  
   for $a in /aci:AdditionalContactInfo   
   return ($a//act:telephoneNumber, $a//act:pager)  
') As Result  
FROM Person.Contact  
WHERE ContactID=3  
```  
  
 以下是結果：  
  
```  
<act:telephoneNumber xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
  <act:number>333-333-3333</act:number>  
</act:telephoneNumber>  
<act:telephoneNumber xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
  <act:number>333-333-3334</act:number>  
</act:telephoneNumber>  
<act:pager xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
  <act:number>999-555-1244</act:number>  
  <act:SpecialInstructions>  
Page only in case of emergencies.  
</act:SpecialInstructions>  
</act:pager>  
```  
  
## <a name="filtering-sequences"></a>篩選序列  
 您可以將述詞加入到運算式中，來篩選運算式傳回的序列。 如需詳細資訊，請參閱[路徑運算式 &#40;XQuery &#41;](../xquery/path-expressions-xquery.md). 例如，下列查詢傳回的序列包含三個 <`a`> 元素節點：  
  
```  
declare @x xml  
set @x = '<root>  
<a attrA="1">111</a>  
<a></a>  
<a></a>  
</root>'  
SELECT @x.query('/root/a')  
```  
  
 以下是結果：  
  
```  
<a attrA="1">111</a>  
<a />  
<a />  
```  
  
 若只要擷取具有 attrA 屬性的 <`a`> 元素，您可以在述詞中指定篩選。 產生的序列將只會有一個 <`a`> 元素。  
  
```  
declare @x xml  
set @x = '<root>  
<a attrA="1">111</a>  
<a></a>  
<a></a>  
</root>'  
SELECT @x.query('/root/a[@attrA]')  
```  
  
 以下是結果：  
  
```  
<a attrA="1">111</a>  
```  
  
 如需如何在路徑運算式中指定述詞的詳細資訊，請參閱[路徑運算式步驟中指定的述詞](../xquery/path-expressions-specifying-predicates.md)。  
  
 下列範例會建立一個子樹的序列運算式，然後將篩選套用到序列中。  
  
```  
declare @x xml  
set @x = '  
<a>  
  <c>C under a</c>  
</a>  
<b>    
   <c>C under b</c>  
</b>  
<c>top level c</c>  
<d></d>  
'  
```  
  
 `(/a, /b)` 中的運算式會建構一個含有子樹 `/a` 及 `/b` 的序列，運算式並會從產生的序列篩選元素 `<c>`。  
  
```  
SELECT @x.query('  
  (/a, /b)/c  
')  
```  
  
 以下是結果：  
  
```  
<c>C under a</c>  
<c>C under b</c>  
```  
  
 下列範例會套用述詞篩選。 運算式將尋找包含 <`c`> 元素的 <`a`> 元素和 <`b`> 元素。  
  
```  
declare @x xml  
set @x = '  
<a>  
  <c>C under a</c>  
</a>  
<b>    
   <c>C under b</c>  
</b>  
  
<c>top level c</c>  
<d></d>  
'  
SELECT @x.query('  
  (/a, /b)[c]  
')  
```  
  
 以下是結果：  
  
```  
<a>  
  <c>C under a</c>  
</a>  
<b>  
  <c>C under b</c>  
</b>  
```  
  
### <a name="implementation-limitations"></a>實作限制  
 以下為其限制：  
  
-   不支援 XQuery 範圍運算式。  
  
-   序列必須是同質的。 特別是，序列中的所有項目必須是節點或是不可部份完成的值。 將會靜態地檢查。  
  
-   不支援使用 UNION、INTERSECT 或 EXCEPT 運算子結合的節點順序。  
  
## <a name="see-also"></a>另請參閱  
 [XQuery 運算式](../xquery/xquery-expressions.md)  
  
  
