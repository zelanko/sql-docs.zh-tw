---
description: Web 組態參考 (Master Data Services)
title: Web 組態參考
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- web configuration file [Master Data Services]
ms.assetid: b8cc9a35-97ab-4fe0-ab4b-c07f13d9793a
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 34e3e849a86cb23c3974b32b9d3d8c0721601274
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456757"
---
# <a name="web-configuration-reference-master-data-services"></a>Web 組態參考 (Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 在 Web.config 檔案中包含讓 Internet Information Services (IIS) 主控 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 應用程式和 Web 服務的組態設定。 這個 Web.config 檔案位於 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 安裝路徑的 WebApplication 資料夾。 如需路徑和權限的詳細資訊，請參閱[資料夾和檔案的權限 &#40;Master Data Services&#41;](../master-data-services/folder-and-file-permissions-master-data-services.md)。  
  
## <a name="webconfig-elements"></a>Web.Config 元素  
 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] **\<masterDataServices>** 除了標準 IIS、.NET Framework、ASP.NET 和 WINDOWS COMMUNICATION FOUNDATION (WCF) 設定元素之外，Web.config 檔案還包含自訂元素。 下表描述 Web.config 檔案中包含的元素。  
  
|組態元素|描述|  
|---------------------------|-----------------|  
|**masterDataServices**|自訂元素。 將 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Web 服務連接到 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫。|  
|**connectionStrings**|ASP.NET 元素。 如需詳細資訊，請參閱 MSDN Library 中的 [connectionStrings 項目 (ASP.NET 設定結構描述)](https://go.microsoft.com/fwlink/?LinkId=178347) 。|  
|**system. web**|ASP.NET 元素。 如需詳細資訊，請參閱 MSDN Library 中的 [system.web 項目 (ASP.NET 設定結構描述)](https://go.microsoft.com/fwlink/?LinkId=178348) 。|  
|**啟動**|.NET Framework 元素。 如需詳細資訊，請參閱 MSDN Library 中的[ \<startup> 元素](https://go.microsoft.com/fwlink/?LinkId=178349)。|  
|**運行**|.NET Framework 元素。 如需詳細資訊，請參閱 MSDN Library 中的[ \<runtime> 元素](https://go.microsoft.com/fwlink/?LinkId=178350)。|  
|**system.codedom**|.NET Framework 元素。 如需詳細資訊，請參閱 MSDN Library 中的[ \<system.codedom> 元素](https://go.microsoft.com/fwlink/?LinkId=178351)。|  
|**副檔名**|ASP.NET 元素。 如需詳細資訊，請參閱 MSDN Library 中的 [system.web.extensions 項目 (ASP.NET 設定結構描述)](https://go.microsoft.com/fwlink/?LinkId=178352) 。|  
|**system.webServer**|包含 IIS 項目的區段群組。 如需詳細資訊，請參閱 MSDN Library 中的 [system.webServer 區段群組 \[IIS 7 設定結構描述\]](https://go.microsoft.com/fwlink/?LinkId=178353)。|  
|**system.serviceModel**|WCF 元素。 如需詳細資訊，請參閱 [\<system.serviceModel>](https://go.microsoft.com/fwlink/?LinkId=178354) MSDN library 中的。|  
|**system.diagnostics**|.NET Framework 元素。 如需詳細資訊，請參閱 MSDN Library 中的[ \<system.diagnostics> 元素](https://go.microsoft.com/fwlink/?LinkId=178355)。|  
|**appSettings**|ASP.NET 元素。 如需詳細資訊，請參閱 MSDN Library 中的 [appSettings 項目 (一般設定結構描述)](https://go.microsoft.com/fwlink/?LinkId=178356) 。|  
  
## <a name="masterdataservices-element"></a>masterDataServices 元素  
 **\<masterDataServices>** 元素是用來將 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Web 服務連接到資料庫的自訂元素 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 。  
  
### <a name="syntax"></a>語法  
  
```  
<masterDataServices>  
   <instance virtualPath="path" siteName="name" connectionName="name" serviceName="name" />  
</masterDataServices>  
```  
  
### <a name="elements-and-attributes"></a>元素和屬性  
  
|Item|描述|  
|----------|-----------------|  
|**instance**|子元素。 包含指定 Web 服務和資料庫連接字串之資訊的屬性。|  
|**virtualPath**|屬性。 指定 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 應用程式和服務的路徑。 這會對應至**path** **\<application>** IIS ApplicationHost.config 檔案中專案下元素的 path 屬性 **\<site>** 。|  
|**siteName**|屬性。 指定主控 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 應用程式和服務之網站的名稱。 這會對應至**name** **\<site>** IIS ApplicationHost.config 檔案中下專案的 name 屬性 **\<sites>** 。|  
|**connectionName**|屬性。 指定要使用之連接的名稱。 這會對應至**name** **\<add>** Web.config 中專案下元素的名稱屬性 **\<connectionStrings>** 。|  
|**serviceName**|屬性。 指定 Web 服務的名稱。 這會對應至**name** **\<service>** Web.config 中專案下元素的名稱屬性 **\<services>** 。|  
  
### <a name="example"></a>範例  
 下列範例示範使用 MDSDB 指定之連接字串的 Contoso 網站和 /MDS 路徑上一項名為 MDS1 的服務。  
  
```  
<masterDataServices>  
   <instance virtualPath="/MDS" siteName="Contoso" connectionName="MDSDB" serviceName="MDS1" />  
</masterDataServices>  
```  
  
  
