---
title: 以 XML 格式保存記錄 |Microsoft Docs
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
- XML persistence [ADO]
- updating data [ADO], persisting data
ms.assetid: f3113ec4-ae31-428f-89c6-bc1024f128ea
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 263f83093c46f4265559fe0b1844112687d4fc67
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924598"
---
# <a name="persisting-records-in-xml-format"></a>以 XML 格式保存記錄
ADTG 格式類似**資料錄集**以 XML 格式的持續性透過 Microsoft OLE DB 持續性提供者實作。 此提供者會從已儲存的 XML 檔案或資料流，包含由 ADO 所產生的結構描述資訊產生順向且唯讀的資料列集。 同樣地，可能需要 ADO **Recordset**，產生的 XML，並將它儲存到檔案或任何可實作 COM 物件**IStream**介面。 (事實上，檔案是另一個例子是支援的物件**IStream**。)如需版本 2.5 及更新版本，ADO 需要在 Microsoft XML Parser (MSXML) 載入到 XML**資料錄集**; 因此 msxml.dll 不需要。  
  
> [!NOTE]
>  儲存階層式時，適用某些限制**資料錄集**（資料圖形） 的 XML 格式。 如果無法儲存到 XML 階層**資料錄集**包含擱置的更新，您不能以參數化的方式儲存和階層式**資料錄集**。 如需詳細資訊，請參閱 <<c0> [ 保存篩選和階層式資料錄集](../../../ado/guide/data/persisting-filtered-and-hierarchical-recordsets.md)。  
  
 最簡單的方式，將資料保存到 XML，並將其載入到上一步一次透過 ADO 是與**儲存**並**開啟**方法，分別。 下列的 ADO 程式碼範例示範儲存中的資料**標題**檔案，稱為 titles.sav 的資料表。  
  
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
  
 ADO 永遠保存整個**資料錄集**物件。 如果您想要保存的資料列的子集**Recordset**物件，請使用**篩選**方法，以縮小資料列，或變更您的選取範圍子句。 不過，您必須開啟**Recordset**與用戶端資料指標的物件 (**CursorLocation** = **adUseClient**) 使用**篩選**方法來儲存資料列的子集。 例如，若要擷取以字母"b"開頭的項目，您可以套用篩選來開啟**資料錄集**物件：  
  
```  
rs.Filter "title_id like 'B*'"  
rs.Save "btitles.sav", adPersistXML  
```  
  
 ADO 一律使用用戶端資料指標引擎的資料列集，來產生可捲動 bookmarkable**資料錄集**根據順向的資料持續性提供者所產生的物件。  
  
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
