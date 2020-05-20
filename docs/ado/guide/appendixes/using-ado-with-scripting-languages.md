---
title: 使用 ADO 搭配指令碼語言 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
ms.openlocfilehash: 71057caed6d28a2923e1c3735e10d20fccc9217d
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82761566"
---
# <a name="using-ado-with-scripting-languages"></a>搭配使用 ADO 與指令碼語言
在腳本環境中，ADO 可讓您透過伺服器端腳本來公開資料。 在此案例中，ADO 會使用其所用的基礎 OLE DB 提供者，而參考指定資料存放區所需的任何其他元件都會安裝在執行 Internet Information Services （IIS）的伺服器上。 使用 Active Server Pages （ASP），ADO 是腳本中所參考的元件，可以產生 HTML，例如。 這個 HTML 內容可以透過 HTTP 傳遞至用戶端網頁瀏覽器。 藉由使用腳本，網頁可以將動作傳送回伺服器端腳本，讓您可以更新、流覽或查看特定資料。  
  
 在網頁中使用 ActiveX 物件之前，請務必瞭解物件是否可安全進行腳本處理。 當物件被視為安全進行腳本處理時，這表示控制項無法在使用者的電腦上採取任何有害動作，因此可以在不要求使用者核准的情況下執行。 下表列出 ADO 物件，並指出它們是否安全地進行腳本處理。  
  
|Object|安全地進行腳本處理嗎？|  
|------------|-------------------------|  
|ADO 連接|是|  
|ADO 命令|否|  
|ADO 參數|否|  
|ADO 記錄集|是|  
|ADO 記錄|是|  
|ADO 資料流程|是|  
|ADO 錯誤|否|  
|ADOX 目錄|否|  
|ADOX 集格|否|  
|RDS DataControl|是|  
|RDS 空間|是|  
|RDS DataFactory|否|  
  
 下表列出 Windows DAC/MDAC 隨附的提供者，並指出它們是否安全地進行腳本處理。  
  
|提供者|安全地進行腳本處理嗎？|  
|--------------|-------------------------|  
|圖形|是|  
|Persist|是|  
|遠端|是|  
|SQL Server 的 OLE DB 提供者（SQLOLEDB）|否|  
|ODBC 的 OLE DB 提供者（MSDASQL）|否|  
  
## <a name="odbc-data-sources"></a>ODBC 資料來源  
 腳本和非腳本 ADO 程式碼之間有一項明顯的差異，就是 ODBC 資料來源（如果有使用的話）。 若為非腳本應用程式，您可以在 ODBC 資料來源管理員中建立使用者 DSN。 對於在 IIS 底下執行的腳本，您必須建立系統 DSN;否則，您的腳本將無法辨識您所建立的資料來源。 這適用于使用 Microsoft OLE DB Provider for ODBC 透過 Microsoft IIS 的任何 ADO 腳本應用程式。  
  
## <a name="referencing-the-ado-library"></a>參考 ADO 程式庫  
 不適用指令碼語言。  
  
## <a name="handling-events"></a>錯誤事件  
 不適用指令碼語言。  
  
 下列主題包含有關搭配使用 ADO 與指令碼語言的更多特定資訊：  
  
-   [VBScript ADO 程式設計](../../../ado/guide/appendixes/vbscript-ado-programming.md)  
  
-   [JScript ADO 程式設計](../../../ado/guide/appendixes/jscript-ado-programming.md)  
  
## <a name="see-also"></a>另請參閱  
 [Microsoft ActiveX Data Objects （ADO）](../../../ado/microsoft-activex-data-objects-ado.md)   
 [搭配使用 ADO 與 Microsoft Visual Basic](../../../ado/guide/appendixes/using-ado-with-microsoft-visual-basic.md)   
 [搭配使用 ADO 與 Microsoft Visual C++](../../../ado/guide/appendixes/using-ado-with-microsoft-visual-c.md)   
