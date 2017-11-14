---
title: "Clone 方法 (ADO) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset20::Clone
- Recordset20::raw_Clone
helpviewer_keywords:
- Clone method [ADO]
ms.assetid: ad49265f-1c05-4271-9bbf-7c00010ac18c
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9b7586bef017cd4e5f3a89586b8600abfd183f5a
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="clone-method-ado"></a>Clone 方法 (ADO)
建立複本[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)從現有物件**資料錄集**物件。 選擇性地指定複製處於唯讀模式。  
  
## <a name="syntax"></a>語法  
  
```  
  
Set rstDuplicate = rstOriginal.Clone (LockType)  
```  
  
## <a name="return-value"></a>傳回值  
 傳回**資料錄集**物件參考。  
  
#### <a name="parameters"></a>參數  
 *rstDuplicate*  
 識別重複項目之物件變數**資料錄集**来建立物件。  
  
 *rstOriginal*  
 物件變數可識別**資料錄集**要複製的物件。  
  
 *LockType*  
 選擇性。 A [LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md)值，指定鎖定類型原始**資料錄集**，或唯讀**資料錄集**。 有效值為**adLockUnspecified**或**Recordset**。  
  
## <a name="remarks"></a>備註  
 使用**複製**方法來建立多個重複**資料錄集**物件，特別是如果您想要維護多個目前記錄的記錄組中。 使用**複製**方法會更有效率，比建立並開啟新**資料錄集**使用相同的定義與原始物件。  
  
 [篩選](../../../ado/reference/ado-api/filter-property.md)屬性的原始**資料錄集**，如果任何項目，不會套用至複製品。 設定**篩選**屬性的新**資料錄集**來篩選結果。 最簡單的方式複製任何現有**篩選**值會指派它，直接、，如下所示。  
  
```  
rsNew.Filter = rsOriginal.Filter  
```  
  
 新建立複製品的目前記錄設定為第一筆記錄。  
  
 您對其中一個變更**資料錄集**物件中會顯示所有它的複製品，不論資料指標類型。 不過，之後您執行[Requery](../../../ado/reference/ado-api/requery-method.md)原始**資料錄集**，複製程式碼將不再同步處理至原始。  
  
 關閉原始**資料錄集**不會關閉它的複本，也不會關閉複本關閉原始或任何其他複本。  
  
 您可以只複製**資料錄集**支援書籤的物件。 書籤值是可互換。也就是從某個書籤參考**資料錄集**物件參照到任何其複製品中的相同記錄。  
  
 某些**資料錄集**觸發的事件也會發生在所有**資料錄集**複製。 不過，因為目前的記錄可以不同之間複製**資料錄集**，事件可能不是有效的複製品。 例如，如果您變更欄位的值， [WillChangeField](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)事件就會發生在變更**資料錄集**和所有複製程式碼中。 *欄位*參數**WillChangeField**事件複製**資料錄集**（其中不進行變更） 將此複本，目前記錄的欄位參考可能會比目前的原始記錄不同的記錄**資料錄集**發生變更。  
  
 下表提供所有的完整清單**資料錄集**事件。 它會指出它們是否有效，而且觸發的任何使用所產生的資料錄集複製品**複製**方法。  
  
|事件|複製程式碼中觸發嗎？|  
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
 [資料錄集物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [再製方法範例 (VB)](../../../ado/reference/ado-api/clone-method-example-vb.md)   
 [再製方法範例 (VBScript)](../../../ado/reference/ado-api/clone-method-example-vbscript.md)   
 [再製方法範例 （VC + +）](../../../ado/reference/ado-api/clone-method-example-vc.md)   

