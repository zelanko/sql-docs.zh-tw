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
ms.openlocfilehash: 13f8e73bc382493084c8d3712d4b7bda2ed35c13
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777527"
---
# <a name="searchdirectionenum"></a>SearchDirectionEnum
指定記錄 [集](./recordset-object-ado.md)內的記錄搜尋方向。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adSearchBackward**|-1|向後搜尋，在 **記錄集**的開頭停止。 如果找不到相符項，則記錄指標位於 [BOF](./bof-eof-properties-ado.md)。|  
|**adSearchForward**|1|向前搜尋，在 **記錄集**結束時停止。 如果找不到相符項，記錄指標就會定位於 [EOF](./bof-eof-properties-ado.md)。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 相等  
 封裝： **.com. 資料**  
  
|持續性|  
|--------------|  
|AdoEnums.SearchDirection.BACKWARD|  
|AdoEnums.SearchDirection.FORWARD|  
  
## <a name="applies-to"></a>套用至  
 [Find 方法 (ADO)](./find-method-ado.md)