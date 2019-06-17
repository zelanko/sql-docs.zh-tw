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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: a5c1c3869b144bb770ca893595986288b07aa596
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66711451"
---
# <a name="searchdirectionenum"></a>SearchDirectionEnum
指定的記錄搜尋中的方向[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adSearchBackward**|-1|搜尋回溯，停止在開頭**資料錄集**。 如果找不到相符項目，位於記錄指標[BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)。|  
|**adSearchForward**|1|搜尋轉送，停止在結尾**資料錄集**。 如果找不到相符項目，位於記錄指標[EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等項目  
 封裝： **com.ms.wfc.data**  
  
|常數|  
|--------------|  
|AdoEnums.SearchDirection.BACKWARD|  
|AdoEnums.SearchDirection.FORWARD|  
  
## <a name="applies-to"></a>適用於  
 [Find 方法 (ADO)](../../../ado/reference/ado-api/find-method-ado.md)
