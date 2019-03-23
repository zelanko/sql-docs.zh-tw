---
title: 互通性與共存性 (Integration Services) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- interoperability and coexistence [Integration Services]
- Integration Services, interoperability and coexistence
ms.assetid: edfbcd56-012f-462e-a542-95491394fda9
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 5552780cdc4a2f4e3faf39b9111882fcf4ffdd63
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/22/2019
ms.locfileid: "58380116"
---
# <a name="interoperability-and-coexistence-integration-services"></a>互通性與共存性 (Integration Services)
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services (SSIS) 可以和 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Integration Services 與 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Integration Services 並存。  
  
## <a name="features-and-differences"></a>功能和差異  
 下表將列出最新與舊版 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]之間的某些差異。  
  
|功能|[!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)]|[!INCLUDE[ssISversion11](../../includes/ssisversion11-md.md)]|[!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)]|  
|-------------|-------------------------------|---------------------------------|---------------------------------|  
|開發環境|[SQL Server 2014 Data Tools-Business Intelligence for Visual Studio 2012 CTP 2](https://www.microsoft.com/download/details.aspx?id=40736)<br /><br /> [SQL Server 2014 Data Tools-Business Intelligence for Visual Studio 2013](https://www.microsoft.com/download/details.aspx?id=42313)|[SQL Server Data Tools for Visual Studio 2010](https://msdn.microsoft.com/library/hh500335\(v=vs.103\).aspx)<br /><br /> [SQL Server Data Tools-Business Intelligence for Visual Studio 2012](https://www.microsoft.com/download/details.aspx?id=36843)|Business Intelligence Development Studio ([!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsOrcas](../../includes/vsorcas-md.md)])|  
|管理環境|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]|  
|msdb 中用來儲存封裝的主要系統資料表|sysssispackages|sysssispackages|sysssispackages|  
|用來執行封裝的主要命令提示字元公用程式|**dtexec** (dtexec.exe)，2014 版|**dtexec** (dtexec.exe)，2012 版|**dtexec** (dtexec.exe)，2008 版|  
|預設的根目錄檔案系統資料夾|C:\Program Files\Microsoft SQL Server\120\DTS|C:\Program Files\Microsoft SQL Server\110\DTS|C:\Program Files\Microsoft SQL Server\100\DTS|  
|預設的根登錄機碼|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\SSIS|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\SSIS|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\SSIS|  
  
## <a name="side-by-side-compatibility-issues"></a>並存相容性問題  
 當您的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services 安裝與 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Integration Services 和 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Integration Services 並存時，可以執行下列工作：  
  
-   **在 SQL Server 資料工具中設計封裝**： 您將使用下列工具開發及維護以相對應之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本為基礎的封裝。  
  
    -   使用 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 版的 Business Intelligence Development Studio，開發與維護以 [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] 為基礎的封裝。  
  
    -   使用 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 版的 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] ，開發與維護以 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)]為基礎的封裝。  
  
    -   使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 版的 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] ，開發與維護以 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)]為基礎的封裝。  
  
-   **載入與執行封裝**： 您可以在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 的 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]版本中，載入與執行在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 和 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中開發的封裝。 當您將封裝加入現有的專案時，封裝就會永久升級為 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services 使用的格式。 當您在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中開啟封裝檔案時，該封裝會暫時升級為 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services 使用的格式。 如果您將變更儲存至封裝，封裝就會永久升級。 這些封裝儲存為 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services 所使用的格式之後，就無法在對應之 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 或 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 版的 Business Intelligence Development Studio 中開啟，也無法由相對應的 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Integration Services 或 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Integration Services 工具執行。  
  
-   **在 SQL Server Management Studio 中管理封裝**。 您無法從 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 或 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 版本，連接至 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 服務的 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]版本之執行個體。 您無法從 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 的 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 版本，連接至 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]版本之執行個體。 您可以使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 版本，管理儲存於 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 或 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 執行個體中的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]封裝。 您必須修改服務設定檔，才可將 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 執行個體加入此服務所管理的位置清單。 如需詳細資訊，請參閱 [設定 Integration Services 服務 &#40;SSIS 服務&#41;](../service/integration-services-service-ssis-service.md)回溯相容。  
  
-   **在 SQL Server 中儲存封裝**。 您可以將封裝儲存在下列資料庫中。  
  
    |封裝格式|[資料庫]|  
    |--------------------|--------------|  
    |[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Integration Services|執行個體的 msdb 資料庫 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|  
    |[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Integration Services|執行個體的 msdb 資料庫 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|  
    |[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services|執行個體的 msdb 資料庫 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|  
  
     在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]的執行個體上，雖然您可以從 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 的執行個體或從 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]的執行個體匯入封裝，但是無法將封裝匯出至 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 的執行個體或是 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]的執行個體。  
  
     在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 或 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]的執行個體上，您無法從 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]的執行個體匯入封裝，或從其中匯出封裝。  
  
-   **執行封裝**。 您可以使用 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Integration Services 與 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 公用程式或 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的 **dtexec** Integration Services 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Integration Services 封裝。 每當 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services 工具載入在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 或 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]中開發的封裝時，此工具就會暫時在記憶體中將該封裝轉換成 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 所使用的封裝格式。 如果 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 或 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 封裝發生無法成功轉換的問題，在解決這些問題之前， [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services 工具將無法執行此封裝。 如需詳細資訊，請參閱 [Upgrade Integration Services Packages](upgrade-integration-services-packages.md)。  
  
  
