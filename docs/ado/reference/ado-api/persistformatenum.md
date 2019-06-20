---
title: PersistFormatEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- PersistFormatEnum
helpviewer_keywords:
- PersistFormatEnum enumeration [ADO]
ms.assetid: ebe1a2ab-e9f1-43a2-8f94-b190c9613d70
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 7167067d0dc5942bc898c4cc2f01cad2a44ec559
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66703481"
---
# <a name="persistformatenum"></a>PersistFormatEnum
指定要儲存的格式[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adPersistADTG**|0|表示 Microsoft 進階資料 TableGram (ADTG) 格式。|  
|**adPersistADO**|1|表示將會使用 ADO 自己可延伸標記語言 (XML) 格式。 這個值是 adPersistXML 相同，而且是適用於處理回溯相容性。|  
|**adPersistXML**|1|指出可延伸標記語言 (XML) 格式。|  
|**adPersistProviderSpecific**|2|表示提供者會保存**資料錄集**使用自己的格式。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等項目  
 封裝： **com.ms.wfc.data**  
  
|常數|  
|--------------|  
|AdoEnums.PersistFormat.ADTG|  
|AdoEnums.PersistFormat.XML|  
  
## <a name="applies-to"></a>適用於  
 [Save 方法](../../../ado/reference/ado-api/save-method.md)
