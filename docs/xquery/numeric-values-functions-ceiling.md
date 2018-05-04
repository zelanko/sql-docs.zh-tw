---
title: ceiling 函數 (XQuery) |Microsoft 文件
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql
ms.service: ''
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
- fn:ceiling function
- ceiling function [XQuery]
ms.assetid: 594f1dd0-3c27-41b3-b809-9ce6714c5a97
caps.latest.revision: 30
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: f143f66c9db70b7777e8a1c36f00cbc8486b2bcb
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="numeric-values-functions---ceiling"></a>數字的值函式-ceiling 
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
 如果類型 *$arg*是三個字的基底類型，其中**xs: float**， **xs: double**，或**xs: decimal**，傳回的型別是相同 *$arg*型別。  
  
 如果類型 *$arg*是衍生自其中一個數字類型，類型的傳回型別是基底的數值類型。  
  
 如果 fn: floor、 fn: ceiling 或 fn: round 函數的輸入是**xdt: untypedatomic**，它會隱含地轉換為**xs: double**。  
  
 任何其他類型都會產生靜態錯誤。  
  
## <a name="examples"></a>範例  
 本主題提供 XQuery 範例，針對 XML 執行個體儲存在各種**xml**類型 AdventureWorks 資料庫中的資料行。  
  
### <a name="a-using-the-ceiling-xquery-function"></a>A. 使用 ceiling() XQuery 函數  
 對於「產品型號 7」，此查詢傳回產品型號之製造過程中的工作中心位置的清單。 如有記載，則此查詢會針對每一個工作中心位置，傳回位置識別碼、工時和批量。 此查詢會使用**ceiling**函數傳回工時，做為型別的值**十進位**。  
  
```  
SELECT ProductModelID, Instructions.query('  
declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";   
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
  
-   **指示**是**xml**類型資料行。 因此， [query （） 方法 （XML 資料類型）](../t-sql/xml/query-method-xml-data-type.md)用來指定 XQuery。 XQuery 陳述式是指定成查詢方法的引數。  
  
-   **for...傳回**是迴圈建構。 在查詢中，**如**迴圈識別一份\<位置 > 項目。 針對每個工作中心位置，**傳回**陳述式中的**如**迴圈描述要產生的 XML:  
  
    -   A\<位置 > 有 LocationID 和 LaborHrs 屬性的項目。 大括號 ({ }) 內的相對應運算式從文件中擷取必要值。  
  
    -   {$i/@LotSize } 運算式擷取 LotSize 屬性文件中，如果有的話。  
  
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
  
-   **Ceiling （)** 函式會將所有的整數值對應至 xs: decimal。  
  
## <a name="see-also"></a>另請參閱  
 [floor 函式&#40;XQuery&#41;](../xquery/numeric-values-functions-floor.md)   
 [round 函式&#40;XQuery&#41;](../xquery/numeric-values-functions-round.md)  
  
  
