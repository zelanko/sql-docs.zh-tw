---
title: "在自訂應用程式中使用 RSClientPrint 控制項 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- RSPrintClient control
- print controls [Reporting Services]
- custom printing [Reporting Services]
- client-side printing
ms.assetid: 8c0bdd18-8905-4e22-9774-a240fc81a8a7
caps.latest.revision: 31
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 8afee187160da9d35efd0c7079b649bac7e73740
ms.contentlocale: zh-tw
ms.lasthandoff: 06/13/2017

---
# <a name="using-the-rsclientprint-control-in-custom-applications"></a>在自訂應用程式中使用 RSClientPrint 控制項
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] ActiveX 控制項**RSPrintClient**，提供在 HTML 檢視器中檢視報表的用戶端列印。 它提供**列印**對話方塊，讓使用者能夠起始列印工作、 預覽報表，指定要列印的頁面並變更邊界。 在用戶端列印作業期間，報表伺服器會在影像 (EMF) 轉譯延伸模組中轉譯報表，然後使用作業系統的列印功能來建立列印工作，並將它傳送到印表機。  
  
 用戶端列印提供控制及改善 HTML 報表的列印輸出品質的方式，亦即，利用使用者電腦上的瀏覽器列印設定，而不使用報表的頁面維度、邊界、頁首和頁尾文字，來建立列印輸出。 列印控制項會讀取報表的屬性值，來設定頁面的大小和邊界。  
  
 開發人員想要啟用協力廠商工具列或檢視器中的用戶端列印功能可以存取 ActiveX 控制項，透過**RSClientPrint** COM 物件。 此控制項可以自由散發。 下列清單提供使用此控制項的一些建議：  
  
-   使用此控制項即可改善網路架構報表的列印功能。 您可以在任何指定的物件[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]-相容的程式設計語言或指令碼。 此控制項並不是要用於 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows Form 應用程式。  
  
-   從 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 程式檔案複製 .cab 檔，然後將它加入自訂應用程式的程式碼庫。  
  
-   使用\<物件 > 若要指定控制項的標記。  
  
-   在 OBJECT CODEBASE 屬性中，指定 .cab 檔的相對 URL 或完整 URL。  
  
-   對 .cab 檔指定您自己的應用程式版本資訊，以追蹤在應用程式中使用的版本。  
  
-   檢閱關於影像 (EMF) 轉譯的線上叢書主題，以了解如何轉譯頁面來進行預覽列印和輸出。  
  
