---
title: VBScript ADO 程式設計 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- ADO, VBScript
- VBScript [ADO]
ms.assetid: 6aaaf6d0-1376-4473-bea6-b81f2645a9ac
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 385826be9e980c2e6a46c880dd6248fd355dade1
ms.sourcegitcommit: 96b2355d54dfad259826e88bdff91cc9344e16f2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2018
ms.locfileid: "51350265"
---
# <a name="vbscript-ado-programming"></a>VBScript ADO 程式設計
## <a name="creating-an-ado-project"></a>建立 ADO 專案  
 Microsoft Visual Basic，Scripting Edition 不支援類型程式庫，因此您不需要在您的專案中參考 ADO。 因此，不支援任何相關聯的功能，例如命令列完成。 此外，根據預設，ADO 列舉常數未定義在 VBScript 中。  
  
 不過，ADO 會提供您具有兩個 include 檔包含下列定義，以便搭配 VBScript:  
  
-   伺服器端指令碼使用 Adovbs.inc，這預設會安裝在 c:\Program Files\Common Files\System\ado\ 資料夾中。  
  
-   用戶端指令碼使用 Adcvbs.inc，這預設會安裝在 c:\Program Files\Common Files\System\msdac\ 資料夾中。  
  
 您可以複製並將常數的定義，從這些檔案貼到您的 ASP 網頁，或者，如果您要執行伺服器端指令碼，將 Adovbs.inc 檔案複製到您的網站上的資料夾，並參考從 ASP 頁面中，例如：  
  
```vb
<!--#include File="adovbs.inc"-->  
```  
  
## <a name="creating-ado-objects-in-vbscript"></a>在 VBScript 中建立 ADO 物件  
 您無法使用**Dim**將物件指派給特定的型別，在 VBScript 中的陳述式。 VBScript 不支援的同時，**的新**搭配使用的語法**Dim**應用程式的 Visual Basic 中的陳述式。 您必須改用**CreateObject**函式呼叫：  
  
```vb
Dim Rs1  
Set Rs1 = Server.CreateObject( "ADODB.Recordset" )  
```  
  
## <a name="vbscript-examples"></a>VBScript 範例  
 下列程式碼是 VBScript Active Server Page (ASP) 檔案中的伺服器端程式設計的一般範例：  
  
```vb
<%  @LANGUAGE="VBSCRIPT" %>  
<%  Option Explicit %>  
<!--#include File="adovbs.inc"-->  
<HTML>  
    <BODY BGCOLOR="White" topmargin="10" leftmargin="10">  
  
    <!-- Your ASP Code goes here -->  
<%  
Dim Source  
Dim Connect  
Dim Rs1  
  
Source = "SELECT * FROM Authors"  
Connect = "Provider=sqloledb;Data Source=srv;" & _  
    "Initial Catalog=Pubs;Integrated Security=SSPI;"  
  
Set Rs1 = Server.CreateObject( "ADODB.Recordset" )  
Rs1.Open Source, Connect, adOpenForwardOnly  
Response.Write("Success!")  
%>  
    </BODY>  
</HTML>  
```  
  
 更具體的 VBScript 範例隨附的 ADO 文件。 如需詳細資訊，請參閱 < [ADO 程式碼範例，在 Microsoft Visual Basic Scripting Edition](../../../ado/reference/ado-api/ado-code-examples-vbscript.md)。  
  
## <a name="differences-between-vbscript-and-visual-basic"></a>VBScript 和 Visual Basic 之間的差異  
 搭配使用 ADO 與 VBScript 是類似於使用 ADO 使用 Visual Basic，在許多方面，包括語法的使用方式。 不過，有一些顯著的差異：  
  
-   VBScript 僅支援 Variant 資料類型，以保留不同類型的資料。 您可以將您需要將資料儲存在 Variant 資料類型，以及資料將適當地運作，因為 VBScript 所執行的轉換。 它會辨識 ADO 中，所需的類型，並據此將變數中的值。  
  
-   您無法使用**上錯誤 goto\<標籤 >** VBScript 內。  
  
-   VBScript 支援一些內建的 Visual Basic 函式的這類**Msgbox**，**日期**，並**IsNumeric**。 不過，因為 VBScript 是 Visual Basic 的子集，並非所有的內建函式支援。 例如，VBScript nepodporuje**格式**函式和檔案 I/O 函式。
