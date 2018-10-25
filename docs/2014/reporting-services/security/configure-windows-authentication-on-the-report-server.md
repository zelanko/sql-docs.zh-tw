---
title: 設定報表伺服器上的 Windows 驗證 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Windows authentication [Reporting Services]
- Reporting Services, configuration
ms.assetid: 4de9c3dd-0ee7-49b3-88bb-209465ca9d86
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: b0ce020f0d3df8b91591daf083748f909edbb1e7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48116340"
---
# <a name="configure-windows-authentication-on-the-report-server"></a>設定報表伺服器上的 Windows 驗證
  依預設， [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 會接受可指定交涉驗證或 NTLM 驗證的要求。 如果您的部署包括了使用這些安全性提供者的用戶端應用程式和瀏覽器，您可以使用預設值，而不需要進行額外的組態設定。 如果您想要針對 Windows 整合式安全性使用不同的安全性提供者 (例如，如果您想要直接使用 Kerberos)，或是您修改了預設值而且想要還原原始設定，您可以使用本主題的資訊來指定報表伺服器上的驗證設定。  
  
 若要使用 Windows 整合式安全性，每一個需要存取報表伺服器的使用者都必須擁有有效的 Windows 本機或網域使用者帳戶，或者必須是 Windows 本機或網域群組帳戶的成員。 您可以將其他信任網域中的帳戶包括在內。 這些帳戶必須對報表伺服器電腦擁有存取權，且必須接著指派給角色，以取得特定報表伺服器作業的存取權。  
  
 也必須符合下列其他需求：  
  
-   RSeportServer.config 檔案必須將`AuthenticationType`設定為`RSWindowsNegotiate`， `RSWindowsKerberos`，或`RSWindowsNTLM`。 根據預設，如果報表伺服器服務帳戶是 NetworkService 或 LocalSystem，RSReportServer.config 檔就會包含 `RSWindowsNegotiate` 設定。否則，就會使用 `RSWindowsNTLM` 設定。 如果您的應用程式只使用 Kerberos 驗證，您可以加入 `RSWindowsKerberos`。  
  
    > [!IMPORTANT]  
    >  使用`RSWindowsNegotiate`如果您設定報表伺服器服務的網域使用者帳戶下執行，而且您並未註冊服務主體名稱 (SPN) 帳戶，將會導致 Kerberos 驗證錯誤。 如需詳細資訊，請參閱本主題的 [在連接報表伺服器時解決 Kerberos 驗證錯誤](#proxyfirewallRSWindowsNegotiate) 。  
  
-   [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 必須設定 Windows 驗證。 根據預設，報表伺服器 Web 服務和報表管理員的 Web.config 檔案包含\<mode ="Windows"> 設定。 如果您將它變更為 \<authentication mode="Forms">，[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的 Windows 驗證將會失敗。  
  
-   報表伺服器 Web 服務的 Web.config 檔案，且必須是報表管理員\<identity impersonate ="true"/ >。  
  
-   用戶端應用程式或瀏覽器必須支援 Windows 整合式安全性。  
  
 若要變更報表伺服器驗證設定，請編輯 RSReportServer.config 檔案中的 XML 元素和值。 您可以複製及貼上本主題的範例，以實作特定的組合。  
  
 如果所有的用戶端和伺服器電腦全都位於相同網域或信任網域，或是公司防火牆後方已部署報表伺服器供內部網路存取使用，預設值便可達到最佳的效果。 若要傳遞 Windows 認證，網域必須是受信任的網域或單一網域。 伺服器必須啟用 Kerberos 第 5 版通訊協定，才能多次傳遞認證。 否則，認證在逾期前僅能傳遞一次。 如需有關如何設定多個電腦連接之認證的詳細資訊，請參閱 <<c0> [ 指定的認證和報表資料來源的連接資訊](../report-data/specify-credential-and-connection-information-for-report-data-sources.md)。  
  
 下列指示用於原生模式報表伺服器。 如果您在 SharePoint 整合模式下部署報表伺服器，您必須使用可指定 Windows 整合式安全性的預設驗證設定。 報表伺服器會使用預設 Windows 驗證延伸模組中的內部功能來支援 SharePoint 整合模式下的報表伺服器。  
  
## <a name="extended-protection-for-authentication"></a>驗證擴充保護  
 從 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]開始，就有驗證擴充保護的支援可以使用。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能可支援使用通道繫結和服務繫結，以增強驗證的保護。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 功能需要搭配支援擴充保護的作業系統使用。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 擴充保護的組態是由 RSReportServer.config 檔案中的設定所決定。 若要更新這個檔案，您可以編輯檔案或使用 WMI API。 如需詳細資訊，請參閱 < [Reporting services 的驗證擴充保護](extended-protection-for-authentication-with-reporting-services.md)。  
  
### <a name="to-configure-a-report-server-to-use-windows-integrated-security"></a>若要設定報表伺服器使用 Windows 整合式安全性  
  
1.  在文字編輯器中開啟 RSReportServer.config。  
  
2.  尋找 <`Authentication`>。  
  
3.  複製下列其中一個最符合您需要的 XML 結構。 您可以指定`RSWindowsNegotiate`， `RSWindowsNTLM`，和`RSWindowsKerberos`依任何順序。 如果您想要驗證連接而不是每一個個別要求，則應該啟用驗證持續性。 在驗證持續性之下，將會在連接的持續時間內允許要求驗證的所有要求。  
  
     當報表伺服器服務帳戶是 NetworkService 或 LocalSystem 時，第一個 XML 結構是預設的組態：  
  
    ```  
    <Authentication>  
          <AuthenticationTypes>  
                 <RSWindowsNegotiate />  
          </AuthenticationTypes>  
          <EnableAuthPersistence>true</EnableAuthPersistence>  
    </Authentication>  
    ```  
  
     當報表伺服器服務帳戶不是 NetworkService 或 LocalSystem 時，第二個 XML 結構是預設的組態：  
  
    ```  
    <Authentication>  
          <AuthenticationTypes>  
                 <RSWindowsNTLM />  
          </AuthenticationTypes>  
          <EnableAuthPersistence>true</EnableAuthPersistence>  
    ```  
  
     \</驗證>  
  
     第三個 XML 結構會指定用於 Windows 整合式安全性的所有安全性封裝：  
  
    ```  
          <AuthenticationTypes>  
                 <RSWindowsNegotiate />  
                 <RSWindowsKerberos />  
                 <RSWindowsNTLM />  
          </AuthenticationTypes>  
    ```  
  
     第四個 XML 結構只會針對不支援 Kerberos 的部署指定 NTLM，或是暫時解決 Kerberos 驗證錯誤：  
  
    ```  
          <AuthenticationTypes>  
                 <RSWindowsNTLM />  
          </AuthenticationTypes>  
    ```  
  
4.  貼上現有的項目，如 <`Authentication`>。  
  
     請注意，您不能搭配 `Custom` 型別使用 `RSWindows`。  
  
5.  修改為擴充保護的適當設定。 預設會停用擴充保護。  如果這些項目不存在，目前的電腦可能未執行支援擴充保護的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 版本。 如需詳細資訊，請參閱＜ [Extended Protection for Authentication with Reporting Services](extended-protection-for-authentication-with-reporting-services.md)＞  
  
    ```  
          <RSWindowsExtendedProtectionLevel>Allow</RSWindowsExtendedProtectionLevel>  
          <RSWindowsExtendedProtectionScenario>Proxy</RSWindowsExtendedProtectionScenario>  
    ```  
  
6.  儲存檔案。  
  
7.  如果您設定了向外延展部署，請針對部署中的其他報表伺服器重複這些步驟。  
  
8.  重新啟動報表伺服器，清除目前開啟的任何工作階段。  
  
##  <a name="proxyfirewallRSWindowsNegotiate"></a> 連接到報表伺服器時解決 Kerberos 驗證錯誤  
 在設定交涉式驗證或 Kerberos 驗證的報表伺服器上，如果發生 Kerberos 驗證錯誤，與報表伺服器的用戶端連接將會失敗。 目前已知以下情況下會發生 Kerberos 驗證錯誤：  
  
-   報表伺服器服務以 Windows 網域使用者帳戶的身分執行，而且您並未針對此帳戶註冊服務主要名稱 (SPN)。  
  
-   使用 `RSWindowsNegotiate` 設定來設定報表伺服器。  
  
-   瀏覽器在它傳送給報表伺服器之要求的驗證標頭中優先選擇 Kerberos (勝於 NTLM)。  
  
 如果您啟用 Kerberos 記錄，就可以偵測此錯誤。 此錯誤的其他徵兆是系統會提示您輸入多次認證，然後您會看到空白瀏覽器視窗。  
  
 您可以確認您遇到了 Kerberos 驗證錯誤藉由移除 < `RSWindowsNegotiate` / > 從您的組態檔，然後重新嘗試連接。  
  
 在您確認問題之後，可以透過以下方式來解決：  
  
-   使用網域使用者帳戶為報表伺服器服務註冊 SPN。 如需詳細資訊，請參閱[為報表伺服器註冊服務主體名稱 &#40;SPN&#41;](../report-server/register-a-service-principal-name-spn-for-a-report-server.md)。  
  
-   變更服務帳戶，以便在類似網路服務的內建帳戶下執行。 內建帳戶會將 HTTP SPN 對應到主機 SPN (當您將電腦加入網路時會加以定義)。 如需詳細資訊，請參閱[設定服務帳戶 &#40;SSRS 設定管理員&#41;](../../sql-server/install/configure-a-service-account-ssrs-configuration-manager.md)。  
  
-   使用 NTLM。 當 Kerberos 驗證失敗時，NTLM 通常會正常運作。 若要使用 NTLM，移除`RSWindowsNegotiate`從 RSReportServer.config 檔案，並確認只有`RSWindowsNTLM`指定。 如果您選擇這個方法，您可以繼續針對報表伺服器服務使用網域使用者帳戶，即使您未針對此帳戶定義 SPN。  
  
#### <a name="logging-information"></a>記錄資訊  
 有幾個記錄資訊來源可幫助解決 Kerberos 相關問題。  
  
##### <a name="user-account-control-attribute"></a>User-Account-Control 屬性  
 判斷 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務帳戶是否在 Active Directory 中設定足夠的屬性。 檢閱 Reporting Services 服務追蹤記錄檔，以尋找為 UserAccountControl 屬性記錄的值。 記錄的值是十進位格式。 您需要將此十進位值轉換成十六進位格式，然後在描述 User-Account-Control 屬性的 MSDN 主題中尋找該值。  
  
-   Reporting Services 服務追蹤記錄項目將會尋找類似以下的項目：  
  
    ```  
    appdomainmanager!DefaultDomain!8f8!01/14/2010-14:42:28:: i INFO: The UserAccountControl value for the service account is 590336  
    ```  
  
-   將此十進位值轉換成十六進位格式的一個選項是使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 計算機。 Windows 計算機支援可顯示 'Dec' 選項和 'Hex' 選項的幾個模式。 選取 'Dec' 選項、貼上或輸入您在記錄檔中找到的十進位值，然後選取 'Hex' 選項。  
  
-   然後參考 [User-Account-Control Attribute](http://go.microsoft.com/fwlink/?LinkId=183366) (User-Account-Control 屬性) 主題來衍生服務帳戶的屬性。  
  
##### <a name="spns-configured-in-active-directory-for-the-reporting-services-service-account"></a>Active Directory 中針對 ssRSnoversion 服務帳戶所設定的 SPN。  
 若要在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務追蹤記錄檔中記錄 SPN，您可以暫時啟用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 擴充保護功能。  
  
-   修改組態檔`rsreportserver.config`藉由將下列設定：  
  
    ```  
    <RSWindowsExtendedProtectionLevel>Allow</RSWindowsExtendedProtectionLevel>   
    <RSWindowsExtendedProtectionScenario>Any</RSWindowsExtendedProtectionScenario>  
    ```  
  
-   重新啟動 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務，並在追蹤記錄檔中尋找類似以下的項目：  
  
    ```  
    rshost!rshost!e44!01/14/2010-14:43:51:: i INFO: Registered valid SPNs list for endpoint 2: rshost!rshost!e44!01/14/2010-14:43:52:: i INFO: SPN Whitelist Added <Explicit> - <HTTP/sqlpod064-13.w2k3.net>.  
    ```  
  
-   \<明確> 底下的值將會包含 Active Directory 中針對 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務帳戶設定的 SPN。  
  
 如果您不想要繼續使用擴充保護，請將組態值設回預設值，並重新啟動 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務帳戶。  
  
```  
<RSWindowsExtendedProtectionLevel>Off</RSWindowsExtendedProtectionLevel>  
<RSWindowsExtendedProtectionScenario>Proxy</RSWindowsExtendedProtectionScenario>  
```  
  
 如需詳細資訊，請參閱[與 Reporting Services 的驗證擴充保護](extended-protection-for-authentication-with-reporting-services.md)  
  
#### <a name="how-the-browser-chooses-negotiated-kerberos-or-negotiated-ntlm"></a>瀏覽器如何選擇交涉式 Kerberos 或交涉式 NTLM  
 當您使用 Internet Explorer 連接報表伺服器時，它會在驗證標頭上指定交涉式 Kerberos 或 NTLM。 在以下情況下會使用 NTLM 取代 Kerberos：  
  
-   此要求會傳送給本機報表伺服器。  
  
-   此要求會傳送到報表伺服器電腦的 IP 位址，而不是主機標頭或伺服器名稱。  
  
-   防火牆軟體會封鎖用於 Kerberos 驗證的通訊埠。  
  
-   特定伺服器的作業系統未啟用 Kerberos。  
  
-   網域包括舊版 Windows 用戶端和伺服器作業系統，這些版本不支援內建在新版作業系統中的 Kerberos 驗證功能。  
  
 此外，Internet Explorer 可能會選擇交涉式 Kerberos 或 NTLM (根據您設定 URL、LAN 和 Proxy 設定的方式而定)。  
  
###### <a name="report-server-url"></a>報表伺服器 URL  
 如果此 URL 包含完整網域名稱，Internet Explorer 會選取 NTLM。 如果此 URL 指定 localhost，Internet Explorer 會選取 NTLM。 如果此 URL 指定電腦的網路名稱，Internet Explorer 會選取交涉，這樣會根據報表伺服器服務帳戶是否有 SPN 存在而成功或失敗。  
  
###### <a name="lan-and-proxy-settings-on-the-client"></a>用戶端上的 LAN 和 Proxy 設定  
 您在 Internet Explorer 中設定的 LAN 和 Proxy 設定可以決定是否優先選擇 NTLM (勝於 Kerberos)。 但是，由於組織之間的 LAN 和 Proxy 設定會有所差異，所以無法精確判斷造成 Kerberos 驗證錯誤的確切設定為何。 例如，您的組織可能會強制 Proxy 設定，這些設定會將 URL 從內部網路 URL 轉換成完整網域名稱 URL (透過網際網路連接來解析)。 如果將不同的驗證提供者用於不同類型的 URL，您可能會發現當您預期某些連接應該會失敗時，這些連接卻成功了。  
  
 如果您遇到連接錯誤，而您認為這些錯誤是因為驗證失敗而發生，您可以嘗試 LAN 和 Proxy 設定的不同組合來隔離問題。 在 Internet Explorer 中，LAN 和 Proxy 設定位於 [區域網路 (LAN) 設定] 對話方塊上，您可以在 [網際網路選項] 的 [連線] 索引標籤上按一下 [區域網路設定] 來開啟此對話方塊。  
  
## <a name="external-resources"></a>外部資源  
  
-   如需 Kerberos 和報表伺服器的其他資訊，請參閱 [Deploying a Business Intelligence Solution Using SharePoint, Reporting Services, and PerformancePoint Monitoring Server with Kerberos](http://go.microsoft.com/fwlink/?LinkID=177751)(搭配 Kerberos 使用 SharePoint、Reporting Services 與 PerformancePoint 監控伺服器部署商業智慧方案)。  
  
## <a name="see-also"></a>另請參閱  
 [使用報表伺服器驗證](authentication-with-the-report-server.md)   
 [在原生模式報表伺服器上授與權限](granting-permissions-on-a-native-mode-report-server.md)   
 [RSReportServer 組態檔](../report-server/rsreportserver-config-configuration-file.md)   
 [設定報表伺服器上的 基本驗證](configure-basic-authentication-on-the-report-server.md)   
 [設定報表伺服器上的自訂或表單驗證](configure-custom-or-forms-authentication-on-the-report-server.md)   
 [Reporting Services 的驗證擴充保護](extended-protection-for-authentication-with-reporting-services.md)  
  
  
