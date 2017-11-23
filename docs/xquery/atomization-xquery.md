---
title: "自動化 (XQuery) |Microsoft 文件"
ms.custom: 
ms.date: 08/01/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: XML
helpviewer_keywords:
- XQuery, atomization
- atomization [XQuery]
ms.assetid: e3d7cf2f-c6fb-43c2-8538-4470a6375af5
caps.latest.revision: "16"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b6be2574663ce5b8f2cb51161033799543f4ca2e
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="atomization-xquery"></a>自動化 (XQuery)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  自動化是擷取項目的具類型值之處理序。 此處理序在某些情況下是隱含的。 有些 XQuery 運算子 (例如算術和比較運算子) 與此處理序相依。 比方說，當您算術運算子將直接套用至節點，節點的具類型的值是第一次擷取隱含地叫用[資料函式](../xquery/data-accessor-functions-data-xquery.md)。 這將會以運算元將不可部份完成值傳遞至算術運算子。  
  
 例如，下列查詢會傳回 LaborHours 屬性的總計。 在此情況下， **data （)**會隱含套用至屬性節點。  
  
```  
declare @x xml  
set @x='<ROOT><Location LID="1" SetupTime="1.1" LaborHours="3.3" />  
<Location LID="2" SetupTime="1.0" LaborHours="5" />  
<Location LID="3" SetupTime="2.1" LaborHours="4" />  
</ROOT>'  
-- data() implicitly applied to the attribute node sequence.  
SELECT @x.query('sum(/ROOT/Location/@LaborHours)')  
```  
  
 雖然並非必要，您也可以明確指定**data （)**函式：  
  
```  
SELECT @x.query('sum(data(ROOT/Location/@LaborHours))')  
```  
  
 另一個隱含自動化的範例是當您使用算術運算子時。 **+** 運算子需要不可部份完成值，和**data （)**隱含地套用至擷取 LaborHours 屬性不可部份完成值。 查詢針對 Instructions 資料行指定**xml** ProductModel 資料表中的類型。 下列查詢會傳回 LaborHours 屬性三次。 在查詢中，請注意下列項目：  
  
-   在建構 OrignialLaborHours 屬性時，自動化會隱含套用至 (`$WC/@LaborHours`) 所傳回的單一序列。 LaborHours 屬性具類型的值會指派給 OrignialLaborHours。  
  
-   在建構 UpdatedLaborHoursV1 屬性時，算術運算子需要不可部份完成值。 因此， **data （)**會隱含套用至所傳回的 LaborHours 屬性 (`$WC/@LaborHours`)。 接著就會在屬性中加入不可部份完成值 1。 屬性 UpdatedLaborHoursV2 的建構顯示明確的應用程式的**data （)**，但不是必要。  
  
```  
SELECT Instructions.query('  
     declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
for $WC in /AWMI:root/AWMI:Location[1]  
        return  
            <WC OriginalLaborHours = "{ $WC/@LaborHours }"  
                UpdatedLaborHoursV1 = "{ $WC/@LaborHours + 1 }"   
                UpdatedLaborHoursV2 = "{ data($WC/@LaborHours) + 1 }" >  
            </WC>') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 以下是結果：  
  
```  
<WC OriginalLaborHours="2.5"   
    UpdatedLaborHoursV1="3.5"   
    UpdatedLaborHoursV2="3.5" />  
```  
  
 自動化會產生簡單類型的執行個體、空集合或是靜態類型錯誤。  
  
 不可部分完成，也會發生在比較運算式參數傳遞至函式，傳回值的函式， **cast （)**運算式和子句所傳遞的順序排序的運算式。  
  
## <a name="see-also"></a>請參閱＜  
 [XQuery 基本概念](../xquery/xquery-basics.md)   
 [比較運算式 &#40;XQuery &#41;](../xquery/comparison-expressions-xquery.md)   
 [針對 xml 資料類型的 XQuery 函式](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
