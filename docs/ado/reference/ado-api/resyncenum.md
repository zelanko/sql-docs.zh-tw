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
ms.openlocfilehash: addaaa07b14b88ed7d72714ba8698da1f2ef2ac9
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777637"
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