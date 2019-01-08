---
title: RDS 教學課程 (VBScript) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- RDS tutorial [ADO], VBScript
ms.assetid: e2a48c4d-88b1-43ff-a202-9cdec54997d2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3a50b9d8c1f22f23f3533240b2543ef981fef8e9
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52535204"
---
# <a name="rds-tutorial-vbscript"></a>RDS 教學課程 (VBScript)
這是 RDS 教學課程中，以 Microsoft Visual Basic Scripting Edition。 如需本教學課程的用途的說明，請參閱 < [RDS 教學課程](../../../ado/guide/remote-data-service/rds-tutorial.md)。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件不會再包含在 Windows 作業系統中 (請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)如需詳細資訊)。 RDS 用戶端元件將會在 Windows 的未來版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 在本教學課程中， [rds。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)和[rds。DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md)會建立在設計階段-也就是其定義使用物件標記，像這樣： `<OBJECT>...</OBJECT>`。 或者，他們無法建立與執行時期[CreateObject 方法 (RDS)](../../../ado/reference/rds-api/createobject-method-rds.md)方法。 比方說， **rds。DataControl**無法建立物件，就像這樣：  
  
```vb
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
  
## <a name="step-1---specify-a-server-program"></a>步驟 1-指定伺服器程式  
 VBScript 可以探索它所存取的 VBScript 執行的 IIS Web 伺服器的名稱**Request.ServerVariables** Active Server Pages 方法：  
  
```vb
"https://<%=Request.ServerVariables("SERVER_NAME")%>"  
```  
  
 不過，本教學課程中，使用虛數的伺服器，您的 「 伺服器 」。  
  
> [!NOTE]
>  注意到的資料型別**ByRef**引數。 VBScript 不會讓您指定變數的型別，所以您必須一律傳遞**Variant**。 使用 HTTP 時，RDS 可讓您將變數傳遞給預期非變異，如果您將它與叫用方法**rds。DataSpace**物件[CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md)方法。 使用 DCOM 或同處理序伺服器時，您必須符合參數型別，用戶端和伺服器端，或您會收到 「 型別不相符 」 的錯誤。  
  
```vb
Set DF1 = DS1.CreateObject("RDSServer.DataFactory", "https://yourServer")  
```  
  
## <a name="step-2a---invoke-the-server-program-with-rdsdatacontrol"></a>步驟 2a： 叫用與 RDS 伺服器程式DataControl  
 這個範例是只是示範程式的註解的預設行為**rds。DataControl**是執行指定的查詢。  
  
```vb
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID="DC1">  
   <PARAM NAME="SQL" VALUE="SELECT * FROM Authors">  
   <PARAM NAME="Connect" VALUE="DSN=Pubs;">  
   <PARAM NAME="Server" VALUE="https://yourServer/">  
</OBJECT>  
...  
<SCRIPT LANGUAGE="VBScript">  
  
Sub RDSTutorial2A()  
   Dim RS  
   DC1.Refresh  
   Set RS = DC1.Recordset  
...  
```  
  
## <a name="step-2b---invoke-the-server-program-with-rdsserverdatafactory"></a>步驟 2b： 叫用伺服器程式 RDSServer.DataFactory  
  
## <a name="step-3---server-obtains-a-recordset"></a>步驟 3-伺服器取得資料錄集  
  
## <a name="step-4---server-returns-the-recordset"></a>步驟 4： 伺服器傳回資料錄集  
  
```vb
Set RS = DF1.Query("DSN=Pubs;", "SELECT * FROM Authors")  
```  
  
## <a name="step-5---datacontrol-is-made-usable-by-visual-controls"></a>步驟 5-DataControl 是所使用的視覺控制項  
  
```vb
' Assign the returned recordset to the DataControl.  
  
DC1.SourceRecordset = RS  
```  
  
## <a name="step-6a---changes-are-sent-to-the-server-with-rdsdatacontrol"></a>步驟 6a-變更傳送到 「 server 含 rds。DataControl  
 這個範例是註解只是示範如何**rds。DataControl**執行更新。  
  
```vb
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID="DC1">  
   <PARAM NAME="SQL" VALUE="SELECT * FROM Authors">  
   <PARAM NAME="Connect" VALUE="DSN=Pubs;">  
   <PARAM NAME="Server" VALUE="https://yourServer/">  
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
  
## <a name="step-6b---changes-are-sent-to-the-server-with-rdsserverdatafactory"></a>步驟 6b-變更傳送到 「 server 含 RDSServer.DataFactory  
  
```vb
DF.SubmitChanges "DSN=Pubs", RS  
  
End Sub  
</SCRIPT>  
</BODY>  
</HTML>  
```  
  
 **這是本教學課程的結尾。**  
  
## <a name="see-also"></a>另請參閱  
 [RDS 教學課程](../../../ado/guide/remote-data-service/rds-tutorial.md)   
