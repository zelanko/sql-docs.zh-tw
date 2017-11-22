---
title: "狀態屬性 (ADO) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: Command25::State
helpviewer_keywords: State property [ADO]
ms.assetid: 0b993bac-2653-40b1-bcbb-5b57b6aae2bf
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: a261e499afc4a65217fe179c48151f52cb817dff
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="state-property-ado"></a>State 屬性 (ADO)
物件的狀態是否已開啟或關閉表示所有適用的物件。 如果物件執行非同步的方法，指出是否連接、 執行，或擷取物件的目前狀態。  
  
## <a name="return-value"></a>傳回值  
 傳回**長**值，可以是[ObjectStateEnum](../../../ado/reference/ado-api/objectstateenum.md)值。 預設值是**adStateClosed**。  
  
## <a name="remarks"></a>備註  
 您可以使用**狀態**屬性來判斷在任何時間的指定物件的目前狀態。  
  
 物件的**狀態**屬性可以具有值的組合。 例如，如果執行陳述式時，此屬性會有的組合的值**adStateOpen**和**adStateExecuting**。  
  
 **狀態**屬性是唯讀的。  
  
## <a name="applies-to"></a>適用於  
  
||||  
|-|-|-|  
|[Command 物件 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)|[Connection 物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[Record 物件 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|  
|[Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|[Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)||  
  
## <a name="see-also"></a>請參閱＜  
 [ConnectionString、 ConnectionTimeout 和 State 屬性範例 (VB)](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vb.md)   
 [ConnectionString、 ConnectionTimeout 和 State 屬性範例 （VC + +）](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vc.md)   
