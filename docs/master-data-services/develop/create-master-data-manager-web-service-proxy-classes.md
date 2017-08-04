---
title: "建立主資料管理員 Web 服務 Proxy 類別 |Microsoft 文件"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 8bdab026-a0c0-41f3-9d36-f3919c23247f
caps.latest.revision: 8
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: a45cd15ced90aef95feb03f8fbaafd5aa70cb746
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="create-master-data-manager-web-service-proxy-classes"></a>建立主資料管理員 Web 服務 Proxy 類別
  [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 服務可讓您以程式設計的方式，從可以存取 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 網站的任何電腦使用 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 的功能。 在您可以開始撰寫程式碼以存取 Web 服務之前，必須先產生 Proxy 類別。 您用來執行 Web 服務作業的主要 Proxy 類別為 <xref:Microsoft.MasterDataServices.ServiceClient> 類別，此類別會實作 <xref:Microsoft.MasterDataServices.IService> 介面。  
  
## <a name="enable-web-service-metadata-publishing"></a>啟用 Web 服務中繼資料發佈  
 在您可以產生 Proxy 類別之前，必須啟用 Web 服務中繼資料發佈。 請遵循下列步驟進行：  
  
1.  開啟[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]文字編輯器中的 Web.config 檔案。 這個檔案位於 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 安裝路徑的 WebApplication 資料夾。  
  
2.  尋找**mdsWsHttpBehavior**區段 **\<serviceBehaviors >**。 如 **\<serviceMetadata >**項目，設定**httpGetEnabled**至**true**。  
  
    > [!NOTE]  
    >  如果您想要透過 Secure Sockets Layer (SSL) 啟用 Web 服務，設定**httpsGetEnabled**至**true**中**mdsWsHttpBehavior** web.config 檔案區段。 您也需要變更**mdsWsHTTPBinding** ，以便設定 SSL，，和註解非 SSL > 一節。  
  
3.  儲存檔案的變更。  
  
4.  測試中繼資料發佈至服務的 URL，例如瀏覽： `http://yourserver/MDS/service/service.svc`。 如果已啟用中繼資料發佈，則會顯示開頭為   
    「您已建立服務」的頁面。  
  
## <a name="creating-proxy-classes-by-using-visual-studio"></a>使用 Visual Studio 建立 Proxy 類別  
 如果您有安裝 Visual Studio 2010，產生 proxy 類別最簡單的方式是加入**服務參考**至您的專案。 服務參考的位址就是 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式的 URL，並附加 /service/service.svc。 例如：`http://yourserver/MDS/service/service.svc`。 如需詳細資訊，請參閱[如何： 加入、 更新或移除服務參考](http://go.microsoft.com/fwlink/?LinkId=221167)。  
  
## <a name="creating-proxy-classes-by-using-svcutilexe"></a>使用 Svcutil.exe 建立 Proxy 類別  
 您必須已經[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]或[!INCLUDE[msCoName](../../includes/msconame-md.md)]才會有 Svcutil.exe 在您的電腦上安裝 Windows SDK。 如果您使用 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]，您須使用 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 命令提示字元執行此命令。 如需詳細資訊，請參閱[ServiceModel Metadata Utility Tool (Svcutil.exe)](http://go.microsoft.com/fwlink/?LinkId=165027)和[從服務中繼資料產生 WCF 用戶端](http://go.microsoft.com/fwlink/?LinkId=164821)。  
  
 若要使用 Svcutil.exe 建立一組 C# Proxy 類別，請使用類似以下的命令：  
  
```  
svcutil.exe http://<server_name:port>/<virtual_path>/Service/Service.svc   
/out:<proxy_name>.cs /messageContract /tcv:Version35   
/noconfig /ct:System.Collections.ObjectModel.Collection`1   
/namespace:*,Microsoft.MasterDataServices  
```  
  
 其中：  
  
-   *servername*:*連接埠*為電腦名稱和連接埠號碼裝載電腦[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]。  
  
-   *virtual_path*是虛擬路徑[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]網際網路資訊服務 (IIS) 中。  
  
-   *proxy_name*是產生之 proxy 檔案的名稱。  
  
## <a name="see-also"></a>另請參閱  
 [分類的 Web 服務作業 &#40;Master Data services&#41;](../../master-data-services/develop/categorized-web-service-operations-master-data-services.md)  
  
  
