---
title: ConnectionTimeout 屬性 (ADO) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: b5cb3e6e1cc4266551bfeabf09bde1a65fea032f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63140264"
---
# <a name="connectiontimeout-property-ado"></a>ConnectionTimeout 屬性 (ADO)
表示要在終止嘗試並產生錯誤前建立連接時的等候的時間。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**長**表示，以秒為單位，時間等待連接開啟的值。 預設值為 15。  
  
## <a name="remarks"></a>備註  
 使用  **ConnectionTimeout**屬性上的[連線](../../../ado/reference/ado-api/connection-object-ado.md)物件如果從網路流量或大量使用伺服器的延遲使得不必放棄嘗試連線。 如果從時間**ConnectionTimeout**設定的屬性經過之前開啟連接，則會發生錯誤和 ADO 取消嘗試。 如果您將屬性設為零，ADO 會等到無限期地開啟連接。 請確定您撰寫程式碼的提供者支援**ConnectionTimeout**功能。  
  
 **ConnectionTimeout**屬性是讀取/寫入，當連接已關閉，且為唯讀狀態開啟時。  
  
## <a name="applies-to"></a>適用於  
 [Connection 物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [ConnectionString、 ConnectionTimeout 和 State 屬性範例 (VB)](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vb.md)   
 [ConnectionString、 ConnectionTimeout 和狀態的屬性範例 （VC + +）](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vc.md)   
 [CommandTimeout 屬性 (ADO)](../../../ado/reference/ado-api/commandtimeout-property-ado.md)
