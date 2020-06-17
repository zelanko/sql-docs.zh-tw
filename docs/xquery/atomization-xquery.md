---
title: 不可部分完成（XQuery） |Microsoft Docs
description: 瞭解不可部分完成在 XQuery 中的程式，其中專案的具類型值會解壓縮到其中。
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- XQuery, atomization
- atomization [XQuery]
ms.assetid: e3d7cf2f-c6fb-43c2-8538-4470a6375af5
author: rothja
ms.author: jroth
ms.openlocfilehash: 70d623d8583535aae7ddcc23f26ab7c5e4e36fc7
ms.sourcegitcommit: 5c7634b007f6808c87094174b80376cb20545d5f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84886887"
---
# <a name="atomization-xquery"></a>自動化 (XQuery)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  自動化是擷取項目的具類型值之處理序。 此處理序在某些情況下是隱含的。 有些 XQuery 運算子 (例如算術和比較運算子) 與此處理序相依。 例如，當您將算術運算子直接套用至節點時，節點的具類型值會先隱含叫用[資料函數](../xquery/data-accessor-functions-data-xquery.md)來取得。 這將會以運算元將不可部份完成值傳遞至算術運算子。  
  
 例如，下列查詢會傳回 LaborHours 屬性的總計。 在此情況下，**資料（）** 會隱含套用至屬性節點。  
  
```  
declare @x xml  
set @x='<ROOT><Location LID="1" SetupTime="1.1" LaborHours="3.3" />  
<Location LID="2" SetupTime="1.0" LaborHours="5" />  
<Location LID="3" SetupTime="2.1" LaborHours="4" />  
</ROOT>'  
-- data() implicitly applied to the attribute node sequence.  
SELECT @x.query('sum(/ROOT/Location/@LaborHours)')  
```  
  
 雖然並非必要，但您也可以明確指定**data （）** 函數：  
  
```  
SELECT @x.query('sum(data(ROOT/Location/@LaborHours))')  
```  
  
 另一個隱含自動化的範例是當您使用算術運算子時。 **+** 運算子需要不可部分完成的值，而且會隱含地套用**data （）** ，以取得 LaborHours 屬性的不可部分完成值。 查詢是針對 ProductModel 資料表中**xml**類型的 [指示] 資料行所指定。 下列查詢會傳回 LaborHours 屬性三次。 在查詢中，請注意下列項目：  
  
-   在建構 OrignialLaborHours 屬性時，自動化會隱含套用至 (`$WC/@LaborHours`) 所傳回的單一序列。 LaborHours 屬性具類型的值會指派給 OrignialLaborHours。  
  
-   在建構 UpdatedLaborHoursV1 屬性時，算術運算子需要不可部份完成值。 因此，**資料（）** 會隱含地套用至（）所傳回的 LaborHours 屬性 `$WC/@LaborHours` 。 接著就會在屬性中加入不可部份完成值 1。 [屬性 UpdatedLaborHoursV2] 的結構會顯示資料的明確應用 **（）**，但不是必要的。  
  
```  
SELECT Instructions.query('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
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
  
 不可部分完成也會發生在傳遞至函式的比較運算式參數、函式所傳回的值、 **cast （）** 運算式，以及 order by 子句中傳遞的排序運算式。  
  
## <a name="see-also"></a>另請參閱  
 [XQuery 基本概念](../xquery/xquery-basics.md)   
 [&#40;XQuery&#41;的比較運算式](../xquery/comparison-expressions-xquery.md)   
 [針對 xml 資料類型的 XQuery 函數](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
