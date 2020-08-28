---
description: AllowNullsEnum
title: AllowNullsEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: c2d21b4a7e4de67e45210f11598a7cf3a2a99b9e
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88985539"
---
# <a name="allownullsenum"></a>AllowNullsEnum
指定是否為具有 null 值的記錄編制索引。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adIndexNullsAllow**|0|索引可允許索引鍵資料行為 null 的專案。 如果在索引鍵資料行中輸入 null 值，則會將專案插入到索引中。|  
|**adIndexNullsDisallow**|1|預設值。 索引不允許索引鍵資料行為 null 的專案。 如果在索引鍵資料行中輸入 null 值，則會發生錯誤。|  
|**adIndexNullsIgnore**|2|索引不會插入包含 null 索引鍵的專案。 如果在索引鍵資料行中輸入 null 值，則會忽略該專案，且不會發生任何錯誤。|  
|**adIndexNullsIgnoreAny**|4|索引不會插入某些索引鍵資料行具有 null 值的專案。 針對具有多資料行索引鍵的索引，如果在某個資料行中輸入 null 值，則會忽略該專案，且不會發生任何錯誤。|  
  
## <a name="applies-to"></a>套用至  
 [IndexNulls 屬性 (ADOX)](./indexnulls-property-adox.md)