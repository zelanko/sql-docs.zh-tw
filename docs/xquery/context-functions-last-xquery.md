---
title: last 函數（XQuery） |Microsoft Docs
description: 深入瞭解 XQuery last （）函式，此函數會傳回序列中最後一個專案的整數索引。
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- last function [XQuery]
- fn:last function
ms.assetid: dc92086e-3b01-4b0b-9f54-3bbf306cf7ae
author: rothja
ms.author: jroth
ms.openlocfilehash: f88c438206551e170810f467e7944b21232e245d
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84529702"
---
# <a name="context-functions---last-xquery"></a>內容函式 - last (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  傳回目前所處理序列中的項目號碼。 具體而言，它會傳回序列中最後一個項目的整數索引。 序列中第一個項目的索引值為 1。  
  
## <a name="syntax"></a>語法  
  
```  
  
fn:last() as xs:integer  
```  
  
## <a name="remarks"></a>備註  
 在 SQL Server 中， **fn： last （）** 只能用於內容相依述詞的內容中。 具體而言，它只能在括號 (`[ ]`) 內使用。  
  
## <a name="examples"></a>範例  
 本主題針對 XML 實例提供 XQuery 範例，這些實例是儲存在 AdventureWorks 資料庫的各種**xml**類型資料行中。  
  
### <a name="a-using-the-last-xquery-function-to-retrieve-the-last-two-manufacturing-steps"></a>A. 使用 last() XQuery 函數以擷取最後兩個製造步驟  
 下列查詢會擷取特定產品型號的最後兩個製造步驟。 在此查詢中，會使用**最後一個（）** 函數所傳回的值（製造步驟數目）來抓取最後兩個製造步驟。  
  
```  
SELECT ProductModelID, Instructions.query('   
declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
  <LastTwoManuSteps>  
   <Last-1Step>   
     { (/AWMI:root/AWMI:Location)[1]/AWMI:step[(last()-1)]/text() }  
   </Last-1Step>  
   <LastStep>   
     { (/AWMI:root/AWMI:Location)[1]/AWMI:step[last()]/text() }  
   </LastStep>  
  </LastTwoManuSteps>  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 在上述查詢中，/中的**最後一個（）** 函數會傳回 `/AWMI:root//AWMI:Location)[1]/AWMI:step[last()]` 製造步驟的數目。 此值是用以擷取工作中心位置的最後一個製造步驟。  
  
 以下是結果：  
  
```  
ProductModelID Result    
-------------- -------------------------------------  
7      <LastTwoManuSteps>  
         <Last-1Step>  
            When finished, inspect the forms for defects per   
            Inspection Specification .  
         </Last-1Step>  
         <LastStep>Remove the frames from the tool and place them   
            in the Completed or Rejected bin as appropriate.  
         </LastStep>  
       </LastTwoManuSteps>  
```  
  
## <a name="see-also"></a>另請參閱  
 [針對 xml 資料類型的 XQuery 函數](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
