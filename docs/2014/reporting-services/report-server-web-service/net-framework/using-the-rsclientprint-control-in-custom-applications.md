---
title: 在自訂應用程式中使用 RSClientPrint 控制項 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- RSPrintClient control
- print controls [Reporting Services]
- custom printing [Reporting Services]
- client-side printing
ms.assetid: 8c0bdd18-8905-4e22-9774-a240fc81a8a7
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 0cddac844ac9603da32a4fabc47fa71a8ddcd226
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56036599"
---
# <a name="using-the-rsclientprint-control-in-custom-applications"></a>在自訂應用程式中使用 RSClientPrint 控制項
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] ActiveX 控制項 **RSPrintClient** 提供在 HTML 檢視器中檢視的報表之用戶端列印。 它提供 [列印] 對話方塊，讓使用者能夠起始列印工作、預覽報表、指定要列印的頁面，以及變更邊界。 在用戶端列印作業期間，報表伺服器會在影像 (EMF) 轉譯延伸模組中轉譯報表，然後使用作業系統的列印功能來建立列印工作，並將它傳送到印表機。  
  
 用戶端列印提供控制及改善 HTML 報表的列印輸出品質的方式，亦即，利用使用者電腦上的瀏覽器列印設定，而不使用報表的頁面維度、邊界、頁首和頁尾文字，來建立列印輸出。 列印控制項會讀取報表的屬性值，來設定頁面的大小和邊界。  
  
 想要在協力廠商工具列或檢視器上啟用用戶端列印功能的開發人員，可以透過 **RSClientPrint** COM 物件來存取 ActiveX 控制項。 此控制項可以自由散發。 下列清單提供使用此控制項的一些建議：  
  
-   使用此控制項即可改善網路架構報表的列印功能。 您可以用 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 相容的程式設計語言或指令碼，來指定物件。 此控制項並不是要用於 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows Form 應用程式。  
  
-   從 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 程式檔案複製 .cab 檔，然後將它加入自訂應用程式的程式碼庫。  
  
-   使用 \<OBJECT> 標記即可指定控制項。  
  
-   在 OBJECT CODEBASE 屬性中，指定 .cab 檔的相對 URL 或完整 URL。  
  
-   對 .cab 檔指定您自己的應用程式版本資訊，以追蹤在應用程式中使用的版本。  
  
-   檢閱關於影像 (EMF) 轉譯的線上叢書主題，以了解如何轉譯頁面來進行預覽列印和輸出。  
  
## <a name="rsprintclient-overview"></a>RSPrintClient 概觀  
 控制項會顯示自訂列印對話方塊，其中支援與其他列印對話方塊一樣的一般功能，包括預覽列印、可指定要列印的特定頁面及範圍、頁面邊界和列印方向等選擇。 此控制項已封裝成 CAB 檔。 [列印] 對話方塊中的文字，已當地語系化成 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 支援的所有語言。 **RSPrintClient** ActiveX 控制項會使用影像轉譯延伸模組 (EMF) 來列印報表。 會使用下列 EMF 裝置資訊：StartPage、 EndPage、 MarginBottom、 MarginLeft、 MarginTop、 MarginRight、 PageHeight 和 PageWidth。 影像轉譯的其他裝置資訊設定則不支援。  
  
### <a name="language-support"></a>語言支援  
 列印控制項會以不同的語言呈現使用者介面文字，並接受根據不同度量系統所輸入的值。 所使用的語言和度量系統是由 **Culture** 和 **UICulture** 屬性來決定。 這兩個屬性都接受 LCID 值。 如果您指定的 LCID 是受支援語言的變異語言，就會呈現最相近的語言。 如果您指定的 LCID 不受支援，而且找不到其他相近的 LCID，就會呈現英文 (美國)。  
  
## <a name="using-rsclientprint-in-code"></a>在程式碼中使用 RSClientPrint  
 **RSClientPrint** 物件的作用，是可以透過程式設計的方式存取 ActiveX 控制項及其方法和屬性。 此控制項會提供預覽列印的強制回應對話方塊。  
  
### <a name="specifying-default-values"></a>指定預設值  
 您可以利用報表的邊界和頁面值，將 [列印] 對話方塊初始化。 根據預設，[列印] 對話方塊會以報表定義的值初始化。 您可以使用預設值，或設定物件的屬性來指定不同的值。  
  
 所有維度均以公釐表示。 如果 **Culture** 與 **UICulture** 已設定為不使用公制度量的地區，則度量的轉換會在執行階段發生。  
  
 若要了解哪些值用於頁面維度和邊界，您可以使用 **GetProperties** 方法來擷取預設值：  
  
-   **PageHeight** 和 **PageWidth** 會指定預設頁高和頁寬。 啟動列印控制項之後，就可以使用這些屬性值來選取目前選定印表機可用的最接近紙張大小。 如果 **PageWidth** 大於 **PageHeight**，列印方向就會設定為 [橫向]。 否則，就會設定為 [縱向]。  
  
-   根據預設，**LeftMargin**、**RightMargin**、**TopMargin** 和 **BottomMargin** 全部都設定為 12.2 公釐。  
  
 這些屬性是儲存在報表伺服器上的 **Item** 屬性集合內。 每次更新報表定義時，就會覆寫這些值。  
  
### <a name="rsclientprint-properties"></a>RSClientPrint 屬性  
  
