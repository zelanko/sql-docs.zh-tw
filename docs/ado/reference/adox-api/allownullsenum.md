---
title: AllowNullsEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- AllowNullsEnum
helpviewer_keywords:
- AllowNullsEnum enumeration [ADOX]
ms.assetid: 6acf3689-1a7f-4379-9d7f-df452ccbac27
author: rothja
ms.author: jroth
ms.openlocfilehash: 74bb82433d17bd47df71d3a9f8574d72ce39a265
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764079"
---
# <a name="allownullsenum"></a>AllowNullsEnum
指定是否要為具有 null 值的記錄編制索引。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adIndexNullsAllow**|0|索引會允許索引鍵資料行為 null 的專案。 如果在索引鍵資料行中輸入 null 值，則會將專案插入至索引中。|  
|**adIndexNullsDisallow**|1|預設值。 索引不允許索引鍵資料行為 null 的專案。 如果在索引鍵資料行中輸入 null 值，就會發生錯誤。|  
|**adIndexNullsIgnore**|2|索引不會插入包含 null 索引鍵的專案。 如果在索引鍵資料行中輸入 null 值，則會忽略該專案，而且不會發生任何錯誤。|  
|**adIndexNullsIgnoreAny**|4|索引不會插入具有 null 值的專案。 針對具有多重資料行索引鍵的索引，如果在某些資料行中輸入 null 值，則會忽略該專案，且不會發生錯誤。|  
  
## <a name="applies-to"></a>套用至  
 [IndexNulls 屬性 (ADOX)](../../../ado/reference/adox-api/indexnulls-property-adox.md)
