---
title: 高可用性 (Reporting Services) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- high availability [SQL Server], Reporting Services
- high availability [Reporting Services]
- Reporting Services, high availability
ms.assetid: 50e0813f-f591-4688-9cd1-e6389a3808e5
caps.latest.revision: 15
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 0884a284e6d9169ce978d3c47330a683e2bb6b52
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37150219"
---
# <a name="high-availability-reporting-services"></a>高可用性 (Reporting Services)
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 報表伺服器是無狀態伺服器，它會將應用程式資料、內容、屬性和工作階段資訊儲存在兩個 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 關聯式資料庫中。 因此，若要確保的可用性，最好[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]功能會執行下列動作：  
  
-   使用的高可用性功能[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssDE](../includes/ssde-md.md)]盡可能增加報表伺服器資料庫的執行時間。 如果您設定[!INCLUDE[ssDE](../includes/ssde-md.md)]執行容錯移轉叢集執行個體，當您建立報表伺服器資料庫時，您可以選取該執行個體。  
  
-   請盡可能使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssHADR](../includes/sshadr-md.md)] 搭配 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 資料庫和資料來源。 如需詳細資訊，請參閱 [Reporting Services 與 AlwaysOn 可用性群組 &#40;SQL Server&#41;](../database-engine/availability-groups/windows/reporting-services-with-always-on-availability-groups-sql-server.md)。  
  
-   將多個報表伺服器設定為在向外延展部署中執行，其中所有伺服器都會共用單一報表伺服器資料庫。 將多個報表伺服器執行個體 (最好位於不同的伺服器上) 部署在向外延展部署中，有助於在其中一個報表伺服器執行個體無法使用時，提供不中斷的服務。  
  
 向外延展部署會提供一種共用資料庫的方式。 如果其中一個報表伺服器無法使用，相同部署中的其他伺服器將繼續運作。  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 無法識別叢集。 向外延展部署本身不會提供負載平衡。它不會偵測報表伺服器的處理負載，也不會將新的處理要求路由傳送至最不忙碌的伺服器。 此外，它不會重新路由傳送完成之前失敗的處理要求。 若要取得負載平衡功能，您必須針對主控報表伺服器的 Web 伺服器設定負載平衡，然後設定向外延展部署中的報表伺服器，讓它們共用相同的報表伺服器資料庫。  
  
 報表伺服器 Web 服務與 Windows 服務會緊密整合而且一起當做單一報表伺服器執行個體執行。 您無法個別針對其中一項服務設定可用性。  
  
## <a name="see-also"></a>另請參閱  
 [高可用性解決方案 &#40;SQL Server&#41;](../sql-server/failover-clusters/high-availability-solutions-sql-server.md)   
 [設定原生模式報表伺服器向外延展部署&#40;SSRS 組態管理員&#41;](install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)  
  
  
