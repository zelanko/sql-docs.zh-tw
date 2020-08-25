---
description: CommandTimeout 屬性 (ADO)
title: " (ADO) 的 CommandTimeout 屬性 |Microsoft Docs"
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
ms.openlocfilehash: eaa3f7aace505092b147fc3d15c2890de50c5958
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88776107"
---
# <a name="commandtimeout-property-ado"></a>CommandTimeout 屬性 (ADO)
表示在終止嘗試並產生錯誤之前，執行命令所要等候的時間長度。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回 **long** 值，指出等候命令執行的時間（以秒為單位）。 預設值為 30。  
  
## <a name="remarks"></a>備註  
 使用[連接](./connection-object-ado.md)物件或[命令](./command-object-ado.md)物件上的**CommandTimeout**屬性，以允許取消[執行](./execute-method-ado-command.md)方法呼叫，因為網路流量或伺服器使用繁重的延遲。 如果在 **CommandTimeout** 屬性中設定的間隔在命令完成執行之前已經過，則會發生錯誤，且 ADO 會取消命令。 如果您將屬性設定為零，則 ADO 會無限期等候，直到執行完成為止。 請確定您撰寫程式碼的提供者和資料來源支援 **CommandTimeout** 功能。  
  
 **連接**物件上的**CommandTimeout**設定不會影響相同**連接**上**命令**物件上的**CommandTimeout**設定;也就是說， **Command**物件的**CommandTimeout**屬性不會繼承**連接**物件之**CommandTimeout**值的值。  
  
 在 **連接** 物件上， **CommandTimeout** 屬性會在開啟 **連接** 之後維持讀取/寫入狀態。  
  
## <a name="applies-to"></a>套用至  

:::row:::
    :::column:::
        [Command 物件 (ADO)](./command-object-ado.md)  
    :::column-end:::
    :::column:::
        [Connection 物件 (ADO)](./connection-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>另請參閱  
 [ActiveConnection、CommandText、CommandTimeout、CommandType、Size 和 Direction 屬性範例 (VB) ](./activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection、CommandText、CommandTimeout、CommandType、Size 和 Direction 屬性範例 (VC + +) ](./activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection、CommandText、CommandTimeout、CommandType、Size 和 Direction 屬性範例 (JScript) ](./activeconnection-commandtext-timeout-type-size-example-jscript.md)   
 [ConnectionTimeout 屬性 (ADO)](./connectiontimeout-property-ado.md)