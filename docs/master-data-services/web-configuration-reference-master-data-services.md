---
title: "Web 組態參考 (Master Data Services) | Microsoft Docs"
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
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: a816a35d944f7d19455e57609ecfebdd630ea9d6
ms.contentlocale: zh-tw
ms.lasthandoff: 09/07/2017

---
# <a name="web-configuration-reference-master-data-services"></a>Web 組態參考 (Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 在 Web.config 檔案中包含讓 Internet Information Services (IIS) 主控 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 應用程式和 Web 服務的組態設定。 這個 Web.config 檔案位於 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 安裝路徑的 WebApplication 資料夾。 如需路徑和權限的詳細資訊，請參閱[資料夾和檔案的權限 &#40;Master Data Services&#41;](../master-data-services/folder-and-file-permissions-master-data-services.md)。  
  
## <a name="webconfig-elements"></a>Web.Config 元素  
 除了標準的 IIS、.NET Framework、ASP.NET 和 Windows Communication Foundation (WCF) 組態項目以外，Web.config 檔案還包含自訂的 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 項目 (**\<masterDataServices>**)。 下表描述 Web.config 檔案中包含的元素。  
  
|組態元素|說明|  
|---------------------------|-----------------|  
|**masterDataServices**|自訂元素。 將 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Web 服務連接到 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫。|  
|**connectionStrings**|ASP.NET 元素。 如需詳細資訊，請參閱 MSDN Library 中的 [connectionStrings 項目 (ASP.NET 設定結構描述)](http://go.microsoft.com/fwlink/?LinkId=178347) 。|  
|**system.web**|ASP.NET 元素。 如需詳細資訊，請參閱 MSDN Library 中的 [system.web 項目 (ASP.NET 設定結構描述)](http://go.microsoft.com/fwlink/?LinkId=178348) 。|  
|**startup**|.NET Framework 元素。 如需詳細資訊，請參閱 MSDN Library 中的 [\<startup 項目](http://go.microsoft.com/fwlink/?LinkId=178349)。|  
|**執行階段**|.NET Framework 元素。 如需詳細資訊，請參閱 MSDN Library 中的 [\<runtime 項目](http://go.microsoft.com/fwlink/?LinkId=178350)。|  
|**system.codedom**|.NET Framework 元素。 如需詳細資訊，請參閱 MSDN Library 中的 [\<system.codedom> 項目](http://go.microsoft.com/fwlink/?LinkId=178351)。|  
|**system.web.extensions**|ASP.NET 元素。 如需詳細資訊，請參閱 MSDN Library 中的 [system.web.extensions 項目 (ASP.NET 設定結構描述)](http://go.microsoft.com/fwlink/?LinkId=178352) 。|  
|**system.webServer**|包含 IIS 項目的區段群組。 如需詳細資訊，請參閱 MSDN Library 中的 [system.webServer 區段群組 \[IIS 7 設定結構描述\]](http://go.microsoft.com/fwlink/?LinkId=178353)。|  
|**system.serviceModel**|WCF 元素。 如需詳細資訊，請參閱 MSDN Library 中的 [\<system.serviceModel>](http://go.microsoft.com/fwlink/?LinkId=178354)。|  
|**system.diagnostics**|.NET Framework 元素。 如需詳細資訊，請參閱 MSDN Library 中的 [\<system.diagnostics> 項目](http://go.microsoft.com/fwlink/?LinkId=178355)。|  
|**appSettings**|ASP.NET 元素。 如需詳細資訊，請參閱 MSDN Library 中的 [appSettings 項目 (一般設定結構描述)](http://go.microsoft.com/fwlink/?LinkId=178356) 。|  
  
## <a name="masterdataservices-element"></a>masterDataServices 元素  
 **\<masterDataServices>** 項目是用來將 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Web 服務連接到 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫的自訂項目。  
  
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
|**virtualPath**|屬性。 指定 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 應用程式和服務的路徑。 這對應於 IIS ApplicationHost.config 檔案中 **\<site>** 項目下之 **\<application>** 項目的 **path** 屬性。|  
|**siteName**|屬性。 指定主控 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 應用程式和服務之網站的名稱。 這對應於 IIS ApplicationHost.config 檔案中 **\<sites>** 項目下之 **\<site>** 項目的 **name** 屬性。|  
|**connectionName**|屬性。 指定要使用之連接的名稱。 這對應於 Web.config 中 **\<connectionStrings>** 項目下之 **\<add>** 項目的 **name** 屬性。|  
|**serviceName**|屬性。 指定 Web 服務的名稱。 這對應於 Web.config 中 **\<services>** 項目下之 **\<service>** 項目的 **name** 屬性。|  
  
### <a name="example"></a>範例  
 下列範例示範使用 MDSDB 指定之連接字串的 Contoso 網站和 /MDS 路徑上一項名為 MDS1 的服務。  
  
```  
<masterDataServices>  
   <instance virtualPath="/MDS" siteName="Contoso" connectionName="MDSDB" serviceName="MDS1" />  
</masterDataServices>  
```  
  
  

