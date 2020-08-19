---
description: SearchDirectionEnum
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
ms.openlocfilehash: 918261998fec061f8f977a8a2dfc614166f564f6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88442160"
---
# <a name="searchdirectionenum"></a>SearchDirectionEnum
指定記錄 [集](../../../ado/reference/ado-api/recordset-object-ado.md)內的記錄搜尋方向。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adSearchBackward**|-1|向後搜尋，在 **記錄集**的開頭停止。 如果找不到相符項，則記錄指標位於 [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)。|  
|**adSearchForward**|1|向前搜尋，在 **記錄集**結束時停止。 如果找不到相符項，記錄指標就會定位於 [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 相等  
 封裝： **.com. 資料**  
  
|常數|  
|--------------|  
|AdoEnums.SearchDirection.BACKWARD|  
|AdoEnums.SearchDirection.FORWARD|  
  
## <a name="applies-to"></a>套用至  
 [Find 方法 (ADO)](../../../ado/reference/ado-api/find-method-ado.md)
