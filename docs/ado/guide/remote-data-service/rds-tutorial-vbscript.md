---
title: RDS 教學課程 (VBScript) |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 02/14/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- RDS tutorial [ADO], VBScript
ms.assetid: e2a48c4d-88b1-43ff-a202-9cdec54997d2
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: daa7caa4677c33469250e77a1e58e77e697e08c1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="rds-tutorial-vbscript"></a>RDS 教學課程 (VBScript)
這是 RDS 教學課程中，以撰寫的 Microsoft Visual Basic Scripting Edition。 如需本教學課程的用途的說明，請參閱[RDS 教學課程](../../../ado/guide/remote-data-service/rds-tutorial.md)。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 在本教學課程， [.RDSDataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)和[.RDSDataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md)在設計階段建立 — 也就是其定義物件的標記，像這樣： `<OBJECT>...</OBJECT>`。 或者，他們可以建立在執行階段使用[CreateObject 方法 (RDS)](../../../ado/reference/rds-api/createobject-method-rds.md)方法。 例如， **.RDSDataControl**無法建立物件，像這樣：  
  
```  
Set DC = Server.CreateObject("RDS.DataControl")  
   <!-- RDS.DataControl -->  
   <OBJECT   
      ID="DC1" CLASSID="CLSID:BD96C556-65A3-11D0-983A-00C04FC29E33">  
   </OBJECT>  
  
   <!-- RDS.DataSpace -->  
   <OBJECT   
      ID="DS1" WIDTH=1 HEIGHT=1  
      CLASSID="CLSID:BD96C556-65A3-11D0-983A-00C04FC29E36">  
   </OBJECT>  
  
   <SCRIPT LANGUAGE="VBScript">  
  
   Sub RDSTutorial()  
   Dim DF1   
```  
  
## <a name="step-1--specify-a-server-program"></a>步驟 1 — 指定伺服器程式  
 VBScript 可以探索的 IIS Web 伺服器執行藉由存取 VBScript 名稱**Request.ServerVariables** Active Server Pages 方法：  
  
```  
"http://<%=Request.ServerVariables("SERVER_NAME")%>"  
```  
  
 不過，此教學課程中，使用虛數的伺服器，您的 「 伺服器 」。  
  
> [!NOTE]
>  請注意的資料型別**ByRef**引數。 VBScript 不會讓您指定變數的型別，所以您永遠必須傳遞**Variant**。 使用 HTTP，RDS 可讓您將變數傳遞給必須有非 Variant，如果您叫用其與方法 **.RDSDataSpace**物件[CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md)方法。 使用 DCOM 或同處理序伺服器時，您必須符合參數類型，用戶端和伺服器端，或您會收到 「 型別不符 」 的錯誤。  
  
```  
Set DF1 = DS1.CreateObject("RDSServer.DataFactory", "http://yourServer")  
```  
  
## <a name="step-2a--invoke-the-server-program-with-rdsdatacontrol"></a>步驟 2a： 叫用的 RDS 伺服器程式DataControl  
 這個範例是只擊發的註解的預設行為 **.RDSDataControl**是執行指定的查詢。  
  
```  
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID="DC1">  
   <PARAM NAME="SQL" VALUE="SELECT * FROM Authors">  
   <PARAM NAME="Connect" VALUE="DSN=Pubs;">  
   <PARAM NAME="Server" VALUE="http://yourServer/">  
</OBJECT>  
...  
<SCRIPT LANGUAGE="VBScript">  
  
Sub RDSTutorial2A()  
   Dim RS  
   DC1.Refresh  
   Set RS = DC1.Recordset  
...  
```  
  
## <a name="step-2b--invoke-the-server-program-with-rdsserverdatafactory"></a>步驟 2b： 叫用伺服器程式與 RDSServer.DataFactory  
  
## <a name="step-3--server-obtains-a-recordset"></a>步驟 3 — 伺服器取得資料錄集  
  
## <a name="step-4--server-returns-the-recordset"></a>步驟 4： 伺服器傳回的資料錄集  
  
```  
Set RS = DF1.Query("DSN=Pubs;", "SELECT * FROM Authors")  
```  
  
## <a name="step-5--datacontrol-is-made-usable-by-visual-controls"></a>步驟 5-DataControl 會使用由視覺控制項  
  
```  
' Assign the returned recordset to the DataControl.  
  
DC1.SourceRecordset = RS  
```  
  
## <a name="step-6a--changes-are-sent-to-the-server-with-rdsdatacontrol"></a>步驟 6a，變更會傳送至 RDS 的伺服器DataControl  
 這個範例是註解只需示範如何 **.RDSDataControl**執行更新。  
  
```  
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID="DC1">  
   <PARAM NAME="SQL" VALUE="SELECT * FROM Authors">  
   <PARAM NAME="Connect" VALUE="DSN=Pubs;">  
   <PARAM NAME="Server" VALUE="http://yourServer/">  
</OBJECT>  
...  
<SCRIPT LANGUAGE="VBScript">  
  
Sub RDSTutorial6A()  
Dim RS  
DC1.Refresh  
...  
Set RS = DC1.Recordset  
' Edit the Recordset object...  
' The SERVER and CONNECT properties are already set from Step 2A.  
Set DC1.SourceRecordset = RS  
...  
DC1.SubmitChanges  
```  
  
## <a name="step-6b--changes-are-sent-to-the-server-with-rdsserverdatafactory"></a>步驟 6b — 變更傳送到 「 server 含 RDSServer.DataFactory  
  
```  
DF.SubmitChanges "DSN=Pubs", RS  
  
End Sub  
</SCRIPT>  
</BODY>  
</HTML>  
```  
  
 **這是教學課程結束時。**  
  
## <a name="see-also"></a>另請參閱  
 [RDS 教學課程](../../../ado/guide/remote-data-service/rds-tutorial.md)   
