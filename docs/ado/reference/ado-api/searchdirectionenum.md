---
title: SearchDirectionEnum |Microsoft 文件
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
- SearchDirectionEnum
helpviewer_keywords:
- SearchDirectionEnum enumeration [ADO]
ms.assetid: 81272ae3-2165-4f4e-adfe-9ede0368cb17
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4f6cba75e0e4a2bf164c36f65c9e5fe58d81b1e4
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2018
ms.locfileid: "35281567"
---
# <a name="searchdirectionenum"></a>SearchDirectionEnum
指定的記錄搜尋方向[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)。  
  
|常數|ReplTest1|描述|  
|--------------|-----------|-----------------|  
|**adSearchBackward**|-1|搜尋是反向的停止開頭**資料錄集**。 如果找不到相符項目，位於記錄指標[BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)。|  
|**adSearchForward**|@shouldalert|搜尋轉寄，結尾處停止**資料錄集**。 如果找不到相符項目，位於記錄指標[EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等項目  
 封裝： **com.ms.wfc.data**  
  
|常數|  
|--------------|  
|AdoEnums.SearchDirection.BACKWARD|  
|AdoEnums.SearchDirection.FORWARD|  
  
## <a name="applies-to"></a>適用於  
 [Find 方法 (ADO)](../../../ado/reference/ado-api/find-method-ado.md)
