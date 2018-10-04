---
title: Error 物件 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error
helpviewer_keywords:
- error object [ADO]
ms.assetid: a175d453-fa55-4f49-9ede-a26d83177919
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ea282362853ca25a761f870970a288585a00160e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47802926"
---
# <a name="error-object"></a>Error 物件
包含屬於單一作業牽涉到提供者的資料存取錯誤的詳細資料。  
  
## <a name="remarks"></a>備註  
 任何涉及 ADO 物件的作業可能會產生一或多個提供者錯誤。 每個錯誤發生時，一或多個**錯誤**物件置於[錯誤](../../../ado/reference/ado-api/errors-collection-ado.md)集合[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件。 另一個 ADO 作業會產生錯誤，當**錯誤**集合會進行清除，和一組新的**錯誤**物件會置於**錯誤**集合。  
  
> [!NOTE]
>  每個**錯誤**物件都代表特定的提供者的錯誤，而不是 ADO 錯誤。 ADO 錯誤會公開至執行階段例外狀況處理機制。 例如，在 Microsoft Visual Basic 中，ADO 特定錯誤的相符項目將會觸發**On Error**事件，並出現在**錯誤**物件。 ADO 錯誤的完整清單，請參閱 < [ErrorValueEnum](../../../ado/reference/ado-api/errorvalueenum.md)主題。  
  
 您可以閱讀**錯誤**物件的屬性，以取得有關每個錯誤，包括下列特定詳細資料：  
  
-   [描述](../../../ado/reference/ado-api/description-property.md)屬性，其中包含錯誤的文字。 這是預設屬性。  
  
-   [數字](../../../ado/reference/ado-api/number-property-ado.md)屬性，其中包含**長**錯誤常數整數值。  
  
-   [來源](../../../ado/reference/ado-api/source-property-ado-error.md)屬性，可識別引發錯誤的物件。 當您有數個時，這會特別有用**錯誤**中的物件**錯誤**遵循要求至資料來源的集合。  
  
-   [SQLState](../../../ado/reference/ado-api/sqlstate-property.md)並[NativeError](../../../ado/reference/ado-api/nativeerror-property-ado.md)屬性，其中提供 SQL 資料來源的資訊。  
  
 發生提供者錯誤時，它會置於**錯誤**的集合**連線**物件。 ADO 支援傳回多個錯誤，單一的 ADO 作業，以提供錯誤的資訊提供者特有的。 若要取得此豐富的錯誤資訊的錯誤處理常式中，使用適當的錯誤捕捉功能的語言或環境正在使用，則使用巢狀的迴圈來列舉每個屬性**錯誤**物件**錯誤**集合。  
  
> [!NOTE]
>  **Microsoft Visual Basic 和 VBScript 使用者**如果無法有效**連接**物件，您必須擷取錯誤資訊**錯誤**物件。  
  
 就如同提供者執行，ADO 清除**OLE 錯誤資訊**物件，才能進行呼叫，可能無法產生新的提供者錯誤。 不過，**錯誤**收集**連線**物件就會清除並填入或提供者會產生新的錯誤時，只[清除](../../../ado/reference/ado-api/clear-method-ado.md)呼叫方法。  
  
 某些屬性和方法會傳回警告，如下所示**錯誤**中的物件**錯誤**集合，但不是會中斷程式執行。 在呼叫之前[Resync](../../../ado/reference/ado-api/resync-method.md)， [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)，或[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)上的方法[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件;[開啟](../../../ado/reference/ado-api/open-method-ado-connection.md)方法**連接**物件，或是設定[篩選](../../../ado/reference/ado-api/filter-property.md)屬性**資料錄集**物件，請呼叫**清除**上的方法**錯誤**集合。 如此一來，您可以閱讀[計數](../../../ado/reference/ado-api/count-property-ado.md)屬性**錯誤**来測試的集合傳回警告。  
  
 **錯誤**物件不是安全的。  
  
 本章節包含下列主題。  
  
-   [Error 物件屬性、方法和事件](../../../ado/reference/ado-api/error-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [描述、 HelpContext、 HelpFile、 NativeError、 數目、 來源和 SQLState 屬性範例 (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [描述、 HelpContext、 HelpFile、 NativeError、 數目、 來源和 SQLState 屬性範例 （VC + +）](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [連接物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Errors 集合 (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)   
 [附錄 A：提供者](../../../ado/guide/appendixes/appendix-a-providers.md)
