---
title: 啟動與停止報表伺服器服務 | Microsoft Docs
description: 了解如何啟動和停止 Windows 服務，其中包含報表伺服器 Web 服務、入口網站，以及背景處理應用程式。
ms.date: 05/21/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- stopping Report Server service
- Report Server Windows service, starting
- Report Server service, starting
- starting Report Server service
ms.assetid: 6ec69ac3-27b0-472d-91e1-733af9078ed2
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b7f60e735ecd2483f8f105666ee181cb48eaa98b
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/13/2020
ms.locfileid: "91987504"
---
# <a name="start-and-stop-the-report-server-service"></a>啟動與停止報表伺服器服務

  報表伺服器會實作為 Windows 服務，其中包含報表伺服器 Web 服務、入口網站，以及幕後處理應用程式。 如果您想要使用任何報表伺服器功能，就必須執行這項服務。 停止此服務會停止所有報表伺服器作業。  
  
 當此服務停止時，原本在服務執行時會進行之排程報表和訂閱處理的要求都會加入至佇列。 這是因為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 所執行的作業會建立事件。 如果您想要在此服務關閉時避免作業積存，請考慮一併停止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent。  
  
 您可以使用各種工具來啟動或停止報表伺服器服務，包括 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 中提供的「服務」工具。  
  
 如果您執行的不只是啟動或停止服務 (例如變更服務帳戶)，則必須使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具。 使用其他工具來變更服務帳戶可能會破壞您的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安裝。 如需詳細資訊，請參閱[設定報表伺服器服務帳戶 &#40;報表伺服器組態管理員&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)。  
  
 您無法暫停並繼續服務。 目前沒有提供啟動參數。 雖然沒有明確的相依性，但是如果您的報表伺服器支援任何訂閱或排程的報表作業，就必須執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent。  
  
## <a name="use-the-reporting-services-configuration-tool"></a>使用 Reporting Services 組態工具  
  
1. 啟動 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具，並連接到報表伺服器。  
  
2. 在報表伺服器 [狀態] 頁面上，選取 [停止] 或 [啟動]。  
  
## <a name="use-administrative-tools"></a>使用系統管理工具  

- 在 [系統管理工具] 中，開啟 [服務]，以滑鼠右鍵按一下 [SQL Server Reporting Services (MSSQLSERVER)]，然後選取 [停止] 或 [重新啟動]。  
  
- 如果您執行多個執行個體，或者報表伺服器是以具名執行個體的形式執行，請確認括號中的執行個體名稱是否對應於您要停止或重新啟動的報表伺服器執行個體。  
  
## <a name="see-also"></a>另請參閱  
 [報表伺服器組態管理員 &#40;原生模式&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)   
 [啟動、停止或暫停 SQL Server Agent 服務](../../ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md)  
  
