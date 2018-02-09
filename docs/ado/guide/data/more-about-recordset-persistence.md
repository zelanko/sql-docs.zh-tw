---
title: "深入了解資料錄集持續性 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
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
- updating data [ADO], persisting data
ms.assetid: a9b287f5-04b0-4514-8143-f67879ca9842
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c5dedcc3c1326c8b71844637c24f81835472ae9e
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="more-about-recordset-persistence"></a>深入了解資料錄集持續性
ADO 資料錄集物件支援儲存內容**資料錄集**使用檔案中的物件及其[儲存](../../../ado/reference/ado-api/save-method.md)方法。 持續儲存的檔案可能存在於本機磁碟機，伺服器，或做為 URL 在 Web 上站台。 更新版本中，還原檔案，其中一種[開啟](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法**資料錄集**物件或[Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md)方法[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件。  
  
 此外， [GetString](../../../ado/reference/ado-api/getstring-method-ado.md)方法轉換**資料錄集**表單中的資料行和資料列會以您指定的字元分隔的物件。  
  
 保存**資料錄集**，開始將它轉換成可儲存在檔案中的表單。 **資料錄集**物件可以儲存在專屬的進階資料 TableGram (ADTG) 格式或開啟的可延伸標記語言 (XML) 格式。 ADTG 範例會顯示在下一節。 如需有關 XML 持續性的詳細資訊，請參閱[XML 格式保存記錄](../../../ado/guide/data/persisting-records-in-xml-format.md)。  
  
 將任何暫止變更儲存在保存檔案。 這樣做可讓您發出查詢，傳回**資料錄集**物件、 編輯**資料錄集**、 將它與暫止的變更儲存、 稍後還原**資料錄集**，然後按一下更新資料來源，將儲存暫止的變更。  
  
 如需持續儲存資訊**資料流**物件，請參閱[資料流和持續性](../../../ado/guide/data/streams-and-persistence.md)。  
  
 如需**資料錄集**持續性，請參閱 < XML 資料錄集持續性案例。  
  
## <a name="example"></a>範例  
  
### <a name="save-a-recordset"></a>儲存資料錄集：  
  
```  
Dim rs as New ADODB.Recordset  
rs.Save "c:\yourFile.adtg", adPersistADTG  
```  
  
### <a name="open-a-persisted-file-with-recordsetopen"></a>開啟 Recordset.Open 保存的檔：  
  
```  
Dim rs as New ADODB.Recordset  
rs.Open "c:\yourFile.adtg", "Provider=MSPersist",,,adCmdFile  
```  
  
 （選擇性） 如果**資料錄集**並沒有作用中連線，您可以接受所有預設值，並在下列程式碼：  
  
```  
Dim rs as New ADODB.Recordset  
rs.Open "c:\yourFile.adtg"  
```  
  
### <a name="open-a-persisted-file-with-connectionexecute"></a>開啟 Connection.Execute 保存的檔：  
  
```  
Dim conn as New ADODB.Connection  
Dim rs as ADODB.Recordset  
conn.Open "Provider=MSPersist"  
Set rs = conn.execute("c:\yourFile.adtg")  
```  
  
### <a name="open-a-persisted-file-with-rdsdatacontrol"></a>開啟.rds 之保存的檔案DataControl:  
 在此情況下，**伺服器**屬性未設定。  
  
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
