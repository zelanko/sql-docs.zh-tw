---
description: Close 方法 (ADO)
title: " (ADO) 的 Close 方法 |Microsoft Docs"
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 5f2fe4aff39b29e937de88f3166698fb8f9ad730
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88776217"
---
# <a name="close-method-ado"></a>Close 方法 (ADO)
關閉開啟的物件和任何相依的物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.Close  
```  
  
## <a name="remarks"></a>備註  
 您可以使用 **close** 方法來關閉 [連接](./connection-object-ado.md)、 [記錄](./record-object-ado.md)、記錄 [集](./recordset-object-ado.md)或 [資料流程](./stream-object-ado.md) 物件，以釋放任何相關聯的系統資源。 關閉物件並不會將它從記憶體中移除;您可以變更其屬性設定，稍後再重新開啟。 若要完全消除記憶體中的物件，請關閉物件，然後在 Visual Basic) 中將物件變數設定為 [ *Nothing* ] (。  
  
## <a name="connection"></a>連線  
 使用 **close** 方法關閉 **連接** 物件也會關閉與連接相關聯的任何使用中 **記錄集** 物件。 與您正在關閉之**連接**物件相關聯的[Command](./command-object-ado.md)物件將會保存，但它將不會再與**連接**物件產生關聯;也就是說，其[ActiveConnection](./activeconnection-property-ado.md)屬性會設定為**Nothing**。 此外，也會清除 **命令** 物件的 [參數](./parameters-collection-ado.md) 集合，以提供任何提供者定義的參數。  
  
 您稍後可以呼叫 [Open](./open-method-ado-connection.md) 方法，重新建立與相同或另一個資料來源的連接。 **連接**物件關閉時，呼叫任何需要開啟資料來源連接的方法會產生錯誤。  
  
 當連接 **上** 有開啟的記錄集物件時，會在連接上開啟 **記錄集** 物件，並在所有的 **記錄集** 物件中回復任何暫止的變更。 明確地關閉 **連接** 物件 (呼叫 **Close** 方法) 而交易進行中時，會產生錯誤。 當交易正在進行時，如果 **連接** 物件超出範圍，則 ADO 會自動回復交易。  
  
## <a name="recordset-record-stream"></a>記錄集、記錄、資料流程  
 使用 **close** 方法來關閉 **記錄集**、 **記錄**或 **資料流程** 物件，會釋出相關聯的資料，以及透過這個特定物件對資料所擁有的任何獨佔存取權。 您稍後可以呼叫 [Open](./open-method-ado-recordset.md) 方法，以相同或已修改的屬性重新開啟物件。  
  
 當 **記錄集** 物件關閉時，呼叫任何需要即時資料指標的方法會產生錯誤。  
  
 如果在立即更新模式中進行編輯，則呼叫 **Close** 方法會產生錯誤;相反地，請先呼叫 [Update](./update-method.md) 或 [CancelUpdate](./cancelupdate-method-ado.md) 方法。 當您在批次更新模式中關閉 **記錄集** 物件時，自上次的 [UpdateBatch](./updatebatch-method.md) 呼叫之後的所有變更都會遺失。  
  
 如果您使用 [Clone](./clone-method-ado.md) 方法來建立開啟 **記錄集** 物件的複本，則關閉原始或複製不會影響任何其他複本。  
  
## <a name="applies-to"></a>套用至  

:::row:::
    :::column:::
        [Connection 物件 (ADO)](./connection-object-ado.md)  
        [Record 物件 (ADO)](./record-object-ado.md)  
    :::column-end:::
    :::column:::
        [Recordset 物件 (ADO)](./recordset-object-ado.md)  
        [Stream 物件 (ADO)](./stream-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>另請參閱  
 [ (VB 的 Open 和 Close 方法範例) ](./open-and-close-methods-example-vb.md)   
 [ (VBScript) 的開啟和關閉方法範例 ](./open-and-close-methods-example-vbscript.md)   
 [Open 和 Close 方法範例 (VC + +) ](./open-and-close-methods-example-vc.md)   
 [ (ADO Connection) 的 Open 方法 ](./open-method-ado-connection.md)   
 [ (ADO 記錄集的 Open 方法) ](./open-method-ado-recordset.md)   
 [Save 方法](./save-method.md)