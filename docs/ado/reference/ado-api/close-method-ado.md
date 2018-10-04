---
title: Close 方法 (ADO) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: f43e59ed38dfde8091cb851f75a133c60874a6af
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47644688"
---
# <a name="close-method-ado"></a>Close 方法 (ADO)
關閉開啟的物件和任何相依的物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.Close  
```  
  
## <a name="remarks"></a>備註  
 使用**關閉**方法以關閉[連線](../../../ado/reference/ado-api/connection-object-ado.md)，則[記錄](../../../ado/reference/ado-api/record-object-ado.md)，則[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)，或[Stream](../../../ado/reference/ado-api/stream-object-ado.md)物件若要釋出的任何相關聯的系統資源。 關閉物件不會將它從記憶體中; 中移除您可以變更其屬性設定，然後稍後再重新開啟它。 若要完全消除從記憶體物件，關閉物件，然後將物件變數設*Nothing* （在 Visual Basic)。  
  
## <a name="connection"></a>連接  
 使用**關閉 **方法以關閉**連線**物件也會關閉任何作用**資料錄集**與連接相關聯的物件。 A[命令](../../../ado/reference/ado-api/command-object-ado.md)相關聯的物件**連線**會保存您在關閉的物件，但它不會再相關聯**連接**物件，也就是其[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)屬性會設定為**Nothing**。 此外，**命令**物件的[參數](../../../ado/reference/ado-api/parameters-collection-ado.md)集合將會清除任何提供者定義的參數。  
  
 您可以於稍後呼叫[開啟](../../../ado/reference/ado-api/open-method-ado-connection.md)方法，以重新建立在相同的或其他資料來源的連接。 雖然**連線**物件關閉時，需要開啟連接至資料來源之任何方法會產生錯誤。  
  
 關閉**連接**物件時沒有開放**資料錄集**連接上的物件回復任何暫止的變更在所有**資料錄集**物件。 明確地關閉**連接**物件 (呼叫**關閉**方法) 進行交易時產生錯誤。 如果**連線**物件就被踢出範圍，當交易正在進行時，ADO 會自動回復交易。  
  
## <a name="recordset-record-stream"></a>資料錄集、 記錄、 Stream  
 使用**關閉**方法以關閉**Recordset**，**記錄**，或**Stream**物件釋放相關聯的資料和任何的獨佔存取權您可能必須透過這個特定的物件資料。 您可以於稍後呼叫[開啟](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法來重新開啟的物件相同，或修改的屬性。  
  
 雖然**資料錄集**物件關閉時，呼叫任何需要即時的資料指標的方法會產生錯誤。  
  
 在立即更新模式中進行編輯時，呼叫**關閉**方法會產生錯誤; 相反地，呼叫[更新](../../../ado/reference/ado-api/update-method.md)或是[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)方法第一次。 如果您關閉**Recordset**物件在批次更新模式中，所有的變更，自上次[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)呼叫將會遺失。  
  
 如果您使用[複製品](../../../ado/reference/ado-api/clone-method-ado.md)方法來建立已開啟的副本**資料錄集**物件時，關閉原始或複本不會影響任何其他複本。  
  
## <a name="applies-to"></a>適用於  
  
|||  
|-|-|  
|[Connection 物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[Record 物件 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|  
|[Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|[Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)|  
  
## <a name="see-also"></a>另請參閱  
 [Open 和 Close 方法範例 (VB)](../../../ado/reference/ado-api/open-and-close-methods-example-vb.md)   
 [Open 和 Close 方法範例 (VBScript)](../../../ado/reference/ado-api/open-and-close-methods-example-vbscript.md)   
 [Open 和 Close 方法範例 （VC + +）](../../../ado/reference/ado-api/open-and-close-methods-example-vc.md)   
 [Open 方法 (ADO Connection)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open 方法 (ADO Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Save 方法](../../../ado/reference/ado-api/save-method.md)
