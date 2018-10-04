---
title: Web 組態參考 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
helpviewer_keywords:
- web configuration file [Master Data Services]
ms.assetid: b8cc9a35-97ab-4fe0-ab4b-c07f13d9793a
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 2f52ca10bd9d857d4e87a54f19cfaa87f1e92575
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48130958"
---
# <a name="web-configuration-reference-master-data-services"></a>Web 組態參考 (Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 在 Web.config 檔案中包含讓 Internet Information Services (IIS) 主控 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 應用程式和 Web 服務的組態設定。 這個 Web.config 檔案位於 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 安裝路徑的 WebApplication 資料夾。 如需路徑和權限的詳細資訊，請參閱[資料夾和檔案的權限 &#40;Master Data Services&#41;](folder-and-file-permissions-master-data-services.md)。  
  
## <a name="webconfig-elements"></a>Web.Config 元素  
 除了標準的 IIS、.NET Framework、ASP.NET 和 Windows Communication Foundation (WCF) 組態項目以外，Web.config 檔案還包含自訂的 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 項目 (**\<masterDataServices>**)。 下表描述 Web.config 檔案中包含的元素。  
  
|組態元素|描述|  
|---------------------------|-----------------|  
|`masterDataServices`|自訂元素。 將 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Web 服務連接到 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫。|  
|`connectionStrings`|ASP.NET 元素。 如需詳細資訊，請參閱 MSDN Library 中的 [connectionStrings 項目 (ASP.NET 設定結構描述)](http://go.microsoft.com/fwlink/?LinkId=178347) 。|  
|`system.web`|ASP.NET 元素。 如需詳細資訊，請參閱 MSDN Library 中的 [system.web 項目 (ASP.NET 設定結構描述)](http://go.microsoft.com/fwlink/?LinkId=178348) 。|  
|`startup`|.NET Framework 元素。 如需詳細資訊，請參閱 MSDN Library 中的 [\<startup 項目](http://go.microsoft.com/fwlink/?LinkId=178349)。|  
|`runtime`|.NET Framework 元素。 如需詳細資訊，請參閱 MSDN Library 中的 [\<runtime 項目](http://go.microsoft.com/fwlink/?LinkId=178350)。|  
|`system.codedom`|.NET Framework 元素。 如需詳細資訊，請參閱 MSDN Library 中的 [\<system.codedom> 項目](http://go.microsoft.com/fwlink/?LinkId=178351)。|  
|`system.web.extensions`|ASP.NET 元素。 如需詳細資訊，請參閱 MSDN Library 中的 [system.web.extensions 項目 (ASP.NET 設定結構描述)](http://go.microsoft.com/fwlink/?LinkId=178352) 。|  
|`system.webServer`|包含 IIS 項目的區段群組。 如需詳細資訊，請參閱 MSDN Library 中的 [system.webServer 區段群組 \[IIS 7 設定結構描述\]](http://go.microsoft.com/fwlink/?LinkId=178353)。|  
|`system.serviceModel`|WCF 元素。 如需詳細資訊，請參閱 MSDN Library 中的 [\<system.serviceModel>](http://go.microsoft.com/fwlink/?LinkId=178354)。|  
|`system.diagnostics`|.NET Framework 元素。 如需詳細資訊，請參閱 MSDN Library 中的 [\<system.diagnostics> 項目](http://go.microsoft.com/fwlink/?LinkId=178355)。|  
|`appSettings`|ASP.NET 元素。 如需詳細資訊，請參閱 MSDN Library 中的 [appSettings 項目 (一般設定結構描述)](http://go.microsoft.com/fwlink/?LinkId=178356) 。|  
  
## <a name="masterdataservices-element"></a>masterDataServices 元素  
 **\<masterDataServices>** 項目是用來將 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Web 服務連接到 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫的自訂項目。  
  
### <a name="syntax"></a>語法  
  
```  
<masterDataServices>  
   <instance virtualPath="path" siteName="name" connectionName="name" serviceName="name" />  
</masterDataServices>  
```  
  
### <a name="elements-and-attributes"></a>元素和屬性  
  
|項目|描述|  
|----------|-----------------|  
|`instance`|子元素。 包含指定 Web 服務和資料庫連接字串之資訊的屬性。|  
|`virtualPath`|屬性。 指定 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 應用程式和服務的路徑。 這會對應至`path`的屬性**\<應用程式 >** 項目底下**\<站台 >** IIS ApplicationHost.config 檔案中的項目。|  
|`siteName`|屬性。 指定主控 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 應用程式和服務之網站的名稱。 這會對應至`name`的屬性**\<站台 >** 項目底下**\<網站 >** IIS ApplicationHost.config 檔案中。|  
|`connectionName`|屬性。 指定要使用之連接的名稱。 這會對應至`name`的屬性**\<新增 >** 項目底下 **\<connectionStrings >** Web.config 中的項目。|  
|`serviceName`|屬性。 指定 Web 服務的名稱。 這會對應至`name`的屬性**\<服務 >** 項目底下**\<服務 >** Web.config 中的項目。|  
  
### <a name="example"></a>範例  
 下列範例示範使用 MDSDB 指定之連接字串的 Contoso 網站和 /MDS 路徑上一項名為 MDS1 的服務。  
  
```  
<masterDataServices>  
   <instance virtualPath="/MDS" siteName="Contoso" connectionName="MDSDB" serviceName="MDS1" />  
</masterDataServices>  
```  
  
  
