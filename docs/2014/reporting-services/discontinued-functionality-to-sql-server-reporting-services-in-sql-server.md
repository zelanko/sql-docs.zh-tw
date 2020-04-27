---
title: 已停止的功能
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.prod_service: reporting-services-native, reporting-services-sharepoint
ms.topic: conceptual
ms.custom: seodec18
ms.date: 12/14/2018
ms.openlocfilehash: 14a5a6e38d4c9fcf306436374d80dd1c1c08b27e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "67413047"
---
# <a name="discontinued-functionality-in-sql-server-reporting-services-ssrs"></a>SQL Server Reporting Services (SSRS) 中已中止的功能

  本主題描述 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 中不再可用的 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]功能。 其中不包含有關停止支援特定版本之作業系統或 [!INCLUDE[msCoName](../includes/msconame-md.md)] Internet Information Services (IIS) 的宣告。 如需系統必要條件的詳細資訊，請參閱[安裝 SQL Server 2014 的硬體和軟體需求](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)。  
  
 本主題內容：  
  
- [SQL Server 2014 Reporting Services 已停止的功能](#bkmk_sql14)  
  
- [SQL Server 2012 Reporting Services 已停止的功能](#bkmk_rc0)  
  
- [SQL Server 2008 R2 Reporting Services 已停止的功能](#bkmk_kj)  
  
##  <a name="sssql14-reporting-services-discontinued-functionality"></a><a name="bkmk_sql14"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] Reporting Services 已停止的功能

 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 中未停止任何 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]功能。  
  
##  <a name="sssql11-reporting-services-discontinued-functionality"></a><a name="bkmk_rc0"></a>[!INCLUDE[ssSQL11](../includes/sssql11-md.md)] Reporting Services 已停止的功能

 本節描述 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 中已停止的 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]功能。  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 中未停止任何 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]功能。  
  
##  <a name="sql-server-2008-r2-reporting-services-discontinued-functionality"></a><a name="bkmk_kj"></a>SQL Server 2008 R2 Reporting Services 已停止的功能

 本節描述中已停止[!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]的。  
  
> [!NOTE]  
> 因為 SQL Server 2008 R2 是 SQL Server 2008 的次要版本更新，所以建議您也檢閱 SQL Server 2008 章節中的內容。
  
### <a name="64-bit-platform-support"></a>64 位元平台支援

 從 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 開始，[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 元件不再支援執行 Windows Server 2003 或 Windows Server 2003 R2 的以 Itanium 為基礎的伺服器。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 繼續支援其他 64 位元作業系統，包括以 Itanium 為基礎系統的 Windows Server 2008 和 Windows Server 2008 R2。 若要從 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 安裝升級為 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]，而此安裝所含 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 是在以 Itanium 為基礎系統版本 Windows Server 2003 或 Windows Server 2003 R2 上，則必須先升級作業系統。  
  
### <a name="data-source-credentials-in-url-access"></a>URL 存取中的資料來源認證

 URL 存取參數字串 [ *dsu：值 =* ] 和 [ *dsp：值 =* ] 現在已停用。 在舊版中，這些參數字串會以純文字儲存在瀏覽器快取中，但這並不安全。  
  
## <a name="next-steps"></a>後續步驟

 - [Reporting Services 的新 &#40;&#41;](what-s-new-reporting-services.md)
 - [SQL Server 2014 中 SQL Server Reporting Services 的行為變更](behavior-changes-to-sql-server-reporting-services-in-sql-server-2016.md)
 - [SQL Server 2014 中已淘汰的 SQL Server Reporting Services 功能](deprecated-features-in-sql-server-reporting-services-ssrs.md)