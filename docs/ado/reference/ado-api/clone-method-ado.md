---
description: Clone 方法 (ADO)
title: " (ADO) 複製方法 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::Clone
- Recordset20::raw_Clone
helpviewer_keywords:
- Clone method [ADO]
ms.assetid: ad49265f-1c05-4271-9bbf-7c00010ac18c
author: rothja
ms.author: jroth
ms.openlocfilehash: c91960975b04e5c09cf2745e1bb77e7b343dbd2e
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88776247"
---
# <a name="clone-method-ado"></a>Clone 方法 (ADO)
從現有的**記錄集**物件建立重複的[記錄集](./recordset-object-ado.md)物件。 （選擇性）指定複製是唯讀的。  
  
## <a name="syntax"></a>語法  
  
```  
  
Set rstDuplicate = rstOriginal.Clone (LockType)  
```  
  
## <a name="return-value"></a>傳回值  
 傳回 **記錄集** 物件參考。  
  
#### <a name="parameters"></a>參數  
 *rstDuplicate*  
 物件變數，識別要建立的重複 **記錄集** 物件。  
  
 *rstOriginal*  
 物件變數，識別要複製的 **記錄集** 物件。  
  
 *LockType*  
 選擇性。 [LockTypeEnum](./locktypeenum.md)值，指定原始**記錄集**的鎖定類型或唯讀**記錄集**。 有效的值為 **adLockUnspecified** 或 **adLockReadOnly**。  
  
## <a name="remarks"></a>備註  
 您可以使用 **Clone** 方法來建立多個重複的 **記錄集** 物件，尤其是如果您想要在一組指定的記錄中維護一個以上的目前記錄。 使用 **Clone** 方法會比建立及開啟新的 **記錄集** 物件，該物件會使用與原始相同的定義，更有效率。  
  
 原始**記錄集**的[Filter](./filter-property.md)屬性（如果有的話）將不會套用至複製。 設定新**記錄集**的**filter**屬性以篩選結果。 複製任何現有 **篩選** 值最簡單的方式，就是直接指派它，如下所示。  
  
```  
rsNew.Filter = rsOriginal.Filter  
```  
  
 新建立之複製的目前記錄會設定為第一筆記錄。  
  
 您對一個 **記錄集** 物件所做的變更，不論資料指標類型為何，都可以在其所有複製中看到。 不過，在原始記錄集上執行重新 [查詢](./requery-method.md) 之後，複製就不會再同步處理至原始 **記錄集**。  
  
 關閉原始 **記錄集** 並不會關閉其複本，也不會關閉複製以關閉原始或任何其他複本。  
  
 您只能複製支援書簽的 **記錄集** 物件。 書簽值是可互換的;也就是說，來自一個 **記錄集** 物件的書簽參考會參考其任何複製中的相同記錄。  
  
 觸發的某些 **記錄集** 事件也會出現在所有 **記錄集** 的複製中。 不過，由於複製的記錄 **集**之間的目前記錄可能不同，因此事件對複製而言可能無效。 例如，如果您變更欄位的值， [WillChangeField](./willchangefield-and-fieldchangecomplete-events-ado.md) 事件就會出現在變更的 **記錄集** 和所有複製中。 在未進行變更的情況下，所複製之**記錄集**之**WillChangeField**事件的*fields*參數 () 將會參考複製的目前記錄的欄位，而這可能與發生變更之原始記錄**集**的目前記錄不同。  
  
 下表提供所有 **記錄集** 事件的完整清單。 它會指出它們是否有效，以及是否針對使用 **Clone** 方法所產生的任何記錄集複製而觸發。  
  
|事件|在複製中觸發？|  
|-----------|--------------------------|  
|[EndOfRecordset](./endofrecordset-event-ado.md)|否|  
|[FetchComplete](./fetchcomplete-event-ado.md)|否|  
|[FetchProgress](./fetchprogress-event-ado.md)|否|  
|[FieldChangeComplete](./willchangefield-and-fieldchangecomplete-events-ado.md)|是|  
|[MoveComplete](./willmove-and-movecomplete-events-ado.md)|否|  
|[RecordChangeComplete](./willchangerecord-and-recordchangecomplete-events-ado.md)|是|  
|[RecordsetChangeComplete](./willchangerecordset-and-recordsetchangecomplete-events-ado.md)|否|  
|[WillChangeField](./willchangefield-and-fieldchangecomplete-events-ado.md)|是|  
|[WillChangeRecord](./willchangerecord-and-recordchangecomplete-events-ado.md)|是|  
|[WillChangeRecordset](./willchangerecordset-and-recordsetchangecomplete-events-ado.md)|否|  
|[WillMove](./willmove-and-movecomplete-events-ado.md)|否|  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (VB) 複製方法範例 ](./clone-method-example-vb.md)   
 [ (VBScript) 的複製方法範例 ](./clone-method-example-vbscript.md)   
 [Clone 方法範例 (VC++)](./clone-method-example-vc.md)