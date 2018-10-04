---
title: GetString 方法 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::raw_GetString
- Recordset20::GetString
helpviewer_keywords:
- GetString method [ADO]
ms.assetid: 92452940-b2a7-456e-94fc-3780c71da33c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1570918c423291b6c4fdd212fcb82f518dfb766e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47708056"
---
# <a name="getstring-method-ado"></a>GetString 方法 (ADO)
傳回[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)做為字串。  
  
## <a name="syntax"></a>語法  
  
```  
  
Variant = recordset.GetString(StringFormat, NumRows, ColumnDelimiter, RowDelimiter, NullExpr)  
```  
  
## <a name="return-value"></a>傳回值  
 傳回**Recordset**做為字串值**Variant** (BSTR)。  
  
#### <a name="parameters"></a>參數  
 *StringFormat*  
 A [StringFormatEnum](../../../ado/reference/ado-api/stringformatenum.md)值，指定如何**資料錄集**應該轉換成字串。 *RowDelimiter*， *ColumnDelimiter*，並*NullExpr*參數只會搭配*StringFormat*的**adClipString**。  
  
 *NumRows*  
 選擇性。 中要轉換的資料列數目**資料錄集**。 如果*NumRows*未指定，或如果大於中的資料列總數**資料錄集**，然後所有的資料列中**資料錄集**會轉換。  
  
 *ColumnDelimiter*  
 選擇性。 使用資料行，如果指定，否則為 TAB 字元之間的分隔符號。  
  
 *RowDelimiter*  
 選擇性。 使用資料列，如果指定，否則為歸位字元之間的分隔符號。  
  
 *NullExpr*  
 選擇性。 用來取代 null 的值，如果指定，否則為空字串的運算式。  
  
## <a name="remarks"></a>備註  
 資料列的資料，但不是含結構描述資料，會儲存為字串。 因此，**資料錄集**無法使用此字串重新開啟。  
  
 這個方法相當於 RDO **GetClipString**方法。  
  
## <a name="applies-to"></a>適用於  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [GetString 方法範例 (VB)](../../../ado/reference/ado-api/getstring-method-example-vb.md)
