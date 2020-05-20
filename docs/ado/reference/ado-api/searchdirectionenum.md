---
title: SearchDirectionEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- SearchDirectionEnum
helpviewer_keywords:
- SearchDirectionEnum enumeration [ADO]
ms.assetid: 81272ae3-2165-4f4e-adfe-9ede0368cb17
author: rothja
ms.author: jroth
ms.openlocfilehash: 7e2928f1817b994c3101182677b5b2fcad9a4b1d
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82755779"
---
# <a name="searchdirectionenum"></a>SearchDirectionEnum
在[記錄集中](../../../ado/reference/ado-api/recordset-object-ado.md)指定記錄搜尋的方向。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adSearchBackward**|-1|向後搜尋，在**記錄集**的開頭處停止。 如果找不到相符的結果，則記錄指標會定位在[BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)。|  
|**adSearchForward**|1|向前搜尋，在**記錄集**結束時停止。 如果找不到相符的結果，則記錄指標會定位於[EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等  
 Package： **.com. wfc. 資料**  
  
|持續性|  
|--------------|  
|AdoEnums.SearchDirection.BACKWARD|  
|AdoEnums.SearchDirection.FORWARD|  
  
## <a name="applies-to"></a>套用至  
 [Find 方法 (ADO)](../../../ado/reference/ado-api/find-method-ado.md)
