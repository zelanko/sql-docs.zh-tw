---
title: 步驟 6：變更傳送到伺服器 （RDS 教學課程） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO], changes sent to server
ms.assetid: b1e927d6-7d50-4978-9eef-045043cdce7a
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: fa60fd6db3da59de9d833c488811b5921ae53987
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66699309"
---
# <a name="step-6-changes-are-sent-to-the-server-rds-tutorial"></a>步驟 6：步驟 6：變更會傳送到伺服器 (RDS 教學課程)
如果**資料錄集**編輯物件時，任何變更 （也就是資料列會加入、 變更或刪除） 傳回給伺服器。  
  
> [!NOTE]
>  RDS 的預設行為可以叫用隱含 ADO 物件和 Microsoft OLE DB 遠端服務提供者。 查詢可能會傳回**Recordset**s，並編輯**資料錄集**s 可以更新資料來源。 本教學課程不會呼叫 RDS 使用 ADO 物件，但這是其外觀如果一樣：  
  
```vb
Dim rs as New ADODB.Recordset  
rs. "SELECT * FROM Authors","=MS Remote;=Pubs;" & _  
=https://yourServer;=SQLOLEDB;"  
...              ' Edit the Recordset.  
rs.   ' The equivalent of   
...  
```  
  
 **組件**假設您只使用在此情況下的[rds。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)且**Recordset**物件現在與相關聯**rds。DataControl**。 [SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md)方法的任何變更，以更新資料來源**資料錄集**物件如果[Server](../../../ado/reference/rds-api/server-property-rds.md)並[Connect](../../../ado/reference/rds-api/connect-property-rds.md)仍會設定屬性。  
  
```vb
Sub RDSTutorial6A()  
Dim DC as New RDS.DataControl  
Dim RS as ADODB.Recordset  
DC. = "https://yourServer"  
DC. = "DSN=Pubs"  
DC. = "SELECT * FROM Authors"  
DC.  
...  
Set RS = DC.  
   ' Edit the Recordset.  
...  
DC.  
...  
```  
  
 **組件 B**或者，您可以更新 「 server 含[RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)物件，指定連接並**資料錄集**物件。  
  
```vb
Sub RDSTutorial6B()  
Dim DS As New RDS.DataSpace  
Dim RS As ADODB.Recordset  
Dim DC As New RDS.DataControl  
Dim DF As Object  
Dim blnStatus As Boolean  
Set DF = DS.("RDSServer.DataFactory", "https://yourServer")  
Set RS = DF. ("DSN=Pubs", "SELECT * FROM Authors")  
DC. = RS    ' Visual controls can now bind to DC.  
    ' Edit the Recordset.  
blnStatus = DF."DSN=Pubs", RS  
End Sub  
```  
  
 **這是本教學課程的結尾。**  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件不會再包含在 Windows 作業系統中 (請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)如需詳細資訊)。 RDS 用戶端元件將會在 Windows 的未來版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="see-also"></a>另請參閱  
 [Microsoft OLE DB 遠端服務提供者 （ADO 服務提供者）](../../../ado/guide/appendixes/microsoft-ole-db-remoting-provider-ado-service-provider.md)   
 [RDS 教學課程](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [RDS 教學課程 (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
