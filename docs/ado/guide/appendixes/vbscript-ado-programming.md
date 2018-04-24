---
title: VBScript ADO 程式設計 |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- ADO, VBScript
- VBScript [ADO]
ms.assetid: 6aaaf6d0-1376-4473-bea6-b81f2645a9ac
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 563770aae88801fd58a67c7c3af2cee241426396
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/18/2018
---
# <a name="vbscript-ado-programming"></a>VBScript ADO 程式設計
## <a name="creating-an-ado-project"></a>建立 ADO 專案  
 Microsoft Visual Basic，Scripting Edition 不支援型別程式庫，因此您不需要在您的專案中參考 ADO。 因此，沒有相關聯的功能，例如命令列完成是受支援。 此外，根據預設，ADO 列舉常數未定義在 VBScript 中。  
  
 不過，ADO 會提供您具有兩個包含檔案，其中包含要搭配 VBScript 的下列定義：  
  
-   對於伺服器端指令碼使用 Adovbs.inc，這是預設安裝在 c:\Program Files\Common Files\System\ado\ 資料夾。  
  
-   供用戶端指令碼使用 Adcvbs.inc，這是預設安裝在 c:\Program Files\Common Files\System\msdac\ 資料夾。  
  
 您可以複製並貼入 ASP 網頁，從這些檔案的常數定義或者，若您執行伺服器端指令碼，將 Adovbs.inc 檔案複製到您的網站上的資料夾，並參考從 ASP 頁面如下：  
  
```  
<!--#include File="adovbs.inc"-->  
```  
  
## <a name="creating-ado-objects-in-vbscript"></a>VBScript 中建立 ADO 物件  
 您無法使用**Dim**將物件指派給特定類型在 VBScript 中的陳述式。 此外，不支援 VBScript**新增**搭配使用的語法**Dim**應用程式的 Visual Basic 中的陳述式。 您必須改為使用**CreateObject**函式呼叫：  
  
```  
Dim Rs1  
Set Rs1 = Server.CreateObject( "ADODB.Recordset" )  
```  
  
## <a name="vbscript-examples"></a>VBScript 範例  
 下列程式碼是 VBScript Active Server Page (ASP) 檔案中的伺服器端程式設計的一般範例：  
  
```  
<%  @LANGUAGE="VBSCRIPT" %>  
<%  Option Explicit %>  
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
  
 更具體的 VBScript 範例隨附的 ADO 文件。 如需詳細資訊，請參閱[ADO 程式碼範例在 Microsoft Visual Basic Scripting Edition](../../../ado/reference/ado-api/ado-code-examples-vbscript.md)。  
  
## <a name="differences-between-vbscript-and-visual-basic"></a>VBScript 和 Visual Basic 之間的差異  
 使用 ADO 搭配 VBScript 是類似於使用 ADO 使用 Visual Basic，在許多方面，包括如何使用語法。 不過，有一些顯著的差異：  
  
-   VBScript 支援只 Variant 資料類型，可存放不同類型的資料。 您可以在 Variant 資料類型，儲存所需的資料，資料將適當地運作，因為 VBScript 所執行的轉換。 它會辨識 ADO 中，所需的類型，並據此轉換中之變數的值。  
  
-   您無法使用**上錯誤 goto\<標籤 >** VBScript 內。  
  
-   VBScript 支援某些內建的 Visual Basic 函式例如**Msgbox**，**日期**，和**IsNumeric**。 不過，因為 VBScript 是 Visual Basic 的子集，並非所有的內建函式支援。 例如，不支援 VBScript**格式**函式和檔案 I/O 函式。
