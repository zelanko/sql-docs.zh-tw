---
title: 深入了解資料錄集的持續性 |Microsoft Docs
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
ms.assetid: a9b287f5-04b0-4514-8143-f67879ca9842
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 88fcf471b2f853a5e1a874c29d2192c17d23b113
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66701951"
---
# <a name="more-about-recordset-persistence"></a>深入了解資料錄集的保存
ADO 資料錄集物件支援將儲存的內容**Recordset**使用檔案中的物件及其[儲存](../../../ado/reference/ado-api/save-method.md)方法。 持續儲存的檔案可能位於本機磁碟機，伺服器上，或做為 URL，在 Web 上站台。 更新版本中，還原檔案與[開放](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法**資料錄集**物件或[Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md)方法[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件。  
  
 颾魤 ㄛ [GetString](../../../ado/reference/ado-api/getstring-method-ado.md)方法將**資料錄集**至表單的資料行和資料列有您指定的字元所分隔的物件。  
  
 若要保存**資料錄集**，開始將它轉換成可以儲存在檔案中的表單。 **資料錄集**物件可以儲存在專屬的進階資料 TableGram (ADTG) 格式或開放式可延伸標記語言 (XML) 格式。 ADTG 範例會顯示在下一節。 如需有關 XML 持續性的詳細資訊，請參閱 <<c0> [ 保存的記錄，以 XML 格式](../../../ado/guide/data/persisting-records-in-xml-format.md)。  
  
 將任何暫止的變更儲存在保存的檔案中。 執行此動作可讓您發出的查詢會傳回**Recordset**物件、 編輯**資料錄集**儲存它，並暫止的變更，稍後再還原**資料錄集**，，然後更新資料來源，將儲存暫止的變更。  
  
 如需持續儲存資訊**Stream**物件，請參閱[資料流和保存](../../../ado/guide/data/streams-and-persistence.md)。  
  
 如需**資料錄集**持續性，請參閱 < XML 資料錄集保存案例。  
  
## <a name="example"></a>範例  
  
### <a name="save-a-recordset"></a>將儲存的資料錄集：  
  
```  
Dim rs as New ADODB.Recordset  
rs.Save "c:\yourFile.adtg", adPersistADTG  
```  
  
### <a name="open-a-persisted-file-with-recordsetopen"></a>開啟 Recordset.Open 保存的檔案：  
  
```  
Dim rs as New ADODB.Recordset  
rs.Open "c:\yourFile.adtg", "Provider=MSPersist",,,adCmdFile  
```  
  
 （選擇性） 如果**資料錄集**會沒有作用中連線，您可以接受所有預設值，並撰寫下列程式碼：  
  
```  
Dim rs as New ADODB.Recordset  
rs.Open "c:\yourFile.adtg"  
```  
  
### <a name="open-a-persisted-file-with-connectionexecute"></a>開啟 Connection.Execute 保存的檔案：  
  
```  
Dim conn as New ADODB.Connection  
Dim rs as ADODB.Recordset  
conn.Open "Provider=MSPersist"  
Set rs = conn.execute("c:\yourFile.adtg")  
```  
  
### <a name="open-a-persisted-file-with-rdsdatacontrol"></a>使用 RDS 開啟持續性的檔案DataControl:  
 在此情況下， **Server**屬性未設定。  
  
```  
Dim dc as New RDS.DataControl  
dc.Connection = "Provider=MSPersist"  
dc.SQL = "c:\yourFile.adtg"  
dc.Refresh  
```  
  
## <a name="see-also"></a>另請參閱  
 [GetString 方法 (ADO)](../../../ado/reference/ado-api/getstring-method-ado.md)   
 [Microsoft OLE DB 持續性提供者 （ADO 服務提供者）](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md)   
 [資料錄集物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [資料流和保存](../../../ado/guide/data/streams-and-persistence.md)
