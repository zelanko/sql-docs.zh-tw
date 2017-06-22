---
title: "啟動和停止報表伺服器服務 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- stopping Report Server service
- Report Server Windows service, starting
- Report Server service, starting
- starting Report Server service
ms.assetid: 6ec69ac3-27b0-472d-91e1-733af9078ed2
caps.latest.revision: 55
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 90106293e319e53c8fcbfe772c119f5c6a0f20c2
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="start-and-stop-the-report-server-service"></a>啟動與停止 Report Server 服務
  報表伺服器會實作成一項 Windows 服務，其中包含報表伺服器 Web 服務、報表管理員和背景處理應用程式。 如果您想要使用任何報表伺服器功能，就必須執行這項服務。 停止此服務會停止所有報表伺服器作業。  
  
 當此服務停止時，原本在服務執行時會進行之排程報表和訂閱處理的要求都會加入至佇列。 這是因為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 所執行的作業會建立事件。 如果您想要在此服務關閉時避免作業積存，請考慮一併停止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent。  
  
 您可以使用各種工具來啟動或停止報表伺服器服務，包括 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 中提供的「服務」工具。  
  
 如果您執行的不只是啟動或停止服務，例如變更服務帳戶，則必須使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具。 使用其他工具來變更服務帳戶可能會破壞您的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安裝。 如需詳細資訊，請參閱[設定報表伺服器服務帳戶 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)。  
  
 您無法暫停和繼續服務。 沒有啟動參數。 雖然沒有明確的相依性，但是如果您的報表伺服器支援任何訂閱或排程的報表作業，就必須執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent。  
  
### <a name="to-start-or-stop-the-service-using-the-reporting-services-configuration-tool"></a>使用 Reporting Services 組態工具來啟動或停止服務  
  
1.  啟動 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具，並連接到報表伺服器。  
  
2.  在 [報表伺服器狀態] 頁面上，按一下 **[停止]** 或 **[啟動]**。  
  
### <a name="to-start-or-stop-the-service-using-services-in-administrative-tools"></a>使用系統管理工具中的服務來啟動或停止服務  
  
-   在 [系統管理工具] 中開啟 [服務]、以滑鼠右鍵按一下 **[SQL Server Reporting Services (MSSQLSERVER)]**，然後按一下 **[停止]** 或 **[重新啟動]**。  
  
 如果您執行多個執行個體，或者報表伺服器是以具名執行個體執行，請確認括號中的執行個體名稱是否對應於您要停止或重新啟動的報表伺服器執行個體。  
  
### <a name="to-start-or-stop-the-service-using-sql-server-configuration-manager"></a>使用 SQL Server 組態管理員來啟動或停止服務  
  
1.  啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員。  
  
2.  選取 [SQL Server 服務]，並以滑鼠右鍵按一下 [SQL Server Reporting Services]，然後按一下 [停止] 或 [重新啟動]。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 組態管理員 &#40;原生模式&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)   
 [啟動、停止或暫停 SQL Server Agent 服務](http://msdn.microsoft.com/library/c95a9759-dd30-4ab6-9ab0-087bb3bfb97c)  
  
  
