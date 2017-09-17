---
title: "資料錄集物件 (ADO) |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset
helpviewer_keywords:
- Recordset object [ADO]
ms.assetid: ede1415f-c3df-4cc5-a05b-2576b2b84b60
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7ad07b3aeaa8428bc5c2dee78a061c511893daef
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="recordset-object-ado"></a>資料錄集物件 (ADO)
代表完整記錄的基底資料表或執行的命令的結果。 在任何時候，**資料錄集**物件是指單一資料錄和目前的記錄集內。  
  
## <a name="remarks"></a>備註  
 您使用**資料錄集**來操作資料提供者的物件。 當您使用 ADO 時，您會操作幾乎已完全使用資料**資料錄集**物件。 所有**資料錄集**物件所組成 （資料列） 的記錄和欄位 （資料行）。 根據提供者，支援的功能有些**資料錄集**方法或屬性可能無法使用。  
  
 ADODB。資料錄集是應該用來建立的 ProgID**資料錄集**物件。 參考過時的 ADOR 的現有應用程式。資料錄集 ProgID 會繼續運作，而不必重新編譯，但新開發應該參考 ADODB。資料錄集。  
  
 有在 ADO 定義四種不同的資料指標類型：  
  
-   **動態資料指標**可讓您檢視新增、 變更和刪除其他使用者; 允許所有類型的移動**資料錄集**不依賴書籤;，而且如果提供者支援，可都讓書籤它們。  
  
-   **索引鍵集資料指標**像動態資料指標，但它會阻止您看到記錄的其他使用者的行為，加上其他使用者刪除的記錄則會防止存取。 仍會看到其他使用者的資料變更。 它一律支援書籤，並因此可讓所有類型的移動**資料錄集**。  
  
-   **靜態資料指標**提供一組記錄，以用來尋找資料，或產生報表的靜態複本，則一律可讓書籤，因此便可透過移動的所有類型**資料錄集**。 新增、 變更或刪除其他使用者將不會顯示的。 這是唯一的資料指標開啟用戶端時，允許類型**資料錄集**物件。  
  
-   **順向資料指標**可讓您只能透過向前捲動**資料錄集**。 新增、 變更或刪除其他使用者將不會顯示的。 這可改善效能的情況下必須只有單一通過**資料錄集**。  
  
 設定[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)屬性，再開啟**資料錄集**選擇資料指標類型，或傳遞*CursorType*引數與[開啟](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法。 某些提供者不支援所有的資料指標類型。 請查看提供者的文件。 如果您未指定資料指標類型，ADO 預設會開啟順向資料指標。  
  
 如果[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性設定為**adUseClient**開啟**資料錄集**、 **UnderlyingValue**屬性[欄位](../../../ado/reference/ado-api/field-object.md)物件不適用於傳回**資料錄集**物件。 某些提供者 （例如 OLE DB 搭配 Microsoft SQL Server 的 Microsoft ODBC 提供者） 搭配使用時，您可以建立**資料錄集**獨立先前定義的物件[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件，並傳遞連接字串與**開啟**方法。 ADO 仍會建立[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件，但它不會將該物件指派給物件變數。 不過，如果您開啟多個**資料錄集**物件，在相同的連線，您應該明確地建立及開啟**連接**物件; 此指派**連接**給物件變數的物件。 開啟時如果您不使用這個物件變數您**資料錄集**物件，建立新的 ADO**連接**每個物件新增**資料錄集**，即使您將相同的傳遞連接字串。  
  
 您可以建立多個**資料錄集**所需的物件。  
  
 當您開啟**資料錄集**，目前的記錄位於第一個記錄 （如果有的話） 和[BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)和[EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)屬性會設為**False**. 如果沒有記錄， **BOF**和**EOF**屬性設定為**True**。  
  
 您可以使用[MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)， **MoveLast**， **MoveNext**，和**MovePrevious**方法;[移動](../../../ado/reference/ado-api/move-method-ado.md)方法。和[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)， [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)，和[篩選](../../../ado/reference/ado-api/filter-property.md)來重新調整位置目前的記錄，假設提供者支援的相關內容這項功能。 順向**資料錄集**物件僅支援[MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)方法。 當您使用**移動**造訪每一筆記錄的方法 (或列舉**資料錄集**)，您可以使用**BOF**和**EOF**屬性決定是否您已經移到範圍之外的開頭或結尾**資料錄集**。  
  
 使用的任何功能之前**資料錄集**物件，您必須呼叫**支援**来驗證的功能也支援或提供的物件上的方法。 您必須不能使用的功能時**支援**方法會傳回 false。 例如，您可以使用**MovePrevious**方法才`Recordset.Supports(adMovePrevious)`傳回**True**。 否則，您會收到錯誤，因為**資料錄集**物件可能已關閉，且功能呈現執行個體上無法使用。 如果您有興趣的一項功能不受支援，**支援**會傳回 false 同時。 在此情況下，您應該避免呼叫對應的屬性或方法上**Recrodset**物件。  
  
 **資料錄集**物件可以支援兩種類型的更新： 立即和批次。 在立即更新所有資料變更會立即都寫入基礎資料來源一旦呼叫[更新](../../../ado/reference/ado-api/update-method.md)方法。 您也可以傳遞值的陣列做為參數與[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)和**更新**方法，並同時更新數個記錄中的欄位。  
  
 如果提供者支援批次更新，您可以讓快取多個記錄的變更，然後再將其傳輸至資料庫的單一呼叫中的提供者[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)方法。 這適用於透過所做變更**AddNew**，**更新**，和[刪除](../../../ado/reference/ado-api/delete-method-ado-recordset.md)方法。 在您呼叫後**UpdateBatch**方法，您可以使用[狀態](../../../ado/reference/ado-api/status-property-ado-recordset.md)屬性來檢查是否有任何的資料衝突，才能加以解決。  
  
> [!NOTE]
>  若要執行查詢，而不使用[命令](../../../ado/reference/ado-api/command-object-ado.md)物件，傳遞查詢字串以**開啟**方法**資料錄集**物件。 不過，**命令**物件時，需要您想要保存的命令文字，並重新執行它，或使用查詢參數。  
  
 [模式](../../../ado/reference/ado-api/mode-property-ado.md)屬性可控制存取權限。  
  
 **欄位**集合是預設成員**資料錄集**物件。 因此，下列兩個程式碼陳述式是相等的。  
  
```  
Debug.Print objRs.Fields.Item(0)  ' Both statements print   
Debug.Print objRs(0)              '  the Value of Item(0).  
```  
  
 當**資料錄集**跨處理序，只傳遞物件**資料列集**值會封送處理，以及的屬性**資料錄集**物件會被忽略。 期間 unmarshalling，**資料列集**解除封裝到新建立**資料錄集**物件，其屬性也會設定為預設值。  
  
 **資料錄集**物件而言是安全的指令碼。  
  
 本章節包含下列主題。  
  
-   [資料錄集物件屬性、 方法和事件](../../../ado/reference/ado-api/recordset-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [連接物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [欄位集合 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [屬性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [附錄 a： 提供者](../../../ado/guide/appendixes/appendix-a-providers.md)
