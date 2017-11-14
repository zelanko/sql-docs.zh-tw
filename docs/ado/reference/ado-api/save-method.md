---
title: "Save 方法 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Recordset::Save
- _Recordset::raw_Save
helpviewer_keywords:
- Save method [ADO]
ms.assetid: ed3d9678-5c28-4e61-8bb3-7dfb66d99cf5
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: edefe1c8d25abd84d5a5f82d7dde8035d82022ee
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="save-method"></a>Save 方法
將儲存[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)檔案中或[資料流](../../../ado/reference/ado-api/stream-object-ado.md)物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
recordset.Save Destination, PersistFormat  
```  
  
#### <a name="parameters"></a>參數  
 *目的地*  
 選擇性。 A **Variant** ，代表檔案的完整路徑名稱其中**資料錄集**儲存，或參考**資料流**物件。  
  
 *PersistFormat*  
 選擇性。 A [PersistFormatEnum](../../../ado/reference/ado-api/persistformatenum.md)值中指定的格式，**資料錄集**（XML 或 ADTG） 儲存。 預設值是**adPersistADTG**。  
  
## <a name="remarks"></a>備註  
 [Save 方法](../../../ado/reference/ado-api/save-method.md)可以只在開啟叫用方法**資料錄集**。 使用[Open 方法 （ADO 資料錄集）](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法來更新還原**資料錄集**從*目的地*。  
  
 如果[篩選屬性](../../../ado/reference/ado-api/filter-property.md)屬性實際上是針對**資料錄集**，則會儲存的資料列篩選器下存取。 如果**資料錄集**為階層式，然後目前的子系**資料錄集**和其子系會儲存包括父系**資料錄集**。 如果子系的 Save 方法**資料錄集**是呼叫，都儲存在子系及其所有子系，但不是父代。  
  
 第一次儲存**資料錄集**，則可以指定選擇性*目的地*。 如果您省略*目的地*，將會以 [來源] 屬性的值設定為名稱建立新檔案**資料錄集**。  
  
 省略*目的地*當您後續呼叫**儲存**第一次儲存或執行階段錯誤發生之後。 如果您後續呼叫**儲存**與新*目的地*、**資料錄集**儲存至新的目的地。 不過，新的目的地和的原始目的端會同時為開啟。  
  
 **儲存**不會關閉**資料錄集**或*目的地*，因此您可以繼續使用**資料錄集**並儲存最新變更。 *目的地*維持開啟直到**資料錄集**已關閉。  
  
 基於安全性，**儲存**方法允許只使用執行 Microsoft Internet explorer 的指令碼的低和自訂安全性設定。  
  
 如果**儲存**時的非同步呼叫方法**資料錄集**擷取、 執行、 或更新作業正在進行中，然後**儲存**等候，直到非同步作業已完成。  
  
 開頭的第一列儲存記錄**資料錄集**。 當**儲存**方法完成後，目前的資料列位置移至第一個資料列**資料錄集**。  
  
 為獲得最佳結果，設定[CursorLocation 屬性 (ADO)](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性**adUseClient**與**儲存**。 如果您的提供者不支援的功能來儲存所需的所有**資料錄集**物件指標服務會提供該功能。  
  
 當**資料錄集**保存在一起**CursorLocation**屬性設定為**adUseServer**，更新功能**資料錄集**限制。 一般而言，只更新單一資料表、 插入和刪除允許 （取決於提供者功能）。 [重新同步處理方法](../../../ado/reference/ado-api/resync-method.md)方法也是在此組態中無法使用。  
  
> [!NOTE]
>  儲存**資料錄集**與**欄位**型別的**adVariant**， **adIDispatch**，或**adIUnknown**是不支援的 ADO，而且可能會導致無法預期的結果。  
  
 只會篩選條件字串的形式 (例如 OrderDate > ' 12/31/1999年 ') 會影響保存的內容**資料錄集**。 陣列建立的篩選**書籤**或使用中的值[FilterGroupEnum](../../../ado/reference/ado-api/filtergroupenum.md)將不會影響保存的內容**資料錄集**。 這些規則適用於**資料錄集**與用戶端或伺服器端資料指標建立。  
  
 因為*目的地*參數可以接受任何支援的 OLE DB IStream 介面的物件，您可以儲存**資料錄集**直接對 ASP 回應物件。 如需詳細資訊，請參閱**XML 資料錄集持續性案例**。  
  
 您也可以儲存**資料錄集**MSXML DOM 物件的執行個體的 XML 格式，為下列 Visual Basic 程式碼所示：  
  
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
>  以 XML 格式儲存階層式資料錄集 （資料圖案） 時，就會套用兩個限制。 如果無法儲存成 XML 階層式**資料錄集**包含擱置的更新，您不能以參數化的方式儲存和階層式**資料錄集**。  
  
 A**資料錄集**儲存在 XML 格式並儲存使用 utf-8 格式。 當這類檔案載入至 ADO 資料流時，資料流物件不會嘗試開啟**資料錄集**從資料流除非資料流的字元集屬性設定為 utf-8 格式的適當值。  
  
## <a name="applies-to"></a>適用於  
  
|||  
|-|-|  
|[資料錄集物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|[資料流物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)|  
  
## <a name="see-also"></a>另請參閱  
 [儲存並開啟方法的範例 (VB)](../../../ado/reference/ado-api/save-and-open-methods-example-vb.md)   
 [儲存並開啟方法的範例 （VC + +）](../../../ado/reference/ado-api/save-and-open-methods-example-vc.md)   
 [Open 方法 （ADO 資料錄集）](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Open 方法 （ADO 資料流）](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [SaveToFile 方法](../../../ado/reference/ado-api/savetofile-method.md)

