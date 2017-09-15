---
title: "ADCPROP_UPDATECRITERIA_ENUM |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- ADCPROP_UPDATECRITERIA_ENUM
helpviewer_keywords:
- ADCPROP_UPDATECRITERIA_ENUM [ADO]
ms.assetid: 33fd7b65-2ec8-4f62-91a7-630b5dab1aa2
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 730a97c27d4aa57632ecf14b0f5cbddffb689d70
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="adcpropupdatecriteriaenum"></a>ADCPROP_UPDATECRITERIA_ENUM
指定哪些欄位可以用來偵測衝突，開放式與資料來源的資料列的更新期間[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件。  
  
 使用這些常數**資料錄集**"**更新條件**"動態屬性，會參考[ADO 動態屬性索引](../../../ado/reference/ado-api/ado-dynamic-property-index.md)而且會記錄在[Microsoft OLE DB 的資料指標服務](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)文件。  
  
|常數|值|Description|  
|--------------|-----------|-----------------|  
|**adCriteriaAllCols**|1|如果已變更資料來源資料列的任何資料行，會偵測衝突。|  
|**adCriteriaKey**|0|偵測到衝突，如果索引鍵的資料行的資料來源的資料列已經變更，這表示已刪除資料列。|  
|**adCriteriaTimeStamp**|3|偵測到衝突，如果時間戳記資料的來源資料列已變更，這表示已存取之資料列之後**資料錄集**取得。|  
|**adCriteriaUpdCols**|2|偵測到衝突，如果任何資料來源的資料行的資料列，對應至已更新欄位**資料錄集**已變更。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等項目  
 封裝： **com.ms.wfc.data**  
  
|常數|  
|--------------|  
|AdoEnums.AdcPropUpdateCriteria.ALLCOLS|  
|AdoEnums.AdcPropUpdateCriteria.KEY|  
|AdoEnums.AdcPropUpdateCriteria.TIMESTAMP|  
|AdoEnums.AdcPropUpdateCriteria.UPDCOLS|
