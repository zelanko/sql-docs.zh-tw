---
title: 資料錄集物件 (ADO) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 1bf2aab4e9f11ff3dae9852dd80007867fe5a462
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47770826"
---
# <a name="recordset-object-ado"></a>Recordset 物件 (ADO)
代表整個記錄集的基底資料表或執行命令的結果。 在任何時候**資料錄集**物件是指單一資料錄和目前的記錄集內。  
  
## <a name="remarks"></a>備註  
 您使用**資料錄集**來操作資料提供者的物件。 當您使用 ADO 時，您操作資料使用幾乎完全**資料錄集**物件。 所有**資料錄集**物件所組成 （資料列） 的記錄和欄位 （資料行）。 根據提供者所支援的功能有些**資料錄集**方法或屬性可能無法使用。  
  
 ADODB。資料錄集是應該用來建立的 ProgID**資料錄集**物件。 參考過期的 ADOR 的現有應用程式。資料錄集 ProgID 會繼續運作而不需要重新編譯，但開發新程式時應該參考 ADODB。資料錄集。  
  
 有在 ADO 中定義的四種不同的資料指標類型：  
  
-   **動態資料指標**可讓您檢視新增、 變更及刪除由其他使用者，可讓所有類型的移動**資料錄集**不依賴書籤 」; 而且可都讓書籤，如果提供者支援它們。  
  
-   **索引鍵集資料指標**Behaves 等動態資料指標，但它會阻止您看到的記錄，讓其他使用者，加上其他使用者刪除的記錄會防止存取。 由其他使用者的資料變更仍會顯示。 它一律支援書籤，並因此可讓所有類型的移動**資料錄集**。  
  
-   **靜態資料指標**提供一組您用來尋找資料，或產生報表記錄的靜態複本，一律可讓書籤，因此便可透過移動的所有類型**資料錄集**。 新增、 變更或刪除由其他使用者將不會顯示的。 這是唯一的型別，當您開啟用戶端時，允許的資料指標**資料錄集**物件。  
  
-   **順向資料指標**可讓您只透過向前捲動**資料錄集**。 新增、 變更或刪除由其他使用者將不會顯示的。 這可改善效能，在您需要僅單一通過**資料錄集**。  
  
 設定[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)屬性，在開啟之前**資料錄集**選擇資料指標類型，或傳遞*CursorType*引數與[開啟](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法。 某些提供者不支援所有的資料指標類型。 請檢查提供者的文件。 如果您未指定資料指標類型，ADO 會開啟預設的順向資料指標。  
  
 如果[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性設定為**adUseClient**以開啟**資料錄集**，則**UnderlyingValue** 屬性[欄位](../../../ado/reference/ado-api/field-object.md)中所傳回的物件沒有**資料錄集**物件。 某些提供者 （例如 OLE DB 搭配使用 Microsoft SQL Server 的 Microsoft ODBC 提供者） 搭配使用時，您可以建立**Recordset**獨立於先前定義的物件[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件，並傳遞連接字串**開啟**方法。 仍會建立 ADO[連線](../../../ado/reference/ado-api/connection-object-ado.md)物件，但它不會將該物件指派給物件變數。 不過，如果您開啟多個**Recordset**物件，在相同的連線，您應該明確地建立並開啟**連線**物件; 此指派**連接**給物件變數的物件。 開啟時如果您不使用此物件變數您**資料錄集**物件，建立新的 ADO**連線**每個物件新增**資料錄集**，即使您傳遞相同連接字串。  
  
 您可以建立多個**資料錄集**物件所需。  
  
 當您開啟**資料錄集**，目前的記錄位於第一筆記錄 （如果有的話） 和[BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)並[EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)屬性設為**False**. 如果不有任何記錄， **BOF**並**EOF**屬性設定為**True**。  
  
 您可以使用[MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)， **MoveLast**， **MoveNext**，以及**MovePrevious**方法，而[移動](../../../ado/reference/ado-api/move-method-ado.md)方法;而[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)， [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)，並[篩選](../../../ado/reference/ado-api/filter-property.md)重新定位的目前的記錄，假設提供者支援的相關屬性功能。 順**Recordset**僅支援物件[MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)方法。 當您使用**移動**方法，以瀏覽每一筆記錄 (或列舉**資料錄集**)，您可以使用**BOF**並**EOF**屬性決定是否您已移動超過的開頭或結尾**資料錄集**。  
  
 之前使用的任何功能**Recordset**物件，您必須呼叫**支援**来驗證的功能也支援或提供的物件上的方法。 您不能使用的功能時**支援**方法會傳回 false。 例如，您可以使用**MovePrevious**方法才`Recordset.Supports(adMovePrevious)`會傳回**True**。 否則，您會收到錯誤，因為**資料錄集**物件可能已關閉，且功能呈現執行個體上無法使用。 如果您有興趣的功能不受支援，**支援**會傳回 false 以及。 在此情況下，您應該避免上呼叫對應的屬性或方法**資料錄集**物件。  
  
 **資料錄集**物件可支援兩種類型的更新： 即時和批次。 在立即更新，所有資料變更會立即都寫入基礎資料來源之後呼叫[更新](../../../ado/reference/ado-api/update-method.md)方法。 您也可以為參數傳遞值的陣列[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)並**更新**方法，並同時更新記錄中的數個欄位。  
  
 如果提供者支援批次更新，您可以快取多個記錄的變更，然後再將它們傳輸至資料庫的單一呼叫中的提供者[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)方法。 這會套用到與所做的變更**AddNew**，**更新**，並[刪除](../../../ado/reference/ado-api/delete-method-ado-recordset.md)方法。 在您呼叫後**UpdateBatch**方法，您可以使用[狀態](../../../ado/reference/ado-api/status-property-ado-recordset.md)屬性，以檢查是否有任何的資料衝突，若要解決這些問題。  
  
> [!NOTE]
>  若要執行查詢，而不使用[命令](../../../ado/reference/ado-api/command-object-ado.md)物件，傳遞至查詢字串**開啟**方法**資料錄集**物件。 不過，**命令**物件時，需要您想要保存的命令文字和重新執行，或使用查詢參數。  
  
 [模式](../../../ado/reference/ado-api/mode-property-ado.md)屬性會管理存取權限。  
  
 **欄位**集合是預設成員**資料錄集**物件。 如此一來，下列兩個程式碼陳述式是相等的。  
  
```  
Debug.Print objRs.Fields.Item(0)  ' Both statements print   
Debug.Print objRs(0)              '  the Value of Item(0).  
```  
  
 當**資料錄集**跨處理序，只會傳遞的物件**資料列集**值封送處理，以及的屬性**資料錄集**物件會被忽略。 Unmarshalling，期間**資料列集**解除封裝到新建**資料錄集**物件，也會設定其屬性設為預設值。  
  
 **資料錄集**物件而言是安全的指令碼。  
  
 本章節包含下列主題。  
  
-   [資料錄集物件屬性、 方法和事件](../../../ado/reference/ado-api/recordset-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [連接物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Fields 集合 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [屬性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [附錄 A：提供者](../../../ado/guide/appendixes/appendix-a-providers.md)
