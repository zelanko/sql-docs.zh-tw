---
title: 保存的資料 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- persisting data [ADO]
- data updates [ADO], persisting data
- data persistence [ADO]
- updating data [ADO], persisting data
ms.assetid: 21c162ca-2845-4dd8-a49d-e715aba8c461
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 0f2d47229b7383c11740ca3d7a20ad8e420931a5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66700481"
---
# <a name="persisting-data"></a>保存資料
可攜式電腦運算 （例如，使用膝上型電腦），已產生可以在連線或中斷連線的狀態下執行的應用程式的需求。 ADO 已新增這個的支援，讓開發人員能夠儲存用戶端資料指標**資料錄集**到磁碟，稍後再重新載入它。  
  
 有幾種的情況中，您可以使用這種類型的功能，包括下列：  
  
-   **傳輸：** 外出應用程式時，務必提供能夠進行變更，並新增新的記錄，則可以稍後重新連線到資料庫和認可。  
  
-   **不常更新的查閱：** 通常應用程式中，資料表做為查閱-例如，州稅資料表。 它們不常更新，並處於唯讀狀態。 而非重新讀取來自伺服器的此資料每次啟動應用程式時，應用程式可以直接將資料從載入本機保存**資料錄集**。  
  
 在 ADO 中，來儲存及載入**資料錄集**，使用**Recordset.Save**並**Recordset.Open(,,,adCmdFile)** ado 方法**資料錄集**物件。  
  
 您可以使用**錄儲存**方法，將您的 ADO**資料錄集**磁碟上的檔案。 (您也可以儲存**Recordset** ado **Stream**物件。 **Stream**稍後本指南會討論物件。)稍後，您可以使用**開放**方法來重新開啟**資料錄集**當您準備好使用它。 根據預設，儲存 ADO**資料錄集**的專屬的 Microsoft 進階資料 TableGram (ADTG) 格式。 使用指定此二進位格式**adPersistADTG PersistFormatEnum**值。 或者，您可以選擇儲存您**Recordset**改為使用 XML 作為**adPersistXML**。 如需將資料錄集儲存為 XML 的詳細資訊，請參閱[保存的記錄，以 XML 格式](../../../ado/guide/data/persisting-records-in-xml-format.md)。  
  
 語法**儲存**方法如下所示：  
  
```  
  
recordset.  
Save  
Destination, PersistFormat  
  
```  
  
 第一次您儲存**Recordset**，選擇性地指定*目的地*。 如果您省略*目的地*，將會設定為值的名稱建立新的檔案[來源](../../../ado/reference/ado-api/source-property-ado-recordset.md)屬性**資料錄集**。  
  
 省略*目的地*當您後續呼叫**儲存**之後會發生第一次儲存或執行階段錯誤。 如果您後續呼叫**儲存**的新*目的地*，則**資料錄集**儲存到新的目的地。 不過，新的目的地和原始目的地將會同時開啟。  
  
 **儲存**不會關閉**Recordset**或*目的地*，因此您可以繼續使用**資料錄集**並儲存您最新的變更。 *目的地*保持開啟，直到**Recordset**已關閉，在這段期間，其他應用程式可以讀取但不是能寫入*目的地*。  
  
 基於安全性，原因**儲存**方法允許只使用執行 Microsoft Internet explorer 的指令碼的低和自訂安全性設定。  
  
 如果**儲存**時的非同步呼叫方法**Recordset**提取、 執行，或更新作業正在進行中，**儲存**會等到非同步作業完成。  
  
 記錄會儲存開頭的第一個資料列**資料錄集**。 當**儲存**方法執行完成後，目前的資料列位置移至第一個資料列**資料錄集**。  
  
 為了獲得最佳結果，請設定[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性設**adUseClient**具有**儲存**。 如果您的提供者不支援的功能來儲存所需的所有**資料錄集**物件，資料指標服務會提供該功能。  
  
 當**資料錄集**與一起保存**CursorLocation**屬性設定為**adUseServer**，更新功能，如**資料錄集**限制。 一般而言，只有單一資料表更新、 插入和刪除允許 （取決於提供者功能）。 [Resync](../../../ado/reference/ado-api/resync-method.md)方法也會在此組態中無法使用。  
  
 因為*目的地*參數可以接受任何支援的 OLE DB 的物件**IStream**介面，您可以將已儲存**資料錄集**直接與 ASP **回應**物件。  
  
 在下列範例中，**儲存**並**開放**方法用來保存**資料錄集**並稍後再重新開啟它：  
  
```  
'BeginPersist  
   conn.ConnectionString = _  
   "Provider=SQLOLEDB;Data Source=MySQLServer;" _  
      & "Integrated Security=SSPI;Initial Catalog=pubs"  
   conn.Open  
  
   conn.Execute "create table testtable (dbkey int " & _  
      "primary key, field1 char(10))"  
   conn.Execute "insert into testtable values (1, 'string1')"  
  
   Set rst.ActiveConnection = conn  
   rst.CursorLocation = adUseClient  
  
   rst.Open "select * from testtable", conn, adOpenStatic, _  
      adLockBatchOptimistic  
  
   'Change the row on the client  
   rst!field1 = "NewValue"  
  
   'Save to a file--the .dat extension is an example; choose  
   'your own extension. The changes will be saved in the file  
   'as well as the original data.  
   MyFile = Dir("c:\temp\temptbl.dat")  
   If MyFile <> "" Then  
       Kill "c:\temp\temptbl.dat"  
   End If  
  
   rst.Save "c:\temp\temptbl.dat", adPersistADTG  
   Set rst = Nothing  
  
   'Now reload the data from the file  
   Set rst = New ADODB.Recordset  
   rst.Open "c:\temp\temptbl.dat", , adOpenStatic, _  
      adLockBatchOptimistic, adCmdFile  
  
   Debug.Print "After Loading the file from disk"  
   Debug.Print "   Current Edited Value: " & rst!field1.Value  
   Debug.Print "   Value Before Editing: " & rst!field1.OriginalValue  
  
   'Note that you can reconnect to a connection and  
   'submit the changes to the data source  
   Set rst.ActiveConnection = conn  
   rst.UpdateBatch  
'EndPersist  
```  
  
## <a name="remarks"></a>備註  
 此章節包含下列主題。  
  
-   [深入了解資料錄集的保存](../../../ado/guide/data/more-about-recordset-persistence.md)  
  
-   [保存篩選過的階層式資料錄集](../../../ado/guide/data/persisting-filtered-and-hierarchical-recordsets.md)  
  
-   [以 XML 格式保存記錄](../../../ado/guide/data/persisting-records-in-xml-format.md)
