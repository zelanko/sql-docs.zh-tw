---
title: Requery 方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::Requery
- Recordset15::raw_Requery
helpviewer_keywords:
- Requery method [ADO]
ms.assetid: d81ab76f-1aa8-4ccf-92ec-b65254dc3ea1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 433f5d279e638e3ccdf7ba3a7bb2590f80b04a6b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63062366"
---
# <a name="requery-method"></a>Requery 方法
更新中的資料[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)重新執行查詢所依據之物件的物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
recordset.Requery Options  
```  
  
#### <a name="parameters"></a>參數  
 *選項。*  
 選擇性。 包含的位元遮罩[的執行方式](../../../ado/reference/ado-api/executeoptionenum.md)並[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)會影響這項作業的值。  
  
> [!NOTE]
>  如果*選項*設為**adAsyncExecute**，這項作業會以非同步方式執行並[RecordsetChangeComplete](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)才決定乾脆時，就會發出事件。 **ExecuteOpenEnum**的值**adExecuteNoRecords**或是**adExecuteStream**不應使用**Requery**。  
  
## <a name="remarks"></a>備註  
 使用**Requery**方法，以重新整理的整個內容**資料錄集**重新發出原始命令，並擷取資料的第二次的資料來源中的物件。 呼叫這個方法就相當於呼叫[關閉](../../../ado/reference/ado-api/close-method-ado.md)並[開啟](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法連續。 如果您正在編輯目前的記錄，或新增記錄，就會發生錯誤。  
  
 雖然**資料錄集**物件開啟時，定義資料指標的本質的屬性 ([CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)， [LockType](../../../ado/reference/ado-api/locktype-property-ado.md)， [MaxRecords](../../../ado/reference/ado-api/maxrecords-property-ado.md)等等) 都是唯讀。 因此， **Requery**方法只重新整理目前的游標。 若要變更任何資料指標屬性並檢視結果，您必須使用[關閉](../../../ado/reference/ado-api/close-method-ado.md)方法，讓屬性變成讀取/寫入一次。 您可以再變更此屬性設定，並且呼叫[開啟](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法來重新開啟資料指標。  
  
## <a name="applies-to"></a>適用於  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Execute、 Requery 和 Clear 方法範例 (VB)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vb.md)   
 [Execute、 Requery 和 Clear 方法範例 (VBScript)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vbscript.md)   
 [Execute、 Requery 和 Clear 方法範例 （VC + +）](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vc.md)   
 [CommandText 屬性 (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)
