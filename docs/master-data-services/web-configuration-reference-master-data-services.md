---
title: "Web 組態參考 (Master Data Services) |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- web configuration file [Master Data Services]
ms.assetid: b8cc9a35-97ab-4fe0-ab4b-c07f13d9793a
caps.latest.revision: 6
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1be0e90d7d2ba9b2751677015957ca249d91119e
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="web-configuration-reference-master-data-services"></a>Web 組態參考 (Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]在 Web.config 檔案中包含的組態設定，讓網際網路資訊服務 (IIS) 主控[!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]Web 應用程式和 Web 服務。 這個 Web.config 檔案位於 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 安裝路徑的 WebApplication 資料夾。 如需路徑和權限的詳細資訊，請參閱[資料夾和檔案的權限 &#40;Master Data Services&#41;](../master-data-services/folder-and-file-permissions-master-data-services.md)。  
  
## <a name="webconfig-elements"></a>Web.Config 元素  
 Web.config 檔案還包含自訂[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]項目，  **\<masterDataServices >**，除了標準的 IIS、.NET Framework、 ASP.NET 和 Windows Communication Foundation (WCF) 組態項目。 下表描述 Web.config 檔案中包含的元素。  
  
|組態元素|說明|  
|---------------------------|-----------------|  
|**masterDataServices**|自訂元素。 將 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Web 服務連接到 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫。|  
|**connectionStrings**|ASP.NET 元素。 如需詳細資訊，請參閱 MSDN Library 中的 [connectionStrings 項目 (ASP.NET 設定結構描述)](http://go.microsoft.com/fwlink/?LinkId=178347) 。|  
|**system.web**|ASP.NET 元素。 如需詳細資訊，請參閱 MSDN Library 中的 [system.web 項目 (ASP.NET 設定結構描述)](http://go.microsoft.com/fwlink/?LinkId=178348) 。|  
|**startup**|.NET Framework 元素。 如需詳細資訊，請參閱[\<啟動 > 項目](http://go.microsoft.com/fwlink/?LinkId=178349)MSDN Library 中。|  
|**執行階段**|.NET Framework 元素。 如需詳細資訊，請參閱[ \<runtime > 項目](http://go.microsoft.com/fwlink/?LinkId=178350)MSDN Library 中。|  
|**system.codedom**|.NET Framework 元素。 如需詳細資訊，請參閱[ \<system.codedom > 項目](http://go.microsoft.com/fwlink/?LinkId=178351)MSDN Library 中。|  
|**system.web.extensions**|ASP.NET 元素。 如需詳細資訊，請參閱 MSDN Library 中的 [system.web.extensions 項目 (ASP.NET 設定結構描述)](http://go.microsoft.com/fwlink/?LinkId=178352) 。|  
|**system.webServer**|包含 IIS 項目的區段群組。 如需詳細資訊，請參閱 MSDN Library 中的 [system.webServer 區段群組 \[IIS 7 設定結構描述\]](http://go.microsoft.com/fwlink/?LinkId=178353)。|  
|**system.serviceModel**|WCF 元素。 如需詳細資訊，請參閱[ \<system.serviceModel >](http://go.microsoft.com/fwlink/?LinkId=178354) MSDN Library 中。|  
|**system.diagnostics**|.NET Framework 元素。 如需詳細資訊，請參閱[ \<system.diagnostics > 項目](http://go.microsoft.com/fwlink/?LinkId=178355)MSDN Library 中。|  
|**appSettings**|ASP.NET 元素。 如需詳細資訊，請參閱 MSDN Library 中的 [appSettings 項目 (一般設定結構描述)](http://go.microsoft.com/fwlink/?LinkId=178356) 。|  
  
## <a name="masterdataservices-element"></a>masterDataServices 元素  
  **\<MasterDataServices >**元素是用來連接的自訂項目[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]Web 服務以[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]資料庫。  
  
### <a name="syntax"></a>語法  
  
```  
<masterDataServices>  
   <instance virtualPath="path" siteName="name" connectionName="name" serviceName="name" />  
</masterDataServices>  
```  
  
### <a name="elements-and-attributes"></a>元素和屬性  
  
|項目|說明|  
|----------|-----------------|  
|**執行個體**|子元素。 包含指定 Web 服務和資料庫連接字串之資訊的屬性。|  
|**virtualPath**|屬性。 指定 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 應用程式和服務的路徑。 這會對應至**路徑**屬性**\<應用程式 >**項目底下**\<網站 >** IIS ApplicationHost.config 檔案中的項目。|  
|**siteName**|屬性。 指定主控 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 應用程式和服務之網站的名稱。 這會對應至**名稱**屬性**\<網站 >**項目底下**\<網站 >** IIS ApplicationHost.config 檔案中。|  
|**connectionName**|屬性。 指定要使用之連接的名稱。 這會對應至**名稱**屬性**\<新增 >**項目底下 **\<connectionStrings >** Web.config 中的項目。|  
|**serviceName**|屬性。 指定 Web 服務的名稱。 這會對應至**名稱**屬性**\<服務 >**項目底下**\<服務 >** Web.config 中的項目。|  
  
### <a name="example"></a>範例  
 下列範例示範使用 MDSDB 指定之連接字串的 Contoso 網站和 /MDS 路徑上一項名為 MDS1 的服務。  
  
```  
<masterDataServices>  
   <instance virtualPath="/MDS" siteName="Contoso" connectionName="MDSDB" serviceName="MDS1" />  
</masterDataServices>  
```  
  
  
