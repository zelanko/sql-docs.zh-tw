---
title: "JScript ADO 程式設計 |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- JScript
helpviewer_keywords:
- JScript programming in ADO
- ADO, JScript programming
ms.assetid: 62273658-0fe7-4aac-b4d8-f725e6baf043
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6ae8137c2e5641594c3ddcf768c47b7fe844fafc
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="jscript-ado-programming"></a>JScript ADO 程式設計
## <a name="creating-an-ado-project"></a>建立 ADO 專案  
 Microsoft JScript 不支援型別程式庫，因此您不需要參考 ADO 在專案中。 因此，沒有相關聯的功能，例如命令列完成是受支援。 此外，根據預設，ADO 列舉常數未定義在 JScript 中。  
  
 不過，ADO 會提供您具有兩個包含檔案，其中包含要搭配 JScript 的下列定義：  
  
-   伺服器端指令碼之使用 Adojavas.inc，這會安裝在 ADO 程式庫資料夾。  
  
-   供用戶端指令碼使用 Adcjavas.inc，安裝於 ADO 文件庫資料夾中。  
  
 您可以複製並貼入 ASP 網頁，從這些檔案的常數定義或者，若您執行伺服器端指令碼，將 Adojavas.inc 檔案複製到您的網站上的資料夾，並參考從 ASP 頁面如下：  
  
```  
<!--#include File="adojavas.inc"-->  
```  
  
## <a name="creating-ado-objects-in-jscript"></a>在 JScript 中建立 ADO 物件  
 您必須改為使用**CreateObject**函式呼叫：  
  
```  
var Rs1;  
Rs1 = Server.CreateObject("ADODB.Recordset");  
```  
  
## <a name="jscript-example"></a>JScript 範例  
 下列程式碼會開啟 Active Server Page (ASP) 檔案中的 JScript 伺服器端程式設計的一般範例**資料錄集**物件：  
  
```  
<%  @LANGUAGE="JScript" %>  
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
