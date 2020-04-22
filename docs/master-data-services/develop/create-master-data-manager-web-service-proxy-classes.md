---
title: 建立主資料管理員 Web 服務 Proxy 類別
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: 8bdab026-a0c0-41f3-9d36-f3919c23247f
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 2e204b5021cb2928988331c73750821225a4192d
ms.sourcegitcommit: 66407a7248118bb3e167fae76bacaa868b134734
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81728434"
---
# <a name="create-master-data-manager-web-service-proxy-classes"></a>建立主資料管理員 Web 服務 Proxy 類別

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 服務可讓您以程式設計的方式，從可以存取 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 網站的任何電腦使用 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 的功能。 在您可以開始撰寫程式碼以存取 Web 服務之前，必須先產生 Proxy 類別。 您用來執行 Web 服務作業的主要 Proxy 類別為 <xref:Microsoft.MasterDataServices.ServiceClient> 類別，此類別會實作 <xref:Microsoft.MasterDataServices.IService> 介面。  
  
## <a name="enable-web-service-metadata-publishing"></a>啟用 Web 服務中繼資料發佈  
 在您可以產生 Proxy 類別之前，必須啟用 Web 服務中繼資料發佈。 請遵循下列步驟進行：  
  
1.  在文字編輯器中開啟 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] Web.config 檔案。 這個檔案位於 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 安裝路徑的 WebApplication 資料夾。  
  
2.  在 **\<serviceBehaviors>** 底下，尋找 **mdsWsHttpBehavior** 區段。 對**\<服務中繼資料>** 元素,將**httpGetEnabled**設定為**true**。  
  
    > [!NOTE]  
    >  如果要透過傳輸層安全 (TLS)啟用 Web 服務(以前稱為安全套接字層 (SSL),請將**HTTPsTK設定**為**true,** 在 Web.config 檔案的**mdsWsHTTPBehavior**部分。 您還需要更改**mdsWsHTTPBinding,** 以便它也可以配置為 TLS,並註釋掉非 TLS 部分。  
  
3.  儲存檔案的變更。  
  
4.  瀏覽至服務 URL (例如：`https://yourserver/MDS/service/service.svc`) 來測試中繼資料發佈。 如果已啟用中繼資料發佈，則會顯示開頭為   
    「您已建立服務」的頁面。  
  
## <a name="creating-proxy-classes-by-using-visual-studio"></a>使用 Visual Studio 建立 Proxy 類別  
 如果您已安裝 Visual Studio 2010，產生 Proxy 類別最簡單的方式，就是將 [服務參考]**** 新增至您的專案。 服務參考的位址就是 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式的 URL，並附加 /service/service.svc。 例如： `https://yourserver/MDS/service/service.svc` 。 如需詳細資訊，請參閱[如何：新增、更新或移除服務參考](https://go.microsoft.com/fwlink/?LinkId=221167)。  
  
## <a name="creating-proxy-classes-by-using-svcutilexe"></a>使用 Svcutil.exe 建立 Proxy 類別  
 您必須安裝或[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]安裝[!INCLUDE[msCoName](../../includes/msconame-md.md)]Windows SDK 才能在電腦上安裝 Svcutil.exe。 如果您使用 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]，您須使用 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 命令提示字元執行此命令。 如需詳細資訊，請參閱 [ServiceModel 中繼資料公用程式工具 (Svcutil.exe)](https://go.microsoft.com/fwlink/?LinkId=165027) 和[從服務中繼資料產生 WCF 用戶端](https://go.microsoft.com/fwlink/?LinkId=164821)。  
  
 若要使用 Svcutil.exe 建立一組 C# Proxy 類別，請使用類似以下的命令：  
  
```  
svcutil.exe https://<server_name:port>/<virtual_path>/Service/Service.svc   
/out:<proxy_name>.cs /messageContract /tcv:Version35   
/noconfig /ct:System.Collections.ObjectModel.Collection`1   
/namespace:*,Microsoft.MasterDataServices  
```  
  
 其中：  
  
-   *servername*:*port* 為主控 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 之電腦的電腦名稱及連接埠號碼。  
  
-   *virtual_path* 為 Internet Information Services (IIS) 中 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 的虛擬路徑。  
  
-   *proxy_name* 為產生之 Proxy 檔案的名稱。  
  
## <a name="see-also"></a>另請參閱  
 [分類的 Web 服務作業 &#40;Master Data Services&#41;](../../master-data-services/develop/categorized-web-service-operations-master-data-services.md)  
  
  
