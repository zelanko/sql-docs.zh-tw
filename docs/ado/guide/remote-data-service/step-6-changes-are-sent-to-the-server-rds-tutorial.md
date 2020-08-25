---
description: 步驟 6：將變更傳送到伺服器 (RDS 教學課程)
title: 步驟6：將變更傳送到伺服器 (RDS 教學課程) |Microsoft Docs
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
ms.openlocfilehash: 0056f965e36fb1fadd3d7f8c08c2514ee2593d46
ms.sourcegitcommit: c4d564435c008e2c92035efd2658172f20f07b2b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88758998"
---
# <a name="step-6-changes-are-sent-to-the-server-rds-tutorial"></a>步驟 6：將變更傳送到伺服器 (RDS 教學課程)
如果已編輯 **記錄集** 物件，則任何變更 (也就是新增、變更或刪除的資料列) 可以傳回給伺服器。  
  
> [!NOTE]
>  RDS 的預設行為可以使用 ADO 物件和 Microsoft OLE DB 遠端處理提供者隱含地叫用。 查詢可以傳回 **記錄集**，而編輯的 **記錄集**可以更新資料來源。 本教學課程不會叫用具有 ADO 物件的 RDS，但這是它在執行時的外觀：  
  
```vb
Dim rs as New ADODB.Recordset  
rs. "SELECT * FROM Authors","=MS Remote;=Pubs;" & _  
=https://yourServer;=SQLOLEDB;"  
...              ' Edit the Recordset.  
rs.   ' The equivalent of   
...  
```  
  
 **部分 A** 在此情況下，假設您只有使用 [RDS。DataControl](../../reference/rds-api/datacontrol-object-rds.md) ，而且 **記錄集** 物件現在與 RDS 相關聯 **。DataControl**。 如果仍然設定[伺服器](../../reference/rds-api/server-property-rds.md)和[連接](../../reference/rds-api/connect-property-rds.md)屬性，則[SubmitChanges](../../reference/rds-api/submitchanges-method-rds.md)方法會使用**記錄集**物件的任何變更來更新資料來源。  
  
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
  
 **B 部分** 或者，您可以使用 [RDSServer. DataFactory](../../reference/rds-api/datafactory-object-rdsserver.md) 物件來補救伺服器，並指定連接和 **記錄集** 物件。  
  
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
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="see-also"></a>另請參閱  
 [Microsoft OLE DB (ADO 服務提供者的遠端處理提供者) ](../appendixes/microsoft-ole-db-remoting-provider-ado-service-provider.md)   
 [RDS 教學課程](./rds-tutorial.md)   
 [RDS 教學課程 (VBScript)](./rds-tutorial-vbscript.md)