---
description: State 屬性 (ADO)
title: State 屬性 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command25::State
helpviewer_keywords:
- State property [ADO]
ms.assetid: 0b993bac-2653-40b1-bcbb-5b57b6aae2bf
author: rothja
ms.author: jroth
ms.openlocfilehash: d118ed6d695f8f047640f0ef16c139204ae36277
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988839"
---
# <a name="state-property-ado"></a>State 屬性 (ADO)
指出物件的狀態為開啟或關閉時，所有適用的物件。 如果物件正在執行非同步方法，則表示物件的目前狀態是連接、執行或正在抓取。  
  
## <a name="return-value"></a>傳回值  
 傳回可以是[ObjectStateEnum](./objectstateenum.md)值的**Long**值。 預設值為 **adStateClosed**。  
  
## <a name="remarks"></a>備註  
 您可以使用 **State** 屬性來判斷指定物件的目前狀態。  
  
 物件的 **State** 屬性可以有值的組合。 例如，如果執行語句，這個屬性將會有 **adStateOpen** 和 **adStateExecuting**的組合值。  
  
 **State**屬性是唯讀的。  
  
## <a name="applies-to"></a>套用至  

:::row:::
    :::column:::
        [Command 物件 (ADO)](./command-object-ado.md)  
        [Connection 物件 (ADO)](./connection-object-ado.md)  
    :::column-end:::
    :::column:::
        [Record 物件 (ADO)](./record-object-ado.md)  
        [Recordset 物件 (ADO)](./recordset-object-ado.md)  
    :::column-end:::
    :::column:::
        [Stream 物件 (ADO)](./stream-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>另請參閱  
 [ConnectionString、ConnectionTimeout 和 State 屬性範例 (VB) ](./connectionstring-connectiontimeout-and-state-properties-example-vb.md)   
 [ConnectionString、ConnectionTimeout 和 State 屬性範例 (VC + +) ](./connectionstring-connectiontimeout-and-state-properties-example-vc.md)