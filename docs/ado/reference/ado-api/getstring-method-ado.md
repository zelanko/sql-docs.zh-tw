---
description: GetString 方法 (ADO)
title: " (ADO) 的 GetString 方法 |Microsoft Docs"
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
author: rothja
ms.author: jroth
ms.openlocfilehash: ef3d32e1caae337ecb2a03bba6af8c7b4cd858de
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443510"
---
# <a name="getstring-method-ado"></a>GetString 方法 (ADO)
以字串形式傳回 [記錄集](../../../ado/reference/ado-api/recordset-object-ado.md) 。  
  
## <a name="syntax"></a>語法  
  
```  
  
Variant = recordset.GetString(StringFormat, NumRows, ColumnDelimiter, RowDelimiter, NullExpr)  
```  
  
## <a name="return-value"></a>傳回值  
 以字串值**變數**形式傳回 (BSTR) 的**記錄集**。  
  
#### <a name="parameters"></a>參數  
 *StringFormat*  
 [StringFormatEnum](../../../ado/reference/ado-api/stringformatenum.md)值，指定如何將**記錄集**轉換成字串。 *RowDelimiter*、 *ColumnDelimiter*和*NullExpr*參數只適用于*StringFormat* **adClipString**。  
  
 *NumRows*  
 選擇性。 要在 **記錄集中**轉換的資料列數目。 如果未指定 *NumRows* ，或它大於 **記錄集中**的資料列總數，則會轉換 **記錄集** 內的所有資料列。  
  
 *ColumnDelimiter*  
 選擇性。 如果有指定，則在資料行之間使用分隔符號，否則為定位字元。  
  
 *RowDelimiter*  
 選擇性。 如果有指定，則為數據列之間使用的分隔符號，否則為換行字元。  
  
 *NullExpr*  
 選擇性。 用來取代 null 值的運算式（如有指定），否則為空字串。  
  
## <a name="remarks"></a>備註  
 資料列資料（但不含架構資料）會儲存至字串。 因此，無法使用此字串重新開啟 **記錄集** 。  
  
 這個方法相當於 RDO **GetClipString** 方法。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [GetString 方法範例 (VB)](../../../ado/reference/ado-api/getstring-method-example-vb.md)
