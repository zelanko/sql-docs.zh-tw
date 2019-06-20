---
title: StringFormatEnum | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 7225f8a7612f08947720eb2912722dc92b7a2a96
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66710803"
---
# <a name="stringformatenum"></a>StringFormatEnum
擷取時指定的格式[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)做為字串。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adClipString**|2|依資料列會分隔*RowDelimiter*，資料行*ColumnDelimiter*，和 null 值*NullExpr*。 這三個參數的[GetString](../../../ado/reference/ado-api/getstring-method-ado.md)方法會只使用有效*StringFormat*的**adClipString**。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等項目  
 封裝： **com.ms.wfc.data**  
  
|常數|  
|--------------|  
|AdoEnums.StringFormat.CLIPSTRING|  
  
## <a name="applies-to"></a>適用於  
 [GetString 方法 (ADO)](../../../ado/reference/ado-api/getstring-method-ado.md)
