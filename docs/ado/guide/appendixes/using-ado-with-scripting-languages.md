---
title: 使用 ADO 與指令碼語言 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: d41d5a0239f11882c135c27fd4af8e817e83b799
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66702771"
---
# <a name="using-ado-with-scripting-languages"></a>搭配使用 ADO 與指令碼語言
在指令碼環境中，ADO 可讓您公開資料，透過伺服器端指令碼。 在此案例中，ADO，基礎 OLE DB 提供者，它會使用，並參考指定的資料存放區所需的其他任何元件會安裝在執行 Internet Information Services (IIS) 伺服器。 ADO 使用 Active Server Pages (ASP)，是可以產生 HTML，例如指令碼中參考的元件。 此 HTML 內容可以透過 HTTP 傳遞至用戶端 Web 瀏覽器。 使用指令碼，網頁就可以將動作傳送回伺服器端指令碼，可讓您更新、 周遊，或檢視特定的資料。  
  
 在網頁上使用 ActiveX 物件之前，務必知道值，指出物件是否安全的。 當物件被視為安全的時表示的控制項無法在使用者電腦上進行任何有害的動作，因此可以執行而不要求使用者核准。 下表列出 ADO 物件，並指出它們是否安全的。  
  
|Object|指令碼處理安全嗎？|  
|------------|-------------------------|  
|ADO 連接|是|  
|ADO 命令|否|  
|ADO 參數|否|  
|ADO 資料錄集|是|  
|ADO 資料錄|是|  
|ADO Stream|是|  
|ADO 錯誤|否|  
|ADOX 目錄|否|  
|ADOX 資料格集|否|  
|RDS DataControl|是|  
|RDS 資料空間|是|  
|RDS DataFactory|否|  
  
 下表列出包含與 Windows DAC/MDAC、 提供者，並指出它們是否安全的。  
  
|提供者|指令碼處理安全嗎？|  
|--------------|-------------------------|  
|形狀圖|是|  
|保存|是|  
|遠端|是|  
|OLE DB Provider for SQL Server (SQLOLEDB)|否|  
|OLE DB Provider for ODBC (MSDASQL)|否|  
  
## <a name="odbc-data-sources"></a>ODBC 資料來源  
 一個顯著的差異，指令碼和非指令碼的 ADO 程式碼之間會是 ODBC 資料來源時，如果使用。 對於非指令碼的應用程式，您可以建立 「 使用者 DSN 中 ODBC 資料來源管理員 」 中。 在 IIS 下執行的指令碼，您必須建立系統 DSN;否則您的指令碼將無法辨識您所建立的資料來源。 這適用於任何 ADO 指令碼應用程式中使用 Microsoft OLE DB Provider for ODBC，透過 Microsoft IIS。  
  
## <a name="referencing-the-ado-library"></a>參考 ADO 程式庫  
 不適用與指令碼語言。  
  
## <a name="handling-events"></a>處理事件  
 不適用與指令碼語言。  
  
 下列主題包含有關搭配使用 ADO 與指令碼語言更具體資訊：  
  
-   [VBScript ADO 程式設計](../../../ado/guide/appendixes/vbscript-ado-programming.md)  
  
-   [JScript ADO 程式設計](../../../ado/guide/appendixes/jscript-ado-programming.md)  
  
## <a name="see-also"></a>另請參閱  
 [Microsoft ActiveX Data Objects (ADO)](../../../ado/microsoft-activex-data-objects-ado.md)   
 [使用 ADO 與 Microsoft Visual Basic](../../../ado/guide/appendixes/using-ado-with-microsoft-visual-basic.md)   
 [搭配使用 ADO 與 Microsoft Visual C++](../../../ado/guide/appendixes/using-ado-with-microsoft-visual-c.md)   
