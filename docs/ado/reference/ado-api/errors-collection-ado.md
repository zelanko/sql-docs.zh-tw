---
title: Errors 集合 (ADO) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: b595baf25a8b0f3982399c384c169c6af3f1cd81
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63253184"
---
# <a name="errors-collection-ado"></a>Errors 集合 (ADO)
包含所有[錯誤](../../../ado/reference/ado-api/error-object.md)單一提供者相關的失敗回應所建立的物件。  
  
## <a name="remarks"></a>備註  
 任何涉及 ADO 物件的作業可能會產生一或多個提供者錯誤。 每個錯誤發生時，一或多個**錯誤**物件可置於**錯誤**集合[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件。 另一個 ADO 作業會產生錯誤，當**錯誤**集合會進行清除，和一組新的**錯誤**物件可以放置在**錯誤**集合。  
  
 每個**錯誤**物件都代表特定的提供者的錯誤，而不是 ADO 錯誤。 ADO 錯誤會公開至執行階段例外狀況處理機制。 例如，在 Microsoft Visual Basic 中，ADO 特定錯誤的相符項目將會觸發[onError](../../../ado/reference/rds-api/onerror-event-rds.md)事件，並出現在**Err**物件。  
  
 不要產生錯誤的 ADO 作業沒有任何作用**錯誤**集合。 使用[清除](../../../ado/reference/ado-api/clear-method-ado.md)方法，以手動方式清除**錯誤**集合。  
  
 一組**錯誤**中的物件**錯誤**集合會描述所有回應單一陳述式中發生的錯誤。 列舉中的特定錯誤**錯誤**集合可讓您更精確地判斷原因和來源的錯誤，並採取適當步驟，以復原的錯誤處理常式。  
  
 某些屬性和方法會傳回警告，如下所示**錯誤**中的物件**錯誤**集合，但不是會中斷程式執行。 在呼叫之前[Resync](../../../ado/reference/ado-api/resync-method.md)， [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)，或[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)上的方法[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件，[開啟](../../../ado/reference/ado-api/open-method-ado-connection.md)方法**連接**物件，或設[篩選](../../../ado/reference/ado-api/filter-property.md)屬性**資料錄集**物件，請呼叫**清除**上的方法**錯誤**集合。 如此一來您可以閱讀[計數](../../../ado/reference/ado-api/count-property-ado.md)屬性**錯誤**来測試的集合傳回警告。  
  
> [!NOTE]
>  請參閱**錯誤**單一 ADO 作業可能會產生多個錯誤的方式的更詳細說明的物件主題。  
  
 本章節包含下列主題。  
  
-   [錯誤的集合屬性、 方法和事件](../../../ado/reference/ado-api/errors-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [Error 物件](../../../ado/reference/ado-api/error-object.md)   
 [附錄 a:提供者](../../../ado/guide/appendixes/appendix-a-providers.md)
