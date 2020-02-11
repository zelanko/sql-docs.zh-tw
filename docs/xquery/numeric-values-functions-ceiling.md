---
title: 上限函數（XQuery） |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:ceiling function
- ceiling function [XQuery]
ms.assetid: 594f1dd0-3c27-41b3-b809-9ce6714c5a97
author: rothja
ms.author: jroth
ms.openlocfilehash: fe18f488b83c1a8c9236c642751c1dc80bfe7e6c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67946572"
---
# <a name="numeric-values-functions---ceiling"></a>數值函式 - ceiling 
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  傳回不含小數的最小數字，不小於其引數的值。 如果引數是空的序列，它會傳回空的序列。  
  
## <a name="syntax"></a>語法  
  
```  
  
fn:ceiling ( $arg as numeric?) as numeric?  
```  
  
## <a name="arguments"></a>引數  
 *$arg*  
 會套用函數的數字。  
  
## <a name="remarks"></a>備註  
 如果 *$arg*的類型是三個數值基底類型之一（ **xs： float**、 **xs： double**或**xs： decimal**），則傳回類型與 *$arg*類型相同。  
  
 如果 *$arg*的類型是衍生自其中一個數數值型別的類型，則傳回類型會是基底數數值型別。  
  
 如果 fn： floor、fn：天花板或 fn： round 函數的輸入是**xdt： untypedAtomic**，它會隱含地轉換為**xs： double**。  
  
 任何其他類型都會產生靜態錯誤。  
  
## <a name="examples"></a>範例  
 本主題針對 XML 實例提供 XQuery 範例，這些實例是儲存在 AdventureWorks 資料庫的各種**xml**類型資料行中。  
  
### <a name="a-using-the-ceiling-xquery-function"></a>A. 使用 ceiling() XQuery 函數  
 對於「產品型號 7」，此查詢傳回產品型號之製造過程中的工作中心位置的清單。 如有記載，則此查詢會針對每一個工作中心位置，傳回位置識別碼、工時和批量。 此查詢會使用**上限**函數，以**decimal**類型的值來傳回勞動時數。  
  
```  
SELECT ProductModelID, Instructions.query('  
declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";   
     for $i in /AWMI:root/AWMI:Location  
     return   
       <Location LocationID="{ $i/@LocationID }"   
                   LaborHrs="{ ceiling($i/@LaborHours) }" >  
                    {   
                      $i/@LotSize  
                    }    
       </Location>  
') AS Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 請注意下列項目是從上一個查詢而來：  
  
-   AWMI 命名空間前置詞代表 Adventure Works Manufacturing Instructions。 此前置詞是指要查詢之文件中使用的相同命名空間。  
  
-   **指示**是**xml**類型資料行。 因此， [query （）方法（XML 資料類型）](../t-sql/xml/query-method-xml-data-type.md)會用來指定 XQuery。 XQuery 陳述式是指定成查詢方法的引數。  
  
-   **針對 .。。return**是迴圈結構。 在查詢中， **for**迴圈會識別> 元素的\<位置清單。 針對每個工作中心位置，「 **for**迴圈」中的**return**語句描述要產生的 XML：  
  
    -   具有\<LocationID 和 LaborHrs 屬性的位置> 元素。 大括號 ({ }) 內的相對應運算式從文件中擷取必要值。  
  
    -   {$i/@LotSize } 運算式會從檔中抓取 LotSize 屬性（如果有的話）。  
  
    -   以下是結果：  
  
```  
ProductModelID Result    
-------------- ------------------------------------------------------  
7      <Location LocationID="10" LaborHrs="3" LotSize="100"/>  
       <Location LocationID="20" LaborHrs="2" LotSize="1"/>     
       <Location LocationID="30" LaborHrs="1" LotSize="1"/>     
       <Location LocationID="45" LaborHrs="1" LotSize="20"/>  
       <Location LocationID="60" LaborHrs="3" LotSize="1"/>     
       <Location LocationID="60" LaborHrs="4" LotSize="1"/>  
```  
  
### <a name="implementation-limitations"></a>實作限制  
 以下為其限制：  
  
-   **上限（）** 函數會將所有整數值對應至 xs： decimal。  
  
## <a name="see-also"></a>另請參閱  
 [floor 函數 &#40;XQuery&#41;](../xquery/numeric-values-functions-floor.md)   
 [round 函數 &#40;XQuery&#41;](../xquery/numeric-values-functions-round.md)  
  
  
