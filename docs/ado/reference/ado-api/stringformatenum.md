---
description: StringFormatEnum
title: StringFormatEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 7fe580d45d20c65c313cd87b3fb47ef63bb349ca
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988419"
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