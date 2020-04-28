---
title: Recordset 物件（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset
helpviewer_keywords:
- Recordset object [ADO]
ms.assetid: ede1415f-c3df-4cc5-a05b-2576b2b84b60
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e76bc993b6f3fed781b8458bc7cf4a70081cd167
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67931369"
---
# <a name="recordset-object-ado"></a>Recordset 物件 (ADO)
代表基表的整組記錄或已執行命令的結果。 **記錄集**物件隨時只會參考集合中的單一記錄做為目前的記錄。  
  
## <a name="remarks"></a>備註  
 您可以使用**記錄集**物件來操作提供者的資料。 使用 ADO 時，您幾乎可以使用**記錄集**物件來運算元據。 所有記錄**集**物件都是由記錄（資料列）和欄位（資料行）所組成。 視提供者支援的功能而定，某些**記錄集**方法或屬性可能無法使用。  
  
 ADODB.記錄集是應該用來建立**記錄集**物件的 ProgID。 參考過時 ADOR 的現有應用程式。記錄集 ProgID 會繼續正常執行，而不需要重新編譯，但新的開發應參考 ADODB。集中.  
  
 ADO 中定義了四種不同的資料指標類型：  
  
-   **動態資料指標**可讓您查看其他使用者的新增、變更和刪除;允許透過不依賴書簽的**記錄集**進行所有類型的移動;如果提供者支援，則會允許書簽。  
  
-   索引**鍵集資料指標**的行為就像動態資料指標，但它會防止您看到其他使用者新增的記錄，並防止存取其他使用者所刪除的記錄。 其他使用者的資料變更仍會顯示。 它一律支援書簽，因此可讓所有類型的移動都通過**記錄集**。  
  
-   **靜態資料指標**提供一組記錄的靜態複本，供您用來尋找資料或產生報表;一律允許書簽，因此允許所有類型的動作通過**記錄集**。 其他使用者的新增、變更或刪除將不會顯示。 當您開啟用戶端**記錄集**物件時，這是唯一允許的資料指標類型。  
  
-   順**向資料指標**可讓您只向前快轉到**記錄集**。 其他使用者的新增、變更或刪除將不會顯示。 這會在您只需要透過**記錄集**進行單一傳遞的情況下改善效能。  
  
 在開啟**記錄集**之前設定[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)屬性，以選擇資料指標類型，或使用[Open](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法傳遞*CursorType*引數。 有些提供者不支援所有資料指標類型。 查看提供者的檔。 如果您未指定資料指標類型，ADO 預設會開啟順向資料指標。  
  
 如果[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性設定為**AdUseClient**以開啟**記錄集**，則傳回的**記錄集**物件中將無法使用[欄位](../../../ado/reference/ado-api/field-object.md)物件上的**UnderlyingValue**屬性。 搭配某些提供者（例如適用于 OLE DB 的 Microsoft ODBC 提供者與 Microsoft SQL Server）一起使用時，您可以透過使用**Open**方法傳遞連接字串，來建立與先前定義的[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件無關的**記錄集**物件。 ADO 仍然會建立[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件，但不會將該物件指派給物件變數。 不過，如果您要在相同的連接上開啟多個**記錄集**物件，您應該明確地建立並開啟**連接**物件;這會將**連接**物件指派給物件變數。 如果您在開啟**記錄集**物件時未使用這個物件變數，ADO 會針對每個新的**記錄集**建立新的**連接**物件，即使您傳遞相同的連接字串也一樣。  
  
 您可以視需要建立多個**記錄集**物件。  
  
 當您開啟**記錄集**時，目前的記錄會定位於第一個記錄（如果有的話），而[BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)和[EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)屬性會設定為**False**。 如果沒有任何記錄，則**BOF**和**EOF**屬性設定為**True**。  
  
 您可以使用[MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)、 **MoveLast**、 **MoveNext**和**MovePrevious**方法;[Move](../../../ado/reference/ado-api/move-method-ado.md)方法;和 [ [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)]、[ [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)] 和 [[篩選](../../../ado/reference/ado-api/filter-property.md)] 屬性，以重新調整目前的記錄，假設提供者支援相關的功能。 順向**記錄集**物件只支援[MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)方法。 當您使用**Move**方法來流覽每一筆記錄（或列舉**記錄集**）時，您可以使用**BOF**和**EOF**屬性來判斷您是否已移至**記錄集**的開頭或結尾之外。  
  
 在使用**記錄集**物件的任何功能之前，您必須先在物件上呼叫**支援**方法，以確認功能已受到支援或可供使用。 當**支援**的方法傳回 false 時，您不能使用此功能。 例如，只有在傳回**True**時**MovePrevious** `Recordset.Supports(adMovePrevious)` ，才可以使用 MovePrevious 方法。 否則，您將會收到錯誤，因為**記錄集**物件可能已關閉，而且在實例上呈現無法使用的功能。 如果您感興趣的功能不受支援，則**支援**也會傳回 false。 在此情況下，您應該避免在**記錄集**物件上呼叫對應的屬性或方法。  
  
 **記錄集**物件可以支援兩種類型的更新：立即和批次處理。 在立即更新中，一旦您呼叫[Update](../../../ado/reference/ado-api/update-method.md)方法，資料的所有變更都會立即寫入基礎資料來源。 您也可以使用[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)和**Update**方法將值陣列當做參數傳遞，並同時更新記錄中的數個欄位。  
  
 如果提供者支援批次更新，您可以讓提供者快取變更為一個以上的記錄，然後使用[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)方法將它們傳輸到資料庫的單一呼叫中。 這適用于使用**AddNew**、 **Update**和[Delete](../../../ado/reference/ado-api/delete-method-ado-recordset.md)方法所做的變更。 呼叫**UpdateBatch**方法之後，您可以使用[Status](../../../ado/reference/ado-api/status-property-ado-recordset.md)屬性來檢查是否有任何資料衝突，以便解決問題。  
  
> [!NOTE]
>  若要在不使用[Command](../../../ado/reference/ado-api/command-object-ado.md)物件的情況下執行查詢，請將查詢字串傳遞至**記錄集**物件的**Open**方法。 不過，當您想要保存命令文字並重新執行它，或使用查詢參數時，需要**command**物件。  
  
 [Mode](../../../ado/reference/ado-api/mode-property-ado.md)屬性會控管存取權限。  
  
 **Fields**集合是**記錄集**物件的預設成員。 因此，下列兩個程式碼語句是相等的。  
  
```  
Debug.Print objRs.Fields.Item(0)  ' Both statements print   
Debug.Print objRs(0)              '  the Value of Item(0).  
```  
  
 在進程之間傳遞**記錄集**物件時，只會封送**處理資料列集值**，而**記錄集**物件的屬性則會被忽略。 在 unmarshalling 期間，資料列**集**會解壓縮到新建立的**記錄集**物件中，這也會將其屬性設定為預設值。  
  
 **記錄集**物件可安全地進行腳本處理。  
  
 本章節包含下列主題。  
  
-   [Recordset 物件屬性、方法和事件](../../../ado/reference/ado-api/recordset-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [Connection 物件（ADO）](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Fields 集合（ADO）](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [Properties 集合（ADO）](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [附錄 A：提供者](../../../ado/guide/appendixes/appendix-a-providers.md)
