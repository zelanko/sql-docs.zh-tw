---
title: "PersistFormatEnum |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: PersistFormatEnum
helpviewer_keywords: PersistFormatEnum enumeration [ADO]
ms.assetid: ebe1a2ab-e9f1-43a2-8f94-b190c9613d70
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2695db14fdbdf05aba5b0a1b14b063ff6672a928
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="persistformatenum"></a>PersistFormatEnum
指定用來儲存格式[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)。  
  
|常數|值|Description|  
|--------------|-----------|-----------------|  
|**adPersistADTG**|0|表示 Microsoft 進階資料 TableGram (ADTG) 格式。|  
|**adPersistADO**|1|表示將會使用 ADO 自己可延伸標記語言 (XML) 格式。 這個值是 adPersistXML 相同，而且是為了回溯相容性。|  
|**adPersistXML**|1|表示可延伸標記語言 (XML) 格式。|  
|**adPersistProviderSpecific**|2|表示提供者將保存**資料錄集**使用自己的格式。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等項目  
 封裝： **com.ms.wfc.data**  
  
|常數|  
|--------------|  
|AdoEnums.PersistFormat.ADTG|  
|AdoEnums.PersistFormat.XML|  
  
## <a name="applies-to"></a>適用於  
 [Save 方法](../../../ado/reference/ado-api/save-method.md)
