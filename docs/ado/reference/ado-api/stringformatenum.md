---
description: StringFormatEnum
title: StringFormatEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- StringFormatEnum
helpviewer_keywords:
- StringFormatEnum enumeration [ADO]
ms.assetid: 28f7d1ec-092b-4323-a39d-d3f882c6c81a
author: rothja
ms.author: jroth
ms.openlocfilehash: d7831d7be2df28d31c88216e67e16efbf611b858
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88441780"
---
# <a name="stringformatenum"></a>StringFormatEnum
指定以字串形式抓取 [記錄集](../../../ado/reference/ado-api/recordset-object-ado.md) 時的格式。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adClipString**|2|依 *RowDelimiter*分隔資料列、依 *ColumnDelimiter*分隔資料行，並依 *NullExpr*分隔 null 值。 這三個 [GetString](../../../ado/reference/ado-api/getstring-method-ado.md) 方法的參數只適用于 *StringFormat* of **adClipString**。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 相等  
 封裝： **.com. 資料**  
  
|常數|  
|--------------|  
|AdoEnums.StringFormat.CLIPSTRING|  
  
## <a name="applies-to"></a>套用至  
 [GetString 方法 (ADO)](../../../ado/reference/ado-api/getstring-method-ado.md)
