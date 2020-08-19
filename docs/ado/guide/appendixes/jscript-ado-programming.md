---
description: JScript ADO 程式設計
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 2f1cad0a2717bb652759a7c8b0d60efc4b3f4541
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88444560"
---
# <a name="jscript-ado-programming"></a>JScript ADO 程式設計
## <a name="creating-an-ado-project"></a>建立 ADO 專案  
 Microsoft JScript 不支援類型程式庫，因此您不需要在專案中參考 ADO。 因此，不支援任何相關聯的功能，例如命令列完成。 此外，根據預設，ADO.NET 列舉的常數不會定義在 JScript 中。  
  
 不過，ADO 提供您兩個包含下列定義的 include 檔案，以搭配 JScript 使用：  
  
-   如果是伺服器端腳本，請使用 Adojavas，它會安裝在 ADO 程式庫資料夾中。  
  
-   若為用戶端腳本，請使用 Adcjavas，它會安裝在 ADO 程式庫資料夾中。  
  
 您可以從這些檔案複製並貼上常數定義至 ASP 頁面，或者，如果您正在進行伺服器端腳本處理，請將 Adojavas 檔案複製到網站上的資料夾，然後從 ASP 頁面參考它，如下所示：  
  
```javascript
<!--#include File="adojavas.inc"-->  
```  
  
## <a name="creating-ado-objects-in-jscript"></a>在 JScript 中建立 ADO 物件  
 您必須改為使用 **CreateObject** 函式呼叫：  
  
```javascript
var Rs1;  
Rs1 = Server.CreateObject("ADODB.Recordset");  
```  
  
## <a name="jscript-example"></a>JScript 範例  
 下列程式碼是在 Active Server Page (ASP) 檔案開啟 **記錄集** 物件的一般 JScript 伺服器端程式設計範例：  
  
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
