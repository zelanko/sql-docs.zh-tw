---
title: 互通性與共存性 (Integration Services) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- interoperability and coexistence [Integration Services]
- Integration Services, interoperability and coexistence
ms.assetid: edfbcd56-012f-462e-a542-95491394fda9
caps.latest.revision: 34
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8f7face1f41fdf02f772c05427db9d45d1bd6050
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37277584"
---
# <a name="interoperability-and-coexistence-integration-services"></a>互通性與共存性 (Integration Services)
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services (SSIS) 可以和 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Integration Services 與 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Integration Services 並存。  
  
## <a name="features-and-differences"></a>功能和差異  
 下表將列出最新與舊版 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 之間的某些差異。  
  
|功能|[!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)]|[!INCLUDE[ssISversion11](../../includes/ssisversion11-md.md)]|[!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)]|  
|-------------|-------------------------------|---------------------------------|---------------------------------|  
|開發環境|[SQL Server 2014 Data Tools – Business Intelligence for Visual Studio 2012 CTP 2](http://www.microsoft.com/download/details.aspx?id=40736)<br /><br /> [SQL Server 2014 Data Tools-Business Intelligence for Visual Studio 2013](http://www.microsoft.com/download/details.aspx?id=42313)|[SQL Server Data Tools for Visual Studio 2010](http://msdn.microsoft.com/library/hh500335\(v=vs.103\).aspx)<br /><br /> [SQL Server Data Tools – Business Intelligence for Visual Studio 2012](http://www.microsoft.com/download/details.aspx?id=36843)|Business Intelligence Development Studio ([!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsOrcas](../../includes/vsorcas-md.md)])|  
|管理環境|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]|  
|msdb 中用來儲存封裝的主要系統資料表|sysssispackages|sysssispackages|sysssispackages|  
|用來執行封裝的主要命令提示字元公用程式|**dtexec** (dtexec.exe)，2014 版|**dtexec** (dtexec.exe)，2012 版|**dtexec** (dtexec.exe)，2008 版|  
|預設的根目錄檔案系統資料夾|C:\Program Files\Microsoft SQL Server\120\DTS|C:\Program Files\Microsoft SQL Server\110\DTS|C:\Program Files\Microsoft SQL Server\100\DTS|  
|預設的根登錄機碼|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\SSIS|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\SSIS|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\SSIS|  
  
## <a name="side-by-side-compatibility-issues"></a>並存相容性問題  
 當您的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services 安裝與 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Integration Services 和 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Integration Services 並存時，可以執行下列工作：  
  
-   **在 SQL Server 資料工具中設計封裝**： 您將使用下列工具開發及維護以相對應之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本為基礎的封裝。  
  
    -   使用 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 版的 Business Intelligence Development Studio，開發與維護以 [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] 為基礎的封裝。  
  
    -   使用[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]新版[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]來開發和維護封裝為基礎的[!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)]。  
  
    -   使用[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]新版[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]來開發和維護封裝為基礎的[!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)]。  
  
-   **載入與執行封裝**： 您可以載入和執行中開發的封裝[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]並[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]，請在[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]新版[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]。 當您將封裝加入現有的專案時，封裝就會永久升級為 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services 使用的格式。 當您在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中開啟封裝檔案時，該封裝會暫時升級為 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services 使用的格式。 如果您將變更儲存至封裝，封裝就會永久升級。 一次儲存格式， [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services 使用，不會再對應中開啟封裝[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]或是[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]版本的 Business Intelligence Development Studio 或由相對應的執行[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]Integration Services 或[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]Integration Services 工具。  
  
-   **在 SQL Server Management Studio 中管理封裝**。 您無法連接到的執行個體[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]版[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]服務，從[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]或[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]版本[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]。 您無法連接到的執行個體[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]或[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]新版[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]服務[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]版本[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]。 您可以使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 版本，管理儲存於 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 或 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 執行個體中的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 封裝。 您必須修改服務設定檔，才可將 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 執行個體加入此服務所管理的位置清單。 如需詳細資訊，請參閱[設定 Integration Services 服務 &#40;SSIS 服務&#41;](../service/integration-services-service-ssis-service.md)。  
  
-   **在 SQL Server 中儲存封裝**。 您可以將封裝儲存在下列資料庫中。  
  
    |封裝格式|[資料庫]|  
    |--------------------|--------------|  
    |[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Integration Services|執行個體的 msdb 資料庫 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|  
    |[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Integration Services|執行個體的 msdb 資料庫 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|  
    |[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services|執行個體的 msdb 資料庫 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|  
  
     執行個體上[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，您可以將封裝匯入的執行個體[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]或執行個體的[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]，但您無法將封裝匯出到的執行個體[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]或執行個體[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]。  
  
     在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 或 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 的執行個體上，您無法從 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的執行個體匯入封裝，或從其中匯出封裝。  
  
-   **執行封裝**。 您可以執行[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]Integration Services 和[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]使用 Integration Services 封裝[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]新版**dtexec**公用程式或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理程式。 每當[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]Integration Services 工具載入封裝中所開發[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]或是[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]，此工具暫時轉換，在記憶體中，要封裝的封裝格式[!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)]使用。 如果[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]或是[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]封裝發生無法成功轉換，問題[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]Integration Services 工具，解決這些問題之前將無法執行封裝。 如需詳細資訊，請參閱 [Upgrade Integration Services Packages](upgrade-integration-services-packages.md)。  
  
  
