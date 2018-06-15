---
title: StringFormatEnum |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- StringFormatEnum
helpviewer_keywords:
- StringFormatEnum enumeration [ADO]
ms.assetid: 28f7d1ec-092b-4323-a39d-d3f882c6c81a
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ac774393a914c13171dfa13150ee708b316fbd03
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2018
ms.locfileid: "35282587"
---
# <a name="stringformatenum"></a>StringFormatEnum
指定的格式，擷取時[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)做為字串。  
  
|常數|ReplTest1|描述|  
|--------------|-----------|-----------------|  
|**adClipString**|2|用來分隔列 *[rowdelimiter]*，資料行 *[columndelimiter]*，和 null 值*NullExpr*。 這三個參數的[GetString](../../../ado/reference/ado-api/getstring-method-ado.md)方法會有效只能搭配*StringFormat*的**adClipString**。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等項目  
 封裝： **com.ms.wfc.data**  
  
|常數|  
|--------------|  
|AdoEnums.StringFormat.CLIPSTRING|  
  
## <a name="applies-to"></a>適用於  
 [GetString 方法 (ADO)](../../../ado/reference/ado-api/getstring-method-ado.md)
