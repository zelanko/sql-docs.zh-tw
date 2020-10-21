---
title: 報表伺服器 Windows 服務 (MSSQLServer) 107 | Microsoft Docs
description: 在此錯誤參考頁面中，了解事件識別碼 107：報表伺服器 Windows 服務 (SQL Server) 無法連線到報表伺服器資料庫。
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: troubleshooting
ms.topic: conceptual
helpviewer_keywords:
- MSSQLServer 107 error
ms.assetid: 52b5704b-27f9-400a-a821-d8fa0786afe4
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 4e68ffa14bfe98bc55e5424abe0dbdac944950a1
ms.sourcegitcommit: fe59f8dc27fd633f5dfce54519d6f5dcea577f56
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/09/2020
ms.locfileid: "91933705"
---
# <a name="report-server-windows-service-mssqlserver-107"></a>報表伺服器 Windows 服務 (MSSQLServer) 107
    
## <a name="details"></a>詳細資料  
  
|類別|值|  
|-|-|  
|產品名稱|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|事件識別碼|107|  
|事件來源|報表伺服器 Windows 服務|  
|元件|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
|訊息文字|報表伺服器 Windows 服務 (MSSQLSERVER) 無法連接到報表伺服器資料庫。|  
  
## <a name="explanation"></a>說明  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 報表伺服器服務無法連接到報表伺服器資料庫。 如果無法建立與報表伺服器資料庫的連接，將會在服務重新啟動期間發生此錯誤。 發生此錯誤的條件如下：  
  
-   當報表伺服器服務啟動時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 服務並未執行。  
  
-   由於遠端連接或 TCP/IP 通訊協定未啟用，而導致 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 服務的連接失敗。  
  
-   未正確設定報表伺服器資料庫。  
  
-   此服務帳戶未正確設定，或是此帳戶不再有報表伺服器資料庫的權限。 如果您並未使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具來設定此帳戶或報表伺服器資料庫，則可能會發生這個狀況。  
  
## <a name="user-action"></a>使用者動作  
 如果 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 服務不在執行中則啟動它，並檢查是否已針對 TCP/IP 通訊協定啟用遠端連接。  
  
 使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具來設定報表伺服器資料庫和服務帳戶。  
  
## <a name="internal-only"></a>僅供內部使用  
  
## <a name="see-also"></a>另請參閱  

 [設定報表伺服器服務帳戶 &#40;報表伺服器組態管理員&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [報表伺服器組態管理員 &#40;原生模式&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)   

 [啟動與停止報表伺服器服務](../../reporting-services/report-server/start-and-stop-the-report-server-service.md)  
  
  
