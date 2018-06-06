---
title: Error 物件 |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error
helpviewer_keywords:
- error object [ADO]
ms.assetid: a175d453-fa55-4f49-9ede-a26d83177919
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6911493ab691b2c5e40ff4fa7331261070d981be
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="error-object"></a>Error 物件
包含關於涉及提供者的單一作業相關的資料存取錯誤的詳細資料。  
  
## <a name="remarks"></a>備註  
 任何作業，涉及 ADO 物件可能會產生一或多個提供者錯誤。 當每個錯誤發生時，一或多個**錯誤**物件置於[錯誤](../../../ado/reference/ado-api/errors-collection-ado.md)集合[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件。 當另一個 ADO 作業會產生錯誤，**錯誤**集合會進行清除，和一組新的**錯誤**物件置於**錯誤**集合。  
  
> [!NOTE]
>  每個**錯誤**物件都代表特定的提供者錯誤，而不是 ADO 錯誤。 ADO 錯誤都會公開至執行階段例外狀況處理機制。 例如，在 Microsoft Visual Basic 中，ADO 特定錯誤的項目將會觸發**On Error**事件，並出現在**錯誤**物件。 ADO 錯誤的完整清單，請參閱[ErrorValueEnum](../../../ado/reference/ado-api/errorvalueenum.md)主題。  
  
 您可以閱讀**錯誤**物件的屬性，以取得有關每個錯誤，包括下列的特定詳細資料：  
  
-   [描述](../../../ado/reference/ado-api/description-property.md)屬性，其中包含錯誤的文字。 這是預設屬性。  
  
-   [數目](../../../ado/reference/ado-api/number-property-ado.md)屬性，其中包含**長**錯誤常數整數值。  
  
-   [來源](../../../ado/reference/ado-api/source-property-ado-error.md)屬性，識別引發錯誤的物件。 這是特別有用，當您有數個**錯誤**中的物件**錯誤**至資料來源之後，要求的集合。  
  
-   [SQLState](../../../ado/reference/ado-api/sqlstate-property.md)和[NativeError](../../../ado/reference/ado-api/nativeerror-property-ado.md)屬性，提供 SQL 資料來源的資訊。  
  
 發生提供者錯誤時，它會放置於**錯誤**集合**連接**物件。 ADO 支援單一 ADO 作業允許取得錯誤資訊特定提供者所傳回的多個錯誤。 若要取得此豐富的錯誤資訊的錯誤處理常式中，使用適當的錯誤截取功能之語言的環境正在使用，然後使用巢狀的迴圈來列舉每個屬性**錯誤**物件存放至**錯誤**集合。  
  
> [!NOTE]
>  **Microsoft Visual Basic 和 VBScript 使用者**如果不是有效**連接**物件，您必須擷取錯誤資訊**錯誤**物件。  
  
 就像提供者執行作業，ADO 清除**OLE 錯誤資訊**物件之前進行呼叫，可能無法產生新的提供者錯誤。 不過，**錯誤**集合**連接**物件是清除，而且只有當提供者產生新的錯誤，或是當填入[清除](../../../ado/reference/ado-api/clear-method-ado.md)方法呼叫。  
  
 某些屬性和方法傳回的警告會顯示為**錯誤**中的物件**錯誤**集合但不是會停止執行程式。 之前先呼叫[重新同步處理](../../../ado/reference/ado-api/resync-method.md)， [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)，或[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)方法[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件;[開啟](../../../ado/reference/ado-api/open-method-ado-connection.md)方法**連接**物件; 或設定[篩選](../../../ado/reference/ado-api/filter-property.md)屬性**資料錄集**物件，呼叫**清除**方法**錯誤**集合。 這樣一來，您可以閱讀[計數](../../../ado/reference/ado-api/count-property-ado.md)屬性**錯誤**来測試的集合傳回警告。  
  
 **錯誤**物件不是安全的。  
  
 本章節包含下列主題。  
  
-   [Error 物件屬性、方法和事件](../../../ado/reference/ado-api/error-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [描述、 HelpContext、 說明檔案、 NativeError、 數字、 來源和 SQLState 屬性範例 (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [描述、 HelpContext、 說明檔案、 NativeError、 數字、 來源和 SQLState 屬性範例 （VC + +）](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [連接物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [錯誤集合 (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)   
 [附錄 A：提供者](../../../ado/guide/appendixes/appendix-a-providers.md)
