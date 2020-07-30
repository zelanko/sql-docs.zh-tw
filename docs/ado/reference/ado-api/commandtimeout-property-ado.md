---
title: CommandTimeout 屬性（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::CommandTimeout
helpviewer_keywords:
- CommandTimeout property [ADO]
ms.assetid: c611f857-d6b0-4dca-8925-f4a02e769eb0
author: rothja
ms.author: jroth
ms.openlocfilehash: 0b708b2b79c22240468811732d2ffae0955ea204
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87242778"
---
# <a name="commandtimeout-property-ado"></a>CommandTimeout 屬性 (ADO)
表示在終止嘗試並產生錯誤之前，執行命令時要等候的時間長度。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**long**值，指出等候命令執行多久的時間（以秒為單位）。 預設為 30。  
  
## <a name="remarks"></a>備註  
 請在[Connection](../../../ado/reference/ado-api/connection-object-ado.md)物件或[Command](../../../ado/reference/ado-api/command-object-ado.md)物件上使用**CommandTimeout**屬性，以允許取消[執行](../../../ado/reference/ado-api/execute-method-ado-command.md)方法呼叫，因為網路流量或伺服器使用繁重的延遲。 如果在**CommandTimeout**屬性中設定的間隔在命令完成執行之前已過期，則會發生錯誤，而且 ADO 會取消命令。 如果您將屬性設定為零，ADO 會無限期地等候，直到執行完成為止。 請確定您撰寫程式碼的提供者和資料來源支援**CommandTimeout**功能。  
  
 **連接**物件上的**CommandTimeout**設定不會影響相同**連接**上**命令**物件上的**CommandTimeout**設定;也就是說， **Command**物件的**CommandTimeout**屬性不會繼承**Connection**物件之**CommandTimeout**值的值。  
  
 在**連接**物件上， **CommandTimeout**屬性會在開啟**連接**之後維持讀取/寫入。  
  
## <a name="applies-to"></a>套用至  

:::row:::
    :::column:::
        [Command 物件 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
    :::column-end:::
    :::column:::
        [Connection 物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>另請參閱  
 [ActiveConnection、CommandText、CommandTimeout、CommandType、Size 和 Direction 屬性範例（VB）](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection、CommandText、CommandTimeout、CommandType、Size 和 Direction 屬性範例（VC + +）](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection、CommandText、CommandTimeout、CommandType、Size 和 Direction 屬性範例（JScript）](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)   
 [ConnectionTimeout 屬性 (ADO)](../../../ado/reference/ado-api/connectiontimeout-property-ado.md)
