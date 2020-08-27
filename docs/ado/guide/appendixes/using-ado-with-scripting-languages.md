---
description: 搭配使用 ADO 與指令碼語言
title: 搭配使用 ADO 與指令碼語言 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- scripting languages [ADO]
- ADO, scripting languages
ms.assetid: 76fc4d00-0c9f-422b-af5c-af6ed8fb29d8
author: rothja
ms.author: jroth
ms.openlocfilehash: 868731f7f7c88a2f6a26b5fab1670de8de96b1b3
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990949"
---
# <a name="using-ado-with-scripting-languages"></a>搭配使用 ADO 與指令碼語言
在腳本環境中，ADO 可讓您透過伺服器端腳本來公開資料。 在此案例中，ADO、它所使用的基礎 OLE DB 提供者，以及參考指定資料存放區所需的任何其他元件，會安裝在執行 Internet Information Services (IIS) 的伺服器上。 使用 Active Server Pages (ASP) ，ADO 是可產生 HTML 的腳本中所參考的元件，例如， 這個 HTML 內容可以透過 HTTP 傳遞給用戶端網頁瀏覽器。 藉由使用腳本，網頁可以將動作傳送回伺服器端腳本，讓您更新、執行或查看特定資料。  
  
 在網頁中使用 ActiveX 物件之前，請務必知道物件是否可安全地進行腳本處理。 當物件被視為安全的腳本時，就表示控制項無法在使用者的電腦上採取任何有害的動作，因此無須要求使用者核准，就可以執行此動作。 下表列出 ADO 物件，並指出它們是否為腳本的安全。  
  
|Object|適用于腳本的安全嗎？|  
|------------|-------------------------|  
|ADO 連接|是|  
|ADO 命令|否|  
|ADO 參數|否|  
|ADO 記錄集|是|  
|ADO 記錄|是|  
|ADO 資料流程|是|  
|ADO 錯誤|否|  
|ADOX 類別目錄|否|  
|ADOX 儲存格集|否|  
|RDS DataControl|是|  
|RDS 空間|是|  
|RDS DataFactory|否|  
  
 下表列出 Windows DAC/MDAC 隨附的提供者，並指出它們是否可以安全地進行腳本處理。  
  
|提供者|適用于腳本的安全嗎？|  
|--------------|-------------------------|  
|形狀|是|  
|Persist|是|  
|遠端|是|  
|適用于 SQL Server (SQLOLEDB 的 OLE DB 提供者) |否|  
|OLE DB Provider for ODBC (MSDASQL) |否|  
  
## <a name="odbc-data-sources"></a>ODBC 資料來源  
 腳本與非腳本 ADO 程式碼之間有一項明顯的差異，就是 ODBC 資料來源（如果使用的話）。 針對非腳本應用程式，您可以在「ODBC 資料來源管理員」中建立使用者 DSN。 針對在 IIS 下執行的腳本，您必須建立系統 DSN。否則，您的腳本將無法辨識您所建立的資料來源。 這適用于使用 Microsoft OLE DB Provider for ODBC 透過 Microsoft IIS 的任何 ADO 腳本應用程式。  
  
## <a name="referencing-the-ado-library"></a>參考 ADO 程式庫  
 不適用於指令碼語言。  
  
## <a name="handling-events"></a>錯誤事件  
 不適用於指令碼語言。  
  
 下列主題包含有關搭配使用 ADO 與指令碼語言的更具體資訊：  
  
-   [VBScript ADO 程式設計](./vbscript-ado-programming.md)  
  
-   [JScript ADO 程式設計](./jscript-ado-programming.md)  
  
## <a name="see-also"></a>另請參閱  
 [Microsoft ActiveX Data Objects (ADO) ](../../microsoft-activex-data-objects-ado.md)   
 [搭配使用 ADO 與 Microsoft Visual Basic](./using-ado-with-microsoft-visual-basic.md)   
 [搭配使用 ADO 與 Microsoft Visual C++](./using-ado-with-microsoft-visual-c.md)