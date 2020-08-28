---
description: ADCPROP_UPDATECRITERIA_ENUM
title: ADCPROP_UPDATECRITERIA_ENUM |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADCPROP_UPDATECRITERIA_ENUM
helpviewer_keywords:
- ADCPROP_UPDATECRITERIA_ENUM [ADO]
ms.assetid: 33fd7b65-2ec8-4f62-91a7-630b5dab1aa2
author: rothja
ms.author: jroth
ms.openlocfilehash: 3711266f3658fe2366caa56c6afba07d6b63c4c9
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88976809"
---
# <a name="adcprop_updatecriteria_enum"></a>ADCPROP_UPDATECRITERIA_ENUM
指定哪些欄位可以用來偵測資料來源之資料列的開放式更新與 [記錄集](./recordset-object-ado.md) 物件之間的衝突。  
  
 將這些常數與 **記錄集** 「**更新準則**」動態屬性搭配使用，這會在 [ADO 動態屬性索引](./ado-dynamic-property-index.md) 中參考，並記載于 OLE DB 檔的 [Microsoft 資料指標服務](../../guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) 中。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adCriteriaAllCols**|1|如果資料來源資料列的任何資料行已變更，則會偵測到衝突。|  
|**adCriteriaKey**|0|如果資料來源資料列的索引鍵資料行已變更，表示資料列已被刪除，則會偵測到衝突。|  
|**adCriteriaTimeStamp**|3|如果資料來源資料列的時間戳記已變更，表示資料列已在取得 **記錄集** 之後存取，就會偵測到衝突。|  
|**adCriteriaUpdCols**|2|如果資料來源資料列的任何資料行對應到 **記錄集** 的更新欄位，則會偵測衝突。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 相等  
 封裝： **.com. 資料**  
  
|持續性|  
|--------------|  
|AdoEnums.AdcPropUpdateCriteria.ALLCOLS|  
|AdoEnums. AdcPropUpdateCriteria 金鑰|  
|AdoEnums. AdcPropUpdateCriteria. TIMESTAMP|  
|AdoEnums.AdcPropUpdateCriteria.UPDCOLS|