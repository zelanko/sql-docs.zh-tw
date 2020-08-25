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
ms.openlocfilehash: 90c6214caa0adc1c11cdc0660b65795624919e51
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777137"
---
# <a name="stringformatenum"></a>StringFormatEnum
指定以字串形式抓取 [記錄集](./recordset-object-ado.md) 時的格式。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adClipString**|2|依 *RowDelimiter*分隔資料列、依 *ColumnDelimiter*分隔資料行，並依 *NullExpr*分隔 null 值。 這三個 [GetString](./getstring-method-ado.md) 方法的參數只適用于 *StringFormat* of **adClipString**。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 相等  
 封裝： **.com. 資料**  
  
|持續性|  
|--------------|  
|AdoEnums.StringFormat.CLIPSTRING|  
  
## <a name="applies-to"></a>套用至  
 [GetString 方法 (ADO)](./getstring-method-ado.md)