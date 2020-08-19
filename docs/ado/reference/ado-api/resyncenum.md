---
description: ResyncEnum
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
ms.openlocfilehash: c379ca2a3f68b195c0020d0e89009d2715da5850
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88442250"
---
# <a name="resyncenum"></a>ResyncEnum
指定重新 [同步](../../../ado/reference/ado-api/resync-method.md)的呼叫是否覆寫基礎值。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adResyncAllValues**|2|預設值。 覆寫資料，並取消暫止的更新。|  
|**adResyncUnderlyingValues**|1|不會覆寫資料，而且不會取消暫止的更新。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 相等  
 封裝： **.com. 資料**  
  
|常數|  
|--------------|  
|AdoEnums.Resync.ALLVALUES|  
|AdoEnums.Resync.UNDERLYINGVALUES|  
  
## <a name="applies-to"></a>套用至  
 [Resync 方法](../../../ado/reference/ado-api/resync-method.md)
