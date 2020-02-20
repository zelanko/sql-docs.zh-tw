---
title: SQL Server Reporting Services 的高可用性 | Microsoft Docs
ms.date: 10/05/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-sharepoint
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 3c9f44a580ef8207c58ec86ed9df668590266e1f
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "65579915"
---
# <a name="high-availability-in-sql-server-reporting-services"></a>SQL Server Reporting Services 的高可用性

[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器是無狀態伺服器，它會將應用程式資料、內容、屬性和工作階段資訊儲存在兩個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 關聯式資料庫中。 因此，確保 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 功能可用性的最佳方式是進行下列作業：  
  
-   使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的高可用性功能，盡可能增加報表伺服器資料庫的執行時間。 如果您將 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體設定為在容錯移轉叢集中執行，就可以在建立報表伺服器資料庫時選取該執行個體。  
  
-   請盡可能使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 來搭配 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 資料庫和資料來源。 如需詳細資訊，請參閱 [Reporting Services 與 AlwaysOn 可用性群組](../../database-engine/availability-groups/windows/reporting-services-with-always-on-availability-groups-sql-server.md)。  
  
-   將多個報表伺服器設定為在向外延展部署中執行，其中所有伺服器都會共用單一報表伺服器資料庫。 將多個報表伺服器執行個體 (最好位於不同的伺服器上) 部署在向外延展部署中，有助於在其中一個報表伺服器執行個體無法使用時，提供不中斷的服務。  
  
 向外延展部署會提供一種共用資料庫的方式。 如果其中一個報表伺服器無法使用，相同部署中的其他伺服器將繼續運作。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 無法識別叢集。 向外延展部署本身不會提供負載平衡。它不會偵測報表伺服器的處理負載，也不會將新的處理要求路由傳送至最不忙碌的伺服器。 此外，它不會重新路由傳送完成之前失敗的處理要求。 若要取得負載平衡功能，您必須針對主控報表伺服器的 Web 伺服器設定負載平衡，然後設定向外延展部署中的報表伺服器，讓它們共用相同的報表伺服器資料庫。  
  
 報表伺服器 Web 服務與 Windows 服務會緊密整合而且一起當做單一報表伺服器執行個體執行。 您無法個別針對其中一項服務設定可用性。  

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](https://go.microsoft.com/fwlink/?LinkId=620231)
