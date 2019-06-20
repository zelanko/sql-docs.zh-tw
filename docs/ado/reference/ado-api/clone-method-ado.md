---
title: Clone 方法 (ADO) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: fbeedf9e56c1f0606a7c8f842baedc9d11ad3929
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66698792"
---
# <a name="clone-method-ado"></a>Clone 方法 (ADO)
建立複本[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)從現有的物件**資料錄集**物件。 選擇性地指定複製處於唯讀模式。  
  
## <a name="syntax"></a>語法  
  
```  
  
Set rstDuplicate = rstOriginal.Clone (LockType)  
```  
  
## <a name="return-value"></a>傳回值  
 傳回**資料錄集**物件參考。  
  
#### <a name="parameters"></a>參數  
 *rstDuplicate*  
 物件變數可識別重複**資料錄集**要建立物件。  
  
 *rstOriginal*  
 物件變數可識別**資料錄集**被複製的物件。  
  
 *LockType*  
 選擇性。 A [LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md)值，指定任一鎖定類型的原始**Recordset**，或唯讀**資料錄集**。 有效值**adLockUnspecified**或是**Recordset**。  
  
## <a name="remarks"></a>備註  
 使用**複製品**方法來建立多個重複**資料錄集**物件，特別是如果您想要維護一組指定的記錄中的多個目前資料錄。 使用**複製品**方法的效率高於建立並開啟新**資料錄集**使用相同的定義與原始物件。  
  
 [篩選條件](../../../ado/reference/ado-api/filter-property.md)屬性的原始**資料錄集**，如果任何項目，不會套用到複製。 設定**篩選條件**屬性的新**資料錄集**來篩選結果。 最簡單的方式複製任何現有**篩選**值會指派它，直接、，如下所示。  
  
```  
rsNew.Filter = rsOriginal.Filter  
```  
  
 建立新建立的複製目前的記錄會設定為第一筆記錄。  
  
 變更您對一**資料錄集**物件會顯示在所有其複製品，無論何種資料指標類型。 不過，您執行之後[Requery](../../../ado/reference/ado-api/requery-method.md)原始**資料錄集**，複製程式碼將不會再同步處理至原始。  
  
 關閉原始**資料錄集**不會關閉其複本，也不會關閉複本關閉原始或任何其他複本。  
  
 您可以只複製**資料錄集**支援書籤的物件。 書籤值是可互換的。也就是書籤參考從某個**資料錄集**物件是指任何其複製品中相同的記錄。  
  
 有些**Recordset**觸發的事件也會發生在所有**資料錄集**複製。 不過，因為目前的記錄就不同複製**資料錄集**，事件可能不是有效的複製。 例如，如果您變更欄位的值， [WillChangeField](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)事件就會發生在已變更**資料錄集**和所有的複製程式碼中。 *欄位*的參數**WillChangeField**複製的事件**資料錄集**（其中不進行變更） 會參考此複本，目前記錄的欄位這可能是不同的記錄比目前的資料錄的原始**資料錄集**發生變更。  
  
 下表提供所有的完整清單**資料錄集**事件。 它會指出它們是否有效且觸發的任何使用所產生的資料錄集複製品**複製品**方法。  
  
|Event - 事件|觸發此選項，以複製程式碼嗎？|  
|-----------|--------------------------|  
|[EndOfRecordset](../../../ado/reference/ado-api/endofrecordset-event-ado.md)|否|  
|[FetchComplete](../../../ado/reference/ado-api/fetchcomplete-event-ado.md)|否|  
|[FetchProgress](../../../ado/reference/ado-api/fetchprogress-event-ado.md)|否|  
|[FieldChangeComplete](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|是|  
|[MoveComplete](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|否|  
|[RecordChangeComplete](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|是|  
|[RecordsetChangeComplete](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|否|  
|[WillChangeField](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|是|  
|[WillChangeRecord](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|是|  
|[WillChangeRecordset](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|否|  
|[WillMove](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|否|  
  
## <a name="applies-to"></a>適用於  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Clone 方法範例 (VB)](../../../ado/reference/ado-api/clone-method-example-vb.md)   
 [Clone 方法範例 (VBScript)](../../../ado/reference/ado-api/clone-method-example-vbscript.md)   
 [Clone 方法範例 (VC++)](../../../ado/reference/ado-api/clone-method-example-vc.md)   
