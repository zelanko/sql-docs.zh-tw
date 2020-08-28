---
description: 以 XML 格式保存記錄
title: 以 XML 格式保存記錄 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- persisting data [ADO]
- data updates [ADO], persisting data
- data persistence [ADO]
- XML persistence [ADO]
- updating data [ADO], persisting data
ms.assetid: f3113ec4-ae31-428f-89c6-bc1024f128ea
author: rothja
ms.author: jroth
ms.openlocfilehash: 31512fd9843ae5ff15fc2f7c6981fccdc926dbb5
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88980059"
---
# <a name="persisting-records-in-xml-format"></a>以 XML 格式保存記錄
如同 ADTG 格式一樣，XML 格式的 **記錄集** 持續性是以 Microsoft OLE DB 持續性提供者來執行。 此提供者會從儲存的 XML 檔案或資料流程產生順向唯讀資料列集，其中包含 ADO 所產生的架構資訊。 同樣地，它可以採用 ADO **記錄集**、產生 XML，然後將它儲存到檔案或任何實作為 COM **IStream** 介面的物件。  (事實上，檔案只是另一個支援 **IStream**) . 2.5 和更新版本的物件範例，ADO 依賴 Microsoft XML 剖析器 (MSXML) 將 XML 載入到 **記錄集**;因此 msxml.dll 是必要的。  
  
> [!NOTE]
>  將階層式 **記錄集** 儲存 (資料圖形) 為 XML 格式時，會有一些限制。 如果階層式 **記錄集** 包含暫止的更新，而您無法儲存參數化階層式 **記錄集**，則無法儲存至 XML。 如需詳細資訊，請參閱 [保存已篩選和階層式記錄集](../../../ado/guide/data/persisting-filtered-and-hierarchical-recordsets.md)。  
  
 最簡單的方式是將資料保存成 XML，並將它重新載入至 ADO，以分別使用 **Save** 和 **Open** 方法。 下列 ADO 程式碼範例示範如何將 **titles** 資料表中的資料儲存至名為 sav 的檔案。  
  
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
  
 ADO 一律會保存整個 **記錄集** 物件。 如果您想要保存 **記錄集** 物件的資料列子集，請使用 **篩選** 方法來縮小資料列的範圍，或變更您的選取子句。 不過，您必須使用用戶端資料指標開啟**記錄集**物件 (**CursorLocation**  =  **adUseClient**) ，才能使用**篩選**方法來儲存資料列的子集。 例如，若要取出以字母 "b" 開頭的標題，您可以將篩選套用至開啟的 **記錄集** 物件：  
  
```  
rs.Filter "title_id like 'B*'"  
rs.Save "btitles.sav", adPersistXML  
```  
  
 ADO 一律會使用用戶端資料指標引擎資料列集，在持續性提供者所產生的順向資料之上產生可滾動的 bookmarkable **記錄集** 物件。  
  
 此章節包含下列主題。  
  
-   [XML 保存格式](../../../ado/guide/data/xml-persistence-format.md)  
  
-   [命名空間](../../../ado/guide/data/namespaces.md)  
  
-   [結構描述區段](../../../ado/guide/data/schema-section.md)  
  
-   [資料區段](../../../ado/guide/data/data-section.md)  
  
-   [XML 中的階層式資料錄集](../../../ado/guide/data/hierarchical-recordsets-in-xml.md)  
  
-   [XML 中的資料錄集動態屬性](../../../ado/guide/data/recordset-dynamic-properties-in-xml.md)  
  
-   [XSLT 轉換](../../../ado/guide/data/xslt-transformations.md)  
  
-   [儲存到 XML DOM 物件](../../../ado/guide/data/saving-to-the-xml-dom-object.md)  
  
-   [XML 安全性考量](../../../ado/guide/data/xml-security-considerations.md)  
  
-   [XML 資料錄集保存案例](../../../ado/guide/data/xml-recordset-persistence-scenario.md)
