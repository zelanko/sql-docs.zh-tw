---
title: "以 XML 格式保存記錄 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
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
- XML persistence [ADO]
- updating data [ADO], persisting data
ms.assetid: f3113ec4-ae31-428f-89c6-bc1024f128ea
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a45c434bdcf551e97eb97f85997ab73c883b599c
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="persisting-records-in-xml-format"></a>以 XML 格式保存記錄
ADTG 格式，例如**資料錄集**持續性 XML 格式使用 Microsoft OLE DB 持續性提供者實作。 此提供者會從已儲存的 XML 檔案或資料流，包含 ADO 所產生的結構描述資訊產生的順向、 唯讀資料列集。 同樣地，可能需要 ADO**資料錄集**、 產生的 XML，並將它儲存到檔案或任何物件實作 COM **IStream**介面。 (事實上，檔案是支援的物件只是另一個範例**IStream**。)版本 2.5 和更新版本中，針對 ADO 會依賴上 Microsoft XML Parser (MSXML) 來將 XML 載入**資料錄集**; 因此 msxml.dll 是必要。  
  
> [!NOTE]
>  儲存階層式時，某些限制適用於**資料錄集**（資料圖形） 為 XML 格式。 如果無法儲存到 XML 階層式**資料錄集**包含擱置的更新，您不能以參數化的方式儲存和階層式**資料錄集**。 如需詳細資訊，請參閱[保存篩選和階層式資料錄集](../../../ado/guide/data/persisting-filtered-and-hierarchical-recordsets.md)。  
  
 最簡單的方式將資料保存在 XML，並將其重新載入一次透過 ADO 是與**儲存**和**開啟**方法，分別。 下列的 ADO 程式碼範例示範儲存中的資料**標題**titles.sav 名為檔案資料表。  
  
```  
Dim rs as new Recordset  
Dim rs2 as new Recordset  
Dim c as new Connection  
Dim s as new Stream  
  
' Query the Titles table.  
c.Open "provider=sqloledb;data source=MySQLServer;initial catalog=pubs;Integrated Security='SSPI'"  
rs.cursorlocation = adUseClient  
rs.Open "select * from titles", c, adOpenStatic  
  
' Save to the file in the XML format. Note that if you don't specify   
' adPersistXML, a binary format (ADTG) will be used by default.  
rs.Save "titles.sav", adPersistXML  
  
' Save the recordset into the ADO Stream object.  
rs.save s, adPersistXML  
rs.Close  
c.Close  
  
set rs = nothing  
  
' Reopen the file.  
rs.Open "titles.sav",,,,adCmdFile  
' Open the Stream back into a Recordset.  
rs2.open s  
```  
  
 ADO 永遠保存整個**資料錄集**物件。 如果您想要保存的資料列的子集**資料錄集**物件，請使用**篩選**方法，以縮小資料列，或變更您的選取範圍子句。 不過，您必須開啟**資料錄集**物件與用戶端資料指標 (**CursorLocation** = **adUseClient**) 使用**篩選**方法來儲存資料列的子集。 例如，若要擷取以字母"b"開頭的項目，您可以套用篩選來開啟**資料錄集**物件：  
  
```  
rs.Filter "title_id like 'B*'"  
rs.Save "btitles.sav", adPersistXML  
```  
  
 ADO 永遠使用用戶端資料指標引擎的資料列集來產生可捲動 bookmarkable**資料錄集**之上順向的資料持續性提供者所產生的物件。  
  
 此章節包含下列主題。  
  
-   [XML 持續性格式](../../../ado/guide/data/xml-persistence-format.md)  
  
-   [命名空間](../../../ado/guide/data/namespaces.md)  
  
-   [結構描述 > 一節](../../../ado/guide/data/schema-section.md)  
  
-   [資料區段](../../../ado/guide/data/data-section.md)  
  
-   [在 XML 中的階層式資料錄集](../../../ado/guide/data/hierarchical-recordsets-in-xml.md)  
  
-   [在 XML 中的資料錄集的動態內容](../../../ado/guide/data/recordset-dynamic-properties-in-xml.md)  
  
-   [XSLT 轉換](../../../ado/guide/data/xslt-transformations.md)  
  
-   [儲存到 XML DOM 物件](../../../ado/guide/data/saving-to-the-xml-dom-object.md)  
  
-   [XML 安全性考量](../../../ado/guide/data/xml-security-considerations.md)  
  
-   [持續性案例中 XML 資料錄集](../../../ado/guide/data/xml-recordset-persistence-scenario.md)

