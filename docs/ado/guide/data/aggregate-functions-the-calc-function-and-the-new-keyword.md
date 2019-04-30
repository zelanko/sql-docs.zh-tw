---
title: 彙總函式、 CALC 函式和 NEW 關鍵字 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 76fbb95117b1aae982242f24dc2cb1e815bc2356
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63063094"
---
# <a name="aggregate-functions-the-calc-function-and-the-new-keyword"></a>彙總函式、CALC 函式和 NEW 關鍵字
資料成形支援下列函數。 指派給包含的資料行的章節，以操作的名稱是*章別名*。  
  
 章別名可以是完整，導致一章包含每個章節資料行名稱所組成*資料行名稱*以句號分隔。 比方說，如果父本章 chap1，包含子章節，chap2，具有 amount 資料行時，amt，則限定的名稱會是 chap1.chap2.amt。  
  
|彙總函式|描述|  
|-------------------------|-----------------|  
|SUM (*章別名*。*資料行名稱*)|計算指定的資料行中的所有值的總和。|  
|AVG (*章別名*。*資料行名稱*)|計算指定的資料行中的所有值的平均值。|  
|最大值 (*章別名*。*資料行名稱*)|計算指定的資料行中的最大值。|  
|最小值 (*章別名*。*資料行名稱*)|計算指定的資料行中的最小值。|  
|計數 (*章別名*[。*資料行名稱*])|計算指定的別名中的資料列數目。 如果指定的資料行，則該資料行的非 Null 唯一資料列會包含在計數中。|  
|Stdev 函數 (*章別名*。*資料行名稱*)|計算指定的資料行中的標準差。|  
|任何 (*章別名*。*資料行名稱*)|指定的資料行的值。 任何具有可預測的值，只有資料行的值相同時一章中的所有資料列。<br /><br /> **請注意**如果資料行不包含所有一章中的資料列的相同值，SHAPE 命令任意傳回其中一個值的任何函式的值。|  
  
|導出的運算式|描述|  
|---------------------------|-----------------|  
|CALC(*expression*)|計算的任意的運算式，但只能出現在資料列**資料錄集**包含 CALC 函式。 使用這些方法的任何運算式[Visual Basic for Applications (VBA) 函式](../../../ado/guide/data/visual-basic-for-applications-functions.md)允許。|  
  
|新的關鍵字|描述|  
|-----------------|-----------------|  
|NEW *field-type* [(*width* &#124; *scale* &#124; *precision* &#124; *error* [, *scale* &#124; *error*])]|加入空白資料行指定型別的**資料錄集**。|  
  
 *欄位類型*傳遞包含新的關鍵字可以是任何下列資料類型。  
  
|OLE DB 資料類型|ADO 資料類型 equivalent(s)|  
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
|DBTYPE_BYTES|adBinary, AdVarBinary, adLongVarBinary|  
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
 [正式 Shape 文法](../../../ado/guide/data/formal-shape-grammar.md)   
 [一般 Shape 命令](../../../ado/guide/data/shape-commands-in-general.md)
