---
description: Save 方法
title: Save 方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 4ffd13c07fad10d4b0386d342a6ddcbec37256da
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88989329"
---
# <a name="save-method"></a>Save 方法
將 [記錄集](./recordset-object-ado.md) 儲存在檔案或 [資料流程](./stream-object-ado.md) 物件中。  
  
## <a name="syntax"></a>語法  
  
```  
  
recordset.Save Destination, PersistFormat  
```  
  
#### <a name="parameters"></a>參數  
 *目的地*  
 選擇性。 **Variant** ，代表要儲存**記錄集**之檔案的完整路徑名稱，或是**資料流程**物件的參考。  
  
 *PersistFormat*  
 選擇性。 [PersistFormatEnum](./persistformatenum.md)值，指定要將**記錄集**儲存 (XML 或 ADTG) 的格式。 預設值為 **adPersistADTG**。  
  
## <a name="remarks"></a>備註  
 [Save 方法]()方法只能在開啟的**記錄集**上叫用。 使用[開放式方法 (ADO 記錄集) ](./open-method-ado-recordset.md)方法，稍後從*目的地*還原**記錄集**。  
  
 如果 [ [篩選] 屬性](./filter-property.md) 屬性對 **記錄集**有效，則只會儲存篩選下的可存取資料列。 如果 **記錄集** 是階層式的，則會儲存目前的子 **記錄集** 和其子系，包括父 **記錄集**。 如果呼叫子 **記錄集** 的 Save 方法，則會儲存子系及其所有子系，但父系則否。  
  
 當您第一次儲存 **記錄集**時，可以選擇是否要指定 *目的地*。 如果您省略 [ *目的地*]，將會建立新的檔案，並將名稱設定為 **記錄集**之 Source 屬性的值。  
  
 當您在第一次儲存之後呼叫 [**儲存**] 之後，請省略*目的地*，否則會發生執行階段錯誤。 如果您之後以新的*目的地*呼叫 [**儲存**]，**記錄集會**儲存至新的目的地。 不過，新的目的地和原始目的地都將開啟。  
  
 [**儲存**] 並不會關閉**記錄集**或*目的地*，因此您可以繼續使用**記錄集**，並儲存最近的變更。 *目的地* 會保持開啟，直到 **記錄集** 關閉為止。  
  
 基於安全性的理由， **Save** 方法只允許從 Microsoft Internet Explorer 所執行的腳本使用低和自訂安全性設定。  
  
 如果在非同步**記錄集**提取、執行或更新作業正在進行時呼叫**Save**方法，請**儲存**等候，直到非同步作業完成為止。  
  
 記錄是從 **記錄集**的第一個資料列開始儲存。 當 **Save** 方法完成時，會將目前的資料列位置移到 **記錄集**的第一個資料列。  
  
 為了獲得最佳結果，請將 [CursorLocation 屬性 (ADO) ](./cursorlocation-property-ado.md) 屬性設定為 **adUseClient** with **Save**。 如果您的提供者不支援儲存 **記錄集** 物件所需的所有功能，則資料指標服務會提供該功能。  
  
 當 **記錄** 集在 **CursorLocation** 屬性設定為 **AdUseServer**時保存時， **記錄集** 的更新功能會受到限制。 一般來說，只允許單一資料表的更新、插入和刪除 (相依于) 提供者功能。 這項設定也無法使用 [Resync 方法](./resync-method.md) 方法。  
  
> [!NOTE]
>  ADO 不支援儲存具有**adVariant**、 **adIDispatch**或**AdIUnknown**類型**欄位**的**記錄集**，而且可能會導致無法預期的結果。  
  
 只有準則字串形式的篩選 (例如，日期記錄 > ' 12/31/1999 ' ) 會影響保存的 **記錄集**的內容。 使用 **書簽** 陣列建立的篩選準則，或使用 [FilterGroupEnum](./filtergroupenum.md) 中的值，將不會影響保存 **記錄集**的內容。 這些規則適用于使用用戶端或伺服器端資料指標所建立的 **記錄集**。  
  
 因為 *Destination* 參數可以接受支援 OLE DB IStream 介面的任何物件，所以您可以將 **記錄集** 直接儲存至 ASP 回應物件。 如需詳細資訊，請參閱 **XML 記錄集持續性案例**。  
  
 您也可以將 XML 格式的 **記錄集** 儲存到 MSXML DOM 物件的實例，如下列 Visual Basic 程式碼所示：  
  
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
>  將階層式記錄集儲存 (資料圖形) 為 XML 格式時，適用兩項限制。 如果階層式 **記錄集** 包含暫止的更新，而您無法儲存參數化階層式 **記錄集**，則無法儲存至 XML。  
  
 以 XML 格式儲存的 **記錄集會** 使用 utf-8 格式儲存。 當這類檔案載入至 ADO 資料流程時，除非資料流程的字元集屬性設定為適用于 UTF-8 格式的值，否則 Stream 物件不會嘗試從資料流程開啟 **記錄集** 。  
  
## <a name="applies-to"></a>套用至  

:::row:::
    :::column:::
        [Recordset 物件 (ADO)](./recordset-object-ado.md)  
    :::column-end:::
    :::column:::
        [Stream 物件 (ADO)](./stream-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>另請參閱  
 [ (VB) 的儲存和開啟方法範例 ](./save-and-open-methods-example-vb.md)   
 [Save 和 Open 方法範例 (VC + +) ](./save-and-open-methods-example-vc.md)   
 [ (ADO 記錄集的 Open 方法) ](./open-method-ado-recordset.md)   
 [ (ADO Stream 的 Open 方法) ](./open-method-ado-stream.md)   
 [SaveToFile 方法](./savetofile-method.md)