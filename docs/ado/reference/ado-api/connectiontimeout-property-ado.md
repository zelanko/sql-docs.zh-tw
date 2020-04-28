---
title: ConnectionTimeout 屬性（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::ConnectionTimeout
helpviewer_keywords:
- ConnectionTimeout property [ADO]
ms.assetid: 8904a403-1383-4b4b-b53d-5c01d6f5deac
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 03d3de2c4aabaf4ad8cbc45d9900b33883ff9a48
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67933469"
---
# <a name="connectiontimeout-property-ado"></a>ConnectionTimeout 屬性 (ADO)
表示在終止嘗試並產生錯誤之前，建立連接之前要等候的時間長度。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**long**值，指出等候連接開啟的時間（以秒為單位）。 預設值為 15。  
  
## <a name="remarks"></a>備註  
 如果網路流量或大量伺服器使用延遲，使其必須放棄連接嘗試，請在[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件上使用**ConnectionTimeout**屬性。 如果**ConnectionTimeout**屬性設定的時間在開啟連接之前就已過期，則會發生錯誤，而且 ADO 會取消嘗試。 如果您將屬性設定為零，ADO 會無限期等待，直到開啟連接為止。 請確定您撰寫程式碼的提供者支援**ConnectionTimeout**功能。  
  
 當連接關閉時， **ConnectionTimeout**屬性是讀取/寫入，而在開啟時則為唯讀。  
  
## <a name="applies-to"></a>套用至  
 [Connection 物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [ConnectionString、ConnectionTimeout 和 State 屬性範例（VB）](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vb.md)   
 [ConnectionString、ConnectionTimeout 和 State 屬性範例（VC + +）](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vc.md)   
 [CommandTimeout 屬性 (ADO)](../../../ado/reference/ado-api/commandtimeout-property-ado.md)
