---
title: 設定報表伺服器上的基本驗證 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services, configuration
- Basic authentication
ms.assetid: 8faf2938-b71b-4e61-a172-46da2209ff55
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 32b46265b5da376bc974b55c48bf54bad88917d8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66102170"
---
# <a name="configure-basic-authentication-on-the-report-server"></a>設定報表伺服器的基本驗證
  根據預設，Reporting Services 會接受可指定交涉式驗證或 NTLM 驗證的要求。 如果您的部署包含了使用基本驗證的用戶端應用程式或瀏覽器，您必須將基本驗證加入支援的類型清單中。 此外，如果您要使用報表產生器，必須啟用對報表產生器檔案的匿名存取。  
  
 若要在報表伺服器上設定基本驗證，請編輯 RSReportServer.config 檔案中的 XML 元素和值。 您可以複製及貼上本主題的範例，以取代預設值。  
  
 在您啟用基本驗證之前，請確認您的安全性基礎結構有支援它。 使用基本驗證時，報表伺服器 Web 服務會將認證傳遞給本機安全性授權。 如果認證指定本機使用者帳戶，報表伺服器電腦上的本機安全性授權將會驗證這位使用者，而此使用者將會取得對於本機資源有效的安全性 Token。 網域使用者帳戶的認證會轉送給網域控制站，並由網域控制站加以驗證。 產生的票證對於網路資源而言是有效的。  
  
 如果您希望在認證傳給網路中的網域控制站的過程中，能夠減低認證被攔截的風險，就需要通道加密，例如安全通訊端層 (SSL)。 基本驗證本身會使用純文字格式傳輸使用者名稱，並使用 base64 編碼方式傳輸密碼。 加入通道加密會讓封包無法讀取。 如需詳細資訊，請參閱 [在原生模式報表伺服器上設定 SSL 連接](configure-ssl-connections-on-a-native-mode-report-server.md)。  
  
 當您啟用基本驗證之後，請注意在使用者設定外部資料來源的連線屬性，而此資料來源會提供資料給報表時，就無法選取 [Windows 整合式安全性]  選項。 資料來源屬性頁上的這個選項將會呈現灰色。  
  
> [!NOTE]  
>  下列指示用於原生模式報表伺服器。 如果您在 SharePoint 整合模式下部署報表伺服器，您必須使用可指定 Windows 整合式安全性的預設驗證設定。 報表伺服器會使用預設 Windows 驗證延伸模組中的內部功能來支援 SharePoint 整合模式下的報表伺服器。  
  
### <a name="to-configure-a-report-server-to-use-basic-authentication"></a>設定報表伺服器使用基本驗證  
  
1.  在文字編輯器中開啟 RSReportServer.config。  
  
     檔案位於* \<磁片磁碟機>：* \Program Files\Microsoft SQL Server\MSRS12。MSSQLSERVER\Reporting Services\reportserver。  
  
2.  尋找 <`Authentication`>。  
  
3.  複製下列其中一個最符合您需要的 XML 結構。 第一個 XML 結構會提供指定所有元素的預留位置，下一節會加以描述：  
  
    ```  
    <Authentication>  
          <AuthenticationTypes>  
                 <RSWindowsBasic>  
                       <LogonMethod>3</LogonMethod>  
                       <Realm></Realm>  
                       <DefaultDomain></DefaultDomain>  
                 </RSWindowsBasic>  
          </AuthenticationTypes>  
          <EnableAuthPersistence>true</EnableAuthPersistence>  
    </Authentication>  
    ```  
  
     如果您使用預設值，可以複製最小元素結構：  
  
    ```  
          <AuthenticationTypes>  
                 <RSWindowsBasic/>  
          </AuthenticationTypes>  
    ```  
  
4.  將它貼到 <`Authentication`> 的現有專案上。  
  
     如果您使用多個驗證類型，請只加入 `RSWindowsBasic` 元素，而不要刪除 `RSWindowsNegotiate`、`RSWindowsNTLM` 或 `RSWindowsKerberos` 的項目。  
  
     若要支援 Safari 瀏覽器，您無法設定報表伺服器使用多個驗證類型。 您只能指定 `RSWindowsBasic` 並刪除其他項目。  
  
     請注意，您無法搭配其他驗證類型使用 `Custom`。  
  
5.  以適用于您環境`Realm`的值取代`DefaultDomain` <> 或 <> 的空白值。  
  
6.  儲存檔案。  
  
7.  如果您設定了向外延展部署，請針對部署中的其他報表伺服器重複這些步驟。  
  
8.  重新啟動報表伺服器，清除目前開啟的任何工作階段。  
  
## <a name="rswindowsbasic-reference"></a>RSWindowsBasic 參考  
 當您設定基本驗證時，可以指定下列元素。  
  
|元素|必要|有效值|  
|-------------|--------------|------------------|  
|LogonMethod|是<br /><br /> 如果您未指定值，將會使用 3。|
  `2` = 網路登入，用於驗證純文字密碼的高效能伺服器。<br /><br /> 
  `3` = 純文字登入，可將登入認證保存在隨著每個 HTTP 要求傳送的驗證封裝中，以便在連接至網路中的其他伺服器時，允許伺服器模擬使用者。 (預設值)<br /><br /> 注意： [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]中不支援值 0 (用於互動式登入) 和 1 (用於批次登入)。|  
