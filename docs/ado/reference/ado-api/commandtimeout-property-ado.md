---
title: "CommandTimeout 屬性 (ADO) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Command15::CommandTimeout
helpviewer_keywords:
- CommandTimeout property [ADO]
ms.assetid: c611f857-d6b0-4dca-8925-f4a02e769eb0
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: a7848d7fb51a01c35f8a8699b89ea132da36396b
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="commandtimeout-property-ado"></a>CommandTimeout 屬性 (ADO)
表示在終止嘗試並產生錯誤之前，執行命令時要等待的時間。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**長**會表示，以秒為單位，等候執行命令的值。 預設值是 30。  
  
## <a name="remarks"></a>備註  
 使用**CommandTimeout**屬性[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件或[命令](../../../ado/reference/ado-api/command-object-ado.md)物件以允許取消[Execute](../../../ado/reference/ado-api/execute-method-ado-command.md)方法呼叫，因為從網路流量或大量使用伺服器的延遲。 如果設定的間隔時間**CommandTimeout**屬性經過之前命令完成執行時，發生錯誤時，ADO 取消命令。 如果您將屬性設為零，ADO 會等候無限期地執行直到完成為止。 請確定您撰寫程式碼支援的提供者和資料來源**CommandTimeout**功能。  
  
 **CommandTimeout**上設定**連接**物件沒有任何作用**CommandTimeout**上設定**命令**物件上相同**連接**; 也就是**命令**物件的**CommandTimeout**屬性不是繼承的值**連接**物件的**CommandTimeout**值。  
  
 在**連接**物件**CommandTimeout**屬性會維持為讀取/寫入之後**連接**開啟。  
  
## <a name="applies-to"></a>適用於  
  
|||  
|-|-|  
|[Command 物件 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)|[Connection 物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ActiveConnection、 CommandText、 CommandTimeout、 CommandType、 大小和方向屬性範例 (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection、 CommandText、 CommandTimeout、 CommandType、 大小和方向屬性範例 （VC + +）](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection、 CommandText、 CommandTimeout、 CommandType、 大小和方向屬性範例 (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)   
 [ConnectionTimeout 屬性 (ADO)](../../../ado/reference/ado-api/connectiontimeout-property-ado.md)
