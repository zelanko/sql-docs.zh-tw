---
title: 有效的布林值 (XQuery) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql
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
- effective Boolean value [XQuery]
- Boolean values
- XQuery, effective Boolean values
- EBV
ms.assetid: 506682b1-b6c9-45e2-aa54-7abd5844c3f1
caps.latest.revision: 17
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 4ab470f5643335cd1ed26edd07aa93284bab1d47
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33077515"
---
# <a name="effective-boolean-value-xquery"></a>有效的布林值 (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  下列為有效的布林值：  
  
-   如果運算元是空的序列或 Boolean false，則為 False。  
  
-   否則，此值為 True。  
  
 對於會傳回單一布林值、節點序列或空序列的運算式，可以計算出有效的布林值。 請注意，在處理下列類型的運算式時，會隱含地計算布林值。  
  
-   邏輯運算式  
  
-   [無法運作](../xquery/functions-on-boolean-values-not-function.md)  
  
-   FLWOR 運算式的 WHERE 子句  
  
-   [條件運算式](../xquery/conditional-expressions-xquery.md)  
  
-   [QuantifiedeExpressions](../xquery/quantified-expressions-xquery.md)  
  
 下列是有效布林值的範例。 當**如果**運算式的處理，決定條件的有效布林值。 因為 `/a[1]` 會傳回空的序列，所以有效布林值為 False。 傳回的結果會是具有一個文字節點 (False) 的 XML。  
  
```  
value is false  
DECLARE @x XML  
SET @x = '<b/>'  
SELECT @x.query('if (/a[1]) then "true" else "false"')  
go  
```  
  
 下列範例中，因為運算式會傳回非空的序列，所以有效布林值為 True。  
  
```  
DECLARE @x XML  
SET @x = '<a/>'  
SELECT @x.query('if (/a[1]) then "true" else "false"')  
go  
```  
  
 在查詢具類型**xml**資料行或變數，您可以有布林類型的節點。 **Data （)** 在此情況下會傳回布林值。 如果查詢運算式傳回的布林值為 True，則有效布林值即為 True，如下個範例所示。 範例中也說明下列各項：  
  
-   建立 XML 結構描述集合。 項目\<b > 集合中是屬於布林類型。  
  
-   具型別的**xml**變數已建立並查詢。  
  
-   `data(/b[1])` 運算式會傳回布林值 True。 因此，此情況中的有效布林值是 True。  
  
-   運算式`data(/b[2])`傳回布林值 false。 因此，此情況中的有效布林值是 False。  
  
```  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema">  
      <element name="s" type="string"/>  
      <element name="b" type="boolean"/>  
</schema>'  
go  
DECLARE @x XML(SC)  
SET @x = '<b>true</b><b>false</b>'  
SELECT @x.query('if (data(/b[1])) then "true" else "false"')  
SELECT @x.query('if (data(/b[2])) then "true" else "false"')  
go  
```  
  
## <a name="see-also"></a>另請參閱  
 [XQuery 基本概念](../xquery/xquery-basics.md)   
 [FLWOR 陳述式和反覆項目&#40;XQuery&#41;](../xquery/flwor-statement-and-iteration-xquery.md)  
  
  
