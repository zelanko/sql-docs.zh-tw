---
description: 深入了解資料錄集的保存
title: 深入瞭解記錄集持續性 |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: ceeb9abb3b14441e6f0e8194d07836cf5d482492
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453180"
---
# <a name="more-about-recordset-persistence"></a>深入了解資料錄集的保存
ADO 記錄集物件支援使用[儲存方法，](../../../ado/reference/ado-api/save-method.md)將**記錄集**物件的內容儲存在檔案中。 持續儲存的檔案可能會存在於本機磁片磁碟機、伺服器或網站上的 URL。 之後，可以使用**記錄集**物件的[Open](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法或[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件的[Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md)方法來還原檔案。  
  
 此外， [GetString](../../../ado/reference/ado-api/getstring-method-ado.md) 方法會將 **記錄集** 物件轉換成表單，其中的資料行和資料列會以您指定的字元分隔。  
  
 若要保存 **記錄集**，請先將它轉換成可儲存在檔案中的表單。 您可以將**記錄集**物件儲存在專屬的 Advanced Data TABLEGRAM (ADTG) 格式或 open 可延伸標記語言 (XML)  (XML) 格式。 下一節會顯示 ADTG 範例。 如需 XML 持續性的詳細資訊，請參閱 [以 xml 格式保存記錄](../../../ado/guide/data/persisting-records-in-xml-format.md)。  
  
 將任何暫止的變更儲存在保存檔案中。 這樣做可讓您發出查詢來傳回 **記錄集** 物件、編輯 **記錄集**、儲存記錄和暫止的變更、稍後還原 **記錄集**，然後以儲存的暫止變更來更新資料來源。  
  
 如需持續儲存 **資料流程** 物件的詳細資訊，請參閱 [資料流程和持續](../../../ado/guide/data/streams-and-persistence.md)性。  
  
 如需 **記錄集** 持續性的範例，請參閱 XML 記錄集持續性案例。  
  
## <a name="example"></a>範例  
  
### <a name="save-a-recordset"></a>儲存記錄集：  
  
```  
Dim rs as New ADODB.Recordset  
rs.Save "c:\yourFile.adtg", adPersistADTG  
```  
  
### <a name="open-a-persisted-file-with-recordsetopen"></a>開啟包含記錄集的保存檔案。開啟：  
  
```  
Dim rs as New ADODB.Recordset  
rs.Open "c:\yourFile.adtg", "Provider=MSPersist",,,adCmdFile  
```  
  
 （選擇性）如果 **記錄集** 沒有使用中的連接，您可以接受所有預設值，並撰寫下列程式碼：  
  
```  
Dim rs as New ADODB.Recordset  
rs.Open "c:\yourFile.adtg"  
```  
  
### <a name="open-a-persisted-file-with-connectionexecute"></a>Connection.Exe刻意開啟保存的檔案：  
  
```  
Dim conn as New ADODB.Connection  
Dim rs as ADODB.Recordset  
conn.Open "Provider=MSPersist"  
Set rs = conn.execute("c:\yourFile.adtg")  
```  
  
### <a name="open-a-persisted-file-with-rdsdatacontrol"></a>使用 RDS 開啟保存的檔案。DataControl  
 在此情況下，不會設定 **伺服器** 屬性。  
  
```  
Dim dc as New RDS.DataControl  
dc.Connection = "Provider=MSPersist"  
dc.SQL = "c:\yourFile.adtg"  
dc.Refresh  
```  
  
## <a name="see-also"></a>另請參閱  
 [ (ADO) 的 GetString 方法 ](../../../ado/reference/ado-api/getstring-method-ado.md)   
 [Microsoft OLE DB 持續性提供者 (ADO 服務提供者) ](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md)   
 [ (ADO) 的記錄集物件 ](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [資料流和保存](../../../ado/guide/data/streams-and-persistence.md)
