---
description: ResyncEnum
title: ResyncEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 0c98c0b0bae307f57e5a77c7ca4ac6b473f4d149
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88989459"
---
# <a name="resyncenum"></a>ResyncEnum
指定重新 [同步](./resync-method.md)的呼叫是否覆寫基礎值。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adResyncAllValues**|2|預設值。 覆寫資料，並取消暫止的更新。|  
|**adResyncUnderlyingValues**|1|不會覆寫資料，而且不會取消暫止的更新。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 相等  
 封裝： **.com. 資料**  
  
|持續性|  
|--------------|  
|AdoEnums.Resync.ALLVALUES|  
|AdoEnums.Resync.UNDERLYINGVALUES|  
  
## <a name="applies-to"></a>套用至  
 [Resync 方法](./resync-method.md)