---
title: Errors 集合（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::Errors
- Connection15::get_Errors
- Connection15::GetErrors
helpviewer_keywords:
- Errors collection [ADO]
ms.assetid: 290819e1-7b39-4e1e-a93b-801257138b00
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e3c8f981d4dc40a4a6f618f3cca387379d51def9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67932972"
---
# <a name="errors-collection-ado"></a>Errors 集合 (ADO)
包含為了回應單一提供者相關的失敗所建立的所有[錯誤](../../../ado/reference/ado-api/error-object.md)物件。  
  
## <a name="remarks"></a>備註  
 任何牽涉到 ADO 物件的作業都可能產生一個或多個提供者錯誤。 當發生每個錯誤時，可以將一個或多個**錯誤**物件放在[Connection](../../../ado/reference/ado-api/connection-object-ado.md)物件的**Errors**集合中。 當另一個 ADO 作業產生錯誤時，會清除**錯誤**集合，而新的**錯誤**物件集合則可以放在**Errors**集合中。  
  
 每個**錯誤**物件都代表特定的提供者錯誤，而不是 ADO 錯誤。 ADO 錯誤會公開給執行時間例外狀況處理機制。 例如，在 Microsoft Visual Basic 中，發生 ADO 特定錯誤時，會觸發[onError](../../../ado/reference/rds-api/onerror-event-rds.md)事件，並出現在**Err**物件中。  
  
 不會產生錯誤的 ADO 作業不會影響**錯誤**集合。 使用[Clear](../../../ado/reference/ado-api/clear-method-ado.md)方法來手動清除**錯誤**集合。  
  
 **錯誤**集合中的一組**錯誤**物件描述回應單一語句時所發生的所有錯誤。 列舉**錯誤**集合中的特定錯誤，可讓您的錯誤處理常式更精確地判斷錯誤的原因和來源，並採取適當的步驟來復原。  
  
 某些屬性和方法會傳回**錯誤**集合中顯示為**錯誤**物件的警告，但不會暫停程式的執行。 在您呼叫[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件上的[Resync](../../../ado/reference/ado-api/resync-method.md)、 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)或[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)方法之前、**連接**物件上的[Open](../../../ado/reference/ado-api/open-method-ado-connection.md)方法，或是設定**記錄集**物件的[Filter](../../../ado/reference/ado-api/filter-property.md)屬性之前，請在**錯誤**集合上呼叫**Clear**方法。 如此一來，您就可以讀取**Errors**集合的[Count](../../../ado/reference/ado-api/count-property-ado.md)屬性來測試傳回的警告。  
  
> [!NOTE]
>  如需單一 ADO 作業如何產生多個錯誤之方式的詳細說明，請參閱**Error**物件主題。  
  
 本章節包含下列主題。  
  
-   [Errors 集合屬性、方法和事件](../../../ado/reference/ado-api/errors-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [Error 物件](../../../ado/reference/ado-api/error-object.md)   
 [附錄 A：提供者](../../../ado/guide/appendixes/appendix-a-providers.md)
