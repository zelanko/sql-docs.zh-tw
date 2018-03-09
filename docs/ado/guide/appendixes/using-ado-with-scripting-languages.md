---
title: "使用 ADO 搭配指令碼語言 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- scripting languages [ADO]
- ADO, scripting languages
ms.assetid: 76fc4d00-0c9f-422b-af5c-af6ed8fb29d8
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 804365750839fd3b9830a9573ab2cf397b529187
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="using-ado-with-scripting-languages"></a>使用 ADO 搭配指令碼語言
在指令碼環境中，ADO 可讓您公開資料透過伺服器端指令碼。 在此案例中，ADO 中，基礎 OLE DB 提供者，它使用，而且參考指定的資料存放區所需的其他元件安裝在執行網際網路資訊服務 (IIS) 的伺服器。 ADO 使用 Active Server Pages (ASP)，是可以產生 HTML，例如指令碼中參考的元件。 這個 HTML 內容可以透過 HTTP 傳遞至用戶端 Web 瀏覽器。 使用指令碼，網頁就可以將動作傳送回伺服器端指令碼，可讓您以更新、 周遊，或檢視特定資料。  
  
 您在網頁中使用 ActiveX 物件之前，請務必知道物件是否可安全用於指令碼。 當物件會被視為安全用於指令碼時，這表示不採取任何有害的動作，在使用者電腦上的控制項，因此可以執行，而要求使用者核准。 下表列出 ADO 物件，並指出它們是否可安全用於指令碼。  
  
|物件|指令碼的安全？|  
|------------|-------------------------|  
|ADO 連接|是|  
|ADO 命令|否|  
|ADO 參數|否|  
|ADO 資料錄集|是|  
|ADO 資料錄|是|  
|ADO 資料流|是|  
|ADO 錯誤|否|  
|ADOX 類別目錄|否|  
|ADOX 資料格集|否|  
|RDS DataControl|是|  
|RDS DataSpace|是|  
|RDS DataFactory|否|  
  
 下表列出包含與 Windows DAC/MDAC、 提供者，並指出它們是否可安全用於指令碼。  
  
|提供者|指令碼的安全？|  
|--------------|-------------------------|  
|形狀圖|是|  
|保存|是|  
|遠端|是|  
|OLE DB Provider for SQL Server (SQLOLEDB)|否|  
|OLE DB Provider for ODBC (MSDASQL)|否|  
  
## <a name="odbc-data-sources"></a>ODBC 資料來源  
 指令碼和非指令碼 ADO 程式碼之間的一個顯著的差異是 ODBC 資料來源時，如果使用。 對於非指令碼的應用程式，您可以建立使用者 DSN ODBC 資料來源管理員 」 中。 在 IIS 底下執行的指令碼，您必須建立系統 DSN。否則您的指令碼將無法辨識您所建立的資料來源。 這適用於任何 ADO 指令碼應用程式中使用 Microsoft OLE DB Provider for ODBC，透過 Microsoft IIS。  
  
## <a name="referencing-the-ado-library"></a>ADO 程式庫的參考  
 與指令碼語言不適用。  
  
## <a name="handling-events"></a>處理事件  
 與指令碼語言不適用。  
  
 下列主題包含更多使用 ADO 搭配指令碼語言的相關資訊：  
  
-   [VBScript ADO 程式設計](../../../ado/guide/appendixes/vbscript-ado-programming.md)  
  
-   [JScript ADO 程式設計](../../../ado/guide/appendixes/jscript-ado-programming.md)  
  
## <a name="see-also"></a>另請參閱  
 [Microsoft ActiveX Data Objects (ADO)](../../../ado/microsoft-activex-data-objects-ado.md)   
 [使用 ADO 搭配 Microsoft Visual Basic](../../../ado/guide/appendixes/using-ado-with-microsoft-visual-basic.md)   
 [搭配使用 ADO 與 Microsoft Visual C++](../../../ado/guide/appendixes/using-ado-with-microsoft-visual-c.md)   
