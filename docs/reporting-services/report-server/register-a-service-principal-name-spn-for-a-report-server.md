---
title: "註冊報表伺服器的服務主體名稱 (SPN) |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: dda91d4f-77cc-4898-ad03-810ece5f8e74
caps.latest.revision: 7
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 9518d1bd3ee166a0f21292ca08130214afc841be
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---
# <a name="register-a-service-principal-name-spn-for-a-report-server"></a>為報表伺服器註冊服務主要名稱 (SPN)
  如果您在使用 Kerberos 通訊協定進行相互驗證的網路中部署 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]，當您想要將報表伺服器服務設定為以網域使用者帳戶的身分執行時，必須為此服務建立服務主要名稱 (SPN)。  
  
## <a name="about-spns"></a>關於 SPN  
 SPN 是使用 Kerberos 驗證之網路上某項服務的唯一識別碼。 它是由服務類別、主機名稱和通訊埠所組成。 在使用 Kerberos 驗證的網路上，伺服器的 SPN 必須在內建的電腦帳戶 (如 NetworkService 或 LocalSystem) 或使用者帳戶下註冊。 內建帳戶會自動註冊 SPN。 但是，當您在網域使用者帳戶下執行服務時，您必須針對您想要使用的帳戶手動註冊 SPN。  
  
 若要建立 SPN，可以使用 **SetSPN** 命令列公用程式。 如需詳細資訊，請參閱下列內容：  
  
-   [Setspn](http://technet.microsoft.com/library/cc731241\(WS.10\).aspx) (http://technet.microsoft.com/library/cc731241(WS.10).aspx)。  
  
-   [Service Principal Names (SPNs) SetSPN Syntax (Setspn.exe)](http://social.technet.microsoft.com/wiki/contents/articles/717.service-principal-names-spns-setspn-syntax-setspn-exe.aspx) (服務主體名稱 (SPN) SetSPN 語法 (Setspn.exe)) (http://social.technet.microsoft.com/wiki/contents/articles/717.service-principal-names-spns-setspn-syntax-setspn-exe.aspx)。  
  
 您必須是網域管理員，才能在網域控制站上執行此公用程式。  
  
## <a name="syntax"></a>語法  
 使用 SetSPN 公用程式來建立報表伺服器之 SPN 的命令語法如下：  
  
```  
Setspn -s http/<computername>.<domainname>:<port> <domain-user-account>  
```  
  
 Windows Server 上提供**SetSPN** 。 **-s** 引數會在確認沒有重複存在之後加入 SPN。 **注意：-s** 從 Windows Server 2008 開始已可於 Windows Server 中使用。  
  
 **HTTP** 為服務類別。 報表伺服器 Web 服務會在 HTTP.SYS 中執行。 依據產品建立適用於 HTTP 的 SPN 就是指相同電腦上在 HTTP.SYS 中執行的所有 Web 應用程式 (包括 IIS 內主控的應用程式) 都將根據網域使用者帳戶來被授與票證。 如果這些服務在不同的帳戶下執行，驗證要求將會失敗。 為了避免這個問題，請務必在相同的帳戶下設定所有要執行的 HTTP 應用程式，或是考慮為每一個應用程式建立主機標頭，然後再為每一個主機標頭建立個別的 SPN。 當您設定主機標頭時，不論 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態為何，都需要進行 DNS 變更。  
  
 您為指定的值\< *computername*>， \< *domainname*>，並\<*連接埠*> 識別主控報表伺服器之電腦的唯一網路位址。 這個值可以是本機主機名稱或完整網域名稱 (FQDN)。 如果您只有一個網域，並使用連接埠 80，您可以省略\< *domainname*> 和\<*連接埠*> 從命令列。 \<*網域使用者帳戶*> 是用以執行報表伺服器服務以及必須註冊 SPN 的使用者帳戶。  
  
## <a name="register-an-spn-for-domain-user-account"></a>為網域使用者帳戶註冊 SPN  
  
#### <a name="to-register-an-spn-for-a-report-server-service-running-as-a-domain-user"></a>若要以網域使用者的身分為報表伺服器服務註冊 SPN  
  
1.  以網域使用者帳戶的身分安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ，並設定要執行的報表伺服器服務。 請注意，要等到您完成下列步驟以後，您才能夠連接報表伺服器。  
  
2.  以網域管理員的身分登入網域控制站。  
  
3.  開啟 [命令提示字元] 視窗。  
  
4.  複製下列命令，使用對您的網路有效的實際值來取代預留位置值：  
  
    ```  
    Setspn -s http/<computer-name>.<domain-name>:<port> <domain-user-account>  
    ```  
  
     例如： `Setspn -s http/MyReportServer.MyDomain.com:80 MyDomainUser`  
  
5.  執行此命令。  
  
6.  開啟 **RsReportServer.config** 檔，並找出 `<AuthenticationTypes>` 區段。  
  
7.  加入 `<RSWindowsNegotiate/>` 當做此區段的第一個項目，以便啟用 NTLM。  
  
## <a name="see-also"></a>請參閱＜  
 [設定服務帳戶 &#40;SSRS 組態管理員 &#41;](http://msdn.microsoft.com/library/25000ad5-3f80-4210-8331-d4754dc217e0)   
 [設定報表伺服器服務帳戶 &#40;SSRS 組態管理員 &#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [管理 Reporting Services 原生模式報表伺服器](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md)  
  
  

