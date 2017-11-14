---
title: "GetString 方法 (ADO) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset20::raw_GetString
- Recordset20::GetString
helpviewer_keywords:
- GetString method [ADO]
ms.assetid: 92452940-b2a7-456e-94fc-3780c71da33c
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d146c1cdd2ebb4f069afef7163ce998cbb149ef6
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="getstring-method-ado"></a>GetString 方法 (ADO)
傳回[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)做為字串。  
  
## <a name="syntax"></a>語法  
  
```  
  
Variant = recordset.GetString(StringFormat, NumRows, ColumnDelimiter, RowDelimiter, NullExpr)  
```  
  
## <a name="return-value"></a>傳回值  
 傳回**資料錄集**做為字串值**Variant** (BSTR)。  
  
#### <a name="parameters"></a>參數  
 *StringFormat*  
 A [StringFormatEnum](../../../ado/reference/ado-api/stringformatenum.md)值，指定如何**資料錄集**應該轉換成字串。 *[Rowdelimiter]*， *[columndelimiter]*，和*NullExpr*參數只會搭配*StringFormat*的**adClipString**。  
  
 *NumRows*  
 選擇性。 轉換中的資料列數目**資料錄集**。 如果*NumRows*未指定，或如果大於中的資料列總數**資料錄集**，然後所有資料列**資料錄集**會轉換。  
  
 *[Columndelimiter]*  
 選擇性。 使用資料行，如果指定，否則為 TAB 字元之間的分隔符號。  
  
 *[Rowdelimiter]*  
 選擇性。 使用資料列，如果指定，否則的歸位字元之間的分隔符號。  
  
 *NullExpr*  
 選擇性。 用來取代 null 值，如果指定，否則為空字串的運算式。  
  
## <a name="remarks"></a>備註  
 資料列資料，但是沒有結構描述資料，會儲存為字串。 因此，**資料錄集**無法使用此字串重新開啟。  
  
 這個方法相當於 RDO **GetClipString**方法。  
  
## <a name="applies-to"></a>適用於  
 [資料錄集物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [GetString 方法範例 (VB)](../../../ado/reference/ado-api/getstring-method-example-vb.md)

