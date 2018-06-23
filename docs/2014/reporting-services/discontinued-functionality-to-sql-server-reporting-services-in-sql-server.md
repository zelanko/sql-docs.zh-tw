---
title: 已停止的 SQL Server Reporting Services SQL Server 2014 中的功能 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- discontinued functionality [Reporting Services]
- Reporting Services, backward compatibility
- Rsactivate.exe
- unsupported features [Reporting Services]
ms.assetid: d529cc96-3483-480b-9bfc-bd28b1d0ef52
caps.latest.revision: 47
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: 627e8fe70de053c0cd53cc24c77438549c794e76
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36131659"
---
# <a name="discontinued-functionality-to-sql-server-reporting-services-in-sql-server-2014"></a>SQL Server 2014 中 SQL Server Reporting Services 已停止的功能
  本主題描述 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 中不再可用的 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]功能。 其中不包含有關停止支援特定版本之作業系統或 [!INCLUDE[msCoName](../includes/msconame-md.md)] Internet Information Services (IIS) 的宣告。 如需有關系統必要條件的詳細資訊，請參閱[硬體和軟體需求，安裝 SQL Server 2014](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)。  
  
 本主題內容：  
  
-   [SQL Server 2014 Reporting Services 已停止的功能](#bkmk_sql14)  
  
-   [SQL Server 2012 Reporting Services 已停止的功能](#bkmk_rc0)  
  
-   [SQL Server 2008 R2 Reporting Services 已停止的功能](#bkmk_kj)  
  
##  <a name="bkmk_sql14"></a> [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] Reporting Services 已停止的功能  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 中未停止任何 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 功能。  
  
##  <a name="bkmk_rc0"></a> [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] Reporting Services 已停止的功能  
 本節描述 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 中已停止的 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 功能。  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 中未停止任何 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 功能。  
  
##  <a name="bkmk_kj"></a> SQL Server 2008 R2 Reporting Services 已停止的功能  
 本章節描述中，停用[!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]。  
  
> [!NOTE]  
>  因為 SQL Server 2008 R2 是 SQL Server 2008 的次要版本更新，所以建議您也檢閱 SQL Server 2008 章節中的內容。  
  
### <a name="64-bit-platform-support"></a>64 位元平台支援  
 從開始[!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]、[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]元件不再支援執行 Windows Server 2003 或 Windows Server 2003 R2 的 Itanium 型伺服器。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 會繼續支援其他 64 位元作業系統，包括 Windows Server 2008 for Itanium-Based Systems 和 Windows Server 2008 R2 的 itanium 型系統。 若要從 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 安裝升級為 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]，而此安裝所含 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 是在以 Itanium 為基礎系統版本 Windows Server 2003 或 Windows Server 2003 R2 上，則必須先升級作業系統。  
  
### <a name="data-source-credentials-in-url-access"></a>URL 存取中的資料來源認證  
 URL 存取參數字串*dsu:datasourcename = value*和*dsp:datasourcename = value*現已停用。 在舊版中，這些參數字串會以純文字儲存在瀏覽器快取中，但這並不安全。  
  
## <a name="see-also"></a>另請參閱  
 [最新消息&#40;Reporting Services&#41;](what-s-new-reporting-services.md)   
 [SQL Server Reporting Services SQL Server 2014 中的行為變更](behavior-changes-to-sql-server-reporting-services-in-sql-server-2016.md)   
 [在 SQL Server Reporting Services SQL Server 2014 中已被取代的功能](deprecated-features-in-sql-server-reporting-services-ssrs.md)  
  
  