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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4a872ee5f4af49d9fbe97621a5d2549fd9472202
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67931233"
---
# <a name="resyncenum"></a>ResyncEnum
指定重新[同步](../../../ado/reference/ado-api/resync-method.md)的呼叫是否覆寫基礎值。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adResyncAllValues**|2|預設。 會覆寫資料，並取消暫止的更新。|  
|**adResyncUnderlyingValues**|1|不會覆寫資料，也不會取消暫止的更新。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等  
 Package： **.com. wfc. 資料**  
  
|持續性|  
|--------------|  
|AdoEnums.Resync.ALLVALUES|  
|AdoEnums.Resync.UNDERLYINGVALUES|  
  
## <a name="applies-to"></a>套用至  
 [Resync 方法](../../../ado/reference/ado-api/resync-method.md)
