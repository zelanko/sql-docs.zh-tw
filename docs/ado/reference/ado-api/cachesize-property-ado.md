---
title: CacheSize 屬性 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::CacheSize
helpviewer_keywords:
- CacheSize property [ADO]
ms.assetid: 49dc9a49-af7b-433b-be36-7a14ca984fb7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 76cd9e4977ffda023c270a027602597ddf7b9a4a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63028225"
---
# <a name="cachesize-property-ado"></a>CacheSize 屬性 (ADO)
指出從資料錄數目[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)會在本機快取在記憶體中的物件。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**長**必須大於 0 的值。 預設值為 1。  
  
## <a name="remarks"></a>備註  
 使用**CacheSize**屬性，即可控制多少筆記錄到本機的記憶體，從提供者擷取一次。 例如，如果**CacheSize**為 10 之後的第一個左,**資料錄集**物件，提供者擷取的前 10 筆記錄到本機的記憶體。 當您瀏覽**資料錄集**物件，提供者傳回的資料從本機記憶體緩衝區。 只要您超出快取中的最後一筆記錄時，提供者會從資料來源擷取的接下來的 10 筆記錄到快取中。  
  
> [!NOTE]
>  **CacheSize**為基礎**開啟資料列的最大**提供者特有的屬性 (在**屬性**的集合**資料錄集**物件)。 您無法設定**CacheSize**的值大於**開啟資料列的最大**。 若要修改提供者都可以開啟的資料列數目，設定**開啟資料列的最大**。  
  
 值**CacheSize**生命週期的期間，可以調整**資料錄集**物件，但變更此值只會影響快取中的記錄數目在後續的擷取資料來源之後。 變更屬性值還不會變更目前的快取內容。  
  
 如果有較少的記錄，以讀取比**CacheSize**指定提供者會傳回剩餘的記錄，並不會發生錯誤。  
  
 A **CacheSize**不允許設定為零，並傳回錯誤。  
  
 從快取中擷取的記錄不會反映其他使用者對來源資料的並行變更。 若要強制更新所有快取的資料，請使用[Resync](../../../ado/reference/ado-api/resync-method.md)方法。  
  
 如果**CacheSize**設為大於一的巡覽方法 ([移動](../../../ado/reference/ado-api/move-method-ado.md)， [MoveFirst、 MoveLast、 MoveNext 和 MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)) 可能會導致瀏覽至已刪除記錄，如果記錄已擷取之後，就會刪除。 之後的初始提取，後續的刪除動作將不會反映在您的資料快取直到您嘗試存取的資料值從已刪除的資料列。 不過，設定**CacheSize**其中一個會消除這個問題因為無法擷取已刪除的資料列。  
  
## <a name="applies-to"></a>適用於  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [CacheSize 屬性範例 (VB)](../../../ado/reference/ado-api/cachesize-property-example-vb.md)   
 [CacheSize 屬性範例 （VC + +）](../../../ado/reference/ado-api/cachesize-property-example-vc.md)   
 [CacheSize 屬性範例 (JScript)](../../../ado/reference/ado-api/cachesize-property-example-jscript.md)
