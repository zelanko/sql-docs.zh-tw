---
title: SQL Server 2014 中已淘汰的 Master Data Services 功能 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: d8506bda-66dd-45a4-bfc9-3a10fa665acc
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: dd6342542da7528fef633ba02a430a8ba2ef5857
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "65483058"
---
# <a name="deprecated-master-data-services-features-in-sql-server-2014"></a>SQL Server 2014 中已被取代的 Master Data Services 功能
  本主題描述 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 中仍然可用但已被取代的 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]功能。 這些功能將在未來的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]版本中移除。 已被取代的功能不應在新應用程式中使用。  
  
## <a name="staging-process"></a>暫存處理序  
 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] Web 應用程式中不再提供 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 中所使用的暫存處理序，不過仍可在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 使用。  
  
 來自 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 暫存處理序的暫存錯誤不再顯示在使用者介面中。 在暫存進程期間填入的錯誤碼仍可在臨時表中使用，您可以在這裡找到： [https://msdn.microsoft.com/library/ff487022.aspx](https://msdn.microsoft.com/library/ff487022.aspx)。  
  
 暫存資料表 (tblStgMember、tblStgMemberAttribute 及 tblStgRelationship) 仍在資料庫中。 用來起始暫存處理序 (mdm.udpStagingSweep) 的預存程序仍在資料庫中。  
  
 仍可使用呼叫暫存處理序的 Web 服務方法。  
  
 在 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]中設定的暫存間隔會套用至 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 和 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 中的暫存處理序。  
  
  中已實作新的、效能更高的暫存處理序。 如需詳細資訊，請參閱[資料匯入 &#40;Master Data Services&#41;](overview-importing-data-from-tables-master-data-services.md)。  
  
## <a name="metadata"></a>中繼資料  
 雖然中繼資料模型仍然顯示在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 應用程式中，不過您不應該使用它。 未來的版本將予以移除。 使用者也不能再于 [ **Explorer** ] 功能區域中查看中繼資料，而且您也無法再建立元資料模型的版本。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 2014 中已停止的 Master Data Services 功能](discontinued-master-data-services-features.md)  
  
  
