---
description: AllowNullsEnum
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
ms.openlocfilehash: 058df53811bfbb48005f1f9c6f08f38410bc54cf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88440500"
---
# <a name="allownullsenum"></a>AllowNullsEnum
指定是否為具有 null 值的記錄編制索引。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adIndexNullsAllow**|0|索引可允許索引鍵資料行為 null 的專案。 如果在索引鍵資料行中輸入 null 值，則會將專案插入到索引中。|  
|**adIndexNullsDisallow**|1|預設值。 索引不允許索引鍵資料行為 null 的專案。 如果在索引鍵資料行中輸入 null 值，則會發生錯誤。|  
|**adIndexNullsIgnore**|2|索引不會插入包含 null 索引鍵的專案。 如果在索引鍵資料行中輸入 null 值，則會忽略該專案，且不會發生任何錯誤。|  
|**adIndexNullsIgnoreAny**|4|索引不會插入某些索引鍵資料行具有 null 值的專案。 針對具有多資料行索引鍵的索引，如果在某個資料行中輸入 null 值，則會忽略該專案，且不會發生任何錯誤。|  
  
## <a name="applies-to"></a>套用至  
 [IndexNulls 屬性 (ADOX)](../../../ado/reference/adox-api/indexnulls-property-adox.md)
