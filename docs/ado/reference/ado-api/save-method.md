---
title: 儲存方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Recordset::Save
- _Recordset::raw_Save
helpviewer_keywords:
- Save method [ADO]
ms.assetid: ed3d9678-5c28-4e61-8bb3-7dfb66d99cf5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6ec1601749b6537484cead17c50492de131932ea
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67931179"
---
# <a name="save-method"></a>Save 方法
將[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)儲存在檔案或[資料流程](../../../ado/reference/ado-api/stream-object-ado.md)物件中。  
  
## <a name="syntax"></a>語法  
  
```  
  
recordset.Save Destination, PersistFormat  
```  
  
#### <a name="parameters"></a>參數  
 *目的地*  
 選擇性。 **Variant** ，代表要儲存**記錄集**之檔案的完整路徑名稱，或**資料流程**物件的參考。  
  
 *PersistFormat*  
 選擇性。 [PersistFormatEnum](../../../ado/reference/ado-api/persistformatenum.md)值，指定儲存**記錄集**的格式（XML 或 ADTG）。 預設值為**adPersistADTG**。  
  
## <a name="remarks"></a>備註  
 只能在開啟的**記錄集**上叫用[Save 方法](../../../ado/reference/ado-api/save-method.md)方法。 使用[Open 方法（ADO Recordset）](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法，稍後從*目的地*還原**記錄集**。  
  
 如果[篩選器屬性](../../../ado/reference/ado-api/filter-property.md)屬性對**記錄集**有效，則只會儲存篩選器底下可存取的資料列。 如果**記錄集**是階層式，則會儲存目前的子**記錄集**和其子系，包括父**記錄集**。 如果呼叫子**記錄集**的 Save 方法，則會儲存子系及其所有子系，但父系則不會。  
  
 第一次儲存**記錄集**時，可以選擇是否要指定*目的地*。 如果您省略*目的地*，將會建立新的檔案，並將名稱設定為**記錄集**之 Source 屬性的值。  
  
 當您後續呼叫**儲存**後第一次儲存時，請省略*目的地*，否則會發生執行階段錯誤。 如果您隨後使用新的*目的地*呼叫 [**儲存**]，則會將**記錄集**儲存至新的目的地。 不過，新的目的地和原始目的地皆會開啟。  
  
 [**儲存**] 不會關閉**記錄集**或*目的地*，因此您可以繼續使用**記錄集**，並儲存最新的變更。 *目的地*會保持開啟狀態，直到**記錄集**關閉為止。  
  
 基於安全性的理由， **Save**方法只允許從 Microsoft Internet Explorer 所執行的腳本使用低和自訂安全性設定。  
  
 如果在進行非同步**記錄集**提取、執行或更新作業時呼叫**save**方法，則會等到非同步作業完成後，再**儲存**等候。  
  
 記錄會從**記錄集**的第一個資料列開始儲存。 當**Save**方法完成時，目前的資料列位置會移到**記錄集**的第一個資料列。  
  
 為獲得最佳結果，請將[CursorLocation 屬性（ADO）](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性設定為 [ **adUseClient** ]，並使用 [**儲存**]。 如果您的提供者不支援儲存**記錄集**物件所需的所有功能，則資料指標服務會提供該功能。  
  
 當**記錄**集保存並將**CursorLocation**屬性設定為**adUseServer**時，**記錄集**的更新功能會受到限制。 一般來說，只允許單一資料表的更新、插入和刪除（相依于提供者功能）。 此設定中也無法使用[Resync 方法](../../../ado/reference/ado-api/resync-method.md)方法。  
  
> [!NOTE]
>  ADO 不支援儲存具有**adVariant**、 **adIDispatch**或**AdIUnknown**類型**欄位**的**記錄集**，而且可能會導致無法預期的結果。  
  
 只有條件字串形式的篩選（例如，訂購單 > ' 12/31/1999 '）會影響保存的**記錄集**內容。 使用**書簽**陣列或使用[FilterGroupEnum](../../../ado/reference/ado-api/filtergroupenum.md)中的值所建立的篩選，將不會影響保存之**記錄集**的內容。 這些規則適用于以用戶端或伺服器端資料指標建立的**記錄集**。  
  
 因為*Destination*參數可以接受任何支援 OLE DB IStream 介面的物件，所以您可以將**記錄集**直接儲存到 ASP Response 物件。 如需詳細資訊，請參閱**XML 記錄集持續性案例**。  
  
 您也可以將 XML 格式的**記錄集**儲存至 MSXML DOM 物件的實例，如下列 Visual Basic 程式碼所示：  
  
```  
Dim xDOM As New MSXML.DOMDocument  
Dim rsXML As New ADODB.Recordset  
Dim sSQL As String, sConn As String  
  
sSQL = "SELECT customerid, companyname, contactname FROM customers"  
sConn="Provider=Microsoft.Jet.OLEDB.4.0;Data Source=Northwind.mdb"  
rsXML.Open sSQL, sConn  
rsXML.Save xDOM, adPersistXML   'Save Recordset directly into a DOM tree.  
...  
```  
  
> [!NOTE]
>  以 XML 格式儲存階層式記錄集（資料圖形）時，適用兩項限制。 如果階層式**記錄集**包含暫止的更新，您就無法儲存到 XML，而且您無法儲存參數化的階層式**記錄集**。  
  
 以 XML 格式儲存的**記錄集會**使用 utf-8 格式儲存。 將這類檔案載入 ADO 資料流程時，除非資料流程的 [字元集] 屬性設定為 UTF-8 格式的適當值，否則資料流程物件不會嘗試從資料流程開啟**記錄集**。  
  
## <a name="applies-to"></a>套用至  
  
|||  
|-|-|  
|[Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|[Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)|  
  
## <a name="see-also"></a>另請參閱  
 [Save 和 Open 方法範例（VB）](../../../ado/reference/ado-api/save-and-open-methods-example-vb.md)   
 [Save 和 Open 方法範例（VC + +）](../../../ado/reference/ado-api/save-and-open-methods-example-vc.md)   
 [Open 方法（ADO Recordset）](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Open 方法（ADO Stream）](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [SaveToFile 方法](../../../ado/reference/ado-api/savetofile-method.md)
