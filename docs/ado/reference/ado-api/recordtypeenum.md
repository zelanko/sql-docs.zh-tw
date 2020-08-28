---
description: RecordTypeEnum
title: RecordTypeEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: ded4106b770ff62edd4b79401885ee5ce3101798
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88989659"
---
# <a name="recordtypeenum"></a>RecordTypeEnum
指定 [記錄](./record-object-ado.md) 物件的類型。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adSimpleRecord**|0|指出 (不包含子節點) 的 *簡單* 記錄。|  
|**adCollectionRecord**|1|指出)  (包含子節點的 *集合* 記錄。|  
|**adRecordUnknown**|-1|指出此 **記錄** 的類型未知。|  
|**adStructDoc**|2|表示一種特殊類型的 *集合* 記錄，表示 COM 結構化檔。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 相等  
 這些常數沒有 ADO/WFC 對等專案。  
  
## <a name="applies-to"></a>套用至  
 [RecordType 屬性 (ADO)](./recordtype-property-ado.md)