---
description: 更新重新同步動態屬性 (ADO)
title: 更新重新同步屬性-動態 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Update Resync property [ADO]
ms.assetid: 8a3bb608-66d7-4128-a3ef-84cb0556de0d
author: rothja
ms.author: jroth
ms.openlocfilehash: 43657b3dddcf53f9aa9df507c646b7f23088f0ef
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88441630"
---
# <a name="update-resync-property-dynamic-ado"></a>更新重新同步動態屬性 (ADO)
指定 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) 方法後面是否接著隱含的 [Resync](../../../ado/reference/ado-api/resync-method.md) 方法作業，如果是，則為該作業的範圍。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回一或多個 [ADCPROP_UPDATERESYNC_ENUM](../../../ado/reference/ado-api/adcprop-updateresync-enum.md) 值。  
  
## <a name="remarks"></a>備註  
 可能會結合 ADCPROP_UPDATERESYNC_ENUM 的值，但 adResyncAll 已代表其餘值的組合。  
  
 常數 **adResyncConflicts** 會將重新同步值儲存為基礎值，但不會覆寫暫止的變更。  
  
 當[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性設定為**AdUseClient**時，**更新重新同步**是附加到[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合的動態屬性。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
