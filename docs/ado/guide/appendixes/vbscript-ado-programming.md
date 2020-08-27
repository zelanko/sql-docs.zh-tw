---
description: VBScript ADO 程式設計
title: VBScript ADO 程式設計 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 6b89d247f5bc91ca0b3494c15d3781116b8c9614
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990919"
---
# <a name="vbscript-ado-programming"></a>VBScript ADO 程式設計
## <a name="creating-an-ado-project"></a>建立 ADO 專案  
 Microsoft Visual Basic，腳本版本不支援型別程式庫，因此您不需要在專案中參考 ADO。 因此，不支援任何相關聯的功能，例如命令列完成。 此外，根據預設，ADO 列舉的常數不會在 VBScript 中定義。  
  
 不過，ADO 提供您兩個包含下列定義的 include 檔案，以搭配 VBScript 使用：  
  
-   針對伺服器端腳本使用 Adovbs，預設會安裝在 c:\Program Files\Common Files\System\ado\ 資料夾中。  
  
-   針對用戶端腳本使用 Adcvbs，預設會安裝在 c:\Program Files\Common Files\System\msdac\ 資料夾中。  
  
 您可以從這些檔案複製並貼上常數定義至 ASP 頁面，或者，如果您正在進行伺服器端腳本處理，請將 Adovbs 檔案複製到網站上的資料夾，然後從 ASP 頁面參考它，如下所示：  
  
```vb
<!--#include File="adovbs.inc"-->  
```  
  
## <a name="creating-ado-objects-in-vbscript"></a>在 VBScript 中建立 ADO 物件  
 您無法使用 **Dim** 語句將物件指派給 VBScript 中的特定類型。 此外，VBScript 也不支援在 Visual Basic for Applications 中搭配**Dim**語句使用的**新**語法。 您必須改為使用 **CreateObject** 函式呼叫：  
  
```vb
Dim Rs1  
Set Rs1 = Server.CreateObject( "ADODB.Recordset" )  
```  
  
## <a name="vbscript-examples"></a>VBScript 範例  
 下列程式碼是在 Active Server Page (ASP) 檔案中 VBScript 伺服器端程式設計的一般範例：  
  
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
  
 ADO 檔中包含更多特定的 VBScript 範例。 如需詳細資訊，請參閱 [Microsoft Visual Basic Scripting Edition 中的 ADO 程式碼範例](../../reference/ado-api/ado-code-examples-vbscript.md)。  
  
## <a name="differences-between-vbscript-and-visual-basic"></a>VBScript 與 Visual Basic 之間的差異  
 搭配使用 ADO 與 VBScript 的方式類似于在許多方面使用 ADO 搭配 Visual Basic，包括如何使用語法。 不過，有一些重大差異存在：  
  
-   VBScript 僅支援 Variant 資料類型，可保存不同類型的資料。 您可以將所需的資料儲存在 Variant 資料類型中，而資料會因為 VBScript 執行的轉換而適當地運作。 它會辨識 ADO 所需的類型，並據以轉換變數中的值。  
  
-   您無法在 VBScript 中使用**on error goto \<label> ** 。  
  
-   VBScript 支援一些內建的 Visual Basic 功能，例如 **Msgbox**、 **Date**和 **IsNumeric**。 不過，因為 VBScript 是 Visual Basic 的子集，所以並非所有的內建函數都受到支援。 例如，VBScript 不支援 **Format** 函數和檔案 i/o 函數。