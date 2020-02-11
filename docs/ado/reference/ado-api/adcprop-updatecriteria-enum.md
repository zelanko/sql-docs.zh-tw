---
title: ADCPROP_UPDATECRITERIA_ENUM |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 12d960e8fcd5e1f27ea8198ce52e080f6fddf7c2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67921410"
---
# <a name="adcprop_updatecriteria_enum"></a>ADCPROP_UPDATECRITERIA_ENUM
指定哪些欄位可以在使用[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件的資料來源的開放式更新期間，用來偵測衝突。  
  
 請使用這些常數搭配**記錄集**「**更新準則**」動態屬性，這會在[ADO 動態屬性索引](../../../ado/reference/ado-api/ado-dynamic-property-index.md)中參考，並記載于 OLE DB 檔的[Microsoft 資料指標服務](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)中。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adCriteriaAllCols**|1|如果資料來源資料列的任何資料行已變更，便會偵測衝突。|  
|**adCriteriaKey**|0|如果資料來源資料列的索引鍵資料行已變更，即會偵測到衝突，這表示已刪除該資料列。|  
|**adCriteriaTimeStamp**|3|如果資料來源資料列的時間戳記已變更，即會偵測到衝突，這表示在取得**記錄集**之後，已經存取過該資料列。|  
|**adCriteriaUpdCols**|2|當對應至**記錄集**之更新欄位的資料來源資料行的任何資料行已變更時，會偵測到衝突。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等  
 Package： **.com. wfc. 資料**  
  
|持續性|  
|--------------|  
|AdoEnums.AdcPropUpdateCriteria.ALLCOLS|  
|AdoEnums. AdcPropUpdateCriteria. KEY|  
|AdoEnums. AdcPropUpdateCriteria. TIMESTAMP|  
|AdoEnums.AdcPropUpdateCriteria.UPDCOLS|
