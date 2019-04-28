---
title: JScript ADO 程式設計 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- JScript
helpviewer_keywords:
- JScript programming in ADO
- ADO, JScript programming
ms.assetid: 62273658-0fe7-4aac-b4d8-f725e6baf043
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: da87199347052189e5af8b881154b37723408d1f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62720355"
---
# <a name="jscript-ado-programming"></a>JScript ADO 程式設計
## <a name="creating-an-ado-project"></a>建立 ADO 專案  
 Microsoft JScript 不支援類型程式庫，因此您不需要參考 ADO 在您的專案。 因此，不支援任何相關聯的功能，例如命令列完成。 此外，根據預設，ADO 列舉常數未定義在 JScript 中。  
  
 不過，ADO 會提供您具有兩個 include 檔包含要搭配 JScript 的下列定義：  
  
-   伺服器端指令碼使用 Adojavas.inc，已安裝的 ADO 程式庫資料夾中。  
  
-   用戶端指令碼使用 Adcjavas.inc，這會安裝的 ADO 程式庫資料夾中。  
  
 您可以複製並將常數的定義，從這些檔案貼到您的 ASP 網頁，或者，如果您要執行伺服器端指令碼，將 Adojavas.inc 檔案複製到您的網站上的資料夾，並參考從您的 ASP 網頁，就像這樣：  
  
```javascript
<!--#include File="adojavas.inc"-->  
```  
  
## <a name="creating-ado-objects-in-jscript"></a>在 JScript 中建立 ADO 物件  
 您必須改用**CreateObject**函式呼叫：  
  
```javascript
var Rs1;  
Rs1 = Server.CreateObject("ADODB.Recordset");  
```  
  
## <a name="jscript-example"></a>JScript 範例  
 下列程式碼是會開啟 Active Server Page (ASP) 檔案中的 JScript 伺服器端程式設計的一般範例**資料錄集**物件：  
  
```javascript
<%  @LANGUAGE="JScript" %>  
<!--#include File="adojavas.inc"-->  
<HTML>  
<BODY BGCOLOR="White" topmargin="10" leftmargin="10">  
<%  
var Source = "SELECT * FROM Authors";  
var Connect =  "Provider=sqloledb;Data Source=srv;" +  
    "Initial Catalog=Pubs;Integrated Security=SSPI;"  
var Rs1 = Server.CreateObject( "ADODB.Recordset.2.5" );  
Rs1.Open(Source,Connect,adOpenForwardOnly);  
Response.Write("Success!");  
%>  
</BODY>  
</HTML>  
```
