---
title: PersistFormatEnum |Microsoft Docs
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
ms.openlocfilehash: 2a26fd370e80cb288ee62b0fc53ed6670300172e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67917610"
---
# <a name="persistformatenum"></a>PersistFormatEnum
指定用來儲存[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)的格式。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adPersistADTG**|0|表示 Microsoft Advanced Data TableGram （ADTG）格式。|  
|**adPersistADO**|1|表示將使用 ADO 本身的可延伸標記語言 (XML) （XML）格式。 這個值與 adPersistXML 相同，而且包含在回溯相容性中。|  
|**adPersistXML**|1|表示可延伸標記語言 (XML) （XML）格式。|  
|**adPersistProviderSpecific**|2|指出提供者會使用其本身的格式保存**記錄集**。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等  
 Package： **.com. wfc. 資料**  
  
|持續性|  
|--------------|  
|AdoEnums.PersistFormat.ADTG|  
|AdoEnums.PersistFormat.XML|  
  
## <a name="applies-to"></a>套用至  
 [Save 方法](../../../ado/reference/ado-api/save-method.md)
