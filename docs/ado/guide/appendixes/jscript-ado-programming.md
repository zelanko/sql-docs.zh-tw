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
ms.openlocfilehash: 8d07759405dc337667cc8971ce7795af428a0cfa
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67926807"
---
# <a name="jscript-ado-programming"></a>JScript ADO 程式設計
## <a name="creating-an-ado-project"></a>建立 ADO 專案  
 Microsoft JScript 不支援類型程式庫，因此您不需要在專案中參考 ADO。 因此，不支援任何相關聯的功能，例如命令列完成。 此外，根據預設，ADO 列舉的常數不會定義于 JScript 中。  
  
 不過，ADO 會提供包含下列定義的兩個包含檔案，以用於 JScript：  
  
-   若為伺服器端腳本，請使用 Adojavas，它會安裝在 ADO 程式庫資料夾中。  
  
-   若為用戶端腳本，請使用安裝在 ADO 程式庫資料夾中的 Adcjavas。  
  
 您可以將這些檔案中的常數定義複製並貼到您的 ASP 頁面中，或者，如果您要執行伺服器端腳本處理，請將 Adojavas 複製到網站上的資料夾，並從您的 ASP 網頁參照它，如下所示：  
  
```javascript
<!--#include File="adojavas.inc"-->  
```  
  
## <a name="creating-ado-objects-in-jscript"></a>在 JScript 中建立 ADO 物件  
 您必須改為使用**CreateObject**函式呼叫：  
  
```javascript
var Rs1;  
Rs1 = Server.CreateObject("ADODB.Recordset");  
```  
  
## <a name="jscript-example"></a>JScript 範例  
 下列程式碼是在開啟**記錄集**物件的 Active server PAGE （ASP）檔案中，JScript 伺服器端程式設計的一般範例：  
  
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
