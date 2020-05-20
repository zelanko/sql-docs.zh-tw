---
title: 步驟6：將變更傳送到伺服器（RDS 教學課程） |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 2094562f03f768ad6c98feccd0ed4a1e932a8fca
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764639"
---
# <a name="step-6-changes-are-sent-to-the-server-rds-tutorial"></a>步驟 6：將變更傳送到伺服器 (RDS 教學課程)
如果已編輯**記錄集**物件，任何變更（也就是加入、變更或刪除的資料列）都可以傳回伺服器。  
  
> [!NOTE]
>  RDS 的預設行為可以使用 ADO 物件和 Microsoft OLE DB 遠端處理提供者來隱含地叫用。 查詢可以傳回**記錄集**，而編輯的**記錄集**可以更新資料來源。 本教學課程不會叫用具有 ADO 物件的 RDS，但這就是它看起來的樣子：  
  
```vb
Dim rs as New ADODB.Recordset  
rs. "SELECT * FROM Authors","=MS Remote;=Pubs;" & _  
=https://yourServer;=SQLOLEDB;"  
...              ' Edit the Recordset.  
rs.   ' The equivalent of   
...  
```  
  
 **部分 A**假設在此情況下，您只使用了[RDS。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) ，而且**記錄集**物件現在與 RDS 相關聯 **。DataControl**。 如果仍然設定[伺服器](../../../ado/reference/rds-api/server-property-rds.md)和[連接](../../../ado/reference/rds-api/connect-property-rds.md)屬性， [SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md)方法會以**記錄集**物件的任何變更來更新資料來源。  
  
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
  
 **第 B 部分**或者，您可以使用[RDSServer. DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)物件來補救伺服器，並指定連接和**記錄集**物件。  
  
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
  
 **本教學課程即將結束。**  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統不再包含 RDS 伺服器元件（如需詳細資訊，請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)）。 RDS 用戶端元件將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="see-also"></a>另請參閱  
 [Microsoft OLE DB 遠端處理提供者（ADO 服務提供者）](../../../ado/guide/appendixes/microsoft-ole-db-remoting-provider-ado-service-provider.md)   
 [RDS 教學課程](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [RDS 教學課程 (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
