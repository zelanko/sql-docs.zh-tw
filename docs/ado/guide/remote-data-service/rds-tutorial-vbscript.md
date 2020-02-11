---
title: RDS 教學課程（VBScript） |Microsoft Docs
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
ms.openlocfilehash: d45347bcdf212158fb6a0ee9f4599e1e1b00ff54
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67922420"
---
# <a name="rds-tutorial-vbscript"></a>RDS 教學課程 (VBScript)
這是以 Microsoft Visual Basic Scripting Edition 撰寫的 RDS 教學課程。 如需本教學課程用途的說明，請參閱[RDS 教學](../../../ado/guide/remote-data-service/rds-tutorial.md)課程。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統不再包含 RDS 伺服器元件（如需詳細資訊，請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)）。 RDS 用戶端元件將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 在本教學課程中， [RDS。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)和[RDS。](../../../ado/reference/rds-api/dataspace-object-rds.md)系統會在設計階段建立「空間」，也就是使用物件標記來定義，如下`<OBJECT>...</OBJECT>`所示：。 或者，您也可以在執行時間使用[CreateObject 方法（RDS）](../../../ado/reference/rds-api/createobject-method-rds.md)方法來建立它們。 例如， **RDS。** 可能會建立 DataControl 物件，如下所示：  
  
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
 VBScript 可以藉由存取 Active Server Pages 可用的 VBScript **request.servervariables**方法，來探索它執行所在的 IIS 網頁伺服器名稱：  
  
```vb
"https://<%=Request.ServerVariables("SERVER_NAME")%>"  
```  
  
 不過，在本教學課程中，請使用虛構伺服器 "yourServer"。  
  
> [!NOTE]
>  請注意**ByRef**引數的資料類型。 VBScript 不會讓您指定變數類型，因此您必須一律傳遞**Variant**。 使用 HTTP 時，如果您以 Rds 叫用，則 RDS 可讓您將 Variant 傳遞給需要非變異的方法 **。[空間**物件[CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md)方法]。 使用 DCOM 或同進程伺服器時，您必須比對用戶端和伺服器端上的參數類型，否則會收到「類型不符」錯誤。  
  
```vb
Set DF1 = DS1.CreateObject("RDSServer.DataFactory", "https://yourServer")  
```  
  
## <a name="step-2a---invoke-the-server-program-with-rdsdatacontrol"></a>步驟 2a-使用 RDS 叫用伺服器程式。DataControl  
 這個範例只是一個批註，示範 RDS 的預設行為 **。DataControl**是執行指定的查詢。  
  
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
  
## <a name="step-2b---invoke-the-server-program-with-rdsserverdatafactory"></a>步驟 2b-使用 RDSServer 來叫用伺服器程式。 DataFactory  
  
## <a name="step-3---server-obtains-a-recordset"></a>步驟 3-伺服器取得記錄集  
  
## <a name="step-4---server-returns-the-recordset"></a>步驟 4-伺服器傳回記錄集  
  
```vb
Set RS = DF1.Query("DSN=Pubs;", "SELECT * FROM Authors")  
```  
  
## <a name="step-5---datacontrol-is-made-usable-by-visual-controls"></a>步驟 5-DataControl 是由視覺效果控制項所使用  
  
```vb
' Assign the returned recordset to the DataControl.  
  
DC1.SourceRecordset = RS  
```  
  
## <a name="step-6a---changes-are-sent-to-the-server-with-rdsdatacontrol"></a>步驟 6a-使用 RDS 將變更傳送至伺服器。DataControl  
 這個範例只是一個批註，示範**RDS 如何。DataControl**會執行更新。  
  
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
  
## <a name="step-6b---changes-are-sent-to-the-server-with-rdsserverdatafactory"></a>步驟 6b-使用 RDSServer 將變更傳送至伺服器。 DataFactory  
  
```vb
DF.SubmitChanges "DSN=Pubs", RS  
  
End Sub  
</SCRIPT>  
</BODY>  
</HTML>  
```  
  
 **本教學課程即將結束。**  
  
## <a name="see-also"></a>另請參閱  
 [RDS 教學課程](../../../ado/guide/remote-data-service/rds-tutorial.md)   
