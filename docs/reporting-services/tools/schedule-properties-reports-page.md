---
title: 排程屬性 (報表頁面) | Microsoft Docs
description: 了解 SQL Server Management Studio 中，列出特定共用排程所有報表的 [Reporting Services 排程屬性] 頁面。
ms.date: 06/30/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: tools
ms.topic: conceptual
f1_keywords:
- sql13.swb.reportserver.scheduleproperties.reports.f1
ms.assetid: 7db728bd-4b08-43ef-a49a-e8dcdd37cf89
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: ad2720898bc340d71644356b0ced7a4b8d647a5a
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/13/2020
ms.locfileid: "91988120"
---
# <a name="schedule-properties-reports-page"></a>排程屬性 (報表頁面)
  使用 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 中的 [ [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] 排程屬性] 頁面來檢視使用特定共用排程的所有報表清單。 排程可用來重新整理報表快照集、產生報表記錄、觸發訂閱或使報表的快取副本過期。 若要了解如何使用排程，請檢視報表的屬性和訂閱資訊。  
  
 雖然這個頁面會顯示使用此共用排程的每份報表，但是它不會指出在該單一報表內使用此共用排程的次數。 例如，假設 Company Sales 報表的 20 位不同訂閱者都使用相同的共用排程來觸發訂閱處理。 在此情況下，Company Sales 報表只會在此清單中顯示一次，即使報表具有共用排程的 20 個參考也一樣。  
  
 開啟 [排程屬性] 頁面：
 1. 啟動 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。
 2. 連接到報表伺服器。
 3. 開啟 [共用排程] 資料夾。
 4. 以滑鼠右鍵按一下共用的排程，然後選取 [屬性]。
 5. 按一下 [報表]。  
  
  您也可以從 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 入口網站的 [網站設定] 管理共用的排程。
  
> [!NOTE]  
>  並非所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本都提供此功能。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本支援的功能清單，請參閱 [SQL Server 2017 的版本及支援的功能](../../sql-server/editions-and-components-of-sql-server-2017.md)。  
  
## <a name="options"></a>選項。  
 **資料夾**  
 指定報表的路徑。  
  
 **Report**  
 指定使用排程之報表的名稱。  
  
## <a name="see-also"></a>另請參閱  
 [建立、修改和刪除共用排程](../../reporting-services/subscriptions/create-modify-and-delete-schedules.md)   
 [[排程]](../../reporting-services/subscriptions/schedules.md)   
 [Management Studio F1 說明中的報表伺服器](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
 [連接至 Management Studio 中的報表伺服器](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [設定報表的一般屬性 (報表管理員)](../reports/configure-execution-properties-for-a-report-report-manager.md)  
  
