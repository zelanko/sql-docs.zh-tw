---
title: 彙總函式、CALC 函數和 NEW 關鍵字 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data shaping [ADO], functions
- CALC function [ADO]
- NEW keyword [ADO]
- aggregate functions [ADO]
ms.assetid: 0590b466-2a36-49a2-868e-028ef5e49394
author: rothja
ms.author: jroth
ms.openlocfilehash: 7bda85bae42b294fa63c67adfe51d8c60c5b56af
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82761274"
---
# <a name="aggregate-functions-the-calc-function-and-the-new-keyword"></a>彙總函式、CALC 函式和 NEW 關鍵字
資料成形支援下列函數。 指派給包含要操作之資料行之章節的名稱是*章節別名*。  
  
 章節別名可以是完整格式，由每個章節的資料行名稱組成，其中包含資料行*名稱，* 並以句號分隔。 例如，如果父系章節 chap1 包含一個子章節 chap2，其中具有金額資料行 amt，則限定名稱會是 chap1. chap2 amt。  
  
|彙總函式|說明|  
|-------------------------|-----------------|  
|總和（*章節-別名）*。*資料行名稱*）|計算指定之資料行中所有值的總和。|  
|AVG （*章節-別名）*。*資料行名稱*）|計算指定資料行中所有值的平均值。|  
|最大值（*章節-別名）*。*資料行名稱*）|計算指定之資料行中的最大值。|  
|最小值（*章節-別名）*。*資料行名稱*）|計算指定資料行中的最小值。|  
|COUNT （*章節-別名*[。*資料行名稱*]）|計算指定之別名中的資料列數目。 如果指定了資料行，此計數只會包含該資料行非 Null 的資料列。|  
|STDEV （*章節-別名*。*資料行名稱*）|計算指定之資料行中的標準差。|  
|任何（*章節-別名*。*資料行名稱*）|指定之資料行的值。 只有當章節中的所有資料列的資料行值都相同時，ANY 才會有可預測的值。<br /><br /> **注意**如果資料行在章節中的所有資料列都未包含相同的值，則 SHAPE 命令會任意傳回其中一個值，以做為 ANY 函數的值。|  
  
|計算運算式|說明|  
|---------------------------|-----------------|  
|CALC （*expression*）|計算任意運算式，但僅限於包含 CALC 函數的**記錄集**資料列。 允許使用這些[Visual Basic for Applications （VBA）函數](../../../ado/guide/data/visual-basic-for-applications-functions.md)的任何運算式。|  
  
|NEW 關鍵字|說明|  
|-----------------|-----------------|  
|新*的欄位類型*[（*寬度*&#124;*小*數位數 &#124;*精確度*&#124;*錯誤*[，*調整*&#124;*錯誤*]）]|將指定類型的空白資料行加入至**記錄集**。|  
  
 使用 NEW 關鍵字傳遞的*欄位類型*可以是下列任何一種資料類型。  
  
|OLE DB 資料類型|ADO 資料類型對等|  
|-----------------------|-----------------------------------|  
|DBTYPE_BSTR|adBSTR|  
|DBTYPE_BOOL|adBoolean|  
|DBTYPE_DECIMAL|adDecimal|  
|DBTYPE_UI1|adUnsignedTinyInt|  
|DBTYPE_I1|adTinyInt|  
|DBTYPE_UI2|adUnsignedSmallInt|  
|DBTYPE_UI4|adUnsignedInt|  
|DBTYPE_I8|adBigInt|  
|DBTYPE_UI8|adUnsignedBigInt|  
|DBTYPE_GUID|adGuid|  
|DBTYPE_BYTES|adBinary、AdVarBinary、adLongVarBinary|  
|DBTYPE_STR|adChar、adVarChar、adLongVarChar|  
|DBTYPE_WSTR|adWChar、adVarWChar、adLongVarWChar|  
|DBTYPE_NUMERIC|adNumeric|  
|DBTYPE_DBDATE|adDBDate|  
|DBTYPE_DBTIME|adDBTime|  
|DBTYPE_DBTIMESTAMP|adDBTimeStamp|  
|DBTYPE_VARNUMERIC|adVarNumeric|  
|DBTYPE_FILETIME|adFileTime|  
|DBTYPE_ERROR|adError|  
  
 當新欄位的類型為 decimal （在 OLE DB 中，DBTYPE_DECIMAL，或在 ADO 中為 adDecimal）時，您必須指定有效位數和小數位數的值。  
  
## <a name="see-also"></a>另請參閱  
 [資料成形範例](../../../ado/guide/data/data-shaping-example.md)   
 [正式圖形文法](../../../ado/guide/data/formal-shape-grammar.md)   
 [一般 Shape 命令](../../../ado/guide/data/shape-commands-in-general.md)