|屬性|類型|RW|預設|描述|  
|--------------|----------|--------|-------------|-----------------|  
|MarginLeft|Double|RW|報表設定|取得或設定左邊界。 如果開發人員未設定或報表中未指定，則預設值為 12.2 公釐。|  
|MarginRight|Double|RW|報表設定|取得或設定右邊界。 如果開發人員未設定或報表中未指定，則預設值為 12.2 公釐。|  
|MarginTop|Double|RW|報表設定|取得或設定上邊界。 如果開發人員未設定或報表中未指定，則預設值為 12.2 公釐。|  
|MarginBottom|Double|RW|報表設定|取得或設定下邊界。 如果開發人員未設定或報表中未指定，則預設值為 12.2 公釐。|  
|PageWidth|Double|RW|報表設定|取得或設定頁寬。 如果開發人員未設定或是報表定義為 215.9 公釐，則為預設值。|  
|PageHeight|Double|RW|報表設定|取得或設定頁高。 如果開發人員未設定或是報表定義為 279.4 公釐，則為預設值。|  
|Culture|Int32|RW|瀏覽器地區設定|指定地區設定識別碼 (LCID)。 此值會決定使用者輸入的度量單位。 例如，如果使用者輸入`3`，值的度量單位是公釐，若語言為法文，或如果語言是英文 （美國） 英吋。 有效值包括：1028, 1031, 1033, 1036, 1040, 1041, 1042, 2052, 3082.|  
|UICulture|String|RW|用戶端文化特性|指定對話方塊的字串當地語系化。 在 [列印] 對話方塊中的文字會當地語系化成下列語言：簡體中文、 中文繁體、 英文、 法文、 德文、 義大利文、 日文、 韓文和西班牙文。 有效值包括：1028, 1031, 1033, 1036, 1040, 1041, 1042, 2052, 3082.|  
|Authenticate|布林|RW|False|指定控制項是否對報表伺服器發出 GET 命令，以起始連接來執行工作階段外的列印。|  
  
### <a name="when-to-set-the-authenticate-property"></a>何時設定驗證屬性  
 當您在瀏覽器工作階段中列印時，不必設定 `Authenticate` 屬性。 在使用中工作階段的環境內，從列印控制項至報表伺服器的全部要求均透過瀏覽器來處理。 瀏覽器會設定對報表伺服器通訊的必要工作階段變數。  
  
 如果在工作階段外列印 (例如，未先開啟報表，就直接將報表傳送到印表機)，列印控制項必須發出 HTTP `GET` 要求，以設定與報表伺服器之間的工作階段。 若要發出 `GET` 要求，請將 `Authenticate` 設定為 `True`。  
  
 唯有使用 Windows 整合式安全性或基本驗證時，才需要發出 `GET` 要求。 如果您使用表單驗證，則會忽略 `Authenticate` 屬性。 您的應用程式程式碼必須設定工作階段，並使用您提供的自訂安全性延伸模組來驗證使用者。 如果您使用表單驗證，請將驗證 Cookie 的逾期值設定為可讓工作階段保留一段合理間隔時間的值。 如果此值太小，則 Cookie 每次過期時，就會提示使用者提供登入認證。  
  
### <a name="clsids"></a>CLSID  
 當您執行內部部署報表時，會使用下列 CLSID 值。  
  
-   41861299-EAB2-4DCC-986C-802AE12AC499  
  
-   5554DCB0-700B-498D-9B58-4E40E5814405  
  
-   60677965-AB8B-464f-9B04-4BA871A2F17F  
  
 當您在 Windows Azure SQL Reporting 執行報表時，會使用下列 CLSID 值。  
  
-   3DD32426-554D-48C0-A200-65D3BF880E38  
  
-   05662494-ACF9-446A-BE4C-7D3F7EA7F62F  
  
### <a name="rsprintclient-support-for-the-print-method"></a>RSPrintClient 支援 Print 方法  
 **RSClientPrint** 物件支援用來啟動 [列印] 對話方塊的 **Print** 方法。 **Print** 方法具有下列引數。  
  
|引數|I/O|類型|描述|  
|--------------|----------|----------|-----------------|  
|ServerPath|In|String|指定報表伺服器虛擬目錄 (例如 https://adventure-works/reportserver)。|  
|ReportPathParameters|In|String|在報表伺服器資料夾命名空間內指定報表的全名，包括參數在內。 報表是透過 URL 存取來擷取。 例如："/AdventureWorks Sample Reports/Employee Sales Summary&EmpID=1234"|  
|ReportName|In|String|報表的簡短名稱 (在上述範例中，簡短名稱為 Employee Sales Summary)。 它會出現在 [列印] 對話方塊及列印佇列中。|  
  
### <a name="example"></a>範例  
 下列 HTML 範例顯示如何在 JavaScript 中指定 .cab 檔、**Print** 方法和屬性：  
  
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
 [使用列印控制項從瀏覽器列印報表 &#40;報表產生器及 SSRS&#41;](../../report-builder/print-reports-from-a-browser-with-the-print-control-report-builder-and-ssrs.md)   
 [列印報表 &#40;報表產生器及 SSRS&#41;](../../report-builder/print-reports-report-builder-and-ssrs.md)   
 [影像裝置資訊設定](../../image-device-information-settings.md)  
  
  
