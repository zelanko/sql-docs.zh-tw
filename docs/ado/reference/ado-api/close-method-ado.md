---
title: Close 方法（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::Close
- _Stream::Close
- _Record::Close
helpviewer_keywords:
- Close method [ADO]
ms.assetid: 3cdf27d1-a180-4cff-8e42-95dec5fb1b55
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8a1d153d1433a377bb488366111b75a986365132
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67919937"
---
# <a name="close-method-ado"></a>Close 方法 (ADO)
關閉開啟的物件和任何相依物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.Close  
```  
  
## <a name="remarks"></a>備註  
 使用**close**方法關閉[連接](../../../ado/reference/ado-api/connection-object-ado.md)、[記錄](../../../ado/reference/ado-api/record-object-ado.md)、[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)或[資料流程](../../../ado/reference/ado-api/stream-object-ado.md)物件，以釋放任何相關聯的系統資源。 關閉物件並不會將它從記憶體中移除;您可以變更其屬性設定，稍後再重新開啟它。 若要完全排除記憶體中的物件，請關閉物件，然後將物件變數設定為 [*無*] （在 Visual Basic 中）。  
  
## <a name="connection"></a>Connection  
 使用**close**方法關閉**連接**物件也會關閉與連接相關聯的任何作用中**記錄集**物件。 與您正在關閉的**連接**物件相關聯的[命令](../../../ado/reference/ado-api/command-object-ado.md)物件將會保存，但不會再與**Connection**物件相關聯。也就是說，其[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)屬性會設定為 [**無**]。 此外，**命令**物件的[parameters](../../../ado/reference/ado-api/parameters-collection-ado.md)集合也會清除任何提供者定義的參數。  
  
 您稍後可以呼叫[Open](../../../ado/reference/ado-api/open-method-ado-connection.md)方法來重新建立與相同或另一個資料來源的連接。 當**連接**物件關閉時，呼叫任何需要開啟資料來源連接的方法，都會產生錯誤。  
  
 當連接上有開啟的**記錄集**物件時，關閉**連接**物件會復原所有**記錄集**物件中的任何暫止變更。 當交易正在進行時，明確關閉**連接**物件（呼叫**Close**方法）會產生錯誤。 當交易正在進行時，如果**連接**物件超出範圍，ADO 會自動回復交易。  
  
## <a name="recordset-record-stream"></a>記錄集、記錄、資料流程  
 使用**close**方法關閉**記錄集**、**記錄**或**資料流程**物件，會釋出相關聯的資料，以及您對該特定物件所擁有之資料的任何獨佔存取權。 您稍後可以呼叫[Open](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法，以相同或已修改的屬性來重新開啟物件。  
  
 當**記錄集**物件關閉時，呼叫任何需要即時資料指標的方法會產生錯誤。  
  
 如果在立即更新模式中進行編輯，則呼叫**Close**方法會產生錯誤;相反地，請先呼叫[Update](../../../ado/reference/ado-api/update-method.md)或[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)方法。 如果您在批次更新模式中關閉**記錄集**物件，最後一個[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)呼叫之後的所有變更都會遺失。  
  
 如果您使用[Clone](../../../ado/reference/ado-api/clone-method-ado.md)方法來建立開啟**記錄集**物件的複本，關閉原始或複製不會影響任何其他複本。  
  
## <a name="applies-to"></a>套用至  
  
|||  
|-|-|  
|[Connection 物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[Record 物件 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|  
|[Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|[Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)|  
  
## <a name="see-also"></a>另請參閱  
 [Open 和 Close 方法範例（VB）](../../../ado/reference/ado-api/open-and-close-methods-example-vb.md)   
 [Open 和 Close 方法範例（VBScript）](../../../ado/reference/ado-api/open-and-close-methods-example-vbscript.md)   
 [Open 和 Close 方法範例（VC + +）](../../../ado/reference/ado-api/open-and-close-methods-example-vc.md)   
 [Open 方法（ADO Connection）](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open 方法（ADO Recordset）](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Save 方法](../../../ado/reference/ado-api/save-method.md)
