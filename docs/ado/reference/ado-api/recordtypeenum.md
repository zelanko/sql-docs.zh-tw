---
title: RecordTypeEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- RecordTypeEnum
helpviewer_keywords:
- RecordTypeEnum enumeration [ADO]
ms.assetid: f557e537-015d-4ba7-8a41-a6f00b366a91
author: rothja
ms.author: jroth
ms.openlocfilehash: 8b47b68b8515ea80405d6083e37a767fb5a6d21e
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82756560"
---
# <a name="recordtypeenum"></a>RecordTypeEnum
指定[記錄](../../../ado/reference/ado-api/record-object-ado.md)物件的類型。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adSimpleRecord**|0|表示*簡單*記錄（不包含子節點）。|  
|**adCollectionRecord**|1|表示*集合*記錄（包含子節點）。|  
|**adRecordUnknown**|-1|表示此**記錄**的類型是未知的。|  
|**adStructDoc**|2|表示代表 COM 結構化檔的一種特殊*集合*記錄。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等  
 這些常數沒有 ADO/WFC 對應項。  
  
## <a name="applies-to"></a>套用至  
 [RecordType 屬性 (ADO)](../../../ado/reference/ado-api/recordtype-property-ado.md)
