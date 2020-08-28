---
description: 彙總函式、CALC 函式和 NEW 關鍵字
title: 彙總函式、CALC 函式和 NEW 關鍵字 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 1b62e392325306bc358283874f4638077d8a4178
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991629"
---
# <a name="aggregate-functions-the-calc-function-and-the-new-keyword"></a>彙總函式、CALC 函式和 NEW 關鍵字
資料成形支援下列功能。 指派給包含要操作之資料行的章節名稱是 *章節別名*。  
  
 章節別名可以是完整的，其中包含每個章節的資料行名稱，包含資料 *行名稱，* 全都以句號分隔。 例如，如果父系章節 chap1 包含的子章節 chap2 （具有金額資料行 amt），則限定名稱會是 chap1. chap2. amt。  
  
|彙總函式|描述|  
|-------------------------|-----------------|  
|SUM (*章節別名*。資料*行名稱*) |計算指定之資料行中所有值的總和。|  
|AVG (*章節-別名*。資料*行名稱*) |計算指定之資料行中所有值的平均值。|  
|最大 (*章節-別名*。資料*行名稱*) |計算指定之資料行中的最大值。|  
|最小 (*章節別名*。資料*行名稱*) |計算指定之資料行中的最小值。|  
|COUNT (*章節別名*[.*資料行名稱*] ) |計算指定之別名中的資料列數目。 如果指定了資料行，計數中只會包含該資料行不是 Null 的資料列。|  
|STDEV (*章節別名*。資料*行名稱*) |計算指定之資料行中的標準差。|  
|任何 (*章節別名*。資料*行名稱*) |指定之資料行的值。 只有在資料行的值與章節中所有資料列的值相同時，才會有可預測的值。<br /><br /> **注意** 如果資料行不包含章節中所有資料列的相同值，則 SHAPE 命令會任意傳回其中一個值，做為 ANY 函數的值。|  
  
|計算運算式|描述|  
|---------------------------|-----------------|  
|CALC (*運算式*) |計算任意運算式，但只在包含 CALC 函數之 **記錄集** 的資料列上。 使用這些 [Visual Basic for Applications (VBA) 函數](./visual-basic-for-applications-functions.md) 的任何運算式都是允許的。|  
  
|NEW 關鍵字|描述|  
|-----------------|-----------------|  
|新 *的欄位-類型* [ (*寬度* &#124; *小* 數位數 &#124; *精確度* &#124; *錯誤* [， *小* 數位數 &#124; *錯誤*] ) ]|將指定類型的空白資料行加入至 **記錄集**。|  
  
 以 NEW 關鍵字傳遞的 *欄位型* 別可以是下列任何一種資料類型。  
  
|OLE DB 資料類型|ADO 資料類型對等的 (s) |  
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
|DBTYPE_STR|adChar、adVarChar、adLongVarChar|  
|DBTYPE_WSTR|adWChar, adVarWChar, adLongVarWChar|  
|DBTYPE_NUMERIC|adNumeric|  
|DBTYPE_DBDATE|adDBDate|  
|DBTYPE_DBTIME|adDBTime|  
|DBTYPE_DBTIMESTAMP|adDBTimeStamp|  
|DBTYPE_VARNUMERIC|adVarNumeric|  
|DBTYPE_FILETIME|adFileTime|  
|DBTYPE_ERROR|adError|  
  
 當新欄位的類型為 decimal (OLE DB、DBTYPE_DECIMAL 或在 ADO 中為 adDecimal) 時，您必須指定有效位數和小數位數的值。  
  
## <a name="see-also"></a>另請參閱  
 [資料成形範例](./data-shaping-example.md)   
 [正式式圖形文法](./formal-shape-grammar.md)   
 [一般 Shape 命令](./shape-commands-in-general.md)