## <a name="rsprintclient-overview"></a>RSPrintClient 概觀  
 控制項會顯示自訂列印對話方塊，其中支援與其他列印對話方塊一樣的一般功能，包括預覽列印、可指定要列印的特定頁面及範圍、頁面邊界和列印方向等選擇。 此控制項已封裝成 CAB 檔。 中的文字**列印**對話方塊當地語系化為所有支援的語言[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 **RSPrintClient** ActiveX 控制項會使用影像轉譯延伸模組 (EMF) 來列印報表。 其中使用下列 EMF 裝置資訊：StartPage、EndPage、MarginBottom、MarginLeft、MarginTop、MarginRight、PageHeight 和 PageWidth。 影像轉譯的其他裝置資訊設定則不支援。  
  
### <a name="language-support"></a>語言支援  
 列印控制項會以不同的語言呈現使用者介面文字，並接受根據不同度量系統所輸入的值。 使用的語言和度量系統由**文化特性**和**UICulture**屬性。 這兩個屬性都接受 LCID 值。 如果您指定的 LCID 是受支援語言的變異語言，就會呈現最相近的語言。 如果您指定的 LCID 不受支援，而且找不到其他相近的 LCID，就會呈現英文 (美國)。  
  
## <a name="using-rsclientprint-in-code"></a>在程式碼中使用 RSClientPrint  
 **RSClientPrint**物件用來以程式設計方式存取 ActiveX 控制項及其方法和屬性。 此控制項會提供預覽列印的強制回應對話方塊。  
  
### <a name="specifying-default-values"></a>指定預設值  
 您可以初始化**列印**對話方塊邊界和頁面值的報表。 根據預設，**列印**報表定義中的值以初始化對話方塊。 您可以使用預設值，或設定物件的屬性來指定不同的值。  
  
 所有維度均以公釐表示。 如果發生於執行階段度量的轉換**文化特性**和**UICulture**會設定為不使用公制測量的地區設定。  
  
 若要了解哪些值用於頁面維度和邊界，您可以使用**GetProperties**方法來擷取預設值：  
  
-   **PageHeight**和**PageWidth**指定的預設頁面高度和寬度。 啟動列印控制項之後，就可以使用這些屬性值來選取目前選定印表機可用的最接近紙張大小。 如果**PageWidth**大於**PageHeight**，方向會設定為 橫向。 否則，就會設定為 [縱向]。  
  
-   **LeftMargin**， **RightMargin**， **TopMargin**，和**BottomMargin**都設為預設 12.2 公釐為單位。  
  
 這些屬性會儲存在**項目**報表伺服器上的屬性集合。 每次更新報表定義時，就會覆寫這些值。  
  
### <a name="rsclientprint-properties"></a>RSClientPrint 屬性  
  
|屬性|Type|RW|預設值|Description|  
|--------------|----------|--------|-------------|-----------------|  
|MarginLeft|Double|RW|報表設定|取得或設定左邊界。 如果開發人員未設定或報表中未指定，則預設值為 12.2 公釐。|  
|MarginRight|Double|RW|報表設定|取得或設定右邊界。 如果開發人員未設定或報表中未指定，則預設值為 12.2 公釐。|  
|MarginTop|Double|RW|報表設定|取得或設定上邊界。 如果開發人員未設定或報表中未指定，則預設值為 12.2 公釐。|  
|MarginBottom|Double|RW|報表設定|取得或設定下邊界。 如果開發人員未設定或報表中未指定，則預設值為 12.2 公釐。|  
|PageWidth|Double|RW|報表設定|取得或設定頁寬。 如果未設定開發人員或是報表定義的預設值是 215.9 公釐為單位。|  
|PageHeight|Double|RW|報表設定|取得或設定頁高。 如果開發人員未設定或是報表定義為 279.4 公釐，則為預設值。|  
|Culture|Int32|RW|瀏覽器地區設定|指定地區設定識別碼 (LCID)。 此值會決定使用者輸入的度量單位。 例如，如果使用者類型**3**，將會以公釐為單位測量值，如果語言為法文或英吋如果語言是英文 （美國）。 有效值包括：1028、1031、1033、1036、1040、1041、1042、2052、3082。|  
|UICulture|字串|RW|用戶端文化特性|指定對話方塊的字串當地語系化。 [列印] 對話方塊中的文字會採用下列語言的當地語系化：簡體中文、繁體中文、英文、法文、德文、義大利文、日文、韓文和西班牙文。 有效值包括：1028、1031、1033、1036、1040、1041、1042、2052、3082。|  
|Authenticate|Boolean|RW|False|指定控制項是否對報表伺服器發出 GET 命令，以起始連接來執行工作階段外的列印。|  
  
### <a name="when-to-set-the-authenticate-property"></a>何時設定驗證屬性  
 當您從列印在瀏覽器工作階段中時，您不需要設定**驗證**屬性。 在使用中工作階段的環境內，從列印控制項至報表伺服器的全部要求均透過瀏覽器來處理。 瀏覽器會設定對報表伺服器通訊的必要工作階段變數。  
  
 如果您列印出的工作階段 （例如，報表直接傳送到印表機未先開啟） 時，列印控制項必須發出 HTTP**取得**設定報表伺服器的工作階段的要求。 要發出**取得**要求您設定**驗證**至**True**。  
  
 您只需要發出**取得**要求，如果您使用 Windows 整合式安全性或基本驗證。 如果您使用表單驗證**驗證**屬性會被忽略。 您的應用程式程式碼必須設定工作階段，並使用您提供的自訂安全性延伸模組來驗證使用者。 如果您使用表單驗證，請將驗證 Cookie 的逾期值設定為可讓工作階段保留一段合理間隔時間的值。 如果此值太小，則 Cookie 每次過期時，就會提示使用者提供登入認證。  
  
### <a name="clsids"></a>CLSID  
 當您執行內部部署報表時，會使用下列 CLSID 值。  
  
-   41861299-EAB2-4DCC-986C-802AE12AC499  
  
-   5554DCB0-700B-498D-9B58-4E40E5814405  
  
-   60677965-AB8B-464f-9B04-4BA871A2F17F  
  
 當您在 Windows Azure SQL Reporting 執行報表時，會使用下列 CLSID 值。  
  
-   3DD32426-554D-48C0-A200-65D3BF880E38  
  
-   05662494-ACF9-446A-BE4C-7D3F7EA7F62F  
  
### <a name="rsprintclient-support-for-the-print-method"></a>RSPrintClient 支援 Print 方法  
 **RSClientPrint**物件支援**列印**方法用來啟動 [列印] 對話方塊。 **列印**方法具有下列引數。  
  
|引數|I/O|Type|Description|  
|--------------|----------|----------|-----------------|  
|ServerPath|In|字串|指定報表伺服器虛擬目錄 (例如， `https://adventure-works/reportserver`)。|  
|ReportPathParameters|In|字串|在報表伺服器資料夾命名空間內指定報表的全名，包括參數在內。 報表是透過 URL 存取來擷取。 例如："/AdventureWorks Sample Reports/Employee Sales Summary&EmpID=1234"|  
|ReportName|In|字串|報表的簡短名稱 (在上述範例中，簡短名稱為 Employee Sales Summary)。 它會出現在 [列印] 對話方塊及列印佇列中。|  
  
### <a name="example"></a>範例  
 下列 HTML 範例顯示如何指定.cab 檔，**列印**方法，並在 JavaScript 中的屬性：  
  
 `<BODY onload="Print()">`  
  
 `<OBJECT ID="RSClientPrint" CLASSID="CLSID: 5554DCB0-700B-498D-9B58-4E40E5814405D3" CODEBASE="<URL to the .CAB file>#Version=<your application version information>" VIEWASTEXT></OBJECT>`  
  
 `<script language="javascript">`  
  
 `function Print()`  
  
 `{`  
  
 `RSClientPrint.MarginLeft = 12.7;`  
  
 `RSClientPrint.MarginTop = 12.7;`  
  
 `RSClientPrint.MarginRight = 12.7;`  
  
 `RSClientPrint.MarginBottom = 12.7;`  
  
 `RSClientPrint.Culture = 1033;`  
  
 `RSClientPrint.UICulture = 9;`  
  
 `RSClientPrint.Print('http://localhost/rtm', '%2fEmployee_Sales_Summary&ReportMonth=6&ReportYear=2004&EmpID=20', 'Employee_Sales_Summary')`  
  
 `}`  
  
 `</script>`  
  
 `</BODY>`  
  
## <a name="see-also"></a>另請參閱  
 [從列印控制項 &#40; 的瀏覽器列印報表報表產生器及 SSRS &#41;](../../../reporting-services/report-builder/print-reports-from-a-browser-with-the-print-control-report-builder-and-ssrs.md)   
 [列印報表 &#40;報表產生器及 SSRS&#41;](../../../reporting-services/report-builder/print-reports-report-builder-and-ssrs.md)   
 [影像裝置資訊設定](../../../reporting-services/image-device-information-settings.md)  
  
  
