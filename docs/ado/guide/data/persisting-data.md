---
title: 保存資料 |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 60b3a9e036bb199b72373055b299f262862a5d16
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759114"
---
# <a name="persisting-data"></a>保存資料
可攜的運算（例如，使用膝上型電腦）已產生應用程式的需求，這項功能可同時在連線和中斷連接的狀態下執行。 ADO 已藉由讓開發人員能夠將用戶端資料指標**記錄集**儲存至磁片，並于稍後重載，而增加了這項功能的支援。  
  
 在幾種情況下，您可以使用這種類型的功能，包括下列各項：  
  
-   **旅行：** 在路上進行應用程式時，請務必提供進行變更的能力，並加入新的記錄，稍後再重新連接到資料庫並加以認可。  
  
-   不**常更新的查閱：** 在應用程式中，通常會使用資料表作為查閱，例如，州稅資料表。 它們不常更新，而且是唯讀的。 應用程式不會在每次啟動應用程式時從伺服器重新讀取這項資料，而是直接從本機保存的**記錄集**載入資料。  
  
 在 ADO 中，若要儲存和載入**記錄集**，請使用**記錄集。儲存**和記錄集。在 ado**記錄集**物件上**開啟（,,,, adCmdFile）** 方法。  
  
 您可以使用**記錄集儲存**方法，將 ADO**記錄集**保存到磁片上的檔案。 （您也可以將**記錄集**儲存至 ADO**資料流程**物件。 本指南稍後會討論**資料流程**物件）。之後，當您準備好要使用時，可以使用**Open**方法重新開啟**記錄集**。 根據預設，ADO 會將**記錄集**儲存為專屬的 Microsoft Advanced Data TABLEGRAM （ADTG）格式。 此二進位格式是使用**AdPersistADTG PersistFormatEnum**值所指定。 或者，您也可以選擇使用**adPersistXML**，將您的**記錄集**儲存為 XML。 如需將記錄集儲存為 XML 的詳細資訊，請參閱[以 Xml 格式保存記錄](../../../ado/guide/data/persisting-records-in-xml-format.md)。  
  
 **Save**方法的語法如下：  
  
```  
  
recordset.  
Save  
Destination, PersistFormat  
  
```  
  
 第一次儲存**記錄集**時，可以選擇是否要指定*目的地*。 如果您省略*目的地*，將會建立新的檔案，並將名稱設定為**記錄集**之[Source](../../../ado/reference/ado-api/source-property-ado-recordset.md)屬性的值。  
  
 當您在第一次儲存後呼叫 [**儲存**] 時省略*目的地*，否則會發生執行階段錯誤。 如果您隨後使用新的*目的地*呼叫 [**儲存**]，則會將**記錄集**儲存至新的目的地。 不過，新的目的地和原始目的地皆會開啟。  
  
 [**儲存**] 不會關閉**記錄集**或*目的地*，因此您可以繼續使用**記錄集**，並儲存最新的變更。 *目的地*會保持開啟狀態，直到**記錄集**關閉為止，在這段期間，其他應用程式可以讀取但不能寫入*目的地*。  
  
 基於安全性的理由， **Save**方法只允許從 Microsoft Internet Explorer 所執行的腳本使用低和自訂安全性設定。  
  
 如果在非同步作業**記錄**檔提取、執行或更新作業正在進行時呼叫**save**方法，請**儲存**等候，直到非同步作業完成為止。  
  
 記錄會從**記錄集**的第一個資料列開始儲存。 當**Save**方法完成時，目前的資料列位置會移到**記錄集**的第一個資料列。  
  
 為獲得最佳結果，請將[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性設定為 [ **adUseClient** ]，並使用 [**儲存**]。 如果您的提供者不支援儲存**記錄集**物件所需的所有功能，則資料指標服務會提供該功能。  
  
 當**記錄**集保存並將**CursorLocation**屬性設定為**adUseServer**時，**記錄集**的更新功能會受到限制。 一般來說，只允許單一資料表的更新、插入和刪除（相依于提供者功能）。 此設定中也無法使用重新[同步](../../../ado/reference/ado-api/resync-method.md)處理方法。  
  
 因為*Destination*參數可以接受任何支援 OLE DB **IStream**介面的物件，所以您可以將**記錄集**直接儲存到 ASP **Response**物件。  
  
 在下列範例中，會使用**Save**和**Open**方法來保存**記錄集**，並于稍後重新開啟它：  
  
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
