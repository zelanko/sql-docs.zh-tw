---
title: 錯誤集合 (ADO) |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::Errors
- Connection15::get_Errors
- Connection15::GetErrors
helpviewer_keywords:
- Errors collection [ADO]
ms.assetid: 290819e1-7b39-4e1e-a93b-801257138b00
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 17e21c1d807ba537544a1578cb9ef2b8ea83ad21
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2018
ms.locfileid: "35278157"
---
# <a name="errors-collection-ado"></a>錯誤集合 (ADO)
包含所有[錯誤](../../../ado/reference/ado-api/error-object.md)為了回應單一提供者相關的失敗所建立的物件。  
  
## <a name="remarks"></a>備註  
 任何作業，涉及 ADO 物件可能會產生一或多個提供者錯誤。 當每個錯誤發生時，一或多個**錯誤**物件可以放在**錯誤**集合[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件。 當另一個 ADO 作業會產生錯誤，**錯誤**集合會進行清除，和一組新的**錯誤**物件可以放在**錯誤**集合。  
  
 每個**錯誤**物件都代表特定的提供者錯誤，而不是 ADO 錯誤。 ADO 錯誤都會公開至執行階段例外狀況處理機制。 例如，在 Microsoft Visual Basic 中，ADO 特定錯誤的項目將會觸發[onError](../../../ado/reference/rds-api/onerror-event-rds.md)事件，並出現在**Err**物件。  
  
 不要產生錯誤的 ADO 作業沒有任何作用**錯誤**集合。 使用[清除](../../../ado/reference/ado-api/clear-method-ado.md)方法，以手動清除**錯誤**集合。  
  
 一組**錯誤**中的物件**錯誤**組說明在單一陳述式中發生的所有錯誤。 列舉中的特定錯誤**錯誤**集合可讓您更精確地判斷原因和來源的錯誤，並採取適當的步驟來復原的錯誤處理常式。  
  
 某些屬性和方法傳回的警告會顯示為**錯誤**中的物件**錯誤**集合但不是會停止執行程式。 之前先呼叫[重新同步處理](../../../ado/reference/ado-api/resync-method.md)， [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)，或[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)方法[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件[開啟](../../../ado/reference/ado-api/open-method-ado-connection.md)方法**連接**物件，或設定[篩選](../../../ado/reference/ado-api/filter-property.md)屬性**資料錄集**物件，呼叫**清除**方法**錯誤**集合。 如此一來您可以閱讀[計數](../../../ado/reference/ado-api/count-property-ado.md)屬性**錯誤**来測試的集合傳回警告。  
  
> [!NOTE]
>  請參閱**錯誤**物件單一 ADO 作業可以產生多個錯誤的方式的更詳細的說明主題。  
  
 本章節包含下列主題。  
  
-   [錯誤集合屬性、 方法和事件](../../../ado/reference/ado-api/errors-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [Error 物件](../../../ado/reference/ado-api/error-object.md)   
 [附錄 A：提供者](../../../ado/guide/appendixes/appendix-a-providers.md)
