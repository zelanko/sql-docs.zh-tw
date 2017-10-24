---
title: "彙總函式、 CALC 函式和 NEW 關鍵字 |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data shaping [ADO], functions
- CALC function [ADO]
- NEW keyword [ADO]
- aggregate functions [ADO]
ms.assetid: 0590b466-2a36-49a2-868e-028ef5e49394
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f24280f155fd5ec6bd86b8486b0f8f77338d8eb6
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="aggregate-functions-the-calc-function-and-the-new-keyword"></a>彙總函式、 CALC 函式和 NEW 關鍵字
資料成形支援下列函數。 要處理指派章節包含的資料行的名稱是*章別名*。  
  
 章別名可以是完整，導致章節包含每個章節資料行名稱所組成*資料行名稱，*以句號分隔。 例如，如果父章 chap1，包含子章節，chap2，都具有 amount 資料行時，amt，就限定的名稱會是 chap1.chap2.amt。  
  
|彙總函式|Description|  
|-------------------------|-----------------|  
|SUM (*章別名*。*資料行名稱*)|計算指定的資料行中的所有值的總和。|  
|AVG (*章別名*。*資料行名稱*)|計算指定的資料行中的所有值的平均值。|  
|最大值 (*章別名*。*資料行名稱*)|計算指定的資料行中的最大值。|  
|MIN (*章別名*。*資料行名稱*)|計算指定的資料行中的最小值。|  
|計數 (*章別名*[。*資料行名稱*])|計算指定的別名中的資料列數目。 如果指定資料行，則該資料行的非 Null 唯一資料列會包含在計數中。|  
|Stdev 函數 (*章別名*。*資料行名稱*)|計算標準差，指定資料行中。|  
|任何 (*章別名*。*資料行名稱*)|指定的資料行的值。 任何在資料行的值是相同的章節中的所有資料列時，才有可預測的值。<br /><br /> **請注意**資料行不包含所有一章中的資料列的相同值，如果 SHAPE 命令任意傳回其中一個值的任何函式的值。|  
  
|計算的運算式|Description|  
|---------------------------|-----------------|  
|計算 (*運算式*)|計算的任意的運算式，但只能出現在資料列**資料錄集**包含 CALC 函式。 使用這些任何運算式[Visual Basic for Applications (VBA) 函數](../../../ado/guide/data/visual-basic-for-applications-functions.md)允許。|  
  
|NEW 關鍵字|Description|  
|-----------------|-----------------|  
|新*欄位類型*[(*寬度*&#124;*標尺*&#124;*精確度*&#124;*錯誤*[，*標尺*&#124;*錯誤*])]|加入空白資料行指定的型別**資料錄集**。|  
  
 *欄位類型*傳遞包含新的關鍵字可以是任何一個下列資料類型。  
  
|OLE DB 資料類型|ADO 資料類型 equivalent(s)|  
|-----------------------|-----------------------------------|  
|DBTYPE_BSTR|adBSTR|  
|DBTYPE_BOOL|AdBoolean|  
|DBTYPE_DECIMAL|adDecimal|  
|DBTYPE_UI1|adUnsignedTinyInt|  
|DBTYPE_I1|adTinyInt|  
|DBTYPE_UI2|adUnsignedSmallInt|  
|DBTYPE_UI4|adUnsignedInt|  
|DBTYPE_I8|adBigInt|  
|DBTYPE_UI8|adUnsignedBigInt|  
|DBTYPE_GUID|adGuid|  
|DBTYPE_BYTES|adBinary，AdVarBinary，adLongVarBinary|  
|DBTYPE_STR|adChar adVarChar adLongVarChar|  
|DBTYPE_WSTR|adWChar adVarWChar adLongVarWChar|  
|DBTYPE_NUMERIC|adNumeric|  
|DBTYPE_DBDATE|adDBDate|  
|DBTYPE_DBTIME|adDBTime|  
|DBTYPE_DBTIMESTAMP|adDBTimeStamp|  
|DBTYPE_VARNUMERIC|adVarNumeric|  
|DBTYPE_FILETIME|adFileTime|  
|DBTYPE_ERROR|adError|  
  
 當新欄位的型別 decimal （OLE db DBTYPE_DECIMAL，或在 ADO 中，adDecimal） 時，您必須指定有效位數和小數位數的值。  
  
## <a name="see-also"></a>另請參閱  
 [資料成形範例](../../../ado/guide/data/data-shaping-example.md)   
 [型式圖形文法](../../../ado/guide/data/formal-shape-grammar.md)   
 [在一般的圖形命令](../../../ado/guide/data/shape-commands-in-general.md)

