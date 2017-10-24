---
title: "Close 方法 (ADO) |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset15::Close
- _Stream::Close
- _Record::Close
helpviewer_keywords:
- Close method [ADO]
ms.assetid: 3cdf27d1-a180-4cff-8e42-95dec5fb1b55
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f8780b5ab445364d5cb99bbde6407052fcfa7db3
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="close-method-ado"></a>Close 方法 (ADO)
關閉開啟的物件和任何相依的物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.Close  
```  
  
## <a name="remarks"></a>備註  
 使用**關閉**方法，關閉[連接](../../../ado/reference/ado-api/connection-object-ado.md)、[記錄](../../../ado/reference/ado-api/record-object-ado.md)、[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)，或[資料流](../../../ado/reference/ado-api/stream-object-ado.md)物件若要釋放任何相關聯的系統資源。 關閉物件不會將它從記憶體中移除您可以變更其屬性設定，並稍後重新開啟它。 若要完全消除從記憶體物件，關閉物件，然後將物件變數設定為*Nothing* （在 Visual Basic)。  
  
## <a name="connection"></a>連接  
 使用**關閉**方法，關閉**連接**物件也會關閉任何使用中**資料錄集**與連接相關聯的物件。 A[命令](../../../ado/reference/ado-api/command-object-ado.md)物件相關聯**連接**會保存您在關閉的物件，但不會再將相關聯**連接**物件，也就是其[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)屬性將設定為**Nothing**。 此外，**命令**物件的[參數](../../../ado/reference/ado-api/parameters-collection-ado.md)集合將會清除任何提供者定義的參數。  
  
 您可以稍後呼叫[開啟](../../../ado/reference/ado-api/open-method-ado-connection.md)方法，以重新建立相同或另一個資料來源的連接。 雖然**連接**物件已關閉時，需要開啟連接至資料來源之任何方法會產生錯誤。  
  
 關閉**連接**物件時開啟**資料錄集**連接上的物件會回復任何暫止的變更中的所有**資料錄集**物件。 明確地關閉**連接**物件 (呼叫**關閉**方法) 進行異動時產生錯誤。 如果**連接**物件超出範圍的交易正在進行時，ADO 會自動回復交易。  
  
## <a name="recordset-record-stream"></a>資料錄集，記錄中，資料流  
 使用**關閉**方法，關閉**資料錄集**，**記錄**，或**資料流**物件釋放相關聯的資料和任何的獨佔存取權您可能必須透過這個特定的物件資料。 您可以稍後呼叫[開啟](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法，以重新開啟與相同，或修改的物件屬性。  
  
 雖然**資料錄集**物件已關閉時，需要即時的資料指標之任何方法會產生錯誤。  
  
 如果編輯正在進行立即更新模式中，呼叫**關閉**方法會產生錯誤; 請改為呼叫[更新](../../../ado/reference/ado-api/update-method.md)或[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)方法第一次。 如果您關閉**資料錄集**物件在批次更新模式時，所有的變更，自上次[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)呼叫將會遺失。  
  
 如果您使用[複製](../../../ado/reference/ado-api/clone-method-ado.md)方法建立的開啟複本**資料錄集**物件時，關閉原始或複製不會影響任何其他複本。  
  
## <a name="applies-to"></a>適用於  
  
|||  
|-|-|  
|[連接物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[記錄物件 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|  
|[資料錄集物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|[資料流物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)|  
  
## <a name="see-also"></a>另請參閱  
 [開啟與關閉方法範例 (VB)](../../../ado/reference/ado-api/open-and-close-methods-example-vb.md)   
 [開啟與關閉方法範例 (VBScript)](../../../ado/reference/ado-api/open-and-close-methods-example-vbscript.md)   
 [開啟與關閉方法範例 （VC + +）](../../../ado/reference/ado-api/open-and-close-methods-example-vc.md)   
 [Open 方法 （ADO 連接）](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open 方法 （ADO 資料錄集）](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Save 方法](../../../ado/reference/ado-api/save-method.md)

