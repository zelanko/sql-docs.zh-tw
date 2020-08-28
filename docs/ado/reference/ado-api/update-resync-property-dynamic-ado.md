---
description: 更新重新同步動態屬性 (ADO)
title: 更新重新同步屬性-動態 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 506fd7fecee179a055e23ffad1beab76bcd2fbe2
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988089"
---
# <a name="update-resync-property-dynamic-ado"></a>更新重新同步動態屬性 (ADO)
指定 [UpdateBatch](./updatebatch-method.md) 方法後面是否接著隱含的 [Resync](./resync-method.md) 方法作業，如果是，則為該作業的範圍。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回一或多個 [ADCPROP_UPDATERESYNC_ENUM](./adcprop-updateresync-enum.md) 值。  
  
## <a name="remarks"></a>備註  
 可能會結合 ADCPROP_UPDATERESYNC_ENUM 的值，但 adResyncAll 已代表其餘值的組合。  
  
 常數 **adResyncConflicts** 會將重新同步值儲存為基礎值，但不會覆寫暫止的變更。  
  
 當[CursorLocation](./cursorlocation-property-ado.md)屬性設定為**AdUseClient**時，**更新重新同步**是附加到[記錄集](./recordset-object-ado.md)物件[屬性](./properties-collection-ado.md)集合的動態屬性。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](./recordset-object-ado.md)