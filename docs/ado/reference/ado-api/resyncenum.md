---
title: ResyncEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ResyncEnum
helpviewer_keywords:
- ResyncEnum enumeration [ADO]
ms.assetid: d3df2c90-e570-4c40-a79a-25b3448a009c
author: rothja
ms.author: jroth
ms.openlocfilehash: a53d2c64e961c1b46b2d170de712493cc06f3910
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82756232"
---
# <a name="resyncenum"></a>ResyncEnum
指定重新[同步](../../../ado/reference/ado-api/resync-method.md)的呼叫是否覆寫基礎值。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adResyncAllValues**|2|預設值。 會覆寫資料，並取消暫止的更新。|  
|**adResyncUnderlyingValues**|1|不會覆寫資料，也不會取消暫止的更新。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等  
 Package： **.com. wfc. 資料**  
  
|持續性|  
|--------------|  
|AdoEnums.Resync.ALLVALUES|  
|AdoEnums.Resync.UNDERLYINGVALUES|  
  
## <a name="applies-to"></a>套用至  
 [Resync 方法](../../../ado/reference/ado-api/resync-method.md)
