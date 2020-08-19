---
description: Requery 方法
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
author: rothja
ms.author: jroth
ms.openlocfilehash: b13d618bf5b9b2c17a4fd93b08f3a861cb958178
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88442320"
---
# <a name="requery-method"></a>Requery 方法
藉由重新執行物件所依據的查詢來更新 [記錄集](../../../ado/reference/ado-api/recordset-object-ado.md) 物件中的資料。  
  
## <a name="syntax"></a>語法  
  
```  
  
recordset.Requery Options  
```  
  
#### <a name="parameters"></a>參數  
 *選項*  
 選擇性。 位元遮罩，包含影響此作業的 [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) 和 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) 值。  
  
> [!NOTE]
>  如果 *選項* 設定為 **adAsyncExecute**，這項作業將會以非同步方式執行，而且會在結束時發出 [RecordsetChangeComplete](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md) 事件。 **AdExecuteNoRecords**或**adExecuteStream**的**ExecuteOpenEnum**值不應與**Requery**一起使用。  
  
## <a name="remarks"></a>備註  
 您可以使用 **Requery** 方法，重新發出原始命令並第二次抓取資料，以重新整理資料來源中 **記錄集** 物件的整個內容。 呼叫這個方法相當於連續呼叫 [Close](../../../ado/reference/ado-api/close-method-ado.md) 和 [Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) 方法。 如果您要編輯目前的記錄或加入新記錄，就會發生錯誤。  
  
 當 **記錄集** 物件開啟時，定義資料指標本質的屬性 ([CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)、 [LockType](../../../ado/reference/ado-api/locktype-property-ado.md)、 [MaxRecords](../../../ado/reference/ado-api/maxrecords-property-ado.md)等) 是唯讀的。 因此， **Requery** 方法只能重新整理目前的資料指標。 若要變更任何資料指標屬性和查看結果，您必須使用 [Close](../../../ado/reference/ado-api/close-method-ado.md) 方法，才能讓屬性再次變成讀取/寫入。 然後，您可以變更屬性設定，並呼叫 [Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) 方法來重新開啟資料指標。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (VB 的 Execute、Requery 和 Clear 方法範例) ](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vb.md)   
 [Execute、Requery 和 Clear 方法範例 (VBScript) ](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vbscript.md)   
 [Execute、Requery 和 Clear 方法範例 (VC + +) ](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vc.md)   
 [CommandText 屬性 (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)