|Realm|選用|指定資源分割區，其中包含用於控制組織中受保護資源之存取權的授權和驗證功能。|  
|DefaultDomain|選用|指定伺服器用以驗證使用者的網域。 雖然這個值是選擇性的，但是如果您省略它，報表伺服器將使用電腦名稱當做網域。 如果電腦是網域的成員，該網域就是預設網域。 如果您在網域控制站上安裝了報表伺服器，則使用的網域就是電腦所控制的網域。|  
  
## <a name="enabling-anonymous-access-to-report-builder-application-files"></a>啟用對報表產生器應用程式檔案的匿名存取  
 報表產生器會使用 ClickOnce 技術，將應用程式檔案下載及安裝到用戶端電腦上。 當它在用戶端電腦上啟動時，ClickOnce 應用程式啟動器將會針對報表伺服器電腦上的其他應用程式檔案發出要求。 如果報表伺服器有設定基本驗證，ClickOnce 應用程式啟動器將無法通過驗證檢查，因為它不支援基本驗證。  
  
 為了解決此問題，您可以設定對報表產生器程式檔案的匿名存取。 這樣做會讓 ClickOnce 在擷取它的檔案時略過驗證檢查。 若要啟用匿名存取，請執行下列動作：  
  
-   確認報表伺服器已設定基本驗證。  
  
-   在 ReportBuilder 之下建立 bin 資料夾，並將四個組件複製到此資料夾。  
  
-   將 `IsReportBuilderAnonymousAccessEnabled` 元素加入到 RSReportServer.config，並將它設定為 `True`。 當您儲存檔案之後，報表伺服器會建立報表產生器的新端點。 端點用於內部存取程式檔案，而且在程式碼內不會有可使用的程式設計介面。 擁有個別的端點可讓報表產生器在報表伺服器服務處理序界限下，於它自己的應用程式定義域內執行。  
  
-   您可以選擇指定最低權限帳戶，在與報表伺服器不同的安全性內容之下處理要求。 這個帳戶會變成匿名帳戶，以便在報表伺服器上存取報表產生器檔案。 此帳戶會設定 ASP.NET 工作處理序內執行緒的識別。 該執行緒內執行的要求會傳遞給報表伺服器，而不需執行驗證檢查。 此帳戶相當於 Internet Information Services （IIS\<）中的 IUSR_ 機> 帳戶，可在啟用匿名存取和模擬時，用來設定 ASP.NET 工作者進程的安全性內容。 若要指定此帳戶，請將它加入報表產生器 Web.config 檔中。  
  
 如果您想要啟用對報表產生器程式檔案的匿名存取，報表伺服器必須設定基本驗證。 如果報表伺服器沒有設定成基本驗證，嘗試啟用匿名存取時，會出現錯誤。  
  
 如需驗證問題和報表產生器的詳細資訊，請參閱[設定報表產生器存取](../report-server/configure-report-builder-access.md)。  
  
#### <a name="to-configure-report-builder-access-on-a-report-server-configured-for-basic-authentication"></a>在有設定基本驗證的報表伺服器上設定報表產生器存取  
  
1.  請檢查 RSReportServer.config 檔案中的驗證設定，以確認報表伺服器有設定基本驗證。  
  
2.  在 ReportBuilder 資料夾下建立 BIN 資料夾。 根據預設，此資料夾位於 \Program Files\Microsoft SQL Server\MSRS12.MSSQLSERVER\Reporting Services\ReportServer\ReportBuilder。  
  
3.  將下列組件從 ReportServer\Bin 資料夾複製到 ReportBuilder\BIN 資料夾：  
  
     Microsoft.ReportingServices.Diagnostics.dll  
  
     Microsoft.ReportingServices.Interfaces.dll  
  
     ReportingServicesAppDomainManager.dll  
  
     RSHttpRuntime.dll  
  
4.  您可以選擇在匿名帳戶之下，建立 Web.config 檔來處理報表產生器要求：  
  
    ```  
    <?xml version="1.0" encoding="utf-8" ?>  
    <configuration>  
    <system.web>  
    <authentication mode="Windows" />    
    <identity impersonate="true " userName="username" password="password"/>  
    </system.web>  
    </configuration>  
    ```  
  
     若您包含 Web.config 檔，則驗證模式必須設定為 `Windows`。  
  
     `Identity impersonate`可以是`True`或`False`。  
  
    -   如果您不希望 ASP.NET 讀取安全性 Token，請將它設定為 `False`。 此要求將會在報表伺服器服務的安全性內容中執行。  
  
    -   如果您希望 ASP.NET 從主機層級讀取安全性 Token，請將它設定為 `True`。 如果您將它設定為 `True`，也必須指定 `userName` 和 `password` 來指派匿名帳戶。 您所指定的認證將會決定要求發出所在的安全性內容。  
  
5.  將 Web.config 檔儲存到 ReportBuilder\bin 資料夾。  
  
6.  開啟 RSReportServer.config 檔案，並在 Services 區段中尋找 `IsReportManagerEnabled`，然後在它的下方加入以下設定：  
  
    ```  
    <IsReportBuilderAnonymousAccessEnabled>True</IsReportBuilderAnonymousAccessEnabled>  
    ```  
  
7.  儲存 RSReportServer.config 並關閉檔案。  
  
8.  重新啟動報表伺服器。  
  
## <a name="see-also"></a>另請參閱  
 [報表伺服器應用程式的應用程式域](../report-server/application-domains-for-report-server-applications.md)   
 [Reporting Services 安全性與保護](reporting-services-security-and-protection.md)  
  
  
