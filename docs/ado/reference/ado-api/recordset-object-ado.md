---
description: Recordset 物件 (ADO)
title: " (ADO) 的記錄集物件 |Microsoft Docs"
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
author: rothja
ms.author: jroth
ms.openlocfilehash: d9fade9e23303c9adaa22cad9822381fd10bb513
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88772267"
---
# <a name="recordset-object-ado"></a>Recordset 物件 (ADO)
表示基表中的整組記錄，或執行命令的結果。 在任何時間， **記錄集** 物件都只會將集合中的單一記錄參考為目前的記錄。  
  
## <a name="remarks"></a>備註  
 您可以使用 **記錄集** 物件操作提供者的資料。 當您使用 ADO 時，會使用 **記錄集** 物件幾乎完全運算元據。 所有 **記錄集** 物件都包含記錄 (資料列) 和欄位 (資料行) 。 視提供者支援的功能而定，可能無法使用某些 **記錄集** 方法或屬性。  
  
 ADODB.記錄集是用來建立 **記錄集** 物件的 ProgID。 參考過期 ADOR 的現有應用程式。記錄集 ProgID 將繼續運作而不需要重新編譯，但新的開發應該參考 ADODB。記錄。  
  
 ADO 中定義了四種不同的資料指標類型：  
  
-   **動態資料指標** 可讓您查看其他使用者的新增、變更和刪除;允許透過不依賴書簽的 **記錄集** 進行所有類型的移動;如果提供者支援，則允許書簽。  
  
-   索引**鍵集資料指標**行為類似動態資料指標，不同之處在于它會防止您看到其他使用者所加入的記錄，並防止存取其他使用者所刪除的記錄。 其他使用者的資料變更仍會顯示。 它一律支援書簽，因此可讓所有類型的移動都通過 **記錄集**。  
  
-   **靜態資料指標** 提供一組記錄的靜態複本，供您用來尋找資料或產生報表;一律允許書簽，因此允許所有類型的移動都通過 **記錄集**。 其他使用者將看不到新增、變更或刪除。 當您開啟用戶端 **記錄集** 物件時，這是唯一允許的資料指標類型。  
  
