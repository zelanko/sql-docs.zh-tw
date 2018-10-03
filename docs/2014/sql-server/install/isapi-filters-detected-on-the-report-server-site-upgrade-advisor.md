---
title: 偵測到報表伺服器站台 (Upgrade Advisor) 上的 ISAPI 篩選器 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- ISAPI filters
- report servers [Reporting Services], upgrade issues
ms.assetid: dd30560d-9e16-47c7-ba68-a9743a657e4e
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 7b30b585fc0448f04be2ee98c23f53794675fefe
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48192208"
---
# <a name="isapi-filters-detected-on-the-report-server-site-upgrade-advisor"></a>在報表伺服器站台上偵測到 ISAPI 篩選器 (Upgrade Advisor)
  Upgrade Advisor 在主控報表伺服器和報表管理員虛擬目錄的網站上偵測到一個或多個 ISAPI 篩選器。 中不支援 ISAPI 篩選器[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 原生。|  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>描述  
 升級之前，請確認網站上的 ISAPI 篩選器是否由 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 應用程式所使用。 如果您不需要 ISAPI 篩選器，就可以升級報表伺服器。 安裝程式將建立預設 URL，但不支援在 IIS 中執行的 ISAPI 篩選器。 如果您需要 ISAPI 篩選器，在您找到主控 ISAPI 篩選器的替代方式 (例如，使用 ISA Server 或繼續在 IIS 中主控 ISAPI 篩選器) 以前，請勿進行升級。 在特定狀況中，報表伺服器支援 ASP.NET HTTPModules 當做 ISAPI 篩選器的取代項目。 如需詳細資訊，請參閱 MSDN 上的 ASP.NET 文件集。  
  
## <a name="corrective-action"></a>更正動作  
 請評估並使用不同的解決方案來主控部署所需要的 ISAPI 篩選器。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 升級問題&#40;Upgrade Advisor&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
