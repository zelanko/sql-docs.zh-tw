---
title: "設定報表伺服器上的基本驗證 | Microsoft Docs"
ms.custom: 
ms.date: 08/26/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Reporting Services, configuration
- Basic authentication
ms.assetid: 8faf2938-b71b-4e61-a172-46da2209ff55
caps.latest.revision: "28"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.openlocfilehash: bfadbdb617198fe04b789d0d1d6589f4af2d887f
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="configure-basic-authentication-on-the-report-server"></a>設定報表伺服器上的基本驗證
  根據預設，Reporting Services 會接受可指定交涉式驗證或 NTLM 驗證的要求。 如果您的部署包含了使用基本驗證的用戶端應用程式或瀏覽器，您必須將基本驗證加入支援的類型清單中。 此外，如果您要使用報表產生器，必須啟用對報表產生器檔案的匿名存取。  
  
 若要在報表伺服器上設定基本驗證，請編輯 RSReportServer.config 檔案中的 XML 元素和值。 您可以複製及貼上本主題的範例，以取代預設值。  
  
 在您啟用基本驗證之前，請確認您的安全性基礎結構有支援它。 使用基本驗證時，報表伺服器 Web 服務會將認證傳遞給本機安全性授權。 如果認證指定本機使用者帳戶，報表伺服器電腦上的本機安全性授權將會驗證這位使用者，而此使用者將會取得對於本機資源有效的安全性 Token。 網域使用者帳戶的認證會轉送給網域控制站，並由網域控制站加以驗證。 產生的票證對於網路資源而言是有效的。  
  
 如果您希望在認證傳給網路中的網域控制站的過程中，能夠減低認證被攔截的風險，就需要通道加密，例如安全通訊端層 (SSL)。 基本驗證本身會使用純文字格式傳輸使用者名稱，並使用 base64 編碼方式傳輸密碼。 加入通道加密會讓封包無法讀取。 如需詳細資訊，請參閱 [在原生模式報表伺服器上設定 SSL 連接](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md)。  
  
 當您啟用基本驗證之後，請注意在使用者設定外部資料來源的連線屬性，而此資料來源會提供資料給報表時，就無法選取 [Windows 整合式安全性] 選項。 資料來源屬性頁上的這個選項將會呈現灰色。  
  
> [!NOTE]  
>  下列指示用於原生模式報表伺服器。 如果您在 SharePoint 整合模式下部署報表伺服器，您必須使用可指定 Windows 整合式安全性的預設驗證設定。 報表伺服器會使用預設 Windows 驗證延伸模組中的內部功能來支援 SharePoint 整合模式下的報表伺服器。  
  
### <a name="to-configure-a-report-server-to-use-basic-authentication"></a>設定報表伺服器使用基本驗證  
  
1.  在文字編輯器中開啟 RSReportServer.config。  
  
     此檔案位於 \<磁碟機>:\Program Files\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\ReportServer。  
  
2.  尋找 \<**驗證**>。  
  
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
  
4.  將它貼到 \<**驗證**> 的現有項目上。  
  
     如果您使用多個驗證類型，請只加入 **RSWindowsBasic** 元素，而不要刪除 **RSWindowsNegotiate**、 **RSWindowsNTLM**或 **RSWindowsKerberos**的項目。  
  
     請注意，您無法搭配其他驗證類型使用 **Custom** 。  
  
5.  使用對環境有效的值來取代 \<**Realm**> 或 \<**DefaultDomain**> 的空白值。  
  
6.  儲存檔案。  
  
7.  如果您設定了向外延展部署，請針對部署中的其他報表伺服器重複這些步驟。  
  
8.  重新啟動報表伺服器，清除目前開啟的任何工作階段。  
  
## <a name="rswindowsbasic-reference"></a>RSWindowsBasic 參考  
 當您設定基本驗證時，可以指定下列元素。  
  
|元素|必要項|有效的值|  
|-------------|--------------|------------------|  
|LogonMethod|是<br /><br /> 如果您未指定值，將會使用 3。|**2** = 網路登入，用於驗證純文字密碼的高效能伺服器。<br /><br /> **3** = 純文字登入，可將登入認證保存在隨著每個 HTTP 要求傳送的驗證封裝中，以便在連接至網路中的其他伺服器時，允許伺服器模擬使用者。 (預設值)<br /><br /> 注意： **中** 不 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]支援值 0 (用於互動式登入) 和 1 (用於批次登入)。|  
|Realm|選擇性|指定資源分割區，其中包含用於控制組織中受保護資源之存取權的授權和驗證功能。|  
|DefaultDomain|選擇性|指定伺服器用以驗證使用者的網域。 雖然這個值是選擇性的，但是如果您省略它，報表伺服器將使用電腦名稱當做網域。 如果電腦是網域的成員，該網域就是預設網域。 如果您在網域控制站上安裝了報表伺服器，則使用的網域就是電腦所控制的網域。|  
  
## <a name="see-also"></a>另請參閱  
 [報表伺服器應用程式的應用程式網域](../../reporting-services/report-server/application-domains-for-report-server-applications.md)   
 [Reporting Services 安全性與保護](../../reporting-services/security/reporting-services-security-and-protection.md)  
  
  
