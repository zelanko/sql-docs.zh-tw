---
title: "Analysis Services 支援的驗證方法 |Microsoft 文件"
ms.custom: 
ms.date: 03/07/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b7aee903-d33a-4c20-86c2-aa013a50949f
caps.latest.revision: "8"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 5fd280c748fd887e3582a95c7f023dbc659b604a
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/08/2017
---
# <a name="authentication-methodologies-supported-by-analysis-services"></a>Analysis Services 支援的驗證方法
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]從 Analysis Services 執行個體的用戶端應用程式的連接必須使用 Windows 驗證 （整合式）。 您可以使用下列任何一種方法來提供 Windows 使用者識別：  
  
-   NTLM  
  
-   Kerberos (請參閱 [設定 Analysis Services 進行 Kerberos 限制委派](../../analysis-services/instances/configure-analysis-services-for-kerberos-constrained-delegation.md))  
  
-   連接字串的 EffectiveUserName  
  
-   基本或匿名 (需要 HTTP 存取的組態)  
  
-   預存認證  
  
 請注意，由於不支援宣告驗證， 因此您不能使用 Windows 的宣告 Token 存取 Analysis Services。 Analysis Services 用戶端程式庫只能與 Windows 安全性主體搭配使用。 如果您的 BI 方案包括宣告識別，則需要每位使用者的 Windows 識別陰影帳戶，或使用預存認證來存取 Analysis Services 資料。  
  
 如需 BI 和 Analysis Services 驗證流程的詳細資訊，請參閱 [Microsoft BI Authentication and Identity Delegation](http://go.microsoft.com/fwlink/?LinkID=286576)(Microsoft BI 驗證及識別委派)。  
  
##  <a name="bkmk_auth"></a> 了解您的驗證替代方案  
 連接到 Analysis Services 資料庫需要 Windows 使用者或群組識別以及相關聯的權限。 此識別可能是一般用途的登入，由需要檢視報表的任何人使用，但是比較可能的案例包含個別使用者的識別。  
  
 表格式或多維度模型通常具有不同的資料存取層級 (依物件或資料本身)，端視提出要求的對象而定。 為了符合此需求，您可以使用 NTLM、Kerberos、EffectiveUserName 或基本驗證。 上述所有技術都會提供一種透過每個連接傳入不同使用者識別的方法。 不過，這些選擇大部分會受限於單躍點限制。 只有含有委派的 Kerberos 允許原始使用者識別跨多個電腦連接流向遠端伺服器上的後端資料存放區。  
  
 **NTLM**  
  
 對於指定 `SSPI=Negotiate`的連接而言，NTLM 是 Kerberos 網域控制站無法使用時所用的備份驗證子系統。 在 NTLM 底下，只要要求是從用戶端到伺服器的直接連接、要求連接的人員擁有資源的權限，而且用戶端與伺服器電腦位於相同的網域中，任何使用者或用戶端應用程式都可以存取伺服器資源。  
  
 在多層式方案中，NLTM 的單躍點限制可能是主要的條件約束。 雖然可以在一部遠端伺服器上完全模擬提出要求的使用者識別，但是卻無法連接到其他伺服器。 如果目前的作業需要多部電腦上執行的服務，您就必須將 Kerberos 限制委派設定為重複使用後端伺服器上的安全性 Token。 或者，您也可以使用預存認證或基本驗證來傳入透過單躍點連線的新識別資訊。  
  
 **Kerberos 驗證和 Kerberos 限制委派**  
  
 Kerberos 驗證是 Active Directory 網域中 Windows 整合式安全性的基礎。 如同 NTLM，除非您啟用委派，否則 Kerberos 底下的模擬會限制為單躍點。  
  
 為了支援多躍點連接，Kerberos 會同時提供限制與非限制委派，但是在大部分情況下，限制委派會被視為安全性最佳作法。 限制委派會允許服務將使用者識別的安全性 Token 傳遞至遠端電腦上指定的下層服務。 若為多層應用程式，將使用者識別從中介層應用程式伺服器委派至後端資料庫 (例如 Analysis Services) 是常見的需求。 例如，根據使用者識別傳回不同資料的表格式或多維度模型會需要來自中介層服務的識別委派，避免讓使用者重新輸入認證，或以其他方式取得安全性認證。  
  
 限制委派需要在 Active Directory 中進行其他組態設定，好讓位於要求傳送和接收端的服務明確獲得委派的授權。 雖然這樣會事先產生組態設定成本，不過一旦設定服務之後，密碼更新就會在 Active Directory 中獨立管理。 您不需要更新應用程式的預存帳戶資訊，但是如果使用以下描述的預存認證選項，則必須自行更新。  
  
 如需設定 Analysis Services 進行限制委派的詳細資訊，請參閱 [設定 Analysis Services 進行 Kerberos 限制委派](../../analysis-services/instances/configure-analysis-services-for-kerberos-constrained-delegation.md)。  
  
> [!NOTE]  
>  Windows Server 2012 支援跨網域的限制委派。 相較之下，在較低功能層級的網域 (例如 Windows Server 2008 或 2008 R2) 中設定 Kerberos 限制委派會要求用戶端與伺服器電腦都必須是相同網域的成員。  
  
 **EffectiveUserName**  
  
 EffectiveUserName 是將識別資訊傳遞至 Analysis Services 所用的連接字串屬性。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 會用它將使用者活動記錄在使用狀況記錄檔中。 Excel Services 和 PerformancePoint Services 可以用它來擷取 SharePoint 活頁簿或儀表板所使用的資料。 它也可以用於針對 Analysis Services 執行個體執行作業的自訂應用程式或指令碼中。  
  
 如需在 SharePoint 中使用 EffectiveUserName 的詳細資訊，請參閱 [Use Analysis Services EffectiveUserName in SharePoint Server 2010](http://go.microsoft.com/fwlink/?LinkId=311905)(在 SharePoint Server 2010 中使用 Analysis Services EffectiveUserName)。  
  
 **基本驗證和匿名使用者**  
  
 基本驗證提供了第四種替代方案，讓您以特定使用者的身分連接到後端伺服器。 使用基本驗證時，Windows 使用者名稱和密碼會透過連接字串傳遞，並導入其他連線加密需求，確保機密資訊在傳輸時受到保護。 使用基本驗證的重要優點在於，驗證要求可以跨越網域界限。  
  
 如果是匿名驗證，您可以將匿名使用者識別設定為特定 Windows 使用者帳戶 (預設為 IUSR_GUEST) 或應用程式集區識別。 匿名使用者帳戶將用於 Analysis Services 連接，而且必須擁有 Analysis Services 執行個體的資料存取權限。 當您使用這種方法時，只有與匿名帳戶相關聯的使用者識別會用於連接。 如果您的應用程式需要其他識別管理，您就必須選擇其他方法，或是使用您所提供的識別管理解決方案來補充。  
  
 只有當您設定 Analysis Services 進行 HTTP 存取，並且使用 IIS 和 msmdpump.dll 來建立連接時，才能使用基本和匿名驗證。 如需詳細資訊，請參閱 [設定 Internet Information Services &#40;IIS&#41; 8.0 上 Analysis Services 的 HTTP 存取](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md)(Microsoft BI 驗證及識別委派)。  
  
 **Stored Credentials**  
  
 大部分中介層應用程式服務都能夠儲存使用者名稱和密碼，然後再用來從下層資料存放區 (例如 Analysis Services 或 SQL Server 關聯式引擎) 擷取資料。 因此，預存認證提供了第五種替代方案，可用於擷取資料。 這種方法的限制包括將使用者名稱和密碼保持在最新狀態的相關維護負擔，以及將單一識別用於連接的作法。 如果您的方案需要原始呼叫端的識別，則預存認證就不會是可行的替代方案。  
  
 如需預存認證的詳細資訊，請參閱[建立、修改及刪除共用資料來源 &#40;SSRS&#41;](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md) 和 [Use Excel Services with Secure Store Service in SharePoint Server 2013](http://go.microsoft.com/fwlink/?LinkID=309869) (在 SharePoint Server 2013 中使用 Excel Services 搭配 Secure Store Service)。  
  
## <a name="see-also"></a>請參閱  
 [使用模擬搭配傳輸安全性](http://go.microsoft.com/fwlink/?LinkId=311727)   
 [設定 Internet Information Services &#40;IIS&#41; 8.0 上 Analysis Services 的 HTTP 存取](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md)   
 [設定 Analysis Services 進行 Kerberos 限制委派](../../analysis-services/instances/configure-analysis-services-for-kerberos-constrained-delegation.md)   
 [Analysis Services 執行個體的 SPN 註冊](../../analysis-services/instances/spn-registration-for-an-analysis-services-instance.md)   
 [連接到 Analysis Services](../../analysis-services/instances/connect-to-analysis-services.md)  
  
  
