---
title: 更新重新同步動態屬性 (ADO) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ed0e3ad8027c31a351ddb4506d3b420aa3a1124d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67938801"
---
# <a name="update-resync-property-dynamic-ado"></a>更新重新同步動態屬性 (ADO)
指定是否[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)方法後面隱含[重新同步處理](../../../ado/reference/ado-api/resync-method.md)方法作業，如果是，該作業的範圍。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回一或多個[ADCPROP_UPDATERESYNC_ENUM](../../../ado/reference/ado-api/adcprop-updateresync-enum.md)值。  
  
## <a name="remarks"></a>備註  
 除了 adResyncAll 已經代表其餘的值的組合，可能會結合 ADCPROP_UPDATERESYNC_ENUM 的值。  
  
 常數**adResyncConflicts**儲存的重新同步處理值為基礎的值，但不會覆寫暫止的變更。  
  
 **更新重新同步處理**動態屬性附加至[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)物件[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合時[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性設定為**adUseClient**。  
  
## <a name="applies-to"></a>適用於  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