-   順**向資料指標**可讓您只在**記錄集中**向前滾動。 其他使用者將看不到新增、變更或刪除。 這可改善在您需要只通過 **記錄集**的單一階段時的效能。  
  
 先設定[CursorType](./cursortype-property-ado.md)屬性，然後再開啟**記錄集**以選擇資料指標類型，或使用[Open](./open-method-ado-recordset.md)方法傳遞*CursorType*引數。 有些提供者不支援所有資料指標類型。 請查看提供者的檔。 如果您未指定資料指標類型，則 ADO 預設會開啟順向資料指標。  
  
 如果[CursorLocation](./cursorlocation-property-ado.md)屬性設定為**AdUseClient**來開啟**記錄集**，則在傳回的**記錄集**物件中無法使用[欄位](./field-object.md)物件上的**UnderlyingValue**屬性。 搭配某些提供者使用 (例如 Microsoft ODBC Provider for OLE DB 與 Microsoft SQL Server) 搭配使用時，您可以藉由使用**Open**方法傳遞連接字串，來建立與先前定義之[連接](./connection-object-ado.md)物件無關的**記錄集**物件。 ADO 仍會建立 [連接](./connection-object-ado.md) 物件，但不會將該物件指派給物件變數。 但是，如果您要透過相同的連接開啟多個 **記錄集** 物件，您應該明確建立並開啟 **連接** 物件;這會將 **連接** 物件指派給物件變數。 如果您未在開啟**記錄集**物件時使用這個物件變數，即使您傳遞相同的連接字串，ADO 仍會為每個新的**記錄集**建立新的**連接**物件。  
  
 您可以視需要建立多個 **記錄集** 物件。  
  
 當您開啟 **記錄集**時，如果有任何) 和 [BOF](./bof-eof-properties-ado.md) 和 [EOF](./bof-eof-properties-ado.md) 屬性設為 **False**，則目前的記錄會定位至第一個記錄 (。 如果沒有任何記錄， **BOF** 和 **EOF** 屬性設定為 **True**。  
  
 您可以使用 [MoveFirst](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md)、 **MoveLast**、 **MoveNext**和 **MovePrevious** 方法; [Move](./move-method-ado.md) 方法;以及 [AbsolutePosition](./absoluteposition-property-ado.md)、 [AbsolutePage](./absolutepage-property-ado.md)和 [Filter](./filter-property.md) 屬性，以重新置放目前的記錄，假設提供者支援相關的功能。 順向 **記錄集** 物件只支援 [MoveNext](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md) 方法。 當您使用 **移動** 方法來造訪每一筆記錄 (或列舉 **記錄集**) 時，您可以使用 **BOF** 和 **EOF** 屬性來判斷您是否已移到 **記錄集**的開頭或結尾之外。  
  
 在使用 **記錄集** 物件的任何功能之前，您必須先在物件上呼叫 **支援** 方法，以確認功能是否受到支援或可用。 當 **支援** 方法傳回 false 時，您不能使用此功能。 例如，只有在傳回 True 時，您才能使用**MovePrevious**方法 `Recordset.Supports(adMovePrevious)` 。 **True** 否則，您將會收到錯誤，因為 **記錄集** 物件可能已經關閉，而且無法在實例上使用轉譯的功能。 如果您感興趣的功能不受支援， **支援** 也會傳回 false。 在此情況下，您應該避免在 **記錄集** 物件上呼叫對應的屬性或方法。  
  
 **記錄集** 物件可以支援兩種類型的更新：立即和批次。 在立即更新中，當您呼叫 [Update](./update-method.md) 方法之後，對資料所做的所有變更都會立即寫入基礎資料來源。 您也可以使用 [AddNew](./addnew-method-ado.md) 和 **Update** 方法，以參數的形式傳遞值陣列，並同時更新記錄中的數個欄位。  
  
 如果提供者支援批次更新，您可以讓提供者快取變更為一個以上的記錄，然後在對資料庫的單一呼叫中使用 [UpdateBatch](./updatebatch-method.md) 方法進行傳輸。 這適用于使用 **AddNew**、 **Update**和 [Delete](./delete-method-ado-recordset.md) 方法進行的變更。 呼叫 **UpdateBatch** 方法之後，您可以使用 [Status](./status-property-ado-recordset.md) 屬性來檢查是否有任何資料衝突，以便解決這些衝突。  
  
> [!NOTE]
>  若要在不使用[Command](./command-object-ado.md)物件的情況下執行查詢，請將查詢字串傳遞至**記錄集**物件的**Open**方法。 但是，當您想要保存命令文字並重新執行它，或使用查詢參數時，需要 **command** 物件。  
  
 [Mode](./mode-property-ado.md)屬性會控制存取權限。  
  
 **Fields**集合是**記錄集**物件的預設成員。 因此，下列兩個程式碼語句是相等的。  
  
```  
Debug.Print objRs.Fields.Item(0)  ' Both statements print   
Debug.Print objRs(0)              '  the Value of Item(0).  
```  
  
 當 **記錄集** 物件跨進程傳遞時，只會封送 **處理資料列集的值** ，而且會忽略 **記錄集** 物件的屬性。 在 unmarshalling 期間， **會將資料列集解壓縮** 至新建立的 **記錄集** 物件，此物件也會將其屬性設定為預設值。  
  
 **記錄集**物件可以安全地進行腳本處理。  
  
 本節包含下列主題。  
  
-   [Recordset 物件屬性、方法和事件](./recordset-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (ADO) 的 Connection 物件 ](./connection-object-ado.md)   
 [ (ADO) 的欄位集合 ](./fields-collection-ado.md)   
 [ (ADO) 的屬性集合 ](./properties-collection-ado.md)   
 [附錄 A：提供者](../../guide/appendixes/appendix-a-providers.md)