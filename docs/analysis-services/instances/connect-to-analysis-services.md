---
title: 連接到 Analysis Services |Microsoft 文件
ms.custom: ''
ms.date: 01/23/2018
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- instances of Analysis Services, connections
ms.assetid: 73ee8171-3379-4384-bfc8-071b3eebbc8f
caps.latest.revision: 46
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 7dbadb28b56be49197f530e735f68238d13bc101
ms.sourcegitcommit: 3206a31870f8febab7d1718fa59fe0590d4d45db
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/24/2018
---
# <a name="connect-to-analysis-services"></a>連接到 Analysis Services
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]若要了解連接字串屬性，用於的連接的驗證方法都支援 Analysis Services，以及如何設定或清除連接再讓伺服器離線的用戶端程式庫中使用本節中的資訊。  

若要深入了解連接到 Azure Analysis Services，請參閱[連接到伺服器](https://docs.microsoft.com/azure/analysis-services/analysis-services-connect)。
  
## <a name="analysis-services-connections"></a>Analysis Services 連接  
 Analysis Services 使用 TCP 當做網路通訊協定，並使用 XML for Analysis (XMLA) 當做溝通通訊協定。 Analysis Services 提供的所有用戶端程式庫在最低層級都會實作 XMLA-over-TCP。 雖然也可以根據原始 XMLA 來建置應用程式，但是大多數應用程式和應用程式開發人員仍然使用用戶端程式庫，因為這些程式庫擁有物件模型及編碼效率等優點。 對於用戶端與 Analysis Services 的連接，如果您無法跨堆疊使用 TCP，則可以使用 IIS 做為中繼連接。 透過 IIS 使用 HTTP 存取的其中一個優點是，能夠從在連接字串上傳遞認證的應用程式進行連接。  
  
 只要是涉及連接的討論內容，通常都包含驗證。 相較於其他 SQL Server 功能，Analysis Services 只會使用 Windows 認證。 您無法對與 Analysis Services 的後端連接使用 SQL Server 資料庫驗證、宣告驗證、表單型驗證或摘要式驗證。 本節將提供更多關於驗證的詳細資訊。  
  
##  <a name="bkmk_clientApps"></a> 連接工作  
  
|連結|工作描述|  
|----------|----------------------|  
|[從用戶端應用程式 &#40; 連接Analysis Services &#41;](../../analysis-services/instances/connect-from-client-applications-analysis-services.md)|如果您還不熟悉 Analysis Services，請閱讀本主題，了解最常搭配 Analysis Services 使用的工具和應用程式。|  
|[連接字串屬性 &#40;Analysis Services &#41;](../../analysis-services/instances/connection-string-properties-analysis-services.md)|Analysis Services 包括許多伺服器和資料庫屬性，可讓您為特定應用程式自訂連接，不必考慮執行個體或資料庫的設定方式。|  
|[Analysis Services 支援的驗證方法](../../analysis-services/instances/authentication-methodologies-supported-by-analysis-services.md)|本主題會簡短介紹 Analysis Services 所使用的驗證方法。|  
|[設定 Analysis Services 進行 Kerberos 限制委派](../../analysis-services/instances/configure-analysis-services-for-kerberos-constrained-delegation.md)|許多商業智慧方案都需要進行模擬，確保只會將經過授權的資料傳回給每個使用者。 在本主題中，您將了解模擬的使用需求， 以及為 Kerberos 限制委派設定 Analysis Services 的步驟。|  
|[Analysis Services 執行個體的 SPN 註冊](../../analysis-services/instances/spn-registration-for-an-analysis-services-instance.md)|如果是在多伺服器解決方案中模擬或委派使用者識別的服務，Kerberos 驗證就需要有效的服務主要名稱 (SPN)。 請透過本主題中的資訊了解 SPN 的建構以及為 Analysis Services 註冊 SPN 的步驟。|  
|[設定 HTTP 存取 Analysis Services 上 Internet Information Services &#40; IIS &#41;8.0](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md)|在設定可透過 HTTP 存取 Analysis Services 時，基本驗證或跨網域界限是兩個很重要的因素。|  
|[用於 Analysis Services 連接的資料提供者](../../analysis-services/instances/data-providers-used-for-analysis-services-connections.md)|Analysis Services 提供三套用於存取伺服器作業或 Analysis Services 資料的用戶端程式庫。 本主題簡單介紹 ADOMD.NET、Analysis Services 管理物件 (AMO) 和 Analysis Services OLE DB 提供者 (MSOLAP)。|  
|[中斷連接使用者和 Analysis Services 伺服器上的工作階段](../../analysis-services/instances/disconnect-users-and-sessions-on-analysis-services-server.md)|讓伺服器離線或執行基準效能測試之前，請清除現有的連接和工作階段。|  
  
## <a name="see-also"></a>另請參閱  
 [後續安裝組態 &#40;Analysis Services &#41;](../../analysis-services/instances/post-install-configuration-analysis-services.md)   
 [Analysis Services 的伺服器屬性](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
  
  
