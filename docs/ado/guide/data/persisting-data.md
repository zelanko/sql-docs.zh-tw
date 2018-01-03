---
title: "保存資料 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- persisting data [ADO]
- data updates [ADO], persisting data
- data persistence [ADO]
- updating data [ADO], persisting data
ms.assetid: 21c162ca-2845-4dd8-a49d-e715aba8c461
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ddcd99ce0c8b59cff252f2e1aa5cf97696298cc5
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="persisting-data"></a>保存資料
可攜式電腦 （例如，使用膝上型電腦） 已產生可以在連線或中斷連線狀態中執行的應用程式的需求。 ADO 已新增對此支援，讓開發人員能夠儲存用戶端資料指標**資料錄集**至磁碟，並稍後重新載入它。  
  
 有幾種的情況中，您可以使用這種類型的功能，包括下列：  
  
-   **出差：**旅進行應用程式，務必提供了可進行變更，並加入新的記錄，然後可以稍後重新連線到資料庫並認可。  
  
-   **不常更新查閱：**通常應用程式中，資料表做為查閱 — 例如，狀態稅資料表。 它們不常更新，且處於唯讀狀態。 而不是這項資料從伺服器重新讀取每次啟動應用程式時，應用程式可以直接將資料載入本機保存從**資料錄集**。  
  
 在 ADO 中，來儲存及載入**資料錄集**，使用**Recordset.Save**和**Recordset.Open(,,,adCmdFile)**方法上之 ADO**資料錄集**物件。  
  
 您可以使用**資料錄集儲存**方法，將您的 ADO**資料錄集**至磁碟上的檔案。 (您也可以儲存**資料錄集**至 ADO**資料流**物件。 **資料流**本指南稍後會討論的物件。)稍後，您可以使用**開啟**方法，以重新開啟**資料錄集**當您準備好使用它。 根據預設，儲存 ADO**資料錄集**成專屬 Microsoft 進階資料 TableGram (ADTG) 格式。 使用指定此二進位格式**adPersistADTG PersistFormatEnum**值。 或者，您可以選擇要儲存您**資料錄集**出為 XML，而非使用**adPersistXML**。 如需有關儲存為 XML 資料錄集的詳細資訊，請參閱[XML 格式保存記錄](../../../ado/guide/data/persisting-records-in-xml-format.md)。  
  
 語法**儲存**方法如下所示：  
  
```  
  
recordset.  
Save  
Destination, PersistFormat  
  
```  
  
 第一次儲存**資料錄集**，則可以指定選擇性*目的地*。 如果您省略*目的地*，將會使用設定為值的名稱建立新檔案[來源](../../../ado/reference/ado-api/source-property-ado-recordset.md)屬性**資料錄集**。  
  
 省略*目的地*當您後續呼叫**儲存**第一次儲存或執行階段錯誤發生之後。 如果您後續呼叫**儲存**與新*目的地*、**資料錄集**儲存至新的目的地。 不過，新的目的地和的原始目的端會同時為開啟。  
  
 **儲存**不會關閉**資料錄集**或*目的地*，因此您可以繼續使用**資料錄集**並儲存最新變更。 *目的地*維持開啟直到**資料錄集**已關閉，請在這段期間，其他應用程式可以讀取但無法寫入*目的地*。  
  
 基於安全性，**儲存**方法允許只使用執行 Microsoft Internet explorer 的指令碼的低和自訂安全性設定。  
  
 如果**儲存**時的非同步呼叫方法**資料錄集**擷取、 執行、 或更新作業正在進行中，**儲存**等到非同步作業完成。  
  
 開頭的第一列儲存記錄**資料錄集**。 當**儲存**方法完成後，目前的資料列位置移至第一個資料列**資料錄集**。  
  
 為獲得最佳結果，設定[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性**adUseClient**與**儲存**。 如果您的提供者不支援的功能來儲存所需的所有**資料錄集**物件指標服務會提供該功能。  
  
 當**資料錄集**保存在一起**CursorLocation**屬性設定為**adUseServer**，更新功能**資料錄集**限制。 一般而言，只更新單一資料表、 插入和刪除允許 （取決於提供者功能）。 [重新同步處理](../../../ado/reference/ado-api/resync-method.md)方法也是在此組態中無法使用。  
  
 因為*目的地*參數可以接受支援的 OLE DB 的任何物件**IStream**介面，您可以儲存**資料錄集**直接為 ASP **回應**物件。  
  
 在下列範例中，**儲存**和**開啟**方法用來保存**資料錄集**並稍後重新開啟它：  
  
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
