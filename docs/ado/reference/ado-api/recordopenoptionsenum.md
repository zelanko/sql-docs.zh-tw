---
title: RecordOpenOptionsEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- RecordOpenOptionsEnum
helpviewer_keywords:
- RecordOpenOptionsEnum enumeration [ADO]
ms.assetid: 9028aba4-90fc-4dfc-88e4-fa8a7b6fedee
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ab648d7fe60a27d36e55cd3d859d0a8c442eef50
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63240339"
---
# <a name="recordopenoptionsenum"></a>RecordOpenOptionsEnum
指定選項，開啟[記錄](../../../ado/reference/ado-api/record-object-ado.md)。 這些值可能會合併使用或者。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adDelayFetchFields**|0x8000|表示欄位相關聯的提供者**記錄**需要一開始，擷取，但可以擷取在第一次嘗試存取該欄位。 預設行為，不存在，此旗標，指出是要擷取所有**記錄**物件欄位。|  
|**adDelayFetchStream**|0x4000|表示預設資料流相關聯的提供者**記錄**需要一開始擷取。 預設行為，不存在，此旗標，指出是要擷取相關聯的預設資料流**記錄**物件。|  
|**adOpenAsync**|0x1000|指出**記錄**物件以非同步的模式開啟。|  
|**adOpenExecuteCommand**|0x10000|表示來源字串包含應該執行的命令文字。 此值相當於**adCmdText**選項**Recordset.Open**。|  
|**adOpenRecordUnspecified**|-1|預設值。 表示未指定任何選項。|  
|**adOpenOutput**|0x800000|表示如果來源會指向包含可執行的指令碼的節點 (例如。ASP 網頁上），然後開啟**記錄**會包含執行的指令碼的結果。 此值只適用於非集合記錄。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等項目  
 這些常數不需要 ADO/WFC 對等項目。  
  
## <a name="applies-to"></a>適用於  
 [Open 方法 (ADO Record)](../../../ado/reference/ado-api/open-method-ado-record.md)
