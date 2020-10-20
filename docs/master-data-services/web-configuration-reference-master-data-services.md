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
ms.openlocfilehash: 7f4baf9f3ef626f5e2dcdc62092afaf1e586df33
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/19/2020
ms.locfileid: "92196092"
---
# <a name="web-configuration-reference-master-data-services"></a>Web 組態參考 (Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 在 Web.config 檔案中包含讓 Internet Information Services (IIS) 主控 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 應用程式和 Web 服務的組態設定。 這個 Web.config 檔案位於 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 安裝路徑的 WebApplication 資料夾。 如需路徑和權限的詳細資訊，請參閱[資料夾和檔案的權限 &#40;Master Data Services&#41;](../master-data-services/folder-and-file-permissions-master-data-services.md)。  
  
## <a name="webconfig-elements"></a>Web.Config 元素  
 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] **\<masterDataServices>** 除了標準 IIS、.NET Framework、ASP.NET 和 WINDOWS COMMUNICATION FOUNDATION (WCF) 設定元素之外，Web.config 檔案還包含自訂元素。 下表描述 Web.config 檔案中包含的元素。  
  
|組態元素|描述|  
|---------------------------|-----------------|  
|**masterDataServices**|自訂元素。 將 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Web 服務連接到 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫。|  
|**connectionStrings**|ASP.NET 元素。 如需詳細資訊，請參閱 MSDN Library 中的 [connectionStrings 項目 (ASP.NET 設定結構描述)](/previous-versions/dotnet/netframework-4.0/bf7sd233(v=vs.100)) 。|  
|**system. web**|ASP.NET 元素。 如需詳細資訊，請參閱 MSDN Library 中的 [system.web 項目 (ASP.NET 設定結構描述)](/previous-versions/dotnet/netframework-4.0/dayb112d(v=vs.100)) 。|  
|**啟動**|.NET Framework 元素。 如需詳細資訊，請參閱 MSDN Library 中的[ \<startup> 元素](/dotnet/framework/configure-apps/file-schema/startup/startup-element)。|  
|**運行**|.NET Framework 元素。 如需詳細資訊，請參閱 MSDN Library 中的[ \<runtime> 元素](/dotnet/framework/configure-apps/file-schema/runtime/runtime-element)。|  
|**system.codedom**|.NET Framework 元素。 如需詳細資訊，請參閱 MSDN Library 中的[ \<system.codedom> 元素](/dotnet/framework/configure-apps/file-schema/compiler/system-codedom-element)。|  
|**副檔名**|ASP.NET 元素。 如需詳細資訊，請參閱 MSDN Library 中的 [system.web.extensions 項目 (ASP.NET 設定結構描述)](/previous-versions/dotnet/netframework-4.0/bb546044(v=vs.100)) 。|  
|**system.webServer**|包含 IIS 項目的區段群組。 如需詳細資訊，請參閱 MSDN Library 中的 [system.webServer 區段群組 \[IIS 7 設定結構描述\]](/previous-versions/iis/settings-schema/ms689429(v=vs.90))。|  
|**system.serviceModel**|WCF 元素。 如需詳細資訊，請參閱 [\<system.serviceModel>](/dotnet/framework/configure-apps/file-schema/wcf/system-servicemodel) MSDN library 中的。|  
|**system.diagnostics**|.NET Framework 元素。 如需詳細資訊，請參閱 MSDN Library 中的[ \<system.diagnostics> 元素](/dotnet/framework/configure-apps/file-schema/trace-debug/system-diagnostics-element)。|  
|**appSettings**|ASP.NET 元素。 如需詳細資訊，請參閱 MSDN Library 中的 [appSettings 項目 (一般設定結構描述)](/previous-versions/dotnet/netframework-4.0/ms228154(v=vs.100)) 。|  
  
## <a name="masterdataservices-element"></a>masterDataServices 元素  
 **\<masterDataServices>** 元素是用來將 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Web 服務連接到資料庫的自訂元素 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 。  
  
### <a name="syntax"></a>語法  
  
```  
<masterDataServices>  
   <instance virtualPath="path" siteName="name" connectionName="name" serviceName="name" />  
</masterDataServices>  
```  
  
### <a name="elements-and-attributes"></a>元素和屬性  
  
|項目|描述|  
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
  
